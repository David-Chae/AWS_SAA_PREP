```markdown
# AWS Secrets Manager - Hands On  
# AWS Secrets Manager - 실습  

🎮 게임보상: "Secrets Manager Hands On 시작" +500 XP  

---

## Introduction to AWS Secrets Manager  
## AWS Secrets Manager 소개  

AWS Secrets Manager is a service designed to easily rotate, manage, and retrieve secrets throughout their lifecycle.  
AWS Secrets Manager는 비밀을 쉽게 회전, 관리 및 생명주기 동안 안전하게 조회할 수 있도록 설계된 서비스입니다.  

It is similar to the AWS Systems Manager Parameter Store in that it allows you to store secret information; however, Secrets Manager differs by providing rotation, management, and tight integrations with various databases.  
SSM Parameter Store와 유사하게 비밀 정보를 저장할 수 있지만, Secrets Manager는 회전, 관리, 그리고 다양한 데이터베이스와의 긴밀한 통합 기능이 제공된다는 점에서 차별화됩니다.  

---

## Supported Database Integrations  
## 지원되는 데이터베이스 통합  

Secrets Manager integrates with databases such as MySQL, PostgreSQL, Amazon Aurora, and Amazon RDS, among others.  
Secrets Manager는 MySQL, PostgreSQL, Amazon Aurora, Amazon RDS 등과 통합됩니다.  

This integration facilitates automatic rotation and management of database credentials.  
이 통합 덕분에 데이터베이스 자격 증명을 자동으로 회전하고 관리할 수 있습니다.  

---

## Pricing Model  
## 요금 모델  

Secrets Manager offers a 30-day free trial.  
Secrets Manager는 30일 무료 체험을 제공합니다.  

Afterward, the pricing is 0.40 per secret per month and 0.05 per 10,000 API calls.  
그 이후 요금은 비밀당 월 $0.40, API 호출 10,000회당 $0.05입니다.  

To remain within the free tier, you can create a secret and then delete it.  
무료 계층을 유지하려면, 비밀을 생성한 후 삭제할 수 있습니다.  

---

## Creating and Storing a New Secret  
## 새로운 비밀 생성 및 저장  

When storing a new secret, you can choose the secret type.  
새 비밀을 저장할 때 비밀 유형을 선택할 수 있습니다.  

Over time, the capability and integrations may increase.  
시간이 지나면서 지원되는 기능과 통합 범위가 늘어날 수 있습니다.  

Currently, supported secret types include Amazon RDS, Amazon DocumentDB, Amazon Redshift, other databases, or custom secrets.  
현재 지원되는 비밀 유형에는 Amazon RDS, Amazon DocumentDB, Amazon Redshift, 기타 데이터베이스 또는 사용자 정의 비밀이 포함됩니다.  

---

## Example: Custom Secret  
## 예시: 사용자 정의 비밀  

For a custom secret, you can specify key-value pairs such as:  
사용자 정의 비밀의 경우, 다음과 같이 키-값 쌍을 지정할 수 있습니다.  

- MySecretKey: MyVerySecretValue  
- MySecretKey: MyVerySecretValue  

- API_KEY: a secret API key string  
- API_KEY: 비밀 API 키 문자열  

You can enter these values through the user interface or edit them as a JSON document.  
이 값을 사용자 인터페이스를 통해 입력하거나 JSON 문서로 편집할 수 있습니다.  

---

## Security and Encryption  
## 보안 및 암호화  

Secrets are kept confidential and accessible only to users with the correct IAM permissions.  
비밀은 기밀로 유지되며 올바른 IAM 권한을 가진 사용자만 접근할 수 있습니다.  

You can specify an encryption key, either the default AWS-managed key or a customer-managed AWS KMS key.  
암호화 키를 지정할 수 있으며, AWS 관리 기본 키 또는 사용자 관리 AWS KMS 키를 선택할 수 있습니다.  

---

## Naming and Resource Permissions  
## 이름 지정 및 리소스 권한  

When creating a secret, you provide a name such as prod/my-secret and optionally a description.  
비밀을 생성할 때, prod/my-secret와 같은 이름을 지정하고 선택적으로 설명을 추가할 수 있습니다.  

You can also define resource policies to restrict access to the secret, including cross-account access, similar to S3 bucket policies.  
S3 버킷 정책과 유사하게 리소스 정책을 정의하여 비밀에 대한 접근을 제한할 수 있으며, 계정 간 접근도 가능합니다.  

---

## Multi-Region Replication  
## 다중 리전 복제  

Secrets Manager allows you to replicate secrets across AWS regions.  
Secrets Manager는 비밀을 AWS 리전 간 복제할 수 있습니다.  

This is useful for multi-region applications or databases.  
이는 다중 리전 애플리케이션 또는 데이터베이스에 유용합니다.  

You can specify target regions and encryption keys for replication, such as replicating to us-west-2 or ap-southeast-1.  
복제를 위해 대상 리전과 암호화 키를 지정할 수 있으며, 예를 들어 us-west-2 또는 ap-southeast-1로 복제할 수 있습니다.  

---

## Secret Rotation  
## 비밀 회전  

You can enable automatic rotation of secrets.  
비밀의 자동 회전을 활성화할 수 있습니다.  

When enabled, you specify a Lambda function that performs the rotation.  
활성화 시, 회전을 수행할 Lambda 함수를 지정합니다.  

This function updates the secret and any associated resources accordingly.  
이 함수는 비밀과 관련 리소스를 자동으로 업데이트합니다.  

For now, rotation can be disabled if not needed.  
필요하지 않은 경우 회전 기능은 비활성화할 수 있습니다.  

---

## Retrieving Secrets Programmatically  
## 프로그램을 통한 비밀 조회  

Secrets Manager provides code snippets to retrieve secrets from your applications.  
Secrets Manager는 애플리케이션에서 비밀을 조회할 수 있는 코드 스니펫을 제공합니다.  

This enables your clients to securely access the stored secrets during runtime.  
이를 통해 클라이언트는 런타임 동안 안전하게 저장된 비밀에 접근할 수 있습니다.  

---

## Managing Amazon RDS Credentials  
## Amazon RDS 자격 증명 관리  

You can store credentials for Amazon RDS databases, including username and password.  
Amazon RDS 데이터베이스용 자격 증명(사용자 이름 및 비밀번호 포함)을 저장할 수 있습니다.  

Thanks to the integration between RDS and Secrets Manager, these credentials can be used to log in to the database.  
RDS와 Secrets Manager의 통합 덕분에, 이 자격 증명을 사용하여 데이터베이스에 로그인할 수 있습니다.  

When rotated, the database credentials are updated automatically.  
회전 시, 데이터베이스 자격 증명이 자동으로 갱신됩니다.  

---

## Configuration Options  
## 구성 옵션  

You can configure multi-region replication and rotation settings for RDS secrets as needed.  
RDS 비밀에 대해 필요에 따라 다중 리전 복제 및 회전 설정을 구성할 수 있습니다.  

Once configured, the secret management process is automated and secure.  
구성 후에는 비밀 관리 과정이 자동화되고 안전하게 됩니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on AWS Secrets Manager.  
이로써 AWS Secrets Manager 실습 강의를 마칩니다.  

The service provides a robust solution for managing secrets securely with features such as rotation, encryption, access control, and multi-region replication.  
회전, 암호화, 접근 제어, 다중 리전 복제 등의 기능을 갖춘 안전한 비밀 관리 솔루션입니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Secrets Manager facilitates easy rotation, management, and retrieval of secrets throughout their lifecycle.  
  AWS Secrets Manager는 비밀의 생명주기 동안 회전, 관리, 조회를 쉽게 수행할 수 있습니다.  

- It offers tight integration with databases like MySQL, PostgreSQL, Amazon Aurora, and RDS.  
  MySQL, PostgreSQL, Amazon Aurora, RDS 등 데이터베이스와 긴밀하게 통합됩니다.  

- Secrets can be stored as key-value pairs, encrypted with default or custom KMS keys, and access is controlled via IAM permissions.  
  비밀은 키-값 쌍으로 저장할 수 있으며, 기본 또는 사용자 지정 KMS 키로 암호화되고 IAM 권한으로 접근을 제어합니다.  

- Secrets Manager supports resource policies for cross-account access and multi-region replication for high availability.  
  Secrets Manager는 계정 간 접근을 위한 리소스 정책과 고가용성을 위한 다중 리전 복제를 지원합니다.  
```

🎮 게임보상 완료: "Secrets Manager Hands On 마스터" +1000 XP 🏆
