# Mobile Application: MyTodoList  
# 모바일 애플리케이션: MyTodoList  
(서버리스 아키텍처 학습을 위해 만든 모바일 앱 예제)  

---

## Introduction to Serverless Architecture for MyTodoList  
## MyTodoList를 위한 서버리스 아키텍처 소개  
(이번 강의에서는 MyTodoList라는 모바일 앱을 예제로 서버리스 아키텍처를 다룸)  

In this lecture, we discuss serverless architectures by creating a mobile application called MyTodoList. The application has the following requirements:  
이번 강의에서는 MyTodoList라는 모바일 앱을 만들며 서버리스 아키텍처를 살펴봅니다. 이 앱에는 다음 요구사항이 있습니다:  

- Expose a REST API with HTTPS endpoints.  
- HTTPS 엔드포인트를 가진 REST API 제공.  
  (외부 클라이언트와 안전하게 통신하기 위함)  

- Implement a serverless architecture.  
- 서버리스 아키텍처 구현.  
  (인프라 관리 없이 확장성 확보)  

- Allow users to directly interact with their own folders in Amazon S3 to manage their data.  
- 사용자가 Amazon S3의 자신의 폴더와 직접 상호작용 가능.  
  (파일 저장 및 관리 기능 제공)  

- Enable user authentication through a managed serverless service.  
- 관리형 서버리스 서비스로 사용자 인증 지원.  
  (보안 강화를 위해 Cognito 사용)  

- Support writing and reading to-dos, with a focus on high read throughput.  
- To-do 작성 및 읽기 지원, 특히 높은 읽기 처리량 최적화.  

- Use a scalable database layer optimized for high read throughput.  
- 높은 읽기 성능에 최적화된 확장 가능한 DB 계층 사용.  

---

## Designing the Serverless REST API  
## 서버리스 REST API 설계  

To start, the mobile clients will communicate via a REST HTTPS interface. We use Amazon API Gateway to expose this API. In a classic serverless API pattern, API Gateway invokes an AWS Lambda function, enabling scalable and serverless compute.  
모바일 클라이언트는 REST HTTPS 인터페이스로 통신합니다. 이 API는 Amazon API Gateway로 노출되며, 전형적인 서버리스 패턴에 따라 API Gateway는 AWS Lambda를 호출해 확장 가능한 서버리스 컴퓨팅을 수행합니다.  

The Lambda function needs to store and read to-dos from a database that scales well and is serverless. For this, we use Amazon DynamoDB as the backend database.  
Lambda 함수는 확장성이 뛰어난 서버리스 DB에서 to-do를 저장/읽어야 하며, 이를 위해 백엔드 DB로 Amazon DynamoDB를 사용합니다.  

---

## Authentication with Amazon Cognito  
## Amazon Cognito를 통한 인증  

For authentication, we use Amazon Cognito, a serverless managed service. The mobile client authenticates with Cognito, and API Gateway verifies the authentication with Cognito. This integration provides a classic serverless API with secure user authentication.  
인증을 위해 서버리스 관리형 서비스인 Amazon Cognito를 사용합니다. 모바일 클라이언트는 Cognito로 인증하며, API Gateway가 이를 검증합니다. 이 통합으로 안전한 사용자 인증을 가진 전형적인 서버리스 API가 완성됩니다.  

---

## Secure Access to Amazon S3  
## Amazon S3에 대한 보안 접근  

Users need access to their own Amazon S3 folders. The mobile clients authenticate with Cognito, which generates temporary credentials. These credentials allow the clients to store and retrieve files in their own restricted space in S3.  
사용자는 자신의 Amazon S3 폴더에 접근해야 합니다. 모바일 클라이언트는 Cognito로 인증하고, Cognito는 임시 자격 증명을 발급합니다. 이 자격 증명으로 사용자는 자신의 제한된 S3 공간에서 파일을 저장/조회할 수 있습니다.  

It is important not to store AWS user credentials directly on mobile clients. Instead, always use Amazon Cognito to generate temporary credentials securely.  
AWS 자격 증명을 모바일 클라이언트에 직접 저장해서는 안 되며, 항상 Cognito를 통해 임시 자격 증명을 안전하게 발급받아야 합니다.  

