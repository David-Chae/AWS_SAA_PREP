# Amazon Simple Notification Service (AWS SNS)  
# 아마존 단순 알림 서비스 (AWS SNS)  

---

## Introduction to Amazon SNS  
## Amazon SNS 소개  

Amazon Simple Notification Service (SNS) is designed to facilitate sending one message to many different receivers efficiently.  
Amazon 단순 알림 서비스(SNS)는 하나의 메시지를 여러 수신자에게 효율적으로 전송할 수 있도록 설계되었습니다.  

Instead of integrating each receiving service directly with the sender, SNS uses a publish-subscribe (Pub/Sub) pattern to simplify message distribution.  
각 수신 서비스를 발신자와 직접 통합하는 대신, SNS는 메시지 배포를 간소화하기 위해 발행-구독(Pub/Sub) 패턴을 사용합니다.  

In a traditional direct integration, for example, a buying service application might send an email notification, a message to a fraud service, a message to a shipping service, and even a message into an SQS queue.  
전통적인 직접 통합에서는 예를 들어, 구매 서비스 애플리케이션이 이메일 알림, 사기 탐지 서비스 메시지, 배송 서비스 메시지, 심지어 SQS 큐로 메시지를 전송해야 합니다.  

This approach becomes cumbersome as each new receiving service requires creating and writing a new integration.  
새로운 수신 서비스가 추가될 때마다 통합 작업을 만들어야 하므로 이 방법은 번거롭습니다.  

With the Pub/Sub pattern, the buying service sends a message to an SNS topic.  
Pub/Sub 패턴에서는 구매 서비스가 SNS 주제(topic)에 메시지를 전송합니다.  

This topic acts as a publisher, and multiple subscribers can receive messages from it.  
이 주제는 발행자 역할을 하며, 여러 구독자가 이 메시지를 받을 수 있습니다.  

Each subscriber independently receives the message published to the SNS topic, enabling scalable and decoupled communication.  
각 구독자는 SNS 주제에 게시된 메시지를 독립적으로 수신하며, 이는 확장 가능하고 분리된 통신을 가능하게 합니다.  

---

## SNS Topics and Subscriptions  
## SNS 주제와 구독  

In Amazon SNS, the event producer sends messages to a specific SNS topic.  
Amazon SNS에서는 이벤트 생산자가 특정 SNS 주제로 메시지를 전송합니다.  

Event receivers, or subscribers, listen to notifications from this topic.  
이벤트 수신자 또는 구독자는 해당 주제의 알림을 수신합니다.  

Each subscriber receives all messages sent to the topic unless message filtering is applied.  
메시지 필터링이 적용되지 않는 한, 각 구독자는 주제로 전송된 모든 메시지를 수신합니다.  

SNS supports up to 12,000,000 plus subscriptions per topic, and your AWS account can have up to 100,000 topics by default.  
SNS는 주제당 최대 1,200만 개 이상의 구독을 지원하며, AWS 계정당 기본적으로 최대 10만 개의 주제를 가질 수 있습니다.  

These limits can be increased upon request.  
이 제한은 요청 시 증가시킬 수 있습니다.  

These numbers illustrate the scalability of SNS for large-scale messaging needs.  
이 수치는 대규모 메시징 요구 사항에서 SNS의 확장성을 보여줍니다.  

---

## Supported Subscriber Types  
## 지원되는 구독자 유형  

Subscribers to an SNS topic can be of various types:  
SNS 주제의 구독자는 다양한 유형일 수 있습니다:  

- Email notifications  
- 이메일 알림  
- SMS and mobile push notifications  
- SMS 및 모바일 푸시 알림  
- HTTP or HTTPS endpoints  
- HTTP 또는 HTTPS 엔드포인트  
- AWS services such as SQS queues, Lambda functions, and Kinesis Data Firehose streams  
- SQS 큐, Lambda 함수, Kinesis Data Firehose 스트림과 같은 AWS 서비스  

This flexibility allows SNS to integrate seamlessly with many systems and services.  
이러한 유연성 덕분에 SNS는 다양한 시스템 및 서비스와 원활하게 통합될 수 있습니다.  

---

## Integration with AWS Services  
## AWS 서비스와의 통합  

Many AWS services send notifications directly to SNS topics.  
많은 AWS 서비스가 SNS 주제로 직접 알림을 전송합니다.  

Examples include:  
예시는 다음과 같습니다:  

- CloudWatch Alarms  
- CloudWatch 알람  
- Auto Scaling Group notifications  
- 오토 스케일링 그룹 알림  
- CloudFormation state changes  
- CloudFormation 상태 변경  
- Budgets  
- 예산  
- S3 bucket events  
- S3 버킷 이벤트  
- Database Migration Service (DMS)  
- 데이터베이스 마이그레이션 서비스(DMS)  
- Lambda  
- Lambda  
- DynamoDB  
- DynamoDB  
- RDS events  
- RDS 이벤트  

