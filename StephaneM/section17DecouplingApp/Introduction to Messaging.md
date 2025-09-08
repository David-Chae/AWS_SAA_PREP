# Introduction to Messaging  
(AWS 메시징 소개)

AWS 통합과 메시징 섹션에 오신 것을 환영합니다.  
여기서는 애플리케이션 간의 통신 방식과 AWS가 제공하는 메시징 서비스를 다룹니다.  

---

## Introduction to Application Communication Patterns  
(애플리케이션 통신 패턴 소개)

여러 애플리케이션을 배포할 경우, 서비스 간에는 데이터를 주고받으며 상호작용해야 합니다.  
이를 위한 주요 통신 패턴은 두 가지가 있습니다:

1. **동기식 통신 (Synchronous Communication)**: 애플리케이션이 직접 연결되어 통신  
2. **비동기식 통신 (Asynchronous Communication)**: 큐(Queue) 같은 미들웨어를 통한 간접 통신  

---

## Synchronous Communication Example  
(동기식 통신 예시)

예: 온라인 스토어에서 **구매 서비스**가 **배송 서비스**에 직접 알림을 보내 물품을 발송하도록 요청  
- 구매 서비스와 배송 서비스가 직접 연결되어 있음  
- 요청-응답 형태의 즉각적 통신  

---

## Asynchronous Communication Example  
(비동기식 통신 예시)

예: 구매 서비스가 구매 정보를 **큐(Queue)**에 넣음 → 배송 서비스는 큐를 읽고 처리  
- 서비스 간 직접 연결이 없음  
- 서비스가 서로 독립적으로 동작 가능  

---

## Advantages of Asynchronous Communication  
(비동기식 통신의 장점)

동기식 통신은 특정 서비스가 트래픽 급증으로 과부하될 경우 문제가 발생할 수 있음.  
예: 영상 인코딩 서비스가 평소 10개 요청을 받다가 갑자기 1,000개 요청을 받으면 장애 발생 가능.  

➡ 비동기식 구조는 미들웨어가 요청을 버퍼링하고 확장 가능하므로 **안정성과 확장성**이 높음.  

---

## AWS Services for Decoupling and Scaling  
(AWS의 비동기/확장 지원 서비스)

AWS는 서비스 간 결합도를 낮추고 확장을 지원하는 다양한 메시징 서비스를 제공:  

- **SQS (Simple Queue Service)**: 큐 기반 비동기 메시징  
- **SNS (Simple Notification Service)**: 발행/구독(pub/sub) 모델  
- **Kinesis**: 실시간 스트리밍 및 빅데이터 처리  

이를 통해 각 애플리케이션은 독립적으로 확장 가능하며, 미들웨어 계층이 유연하게 스케일링 가능.  

---

## Key Takeaways  
(핵심 요약)

- 애플리케이션 간 통신은 **동기식** 또는 **비동기식** 패턴으로 이루어진다.  
- 동기식: 서비스 간 직접 연결  
- 비동기식: 큐와 같은 미들웨어를 통한 간접 연결  
- AWS의 **SQS, SNS, Kinesis**는 확장 가능하고 느슨하게 결합된 아키텍처를 구현하는 핵심 서비스  



# Introduction to Messaging  

Welcome to the section on AWS integration and messaging.  

---

## Introduction to Application Communication Patterns  

In this section, we will explore how to orchestrate interactions between different services using middleware.  
When deploying multiple applications, they inevitably need to communicate with one another to share information and data.  

There are two primary patterns of application communication:  

1. **Synchronous communication**: where one application directly connects to another.  
2. **Asynchronous communication**: where applications communicate via an intermediary such as a queue.  

---

## Synchronous Communication Example  

For example, consider an online store with a **buying service** and a **shipping service**.  
When an item is purchased, the buying service directly notifies the shipping service to send the item.  

➡️ Here, the buying and shipping services are directly connected, representing **synchronous communication**.  

---

## Asynchronous Communication Example  

Alternatively, in **asynchronous** or **event-based communication**, a middleware such as a **queue** connects the applications.  

- The buying service places a message indicating a purchase into the queue.  
- The shipping service then polls the queue for new messages and processes them independently.  

This decouples the services, as they do not communicate directly.  

---

## Advantages of Asynchronous Communication  

Synchronous communication can be problematic if one service becomes overwhelmed, such as during sudden spikes in traffic.  

For instance, a video encoding service receiving **1,000 videos at once instead of the usual 10** could experience outages.  

➡️ Decoupling applications using asynchronous communication allows the middleware layer to scale independently, handling traffic spikes more gracefully.  

---

## AWS Services for Decoupling and Scaling  

AWS provides several services to facilitate scalable, decoupled communication:  

- **SQS (Simple Queue Service):** Implements a queue model for asynchronous messaging.  
- **SNS (Simple Notification Service):** Implements a publish/subscribe model.  
- **Kinesis:** Supports real-time streaming and big data processing.  

Using these services, applications can scale independently while the middleware scales efficiently as well.  

In this section, we will learn about these three technologies and how they enable scalable, decoupled service communication.  

---

## Key Takeaways  

- Applications communicate through **synchronous** or **asynchronous** patterns.  
- **Synchronous communication** involves direct connections between services.  
- **Asynchronous communication** uses middleware like queues to decouple services.  
- AWS services such as **SQS, SNS, and Kinesis** enable scalable, decoupled communication. 


