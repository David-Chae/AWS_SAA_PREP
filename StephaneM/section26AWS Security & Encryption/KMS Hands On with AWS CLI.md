# KMS Hands On with AWS CLI  
# AWS CLI로 KMS 실습  
🎮 게임보상: AWS CLI 암호화/복호화 퀘스트 완료 시 +500 XP  

---

## Introduction to AWS KMS Service  
## AWS KMS 서비스 소개  

Let's have a look at the AWS Key Management Service (KMS). On the left-hand side, we can observe the AWS managed keys. If you have been using KMS encryption throughout this course, these keys will appear here.  
AWS 키 관리 서비스(KMS)를 살펴봅시다. 좌측에는 AWS 관리형 키가 보입니다. 지금까지 KMS 암호화를 사용해왔다면 여기에서 키들이 나타날 것입니다.  

For example, consider the AWS Elastic Block Store (EBS) key. This is an AWS managed key because it belongs to the EBS service. We can examine how it is being used.  
예를 들어 AWS Elastic Block Store(EBS) 키를 보겠습니다. 이 키는 EBS 서비스에 속하기 때문에 AWS 관리형 키입니다. 이를 어떻게 사용하는지 확인할 수 있습니다.  

---

## Key Policy Overview  
## 키 정책 개요  

There is a key policy associated with this key. This complex policy defines what can access the key. Since this is an EBS AWS key, all actions are allowed, but with conditions:  
이 키에는 키 정책이 연결되어 있습니다. 이 복잡한 정책은 누가 이 키에 접근할 수 있는지 정의합니다. 이 키는 EBS 키이므로 모든 작업이 허용되지만 조건이 있습니다:  

- The caller's account must be mine.  
  호출자의 계정이 내 계정이어야 합니다.  

- The "Via Service" must be the EC2 service, which is a service above the EBS service.  
  "Via Service"는 EC2 서비스여야 하며, 이는 EBS 위에 있는 서비스입니다.  

If we look at another AWS managed key, for example, the Simple Queue Service (SQS) key, the key policy specifies that the "Via Service" condition is the SQS service. This allows only access from SQS to this key.  
다른 AWS 관리형 키, 예를 들어 SQS(Simple Queue Service) 키를 보면, "Via Service" 조건이 SQS 서비스로 지정되어 있습니다. 이는 SQS를 통한 접근만 허용합니다.  

---

## Cryptographic Configuration  
## 암호화 설정  

The cryptographic configuration shows that this key is symmetric and originates from KMS. It is used to encrypt and decrypt data.  
암호화 설정에 따르면 이 키는 대칭 키이며 KMS에서 생성되었습니다. 데이터 암호화와 복호화에 사용됩니다.  

---

## Customer Managed Keys and Custom Key Store  
## 고객 관리형 키와 사용자 지정 키 저장소  

Apart from AWS managed keys, there are customer managed keys and custom key stores. The custom key store is used when we want to use CloudHSM, but this is out of scope for this exam. We will focus on customer managed keys, which are keys created by us within KMS instead of using AWS managed keys.  
AWS 관리형 키 외에도 고객 관리형 키와 사용자 지정 키 저장소가 있습니다. 사용자 지정 키 저장소는 CloudHSM을 사용하고 싶을 때 활용되지만, 이번 시험 범위에는 포함되지 않습니다. 우리는 AWS 관리형 키 대신 직접 생성하는 고객 관리형 키에 집중합니다.  

---

## Creating a Customer Managed Key  
## 고객 관리형 키 생성  

When creating a customer managed key, be aware that it costs $1 per month. If you want to avoid charges, do not create one.  
고객 관리형 키를 만들면 월 $1의 비용이 발생합니다. 요금을 피하려면 생성하지 마세요.  

For the key type, there are multiple options:  
키 유형에는 여러 옵션이 있습니다:  

- Symmetric key  
  대칭 키  

- Asymmetric key  
  비대칭 키  

Asymmetric keys can be used for encrypt and decrypt or sign and verify operations, but this is out of scope for this lecture. We will use the symmetric key type with encrypt and decrypt options, which is the most basic.  
비대칭 키는 암호화/복호화 또는 서명/검증에 사용되지만, 이번 강의에서는 범위에 포함되지 않습니다. 우리는 가장 기본적인 대칭 키를 사용합니다.  

---

## Advanced Options  
## 고급 옵션  

The key origin can be:  
키의 생성 출처는 다음과 같습니다:  

- KMS (default, where KMS creates the key)  
  KMS (기본값, KMS에서 키를 생성)  

- External (imported key)  
  외부 (가져온 키)  

