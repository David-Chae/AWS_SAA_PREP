# SQS and Auto Scaling Group Integration  
# SQS와 오토 스케일링 그룹 통합  

---

## Introduction to SQS and Auto Scaling Groups  
## SQS와 오토 스케일링 그룹 소개  

We can use the SQS queue in conjunction with Auto Scaling Groups (ASG).  
SQS 큐를 오토 스케일링 그룹(ASG)과 함께 사용할 수 있습니다.  

This integration opens up several useful patterns.  
이 통합은 여러 가지 유용한 패턴을 가능하게 합니다.  

Essentially, we have an SQS queue and an Auto Scaling Group.  
기본적으로 우리는 SQS 큐와 오토 스케일링 그룹을 갖게 됩니다.  

The EC2 instances within the ASG poll for messages from the SQS queue.  
ASG 내의 EC2 인스턴스가 SQS 큐에서 메시지를 가져옵니다.  

The main idea is to scale the Auto Scaling Group automatically based on the size of the queue.  
핵심 개념은 큐의 크기에 따라 오토 스케일링 그룹을 자동으로 확장 또는 축소하는 것입니다.  

We monitor the CloudWatch metric called the approximate number of messages, which represents how many messages remain in the queue.  
우리는 CloudWatch 지표인 **ApproximateNumberOfMessages**(대략적인 메시지 수)를 모니터링하는데, 이는 큐에 남아 있는 메시지 개수를 나타냅니다.  

You can set an alarm such that if this metric exceeds a threshold—for example, 1,000 messages—this indicates a backlog in processing.  
이 지표가 임계값(예: 1,000개 메시지)을 초과하면 처리 지연이 발생했음을 알리는 알람을 설정할 수 있습니다.  

When the alarm triggers, it initiates a scaling action in your Auto Scaling Group.  
알람이 트리거되면 오토 스케일링 그룹에서 스케일링 작업이 시작됩니다.  

This means more EC2 instances will be added to the group to handle the increased load.  
즉, 증가한 부하를 처리하기 위해 더 많은 EC2 인스턴스가 그룹에 추가됩니다.  

As a result, messages will be processed faster, reducing the queue size.  
그 결과 메시지가 더 빠르게 처리되어 큐 크기가 줄어듭니다.  

This scaling works both ways: you can scale up or scale down based on the queue length.  
이 스케일링은 양방향으로 작동하여 큐 길이에 따라 확장(Scale up) 또는 축소(Scale down)가 가능합니다.  

---

## Patterns Enabled by SQS and Auto Scaling  
## SQS와 오토 스케일링으로 가능한 패턴들  

Consider a scenario where you are running a major sales campaign, the biggest marketing campaign you have ever done.  
예를 들어, 가장 큰 마케팅 캠페인인 대규모 세일 캠페인을 진행한다고 가정합시다.  

All your customers will place orders, which need to be stored in databases.  
모든 고객들이 주문을 넣으며, 이 주문은 데이터베이스에 저장되어야 합니다.  

These databases could be Amazon RDS or Amazon Aurora for OLTP workloads, or Amazon DynamoDB if you prefer a NoSQL database.  
데이터베이스는 OLTP 워크로드에 적합한 Amazon RDS 또는 Amazon Aurora일 수 있고, NoSQL 데이터베이스가 필요하다면 Amazon DynamoDB일 수도 있습니다.  

During sudden spikes, transactions may be written very quickly into these databases.  
갑작스러운 트래픽 급증 시, 트랜잭션이 매우 빠르게 데이터베이스에 기록될 수 있습니다.  

Your application can handle requests, but if the databases become overloaded, errors may occur, causing loss of customer transactions, which is detrimental to your business.  
애플리케이션은 요청을 처리할 수 있지만 데이터베이스가 과부하되면 오류가 발생하여 고객 트랜잭션이 손실될 수 있으며, 이는 비즈니스에 치명적입니다.  

---

## Using SQS as a Buffer for Database Writes  
## 데이터베이스 쓰기를 위한 버퍼로서의 SQS  

To solve this problem, we can use SQS as a buffer for database writes.  
이 문제를 해결하기 위해 SQS를 데이터베이스 쓰기의 버퍼로 사용할 수 있습니다.  

This is a common exam pattern.  
이는 시험에서 자주 등장하는 패턴입니다.  

Instead of writing transactions directly into the database, the application writes transaction requests into the SQS queue.  
트랜잭션을 데이터베이스에 직접 기록하는 대신, 애플리케이션은 트랜잭션 요청을 SQS 큐에 기록합니다.  

