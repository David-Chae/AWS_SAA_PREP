# Microservices Architecture  
# 마이크로서비스 아키텍처  
(주제 제목을 나타냄)

---

## Introduction to Microservices Architecture  
## 마이크로서비스 아키텍처 소개  
(마이크로서비스 아키텍처의 개념을 설명하기 위한 도입 부분)

We are now discussing microservices. While this is not exactly serverless architecture, it remains a very interesting topic.  
지금 우리는 마이크로서비스에 대해 논의하고 있습니다. 이는 정확히 서버리스 아키텍처는 아니지만 여전히 매우 흥미로운 주제입니다.  
(마이크로서비스와 서버리스의 차이와 흥미로움을 강조)

The goal is to switch to a microservices architecture where many services interact with each other, often using REST APIs. This is how they communicate with one another.  
목표는 다수의 서비스가 서로 상호작용하는 마이크로서비스 아키텍처로 전환하는 것입니다. 이때 주로 REST API를 사용하여 통신합니다.  
(마이크로서비스 간 상호작용 방식 설명)

Each microservice's architecture may vary in form and shape, giving us the freedom to design each service as we want.  
각 마이크로서비스의 아키텍처는 형태와 구조가 다양할 수 있으며, 이를 통해 원하는 방식으로 설계할 자유가 주어집니다.  
(유연한 설계 가능성 강조)

The motivation for adopting microservices includes having a leaner development lifecycle for each service, enabling each service to scale independently, and allowing each to maintain its own code repository.  
마이크로서비스를 도입하는 이유는 각 서비스의 개발 주기를 단순화하고, 독립적인 확장을 가능하게 하며, 자체 코드 저장소를 유지할 수 있기 때문입니다.  
(마이크로서비스 도입의 장점 설명)

---

## Example Microservices Setup  
## 마이크로서비스 설정 예시  
(구체적인 아키텍처 사례를 소개)

Consider a scenario where users communicate with the first microservice over HTTPS.  
사용자가 HTTPS를 통해 첫 번째 마이크로서비스와 통신하는 시나리오를 생각해봅시다.  
(사용자와 서비스 간 연결 설명)

We have chosen to use an Elastic Load Balancer (ELB) that routes requests to ECS (Elastic Container Service), which then interacts with DynamoDB.  
우리는 요청을 ECS(Elastic Container Service)로 라우팅하는 Elastic Load Balancer(ELB)를 사용하며, ECS는 DynamoDB와 상호작용합니다.  
(서비스 처리 흐름 설명)

ECS is AWS's service for running Docker containers.  
ECS는 Docker 컨테이너를 실행하기 위한 AWS의 서비스입니다.  
(기술 정의 제공)

This first microservice typically has a DNS name or URL, such as service1.example.com.  
첫 번째 마이크로서비스는 보통 service1.example.com 같은 DNS 이름 또는 URL을 가집니다.  
(서비스 접근 방식 설명)

To resolve this, a DNS query is made to Route 53, which returns an alias record, allowing interaction with the service.  
이를 해결하기 위해 Route 53에 DNS 쿼리를 보내면, 별칭 레코드가 반환되어 서비스와의 상호작용이 가능합니다.  
(DNS 해석 과정 설명)

We may also have a second microservice using a classic serverless architecture.  
또 다른 마이크로서비스는 전형적인 서버리스 아키텍처를 사용할 수도 있습니다.  
(다양한 서비스 아키텍처 가능성 소개)

Instead of DynamoDB, it uses ElastiCache as its backend.  
이 서비스는 DynamoDB 대신 ElastiCache를 백엔드로 사용합니다.  
(백엔드 변경 예시)

This is just an example to illustrate that different microservices can use different architectures and backends.  
이는 단순히 마이크로서비스마다 다른 아키텍처와 백엔드를 사용할 수 있다는 것을 보여주는 예시입니다.  
(핵심 메시지 강조)

The second service's Lambda function might call the first microservice's ELB to retrieve information necessary for its response.  
두 번째 서비스의 Lambda 함수는 응답에 필요한 정보를 얻기 위해 첫 번째 마이크로서비스의 ELB를 호출할 수 있습니다.  
(서비스 간 상호작용 예시)

A third microservice might use an ELB but not be serverless. Instead, it could use Amazon EC2 with auto-scaling and an Amazon RDS database, representing a more traditional architecture.  
세 번째 마이크로서비스는 ELB를 사용하지만 서버리스는 아닐 수 있습니다. 대신 Amazon EC2와 오토스케일링, 그리고 Amazon RDS 데이터베이스를 사용하는 전통적인 아키텍처일 수 있습니다.  
(다른 아키텍처 접근법 제시)

This EC2 instance may need to call the second microservice before making decisions.  
이 EC2 인스턴스는 결정을 내리기 전에 두 번째 마이크로서비스를 호출해야 할 수도 있습니다.  
(서비스 간 종속성 설명)

This interaction is represented by dotted lines, and the URL for this service might be service3.example.com.  
이러한 상호작용은 점선으로 표시되며, 이 서비스의 URL은 service3.example.com일 수 있습니다.  
(시각적 다이어그램 설명)

---

## Design Flexibility and Interaction Patterns  
## 설계 유연성과 상호작용 패턴  
(서비스 간 다양한 통신 패턴 설명)

