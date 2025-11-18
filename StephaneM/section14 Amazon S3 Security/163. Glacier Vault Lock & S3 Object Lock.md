# Glacier Vault Lock & S3 Object Lock  
# Glacier 볼트 잠금 및 S3 객체 잠금  

---

## Introduction to S3 Glacier Vault Lock  
## S3 Glacier 볼트 잠금 소개  

The concept of S3 Glacier Vault Lock is designed to implement a Write Once Read Many (WORM) model.  
S3 Glacier 볼트 잠금 개념은 WORM(Write Once Read Many, 한 번 쓰고 여러 번 읽기) 모델을 구현하도록 설계되었습니다.  

---

This means that once an object is placed into your S3 Glacier Vault, it can be locked so that it cannot be modified or deleted under any circumstances.  
즉, 객체가 S3 Glacier 볼트에 저장되면 어떤 상황에서도 수정하거나 삭제할 수 없도록 잠글 수 있습니다.  

---

To achieve this, you create a Vault Lock Policy on top of your Glacier vault.  
이를 위해 Glacier 볼트 위에 Vault Lock 정책을 생성합니다.  

---

Once this policy is locked, it cannot be changed or deleted by anyone in the future.  
이 정책이 잠기면, 앞으로 누구도 이를 변경하거나 삭제할 수 없습니다.  

---

This feature is particularly useful for compliance and data retention purposes.  
이 기능은 특히 규정 준수(compliance) 및 데이터 보존(data retention) 목적에 유용합니다.  

---

Once an object is inserted into a Glacier vault that has a Vault Lock Policy enabled and locked, the object cannot be deleted, not even by administrators or AWS.  
Vault Lock 정책이 활성화되고 잠긴 Glacier 볼트에 객체를 삽입하면, 관리자나 AWS조차도 객체를 삭제할 수 없습니다.  

---

This ensures strong compliance and legal data retention guarantees.  
이는 강력한 규정 준수와 법적 데이터 보존 보장을 제공합니다.  

---

## S3 Object Lock Overview  
## S3 객체 잠금 개요  

A similar but more granular option exists for S3 buckets, known as S3 Object Lock.  
S3 버킷에는 비슷하지만 더 세분화된 옵션인 S3 객체 잠금이 존재합니다.  

---

However, it is somewhat more complex. To enable S3 Object Lock, you must first enable versioning on the bucket.  
하지만 조금 더 복잡합니다. S3 객체 잠금을 사용하려면 먼저 버킷에서 버전 관리를 활성화해야 합니다.  

---

S3 Object Lock allows you to apply a WORM model at the individual object level within your bucket.  
S3 객체 잠금을 사용하면 버킷 내 개별 객체 수준에서 WORM 모델을 적용할 수 있습니다.  

---

This means you can lock specific object versions to prevent deletion for a specified amount of time.  
즉, 특정 객체 버전을 일정 기간 삭제되지 않도록 잠글 수 있습니다.  

---

There are two retention modes available:  
사용 가능한 보존 모드는 두 가지가 있습니다:  

---

- Compliance Mode  
- 준수 모드(Compliance Mode)  

- Governance Mode  
- 관리 모드(Governance Mode)  

---

### Compliance Mode  
### 준수 모드  

Compliance mode closely resembles the Glacier Vault Lock.  
준수 모드는 Glacier 볼트 잠금과 매우 유사합니다.  

---

Object versions cannot be overwritten or deleted by any user, including the root user.  
객체 버전은 루트 사용자 포함 모든 사용자에 의해 덮어쓰거나 삭제할 수 없습니다.  

---

Neither the retention modes nor the retention periods can be changed or shortened once set.  
한 번 설정되면 보존 모드나 보존 기간은 변경하거나 단축할 수 없습니다.  

---

This mode is used when strict compliance is required.  
이 모드는 엄격한 규정 준수가 필요한 경우 사용됩니다.  

---

### Governance Mode  
### 관리 모드  

Governance mode offers more flexibility.  
관리 모드는 더 유연한 옵션을 제공합니다.  

---

Most users cannot override or delete an object version or alter its lock settings.  
대부분의 사용자는 객체 버전을 덮어쓰거나 삭제하거나 잠금 설정을 변경할 수 없습니다.  

---

