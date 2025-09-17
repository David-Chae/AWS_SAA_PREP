# Serverless Website: MyBlog.com  
# 서버리스 웹사이트: MyBlog.com  
(완전 서버리스로 운영되는 글로벌 블로그 예제)  

---

## Introduction to Serverless Hosted Website: MyBlog.com  
## MyBlog.com 서버리스 호스팅 웹사이트 소개  

Let's discuss a serverless hosted website, perhaps named MyBlog.com.  
MyBlog.com이라는 서버리스 기반 웹사이트를 논의해봅시다.  

Our website should scale globally.  
우리 웹사이트는 전 세계적으로 확장 가능해야 합니다.  

We rarely write blogs but often read them.  
우리는 블로그 글을 자주 작성하지는 않지만, 읽기는 자주 합니다.  

The blog is viewed by hundreds of thousands of people online.  
블로그는 온라인에서 수십만 명이 열람합니다.  

We typically add blogs maybe once a day or once a week.  
보통 하루에 한 번 또는 일주일에 한 번 정도 블로그 글을 작성합니다.  

Most of the time, these blogs are being read.  
대부분의 시간에는 블로그 글이 읽히고 있습니다.  

Therefore, most of the website consists of purely static files, with a small portion being a dynamic REST API.  
따라서 웹사이트 대부분은 정적 파일이고, 일부만 동적인 REST API입니다.  

We want to implement caching wherever possible to save costs and reduce latency, ensuring a great user experience.  
비용 절감과 지연 시간 최소화를 위해 가능한 모든 곳에 캐싱을 적용해 사용자 경험을 개선하고자 합니다.  

Additionally, any new user subscribing to the blog should receive a warm welcome email.  
추가로, 블로그에 새로 가입하는 사용자는 환영 이메일을 받아야 합니다.  

This entire setup should be serverless.  
이 모든 구성이 서버리스로 이루어져야 합니다.  

Also, any photo uploaded to the blog should have a thumbnail generated serverlessly, as we prefer serverless solutions.  
또한, 블로그에 업로드되는 모든 사진은 서버리스 방식으로 자동 썸네일이 생성되도록 해야 합니다.  

How do we implement all these requirements?  
그렇다면 이러한 요구사항들을 어떻게 구현할까요?  

---

## Serving Static Content Globally  
## 정적 콘텐츠 글로벌 제공  

First, we want to serve static content globally.  
먼저, 정적 콘텐츠를 전 세계적으로 제공해야 합니다.  

Our clients will access static content stored in an Amazon S3 bucket.  
클라이언트는 Amazon S3 버킷에 저장된 정적 콘텐츠에 접근합니다.  

Since the S3 bucket is region-specific, how do we expose this content globally?  
S3 버킷은 지역 단위로 존재하는데, 이를 어떻게 전 세계적으로 노출할까요?  

We use Amazon CloudFront, a global content delivery network (CDN).  
Amazon CloudFront라는 글로벌 CDN을 사용합니다.  

Clients interact with CloudFront edge locations, which cache data directly from Amazon S3.  
클라이언트는 CloudFront 엣지 로케이션과 통신하며, 이곳에서 Amazon S3 데이터를 캐싱합니다.  

This setup is straightforward and effective.  
이 구조는 간단하면서도 효과적입니다.  

We have seen CloudFront and S3 as a classic architecture for global static content delivery.  
CloudFront와 S3는 글로벌 정적 콘텐츠 제공의 고전적인 아키텍처입니다.  

---

## Securing Access to S3 Content  
## S3 콘텐츠 접근 보안 강화  

How do we secure this setup?  
이 구성을 어떻게 보안할까요?  

Clients interact with CloudFront, which is globally distributed.  
클라이언트는 전 세계적으로 분산된 CloudFront와 통신합니다.  

We add an Origin Access Control (OAC) to ensure that our Amazon S3 bucket can only be accessed by CloudFront.  
Amazon S3 버킷은 오직 CloudFront를 통해서만 접근할 수 있도록 **OAC(Origin Access Control)**를 추가합니다.  

We add a bucket policy authorizing only the CloudFront distribution.  
S3 버킷 정책을 추가하여 CloudFront 배포만 허용합니다.  

This prevents users from accessing the S3 bucket directly, securing our content effectively.  
이를 통해 사용자가 S3 버킷에 직접 접근하지 못하도록 막아 콘텐츠를 효과적으로 보호합니다.  

---

## Implementing a Public Serverless REST API  
## 공개 서버리스 REST API 구현  

Next, we add a public serverless REST API.  
다음으로, 공개용 서버리스 REST API를 추가합니다.  

Clients send REST HTTPS requests to Amazon API Gateway, which invokes Lambda functions.  
클라이언트는 REST HTTPS 요청을 API Gateway에 보내며, 이는 Lambda 함수를 호출합니다.  

These functions query and read data from DynamoDB.  
이 함수는 DynamoDB에서 데이터를 쿼리하고 읽습니다.  

Because there are many reads, we can use DAX as a caching layer to improve performance.  
읽기 요청이 많으므로 DAX를 캐싱 레이어로 사용해 성능을 개선할 수 있습니다.  

