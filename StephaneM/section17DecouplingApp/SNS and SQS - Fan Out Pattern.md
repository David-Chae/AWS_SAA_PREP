# SNS and SQS - Fan Out Pattern  
# SNS와 SQS - 팬 아웃 패턴  

---

## SNS and SQS Fan-Out Pattern  
## SNS와 SQS 팬 아웃 패턴  

Let's discuss the SNS plus SQS fan-out pattern.  
SNS와 SQS 팬 아웃 패턴에 대해 알아보겠습니다.  

The core idea is to send a message to multiple SQS queues efficiently.  
핵심 아이디어는 하나의 메시지를 여러 SQS 큐에 효율적으로 전송하는 것입니다.  

Sending messages individually to every SQS queue can lead to problems such as application crashes during delivery, delivery failures, or complications when adding more SQS queues later.  
각 SQS 큐에 메시지를 개별적으로 보내면, 전송 중 애플리케이션 충돌, 전송 실패, 또는 이후 SQS 큐를 추가할 때 복잡한 문제가 발생할 수 있습니다.  

Instead, the fan-out pattern involves pushing a single message to an SNS topic.  
대신, 팬 아웃 패턴은 하나의 메시지를 SNS 주제로 전송하는 방식입니다.  

Multiple SQS queues subscribe to this SNS topic, acting as subscribers.  
여러 SQS 큐가 이 SNS 주제를 구독자로서 구독합니다.  

All these queues receive the messages sent to the SNS topic.  
이 모든 큐는 SNS 주제로 전송된 메시지를 수신합니다.  

For example, a buying service wants to send messages to two SQS queues.  
예를 들어, 구매 서비스가 두 개의 SQS 큐로 메시지를 보내고자 합니다.  

Instead of sending messages separately, it sends one message to an SNS topic.  
메시지를 각각 보내는 대신, 하나의 메시지를 SNS 주제로 전송합니다.  

The fraud service and the shipping service each have their own SQS queues subscribed to this SNS topic, allowing them to read all messages independently.  
사기 서비스와 배송 서비스는 각자 SNS 주제를 구독하는 SQS 큐를 가지고 있으며, 이를 통해 모든 메시지를 독립적으로 읽을 수 있습니다.  

This approach provides a fully decoupled model with no data loss.  
이 접근 방식은 데이터 손실 없는 완전히 분리된 모델을 제공합니다.  

SQS offers data persistence, delayed processing, and retries.  
SQS는 데이터 영속성, 지연 처리, 재시도를 제공합니다.  

Additionally, more SQS queues can be added as subscribers to the SNS topic over time.  
추가로, 시간이 지나면서 더 많은 SQS 큐를 SNS 주제 구독자로 추가할 수 있습니다.  

To enable this, the SQS queue access policy must allow the SNS topic to write to the SQS queue.  
이를 위해 SQS 큐 접근 정책에서 SNS 주제가 큐에 메시지를 쓸 수 있도록 허용해야 합니다.  

This is another use case for queue access policies.  
이는 큐 접근 정책의 또 다른 활용 사례입니다.  

Moreover, cross-region delivery is possible, where an SNS topic in one region can send messages to SQS queues in other regions if security policies permit.  
또한, 교차 리전 전송도 가능하며, 보안 정책이 허용되는 경우 한 리전의 SNS 주제가 다른 리전의 SQS 큐로 메시지를 보낼 수 있습니다.  

---

## Using Fan-Out Pattern for S3 Events  
## S3 이벤트에 팬 아웃 패턴 사용  

S3 event rules have limitations; for example, for a combination of event type and prefix, only one S3 event rule can exist.  
S3 이벤트 규칙에는 제한이 있습니다. 예를 들어, 이벤트 유형과 접두어 조합에 대해 하나의 S3 이벤트 규칙만 존재할 수 있습니다.  

To send the same S3 event notification to multiple SQS queues, the fan-out pattern is used.  
동일한 S3 이벤트 알림을 여러 SQS 큐로 보내려면 팬 아웃 패턴을 사용합니다.  

When an S3 object is created, the event is sent to an SNS topic.  
S3 객체가 생성되면 이벤트가 SNS 주제로 전송됩니다.  

Multiple SQS queues subscribe to this SNS topic.  
여러 SQS 큐가 이 SNS 주제를 구독합니다.  

Other types of applications, such as email or Lambda functions, can also subscribe.  
이메일이나 Lambda 함수와 같은 다른 유형의 애플리케이션도 구독할 수 있습니다.  

This allows the event message from Amazon S3 to reach many destinations through the fan-out pattern.  
이를 통해 Amazon S3의 이벤트 메시지가 팬 아웃 패턴을 통해 여러 목적지에 도달할 수 있습니다.  

Another architecture involves sending data directly from SNS to Amazon S3 via Kinesis Data Firehose (KDF).  
또 다른 아키텍처는 SNS에서 Kinesis Data Firehose(KDF)를 통해 Amazon S3로 데이터를 직접 전송하는 방식입니다.  

SNS integrates directly with KDF, so a buying service can send data to an SNS topic, which KDF receives and then delivers to an Amazon S3 bucket or any supported KDF destination.  
SNS는 KDF와 직접 통합되므로, 구매 서비스가 SNS 주제로 데이터를 전송하면 KDF가 이를 수신하여 Amazon S3 버킷이나 지원되는 KDF 목적지로 전달합니다.  

This provides extensibility for persisting messages from SNS topics.  
이를 통해 SNS 주제의 메시지를 저장할 수 있는 확장성을 제공합니다.  

---

