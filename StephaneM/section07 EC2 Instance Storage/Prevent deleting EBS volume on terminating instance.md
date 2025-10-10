## 🧭 1. Background: What Happens by Default

When you launch an EC2 instance, the **root EBS volume** (the one attached at `/dev/xvda` or `/dev/sda1`) usually has:

```
DeleteOnTermination = true
```

That means — when you terminate the instance, **the root volume is automatically deleted**.

But this setting can be changed.

---

## ⚙️ 2. Option A — Change the Setting **Before Launch**

If you’re launching a new instance:

1. In the **EC2 console**, go to **Launch instance → Configure storage**.
2. For the root volume, uncheck the box:

   ```
   Delete on termination
   ```
3. Launch the instance normally.

Now, when you terminate that instance later, the root EBS volume will remain.

---

## 🪄 3. Option B — Change the Setting **After Instance Creation (Before Termination)**

If the instance already exists, you can modify this attribute **before terminating it**.

### Using AWS CLI

```bash
aws ec2 modify-instance-attribute \
    --instance-id i-0123456789abcdef0 \
    --block-device-mappings '[{"DeviceName":"/dev/xvda","Ebs":{"DeleteOnTermination":false}}]'
```

> Replace `/dev/xvda` with your actual root device name (check with `aws ec2 describe-instances`).

You can verify the change:

```bash
aws ec2 describe-instances --instance-id i-0123456789abcdef0 \
  --query "Reservations[].Instances[].BlockDeviceMappings[].Ebs.DeleteOnTermination"
```

This should now return `false`.

Now, when you terminate the instance, the **root volume will stay** in your account.

---

## 🧩 4. Option C — If Instance Is Already Terminated

If you’ve already terminated the instance, and the root volume was deleted, unfortunately:

> You can’t recover that volume **unless** you had a snapshot.

However, if you had taken a **snapshot**, you can easily recreate a volume from it:

```bash
aws ec2 create-volume --snapshot-id snap-0abc123456789def0 --availability-zone ap-southeast-2a
```

Then you can attach it to another instance or keep it for backup.

---

## 🧠 5. Pro Tip — Persistent Root Volume Pattern

A useful pattern for data persistence:

1. Launch instance with root EBS volume.
2. Set `DeleteOnTermination=false` for root.
3. When you terminate and later relaunch, attach the old volume again as root:

   ```bash
   aws ec2 attach-volume --volume-id vol-0abc123456789def0 --instance-id i-0987abcdef6543210 --device /dev/xvda
   ```

This way, your OS, configurations, and data persist across instances.

---

✅ **Summary**

| Scenario          | What to Do                            | Command/Option                           |
| ----------------- | ------------------------------------- | ---------------------------------------- |
| Before launch     | Uncheck *Delete on termination*       | Console or CLI `--block-device-mappings` |
| After launch      | `aws ec2 modify-instance-attribute`   | Set `DeleteOnTermination=false`          |
| After termination | Recreate from snapshot (if available) | `aws ec2 create-volume`                  |


---

## 🧭 1. 기본 개념 — EC2 종료 시 루트 EBS 볼륨 삭제의 기본 동작

EC2 인스턴스를 생성하면, 기본적으로 **루트 EBS 볼륨(root volume)** 은 아래 설정을 가지고 있습니다:

```
DeleteOnTermination = true
```

즉, 인스턴스를 **종료(terminate)** 하면 루트 볼륨이 자동으로 **삭제됩니다.**

하지만 이 설정은 변경할 수 있습니다.
→ 변경해두면 인스턴스가 삭제되어도 **루트 볼륨은 그대로 남습니다.**

---

## ⚙️ 2. 방법 A — 인스턴스 생성 전에 설정 변경

새 인스턴스를 만들 때 미리 설정할 수 있습니다.

1. **AWS 콘솔 → EC2 → 인스턴스 시작(Launch instance)**
2. "스토리지 구성(Configure storage)" 단계에서
   루트 볼륨 항목의 “**Delete on termination**” 체크박스를 **해제**합니다.
3. 인스턴스 생성 완료.

이렇게 하면 나중에 인스턴스를 종료해도 루트 볼륨이 자동 삭제되지 않고 **EBS 볼륨으로 남습니다.**

---

## 🪄 3. 방법 B — 이미 생성된 인스턴스의 설정을 변경 (종료 전에만 가능)

이미 인스턴스를 만들었더라도, **종료하기 전이라면** `DeleteOnTermination` 속성을 바꿀 수 있습니다.

### 🔧 AWS CLI 명령어 예시

```bash
aws ec2 modify-instance-attribute \
    --instance-id i-0123456789abcdef0 \
    --block-device-mappings '[{"DeviceName":"/dev/xvda","Ebs":{"DeleteOnTermination":false}}]'
```

> `/dev/xvda` 는 루트 디바이스 이름입니다.
> 정확한 이름은 아래 명령으로 확인할 수 있습니다:
>
> ```bash
> aws ec2 describe-instances --instance-id i-0123456789abcdef0
> ```

변경이 제대로 적용되었는지 확인하려면:

```bash
aws ec2 describe-instances --instance-id i-0123456789abcdef0 \
  --query "Reservations[].Instances[].BlockDeviceMappings[].Ebs.DeleteOnTermination"
```

이제 결과가 `false`로 표시되어야 합니다.

✅ 이렇게 설정해두면, 인스턴스를 **terminate 해도 루트 EBS 볼륨은 삭제되지 않습니다.**

---

## 🪦 4. 이미 인스턴스를 종료한 경우

만약 인스턴스를 **이미 종료했고**, 루트 볼륨이 **삭제된 상태라면**,
**스냅샷(snapshot)** 이 없는 한 원본 볼륨을 복구할 방법은 없습니다.

하지만, 스냅샷이 있다면 아래처럼 새 볼륨을 복원할 수 있습니다:

```bash
aws ec2 create-volume \
    --snapshot-id snap-0abc123456789def0 \
    --availability-zone ap-southeast-2a
```

→ 이렇게 만들어진 볼륨을 다른 인스턴스에 **attach** 해서 사용할 수 있습니다.

---

## 🧠 5. 프로 팁 — “영구 루트 볼륨” 패턴

운영 환경에서 자주 쓰는 안전한 패턴입니다:

1. 인스턴스를 만들 때 `DeleteOnTermination=false` 로 설정.
2. 인스턴스를 종료해도 루트 볼륨이 남음.
3. 새 인스턴스를 시작할 때, 이전 루트 볼륨을 다시 붙임:

   ```bash
   aws ec2 attach-volume \
       --volume-id vol-0abc123456789def0 \
       --instance-id i-0987abcdef6543210 \
       --device /dev/xvda
   ```

→ 이렇게 하면 OS, 설정, 데이터가 그대로 유지됩니다.

---

## ✅ 요약 정리

| 상황          | 조치 방법                           | 명령 또는 옵션                        |
| ----------- | ------------------------------- | ------------------------------- |
| 인스턴스 생성 전   | 콘솔에서 “Delete on termination” 해제 | 콘솔 또는 `--block-device-mappings` |
| 생성 후 (종료 전) | `modify-instance-attribute`로 수정 | `DeleteOnTermination=false`     |
| 이미 종료된 후    | 스냅샷으로 새 볼륨 생성                   | `create-volume --snapshot-id`   |
