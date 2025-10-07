아주 예리하게 보셨습니다 — 이건 **보안적으로 매우 중요한 관찰**이에요.
요약부터 말씀드리면 👇

> 🔍 EC2 Instance Connect로 접속했는데 `~/.aws/credentials` 파일이 이미 존재한다면,
> **“누군가(또는 어떤 시스템)”이 그 인스턴스 안에 자격증명을 자동으로 주입했을 가능성**이 있습니다.

이건 **정상일 수도 있고, 심각한 보안 위험 신호일 수도 있습니다.**
아래에서 단계별로 정확히 판단하고 조치하는 법을 알려드릴게요.

---

## 🧭 1️⃣ 우선 사실관계부터 정리

EC2 Instance Connect는 기본적으로:

* **임시 SSH 세션만 열어주는 서비스**입니다.
* 연결 자체로는 AWS 자격증명(`~/.aws/credentials`)을 **주입하지 않습니다.**

즉,

> EC2 Instance Connect만으로는 credentials 파일이 생기지 않습니다.

---

## ⚠️ 2️⃣ 그럼 왜 생겼을까? 가능한 4가지 원인

| 원인                                                  | 설명                                                     | 위험도     |
| --------------------------------------------------- | ------------------------------------------------------ | ------- |
| 🟩 **(1) 인스턴스 프로필(IAM Role)**                       | EC2에 IAM Role이 연결되어 있으면, 내부적으로 STS 임시 자격증명을 발급받을 수 있음. | 낮음 (정상) |
| 🟨 **(2) 사용자가 직접 AWS CLI 설치 후 configure 한 적이 있음**   | 과거에 수동으로 입력된 적이 남아 있을 수 있음.                            | 중간      |
| 🟧 **(3) AMI 이미지 제작 시 이미 credential 파일이 포함됨**       | 다른 계정/환경에서 만든 이미지에 credential이 박혀 있었음.                 | 높음      |
| 🟥 **(4) 다른 사용자가 해당 인스턴스에 접근해서 credential을 생성/복사함** | 보안 침해 가능성. 즉시 조사 필요.                                   | 매우 높음   |

---

## 🧩 3️⃣ 우선 확인해야 할 핵심 명령어

### ✅ (1) 어떤 IAM Role이 연결되어 있는지 확인

```bash
curl -s http://169.254.169.254/latest/meta-data/iam/info
```

결과 예시:

```json
{
  "InstanceProfileArn" : "arn:aws:iam::123456789012:instance-profile/MyEC2Role",
  "InstanceProfileId" : "AIPAJU4DZX...",
  ...
}
```

* 만약 Role이 있다면 → AWS CLI가 **임시자격증명(STS)**을 자동으로 `/var/lib/aws/`나 `~/.aws/cli/cache` 등에 저장할 수 있습니다.
* 이건 **정상적인 동작**입니다.

---

### ✅ (2) 실제 자격증명 파일 내용 확인

```bash
cat ~/.aws/credentials
```

* 만약 내용이 이런 형태라면:

  ```
  [default]
  aws_access_key_id = ASIA...
  aws_secret_access_key = ...
  aws_session_token = ...
  ```

  → 이건 **임시 STS 세션 자격증명**으로, **EC2 IAM Role에서 자동 생성된 것**입니다.
  즉 **정상**입니다. (EC2 Instance Metadata Service에서 자동 제공됨)

* 반면 이런 형태라면:

  ```
  [default]
  aws_access_key_id = AKIA...
  aws_secret_access_key = ...
  ```

  즉 `AKIA`로 시작하는 **영구 자격증명**이면 → 사람이 수동으로 넣었거나 이미지에 포함된 겁니다.
  **즉시 삭제 필요.**

---

### ✅ (3) 파일 생성 시각 및 변경 시각 확인

```bash
ls -l --time=ctime ~/.aws/credentials
```

또는:

```bash
stat ~/.aws/credentials
```

→ “언제” 만들어졌는지 확인해서,
본인이 만든 시점과 맞지 않으면 의심해봐야 합니다.

---

## 🚨 4️⃣ 만약 영구 키(AKIA...)가 들어있다면

**즉시 아래 조치:**

1. **키 확인**

   ```bash
   cat ~/.aws/credentials
   ```

   → `aws_access_key_id` 복사

2. **AWS CLI (또는 콘솔)** 로 해당 키의 최근 사용 로그 조회:

   ```bash
   aws iam get-access-key-last-used --access-key-id <KEY_ID>
   ```

3. **루트 또는 IAM 콘솔에서 해당 키 즉시 비활성화 또는 삭제**

   ```bash
   aws iam update-access-key --access-key-id <KEY_ID> --status Inactive --user-name <USER>
   ```

   또는:

   ```bash
   aws iam delete-access-key --access-key-id <KEY_ID> --user-name <USER>
   ```

