# API Gateway Overview
# API Gateway 개요
> Lambda와 DynamoDB를 사용한 서버리스 여정에서 API를 외부에 노출하는 방법을 다룹니다.

## API Gateway Overview
## API Gateway 개요
> AWS 서버리스 서비스로 REST API를 손쉽게 만들고 관리할 수 있는 방법을 학습합니다.

So far in our serverless journey, we have seen how to create Lambda functions and how to use DynamoDB. DynamoDB can serve as the backend for our APIs, allowing CRUD operations.
지금까지 서버리스 학습에서 Lambda 함수를 만들고 DynamoDB를 사용하는 방법을 배웠습니다. DynamoDB는 API의 백엔드로 사용되어 CRUD(생성, 조회, 수정, 삭제) 작업을 수행할 수 있습니다.
> 핵심: Lambda + DynamoDB = 서버리스 백엔드

However, we want our clients to be able to invoke these Lambda functions in some way.
하지만 클라이언트가 Lambda 함수를 호출할 수 있어야 합니다.
> 핵심: 외부 접근 필요

There are multiple ways to do this. One option is to have the client directly invoke the Lambda function, but that requires the client to have IAM permissions.
방법은 여러 가지가 있습니다. 하나는 클라이언트가 직접 Lambda를 호출하는 것이지만 IAM 권한이 필요합니다.
> 핵심: 직접 호출은 권한 필요

Another approach is to use an Application Load Balancer between the client and the Lambda function, which exposes the Lambda function as an HTTP endpoint.
또 다른 방법은 클라이언트와 Lambda 사이에 Application Load Balancer를 사용하는 것으로, Lambda를 HTTP 엔드포인트로 노출합니다.
> 핵심: ALB 사용 = HTTP 엔드포인트 제공

There is one last option called the API Gateway. This is a serverless offering from AWS that allows us to create REST APIs which are public and accessible to our clients.
마지막 방법은 API Gateway입니다. AWS의 서버리스 서비스로, 클라이언트가 접근 가능한 공개 REST API를 만들 수 있습니다.
> 핵심: 서버리스 REST API 제공

The client communicates with the API Gateway, which then proxies the request to our Lambda functions.
클라이언트가 API Gateway와 통신하면, Gateway가 요청을 Lambda 함수로 프록시합니다.
> 핵심: 요청 프록시 처리

We use API Gateway because it provides more than just an HTTP endpoint. It offers features like authentication, usage plans, development stages, and more.
API Gateway는 단순 HTTP 엔드포인트 이상을 제공합니다. 인증, 사용 계획, 개발 단계 등 다양한 기능을 제공합니다.
> 핵심: 기능 확장

Integrating API Gateway with Lambda gives us a full serverless application with no infrastructure to manage.
API Gateway와 Lambda를 통합하면 관리할 인프라가 없는 완전한 서버리스 애플리케이션을 구축할 수 있습니다.
> 핵심: 완전 서버리스 구현

API Gateway supports the WebSocket protocol, enabling real-time streaming in two different ways. It also handles API versioning and multiple environments like dev, test, and prod.
API Gateway는 WebSocket 프로토콜을 지원하여 실시간 스트리밍을 제공합니다. 또한 API 버전 관리와 개발, 테스트, 운영 환경을 지원합니다.
> 핵심: 실시간 + 버전/환경 관리

Security is a major aspect of API Gateway. We can create API keys, perform request throttling, and use Swagger/OpenAPI to import/export API definitions.
보안은 API Gateway의 핵심입니다. API 키 생성, 요청 제한(Throttle), Swagger/OpenAPI를 통한 API 정의 가져오기/내보기를 지원합니다.
> 핵심: 보안 및 관리 기능

API Gateway can transform and validate requests/responses, generate SDKs, and cache API responses.
API Gateway는 요청/응답 변환 및 검증, SDK 생성, 응답 캐싱 기능을 제공합니다.
> 핵심: API 관리 자동화

