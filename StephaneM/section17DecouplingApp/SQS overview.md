# Amazon SQS - Standard Queues Overview  
# 아마존 SQS - 표준 큐 개요  

---

## Introduction to Amazon SQS  
## 아마존 SQS 소개  

Amazon Simple Queue Service (SQS) is a simple queuing service where the core component is a queue.  
아마존 SQS(Simple Queue Service)는 핵심 구성 요소가 큐인 단순한 메시지 큐 서비스입니다.  

An SQS queue contains messages that are sent by producers.  
SQS 큐는 생산자가 보낸 메시지를 담습니다.  

Producers can be one or multiple entities sending messages into the SQS queue.  
생산자는 하나 또는 여러 개체가 될 수 있으며, 메시지를 SQS 큐로 전송합니다.  

These messages can be any instructions or data, such as "process this order" or "process this video."  
메시지는 “이 주문을 처리해라” 또는 “이 영상을 처리해라” 같은 지시나 데이터일 수 있습니다.  

Consumers are the entities that process messages from the queue.  
소비자는 큐에서 메시지를 가져와 처리하는 개체입니다.  

They poll the queue by asking if there are any messages available.  
소비자는 메시지가 있는지 큐에 요청(poll)합니다.  

If messages exist, the queue returns them to the consumer.  
메시지가 있으면 큐는 그것을 소비자에게 반환합니다.  

The consumer then processes the message and deletes it from the queue.  
소비자는 메시지를 처리한 후 큐에서 삭제합니다.  

Multiple consumers can consume messages from the same SQS queue, enabling parallel processing.  
여러 소비자가 같은 SQS 큐에서 메시지를 처리할 수 있어 병렬 처리가 가능합니다.  

The queuing service acts as a buffer to decouple producers and consumers, allowing them to operate independently.  
큐 서비스는 생산자와 소비자를 분리하는 버퍼 역할을 하여 독립적으로 동작할 수 있게 합니다.  

Amazon SQS is a fully managed service and one of the oldest services on AWS, with over 10 years of operation.  
아마존 SQS는 완전관리형 서비스이며, AWS에서 10년 이상 운영된 가장 오래된 서비스 중 하나입니다.  

It is primarily used for application decoupling, a key concept in AWS architecture.  
이는 AWS 아키텍처의 핵심 개념인 애플리케이션 분리에 주로 사용됩니다.  

---

## Features of Amazon SQS Standard Queues  
## 아마존 SQS 표준 큐의 특징  

Amazon SQS standard queues provide unlimited throughput...  
아마존 SQS 표준 큐는 무제한 처리량을 제공하며...  

(여기서는 메시지 무제한 저장, 최대 14일 보관, 낮은 지연시간 <10ms, 메시지 크기 256KB 제한, 최소 1회 이상 전달, 순서 보장은 최선 노력(best-effort)임 등을 설명)  

---

## Message Production and Consumption  
## 메시지 생산과 소비  

Producers send messages up to 256 kilobytes into SQS queues using SDKs.  
생산자는 SDK를 사용하여 최대 256KB 메시지를 SQS 큐에 보냅니다.  

The API used to send messages is called SendMessage.  
메시지를 보내는 데 사용되는 API는 **SendMessage**입니다.  

Messages are persisted in the queue until a consumer reads and deletes them.  
메시지는 소비자가 읽고 삭제할 때까지 큐에 저장됩니다.  

Consumers poll the queue using the ReceiveMessage API.  
소비자는 **ReceiveMessage** API를 사용하여 큐에서 메시지를 가져옵니다.  

They can receive up to 10 messages at a time.  
한 번에 최대 10개의 메시지를 받을 수 있습니다.  

After processing, consumers delete messages using the DeleteMessage API.  
처리 후 소비자는 **DeleteMessage** API로 메시지를 삭제합니다.  

Multiple consumers can process messages in parallel, improving throughput and scalability.  
여러 소비자가 병렬로 메시지를 처리할 수 있어 처리량과 확장성이 향상됩니다.  

---

## Scaling Consumers with Auto Scaling Groups  
## 오토 스케일링 그룹을 통한 소비자 확장  

To handle increased volume, consumers can scale horizontally.  
메시지 양이 증가하면 소비자는 수평 확장할 수 있습니다.  

Consumers on EC2 can be managed by Auto Scaling Groups (ASG).  
EC2 인스턴스에서 실행되는 소비자는 **Auto Scaling Group(ASG)**으로 관리할 수 있습니다.  

Scaling can be based on queue length metric (ApproximateNumberOfMessages).  
스케일링은 큐 길이 지표(ApproximateNumberOfMessages)에 따라 결정됩니다.  

CloudWatch alarms can trigger ASG to increase/decrease consumer instances dynamically.  
CloudWatch 알람을 통해 ASG가 소비자 인스턴스를 동적으로 늘리거나 줄일 수 있습니다.  

---

## Application Decoupling Use Case  
## 애플리케이션 분리 활용 사례  

Example: A video processing application.  
예시: 비디오 처리 애플리케이션.  

- Front-end receives requests and sends messages to SQS.  
프론트엔드는 요청을 받아 메시지를 SQS에 보냅니다.  

- Back-end consumes messages, processes videos, and stores in S3.  
백엔드는 메시지를 소비하고 비디오를 처리해 S3에 저장합니다.  

➡️ This allows independent scaling of front-end and back-end tiers.  
➡️ 이를 통해 프론트엔드와 백엔드를 독립적으로 확장할 수 있습니다.  

---

## Security Features of Amazon SQS  
## 아마존 SQS의 보안 기능  

- In-flight encryption: HTTPS.  
전송 중 암호화: HTTPS 사용.  

- At-rest encryption: AWS KMS.  
저장 시 암호화: AWS KMS 사용.  

- Client-side encryption supported manually.  
클라이언트 측 암호화는 직접 구현 가능.  

- Access control via IAM policies.  
IAM 정책을 통한 접근 제어 가능.  

- Supports access policies (like S3 bucket policies).  
S3 버킷 정책과 유사한 액세스 정책 지원.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon SQS is a fully managed queuing service.  
아마존 SQS는 완전관리형 큐 서비스입니다.  

- Producers send messages (≤ 256 KB), consumers poll and delete them.  
생산자는 메시지(최대 256KB)를 보내고 소비자는 가져와 처리 후 삭제합니다.  

- Standard queues provide at-least-once delivery and best-effort ordering.  
표준 큐는 최소 1회 이상 전달 보장, 순서 보장은 최선의 노력 수준입니다.  

- SQS integrates with Auto Scaling to dynamically adjust consumers.  
SQS는 오토 스케일링과 통합되어 소비자를 동적으로 조절할 수 있습니다. 