For global scalability, we can leverage DynamoDB Global Tables to reduce latency in different parts of the world, speeding up our infrastructure.  
글로벌 확장을 위해 DynamoDB 글로벌 테이블을 활용하여 지연 시간을 줄이고 인프라 속도를 높일 수 있습니다.  

---

## User Welcome Email Flow  
## 사용자 환영 이메일 흐름  

When a user subscribes, we want to send them a welcome email.  
사용자가 구독하면 환영 이메일을 보내야 합니다.  

We enable DynamoDB Streams on the user table to capture changes.  
사용자 테이블에서 변경사항을 추적하기 위해 DynamoDB Streams를 활성화합니다.  

The DynamoDB Stream triggers a Lambda function.  
DynamoDB Stream은 Lambda 함수를 트리거합니다.  

This Lambda function has an IAM role allowing it to use Amazon Simple Email Service (SES) to send emails.  
이 Lambda 함수는 Amazon SES를 이용해 이메일을 보낼 수 있도록 IAM 역할을 부여받습니다.  

This creates a serverless user welcome email flow that requires no infrastructure management and scales well.  
이로써 인프라 관리가 필요 없고 잘 확장되는 서버리스 환영 이메일 흐름이 완성됩니다.  

---

## Serverless Image Thumbnail Generation  
## 서버리스 이미지 썸네일 생성  

When users upload images, we want thumbnails to be created automatically.  
사용자가 이미지를 업로드하면 자동으로 썸네일이 생성되어야 합니다.  

Clients upload photos directly to the S3 bucket or via CloudFront using S3 Transfer Acceleration.  
클라이언트는 사진을 직접 S3 버킷에 업로드하거나 CloudFront를 통해 S3 전송 가속(Transfer Acceleration)을 사용할 수 있습니다.  

When a file is added to S3, it triggers a Lambda function.  
S3에 파일이 추가되면 Lambda 함수가 트리거됩니다.  

The Lambda function generates a thumbnail and stores it in an S3 bucket, which could be different from the original.  
Lambda 함수는 썸네일을 생성해 S3 버킷에 저장하며, 원본과 다른 버킷에 저장할 수도 있습니다.  

Amazon S3 can also trigger SQS or SNS notifications, providing flexibility in designing serverless architectures.  
Amazon S3는 SQS나 SNS 알림도 트리거할 수 있어 서버리스 아키텍처 설계에 유연성을 제공합니다.  

---

## Summary of the Serverless Architecture  
## 서버리스 아키텍처 요약  

This architecture is fully serverless and globally scalable.  
이 아키텍처는 완전 서버리스이며 글로벌 확장이 가능합니다.  

We use CloudFront with S3 for static content distribution.  
정적 콘텐츠 배포에는 CloudFront와 S3를 사용합니다.  

The REST API is serverless, implemented with API Gateway, Lambda, and DynamoDB Global Tables.  
REST API는 API Gateway, Lambda, DynamoDB 글로벌 테이블로 서버리스 방식으로 구현됩니다.  

We did not require Cognito since the REST API is public.  
REST API는 공개용이므로 Cognito는 필요하지 않습니다.  

DynamoDB Streams trigger Lambda functions for event-driven workflows like sending emails.  
DynamoDB Streams는 이메일 전송 같은 이벤트 기반 워크플로우를 위해 Lambda 함수를 트리거합니다.  

S3 triggers Lambda, SQS, or SNS for event notifications, providing flexibility.  
S3는 Lambda, SQS, SNS를 트리거해 이벤트 알림을 처리할 수 있어 유연성을 제공합니다.  

This comprehensive architecture demonstrates how to build cool applications using serverless concepts effectively.  
이 종합적인 아키텍처는 서버리스 개념을 효과적으로 활용해 멋진 애플리케이션을 구축하는 방법을 보여줍니다.  

---

## Key Takeaways  
## 핵심 요약  

- Serverless architecture enables scalable, globally distributed websites with minimal infrastructure management.  
- 서버리스 아키텍처는 최소한의 인프라 관리로 확장 가능하고 글로벌 분산 웹사이트를 지원합니다.  

- Amazon CloudFront combined with S3 provides secure, cached, and global static content delivery.  
- Amazon CloudFront와 S3를 결합하면 보안 강화, 캐싱, 글로벌 정적 콘텐츠 제공이 가능합니다.  

- Serverless REST APIs can be implemented using API Gateway, Lambda, and DynamoDB with optional caching via DAX.  
- 서버리스 REST API는 API Gateway, Lambda, DynamoDB로 구현 가능하며, DAX로 캐싱을 적용할 수 있습니다.  

- Event-driven workflows, such as user welcome emails and image thumbnail generation, can be efficiently handled using DynamoDB streams, Lambda, and Amazon SES or S3 triggers.  
- 이벤트 기반 워크플로우(예: 환영 이메일, 이미지 썸네일 생성)는 DynamoDB Streams, Lambda, Amazon SES 또는 S3 트리거로 효율적으로 처리할 수 있습니다.  

---

🎮 **게임 보상 획득!**
🏆 **"서버리스 아키텍트 2단계 달성!"**
(CloudFront + S3 + Lambda + DynamoDB + SES + Event-driven 패턴 이해 완료)
