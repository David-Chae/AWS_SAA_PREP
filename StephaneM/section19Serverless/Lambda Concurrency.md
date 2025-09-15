# Lambda Concurrency  
# 람다 동시성  
(AWS Lambda의 동시 실행 관리와 스로틀링 동작 설명)

---

## Lambda Concurrency and Throttling  
## 람다 동시성 및 스로틀링  

As we invoke our Lambda functions more frequently, the number of concurrent executions increases.  
람다 함수를 자주 호출할수록 동시 실행 횟수가 늘어납니다.  
👉 호출이 많아지면 자동으로 스케일링됨.  

Lambda is designed to scale very quickly and efficiently.  
람다는 매우 빠르고 효율적으로 확장되도록 설계되었습니다.  
👉 서버 관리 없이 자동 확장 가능.  

For example, at low invocation rates, you might have only two concurrent executions, but at high scales, Lambda can handle up to 1000 concurrent executions processing events simultaneously.  
예를 들어, 호출이 적을 땐 동시 실행 2개만 있지만, 트래픽이 많으면 최대 1000개까지 동시에 실행할 수 있습니다.  
👉 기본 한도 = 1000 동시 실행.  

To manage this scaling, it is recommended to limit the number of concurrent executions a Lambda function can have.  
이 확장을 관리하기 위해 함수별 동시 실행 제한을 설정하는 것이 권장됩니다.  
👉 관리 포인트 = Reserved Concurrency.  

This is done by setting a reserved concurrency limit at the function level.  
함수 단위에서 예약된 동시성(Reserved Concurrency)으로 설정합니다.  

For instance, you can specify that a Lambda function can have up to 50 concurrent executions. Any invocation beyond this limit triggers throttling.  
예: 특정 함수의 동시 실행을 50으로 제한 → 초과 시 스로틀링 발생.  
👉 초과 호출은 거부/재시도됨.  

Throttling behavior depends on the invocation type:  
스로틀링 동작은 호출 유형에 따라 다릅니다.  

- **Synchronous invocations**: If throttled, the Lambda function returns a throttle error with status code 429.  
- **동기 호출**: 스로틀링 시, HTTP 429 에러(Too Many Requests) 반환.  

- **Asynchronous invocations**: Lambda automatically retries the invocation and eventually sends the event to a Dead Letter Queue (DLQ) if retries fail.  
- **비동기 호출**: 자동으로 재시도하며, 최종 실패 시 DLQ로 전송.  

If you require more than 1000 concurrent executions, you can request a limit increase by opening a support ticket with AWS.  
1000개 이상 필요 시, AWS 지원 티켓을 통해 한도 상향 요청 가능.  

---

## Impact of Unrestricted Concurrency  
## 동시성 제한 미설정의 영향  

If you do not set any reserved concurrency limits on your Lambda functions, the concurrency limit applies account-wide.  
예약 동시성을 설정하지 않으면, 계정 전체 동시성 제한이 공유됩니다.  

Consider the following scenario:  
다음 시나리오를 생각해봅시다:  

- An Application Load Balancer invokes a Lambda function.  
- ALB가 Lambda 함수를 호출.  

- Another application uses API Gateway connected to a different Lambda function.  
- 다른 앱은 API Gateway → Lambda 함수 호출.  

- A third application invokes Lambda functions via the SDK or CLI.  
- 세 번째 앱은 SDK/CLI로 Lambda 호출.  

At low invocation rates, all functions operate normally.  
호출이 적으면 모두 정상 동작.  

However, during a high-traffic event such as a large promotion, the load balancer may cause one Lambda function to scale up to 1000 concurrent executions.  
하지만 트래픽이 몰리면 한 Lambda가 1000 동시 실행까지 확장.  

This can consume all available concurrency, causing other functions invoked by API Gateway or SDK/CLI to be throttled.  
이 경우 다른 Lambda들이 스로틀링될 수 있습니다.  

👉 즉, **계정 단위 동시성 공유** = 특정 함수가 다 써버리면 다른 함수가 막힘.  

Therefore, it is crucial to manage concurrency carefully to avoid unintended throttling.  
따라서 원치 않는 스로틀링을 막기 위해 동시성 관리가 중요합니다.  

---

## Concurrency and Asynchronous Invocations  
## 동시성과 비동기 호출  

