```markdown
# EventBridge Overview (formerly CloudWatch Events)  
# EventBridge 개요 (이전 이름: CloudWatch Events)  
(제목: AWS EventBridge의 기본 개념과 활용 방법 소개)  

---

## Introduction to Amazon EventBridge  
## Amazon EventBridge 소개  
Amazon EventBridge, formerly known as CloudWatch Events, is a service that allows you to schedule and react to events within AWS.  
Amazon EventBridge는 이전에 CloudWatch Events로 알려졌던 서비스로, AWS 내에서 이벤트를 예약하고 대응할 수 있게 해줍니다.  
(기능 정의)  

Although the name has changed, you will see EventBridge referenced in AWS exams and documentation.  
이름은 변경되었지만, AWS 시험과 문서에서 EventBridge를 계속 확인할 수 있습니다.  
(시험/문서 상 인식 안내)  

If you have prior AWS experience, you might recognize it as CloudWatch Events.  
이전에 AWS를 사용한 경험이 있다면 CloudWatch Events로 익숙할 수 있습니다.  
(기존 명칭과 연결)  

---

## Scheduling and Event Patterns  
## 예약 및 이벤트 패턴  
With EventBridge, you can schedule cron jobs in the cloud.  
EventBridge를 사용하면 클라우드에서 크론 작업을 예약할 수 있습니다.  
(기본 사용 예시)  

For example, you can configure it to trigger a Lambda function every hour, which then runs a script.  
예를 들어, 매시간 Lambda 함수를 트리거하여 스크립트를 실행하도록 설정할 수 있습니다.  
(실제 활용 예)  

Events are generated on this schedule, hence the name Amazon EventBridge.  
이 일정에 따라 이벤트가 생성되므로 Amazon EventBridge라는 이름이 붙었습니다.  
(이름의 의미)  

Beyond scheduled events, EventBridge can also react to specific event patterns.  
예약된 이벤트뿐 아니라, EventBridge는 특정 이벤트 패턴에도 반응할 수 있습니다.  
(패턴 기반 반응 기능)  

Event rules can respond to AWS service activities.  
이벤트 규칙은 AWS 서비스 활동에 대응할 수 있습니다.  
(규칙 기능 설명)  

For instance, you can react to the event of an IAM root user signing into the AWS console.  
예를 들어, IAM 루트 사용자가 AWS 콘솔에 로그인할 때 이벤트에 대응할 수 있습니다.  
(보안 관련 사용 예)  

---

## Security Use Case Example  
## 보안 사용 사례 예시  
When the root user signs in, you might want to send a message to an SNS topic to receive an email notification.  
루트 사용자가 로그인하면, SNS 토픽으로 메시지를 보내 이메일 알림을 받도록 할 수 있습니다.  
(보안 모니터링 예)  

This is a useful security feature to monitor root account usage.  
루트 계정 사용을 모니터링할 수 있는 유용한 보안 기능입니다.  
(실무 활용)  

EventBridge supports multiple destinations for events, including triggering Lambda functions, sending SNS or SQS messages, and more.  
EventBridge는 이벤트 목적지를 다양하게 지원하며, Lambda 함수 트리거, SNS/SQS 메시지 전송 등 여러 작업이 가능합니다.  
(다양한 이벤트 목적지)  

---

## Event Sources and Integration  
## 이벤트 소스 및 통합  
EventBridge acts as a central hub receiving events from various sources:  
EventBridge는 다양한 소스에서 이벤트를 수신하는 중앙 허브 역할을 합니다.  
(기능 요약)  

- EC2 instances (start, stop, terminate events)  
- EC2 인스턴스 (시작, 중지, 종료 이벤트)  

- CodeBuild (build success or failure)  
- CodeBuild (빌드 성공 또는 실패 이벤트)  

- S3 (object uploads)  
- S3 (객체 업로드 이벤트)  

- Trusted Advisor (security findings)  
- Trusted Advisor (보안 관련 결과)  

You can also combine EventBridge with CloudTrail to intercept any API call made within your AWS accounts, which is a powerful feature for monitoring and automation.  
EventBridge를 CloudTrail과 결합하면 AWS 계정 내에서 발생하는 모든 API 호출을 캡처할 수 있으며, 모니터링과 자동화에 강력한 기능을 제공합니다.  
(강력한 모니터링/자동화 기능)  

---

## Scheduling Flexibility  
## 예약 유연성  
EventBridge supports flexible scheduling options such as every four hours, every Monday at 8:00 AM, or the first Monday of the month.  
EventBridge는 4시간마다, 매주 월요일 8:00 AM, 매달 첫 번째 월요일 등 유연한 예약 옵션을 지원합니다.  
(유연한 예약 기능)  

These scheduled events are sent into EventBridge where you can apply filters to select specific events, such as those related to a particular S3 bucket.  
이 예약 이벤트는 EventBridge로 전송되며, 특정 이벤트(예: 특정 S3 버킷 관련 이벤트)를 필터링할 수 있습니다.  
(필터링 기능)  

---

## Event Details and JSON Format  
## 이벤트 세부 정보 및 JSON 형식  
Events in EventBridge are represented as JSON documents containing detailed information such as instance IDs, timestamps, IP addresses, and more.  
EventBridge의 이벤트는 인스턴스 ID, 타임스탬프, IP 주소 등 상세 정보를 포함한 JSON 문서로 표현됩니다.  
(이벤트 구조)  

This rich event data enables powerful integrations and automation workflows.  
이 풍부한 이벤트 데이터는 강력한 통합 및 자동화 워크플로우를 가능하게 합니다.  
(활용 가치)  

---

## Event Destinations  
## 이벤트 목적지  
EventBridge events can be sent to various AWS services, including:  
EventBridge 이벤트는 다음과 같은 AWS 서비스로 전송될 수 있습니다.  
(목적지 목록)  

- Lambda functions  
- Lambda 함수  

- AWS Batch jobs  
- AWS Batch 작업  

- Amazon ECS tasks  
- Amazon ECS 태스크  

- SQS queues  
- SQS 큐  

- SNS topics  
- SNS 토픽  

- Kinesis Data Streams  
- Kinesis 데이터 스트림  

- Step Functions  
- Step Functions  

- CodePipeline pipelines  
- CodePipeline 파이프라인  

- CodeBuild projects  
- CodeBuild 프로젝트  

- Systems Manager (SSM) automation  
- Systems Manager (SSM) 자동화  

- EC2 actions such as starting, stopping, or restarting instances  
- EC2 인스턴스 시작, 중지, 재시작 등의 동작  

This flexibility allows you to build complex event-driven architectures tailored to your use cases.  
이러한 유연성 덕분에 사용 사례에 맞춘 복잡한 이벤트 기반 아키텍처를 구축할 수 있습니다.  
(실무 활용)  

---

## Event Buses in Amazon EventBridge  
## Amazon EventBridge의 이벤트 버스  
Amazon EventBridge provides three types of event buses:  
Amazon EventBridge는 세 가지 유형의 이벤트 버스를 제공합니다.  

- Default Event Bus: Receives events from AWS services within your account.  
- 기본 이벤트 버스: 계정 내 AWS 서비스에서 발생하는 이벤트를 수신합니다.  

- Partner Event Bus: Receives events from SaaS partners integrated with AWS, such as Zendesk, Datadog, or Auth0.  
- 파트너 이벤트 버스: AWS와 통합된 SaaS 파트너(Zendesk, Datadog, Auth0 등) 이벤트를 수신합니다.  

- Custom Event Bus: Allows you to create your own event buses for custom applications to send events.  
- 맞춤 이벤트 버스: 커스텀 애플리케이션이 이벤트를 전송할 수 있는 이벤트 버스를 생성할 수 있습니다.  

Each event bus enables you to route events to different destinations using EventBridge rules.  
각 이벤트 버스는 EventBridge 규칙을 사용하여 이벤트를 다양한 목적지로 라우팅할 수 있습니다.  
(라우팅 기능)  

---

## Cross-Account Event Sharing  
## 크로스 계정 이벤트 공유  
EventBridge supports resource-based policies that allow you to manage permissions for event buses.  
EventBridge는 이벤트 버스 권한을 관리할 수 있는 리소스 기반 정책을 지원합니다.  
(권한 관리)  

For example, you can configure a central event bus in one AWS account to receive events from other accounts within your AWS Organization.  
예를 들어, 한 AWS 계정의 중앙 이벤트 버스가 조직 내 다른 계정에서 발생한 이벤트를 수신하도록 구성할 수 있습니다.  
(실무 예시)  

This is achieved by adding resource-based policies that permit other accounts to send events to the central event bus.  
이는 다른 계정이 중앙 이벤트 버스로 이벤트를 전송할 수 있도록 리소스 기반 정책을 추가하여 구현됩니다.  
(정책 적용 방법)  

---

## Event Archiving and Replay  
## 이벤트 아카이빙 및 재생  
EventBridge allows you to archive events, either all events or a filtered subset, with retention periods that can be indefinite or time-limited.  
EventBridge는 이벤트 전체 또는 필터링된 일부 이벤트를 아카이브할 수 있으며, 보존 기간은 무기한 또는 제한 기간으로 설정 가능합니다.  
(아카이빙 기능)  

Archived events can be replayed later, which is useful for debugging, troubleshooting, and fixing production issues.  
아카이브된 이벤트는 나중에 재생할 수 있으며, 디버깅, 문제 해결, 프로덕션 문제 수정에 유용합니다.  
(재생 활용)  

For example, if a Lambda function has a bug, you can fix it and then replay the archived events to retest the function.  
예를 들어, Lambda 함수에 버그가 있을 경우 수정 후 아카이브된 이벤트를 재생하여 함수 테스트를 다시 수행할 수 있습니다.  
(실무 예시)  

---

## Schema Registry  
## 스키마 레지스트리  
EventBridge includes a Schema Registry that analyzes events on your event bus and infers their schemas.  
EventBridge에는 이벤트 버스의 이벤트를 분석하고 스키마를 추론하는 스키마 레지스트리가 포함되어 있습니다.  
(스키마 관리 기능)  

This feature allows you to generate code for your applications that understands the structure of the event data in advance.  
이를 통해 이벤트 데이터 구조를 사전에 이해하는 애플리케이션 코드를 생성할 수 있습니다.  
(자동 코드 생성)  

Schemas can be versioned to accommodate changes over time.  
스키마는 시간이 지나면서 변경 사항을 반영할 수 있도록 버전 관리가 가능합니다.  
(버전 관리)  

For example, a schema for a CodePipeline event can be downloaded and used to structure your application code accordingly.  
예를 들어, CodePipeline 이벤트 스키마를 다운로드하여 애플리케이션 코드 구조에 맞게 사용할 수 있습니다.  
(실무 예시)  

---

## Summary  
## 요약  
In summary, Amazon EventBridge enables you to react to events happening within your AWS accounts using the default event bus, integrate with SaaS partners through partner event buses, and handle custom events with custom event buses.
```


