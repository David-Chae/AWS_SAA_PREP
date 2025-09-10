# SQS vs SNS vs Kinesis  
# SQS vs SNS vs Kinesis  

---

## Understanding the Differences Between SQS, SNS, and Kinesis  
## SQS, SNS, Kinesis의 차이 이해하기  

It is very important to understand the differences between SQS, SNS, and Kinesis.  
SQS, SNS, Kinesis의 차이를 이해하는 것은 매우 중요합니다.  

---

## Amazon SQS (Simple Queue Service)  
## 아마존 SQS (Simple Queue Service)  

SQS operates on a model where consumers pull data by requesting messages from the SQS queue.  
SQS는 소비자가 SQS 큐에서 메시지를 요청하여 데이터를 가져오는 풀 모델로 작동합니다.  

Once the data is processed, the consumer must delete it from the queue so that no other consumers can read it again.  
데이터 처리 후, 소비자는 다른 소비자가 다시 읽지 못하도록 큐에서 데이터를 삭제해야 합니다.  

You can have as many workers or consumers as you want, and they all work together to consume and delete all the messages from the queue.  
원하는 만큼 워커나 소비자를 둘 수 있으며, 모든 소비자가 함께 메시지를 처리하고 삭제합니다.  

You do not need to provision throughput in advance because it is a managed service that can scale to hundreds of thousands of messages very quickly.  
SQS는 관리형 서비스로 수십만 개 메시지까지 빠르게 확장 가능하므로 사전에 처리량을 설정할 필요가 없습니다.  

Ordering guarantees are available only if you enable FIFO queues, which provide first-in, first-out ordering.  
FIFO 큐를 활성화해야만 메시지 순서 보장이 제공되며, FIFO는 선입선출 순서를 의미합니다.  

Additionally, SQS supports individual message delay capability, allowing a message to appear to a consumer in the queue after a specified delay, for example, 30 seconds.  
또한 SQS는 개별 메시지 지연 기능을 지원하여, 예를 들어 30초 후에 메시지가 소비자에게 나타나도록 설정할 수 있습니다.  

---

## Amazon SNS (Simple Notification Service)  
## 아마존 SNS (Simple Notification Service)  

SNS follows a different model known as the publish-subscribe (pub-sub) model.  
SNS는 퍼블리시-서브스크라이브(pub-sub) 모델을 따릅니다.  

In this model, you push data to many subscribers, and they all receive a copy of the message you send.  
이 모델에서는 데이터를 여러 구독자에게 푸시하고, 모든 구독자가 메시지 사본을 받습니다.  

SNS supports up to 12,500,000 subscribers per topic.  
SNS는 토픽당 최대 12,500,000명의 구독자를 지원합니다.  

Once data is sent to SNS, it is not persistent, meaning that if the message is not delivered, there is a chance of losing it.  
데이터가 SNS로 전송되면 영구 저장되지 않으므로, 메시지가 전달되지 않으면 손실될 수 있습니다.  

SNS can scale to hundreds of thousands of topics, and like SQS, you do not need to provision throughput in advance.  
SNS는 수십만 개 토픽까지 확장 가능하며, SQS처럼 사전에 처리량을 설정할 필요가 없습니다.  

You can combine SNS with SQS using the fan-out architecture pattern.  
SNS를 SQS와 결합하여 팬아웃(fan-out) 아키텍처 패턴을 사용할 수 있습니다.  

This allows you to combine SNS with SQS or SNS FIFO topics with SQS FIFO queues.  
이를 통해 SNS와 SQS 또는 SNS FIFO 토픽과 SQS FIFO 큐를 결합할 수 있습니다.  

---

## Amazon Kinesis  
## 아마존 Kinesis  

Kinesis offers two modes of consumption:  
Kinesis는 두 가지 데이터 소비 모드를 제공합니다.  

**Standard mode**: Consumers pull data from Kinesis, with a throughput of two megabytes per second per shard.  
**표준 모드**: 소비자가 Kinesis에서 데이터를 풀로 가져오며, 샤드당 초당 2MB 처리량을 제공합니다.  