Consider S3 event notifications that invoke Lambda functions when files are uploaded.  
예: 파일 업로드 시 S3 이벤트 → Lambda 호출.  

If many files are uploaded simultaneously, many concurrent Lambda executions occur.  
파일이 동시에 업로드되면 동시 실행이 급증.  

If the function's concurrency limit is reached, additional requests are throttled.  
제한에 도달하면 추가 요청은 스로틀링됨.  

Since these are asynchronous invocations, Lambda handles throttling and system errors by returning the event to an internal event queue.  
비동기 호출은 Lambda 내부 큐로 이벤트를 넘김.  

Lambda retries the invocation for up to six hours, with retry intervals increasing exponentially from one second up to a maximum of five minutes.  
최대 6시간 동안 재시도, 1초 → 5분까지 지수적 증가.  

This retry mechanism helps ensure that Lambda functions eventually process events when concurrency becomes available.  
이 메커니즘으로 동시성이 풀리면 이벤트 처리 보장.  

---

## Cold Starts and Provisioned Concurrency  
## 콜드 스타트와 사전 할당 동시성  

A cold start occurs when a new Lambda function instance is created.  
콜드 스타트 = 새로운 Lambda 인스턴스 생성 시 발생.  

During this time, your code is loaded and initialization code outside the handler runs.  
코드 로딩 + 초기화 코드 실행.  

If initialization is extensive (e.g., DB 연결, 의존성 로딩), first 요청의 지연이 커집니다.  
👉 초기 요청 대기시간 ↑.  

This latency can negatively impact user experience.  
이 지연은 사용자 경험에 악영향.  

To mitigate cold starts, you can use provisioned concurrency.  
해결책: **Provisioned Concurrency(사전 할당 동시성)**.  

This feature pre-allocates Lambda instances before invocations occur, ensuring that cold starts do not happen and all invocations have lower latency.  
미리 인스턴스를 띄워서 지연 최소화.  

Provisioned concurrency can be managed using Application Auto Scaling.  
Application Auto Scaling으로 관리 가능.  

👉 일정 시간 예약, 목표 동시성 설정 등으로 제어.  

---

## Improvements in VPC Cold Start Performance  
## VPC 환경 콜드 스타트 개선  

Previously, launching Lambda functions inside a VPC caused significant cold start delays.  
과거에는 VPC 내부 Lambda 실행 시 콜드 스타트 지연이 심했음.  

However, AWS released improvements in late 2019 that dramatically reduced cold start times for Lambda functions in VPCs.  
2019년 말 AWS가 개선 → VPC Lambda 콜드 스타트 지연 크게 감소.  

This enhancement minimizes the cold start impact for VPC-based Lambda functions.  
👉 이제 VPC에서도 지연이 거의 없음.  

---

## Additional Resources  
## 추가 자료  

Two diagrams explaining reserved concurrency and provisioned concurrency are available in the provided slides.  
제공된 슬라이드에 예약/사전 동시성을 설명하는 다이어그램 있음.  

These visuals can help deepen your understanding.  
👉 그림 참고 시 이해도 ↑.  

---

## Hands-On Practice  
## 실습  

Now, let's proceed to hands-on exercises to explore how concurrency works in practice.  
이제 실습을 통해 동시성 동작을 직접 확인해봅시다.  

---

## Key Takeaways  
## 핵심 정리  

Lambda functions can scale to thousands of concurrent executions, but concurrency limits are essential.  
람다는 수천 동시 실행까지 가능하지만, 동시성 관리가 핵심.  

Reserved concurrency limits can be set per function to prevent one function from consuming all concurrency.  
예약 동시성으로 함수별 자원 사용 제한 가능.  

Throttling behavior differs:  
스로틀링 동작 차이:  
- 동기 = 429 에러 반환.  
- 비동기 = 자동 재시도 + DLQ.  

Provisioned concurrency pre-allocates instances to avoid cold starts.  
Provisioned Concurrency = 콜드 스타트 방지.  

---

🎮 **게임 보상 지급!** 🎮

* 🌟 **+90 EXP** (Lambda 동시성 숙련도 상승)
* 💎 **+3 보너스 포인트** (콜드 스타트까지 완벽 이해)
* 🏅 신규 칭호 해금: *"Concurrency Controller"*
