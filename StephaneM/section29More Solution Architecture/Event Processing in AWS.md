```markdown
# Event Processing in AWS  
# AWS에서의 이벤트 처리  

Let's discuss event processing in AWS, exploring the different possibilities and the constraints associated with each.  
AWS에서 이벤트 처리를 논의하면서 가능한 방법들과 각각의 제약사항을 살펴봅시다.  

---

## Using SQS and Lambda  
## SQS와 Lambda 사용  

One common approach is to use Amazon Simple Queue Service (SQS) with AWS Lambda.  
일반적인 방법 중 하나는 Amazon SQS와 AWS Lambda를 함께 사용하는 것입니다.  

Events are inserted into an SQS queue, and the Lambda service pulls messages from this queue.  
이벤트는 SQS 큐에 삽입되고, Lambda 서비스는 이 큐에서 메시지를 가져옵니다.  

If there are processing issues, Lambda puts the messages back into the SQS queue and retries pulling them.  
처리에 문제가 발생하면 Lambda는 메시지를 다시 SQS 큐에 넣고 재시도합니다.  

This retry mechanism can potentially lead to an infinite loop if a message consistently fails processing.  
이 재시도 메커니즘은 특정 메시지가 계속 실패할 경우 무한 루프에 빠질 수 있습니다.  

To handle such cases, you can configure SQS to send messages to a dead letter queue (DLQ) after a specified number of retries, for example, five attempts.  
이런 상황을 방지하기 위해, SQS에 재시도 횟수(예: 5회) 초과 시 메시지를 DLQ(사망 편지 큐)로 보내도록 설정할 수 있습니다.  

This setup provides a way to isolate problematic messages and prevent blocking the queue.  
이 설정은 문제가 있는 메시지를 격리하여 큐 전체가 막히는 것을 방지합니다.  

---

## Using SQS FIFO and Lambda  
## SQS FIFO와 Lambda 사용  

Another option is to use SQS FIFO (First-In-First-Out) queues with Lambda.  
또 다른 방법은 SQS FIFO 큐를 Lambda와 함께 사용하는 것입니다.  

FIFO queues ensure that messages are processed in order.  
FIFO 큐는 메시지가 순서대로 처리되도록 보장합니다.  

However, if one message fails processing, it blocks the entire queue, causing a never-ending blocking process.  
하지만 하나의 메시지가 실패하면 큐 전체가 멈춰서 끝없는 블로킹 상황이 발생할 수 있습니다.  

To mitigate this, you can configure a dead letter queue to receive messages that fail processing after multiple retries.  
이를 완화하기 위해 여러 번 재시도 후 실패한 메시지를 DLQ로 보낼 수 있습니다.  

This allows the Lambda function to continue processing subsequent messages without being blocked.  
이렇게 하면 Lambda가 다음 메시지들을 막힘 없이 처리할 수 있습니다.  

---

## Using SNS and Lambda  
## SNS와 Lambda 사용  

Alternatively, you can use Amazon Simple Notification Service (SNS) with Lambda.  
또는 Amazon SNS와 Lambda를 함께 사용할 수도 있습니다.  

In this architecture, messages are sent asynchronously from SNS to Lambda.  
이 아키텍처에서는 메시지가 SNS에서 Lambda로 비동기적으로 전송됩니다.  

Lambda has a different retry behavior here: it retries processing a message internally up to three times.  
이 경우 Lambda는 메시지 처리를 내부적으로 최대 3번까지 재시도합니다.  

If the message still fails, it is discarded or can be sent to a dead letter queue configured at the Lambda service level, such as an SQS queue for later processing.  
그래도 실패하면 메시지는 버려지거나 Lambda 서비스 레벨에서 구성된 DLQ(SQS 큐 등)에 보내져 나중에 처리할 수 있습니다.  

Note the architectural difference: with SQS, the DLQ is configured on the SQS side, whereas with Lambda, the DLQ is configured on the Lambda side.  
여기서 중요한 차이점은 SQS의 경우 DLQ가 SQS 측에서 설정되지만, Lambda의 경우 DLQ가 Lambda 측에서 설정된다는 점입니다.  

---

## Fan Out Pattern  
## 팬 아웃 패턴  

The Fan Out pattern is used to deliver data to multiple SQS queues reliably.  
팬 아웃 패턴은 데이터를 여러 SQS 큐로 안정적으로 전달하기 위해 사용됩니다.  

**Option 1:** Your application, with the AWS SDK installed, sends the same message sequentially to multiple SQS queues.  
**옵션 1:** AWS SDK가 설치된 애플리케이션이 동일한 메시지를 여러 SQS 큐에 순차적으로 전송합니다.  

While this works, it is not reliable because if the application crashes after sending to some queues, others will miss the message, leading to inconsistent queue contents.  
이 방식은 동작하긴 하지만, 중간에 애플리케이션이 크래시되면 일부 큐에만 메시지가 전달되어 데이터 불일치가 발생할 수 있습니다.  

**Option 2:** Use an SNS topic as a middle layer. Your SQS queues subscribe to this SNS topic.  
**옵션 2:** SNS 토픽을 중간 계층으로 사용합니다. SQS 큐들이 이 SNS 토픽을 구독합니다.  

When your application sends a message to the SNS topic, SNS fans out the message to all subscribed SQS queues.  
애플리케이션이 메시지를 SNS 토픽에 보내면, SNS는 이를 구독 중인 모든 SQS 큐로 전달합니다.  

This approach provides higher reliability and is a common design pattern in AWS.  
이 방식은 더 높은 신뢰성을 제공하며 AWS에서 흔히 사용되는 패턴입니다.  

---

## Amazon S3 Event Notifications  
## Amazon S3 이벤트 알림  

Amazon S3 can generate event notifications for specific bucket events such as object creation, removal, restoration, or replication.  
Amazon S3는 객체 생성, 삭제, 복원, 복제와 같은 특정 버킷 이벤트에 대해 알림을 생성할 수 있습니다.  

You can also filter events by object name.  
또한 객체 이름을 기준으로 이벤트를 필터링할 수도 있습니다.  

A typical use case is generating thumbnails for images uploaded to an S3 bucket.  
일반적인 사용 사례는 S3 버킷에 업로드된 이미지에 대한 썸네일 생성입니다.  

S3 event notifications can be sent to SNS, SQS, or Lambda functions.  
S3 이벤트 알림은 SNS, SQS 또는 Lambda 함수로 보낼 수 있습니다.  

You can create multiple event notifications as needed.  
필요에 따라 여러 이벤트 알림을 생성할 수 있습니다.  

These notifications are typically delivered within seconds, although sometimes delivery can take a minute or longer.  
이 알림은 보통 몇 초 내에 전달되지만, 때로는 1분 이상 걸릴 수도 있습니다.  

Remember these three integration options for S3 events: SNS, SQS, and Lambda.  
S3 이벤트의 3가지 통합 옵션: SNS, SQS, Lambda를 기억하세요.  

---

## Amazon EventBridge  
## Amazon EventBridge  

Amazon EventBridge is another option for event processing.  
Amazon EventBridge는 이벤트 처리를 위한 또 다른 옵션입니다.  

Events occurring in your Amazon S3 buckets are sent to EventBridge.  
Amazon S3 버킷에서 발생하는 이벤트는 EventBridge로 전송됩니다.  

Using rules, you can route these events to over 18 AWS services as destinations.  
규칙을 사용해 이 이벤트를 18개 이상의 AWS 서비스로 라우팅할 수 있습니다.  

### Why use EventBridge?  
### EventBridge를 사용하는 이유  

It provides filtering options with advanced rules, allowing filtering on metadata, object size, name, and more.  
고급 규칙을 통한 필터링 기능을 제공하여 메타데이터, 객체 크기, 이름 등으로 필터링할 수 있습니다.  

It supports sending events to multiple destinations simultaneously, such as Step Functions, Kinesis Streams, or Data Firehose.  
Step Functions, Kinesis Streams, Data Firehose와 같은 여러 대상으로 이벤트를 동시에 전송할 수 있습니다.  

EventBridge offers capabilities like archiving, replaying, and reliable delivery of events, which may be desirable for your applications.  
EventBridge는 이벤트 아카이빙, 재생, 신뢰성 있는 전달 기능을 제공하여 애플리케이션에 유용할 수 있습니다.  

---

## EventBridge and CloudTrail Integration  
## EventBridge와 CloudTrail 통합  

EventBridge can intercept any API call by integrating with AWS CloudTrail.  
EventBridge는 AWS CloudTrail과 통합하여 모든 API 호출을 가로챌 수 있습니다.  

For example, if you want to react to a user deleting a DynamoDB table using the DeleteTable API call, this call is logged in CloudTrail.  
예를 들어, 사용자가 DynamoDB 테이블을 DeleteTable API 호출로 삭제하면 이 호출은 CloudTrail에 기록됩니다.  

This log triggers an event in EventBridge, which you can use to create alerts, such as sending notifications via Amazon SNS.  
이 로그는 EventBridge에서 이벤트를 발생시키며, 이를 통해 SNS 알림 전송 같은 경고를 생성할 수 있습니다.  

---

## External Events into AWS  
## 외부 이벤트를 AWS로 통합  

You can also integrate external events into AWS using API Gateway.  
API Gateway를 사용하여 외부 이벤트를 AWS로 통합할 수도 있습니다.  

Clients send requests to the API Gateway, which then sends messages into Kinesis Data Streams.  
클라이언트가 API Gateway로 요청을 보내면, 이는 Kinesis Data Streams로 메시지를 전달합니다.  

The records can be processed by Kinesis Data Firehose and eventually stored in Amazon S3.  
이 데이터는 Kinesis Data Firehose에서 처리된 후 최종적으로 Amazon S3에 저장됩니다.  

This architecture enables you to build complex event-driven automations using various AWS services.  
이 아키텍처를 통해 다양한 AWS 서비스를 활용한 복잡한 이벤트 기반 자동화를 구축할 수 있습니다.  

---

## Conclusion  
## 결론  

We have explored various options for event processing in AWS, including SQS with Lambda, SNS with Lambda, the Fan Out pattern using SNS and SQS, S3 event notifications, EventBridge, and external event integration via API Gateway.  
이번에는 SQS+Lambda, SNS+Lambda, SNS와 SQS를 활용한 팬 아웃 패턴, S3 이벤트 알림, EventBridge, API Gateway를 통한 외부 이벤트 통합 등 AWS에서의 이벤트 처리 방안을 살펴보았습니다.  

These options provide flexible and powerful ways to build event-driven architectures and automations in AWS.  
이러한 옵션들은 AWS에서 유연하고 강력한 이벤트 기반 아키텍처와 자동화를 구축할 수 있는 방법을 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS offers multiple event processing architectures including SQS with Lambda, SNS with Lambda, and EventBridge.  
- AWS는 SQS+Lambda, SNS+Lambda, EventBridge 등 다양한 이벤트 처리 아키텍처를 제공합니다.  

- SQS queues can be configured with dead letter queues (DLQ) to handle message processing failures.  
- SQS 큐는 DLQ를 설정하여 메시지 처리 실패를 관리할 수 있습니다.  

- The Fan Out pattern using SNS topics and multiple SQS queues ensures reliable message delivery to multiple destinations.  
- SNS 토픽과 여러 SQS 큐를 활용한 팬 아웃 패턴은 메시지를 여러 대상으로 안정적으로 전달할 수 있습니다.  

- Amazon EventBridge provides advanced filtering, multiple destinations, and integration with CloudTrail for API call event monitoring.  
- Amazon EventBridge는 고급 필터링, 다중 대상 지원, CloudTrail 통합을 통한 API 호출 모니터링 기능을 제공합니다.  
```

---

게임 보상 🎮:
당신은 **AWS 이벤트 처리 마스터 배지 🏅**를 획득했습니다!
레벨업 ⬆️ → "이벤트 드리븐 아키텍트"

---
