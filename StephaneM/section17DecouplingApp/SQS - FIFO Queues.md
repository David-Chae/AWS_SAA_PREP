# SQS - FIFO Queues  
# SQS - FIFO 큐  

---

## Introduction to Amazon SQS FIFO Queues  
## Amazon SQS FIFO 큐 소개  

Amazon's SQS FIFO queues ensure that messages are processed in the exact order they are sent.  
Amazon의 SQS FIFO 큐는 메시지가 전송된 정확한 순서대로 처리되도록 보장합니다.  

FIFO stands for "first in, first out," which corresponds to the ordering of messages in the queue.  
FIFO는 "선입선출(First In, First Out)"을 의미하며, 큐에서 메시지가 처리되는 순서를 나타냅니다.  

When a producer sends messages in a specific order, such as one, two, three, four, the consumer polling messages from the SQS FIFO queue will receive these messages in the same order.  
프로듀서가 메시지를 1, 2, 3, 4 순서로 전송하면, SQS FIFO 큐에서 메시지를 가져오는 소비자는 동일한 순서로 메시지를 받습니다.  

This ordering guarantee is a key feature of FIFO queues.  
이 순서 보장은 FIFO 큐의 핵심 기능입니다.  

In contrast, regular SQS queues do not guarantee message order; messages can be received out of order.  
반면, 일반 SQS 큐는 메시지 순서를 보장하지 않으며, 메시지가 뒤섞여 도착할 수 있습니다.  

Due to the ordering guarantee in FIFO queues, there are throughput limits: about 300 messages per second without batching and 3,000 messages per second with batching.  
FIFO 큐의 순서 보장 기능 때문에 처리량 제한이 있습니다: 배치 없이 초당 약 300개의 메시지, 배치 시 초당 약 3,000개의 메시지입니다.  

---

## Exactly-Once Message Delivery and Deduplication  
## 정확히 한 번의 메시지 전송과 중복 제거  

FIFO queues also support exactly-once message delivery.  
FIFO 큐는 메시지를 정확히 한 번만 전달하는 기능을 지원합니다.  

This means duplicates can be removed directly at the queue level.  
즉, 큐 수준에서 중복 메시지를 직접 제거할 수 있습니다.  

To enable this, each message sent must include a deduplication ID.  
이를 위해 각 메시지에는 **중복 제거 ID(deduplication ID)** 가 포함되어야 합니다.  

If the same deduplication ID is seen twice within a five-minute window, duplicates are removed automatically.  
같은 중복 제거 ID가 5분 이내에 두 번 나타나면, 중복 메시지가 자동으로 제거됩니다.  

This feature is very useful to ensure no duplicate messages are processed within that time frame.  
이 기능은 해당 시간 동안 중복 메시지가 처리되지 않도록 보장하는 데 매우 유용합니다.  

---

## Message Group ID and Ordering Guarantee  
## 메시지 그룹 ID와 순서 보장  

Messages are processed in order by the consumer, and the ordering guarantee applies at the message group ID level.  
메시지는 소비자에 의해 순서대로 처리되며, 순서 보장은 메시지 그룹 ID 수준에서 적용됩니다.  

Every message sent to an Amazon SQS FIFO queue must include a message group ID.  
Amazon SQS FIFO 큐에 전송되는 모든 메시지에는 **메시지 그룹 ID**가 포함되어야 합니다.  

All messages with the same message group ID are guaranteed to be processed in order.  
같은 메시지 그룹 ID를 가진 메시지는 순서대로 처리될 것이 보장됩니다.  

This allows for ordered processing within groups while enabling parallel processing across different groups.  
이 방식은 그룹 내에서 순서 처리를 보장하면서도, 다른 그룹 간에는 병렬 처리를 가능하게 합니다.  

---

## Creating a FIFO Queue in the AWS Console  
## AWS 콘솔에서 FIFO 큐 생성하기  

Let's explore how FIFO queues work in the AWS console.  
AWS 콘솔에서 FIFO 큐가 어떻게 동작하는지 살펴봅시다.  

To create a FIFO queue, navigate to the SQS service and create a new queue.  
FIFO 큐를 생성하려면, SQS 서비스로 이동해 새 큐를 생성합니다.  

Select the FIFO queue option, which ensures first-in-first-out delivery and preserves message ordering.  
FIFO 큐 옵션을 선택하면 선입선출 전달과 메시지 순서 보장이 활성화됩니다.  

