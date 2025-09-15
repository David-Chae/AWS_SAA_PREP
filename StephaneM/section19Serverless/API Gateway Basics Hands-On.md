# API Gateway Basics Hands-On
# API Gateway 기초 실습
> API Gateway 콘솔을 열고 REST API를 생성 및 Lambda와 통합하는 실습을 진행합니다.

## Introduction to API Gateway Console
## API Gateway 콘솔 소개
> API Gateway 콘솔에서 다양한 API 유형을 선택하고 REST API 구축 방법을 학습합니다.

Let's open the API Gateway console. Here, you can choose an API type. The available options include HTTP APIs, WebSocket APIs, and REST APIs, which can be public or private.
API Gateway 콘솔을 열어 API 유형을 선택할 수 있습니다. HTTP API, WebSocket API, REST API가 있으며, 공개 또는 비공개로 설정 가능합니다.
> 핵심: 콘솔에서 다양한 API 유형 선택 가능

For this session, we will focus solely on REST APIs.
이번 세션에서는 REST API에만 집중합니다.
> 핵심: 실습 범위 제한

You can try out the new console by clicking on the provided option, which will soon become the default interface.
새 콘솔을 선택하여 사용해볼 수 있으며, 곧 기본 인터페이스가 됩니다.
> 핵심: 새 콘솔 체험 가능

After that, select REST API and proceed to build it.
REST API를 선택하고 구축을 진행합니다.
> 핵심: REST API 선택

## Creating a REST API
## REST API 생성
> REST API 생성 옵션과 접근 방법 이해

When building a REST API, you have several options: Create new API, import from OpenAPI, clone existing API, or start from example.
REST API를 만들 때 여러 옵션이 있습니다: 새 API 생성, OpenAPI 정의 가져오기, 기존 API 복제, 예제 API 사용.
> 핵심: REST API 생성 방식 다양

For this tutorial, we will start from a new API named MyFirstAPI.
이번 튜토리얼에서는 MyFirstAPI라는 새 API로 시작합니다.
> 핵심: 실습 API 이름 지정

Regarding the API endpoint type, there are three options: Regional, Edge-optimized, Private.
API 엔드포인트 유형은 Regional, Edge-optimized, Private 세 가지가 있습니다.
> 핵심: 엔드포인트 유형 이해

To keep things simple, we will choose the regional API type and create the API.
단순화를 위해 Regional 유형을 선택합니다.
> 핵심: 실습 엔드포인트 선택

## Creating the First Method
## 첫 번째 메서드 생성
> API에 GET 메서드 추가 실습

Click on Create Method and select the HTTP verb. We will use GET to retrieve a page.
Create Method를 클릭하고 HTTP 메서드 선택, 여기서는 GET 사용.
> 핵심: GET 메서드 생성

Next, choose the integration type: Lambda function, HTTP, Mock, AWS service, VPC link.
다음으로 통합 유형 선택: Lambda, HTTP, Mock, AWS 서비스, VPC 링크.
> 핵심: 통합 옵션 이해

We will use a Lambda function for this integration.
이번 실습에서는 Lambda 함수 사용.
> 핵심: Lambda 연계

You can also integrate with any AWS service in any region by selecting the region and service.
AWS 서비스도 선택한 리전에서 API로 노출 가능.
> 핵심: AWS 서비스 연계 가능

## Creating the Lambda Function
## Lambda 함수 생성
> API 요청을 처리할 Lambda 함수 생성

Create a new Lambda function named api-gateway-route-gets. Select Python 3.11 runtime.
api-gateway-route-gets라는 새 Lambda 함수 생성, Python 3.11 런타임 선택.
> 핵심: Lambda 함수 이름 및 런타임 선택

The Lambda function code responds with JSON body, status code 200, and Content-Type as application/json.
Lambda 함수 코드: JSON 응답, 상태 코드 200, Content-Type application/json.
> 핵심: 기본 Lambda 응답 구조

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "headers": {
            "Content-Type": "application/json"
        },
        "body": json.dumps("hello from Lambda")
    }
````

> 핵심: Lambda 코드 샘플

