# High Availability and Scalability  
# 고가용성과 확장성  

---

## Introduction to Scalability and High Availability  
## 확장성과 고가용성 소개  

This lecture provides a brief overview of scalability and high availability concepts.  
이 강의는 확장성과 고가용성 개념에 대한 간단한 개요를 제공합니다.  

It is designed for beginners, so if you are already confident with these topics, you may choose to skip this lecture.  
이 강의는 초보자를 위해 설계되었으므로, 이미 이 주제에 익숙하다면 건너뛰어도 됩니다.  

---

## What is Scalability?  
## 확장성이란 무엇인가?  

Scalability means that your application system can handle a greater load by adapting accordingly.  
확장성이란 애플리케이션 시스템이 더 큰 부하를 처리할 수 있도록 조정되는 것을 의미합니다.  

There are two types of scalability:  
확장성에는 두 가지 유형이 있습니다:  

- Vertical scalability  
- 수직 확장성  

- Horizontal scalability (also called elasticity)  
- 수평 확장성 (탄력성이라고도 함)  

It is important to note that scalability is different from high availability, although they are related concepts.  
확장성과 고가용성은 관련된 개념이지만 서로 다르다는 점이 중요합니다.  

---

## Vertical Scalability  
## 수직 확장성  

Vertical scalability means increasing the size or capacity of your instance.  
수직 확장성이란 인스턴스의 크기나 용량을 늘리는 것을 의미합니다.  

For example, consider a phone operator:  
예를 들어, 콜센터 상담원을 생각해 봅시다:  

- A junior operator can take five calls per minute.  
- 주니어 상담원은 분당 다섯 통의 전화를 받을 수 있습니다.  

- A senior operator can take up to ten calls per minute.  
- 시니어 상담원은 분당 열 통의 전화를 받을 수 있습니다.  

Upgrading from a junior to a senior operator is an example of vertical scalability, as the capacity goes up.  
주니어에서 시니어 상담원으로 업그레이드하는 것은 처리 용량이 늘어나므로 수직 확장성의 예시입니다.  

In cloud computing, for instance in Amazon EC2, vertical scaling means upgrading your application from a smaller instance type like t2.micro to a larger one like t2.large.  
클라우드 컴퓨팅에서, 예를 들어 Amazon EC2에서는 작은 인스턴스(t2.micro)에서 큰 인스턴스(t2.large)로 업그레이드하는 것이 수직 확장성입니다.  

Vertical scalability is commonly used for non-distributed systems such as databases.  
수직 확장성은 데이터베이스 같은 비분산 시스템에서 주로 사용됩니다.  

Services like RDS or ElastiCache allow vertical scaling by upgrading the underlying instance type.  
RDS나 ElastiCache 같은 서비스는 기본 인스턴스 유형을 업그레이드하여 수직 확장을 지원합니다.  

However, there are hardware limits to vertical scaling.  
그러나 수직 확장에는 하드웨어 한계가 존재합니다.  

---

## Horizontal Scalability  
## 수평 확장성  

Horizontal scalability means increasing the number of instances or systems for your application.  
수평 확장성이란 애플리케이션에 필요한 인스턴스나 시스템의 수를 늘리는 것을 의미합니다.  

Using the call center example again:  
다시 콜센터 예시로 설명해 보겠습니다:  

- Instead of upgrading one operator, you hire a second operator, doubling capacity.  
- 한 상담원을 업그레이드하는 대신, 두 번째 상담원을 고용하면 처리 용량이 두 배가 됩니다.  

- Hiring more operators, such as six, further increases capacity.  
- 여섯 명까지 더 고용하면 처리 용량은 더욱 늘어납니다.  

This is horizontal scaling.  
이것이 수평 확장성입니다.  

Horizontal scaling implies a distributed system, which is common in web or modern applications.  
수평 확장성은 분산 시스템을 의미하며, 웹이나 현대 애플리케이션에서 흔히 사용됩니다.  

Not every application can be distributed.  
모든 애플리케이션이 분산될 수 있는 것은 아닙니다.  

Thanks to cloud offerings like Amazon EC2, horizontal scaling is easy: you can add new instances with a few clicks.  
Amazon EC2와 같은 클라우드 서비스 덕분에, 수평 확장은 몇 번의 클릭으로 쉽게 새로운 인스턴스를 추가할 수 있습니다.  

---

## High Availability  
## 고가용성  

