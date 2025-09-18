```markdown
# SSM Parameter Store Overview  
# SSM 파라미터 스토어 개요  

🎮 게임보상: "SSM 마스터" 업적 달성 +500 XP  

---

## Introduction to SSM Parameter Store  
## SSM 파라미터 스토어 소개  

SSM Parameter Store is a secure storage solution for configuration and secrets.  
SSM 파라미터 스토어는 구성 설정과 비밀 정보를 안전하게 저장할 수 있는 솔루션입니다.  

It allows you to store configuration data and secrets securely.  
구성 데이터와 비밀 정보를 안전하게 저장할 수 있습니다.  

Optionally, you can choose to encrypt these configurations, making them secrets by using the KMS service.  
선택적으로 KMS 서비스를 이용해 이 데이터를 암호화하여 비밀로 만들 수도 있습니다.  

SSM Parameter Store is serverless, scalable, and durable.  
SSM 파라미터 스토어는 서버리스이며, 확장 가능하고 내구성이 뛰어납니다.  

The SDK is very easy to use.  
SDK 사용법도 매우 간단합니다.  

If you update your parameters, you have version tracking of them.  
파라미터를 업데이트하면 버전 추적 기능이 제공됩니다.  

Security is provided through IAM, and you receive notifications with Amazon EventBridge in certain cases.  
보안은 IAM을 통해 제공되며, 특정 상황에서는 Amazon EventBridge로 알림을 받을 수 있습니다.  

There is full integration with CloudFormation, which means CloudFormation can leverage parameters from Parameter Store as input parameters for your stacks.  
CloudFormation과 완전히 통합되어 있어, CloudFormation이 파라미터 스토어의 값을 스택 입력 파라미터로 활용할 수 있습니다.  

---

## Example Usage  
## 사용 예시  

Consider an application that uses the SSM Parameter Store.  
SSM 파라미터 스토어를 사용하는 애플리케이션을 예로 들어보겠습니다.  

You can store plain text configuration in this way.  
평문 구성 데이터를 이렇게 저장할 수 있습니다.  

The IAM permissions of your applications are checked, for example, your EC2 instance role.  
예를 들어, EC2 인스턴스 역할과 같은 애플리케이션의 IAM 권한이 확인됩니다.  

Alternatively, you can have encrypted configuration.  
또는 암호화된 구성 데이터를 저장할 수도 있습니다.  

In that case, the SSM Parameter Store encrypts it with KMS.  
이 경우 SSM 파라미터 스토어가 KMS로 데이터를 암호화합니다.  

The KMS service is used for encryption and decryption.  
암호화 및 복호화에는 KMS 서비스가 사용됩니다.  

You must ensure that your applications have access to the underlying KMS key to perform encryption and decryption.  
애플리케이션이 암호화 및 복호화를 수행하려면 KMS 키에 접근 권한이 있는지 확인해야 합니다.  

---

## Hierarchical Parameter Organization  
## 계층적 파라미터 구조  

You can store parameters in the Parameter Store with a hierarchy.  
파라미터를 계층 구조로 저장할 수 있습니다.  

For example, you can define a path such as my-department/my-app/dev/Dev-DB-URL and Dev-DB-password within that folder.  
예를 들어, `my-department/my-app/dev/Dev-DB-URL` 및 `Dev-DB-password`와 같은 경로로 저장할 수 있습니다.  

This means your parameters go all the way down into the hierarchy.  
즉, 파라미터가 계층 구조 하위까지 내려갑니다.  

You can go one level up and store a parameter for the Prod-DB-URL as well as a Prod-DB-password, and go up to another app or another department.  
한 단계 위로 올라가 Prod-DB-URL 및 Prod-DB-password를 저장하거나, 다른 애플리케이션 또는 다른 부서 경로로 저장할 수 있습니다.  

This allows you to organize your parameters in a structured fashion.  
이를 통해 파라미터를 구조적으로 체계적으로 관리할 수 있습니다.  

This organization simplifies your IAM policies, allowing applications to have access to an entire department, an entire app, or just an app department environment-specific path.  
이 구조는 IAM 정책을 단순화하여, 애플리케이션이 전체 부서, 전체 애플리케이션, 또는 특정 환경 경로에 접근하도록 설정할 수 있습니다.  

---

## Accessing Secrets and Public Parameters  
## 비밀 정보 및 공개 파라미터 접근  

You also have the opportunity to access Secrets from Secrets Manager through the Parameter Store by using a specific reference.  
특정 참조를 사용하면 Parameter Store를 통해 Secrets Manager의 비밀 정보에 접근할 수 있습니다.  

This is a useful trick that not many people know.  
많은 사람이 모르는 유용한 팁입니다.  

There are also public parameters issued by AWS that you can use.  
AWS에서 제공하는 공개 파라미터도 사용할 수 있습니다.  

For example, if you want to find the latest AMI for Amazon EC2 in your specific region, this is available within the Parameter Store as an API call.  
예를 들어, 특정 리전의 최신 Amazon EC2 AMI를 찾고 싶다면, Parameter Store API 호출을 통해 가능합니다.  

---

## Application Example with IAM Roles  
## IAM 역할을 활용한 애플리케이션 예시  

For example, a Dev Lambda function can have an IAM role that allows it to access the DB-URL and DB-password within the Dev environment of your app.  
예를 들어, 개발 환경의 Lambda 함수가 Dev 환경의 DB-URL과 DB-password에 접근할 수 있는 IAM 역할을 가질 수 있습니다.  

A Prod Lambda function, with a different IAM policy and possibly some environment variables, can access the Prod DB-URL and Prod-DB-password of another path.  
프로덕션 환경 Lambda 함수는 다른 IAM 정책과 환경 변수를 통해 다른 경로의 Prod DB-URL 및 Prod-DB-password에 접근할 수 있습니다.  

---

## Parameter Tiers: Standard and Advanced  
## 파라미터 등급: Standard와 Advanced  

Within Systems Manager, there are two kinds of parameter tiers: standard and advanced.  
Systems Manager 내 파라미터는 Standard와 Advanced 두 가지 등급이 있습니다.  

The main difference is the size limit—4KB for standard and 8KB for advanced.  
주요 차이점은 크기 제한으로, Standard는 4KB, Advanced는 8KB입니다.  

The availability of parameter policies also differs: standard has none, while advanced supports them.  
파라미터 정책 지원 여부도 다릅니다. Standard는 없지만, Advanced는 지원합니다.  

The advanced type of parameters costs $0.05 per month, whereas the standard tier is free.  
Advanced 파라미터는 월 $0.05 비용이 발생하며, Standard는 무료입니다.  

---

## Parameter Policies (Advanced Only)  
## 파라미터 정책 (Advanced 전용)  

Parameter policies are available only for advanced parameters.  
파라미터 정책은 Advanced 파라미터에서만 사용할 수 있습니다.  

These allow you to assign a time to live (TTL) to a parameter, which means an expiration date.  
이 정책을 통해 파라미터에 TTL(유효 기간)을 설정할 수 있으며, 이는 만료일을 의미합니다.  

This forces users to update or delete sensitive data such as passwords.  
이를 통해 사용자는 비밀번호와 같은 민감 데이터를 업데이트하거나 삭제하도록 강제할 수 있습니다.  

You can assign multiple policies at a time.  
여러 정책을 동시에 적용할 수 있습니다.  

---

## Example: Expiration Policy and EventBridge Notifications  
## 예시: 만료 정책 및 EventBridge 알림  

Here is an example policy: an expiration policy to delete a parameter at a specific timestamp.  
예시 정책: 특정 시점에 파라미터를 삭제하는 만료 정책입니다.  

Through EventBridge integration, EventBridge receives notifications.  
EventBridge 통합을 통해 EventBridge가 알림을 받습니다.  

For example, 15 days before the parameter expires, you will receive a notification in EventBridge, giving you enough time to update it and ensure the parameter is not deleted due to TTL.  
예를 들어, 파라미터 만료 15일 전에 EventBridge 알림을 받아 TTL로 인해 삭제되지 않도록 업데이트할 충분한 시간을 제공합니다.  

Sometimes, you may want to ensure parameters change periodically.  
때때로, 파라미터가 주기적으로 변경되도록 하고 싶을 수 있습니다.  

You can have a no-change notification in EventBridge so that if a parameter has not been updated for 20 days, you will be notified as well.  
파라미터가 20일 동안 업데이트되지 않은 경우 EventBridge로 알림을 받을 수 있는 기능을 설정할 수 있습니다.  

This allows you to be creative with the Parameter Store.  
이를 통해 Parameter Store를 보다 창의적으로 활용할 수 있습니다.  

---

## Conclusion  
## 결론  

Now you have an understanding of the idea behind SSM Parameter Store.  
이제 SSM 파라미터 스토어의 개념을 이해하게 되었습니다.  

---

## Key Takeaways  
## 핵심 요약  

- SSM Parameter Store provides secure, serverless, and scalable storage for configuration and secrets, with optional KMS encryption.  
  SSM 파라미터 스토어는 구성 및 비밀 정보를 위한 안전하고 서버리스이며 확장 가능한 저장소를 제공하며, KMS 암호화를 선택적으로 사용할 수 있습니다.  

- Parameters can be organized hierarchically, simplifying IAM policy management and access control.  
  파라미터는 계층 구조로 저장할 수 있어 IAM 정책 관리와 접근 제어를 단순화할 수 있습니다.  

- There are standard and advanced parameter tiers, with advanced supporting parameter policies like expiration (TTL) and notifications via EventBridge.  
```


Standard와 Advanced 파라미터 등급이 있으며, Advanced는 만료(TTL) 및 EventBridge 알림과 같은 정책을 지원합니다.

* Parameter Store integrates with CloudFormation, Secrets Manager, and supports public parameters for AWS resources.
  Parameter Store는 CloudFormation, Secrets Manager와 통합되며, AWS 리소스를 위한 공개 파라미터도 지원합니다.

🎮 게임보상: "SSM 파라미터 전략가" +700 XP 🔑