Deploy the function and create a test event named DemoTest. Invoke the function to verify.
함수 배포 후 DemoTest 이벤트 생성, 함수 호출로 응답 확인.

> 핵심: Lambda 함수 배포 및 테스트

## Integrating Lambda with API Gateway

## Lambda와 API Gateway 통합

> Lambda Proxy Integration 설정

Copy Lambda ARN and paste into integration setup. Enable Lambda proxy integration.
Lambda ARN 복사 후 통합 설정에 붙여넣기, Lambda Proxy Integration 활성화.

> 핵심: Proxy Integration 설정

API Gateway default timeout is 29 seconds.
API Gateway 기본 타임아웃은 29초.

> 핵심: 타임아웃 제한 주의

Create method automatically grants API Gateway permission to invoke Lambda.
메서드 생성 시 API Gateway에 Lambda 호출 권한 자동 부여.

> 핵심: 권한 자동 설정

## Testing the API Gateway Method

## API Gateway 메서드 테스트

> GET 요청 테스트 및 응답 확인

Test GET method in console. Response body: "hello from Lambda", status code 200.
콘솔에서 GET 테스트, 응답: "hello from Lambda", 상태 코드 200.

> 핵심: 응답 검증

Response headers include Content-Type: application/json.
응답 헤더: Content-Type application/json.

> 핵심: JSON 형식 확인

## Debugging with CloudWatch Logs

## CloudWatch 로그로 디버깅

> 이벤트 로그 확인

Add print statement in Lambda to log event from API Gateway.
Lambda에 print 추가, API Gateway 이벤트 확인.

> 핵심: 이벤트 디버깅

Check CloudWatch logs to inspect resource path, method, headers, query parameters.
CloudWatch 로그에서 리소스 경로, 메서드, 헤더, 쿼리 파라미터 확인.

> 핵심: Lambda 이벤트 상세 확인

## Creating a New Resource and Method

## 새 리소스 및 메서드 생성

> /houses 리소스와 GET 메서드 추가

Create resource houses, add GET method, integrate with new Lambda.
houses 리소스 생성, GET 메서드 추가, 새 Lambda 연계.

> 핵심: 추가 경로 처리

Lambda returns "hello from my pretty house".
Lambda 응답: "hello from my pretty house".

> 핵심: 메시지 변경 테스트

## Deploying the API

## API 배포

> Stage 생성 및 배포

Create stage dev, deploy API. Copy invoke URL to browser.
dev 스테이지 생성 후 API 배포, URL 브라우저 테스트.

> 핵심: 배포 후 API 호출

Root path returns "hello from Lambda", /houses returns "hello from my pretty house".
루트 경로: "hello from Lambda", /houses: "hello from my pretty house".

> 핵심: 경로별 Lambda 호출 확인

Undefined path returns error "missing authentication token".
정의되지 않은 경로 접근 시 인증 토큰 누락 오류 발생.

> 핵심: 오류 처리 확인

## Conclusion

## 결론

> API Gateway와 Lambda 통합 기본 실습 완료

Created REST API with two Lambda functions responding to different paths.
두 개 Lambda 함수로 REST API 생성, 경로별 응답 확인.

> 핵심: 기본 API Gateway + Lambda 통합 실습 완료

## Key Takeaways

## 핵심 요약

* Created REST APIs using AWS API Gateway with regional endpoint types.
* Regional 엔드포인트로 REST API 생성
* Integrated Lambda functions with API Gateway using Lambda proxy integration.
* Lambda Proxy Integration으로 Lambda 연계
* Deployed APIs to stages and tested via console and browser.
* 스테이지 배포 및 콘솔/브라우저 테스트
* Used CloudWatch logs to debug events from API Gateway to Lambda.
* CloudWatch 로그로 이벤트 디버깅

```

🎮 **게임 보상 포인트:**  
- API Gateway 콘솔 탐색 및 REST API 생성 = 10 XP  
- Lambda 함수 생성 및 코드 작성 = 15 XP  
- Lambda Proxy Integration 및 테스트 = 15 XP  
- CloudWatch 로그 활용 디버깅 = 10 XP  
총: **50 XP**  