The key point is that you are free to design each microservice as you wish, which is why the example shows various architectures.  
핵심은 각 마이크로서비스를 원하는 대로 설계할 수 있다는 것이며, 그래서 예시에서 다양한 아키텍처가 제시됩니다.  
(설계 자유 강조)

There are two main patterns for microservice communication:  
마이크로서비스 통신에는 두 가지 주요 패턴이 있습니다.  
(통신 방식 소개)

**Synchronous pattern:** Explicit calls to other microservices, typically over HTTPS using API Gateway or Load Balancer.  
**동기 패턴:** API Gateway 또는 Load Balancer를 통해 HTTPS로 다른 마이크로서비스를 직접 호출하는 방식입니다.  
(동기식 통신 방식 설명)

**Asynchronous pattern:** Using messaging services such as SQS, Kinesis, SNS, Lambda triggers, or S3.  
**비동기 패턴:** SQS, Kinesis, SNS, Lambda 트리거, S3와 같은 메시징 서비스를 사용하는 방식입니다.  
(비동기식 통신 방식 설명)

In this pattern, a message is placed in a queue or stream without expecting an immediate response; something else will process it asynchronously.  
이 방식에서는 메시지를 큐나 스트림에 넣고 즉각적인 응답을 기대하지 않으며, 다른 프로세스가 이를 비동기적으로 처리합니다.  
(비동기 처리 개념 설명)

---

## Challenges of Microservices  
## 마이크로서비스의 도전 과제  
(단점과 어려움 소개)

Some challenges associated with microservices include:  
마이크로서비스와 관련된 몇 가지 어려움은 다음과 같습니다.  
(문제 목록 도입)

- Overhead in creating each new microservice.  
- 새로운 마이크로서비스를 만들 때 발생하는 오버헤드.  
(추가 관리 비용)

- Difficulty optimizing server density or utilization.  
- 서버 밀도나 자원 활용을 최적화하기 어려움.  
(자원 관리 문제)

- Complexity in running multiple versions of microservices simultaneously.  
- 여러 버전의 마이크로서비스를 동시에 운영하는 복잡성.  
(버전 관리 문제)

- Proliferation of client-side code requirements to integrate with many separate services.  
- 여러 개별 서비스와 통합하기 위해 클라이언트 측 코드 요구사항이 증가함.  
(클라이언트 부담 증가)

Many of these challenges can be addressed by using serverless patterns.  
이러한 문제 중 많은 부분은 서버리스 패턴을 사용하여 해결할 수 있습니다.  
(해결 방향 제시)

For example, API Gateway and Lambda scale automatically, and you pay only for usage, eliminating concerns about server utilization.  
예를 들어 API Gateway와 Lambda는 자동으로 확장되며, 사용한 만큼만 비용을 지불하기 때문에 서버 활용도에 대한 걱정이 사라집니다.  
(서버리스 장점 강조)

Additionally, APIs can be easily cloned or environments reproduced in API Gateway.  
또한 API Gateway에서는 API를 쉽게 복제하거나 환경을 재현할 수 있습니다.  
(API 관리 편의성)

Client SDKs can be generated through Swagger integration for API Gateway, simplifying client-side integration.  
API Gateway는 Swagger와 통합하여 클라이언트 SDK를 생성할 수 있어 클라이언트 측 통합을 단순화합니다.  
(클라이언트 지원 기능 강조)

---

## Conclusion  
## 결론  
(전체 요약)

In summary, microservices represent a design approach that allows you to use various architectures.  
요약하면, 마이크로서비스는 다양한 아키텍처를 사용할 수 있게 하는 설계 접근 방식입니다.  
(핵심 정리)

While microservices solve some problems, they also introduce new challenges.  
마이크로서비스는 일부 문제를 해결하지만, 동시에 새로운 도전 과제도 만들어냅니다.  
(양면성 설명)

Understanding these trade-offs helps in designing effective systems.  
이러한 트레이드오프를 이해하면 효과적인 시스템을 설계하는 데 도움이 됩니다.  
(균형 잡힌 설계 강조)

---

## Key Takeaways  
## 핵심 요점  
(주요 교훈 정리)

- Microservices architecture enables independent scaling and development lifecycles for each service.  
- 마이크로서비스 아키텍처는 각 서비스의 독립적인 확장과 개발 주기를 가능하게 합니다.  

- Services interact primarily through REST APIs, allowing diverse architectures per service.  
- 서비스는 주로 REST API를 통해 상호작용하며, 각기 다른 아키텍처를 허용합니다.  

- Communication patterns include synchronous calls via API Gateway or Load Balancer, and asynchronous messaging using SQS, Kinesis, SNS, Lambda triggers, or S3.  
- 통신 패턴에는 API Gateway나 Load Balancer를 통한 동기 호출과 SQS, Kinesis, SNS, Lambda 트리거, S3를 이용한 비동기 메시징이 포함됩니다.  

- Challenges include overhead in creating services, server utilization optimization, managing multiple versions, and client-side integration complexity, some of which can be mitigated by serverless patterns.  
- 도전 과제로는 서비스 생성 오버헤드, 서버 자원 최적화, 다중 버전 관리, 클라이언트 통합 복잡성이 있으며, 일부는 서버리스 패턴으로 완화할 수 있습니다.  

---

👑 게임 보상: **"Microservices Architect Badge 🏗️"** 획득!
(마이크로서비스 아키텍처를 이해하고 설명할 수 있는 능력을 얻었습니다 🎉)