- Custom key store (CloudHSM)  
  사용자 지정 키 저장소 (CloudHSM)  

We will use KMS as the key origin.  
우리는 기본 KMS를 사용합니다.  

For regionality, options are:  
리전성에 따른 옵션은 다음과 같습니다:  

- Single region key  
  단일 리전 키  

- Multi-region key  
  다중 리전 키  

We will consider the single region key, which is the oldest and most common option.  
우리는 가장 오래되고 흔한 단일 리전 키를 고려합니다.  

---

## Key Alias and Permissions  
## 키 별칭과 권한  

We assign a key alias, for example, "tutorial".  
우리는 키 별칭을 부여합니다. 예: "tutorial".  

Next, we define key administrators. If none are defined, the default KMS key policy applies.  
그다음 키 관리자를 정의합니다. 관리자를 정의하지 않으면 기본 KMS 키 정책이 적용됩니다.  

Then, we specify who can use the key. By default, everyone with the right IAM permissions can use it. For extra security, you could restrict usage to specific users, such as only Stefan.  
그 후 키를 사용할 수 있는 사람을 지정합니다. 기본적으로 IAM 권한이 있는 사람은 누구나 사용할 수 있습니다. 추가 보안을 위해 특정 사용자(예: Stefan만)로 제한할 수 있습니다.  

Additionally, you can allow other AWS accounts to access your key, useful for sharing encrypted snapshots like EBS snapshots.  
또한 다른 AWS 계정이 키에 접근할 수 있도록 허용할 수 있습니다. 이는 EBS 스냅샷 같은 암호화된 스냅샷을 공유할 때 유용합니다.  

---

## Summary of Key Creation  
## 키 생성 요약  

- Symmetric key  
  대칭 키  

- Default key policy enabling IAM user permissions  
  IAM 사용자 권한을 허용하는 기본 키 정책  

This allows any action on KMS resources as long as the user has the appropriate IAM permissions.  
이는 사용자가 올바른 IAM 권한을 가지고 있으면 KMS 리소스에서 모든 작업을 허용합니다.  

After finishing, the key is created and can be viewed. The key policy is essentially an IAM policy for the key. You can switch to a default view to see a summary of:  
생성이 끝나면 키가 생성되고 확인할 수 있습니다. 키 정책은 본질적으로 키에 대한 IAM 정책입니다. 기본 보기에서 요약을 확인할 수 있습니다:  

- Key administrators  
  키 관리자  

- Whether key deletion is allowed  
  키 삭제 허용 여부  

- Key users  
  키 사용자  

- Access by other accounts  
  다른 계정 접근  

---

## Additional Key Settings  
## 추가 키 설정  

- Cryptographic configuration (not modified here)  
  암호화 설정 (여기서는 수정하지 않음)  

- Tags (not needed)  
  태그 (불필요)  

- Key rotation: automatic key rotation can be enabled with a customizable rotation period from 90 days to 2,560 days (approximately 7 years).  
  키 회전: 자동 회전은 90일 ~ 2,560일(약 7년) 주기로 설정할 수 있습니다.  

You can also initiate on-demand key rotation. Rotation events appear in the key rotation history.  
필요 시 즉시 키 회전을 시작할 수도 있습니다. 회전 이벤트는 기록에 나타납니다.  

The key alias is "tutorial", which can be used to refer to the key with an alias ARN, simplifying references.  
키 별칭은 "tutorial"이며, 이는 ARN 별칭으로 참조를 단순화할 수 있습니다.  

Key actions include disabling the key or scheduling key deletion.  
키 작업에는 키 비활성화 또는 삭제 예약이 포함됩니다.  

---

## Using the AWS CLI to Encrypt and Decrypt Data with KMS  
## AWS CLI를 사용한 KMS 데이터 암호화 및 복호화  

We will now use the CLI to encrypt and decrypt some data using KMS. The script `kms-demo-cli.sh` demonstrates how to use the encrypt and decrypt commands with an example.  
이제 CLI를 사용해 데이터를 KMS로 암호화 및 복호화합니다. `kms-demo-cli.sh` 스크립트는 encrypt와 decrypt 명령 사용 예제를 보여줍니다.  

---

### Creating a Secret File  
### 비밀 파일 생성  

First, create a file named `ExampleSecretFile.txt` containing a secret password. For example:  
먼저 `ExampleSecretFile.txt` 파일을 만들고 비밀번호를 작성합니다. 예:  

```

SuperSecretPassword

```

This file can contain any text you want. We will encrypt and then decrypt this file using KMS.  
이 파일은 원하는 텍스트를 포함할 수 있습니다. 우리는 이 파일을 KMS로 암호화 후 복호화할 것입니다.  

