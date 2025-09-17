```markdown
# AWS Config - Overview  
# AWS Config - 개요  

## Introduction to AWS Config  
## AWS Config 소개  
AWS Config is a service that allows you to audit and record the compliance of your resources in AWS based on rules that you set.  
AWS Config는 사용자가 설정한 규칙을 기반으로 AWS 리소스의 준수 여부를 감사하고 기록할 수 있는 서비스입니다.  
(규정 준수 감사 기능)  

It also records configurations and their changes over time, enabling you to quickly roll back and understand what happened in your infrastructure if needed.  
또한 구성과 그 변경 사항을 시간 경과에 따라 기록하여 필요 시 빠르게 롤백하고 인프라에서 발생한 일을 이해할 수 있습니다.  
(변경 추적 및 롤백 지원)  

---

## Use Cases for AWS Config  
## AWS Config 사용 사례  
Some questions that AWS Config can help answer include:  
AWS Config가 답변할 수 있는 질문에는 다음과 같은 것들이 있습니다:  
(활용 예시)  

- Is there unrestricted SSH access to my security groups?  
- 내 보안 그룹에 제한 없는 SSH 접근이 있나요?  
- Do my buckets have public access?  
- 내 버킷이 공개 접근을 허용하고 있나요?  
- Has the configuration of an Application Load Balancer (ALB) changed over time?  
- 애플리케이션 로드 밸런서(ALB)의 구성은 시간이 지남에 따라 변경되었나요?  

Based on the compliance of these rules, you can receive alerts or SNS notifications for any changes.  
이 규칙들의 준수 여부에 따라, 변경 사항 발생 시 알림이나 SNS 통지를 받을 수 있습니다.  
(자동 알림 기능)  

---

## Regional and Aggregated Configuration  
## 리전별 및 통합 구성  
Config is a per-region service, so you need to configure it for all regions if required.  
Config는 리전별 서비스이므로 필요 시 모든 리전에 대해 설정해야 합니다.  
(리전별 설정 필요)  

You can aggregate data across regions and accounts to centralize it into one place.  
여러 리전과 계정의 데이터를 집계하여 한 곳에서 중앙 관리할 수 있습니다.  
(데이터 집계)  

Additionally, you can store the configuration of all your resources into Amazon S3 for historical analysis, for example, using serverless query engines such as Athena.  
또한, 모든 리소스의 구성을 Amazon S3에 저장하여 과거 분석에 활용할 수 있으며, Athena와 같은 서버리스 쿼리 엔진을 사용할 수 있습니다.  
(히스토리 분석)  

---

## Types of Config Rules  
## Config 규칙 유형  
You can use AWS managed Config rules, of which there are over 75 available, or create your own custom Config rules.  
AWS에서 제공하는 75개 이상의 관리형 Config 규칙을 사용하거나, 직접 커스텀 규칙을 생성할 수 있습니다.  
(규칙 유형)  

Custom rules require you to define the logic yourself, typically using a Lambda function.  
커스텀 규칙은 일반적으로 Lambda 함수를 사용해 로직을 직접 정의해야 합니다.  
(사용자 정의 규칙)  

For example, you can evaluate if each EBS disk is of type gp2 or if each t2 instance in your development accounts is of type t2.micro.  
예를 들어, 각 EBS 디스크가 gp2 타입인지, 개발 계정의 t2 인스턴스가 t2.micro인지 평가할 수 있습니다.  
(실무 예시)  

---

## Rule Evaluation Triggers  
## 규칙 평가 트리거  
Some rules can be evaluated or triggered whenever a configuration changes.  
일부 규칙은 구성 변경 시 즉시 평가 또는 트리거될 수 있습니다.  
(변경 기반 평가)  

For example, when a new configuration of your EBS disk occurs, the rule evaluates the disk type.  
예를 들어, EBS 디스크의 새 구성이 발생하면, 규칙이 디스크 유형을 평가합니다.  
(실시간 평가)  

Alternatively, rules can be evaluated at regular time intervals, such as every two hours, to ensure compliance continuously.  
또는 규칙을 일정 시간 간격(예: 2시간마다)으로 평가하여 지속적으로 규정 준수를 확인할 수 있습니다.  
(정기 평가)  

---

## Compliance vs Enforcement  
## 준수 모니터링 vs 강제 적용  
Config Rules are used solely for compliance monitoring.  
Config 규칙은 오직 준수 모니터링 용도로 사용됩니다.  
(모니터링 목적)  

They do not prevent actions from happening and do not replace security mechanisms such as IAM.  
행동을 방지하지 않으며, IAM과 같은 보안 메커니즘을 대체하지 않습니다.  
(강제 적용 아님)  

Instead, they provide an overview of your configuration and the compliance status of your resources.  
대신 구성과 리소스 준수 상태를 한눈에 확인할 수 있도록 해줍니다.  
(상태 시각화)  

---

## Cost Considerations  
## 비용 고려 사항  
AWS Config can become expensive quickly.  
AWS Config는 빠르게 비용이 증가할 수 있습니다.  
(비용 주의)  

The pricing is 0.003 per configuration item recorded per region and 0.001 per Config rule evaluation per region.  
가격은 리전별 기록된 구성 항목당 0.003 USD, Config 규칙 평가당 0.001 USD입니다.  
(가격 예시)  

---

## Viewing Compliance History  
## 준수 기록 보기  
For each resource, you can view its compliance status over time.  
각 리소스에 대해 시간 경과에 따른 준수 상태를 확인할 수 있습니다.  
(이력 확인)  

For example, you can see when a security group was non-compliant.  
예를 들어, 보안 그룹이 준수하지 않았던 시점을 확인할 수 있습니다.  
(준수 상태 확인)  

You can also view the resource's configuration history, including when changes occurred and who made them.  
리소스 구성 변경 이력과 변경 시점, 변경자도 확인할 수 있습니다.  
(변경 추적)  

By linking Config with CloudTrail, you can view the API calls made for that resource, providing a full picture of activity.  
Config를 CloudTrail과 연결하면, 해당 리소스에 대한 API 호출도 확인할 수 있어 전체 활동을 파악할 수 있습니다.  
(활동 추적)  

---

## Remediation of Non-Compliant Resources  
## 비준수 리소스 수정  
Although Config does not deny actions, you can remediate non-compliant resources using SSM Automation Documents.  
Config는 행동을 막지 않지만, SSM 자동화 문서를 사용해 비준수 리소스를 수정할 수 있습니다.  
(자동 수정)  

For example, you can monitor whether IAM access keys have expired (e.g., older than 90 days) and mark them as non-compliant.  
예를 들어, IAM 액세스 키가 만료되었는지(예: 90일 이상) 모니터링하고 비준수로 표시할 수 있습니다.  
(실무 예시)  

When a resource is non-compliant, you can trigger a remediation action such as the SSM document named RevokeUnusedIAMUserCredentials to deactivate those IAM access keys.  
리소스가 비준수일 때, RevokeUnusedIAMUserCredentials와 같은 SSM 문서를 트리거하여 해당 IAM 액세스 키를 비활성화할 수 있습니다.  
(자동화 실행)  

---

## Custom Remediation  
## 사용자 정의 수정  
You can use AWS-managed documents or create your own automation documents for remediation.  
AWS 관리 문서를 사용하거나 자체 자동화 문서를 생성하여 수정할 수 있습니다.  
(유연한 수정)  

If you want to extend functionality, you can create a document that invokes a Lambda function, allowing you to implement any custom remediation logic.  
기능 확장을 원하면 Lambda 함수를 호출하는 문서를 생성하여 커스텀 수정 로직을 구현할 수 있습니다.  
(커스텀 로직 적용)  

Remediation actions may include retries; for example, if a resource remains non-compliant after an auto-remediation, it may retry up to five times.  
수정 작업에는 재시도가 포함될 수 있습니다. 예를 들어, 자동 수정 후에도 비준수 상태가 지속되면 최대 5회까지 재시도할 수 있습니다.  
(재시도 가능)  

---

## Notifications  
## 알림  
You can use EventBridge to trigger notifications when resources become non-compliant.  
리소스가 비준수 상태가 되면 EventBridge를 사용해 알림을 트리거할 수 있습니다.  
(알림 트리거)  

For instance, if a security group becomes non-compliant, an EventBridge event can be triggered and passed to any target resource you choose.  
예를 들어, 보안 그룹이 비준수 상태가 되면 EventBridge 이벤트가 트리거되어 선택한 대상 리소스로 전달될 수 있습니다.  
(SNS, Slack 등 통합 가능)  

Additionally, you can send all changes and compliance notifications from Config to SNS.  
또한, Config에서 발생하는 모든 변경 및 준수 알림을 SNS로 전송할 수 있습니다.  
(중앙집중 알림)  

Using SNS filtering, you can filter for specific events and send notifications to an admin email, Slack channel, or other destinations to centralize alerts.  
SNS 필터링을 사용하면 특정 이벤트만 필터링하여 관리자 이메일, Slack 채널 등으로 알림을 중앙화할 수 있습니다.  
(필터링 및 중앙집중)  

---

## Conclusion  
## 결론  
This concludes the overview of AWS Config.  
이로써 AWS Config 개요를 마칩니다.  
(정리)  

It provides auditing, compliance monitoring, configuration history, remediation, and notification capabilities for your AWS resources.  
AWS 리소스에 대해 감사, 준수 모니터링, 구성 이력, 수정, 알림 기능을 제공합니다.  
(주요 기능 요약)  

In the next lecture, we will have some hands-on experience with AWS Config.  
다음 강의에서는 AWS Config 실습을 진행할 예정입니다.  
(실습 예고)  

---

##
```


Key Takeaways

## 핵심 요약

* AWS Config is a service for auditing and recording compliance of AWS resources based on user-defined rules.

* AWS Config는 사용자 정의 규칙 기반으로 AWS 리소스의 준수 여부를 감사하고 기록하는 서비스입니다.

* Config records configuration changes over time, enabling rollback and investigation of infrastructure changes.

* Config는 구성 변경을 시간 경과에 따라 기록하여 롤백 및 인프라 변경 조사 기능을 제공합니다.

* Users can use AWS managed rules or create custom rules via Lambda functions to evaluate resource compliance.

* 사용자는 AWS 관리형 규칙을 사용하거나 Lambda 함수를 통해 커스텀 규칙을 생성하여 리소스 준수를 평가할 수 있습니다.

* Config supports remediation actions through SSM Automation Documents and notifications via EventBridge and SNS.

* Config는 SSM 자동화 문서를 통한 수정 작업과 EventBridge 및 SNS를 통한 알림을 지원합니다.

```
게임보상: 🏅 AWS Config 대가! 이제 규칙 기반 준수 모니터링, 변경 기록 추적, 자동 수정, 알림까지 완벽하게 이해하고 활용할 수 있는 능력을 얻었습니다. ⚡📊
```