When naming the queue, it must end with the suffix .fifo. For example, DemoQueue.fifo.  
큐 이름을 지정할 때 반드시 **.fifo** 접미사로 끝나야 합니다. 예: `DemoQueue.fifo`.  

This suffix is mandatory to create a FIFO queue.  
이 접미사는 FIFO 큐를 생성하기 위해 필수적입니다.  

The configuration options for FIFO queues are similar to standard queues, with one additional setting called content-based deduplication.  
FIFO 큐의 설정 옵션은 표준 큐와 비슷하지만, **콘텐츠 기반 중복 제거(content-based deduplication)** 라는 추가 설정이 있습니다.  

This option deduplicates messages if the same content is sent twice within a five-minute window.  
이 옵션은 동일한 콘텐츠가 5분 내에 두 번 전송되면 메시지를 자동으로 중복 제거합니다.  

Other settings such as access policy and encryption remain the same.  
접근 정책이나 암호화와 같은 다른 설정은 동일하게 유지됩니다.  

---

## Sending Messages to the FIFO Queue  
## FIFO 큐에 메시지 보내기  

After creating the queue, you can send messages.  
큐를 생성한 후 메시지를 전송할 수 있습니다.  

Each message requires a message group ID and a deduplication ID.  
각 메시지에는 **메시지 그룹 ID**와 **중복 제거 ID**가 필요합니다.  

For this demonstration, we use the message group ID demo for all messages.  
이 데모에서는 모든 메시지에 메시지 그룹 ID로 `demo`를 사용합니다.  

For example, send the message "Hello World 1" with deduplication ID ID1, then "Hello World 2" with deduplication ID ID2, and so forth for subsequent messages.  
예를 들어, "Hello World 1" 메시지를 `ID1` 중복 제거 ID와 함께 보내고, "Hello World 2"를 `ID2`와 함께 보내며, 이후 메시지도 같은 방식으로 전송합니다.  

---

## Receiving Messages and Order Verification  
## 메시지 수신 및 순서 검증  

Once messages are sent, they are ready to be received.  
메시지가 전송되면, 수신할 준비가 됩니다.  

If you pull four messages from the queue, you will observe that the messages are received in the exact order they were sent:  
큐에서 네 개의 메시지를 가져오면, 메시지가 전송된 정확한 순서대로 수신됨을 확인할 수 있습니다:  

First message: "Hello World 1"  
첫 번째 메시지: "Hello World 1"  

Second message: "Hello World 2"  
두 번째 메시지: "Hello World 2"  

Third message: "Hello World 3"  
세 번째 메시지: "Hello World 3"  

Fourth message: "Hello World 4"  
네 번째 메시지: "Hello World 4"  

This ordering is guaranteed by the FIFO queue.  
이 순서는 FIFO 큐에 의해 보장됩니다.  

After processing, you can delete the messages from the queue.  
처리가 끝난 후 메시지를 큐에서 삭제할 수 있습니다.  

This concludes the demonstration of FIFO queue functionality.  
이것으로 FIFO 큐 기능에 대한 데모가 마무리됩니다.  

---

## Conclusion  
## 결론  

Amazon SQS FIFO queues provide reliable, ordered message delivery with exactly-once processing capabilities.  
Amazon SQS FIFO 큐는 신뢰할 수 있는 순차적 메시지 전달과 **정확히 한 번 처리** 기능을 제공합니다.  

They are suitable for applications that require strict message ordering and deduplication.  
이는 엄격한 메시지 순서와 중복 제거가 필요한 애플리케이션에 적합합니다.  

---

## Key Takeaways  
## 핵심 요약  

Amazon SQS FIFO queues guarantee first-in, first-out message ordering.  
Amazon SQS FIFO 큐는 선입선출 메시지 순서를 보장합니다.  

FIFO queues support exactly-once message delivery using deduplication IDs.  
FIFO 큐는 **중복 제거 ID**를 사용해 정확히 한 번의 메시지 전송을 지원합니다.  

Message ordering is maintained within each message group ID.  
메시지 순서는 각 메시지 그룹 ID 내에서 유지됩니다.  

FIFO queues have throughput limits: approximately 300 messages per second without batching and 3,000 with batching.  
FIFO 큐에는 처리량 제한이 있으며, 배치 없이 초당 약 300개, 배치 시 초당 약 3,000개의 메시지를 지원합니다.  