요약하면, Amazon EventBridge는 기본 이벤트 버스를 사용해 AWS 계정 내 이벤트에 대응하고, 파트너 이벤트 버스를 통해 SaaS 파트너와 통합하며, 커스텀 이벤트 버스를 통해 맞춤 이벤트를 처리할 수 있습니다.
(서비스 요약)

It provides powerful features such as the Schema Registry for event structure inference and resource-based policies for cross-account event sharing.
스키마 레지스트리를 통한 이벤트 구조 추론, 크로스 계정 이벤트 공유를 위한 리소스 기반 정책 등 강력한 기능을 제공합니다.
(주요 기능)

EventBridge is a versatile service that supports a wide range of event-driven architectures and automation scenarios.
EventBridge는 다양한 이벤트 기반 아키텍처와 자동화 시나리오를 지원하는 다재다능한 서비스입니다.
(특징 요약)

---

## Key Takeaways

## 핵심 요약

* Amazon EventBridge, formerly known as CloudWatch Events, enables scheduling and reacting to events within AWS.

* Amazon EventBridge(이전 CloudWatch Events)는 AWS 내에서 이벤트 예약 및 대응을 지원합니다.

* EventBridge supports multiple event buses: default, partner, and custom, allowing integration with AWS services, SaaS partners, and custom applications.

* EventBridge는 기본, 파트너, 커스텀 이벤트 버스를 지원하며, AWS 서비스, SaaS 파트너, 커스텀 애플리케이션과 통합할 수 있습니다.

* Events can trigger various AWS services such as Lambda, SNS, SQS, ECS, Step Functions, and more.

* 이벤트는 Lambda, SNS, SQS, ECS, Step Functions 등 다양한 AWS 서비스를 트리거할 수 있습니다.

* Features include event archiving and replay, schema registry for event structure inference, and resource-based policies for cross-account event sharing.

* 기능에는 이벤트 아카이빙/재생, 이벤트 구조 추론을 위한 스키마 레지스트리, 크로스 계정 이벤트 공유를 위한 리소스 기반 정책이 포함됩니다.

```
🎮 **게임보상**: EventBridge 마스터 완료! **+250 EXP**와 **“Event-Driven Architect 🛠️” 배지** 획득!  
```