---

### Encrypting the File Using KMS CLI  
### KMS CLI로 파일 암호화  

Use the encrypt command specifying:  
다음과 같이 encrypt 명령을 사용합니다:  

- The key ID (for example, alias/tutorial)  
  키 ID (예: alias/tutorial)  

- The plaintext file path (ExampleSecretFile.txt)  
  평문 파일 경로 (ExampleSecretFile.txt)  

- Output format as text  
  출력 형식: text  

- The AWS region where the key is located  
  키가 있는 AWS 리전  

This command outputs a base64-encoded ciphertext blob representing the encrypted content.  
이 명령은 암호화된 내용을 나타내는 base64 인코딩된 암호문 블롭을 출력합니다.  

---

### Base64 Decoding the Encrypted File  
### 암호화된 파일 Base64 디코딩  

After encryption, the output is saved as `ExampleSecretFileEncrypted.base64`. This file contains base64-encoded encrypted content.  
암호화 후 출력은 `ExampleSecretFileEncrypted.base64`로 저장됩니다. 이 파일에는 base64 인코딩된 암호화 데이터가 들어있습니다.  

To obtain the binary encrypted value, perform a base64 decode:  
이진 암호화 값을 얻으려면 base64 디코딩을 수행합니다:  

- On Linux/macOS, use `base64 --decode`  
  Linux/macOS: `base64 --decode`  

- On Windows, use the appropriate base64 decoding command  
  Windows: 적절한 base64 디코딩 명령 사용  

This produces a binary file `ExampleSecretFileEncrypted` which cannot be opened as text because it contains binary data.  
이 과정에서 `ExampleSecretFileEncrypted`라는 이진 파일이 생성되며, 이는 텍스트로 열 수 없습니다.  

---

### Decrypting the Encrypted File  
### 암호화된 파일 복호화  

To decrypt, use the decrypt command specifying:  
복호화를 위해 다음과 같이 decrypt 명령을 사용합니다:  

- The encrypted binary file  
  암호화된 이진 파일  

- Output as plaintext  
  출력: 평문  

- The AWS region  
  AWS 리전  

KMS automatically determines the key to use for decryption from the encrypted blob.  
KMS는 암호문 블롭에서 복호화에 사용할 키를 자동으로 결정합니다.  

The decrypted output is base64-encoded and saved to a file, for example, `ExampleFileDecrypted.base64`.  
복호화된 출력은 base64 형식으로 저장되며 예: `ExampleFileDecrypted.base64`.  

---

### Base64 Decoding the Decrypted File  
### 복호화된 파일 Base64 디코딩  

Perform a base64 decode on the decrypted base64 file to obtain the original plaintext file:  
복호화된 base64 파일을 디코딩해 원래 평문 파일을 얻습니다:  

Use the appropriate base64 decode command depending on your operating system.  
운영체제에 따라 적절한 base64 디코딩 명령을 사용하세요.  

After decoding, the original secret password is recovered in the plaintext file.  
디코딩 후 원래의 비밀번호가 평문 파일에서 복원됩니다.  

---

## Summary  
## 요약  

We have demonstrated the encryption and decryption process using AWS KMS customer managed keys via the CLI. Although these are low-level commands, SDKs abstract much of this complexity. This example shows how to use the encrypt and decrypt commands with your own customer master key.  
우리는 CLI를 통해 AWS KMS 고객 관리형 키로 암호화 및 복호화 과정을 시연했습니다. 이는 저수준 명령이지만, SDK는 이러한 복잡성을 추상화합니다. 이번 예제는 직접 생성한 고객 마스터 키로 encrypt/decrypt 명령을 사용하는 방법을 보여줍니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS KMS provides managed keys and allows creation of customer managed keys for encryption.  
  AWS KMS는 관리형 키를 제공하며, 고객 관리형 키 생성을 허용합니다.  

- Key policies define access permissions and conditions for KMS keys.  
  키 정책은 접근 권한과 조건을 정의합니다.  

- Customer managed keys can be symmetric or asymmetric, with options for key origin and regionality.  
  고객 관리형 키는 대칭 또는 비대칭일 수 있으며, 생성 출처와 리전성을 설정할 수 있습니다.  

- KMS CLI commands enable encryption and decryption of data using specified keys with base64 encoding and decoding.  
  KMS CLI 명령을 사용하면 지정된 키로 데이터 암호화 및 복호화를 수행하고 base64 인코딩/디코딩을 활용할 수 있습니다.  

🎮 게임보상: "KMS CLI 마스터" 업적 달성! +700 XP 🔑  
```
