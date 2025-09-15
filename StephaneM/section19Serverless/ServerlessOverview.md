# Serverless Introduction  
# 서버리스 소개  
➡️ 서버리스 개념과 AWS에서의 활용을 학습합니다. 게임보상: ⭐ +10  

---

## Introduction to Serverless  
## 서버리스 개념 소개  
➡️ 서버리스의 정의와 초기 의미를 설명합니다.  

Serverless is a relatively new concept in cloud computing.  
서버리스는 클라우드 컴퓨팅에서 비교적 새로운 개념입니다.  
➡️ 클라우드 환경에서 서버 관리 부담을 줄이는 접근 방식.  

When developers use serverless services, they no longer have to manage servers directly.  
개발자가 서버리스 서비스를 사용할 때, 더 이상 서버를 직접 관리할 필요가 없습니다.  
➡️ 코드 작성에 집중할 수 있음.  

It is important to note that servers still exist; however, developers do not manage or provision them.  
서버는 여전히 존재하지만, 개발자는 이를 관리하거나 프로비저닝하지 않습니다.  
➡️ 보이지 않는 서버 개념 이해 필요.  

Instead, they simply deploy code, often in the form of functions.  
대신 개발자는 코드를 배포하며, 대부분 함수 형태로 배포합니다.  
➡️ FaaS(Function as a Service) 중심.  

Initially, serverless referred specifically to Function as a Service, or FaaS.  
초기 서버리스는 주로 FaaS(Function as a Service)를 의미했습니다.  
➡️ AWS Lambda가 대표적 예시.  

This concept was pioneered by AWS Lambda.  
이 개념은 AWS Lambda에 의해 처음 구현되었습니다.  
➡️ 서버리스의 기원.  

Over time, the meaning of serverless has expanded to include a broader range of remotely managed services.  
시간이 지나면서 서버리스는 원격으로 관리되는 더 넓은 범위의 서비스로 의미가 확장되었습니다.  
➡️ 함수 외에도 다양한 서버리스 서비스 포함.  

---

## Expanded Scope of Serverless  
## 서버리스의 확장 범위  
➡️ 서버리스가 포함하는 서비스 종류 설명.  

Today, serverless encompasses not only functions but also managed databases, messaging systems, and storage services.  
현재 서버리스는 함수뿐만 아니라 관리형 데이터베이스, 메시징 시스템, 스토리지 서비스도 포함합니다.  
➡️ 서버리스 = 서버 관리 없이 제공되는 모든 서비스.  

The key characteristic is that you do not provision or manage the underlying servers for these services.  
주요 특징은 이러한 서비스의 기본 서버를 프로비저닝하거나 관리하지 않는다는 점입니다.  
➡️ 서버 존재는 보이지만 관리하지 않음.  

Serverless means you do not see or provision servers, even though they exist behind the scenes.  
서버리스란 서버가 존재하더라도 사용자가 보거나 프로비저닝하지 않는다는 의미입니다.  
➡️ 서버는 추상화됨.  

---

## Example Serverless Architecture in AWS  
## AWS 서버리스 아키텍처 예시  
➡️ AWS를 활용한 서버리스 구성 예제.  

Consider an example architecture in AWS:  
AWS의 예시 아키텍처를 고려해봅시다:  

Users access static content hosted on Amazon S3 buckets, possibly delivered via CloudFront.  
사용자는 Amazon S3 버킷에 호스팅된 정적 콘텐츠에 접근하며, CloudFront를 통해 전달될 수도 있습니다.  
➡️ 정적 콘텐츠 제공 방법.  

User authentication is handled by Amazon Cognito, which stores user identities.  
사용자 인증은 Amazon Cognito가 처리하며, 사용자 정보를 저장합니다.  
➡️ 서버리스 인증 관리.  

Users invoke REST APIs through API Gateway.  
사용자는 API Gateway를 통해 REST API를 호출합니다.  
➡️ API 요청 처리 구조.  

API Gateway triggers AWS Lambda functions.  
API Gateway는 AWS Lambda 함수를 트리거합니다.  
➡️ 이벤트 기반 함수 실행.  

Lambda functions interact with DynamoDB to store and retrieve data.  
Lambda 함수는 DynamoDB와 상호작용하여 데이터를 저장하고 조회합니다.  
➡️ 서버리스 데이터 처리.  

This architecture demonstrates a typical serverless application using AWS services.  
이 아키텍처는 AWS 서비스를 활용한 전형적인 서버리스 애플리케이션을 보여줍니다.  
➡️ 서버리스 아키텍처 이해.  