High availability usually goes hand in hand with horizontal scaling but is not the same.  
고가용성은 보통 수평 확장성과 함께 사용되지만, 같은 개념은 아닙니다.  

It means running your application or system in at least two data centers or availability zones (AZ) in AWS.  
고가용성이란 AWS에서 최소 두 개의 데이터 센터 또는 가용 영역(AZ)에서 애플리케이션이나 시스템을 실행하는 것을 의미합니다.  

The goal is to survive a data center loss; if one center goes down, the system continues running.  
목표는 데이터 센터 장애에도 서비스가 지속되도록 하는 것입니다.  

For example, having three phone operators in a New York building and three in a San Francisco building ensures that if the New York building loses connection, the San Francisco operators can still take calls.  
예를 들어, 뉴욕 건물에 상담원 세 명, 샌프란시스코 건물에 상담원 세 명이 있다면, 뉴욕 건물이 연결을 잃더라도 샌프란시스코 상담원들이 전화를 받을 수 있습니다.  

This setup is highly available.  
이런 구성이 고가용성입니다.  

High availability can be:  
고가용성에는 두 가지 유형이 있습니다:  

- Passive: For example, RDS Multi-AZ deployments where a standby instance exists but is not actively serving.  
- 수동형: 예를 들어, RDS Multi-AZ 배포에서는 대기 인스턴스가 존재하지만 실제로 서비스하지 않습니다.  

- Active: When multiple instances actively serve traffic simultaneously, such as horizontally scaled phone operators in two buildings both taking calls at the same time.  
- 능동형: 두 건물의 상담원들이 동시에 전화를 받는 것처럼, 여러 인스턴스가 동시에 트래픽을 처리하는 경우입니다.  

---

## Scalability and High Availability in AWS  
## AWS에서의 확장성과 고가용성  

Vertical scaling: Increasing instance size, such as from t2.nano (0.5 GB RAM, 1 vCPU) to a1.12tb1.metal (12.3 TB RAM, 450 vCPUs).  
수직 확장: 예를 들어, t2.nano(0.5 GB RAM, 1 vCPU)에서 a1.12tb1.metal(12.3 TB RAM, 450 vCPUs)로 인스턴스 크기를 키우는 것.  

Horizontal scaling: Increasing the number of instances, known as scaling out (adding instances) or scaling in (removing instances).  
수평 확장: 인스턴스 수를 늘리거나 줄이는 것. 인스턴스를 추가하는 것을 확장(out), 제거하는 것을 축소(in)라고 합니다.  

High availability: Running the same application instance across multiple availability zones, enabled in auto-scaling groups or load balancers.  
고가용성: 동일한 애플리케이션 인스턴스를 여러 가용 영역에서 실행하는 것. 오토스케일링 그룹이나 로드 밸런서를 통해 구현됩니다.  

---

## Summary  
## 요약  

This lecture provided a quick overview of the terms high availability and scalability.  
이 강의에서는 고가용성과 확장성 용어에 대한 빠른 개요를 제공했습니다.  

Understanding these concepts is essential, especially for exam questions where they may be tested or confused.  
이 개념들을 이해하는 것은 중요하며, 특히 시험 문제에서 자주 출제되거나 혼동되기 쉽습니다.  

Remember the call center example to help conceptualize these ideas.  
콜센터 예시를 기억하면 개념 이해에 도움이 됩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Scalability allows an application system to handle increased load by adapting, either vertically or horizontally.  
- 확장성은 시스템이 수직 또는 수평으로 조정되어 더 큰 부하를 처리할 수 있게 합니다.  

- Vertical scalability involves increasing the size or capacity of a single instance, such as upgrading a server or operator's capability.  
- 수직 확장은 단일 인스턴스의 크기나 용량을 키우는 것입니다. 예: 서버 성능 업그레이드.  

- Horizontal scalability involves increasing the number of instances or systems, commonly used in distributed systems and modern web applications.  
- 수평 확장은 인스턴스나 시스템 수를 늘리는 것입니다. 분산 시스템과 현대 웹 애플리케이션에서 흔히 사용됩니다.  

- High availability ensures system operation across multiple data centers or availability zones to survive failures, often implemented alongside horizontal scaling.  
- 고가용성은 여러 데이터 센터/가용 영역에서 시스템이 실행되어 장애 시에도 서비스가 유지되도록 합니다. 보통 수평 확장과 함께 구현됩니다.