## Fan-Out Pattern with FIFO Topics  
## FIFO 주제와 팬 아웃 패턴  

SNS supports FIFO (First-In-First-Out) topics, which maintain message ordering.  
SNS는 메시지 순서를 유지하는 FIFO(선입선출) 주제를 지원합니다.  

Producers send messages in order (e.g., one, two, three, four), and subscribers, which must be SQS FIFO queues, receive messages in the same order.  
생산자가 메시지를 순서대로 보내면(예: one, two, three, four), 구독자(SQS FIFO 큐)는 같은 순서로 메시지를 수신합니다.  

SNS FIFO topics provide features such as ordering by message group ID and deduplication using a deduplication ID or content-based deduplication.  
SNS FIFO 주제는 메시지 그룹 ID별 순서 보장 및 deduplication ID나 콘텐츠 기반 중복 제거 기능을 제공합니다.  

Both SQS standard and FIFO queues can subscribe, but throughput is limited to that of the SQS FIFO queue.  
SQS 표준 큐와 FIFO 큐 모두 구독할 수 있지만, 처리량은 SQS FIFO 큐의 제한을 받습니다.  

This is useful when fan-out with ordering and deduplication is required.  
순서와 중복 제거가 필요한 팬 아웃 시 유용합니다.  

For example, a buying service sends data to an SNS FIFO topic, which fans out to two SQS FIFO queues.  
예를 들어, 구매 서비스가 SNS FIFO 주제로 데이터를 보내면, 두 개의 SQS FIFO 큐로 팬 아웃됩니다.  

The fraud service and shipping service read from these FIFO queues, preserving order and deduplication.  
사기 서비스와 배송 서비스는 이 FIFO 큐에서 메시지를 읽어 순서와 중복 제거를 유지합니다.  

---

## Message Filtering in SNS  
## SNS에서 메시지 필터링  

SNS supports message filtering, which uses JSON policies to filter messages sent to topic subscriptions.  
SNS는 JSON 정책을 사용하여 주제 구독으로 전송되는 메시지를 필터링하는 메시지 필터링을 지원합니다.  

If a subscription has no filter policy, it receives every message by default.  
구독에 필터 정책이 없으면 기본적으로 모든 메시지를 수신합니다.  

For example, a buying service sends transactions to an SNS topic.  
예를 들어, 구매 서비스가 트랜잭션을 SNS 주제로 전송합니다.  

Each transaction includes fields such as order number, product (e.g., pencil), quantity, and state (e.g., placed).  
각 트랜잭션에는 주문 번호, 상품(예: 연필), 수량, 상태(예: placed)와 같은 필드가 포함됩니다.  

To create an SQS queue that receives only placed orders, the queue subscribes to the SNS topic with a filter policy specifying that the state equals "Placed".  
placed 상태인 주문만 수신하도록 SQS 큐를 만들려면, 큐가 SNS 주제를 구독하고 상태가 "Placed"인 메시지만 수신하도록 필터 정책을 지정합니다.  

Only messages matching the filter policy are delivered to that SQS queue.  
필터 정책과 일치하는 메시지만 해당 SQS 큐로 전달됩니다.  

Similarly, another SQS queue can be created for canceled orders with a corresponding filter policy.  
마찬가지로, 취소된 주문용 SQS 큐도 해당 필터 정책과 함께 생성할 수 있습니다.  

These queues receive distinct messages from the same SNS topic.  
이 큐들은 같은 SNS 주제에서 서로 다른 메시지를 수신합니다.  

Filter policies can also be applied to other subscription types, such as email for canceled orders.  
필터 정책은 취소된 주문 이메일과 같은 다른 구독 유형에도 적용할 수 있습니다.  

Additional filters can be created for declined orders or other states.  
거부된 주문이나 다른 상태에 대한 추가 필터도 생성할 수 있습니다.  

An SQS queue without a filter policy will receive all messages from the SNS topic.  
필터 정책이 없는 SQS 큐는 SNS 주제의 모든 메시지를 수신합니다.  

Using fan-out patterns, message filtering, FIFO queues, and FIFO topics, many different architectures and use cases are possible.  
팬 아웃 패턴, 메시지 필터링, FIFO 큐 및 FIFO 주제를 사용하면 다양한 아키텍처와 사용 사례가 가능합니다.  

These concepts are important and may be tested in exams.  
이러한 개념은 중요하며 시험에서 출제될 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- The SNS plus SQS fan-out pattern allows sending a single message to multiple SQS queues by subscribing them to an SNS topic.  
- SNS와 SQS 팬 아웃 패턴을 사용하면 하나의 메시지를 여러 SQS 큐에 보내기 위해 SNS 주제에 구독시킬 수 있습니다.  

- This pattern ensures a fully decoupled model with no data loss, supporting data persistence, delayed processing, and retries.  
- 이 패턴은 데이터 손실 없는 완전히 분리된 모델을 보장하며, 데이터 영속성, 지연 처리, 재시도를 지원합니다.  

- SNS topics can integrate with various subscribers including SQS queues, Lambda functions, email, and Kinesis Data Firehose for extensible message delivery.  
- SNS 주제는 SQS 큐, Lambda 함수, 이메일, Kinesis Data Firehose 등 다양한 구독자와 통합되어 확장 가능한 메시지 전달을 제공합니다.  

- Message filtering in SNS enables selective delivery to subscribers based on JSON filter policies, enhancing message routing efficiency.  
- SNS의 메시지 필터링은 JSON 필터 정책 기반으로 구독자에게 선택적 메시지 전달을 가능하게 하여 메시지 라우팅 효율성을 높입니다.  
