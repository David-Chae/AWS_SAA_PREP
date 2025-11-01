# S3 Event Notifications  
# S3 이벤트 알림(S3 Event Notifications)  

---

## Introduction to S3 Event Notifications  
## S3 이벤트 알림 소개  

Amazon S3 Event Notifications enable you to respond automatically to specific events occurring within your S3 buckets.  
Amazon S3 이벤트 알림은 S3 버킷 내에서 발생하는 특정 이벤트에 자동으로 대응할 수 있게 해줍니다.  

These events include actions such as object creation, removal, restoration, or replication.  
이 이벤트에는 객체 생성, 삭제, 복원 또는 복제와 같은 작업이 포함됩니다.  

You can filter these events, for example, to only consider objects that end with .JPEG.  
예를 들어, .JPEG로 끝나는 객체만 고려하도록 이벤트를 필터링할 수 있습니다.  

The primary use case for Event Notifications is to trigger automated workflows.  
이벤트 알림의 주요 사용 사례는 자동화된 워크플로우를 트리거하는 것입니다.  

For instance, you might want to generate thumbnails for all images uploaded to Amazon S3.  
예를 들어, S3에 업로드된 모든 이미지에 대해 썸네일을 생성할 수 있습니다.  

To achieve this, you create an Event Notification and configure it to send events to one or more destinations.  
이를 위해 이벤트 알림을 생성하고 하나 이상의 대상에 이벤트를 전송하도록 구성합니다.  

---

## Event Notification Destinations  
## 이벤트 알림 대상  

You can send S3 Event Notifications to several types of destinations:  
S3 이벤트 알림을 여러 유형의 대상으로 전송할 수 있습니다:  

- SNS Topic  
- SNS 주제  
- SQS Queue  
- SQS 큐  
- Lambda Function  
- Lambda 함수  

If you are unfamiliar with these services, they will be covered in subsequent lectures.  
이 서비스에 익숙하지 않다면, 이후 강의에서 다룰 예정입니다.  

You can create as many S3 Event Notifications as needed and send them to any combination of these targets.  
필요한 만큼 S3 이벤트 알림을 생성하고, 대상 조합에 따라 전송할 수 있습니다.  

Typically, events are delivered within seconds, although delivery can sometimes take a minute or longer.  
일반적으로 이벤트는 몇 초 내에 전달되지만, 때때로 1분 이상 걸릴 수도 있습니다.  

---

## Required Permissions for Event Notifications  
## 이벤트 알림에 필요한 권한  

For Event Notifications to function correctly, appropriate IAM permissions must be configured.  
이벤트 알림이 정상 작동하려면 적절한 IAM 권한을 구성해야 합니다.  

When the S3 service sends data to an SNS topic, for example, an SNS resource access policy must be attached to the topic.  
예를 들어, S3 서비스가 SNS 주제로 데이터를 보낼 때 SNS 리소스 액세스 정책이 주제에 연결되어 있어야 합니다.  

This policy authorizes the S3 bucket to send messages directly to the SNS topic.  
이 정책은 S3 버킷이 SNS 주제로 직접 메시지를 전송할 수 있도록 권한을 부여합니다.  

Similarly, if you use an SQS queue as a destination, you must create an SQS resource access policy that authorizes the S3 service to send data to the queue.  
마찬가지로 SQS 큐를 대상으로 사용할 경우, S3 서비스가 데이터를 큐로 전송할 수 있도록 SQS 리소스 액세스 정책을 생성해야 합니다.  

For Lambda functions, a Lambda resource policy must be attached to the function to grant Amazon S3 permission to invoke it.  
Lambda 함수의 경우, S3가 해당 함수를 호출할 수 있도록 Lambda 리소스 정책이 연결되어야 합니다.  

Unlike IAM roles, these resource access policies are attached directly to the SNS topic, SQS queue, or Lambda function.  
IAM 역할과 달리, 이러한 리소스 액세스 정책은 SNS 주제, SQS 큐 또는 Lambda 함수에 직접 연결됩니다.  

They function similarly to S3 bucket policies by defining permissions for the respective resources.  
이 정책은 각 리소스에 대한 권한을 정의함으로써 S3 버킷 정책과 유사하게 작동합니다.  