AWS defines SQS as infinitely scalable and free from throughput issues.  
AWS는 SQS를 **무한 확장 가능하며 처리량 문제에서 자유로운 서비스**로 정의합니다.  

The requests enter your application and are enqueued as messages in the SQS queue.  
요청은 애플리케이션에 들어와 SQS 큐에 메시지로 저장됩니다.  

This guarantees that no transaction is lost, as all messages are durably stored in the queue.  
모든 메시지가 큐에 내구성 있게 저장되므로, 트랜잭션이 손실되지 않음을 보장합니다.  

We can create another Auto Scaling Group whose sole role is to dequeue messages and insert them into the databases.  
메시지를 큐에서 꺼내 데이터베이스에 삽입하는 전용 오토 스케일링 그룹을 만들 수 있습니다.  

Only when a message is confirmed to be inserted into the database do we delete it from the original SQS queue.  
메시지가 데이터베이스에 삽입되었음이 확인될 때만 원래 SQS 큐에서 해당 메시지를 삭제합니다.  

This pattern ensures every transaction is eventually written to the database.  
이 패턴은 모든 트랜잭션이 결국 데이터베이스에 기록되도록 보장합니다.  

This pattern works well if the client does not require immediate confirmation that the write has occurred in the database.  
클라이언트가 데이터베이스에 쓰기가 즉시 완료되었다는 확인을 요구하지 않을 때 이 패턴이 잘 작동합니다.  

Since the write to the SQS queue guarantees eventual database insertion, this approach provides reliability and decouples the application from the database write latency.  
SQS 큐에 기록된 메시지는 결국 데이터베이스에 삽입되므로, 이 접근법은 신뢰성을 보장하며 애플리케이션을 데이터베이스 쓰기 지연으로부터 분리합니다.  

---

## Decoupling Application Tiers with SQS  
## SQS를 통한 애플리케이션 계층 분리  

SQS also enables decoupling between application tiers.  
SQS는 애플리케이션 계층 간의 분리도 가능하게 합니다.  

For example, an application might receive a request, perform some processing, and send back a response.  
예를 들어, 애플리케이션이 요청을 받고 일부 처리를 수행한 뒤 응답을 반환할 수 있습니다.  

Instead, you can decouple this by having all requests come into a front-end web application, which sends the requests into an SQS queue.  
대신 모든 요청을 프런트엔드 웹 애플리케이션이 받아서 이를 SQS 큐에 넣도록 하여 계층을 분리할 수 있습니다.  

The backend processing jobs then receive these messages and handle them asynchronously at their own pace.  
백엔드 처리 작업은 이 메시지를 받아 비동기적으로 자체 속도에 맞게 처리합니다.  

This setup allows you to scale the backend processing independently and efficiently.  
이 방식은 백엔드 처리를 독립적이고 효율적으로 확장할 수 있도록 합니다.  

---

## Conclusion  
## 결론  

SQS is a very common and powerful tool for handling decoupling, sudden spikes in load, timeouts, and scaling requirements.  
SQS는 계층 분리, 갑작스러운 부하 증가, 타임아웃, 스케일링 요구 사항을 처리하는 데 매우 일반적이고 강력한 도구입니다.  

When you need to scale quickly and reliably, especially in exam scenarios, consider using an SQS queue.  
빠르고 안정적으로 확장이 필요할 때, 특히 시험 시나리오에서, SQS 큐 사용을 고려해야 합니다.  

---

## Key Takeaways  
## 핵심 요약  

SQS queues can be integrated with Auto Scaling Groups to automatically scale EC2 instances based on queue size.  
SQS 큐는 오토 스케일링 그룹과 통합되어 큐 크기에 따라 EC2 인스턴스를 자동으로 확장할 수 있습니다.  

CloudWatch metrics like approximate number of messages in the queue can trigger alarms to scale resources up or down.  
CloudWatch 지표(큐 내 대략적인 메시지 수 등)를 기반으로 알람을 트리거하여 리소스를 확장하거나 축소할 수 있습니다.  

Using SQS as a buffer between applications and databases prevents data loss during high transaction loads.  
SQS를 애플리케이션과 데이터베이스 사이의 버퍼로 사용하면 높은 트랜잭션 부하 중에도 데이터 손실을 방지할 수 있습니다.  

Decoupling application tiers with SQS allows for scalable, asynchronous processing of requests.  
SQS를 통한 애플리케이션 계층 분리는 요청의 확장 가능하고 비동기적인 처리를 가능하게 합니다. 