4. **해당 EC2 이미지(AMI) 재검토**

   * 혹시 이미 다른 곳에서 같은 이미지로 여러 인스턴스 띄운 적 있다면, 전부 점검해야 합니다.
   * **보안 사고 가능성**이 있기 때문입니다.

---

## ✅ 5️⃣ 만약 STS 세션 키(ASIA...)라면

→ 정상입니다.
EC2에 연결된 IAM Role을 통해 자동으로 임시키가 주입된 것입니다.
이 키는 몇 시간 후 자동 만료되며, EC2 내부 AWS CLI에서 AWS 자원을 제어할 때 사용됩니다.

**확인용 명령:**

```bash
aws sts get-caller-identity
```

예시 출력:

```
{
    "UserId": "AROA...:i-0abcd1234ef56789",
    "Account": "123456789012",
    "Arn": "arn:aws:sts::123456789012:assumed-role/MyEC2Role/i-0abcd1234ef56789"
}
```

→ 이렇게 나오면 완전 정상입니다.
(즉, EC2의 IAM Role “MyEC2Role”이 세션을 임시로 부여받은 것)

---

## 🧠 요약 정리

| 상황                               | 조치                                |
| -------------------------------- | --------------------------------- |
| `ASIA...` 로 시작                   | IAM Role에서 자동 주입된 STS 자격증명 → ✅ 정상 |
| `AKIA...` 로 시작                   | 사람이 입력 or 이미지에 포함 → 🚨 즉시 삭제      |
| 생성시간 의심 / 출처 불명                  | IAM / CloudTrail 로그 점검, 인스턴스 격리   |
| EC2 IAM Role 없음 + credentials 존재 | 거의 확실히 유출 또는 이미지 오염 가능성           |

---

## 🔐 추가 보안 강화 팁

1. **EC2 인스턴스에 Role 연결이 되어 있지 않다면**, 직접 키를 넣지 마세요.
   → 대신 Role을 만들어 EC2 Instance Profile로 연결.
2. **루트 계정 키 절대 사용 금지**
3. **AWS CLI 캐시 폴더 주기적 점검**
4. **CloudTrail 활성화 + GuardDuty 켜기**
5. **보안 이벤트 자동 알림 (SNS + CloudWatch)** 설정


좋아요, 결정을 내리기 전에 **이 파일이 무엇인지 정확히 확인하는 것이 먼저**입니다.
삭제 여부는 **내용과 출처**에 따라 달라집니다.

---

## 1️⃣ 먼저 확인할 것

```bash
cat ~/.aws/credentials
```

* **임시 STS 세션 키**인지 확인

  ```
  [default]
  aws_access_key_id = ASIA...
  aws_secret_access_key = ...
  aws_session_token = ...
  ```

  → `ASIA`로 시작하면 **EC2 IAM Role에서 자동으로 부여된 임시 키**입니다.
  이 경우 **삭제해도 문제가 없음**, 다만 **AWS CLI/SDK가 해당 Role을 사용해 자동으로 다시 가져올 수 있음**.

* **영구 키(Access Key ID)**인지 확인

  ```
  [default]
  aws_access_key_id = AKIA...
  aws_secret_access_key = ...
  ```

  → 사람이 넣은 키 또는 이미지에 포함된 키.
  **즉시 삭제 후 키 폐기 필요**. (보안 사고 예방)

---

## 2️⃣ 삭제 여부 판단

| 경우                  | 삭제 여부                                |
| ------------------- | ------------------------------------ |
| **임시 STS 키(ASIA…)** | 삭제 가능하지만 없어도 AWS CLI가 Role 통해 자동 발급  |
| **영구 키(AKIA…)**     | 반드시 삭제 + AWS 계정에서 키 비활성화/폐기          |
| **출처 불명 / 의심됨**     | 삭제 후 IAM Role 확인 및 CloudTrail 이벤트 점검 |

---

## 3️⃣ 삭제 명령

```bash
rm ~/.aws/credentials
```

> Linux / macOS / WSL
> Windows PowerShell:

```powershell
del $env:USERPROFILE\.aws\credentials
```

> 삭제 후 AWS CLI 사용 시 IAM Role이 연결된 EC2라면 **자동으로 STS 임시 자격증명을 가져와 사용 가능**합니다.

---

💡 **Tip**

* 삭제 후 CLI 실행 테스트:

```bash
aws sts get-caller-identity
```

→ Role이 정상 연결되어 있으면 여전히 AWS API 호출 가능
→ Role이 없거나 영구 키 필요 시 오류 발생

---

정리하면:

* **임시 키 → 삭제 가능, 안전**
* **영구 키 → 삭제 + AWS 키 폐기 필수**
* **불명 → 삭제 후 조사**
