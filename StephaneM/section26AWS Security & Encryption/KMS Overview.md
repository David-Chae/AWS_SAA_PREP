```markdown
# KMS Overview  
# KMS 개요  

## Introduction to AWS KMS  
## AWS KMS 소개  

AWS Key Management Service (KMS) is a key management service provided by AWS.  
AWS Key Management Service(KMS)는 AWS에서 제공하는 키 관리 서비스입니다.  
(암호화 키를 관리하는 서비스임)  

Although many users have been utilizing it unknowingly, anytime encryption is involved with an AWS service, it is most likely using KMS encryption.  
많은 사용자가 모르게 사용하고 있지만, AWS 서비스에서 암호화가 사용될 때 대부분 KMS 암호화를 사용합니다.  
(암호화의 기본 엔진 역할 수행)  

The primary purpose of KMS is for AWS to manage the encryption keys on behalf of users, reducing the operational burden.  
KMS의 주요 목적은 사용자를 대신해 AWS가 암호화 키를 관리하여 운영 부담을 줄이는 것입니다.  
(운영 효율성 제공)  

KMS is fully integrated with AWS Identity and Access Management (IAM) for authorization, providing straightforward methods to control access to encrypted data.  
KMS는 IAM(Identity and Access Management)과 완전히 통합되어 권한 부여를 관리하며, 암호화된 데이터 접근을 쉽게 제어할 수 있습니다.  
(IAM과의 통합)  

One of the powerful features of AWS KMS is the ability to audit every API call made to use your keys through AWS CloudTrail, which is an important aspect often tested in certification exams.  
KMS의 강력한 기능 중 하나는 CloudTrail을 통해 모든 키 관련 API 호출을 감사할 수 있다는 점이며, 이는 자격증 시험에서 자주 출제됩니다.  
(추적 및 감사 가능)  

---

## Integration with AWS Services  
## AWS 서비스와의 통합  

AWS KMS can be seamlessly integrated with most AWS services.  
AWS KMS는 대부분의 AWS 서비스와 원활하게 통합됩니다.  
(다양한 서비스 지원)  

For example, to encrypt data at rest in an Elastic Block Store (EBS) volume, you simply enable KMS integration.  
예를 들어, EBS 볼륨에 저장 데이터를 암호화하려면 KMS 통합만 활성화하면 됩니다.  
(손쉬운 통합 방식)  

The same applies to Amazon S3, Amazon RDS, AWS Systems Manager (SSM), and virtually all services that require encryption.  
Amazon S3, RDS, SSM 등 암호화가 필요한 거의 모든 서비스에도 동일하게 적용됩니다.  
(광범위한 서비스 적용)  

Additionally, KMS can be used directly by users through API calls, the AWS Command Line Interface (CLI), or SDKs.  
또한 사용자는 API 호출, CLI, SDK를 통해 직접 KMS를 사용할 수도 있습니다.  
(개발자 친화적 활용)  

This allows you to encrypt any secret data using a KMS key.  
이를 통해 KMS 키로 모든 비밀 데이터를 암호화할 수 있습니다.  
(민감 데이터 보호)  

Encrypted secrets can then be safely stored in your code or environment variables, which is a much better security practice than storing secrets in plain text.  
암호화된 비밀은 코드나 환경 변수에 안전하게 저장할 수 있으며, 평문으로 저장하는 것보다 훨씬 안전합니다.  
(보안 모범 사례)  

---

## Types of KMS Keys  
## KMS 키 유형  

AWS KMS keys, formerly known as Customer Master Keys (CMKs), are now simply referred to as KMS keys to avoid confusion with customer managed keys.  
이전에는 CMK(Customer Master Key)라 불렸던 AWS KMS 키는 혼동을 피하기 위해 이제 단순히 KMS 키라고 합니다.  
(용어 변경)  

There are two main types of KMS keys:  
KMS 키에는 두 가지 주요 유형이 있습니다.  

### Symmetric KMS Keys  
### 대칭 KMS 키  

These use a single key for both encryption and decryption.  
암호화와 복호화에 동일한 키를 사용합니다.  
(단일 키 사용)  

All AWS services integrated with KMS use symmetric keys.  
KMS와 통합된 모든 AWS 서비스는 대칭 키를 사용합니다.  
(표준 방식)  

When using symmetric keys, you never get direct access to the key material; instead, you interact with the key through KMS API calls.  
대칭 키 사용 시 실제 키 자체에 접근하지 않고, API 호출을 통해서만 사용합니다.  
(보안성 강화)  

### Asymmetric KMS Keys  
### 비대칭 KMS 키  

These consist of a public key used for encryption and a private key used for decryption.  
암호화를 위한 공개 키와 복호화를 위한 개인 키로 구성됩니다.  
(공개키/개인키 구조)  

They support encrypt/decrypt or sign/verify operations.  
암호화/복호화 또는 서명/검증 작업을 지원합니다.  
(다양한 보안 기능)  

The public key can be downloaded from KMS, but the private key is only accessible via API calls.  
공개 키는 다운로드 가능하지만, 개인 키는 API 호출로만 접근할 수 있습니다.  
(개인 키 보안 유지)  

Asymmetric keys are useful when encryption needs to be performed outside of AWS by users who do not have access to the KMS API.  
비대칭 키는 AWS API에 접근할 수 없는 외부 사용자에게 유용합니다.  
(외부 활용 사례)  

---

## Categories of KMS Keys  
## KMS 키 분류  

AWS Owned Keys: These are free and used internally by AWS services, such as SSE-S3 or DynamoDB encryption. These keys are not visible to users.  
AWS 소유 키: 무료이며, SSE-S3 또는 DynamoDB 암호화 같은 내부 서비스에 사용됩니다. 사용자가 볼 수 없습니다.  
(내부 전용)  

AWS Managed Keys: Also free, these keys are prefixed with AWS/ followed by the service name, for example, AWS/RDS or AWS/EBS. They can be used only within the service they are assigned to.  
AWS 관리 키: 무료이며 `AWS/서비스명` 형식으로 표시됩니다. 예: AWS/RDS, AWS/EBS. 해당 서비스 내에서만 사용 가능합니다.  
(자동 관리 키)  

Customer Managed Keys: These are keys created and managed by customers, costing approximately $1 per month. Customers can import keys as well, with the same cost. Additionally, there is a charge of about $0.03 per 10,000 API calls to KMS.  
고객 관리 키: 사용자가 직접 생성/관리하는 키로 월 약 $1의 비용이 발생합니다. 가져오기(import)한 키도 동일한 비용이 부과됩니다. 또한 KMS API 호출 1만 건당 약 $0.03의 요금이 발생합니다.  
(비용 발생 항목)  

---

## Key Rotation and Regional Scope  
## 키 순환 및 리전 범위  

KMS supports automatic key rotation:  
KMS는 자동 키 순환을 지원합니다.  

- For AWS managed keys, rotation occurs automatically every year.  
- AWS 관리 키는 매년 자동 순환됩니다.  

- For customer managed keys, automatic rotation can be enabled with a configurable period, and on-demand rotation is also supported.  
- 고객 관리 키는 자동 순환을 사용자가 설정할 수 있으며, 필요 시 수동 순환도 가능합니다.  

- Imported keys require manual rotation.  
- 가져오기 키는 반드시 수동으로 순환해야 합니다.  

KMS keys are scoped per AWS region.  
KMS 키는 AWS 리전별로 제한됩니다.  
(리전 단위로 분리됨)  

For example, if you have an EBS volume encrypted with a KMS key in the EU West 2 region, copying that volume to another region requires several steps:  
예를 들어, EU West 2 리전에서 KMS 키로 암호화된 EBS 볼륨을 다른 리전으로 복사하려면 다음 단계를 거칩니다.  

1. Take a snapshot of the encrypted EBS volume. The snapshot is encrypted with the same KMS key.  
1. 암호화된 EBS 볼륨의 스냅샷을 생성합니다. 해당 스냅샷은 동일한 KMS 키로 암호화됩니다.  

2. Copy the snapshot to the target region, re-encrypting it with a different KMS key (AWS handles this).  
2. 스냅샷을 대상 리전으로 복사할 때 다른 KMS 키로 재암호화됩니다(AWS가 처리).  

3. Restore the snapshot into a new EBS volume in the target region, encrypted with the new KMS key.  
3. 새 KMS 키로 암호화된 상태로 스냅샷을 대상 리전에서 EBS 볼륨으로 복원합니다.  

The same KMS key cannot exist in two regions simultaneously.  
동일한 KMS 키는 두 리전에 동시에 존재할 수 없습니다.  
(리전 독립성 유지)  

---

## KMS Key Policies  
## KMS 키 정책  

KMS key policies control access to your KMS keys and are similar to S3 bucket policies.  
KMS 키 정책은 접근을 제어하며, S3 버킷 정책과 유사합니다.  
(정책 기반 접근 제어)  

However, if a KMS key does not have an associated key policy, no one can access it.  
그러나 키 정책이 없는 경우 누구도 해당 KMS 키에 접근할 수 없습니다.  
(정책 필수 조건)  

There are two types of KMS key policies:  
KMS 키 정책에는 두 가지 유형이 있습니다.  

### Default Key Policy  
### 기본 키 정책  

Created automatically if no custom policy is provided.  
사용자가 정책을 정의하지 않으면 자동으로 생성됩니다.  

It allows everyone in your AWS account to access the key, provided they have the appropriate IAM permissions.  
IAM 권한이 있다면 계정 내 모든 사용자가 키에 접근할 수 있습니다.  

### Custom Key Policy  
### 사용자 정의 키 정책  

Allows you to define specific users and roles that can access or administer the key.  
특정 사용자와 역할이 키를 접근/관리할 수 있도록 정의할 수 있습니다.  

This is particularly useful for cross-account access, where you can authorize another AWS account to use your KMS key.  
특히 교차 계정 접근 시 유용하며, 다른 AWS 계정이 내 KMS 키를 사용하도록 허용할 수 있습니다.  

An example use case is sharing encrypted snapshots across accounts.  
예: 암호화된 스냅샷을 계정 간에 공유하는 경우.  

You create a snapshot encrypted with your customer managed key, attach a custom key policy authorizing cross-account access, share the snapshot with the target account, and then the target account copies and re-encrypts the snapshot with its own customer managed key before creating a volume.  
고객 관리 키로 암호화된 스냅샷을 생성 → 사용자 정의 정책으로 교차 계정 권한 부여 → 대상 계정에 공유 → 대상 계정은 해당 스냅샷을 복사 후 자체 고객 관리 키로 재암호화하여 볼륨 생성.  
(실제 활용 흐름 예시)  

---

## Summary  
## 요약  

This overview covered the fundamentals of AWS KMS, including its integration with AWS services, types of keys, key management, regional considerations, and key policies.  
이번 개요에서는 AWS KMS의 기초, 서비스 통합, 키 유형, 관리, 리전 제한, 키 정책을 다뤘습니다.  

Understanding these concepts is essential for securely managing encryption keys and encrypted data within AWS environments.  
이러한 개념을 이해하는 것은 AWS 환경에서 암호화 키와 데이터를 안전하게 관리하는 데 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS KMS is a key management service that manages encryption keys, integrated with IAM for access control.  
- AWS KMS는 키를 관리하는 서비스이며 IAM과 통합되어 접근 제어를 지원합니다.  

- KMS supports symmetric keys (single key for encrypt/decrypt) and asymmetric keys (public/private key pairs).  
- KMS는 대칭 키(단일 키)와 비대칭 키(공개/개인 키 쌍)를 지원합니다.  

- Different types of KMS keys include AWS owned keys, AWS managed keys, and customer managed keys, each with distinct usage and pricing.  
- KMS 키 유형: AWS 소유 키, AWS 관리 키, 고객 관리 키로 구분되며 각각 사용처와 비용이 다릅니다.  

- KMS keys are region-specific; copying encrypted snapshots across regions requires re-encryption with a different key.  
- KMS 키는 리전별로 독립적이며, 스냅샷을 다른 리전으로 복사 시 재암호화가 필요합니다.  

- KMS key policies control access, with default policies allowing account-wide access and custom policies enabling fine-grained and cross-account permissions.  
- KMS 키 정책은 접근 제어를 담당하며, 기본 정책은 계정 내 전체 접근을, 사용자 정의 정책은 세밀한 및 교차 계정 권한을 제공합니다.  
```

🎮 게임보상: 🗝️ **"KMS 키 마스터 레벨 달성!"** 🔐 IAM, 대칭/비대칭 키, 리전별 제한, 정책까지 완벽 정복! 🚀