**Enhanced fan-out mode**: Kinesis pushes data to consumers, providing two megabytes per second per shard per consumer.  
**향상된 팬아웃 모드**: Kinesis가 데이터를 소비자에게 푸시하며, 샤드당 소비자당 초당 2MB 처리량을 제공합니다.  

This mode offers much higher throughput and allows more applications to read from your Kinesis stream.  
이 모드는 훨씬 높은 처리량을 제공하며, 더 많은 애플리케이션이 Kinesis 스트림에서 데이터를 읽을 수 있습니다.  

Kinesis stores data persistently with the new Kinesis Data Streams, enabling replay of data.  
Kinesis는 데이터를 지속적으로 저장하며, Kinesis Data Streams를 통해 데이터 재생(replay)을 지원합니다.  

It is typically used for real-time big data analytics and ETL (Extract, Transform, Load) processes.  
주로 실시간 빅데이터 분석 및 ETL(추출, 변환, 적재) 프로세스에 사용됩니다.  

Ordering is guaranteed at the shard level.  
순서는 샤드 단위로 보장됩니다.  

You must specify the number of shards per Kinesis data stream in advance, which means you need to scale shards yourself.  
각 Kinesis 데이터 스트림의 샤드 수를 미리 지정해야 하므로 샤드를 직접 확장해야 합니다.  

Data expires after a configurable retention period, which ranges from one to 365 days at the time of recording.  
데이터는 설정 가능한 보존 기간 후 만료되며, 기록 시점 기준 1일부터 365일까지 가능합니다.  

Regarding capacity modes, Kinesis supports:  
Kinesis는 용량 모드로 다음을 지원합니다.  

**Provisioned mode**: You specify the number of shards in advance.  
**프로비저닝 모드**: 샤드 수를 미리 지정합니다.  

**On-demand capacity mode**: The number of shards is adjusted automatically by Kinesis Data Streams.  
**온디맨드 모드**: 샤드 수가 Kinesis Data Streams에 의해 자동으로 조정됩니다.  

---

## Summary  
## 요약  

This concludes the lecture on SQS, SNS, and Kinesis.  
이로써 SQS, SNS, Kinesis 강의를 마칩니다.  

Understanding these services and their differences is crucial for designing scalable and efficient data processing architectures.  
이 서비스들과 그 차이를 이해하는 것은 확장 가능하고 효율적인 데이터 처리 아키텍처를 설계하는 데 중요합니다.  

---

## Key Takeaways  
## 핵심 요약  

- SQS uses a pull model where consumers request and delete messages, supporting multiple consumers working together without needing to provision throughput.  
- SQS는 소비자가 메시지를 요청하고 삭제하는 풀 모델을 사용하며, 여러 소비자가 협력하여 처리할 수 있고 사전 처리량 설정이 필요 없습니다.  

- SNS operates on a pub-sub model, pushing messages to many subscribers, with high scalability but no message persistence.  
- SNS는 퍼블리시-서브스크라이브 모델을 사용하며, 많은 구독자에게 메시지를 푸시하고 높은 확장성을 제공하지만 메시지는 영구 저장되지 않습니다.  

- Kinesis supports both pull and push consumption modes, offers data persistence, ordering at shard level, and requires shard provisioning or can operate on-demand.  
- Kinesis는 풀 및 푸시 소비 모드를 모두 지원하며, 데이터 영구 저장, 샤드 단위 순서 보장 기능을 제공하며 샤드 수를 사전 지정하거나 온디맨드로 운영할 수 있습니다.  

- Combining SNS with SQS enables fan-out architectures, and Kinesis is suited for real-time big data analytics and ETL workloads.  
- SNS와 SQS를 결합하면 팬아웃 아키텍처를 구현할 수 있으며, Kinesis는 실시간 빅데이터 분석 및 ETL 워크로드에 적합합니다.  