However, some users with special permissions granted through IAM can change the retention or delete the object directly.  
하지만 IAM을 통해 특별 권한을 부여받은 일부 사용자는 보존 기간을 변경하거나 객체를 직접 삭제할 수 있습니다.  

---

This mode is suitable when some administrative flexibility is needed.  
이 모드는 일부 관리 유연성이 필요한 경우 적합합니다.  

---

In both retention modes, you must specify a retention period.  
두 보존 모드 모두에서 보존 기간을 지정해야 합니다.  

---

This period defines how long the object is protected.  
이 기간은 객체가 보호되는 시간을 정의합니다.  

---

The retention period can be extended if necessary.  
필요한 경우 보존 기간을 연장할 수 있습니다.  

---

## Legal Hold on S3 Objects  
## S3 객체의 법적 보류(Legal Hold)  

In addition to retention modes, S3 Object Lock supports placing a legal hold on an object.  
보존 모드 외에도, S3 객체 잠금은 객체에 법적 보류(Legal Hold)를 적용할 수 있습니다.  

---

Legal hold protects the object indefinitely, independent of any retention period set previously.  
법적 보류는 이전에 설정된 보존 기간과 관계없이 객체를 무기한 보호합니다.  

---

For example, if an object is important for a trial or legal investigation, a legal hold can be placed on it to ensure it remains protected forever, regardless of retention settings.  
예를 들어, 객체가 재판이나 법적 조사에 중요하다면, 법적 보류를 적용하여 보존 기간과 상관없이 영구적으로 보호할 수 있습니다.  

---

Users with the IAM permission s3:PutObjectLegalHold can place or remove legal holds on objects.  
s3:PutObjectLegalHold IAM 권한을 가진 사용자는 객체에 법적 보류를 설정하거나 해제할 수 있습니다.  

---

This provides flexibility to protect objects during legal investigations and remove holds once they are no longer necessary.  
이는 법적 조사 중 객체를 보호하고, 필요 없을 때 보류를 해제할 수 있는 유연성을 제공합니다.  

---

## Summary  
## 요약  

Understanding the differences between Glacier Vault Lock and S3 Object Lock is important, especially for compliance and data retention strategies.  
Glacier 볼트 잠금과 S3 객체 잠금의 차이를 이해하는 것은 규정 준수 및 데이터 보존 전략에 있어 중요합니다.  

---

Glacier Vault Lock applies a strict WORM model at the vault level, while S3 Object Lock provides more granular control with retention modes and legal holds at the object level.  
Glacier 볼트 잠금은 볼트 수준에서 엄격한 WORM 모델을 적용하며, S3 객체 잠금은 객체 수준에서 보존 모드와 법적 보류를 통해 더 세분화된 제어를 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Glacier Vault Lock enables a Write Once Read Many (WORM) model by locking vault policies to prevent any modifications or deletions.  
- S3 Glacier 볼트 잠금은 볼트 정책을 잠금으로써 수정이나 삭제를 방지하여 WORM 모델을 구현합니다.  

- S3 Object Lock requires versioning enabled and allows locking individual object versions with retention modes.  
- S3 객체 잠금은 버전 관리 활성화가 필요하며, 보존 모드를 통해 개별 객체 버전을 잠글 수 있습니다.  

- Compliance mode in S3 Object Lock strictly prevents any changes or deletions, including by root users.  
- S3 객체 잠금의 준수 모드는 루트 사용자 포함 모든 변경이나 삭제를 엄격히 방지합니다.  

- Governance mode allows certain admin users with IAM permissions to override retention settings or delete objects.  
- 관리 모드는 IAM 권한을 가진 특정 관리자 사용자가 보존 설정을 변경하거나 객체를 삭제할 수 있도록 허용합니다.  

- Legal hold on S3 objects protects them indefinitely, independent of retention periods, and can be applied or removed by users with specific IAM permissions.  
- S3 객체의 법적 보류는 보존 기간과 상관없이 객체를 무기한 보호하며, 특정 IAM 권한을 가진 사용자가 설정하거나 해제할 수 있습니다.  

🎮 **게임보상:**

* Glacier Vault Lock & S3 Object Lock 개념 이해 +10 XP
* WORM 모델, 준수 모드/관리 모드 구분 +10 XP
* 법적 보류(Legal Hold) 활용 이해 +10 XP
  총 **30 XP 획득!** 🎉
