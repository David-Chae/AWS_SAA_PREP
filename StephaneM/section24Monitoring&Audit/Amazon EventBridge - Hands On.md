```markdown
# Amazon EventBridge - Hands On  
# Amazon EventBridge - 실습  
(제목: EventBridge 실습을 통한 이해와 활용)  

---

## Introduction to Amazon EventBridge  
## Amazon EventBridge 소개  
Amazon EventBridge is a service that allows you to react to events happening within your AWS account or from partner services.  
Amazon EventBridge는 AWS 계정 내 이벤트나 파트너 서비스 이벤트에 대응할 수 있는 서비스입니다.  
(서비스 기능 개요)  

It offers several features including rules, pipes to connect event sources, schedules to invoke targets regularly, and a schema registry to organize your event schemas.  
이 서비스는 규칙(Rules), 이벤트 소스 연결용 파이프(Pipes), 타깃 정기 호출용 스케줄(Schedules), 이벤트 스키마 관리용 스키마 레지스트리(Schema Registry) 등의 기능을 제공합니다.  
(주요 기능 설명)  

---

## EventBridge Rules  
## EventBridge 규칙(Rules)  
Rules are the core feature of EventBridge that enable you to respond to events in your account.  
규칙(Rules)은 EventBridge의 핵심 기능으로, 계정 내 이벤트에 대응할 수 있게 해줍니다.  
(핵심 기능)  

For example, you can create a rule that triggers whenever an EC2 instance changes state, such as starting, stopping, or terminating.  
예를 들어, EC2 인스턴스 상태가 시작, 중지, 종료될 때마다 트리거되는 규칙을 생성할 수 있습니다.  
(실제 활용 예시)  

When creating a rule, you specify an event pattern to match events.  
규칙 생성 시 이벤트 패턴을 지정하여 이벤트를 매칭합니다.  
(규칙 설정 과정)  

For instance, you can select the EC2 service and choose the event type "Instance State-change Notification".  
예를 들어, EC2 서비스를 선택하고 "인스턴스 상태 변경 알림(Instance State-change Notification)" 이벤트 유형을 선택할 수 있습니다.  
(이벤트 유형 선택 예시)  

You can further filter by specific states, such as "shutting down" or "terminated", to be notified only when these occur.  
추가로 "종료 중(shutting down)" 또는 "종료됨(terminated)"과 같은 특정 상태로 필터링하여 해당 상태일 때만 알림을 받을 수 있습니다.  
(상태 필터링)  

---

## Selecting Targets for Rules  
## 규칙 대상(Target) 선택  
Once a rule is triggered, you must specify a target to handle the event.  
규칙이 트리거되면, 이벤트를 처리할 대상을 지정해야 합니다.  
(대상 지정 필요성)  

EventBridge supports many target types, including:  
EventBridge는 다음과 같은 여러 대상 유형을 지원합니다.  

- Sending notifications to an SNS topic  
- SNS 토픽으로 알림 전송  

- Starting or stopping EC2 instances  
- EC2 인스턴스 시작 또는 중지  

- Running ECS tasks  
- ECS 태스크 실행  

- Invoking Lambda functions  
- Lambda 함수 호출  

- Sending messages to SQS queues  
- SQS 큐로 메시지 전송  

For example, you can create an SNS topic and subscribe an email address to receive notifications whenever the rule triggers.  
예를 들어, SNS 토픽을 생성하고 이메일 주소를 구독하면 규칙이 트리거될 때마다 알림을 받을 수 있습니다.  
(실무 활용 예시)  

---

## Creating an SNS Topic  
## SNS 토픽 생성  
To send notifications, you first create an SNS topic, such as "demotopic", and then select it as the target for your EventBridge rule.  
알림을 보내려면 먼저 "demotopic"과 같은 SNS 토픽을 생성하고 EventBridge 규칙의 대상으로 선택합니다.  
(설정 과정)  

If the topic has an email subscription, you will receive emails whenever the rule triggers due to an EC2 instance state change.  
이 토픽이 이메일 구독을 가지고 있다면, EC2 인스턴스 상태 변경으로 규칙이 트리거될 때마다 이메일을 받게 됩니다.  
(알림 동작 설명)  

---

## EventBridge Scheduler  
## EventBridge 스케줄러  
EventBridge also provides a Scheduler feature that allows you to run tasks on a recurring or one-time schedule.  
EventBridge는 반복 또는 단일 스케줄로 작업을 실행할 수 있는 스케줄러 기능도 제공합니다.  
(스케줄러 기능)  

For example, you can set up a schedule to run every hour to invoke a Lambda function for cleanup or send a message to an SQS queue to trigger automation.  
예를 들어, 매시간 Lambda 함수를 호출하거나 SQS 큐로 메시지를 보내 자동화 작업을 트리거하는 스케줄을 설정할 수 있습니다.  
(활용 예시)  

You can configure the schedule with options such as rate expressions (e.g., every one hour) and flexible time windows.  
스케줄은 실행 간격(rate expression, 예: 1시간마다)과 유연한 시간 창(flexible time window) 옵션으로 구성할 수 있습니다.  
(세부 설정 가능)  

The Scheduler UI is separate from the main EventBridge events and buses interface.  
스케줄러 UI는 EventBridge 메인 이벤트 및 버스 인터페이스와 별도로 제공됩니다.  
(UI 설명)  

---

## Event Buses  
## 이벤트 버스  
EventBridge uses event buses to organize events.  
EventBridge는 이벤트를 구성하기 위해 이벤트 버스를 사용합니다.  
(이벤트 구조화)  

By default, there is a "default" event bus for your account.  
기본적으로 계정에는 "default" 이벤트 버스가 있습니다.  
(기본 버스 설명)  

You can create additional event buses to separate events for security or organizational purposes.  
보안 또는 조직적 목적을 위해 추가 이벤트 버스를 생성할 수 있습니다.  
(목적별 이벤트 분리)  

Each event bus can have its own set of rules.  
각 이벤트 버스는 자체 규칙 세트를 가질 수 있습니다.  
(규칙 관리)  

---

## Replaying Events  
## 이벤트 재생  
Amazon EventBridge allows you to replay events on an event bus.  
Amazon EventBridge는 이벤트 버스에서 이벤트를 재생할 수 있습니다.  
(재생 기능)  

This feature is useful for debugging or reprocessing events that have already occurred.  
이 기능은 디버깅이나 이미 발생한 이벤트 재처리에 유용합니다.  
(활용 예시)  

---

## Partner Event Sources  
## 파트너 이벤트 소스  
In addition to AWS service events, EventBridge supports partner event sources.  
AWS 서비스 이벤트 외에도 EventBridge는 파트너 이벤트 소스를 지원합니다.  
(파트너 통합)  

For example, you can integrate Auth0 so that when a user signs up, an event is sent directly to EventBridge.  
예를 들어, Auth0와 통합하면 사용자가 가입할 때 이벤트가 EventBridge로 바로 전송됩니다.  
(실무 예시)  

This enables automation and workflows triggered by external SaaS services without writing glue code.  
이를 통해 외부 SaaS 서비스 기반의 자동화와 워크플로우를 추가 코드 없이 구현할 수 있습니다.  
(효율적 자동화)  

---

## API Destinations  
## API 목적지  
EventBridge rules can also send events to API destinations outside of AWS.  
EventBridge 규칙은 AWS 외부의 API 목적지로 이벤트를 전송할 수도 있습니다.  
(외부 API 호출 가능)  

This allows you to invoke external APIs or SaaS services as part of your event-driven architecture.  
이를 통해 이벤트 기반 아키텍처의 일부로 외부 API나 SaaS 서비스를 호출할 수 있습니다.  
(외부 연동)  

---

## Schema Registry  
## 스키마 레지스트리  
EventBridge includes a schema registry that catalogs the structure of events.  
EventBridge에는 이벤트 구조를 카탈로그화하는 스키마 레지스트리가 포함되어 있습니다.  
(스키마 관리 기능)  

You can browse event schemas for AWS services, such as EC2 instance state changes, to understand the JSON structure and data types.  
EC2 인스턴스 상태 변경과 같은 AWS 서비스 이벤트 스키마를 확인하여 JSON 구조와 데이터 타입을 이해할 수 있습니다.  
(스키마 확인)  

The registry also allows you to download code bindings in languages like Java, Python, TypeScript, and Go, enabling you to develop applications that consume events without manually defining schemas.  
레지스트리는 Java, Python, TypeScript, Go 등의 언어로 코드 바인딩을 다운로드할 수 있어, 이벤트를 수동으로 정의하지 않고도 애플리케이션 개발이 가능합니다.  
(코드 자동 생성)  

---

## Summary  
## 요약  
Amazon EventBridge is a powerful event-driven service that enables you to react to AWS and partner events using rules and schedules.  
Amazon EventBridge는 규칙과 스케줄을 통해 AWS 및 파트너 이벤트에 대응할 수 있는 강력한 이벤트 기반 서비스입니다.  
(서비스 요약)  

It supports a wide range of targets and integrations, event buses for separation, event replay for debugging, and a schema registry for development ease.  
다양한 대상 및 통합, 이벤트 분리를 위한 이벤트 버스, 디버깅용 이벤트 재생, 개발 편의성을 위한 스키마 레지스트리를 지원합니다.  
(주요 기능 정리)  

As a best practice, familiarize yourself with creating rules and schedules to leverage EventBridge effectively.  
모범 사례로, EventBridge를 효과적으로 활용하기 위해 규칙과 스케줄 생성에 익숙해지는 것이 좋습니다.  
(활용 팁)  

---

## Key Takeaways  
## 핵심 요약  
- Amazon EventBridge enables reacting to events in your AWS account using rules.  
- Amazon EventBridge는 규칙을 통해 AWS 계정 내 이벤트에 대응할 수 있습니다.  

- EventBridge rules can trigger various targets, such as SNS topics, Lambda functions, or ECS tasks.  
- EventBridge 규칙은 SNS 토픽, Lambda 함수, ECS 태스크 등 다양한 대상을 트리거할 수 있습니다.  

- EventBridge Scheduler allows setting up recurring or one-time schedules to invoke targets.  
- EventBridge 스케줄러를 사용하면 반복 또는 단일 스케줄로 대상 호출을 설정할 수 있습니다.  

- Event buses provide event separation and security, and EventBridge supports partner event sources and schema registries for integration and development.  
- 이벤트 버스는 이벤트 분리 및 보안을 제공하며, EventBridge는 파트너 이벤트 소스 및 스키마 레지스트리를 통한 통합과 개발을 지원합니다.  
```

🎮 **게임보상**: EventBridge Hands-On 완료! **+300 EXP**와 **“Event-Driven Pro ⚡” 배지** 획득!
