# Amazon MQ  
# 아마존 MQ  

---

## Introduction to Amazon MQ  
## Amazon MQ 소개  

Let us now discuss Amazon MQ.  
이제 Amazon MQ에 대해 알아보겠습니다.  

We are familiar with SQS and SNS, which are cloud-native services because they use proprietary AWS protocols and their own sets of APIs.  
우리는 SQS와 SNS에 익숙한데, 이들은 고유한 AWS 프로토콜과 API를 사용하기 때문에 클라우드 네이티브 서비스입니다.  

However, if you are running traditional applications on-premises, you may use open protocols such as MQTT, AMQP, STOMP, Openwire, and WSS.  
하지만 기존 온프레미스 애플리케이션을 운영한다면 MQTT, AMQP, STOMP, Openwire, WSS와 같은 오픈 프로토콜을 사용할 수 있습니다.  

When migrating your application to the cloud, you might not want to re-engineer it to use SQS and SNS protocols or APIs.  
애플리케이션을 클라우드로 이전할 때, SQS와 SNS 프로토콜이나 API를 사용하도록 재설계하고 싶지 않을 수 있습니다.  

Instead, you want to continue using the traditional protocols you are accustomed to, such as MQTT and AMQP.  
대신 익숙한 기존 프로토콜(MQTT, AMQP 등)을 계속 사용하고 싶을 것입니다.  

For this purpose, Amazon MQ is available.  
이 목적을 위해 Amazon MQ가 제공됩니다.  

---

Amazon MQ is a managed message broker service for two technologies: RabbitMQ and ActiveMQ.  
Amazon MQ는 RabbitMQ와 ActiveMQ 두 가지 기술을 지원하는 관리형 메시지 브로커 서비스입니다.  

RabbitMQ and ActiveMQ are on-premises technologies that provide access to the open protocols mentioned earlier.  
RabbitMQ와 ActiveMQ는 앞서 언급한 오픈 프로토콜을 지원하는 온프레미스 기술입니다.  

Amazon MQ offers a managed version of these brokers on the cloud.  
Amazon MQ는 클라우드에서 이러한 브로커의 관리형 버전을 제공합니다.  

This has important implications. Firstly, Amazon MQ does not scale as much as SQS or SNS, which have virtually infinite scaling capabilities.  
이것은 중요한 의미를 가집니다. 우선, Amazon MQ는 사실상 무한 확장이 가능한 SQS나 SNS만큼 확장되지 않습니다.  

Because Amazon MQ runs on servers, you may encounter server issues.  
Amazon MQ는 서버에서 실행되므로 서버 관련 문제가 발생할 수 있습니다.  

To ensure high availability, you can run a multi-Availability Zone (multi-AZ) setup with failover.  
고가용성을 위해 다중 가용 영역(Multi-AZ) 구성과 장애 조치(failover)를 설정할 수 있습니다.  

Amazon MQ includes both queue features, similar to SQS, and topic features, similar to SNS, within a single broker.  
Amazon MQ는 하나의 브로커 안에 SQS와 유사한 큐 기능과 SNS와 유사한 토픽 기능을 모두 포함합니다.  

---

## High Availability in Amazon MQ  
## Amazon MQ의 고가용성  

Consider a region such as us-east-1 with two Availability Zones: us-east-1a and us-east-1b.  
예를 들어 us-east-1 리전에는 us-east-1a와 us-east-1b 두 개의 가용 영역이 있다고 가정합니다.  

One zone will be active, and the other will be standby.  
한 영역은 활성(active) 상태이고, 다른 영역은 대기(standby) 상태가 됩니다.  

An Amazon MQ broker runs in both Availability Zones, where one is active and the other is standby.  
Amazon MQ 브로커는 두 가용 영역 모두에서 실행되며, 한쪽은 활성, 다른 쪽은 대기 상태입니다.  

For failover to function correctly, you need to define Amazon Elastic File System (EFS) as your backend storage.  
장애 조치(failover)가 제대로 작동하려면 Amazon Elastic File System(EFS)을 백엔드 스토리지로 정의해야 합니다.  

Amazon EFS is a network file system that can be mounted onto multiple Availability Zones.  
Amazon EFS는 여러 가용 영역에 마운트할 수 있는 네트워크 파일 시스템입니다.  

When failover occurs, the standby broker is also mounted onto Amazon EFS, ensuring it has the same data as the active queue.  
장애 조치가 발생하면 대기 브로커도 Amazon EFS에 마운트되어 활성 큐와 동일한 데이터를 갖게 됩니다.  

This setup allows failover to happen correctly, preserving data integrity.  
이 구성은 장애 조치가 올바르게 작동하도록 하여 데이터 무결성을 보장합니다.  

If your client communicates with the Amazon MQ broker and a failover occurs, the data remains safe thanks to Amazon EFS.  
클라이언트가 Amazon MQ 브로커와 통신 중 장애 조치가 발생해도, Amazon EFS 덕분에 데이터는 안전하게 유지됩니다.  

That concludes the key points to remember about Amazon MQ for the exam.  
이로써 시험 대비 Amazon MQ의 핵심 포인트가 마무리됩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon MQ is a managed message broker service supporting RabbitMQ and ActiveMQ, enabling the use of traditional open protocols in the cloud.  
- Amazon MQ는 RabbitMQ와 ActiveMQ를 지원하는 관리형 메시지 브로커 서비스로, 클라우드에서 기존 오픈 프로토콜을 사용할 수 있습니다.  

- It supports protocols like MQTT, AMQP, STOMP, Openwire, and WSS, facilitating migration of on-premises applications without re-engineering.  
- MQTT, AMQP, STOMP, Openwire, WSS 등의 프로토콜을 지원하여, 온프레미스 애플리케이션을 재설계 없이 클라우드로 이전할 수 있습니다.  

- Amazon MQ provides both queue and topic features within a single broker, similar to SQS and SNS respectively.  
- Amazon MQ는 하나의 브로커 안에서 큐 기능(SQS 유사)과 토픽 기능(SNS 유사)을 모두 제공합니다.  

- High availability is achieved through multi-AZ deployment with failover using Amazon EFS as backend storage to synchronize data between active and standby brokers.  
- 고가용성은 다중 가용 영역(Multi-AZ) 배포와 Amazon EFS를 백엔드 스토리지로 사용하는 장애 조치를 통해 활성 브로커와 대기 브로커 간 데이터를 동기화하여 구현됩니다.  