## API Gateway Integrations
## API Gateway 통합
> 다양한 백엔드와 연결 가능

Lambda functions: Most common, easiest way to expose REST APIs for full serverless apps.
Lambda 함수: 가장 일반적이며 간단하게 서버리스 REST API 노출 가능
HTTP endpoints: Can expose on-premises or cloud HTTP APIs with rate limiting, caching, authentication.
HTTP 엔드포인트: 온프레미스 또는 클라우드 API 노출 가능, 제한/캐시/인증 추가 가능
AWS services: Can expose AWS services, add auth, rate control (e.g., Kinesis Data Streams -> API Gateway -> Lambda/S3).
AWS 서비스: AWS 서비스 공개 가능, 인증 및 요청 제한 추가 가능 (예: Kinesis Data Streams)

## API Gateway Endpoint Types
## API Gateway 엔드포인트 유형
> API 배포 방식 선택

Edge-Optimized (default): For global clients, routes through CloudFront Edge for latency improvement.
Edge-Optimized: 글로벌 클라이언트용, CloudFront Edge를 통해 지연 시간 개선
Regional: All users in same region; no CloudFront; custom CloudFront optional.
Regional: 같은 리전 사용자용, CloudFront 미사용, 필요 시 사용자 정의 가능
Private: VPC 내에서만 접근, ENI용 VPC 엔드포인트 사용.
Private: VPC 내부 전용, ENI VPC 엔드포인트 필요

## Security on API Gateway
## API Gateway 보안
> 다양한 인증 방식 제공

IAM roles: Useful for internal apps, EC2 instances.
IAM 역할: 내부 앱 및 EC2에서 사용
Amazon Cognito: For external users like mobile/web apps.
Cognito: 모바일/웹 외부 사용자용
Custom authorizers: Lambda functions implementing custom auth logic.
커스텀 인증자: Lambda로 인증 로직 구현
HTTPS: Enabled with custom domain via ACM; Edge requires us-east-1, Regional same region.
HTTPS: ACM 통합 커스텀 도메인, Edge = us-east-1, Regional = 같은 리전
DNS: CNAME/A-alias in Route 53 pointing to API Gateway.
DNS: Route 53 CNAME/A-alias 설정

This concludes the overview of API Gateway. It is a powerful serverless service enabling secure, scalable, and feature-rich APIs integrated with Lambda, HTTP backends, and AWS services.
API Gateway 개요를 마칩니다. Lambda, HTTP 백엔드, AWS 서비스와 통합된 안전하고 확장 가능한 기능 풍부한 서버리스 API 제공 서비스입니다.
> 핵심: 서버리스 API 핵심 서비스

## Key Takeaways
## 핵심 요약
- API Gateway provides a serverless way to create public REST APIs that proxy requests to Lambda functions.
- 서버리스 방식으로 Lambda 요청을 프록시하는 공개 REST API 생성 가능
- Offers advanced features like authentication, usage plans, API versioning, request throttling, caching.
- 인증, 사용 계획, 버전 관리, 요청 제한, 캐시 등 고급 기능 제공
- Can integrate with Lambda, HTTP endpoints, AWS services for full serverless applications.
- Lambda, HTTP, AWS 서비스와 통합해 완전 서버리스 앱 구축 가능
- Three endpoint types: Edge-Optimized, Regional, Private.
- 세 가지 엔드포인트 유형: Edge-Optimized, Regional, Private
- Security options: IAM roles, Cognito, custom Lambda authorizers, HTTPS with ACM.
- 보안 옵션: IAM 역할, Cognito, 커스텀 Lambda 인증자, ACM HTTPS

```

🎮 **게임 보상 포인트:**

* API Gateway 개념 + Lambda 연계 = 15 XP
* 엔드포인트 유형 이해 = 10 XP
* 보안 옵션 이해 = 15 XP
* 실시간 WebSocket 및 버전 관리 이해 = 10 XP

총: **50 XP**