This integration enables automated workflows and alerting within AWS environments.  
이 통합은 AWS 환경에서 자동화된 워크플로우와 알림 기능을 제공합니다.  

---

## Publishing Messages to SNS  
## SNS에 메시지 게시  

To publish a message to SNS, you use the publish SDK method targeting a specific topic.  
SNS에 메시지를 게시하려면 특정 주제를 대상으로 하는 publish SDK 메서드를 사용합니다.  

The workflow involves:  
워크플로우는 다음과 같습니다:  

1. Creating an SNS topic  
1. SNS 주제 생성  
2. Creating one or more subscriptions to that topic  
2. 해당 주제에 하나 이상의 구독 생성  
3. Publishing messages to the topic  
3. 주제로 메시지 게시  

All subscribers automatically receive the published messages.  
모든 구독자는 게시된 메시지를 자동으로 수신합니다.  

For mobile applications, SNS supports direct publishing through platform applications and endpoints.  
모바일 애플리케이션의 경우, SNS는 플랫폼 애플리케이션 및 엔드포인트를 통한 직접 게시를 지원합니다.  

Supported platforms include Google Cloud Messaging (GCM), Apple Push Notification Service (APNS), and Amazon Device Messaging (ADM).  
지원되는 플랫폼에는 Google Cloud Messaging(GCM), Apple Push Notification Service(APNS), Amazon Device Messaging(ADM)이 포함됩니다.  

This allows mobile apps to receive push notifications via SNS.  
이를 통해 모바일 앱은 SNS를 통해 푸시 알림을 수신할 수 있습니다.  

---

## Security Features of Amazon SNS  
## Amazon SNS의 보안 기능  

Amazon SNS provides robust security features similar to those of Amazon SQS:  
Amazon SNS는 Amazon SQS와 유사한 강력한 보안 기능을 제공합니다:  

- In-flight encryption by default  
- 기본적으로 전송 중 암호화  
- At-rest encryption using AWS Key Management Service (KMS) keys  
- AWS Key Management Service(KMS) 키를 사용한 저장 시 암호화  
- Client-side encryption, where clients are responsible for encrypting and decrypting messages  
- 클라이언트 측 암호화(메시지 암호화와 복호화를 클라이언트가 담당)  

Access control is managed primarily through IAM policies, which regulate all SNS API actions.  
접근 제어는 주로 IAM 정책을 통해 관리되며, 모든 SNS API 작업을 규제합니다.  

SNS access policies, similar to S3 bucket policies, allow fine-grained permissions.  
S3 버킷 정책과 유사한 SNS 접근 정책은 세밀한 권한 설정을 허용합니다.  

They are particularly useful for enabling cross-account access to SNS topics or allowing other AWS services, such as S3 events, to publish messages to SNS topics.  
이는 SNS 주제에 대한 교차 계정 접근을 허용하거나, S3 이벤트와 같은 다른 AWS 서비스가 SNS 주제로 메시지를 게시하도록 허용할 때 특히 유용합니다.  

---

## Conclusion  
## 결론  

Amazon SNS simplifies the process of sending notifications to multiple receivers using the publish-subscribe pattern.  
Amazon SNS는 Pub/Sub 패턴을 사용하여 여러 수신자에게 알림을 보내는 과정을 단순화합니다.  

Its integration with various AWS services and support for multiple subscriber types make it a versatile tool for building scalable, event-driven architectures.  
다양한 AWS 서비스와의 통합 및 여러 구독자 유형 지원 덕분에 확장 가능하고 이벤트 기반 아키텍처를 구축하는 데 유용한 도구입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon SNS enables a publish-subscribe messaging pattern, allowing one message to be sent to many subscribers efficiently.  
- Amazon SNS는 발행-구독 메시징 패턴을 제공하여 하나의 메시지를 여러 구독자에게 효율적으로 전송할 수 있습니다.  

- SNS supports various subscriber types including email, SMS, HTTP(S) endpoints, and AWS services like SQS, Lambda, and Kinesis Data Firehose.  
- SNS는 이메일, SMS, HTTP(S) 엔드포인트, SQS, Lambda, Kinesis Data Firehose 등 다양한 구독자 유형을 지원합니다.  

- SNS integrates with many AWS services to receive notifications automatically, such as CloudWatch Alarms, Auto Scaling, and S3 events.  
- SNS는 CloudWatch 알람, 오토 스케일링, S3 이벤트 등 다양한 AWS 서비스와 통합되어 자동으로 알림을 수신할 수 있습니다.  

- Security in SNS includes in-flight and at-rest encryption, IAM policies, and SNS access policies for fine-grained access control.  
- SNS의 보안 기능에는 전송 중 및 저장 시 암호화, IAM 정책, 세밀한 접근 제어를 위한 SNS 접근 정책이 포함됩니다. 
