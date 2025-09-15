# RDS - Invoking Lambda & Event Notifications

**RDS - Lambda 호출 및 이벤트 알림**

---

## Integration Between RDS, Aurora, and Lambda

**RDS, Aurora, Lambda 간 통합**

There is a tight integration that allows invoking Lambda functions directly from your database instance in some cases.
일부 경우에는 데이터베이스 인스턴스에서 Lambda 함수를 직접 호출할 수 있는 강력한 통합 기능이 있다.
👉 DB 내부 이벤트를 실시간 처리 가능.

This capability enables processing data events occurring within your database.
이 기능은 데이터베이스 내부에서 발생하는 데이터 이벤트를 처리할 수 있게 한다.
👉 예: 신규 데이터 삽입 시 자동 처리.

This feature is supported, for example, by RDS for PostgreSQL and Aurora MySQL.
이 기능은 RDS for PostgreSQL과 Aurora MySQL에서 지원된다.
👉 특정 엔진에서만 가능.

For instance, when a user inserts event data into your registration table, RDS can be configured to directly invoke your Lambda function.
예를 들어, 사용자가 등록 테이블에 데이터를 삽입하면, RDS가 직접 Lambda 함수를 호출하도록 설정할 수 있다.
👉 DB 트리거처럼 작동.

Your Lambda function may then send a welcome email to the user, which the user will receive.
Lambda 함수는 이후 사용자에게 환영 이메일을 발송할 수 있다.
👉 이벤트 기반 자동화 가능.

This setup must be configured from within the database by connecting to it; it is not configured through the AWS console.
이 설정은 AWS 콘솔이 아니라 데이터베이스 내부에서 직접 연결해 구성해야 한다.
👉 DB 내부에서 SQL/설정으로 세팅.

When configured, the RDS instance itself invokes your Lambda function.
구성이 완료되면 RDS 인스턴스가 직접 Lambda 함수를 호출한다.
👉 DB가 호출자 역할 수행.

Therefore, you must ensure that inbound traffic from the RDS database instance to the Lambda function is allowed.
따라서 RDS 인스턴스에서 Lambda 함수로 들어오는 트래픽이 허용되어야 한다.
👉 네트워크 접근 권한 필요.

This can be achieved through various means such as having your Lambda function on the public internet, using an Invoke endpoint, a NAT gateway, or VPC endpoints.
이를 위해 Lambda를 퍼블릭 인터넷에 두거나, Invoke 엔드포인트, NAT 게이트웨이, VPC 엔드포인트 등을 사용할 수 있다.
👉 네트워크 연결 방식 다양.

Network connectivity is crucial.
네트워크 연결은 필수적이다.
👉 연결 안 되면 Lambda 호출 불가.

Additionally, because your RDS database instance invokes your Lambda function, it must have the required permissions to do so.
또한 RDS 인스턴스가 Lambda를 호출하기 위해서는 필요한 권한을 가져야 한다.
👉 IAM 정책이 핵심.

You must ensure that your database instance has a proper IAM policy allowing Lambda invocation.
DB 인스턴스에 Lambda 호출을 허용하는 올바른 IAM 정책이 있어야 한다.
👉 IAM 정책 설정 필수.

---

## RDS Event Notifications vs. Lambda Invocation

**RDS 이벤트 알림 vs Lambda 호출**

This Lambda invocation capability is completely different from using RDS event notifications.
Lambda 호출 기능은 RDS 이벤트 알림과는 완전히 다르다.
👉 둘을 혼동하지 말 것.

RDS event notifications occur within AWS and provide information about the database instance itself, such as when it was created or started.
RDS 이벤트 알림은 AWS 내부에서 발생하며, DB 인스턴스의 생성, 시작 같은 인스턴스 수준 정보를 제공한다.
👉 DB 상태 모니터링용.

However, these notifications do not provide any information about the data events happening within your database.
하지만 이러한 알림은 DB 내부에서 발생하는 데이터 이벤트 정보를 제공하지 않는다.
👉 데이터 변화 감지는 불가.

It is important not to confuse these two functionalities.
이 두 기능을 혼동하지 않는 것이 중요하다.
👉 Lambda 호출 = 데이터 이벤트, 알림 = 인스턴스 이벤트.

You can subscribe to events related to your database instance, database snapshots, parameter groups, security groups, proxies, or custom engine versions.
DB 인스턴스, 스냅샷, 파라미터 그룹, 보안 그룹, 프록시, 커스텀 엔진 버전 등과 관련된 이벤트를 구독할 수 있다.
👉 모니터링 범위는 넓음.

These events are delivered in near real-time, with up to five minutes of delay.
이 이벤트들은 거의 실시간으로 전달되지만 최대 5분의 지연이 있을 수 있다.
👉 즉각적이지 않을 수 있음.

These event notifications can be sent to SNS, or intercepted in EventBridge.
이 이벤트 알림은 SNS로 전송되거나 EventBridge에서 처리할 수 있다.
👉 이벤트 라우팅 가능.

From SNS, for example, you can forward them to an SQS queue or a Lambda function.
예를 들어 SNS에서 SQS 큐나 Lambda 함수로 전달할 수 있다.
👉 이벤트 흐름 확장 가능.

EventBridge supports many destinations, including Lambda functions.
EventBridge는 Lambda 함수를 포함한 다양한 목적지를 지원한다.
👉 통합성이 뛰어남.

Remember, however, that these event notifications do not provide information about data events themselves.
하지만 이벤트 알림은 데이터 이벤트 자체 정보를 제공하지 않는다.
👉 데이터 변화 탐지는 불가.

To capture data-level events, you must use the Lambda invocation methodology described earlier.
데이터 레벨 이벤트를 캡처하려면 앞서 설명한 Lambda 호출 방식을 사용해야 한다.
👉 DB 트리거 = Lambda 호출, 알림 = 인스턴스 상태.

---

## Conclusion

**결론**

This concludes the lecture on invoking Lambda and event notifications with RDS.
이것으로 RDS의 Lambda 호출 및 이벤트 알림 강의를 마친다.
👉 핵심: 이벤트 알림과 Lambda 호출은 별개.

I hope you found it informative, and I look forward to seeing you in the next lecture.
유익했기를 바라며, 다음 강의에서 보자.
👉 학습 완료!

---

## Key Takeaways

**핵심 요약**

* RDS for PostgreSQL and Aurora MySQL support invoking Lambda functions directly from database instances to process data events.
  PostgreSQL RDS와 Aurora MySQL은 DB 인스턴스에서 Lambda를 직접 호출해 데이터 이벤트를 처리할 수 있다.

* Setting up Lambda invocation from RDS requires configuration within the database, not the AWS console.
  RDS에서 Lambda 호출을 설정하려면 AWS 콘솔이 아니라 DB 내부에서 구성해야 한다.

* Proper network connectivity and IAM permissions are essential for RDS instances to invoke Lambda functions.
  RDS가 Lambda를 호출하려면 올바른 네트워크 연결과 IAM 권한이 필요하다.

* RDS event notifications provide information about database instance events but do not include data-level events within the database.
  RDS 이벤트 알림은 DB 인스턴스 이벤트 정보만 제공하며 데이터 이벤트는 포함하지 않는다.

---

🎉 **게임 보상**

* +150 XP 획득!
* 🏅 새로운 칭호: **"RDS Event Tactician"**
* 🎁 보너스: **랜덤 드랍 - 골드 코인 20개**