This section of the course will focus on learning about Lambda, DynamoDB, API Gateway, Cognito, and related services in depth.  
이 강좌에서는 Lambda, DynamoDB, API Gateway, Cognito 및 관련 서비스를 심도 있게 학습합니다.  
➡️ 핵심 서버리스 서비스.  

---

## Additional AWS Serverless Services  
## 추가 AWS 서버리스 서비스  
➡️ Lambda 외의 서버리스 서비스 소개.  

Beyond Lambda and DynamoDB, AWS offers several other serverless services:  
Lambda와 DynamoDB 외에도 AWS는 다양한 서버리스 서비스를 제공합니다:  

- Amazon S3 for storage.  
- 스토리지용 Amazon S3  
➡️ 서버 관리 없는 스토리지 제공.  

- Amazon SNS and SQS for messaging, both of which scale automatically without server management.  
- 메시징용 Amazon SNS와 SQS, 자동 확장 가능하며 서버 관리 불필요  
➡️ 서버리스 메시징.  

- Kinesis Data Firehose, which scales based on throughput and charges based on usage without server provisioning.  
- Kinesis Data Firehose, 처리량에 따라 확장하며 사용량 기반 요금, 서버 프로비저닝 불필요  
➡️ 스트리밍 데이터 처리.  

- Aurora Serverless, a database that scales on demand without server management.  
- Aurora Serverless, 필요에 따라 자동 확장하는 데이터베이스, 서버 관리 불필요  
➡️ 서버리스 DB.  

- AWS Step Functions for orchestrating workflows.  
- 워크플로우 오케스트레이션용 AWS Step Functions  
➡️ 서버리스 워크플로우 관리.  

- AWS Fargate, a serverless compute engine for running Docker containers without provisioning infrastructure.  
- AWS Fargate, 인프라 프로비저닝 없이 Docker 컨테이너 실행 가능한 서버리스 컴퓨트 엔진  
➡️ 서버리스 컨테이너 실행.  

These services collectively enable building fully serverless applications.  
이러한 서비스들은 함께 완전한 서버리스 애플리케이션 구축을 가능하게 합니다.  
➡️ 전체 서버리스 생태계 이해.  

---

## Conclusion  
## 결론  
➡️ 서버리스 개요 요약.  

This introduction provides a brief overview of serverless computing and its ecosystem within AWS.  
이 소개에서는 AWS 내 서버리스 컴퓨팅과 생태계에 대한 간단한 개요를 제공합니다.  
➡️ 서버리스의 전체 그림.  

The next lecture will focus on AWS Lambda, which is a foundational service in serverless architectures.  
다음 강의에서는 서버리스 아키텍처의 핵심 서비스인 AWS Lambda를 학습합니다.  
➡️ Lambda 학습 예고.  

The exam will test your knowledge of serverless concepts extensively, so it is important to understand these fundamentals.  
시험에서는 서버리스 개념에 대한 지식을 광범위하게 평가하므로 기본 개념을 이해하는 것이 중요합니다.  
➡️ 시험 대비 팁.  

---

## Key Takeaways  
## 핵심 요약  
➡️ 서버리스 핵심 포인트.  

- Serverless computing means developers do not manage servers directly, though servers still exist.  
- 서버리스 컴퓨팅은 개발자가 서버를 직접 관리하지 않지만, 서버는 여전히 존재한다는 의미입니다.  

- Initially, serverless referred to Function as a Service (FaaS), pioneered by AWS Lambda.  
- 초기 서버리스는 AWS Lambda가 선도한 FaaS를 의미했습니다.  

- Serverless now includes managed services like databases, messaging, and storage without provisioning servers.  
- 서버리스는 이제 데이터베이스, 메시징, 스토리지 등 서버 프로비저닝 없이 제공되는 관리형 서비스도 포함합니다.  

- AWS serverless architecture commonly involves Lambda, DynamoDB, API Gateway, Cognito, S3, SNS, SQS, Kinesis Data Firehose, Aurora Serverless, Step Functions, and Fargate.  
- AWS 서버리스 아키텍처에는 Lambda, DynamoDB, API Gateway, Cognito, S3, SNS, SQS, Kinesis Data Firehose, Aurora Serverless, Step Functions, Fargate 등이 포함됩니다.  
➡️ 시험 및 실무 핵심 구성 요소.  
```

게임보상: 🎮 +20 XP, 서버리스 개념 이해 완료!