---

## Scaling and Performance Optimization  
## 확장 및 성능 최적화  

As the application scales and user count increases, we observe a very high read throughput with many read capacity units (RCUs) consumed. Since to-dos do not change frequently, we can optimize performance and reduce costs by introducing caching.  
애플리케이션이 확장되고 사용자 수가 증가하면 읽기 처리량이 크게 늘어나고 RCU가 많이 소비됩니다. 하지만 to-do 데이터는 자주 바뀌지 않으므로 캐싱을 도입해 성능을 최적화하고 비용을 줄일 수 있습니다.  

We add DynamoDB Accelerator (DAX) as a caching layer before DynamoDB. DAX caches read requests, reducing the load on DynamoDB and lowering read capacity unit consumption. This improves scalability and reduces overall costs.  
DynamoDB 앞단에 캐싱 레이어로 DynamoDB Accelerator(DAX)를 추가합니다. DAX는 읽기 요청을 캐시해 DynamoDB 부하와 RCU 소비를 줄여 확장성과 비용 효율성을 향상시킵니다.  

Additionally, caching can be implemented at the Amazon API Gateway level for API responses that rarely change. This further enhances performance by caching responses for specific API routes.  
추가로, 자주 변하지 않는 API 응답은 Amazon API Gateway 수준에서 캐싱할 수 있으며, 특정 API 경로의 성능을 더욱 향상시킵니다.  

---

## Summary of the Serverless Architecture  
## 서버리스 아키텍처 요약  

This architecture demonstrates a fully serverless REST API using HTTPS, API Gateway, Lambda, and DynamoDB. Authentication is handled by Cognito, which also generates temporary credentials for secure S3 access.  
이 아키텍처는 HTTPS, API Gateway, Lambda, DynamoDB를 활용한 완전한 서버리스 REST API를 보여줍니다. 인증은 Cognito가 담당하며, 동시에 S3에 안전하게 접근할 임시 자격 증명을 생성합니다.  

Caching with DAX improves read throughput and reduces costs, while API Gateway caching can be used for static API responses. Security is integrated throughout with Cognito directly linked to API Gateway.  
DAX 캐싱은 읽기 성능을 향상시키고 비용을 절감하며, API Gateway 캐싱은 정적 API 응답에 활용됩니다. Cognito와 API Gateway의 직접 연동을 통해 보안도 아키텍처 전반에 걸쳐 강화됩니다.  

This example provides a foundational understanding of serverless architectures and the AWS components involved.  
이 예제는 서버리스 아키텍처와 관련 AWS 컴포넌트에 대한 기초 이해를 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Implemented a serverless architecture for a mobile application called MyTodoList using AWS services.  
- AWS 서비스를 활용해 MyTodoList 모바일 앱에 서버리스 아키텍처 구현.  

- Utilized Amazon API Gateway, Lambda, DynamoDB, and Cognito for REST API, compute, database, and authentication respectively.  
- REST API, 컴퓨팅, 데이터베이스, 인증에 각각 API Gateway, Lambda, DynamoDB, Cognito 사용.  

- Enabled users to access their own folders in Amazon S3 securely via temporary credentials generated by Cognito.  
- Cognito가 발급한 임시 자격 증명으로 사용자가 안전하게 자신의 S3 폴더에 접근 가능.  

- Improved read throughput and reduced costs by introducing DynamoDB Accelerator (DAX) caching and optional API Gateway response caching.  
- DAX 캐싱 및 API Gateway 응답 캐싱으로 읽기 성능 향상 및 비용 절감.  

---

📌 정리: 이 문서는 **MyTodoList 앱**을 예제로, **서버리스 아키텍처**를 단계별로 설명하면서 AWS 서비스(API Gateway, Lambda, DynamoDB, Cognito, S3, DAX)를 어떻게 조합하는지 보여줍니다.

👉 게임 보상 🎁 : **"서버리스 마스터 1단계 달성! 🏆"**
(AWS Step Functions, Lambda, DynamoDB, Cognito, API Gateway 개념 습득)