---

## Event Notification Targets Summary  
## 이벤트 알림 대상 요약  

Remember that SNS, SQS, and Lambda functions serve as primary Event Notification targets.  
SNS, SQS, Lambda 함수가 주요 이벤트 알림 대상임을 기억하세요.  

However, there is a fourth integration to consider: Amazon EventBridge.  
하지만 고려해야 할 네 번째 통합 대상이 있습니다: Amazon EventBridge.  

---

## Integration with Amazon EventBridge  
## Amazon EventBridge와 통합  

All events occurring in your Amazon S3 buckets are sent to Amazon EventBridge.  
S3 버킷에서 발생하는 모든 이벤트는 Amazon EventBridge로 전송됩니다.  

From EventBridge, you can set up rules to route these events to over 18 different AWS services as destinations, greatly enhancing the capabilities of S3 Event Notifications.  
EventBridge에서는 규칙을 설정하여 이 이벤트를 18개 이상의 AWS 서비스 대상으로 라우팅할 수 있어, S3 이벤트 알림 기능을 크게 확장할 수 있습니다.  

EventBridge provides advanced filtering options beyond those available directly in S3.  
EventBridge는 S3에서 제공하는 필터링 기능보다 더 고급 필터링 옵션을 제공합니다.  

You can filter events by metadata, object size, and name.  
이벤트를 메타데이터, 객체 크기, 이름별로 필터링할 수 있습니다.  

Additionally, you can send events to multiple destinations simultaneously, such as Step Functions, Kinesis Data Streams, or Firehose.  
또한 Step Functions, Kinesis Data Streams, Firehose 등 여러 대상으로 동시에 이벤트를 전송할 수 있습니다.  

EventBridge also offers features like event archiving, replay, and more reliable delivery.  
EventBridge는 이벤트 아카이빙, 재생, 보다 안정적인 전달 등의 기능도 제공합니다.  

These capabilities significantly improve event handling and processing workflows.  
이 기능들은 이벤트 처리와 워크플로우 처리 능력을 크게 향상시킵니다.  

---

## Conclusion  
## 결론  

In summary, Amazon S3 Event Notifications allow you to react to events occurring in your S3 buckets by sending notifications to SNS, SQS, Lambda, or Amazon EventBridge.  
요약하면, S3 이벤트 알림은 S3 버킷에서 발생하는 이벤트에 대해 SNS, SQS, Lambda, Amazon EventBridge로 알림을 전송하여 자동으로 대응할 수 있게 합니다.  

This enables automated and scalable event-driven architectures within AWS.  
이를 통해 AWS 내에서 자동화되고 확장 가능한 이벤트 기반 아키텍처를 구현할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 Event Notifications allow automatic reactions to events such as object creation, removal, restoration, or replication.  
- S3 이벤트 알림은 객체 생성, 삭제, 복원, 복제 등 이벤트에 자동으로 대응할 수 있게 해줍니다.  

- Event Notifications can be sent to SNS topics, SQS queues, Lambda functions, or Amazon EventBridge.  
- 이벤트 알림은 SNS 주제, SQS 큐, Lambda 함수, Amazon EventBridge로 전송할 수 있습니다.  

- Proper resource access policies must be attached to SNS, SQS, and Lambda to authorize S3 to send events.  
- S3가 이벤트를 전송할 수 있도록 SNS, SQS, Lambda에 적절한 리소스 액세스 정책이 연결되어야 합니다.  

- Amazon EventBridge enhances S3 Event Notifications with advanced filtering, multiple destinations, event archiving, replay, and reliable delivery.  
- Amazon EventBridge는 고급 필터링, 다중 대상 전송, 이벤트 아카이빙, 재생, 안정적인 전달을 통해 S3 이벤트 알림 기능을 강화합니다.  

🎮 **게임보상:**

* **S3 Event Notifications 학습 완료!**

  * 이벤트 알림 개념 이해 +10
  * SNS/SQS/Lambda/EventBridge 대상 이해 +15
  * 리소스 정책과 권한 구조 이해 +10
    총 **35 XP 획득!** 🎉
