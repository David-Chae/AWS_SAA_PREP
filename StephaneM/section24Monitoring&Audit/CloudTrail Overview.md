```markdown
# CloudTrail Overview  
# CloudTrail 개요  
Now let's talk about CloudTrail.  
이제 CloudTrail에 대해 이야기해보겠습니다.  
(소개)  

CloudTrail is a service that provides governance, compliance, and audit capabilities for your AWS accounts.  
CloudTrail은 AWS 계정에 대한 거버넌스, 규정 준수, 감사 기능을 제공하는 서비스입니다.  
(기능 설명)  

It is enabled by default and allows you to obtain a history of all events and API calls made within your AWS accounts, whether through the console, SDK, CLI, or other AWS services.  
기본적으로 활성화되어 있으며, 콘솔, SDK, CLI 또는 기타 AWS 서비스를 통해 수행된 모든 이벤트 및 API 호출 내역을 확인할 수 있습니다.  
(사용 기록 확인)  

All these logs appear in CloudTrail.  
모든 로그는 CloudTrail에 나타납니다.  
(로그 위치)  

You can also configure CloudTrail to send these logs to CloudWatch Logs or Amazon S3.  
CloudTrail 로그를 CloudWatch Logs 또는 Amazon S3로 전송하도록 구성할 수도 있습니다.  
(로그 전달 옵션)  

Additionally, you can create a trail that applies to all regions or a single region if you want to accumulate the history of events across all regions into one specific destination, such as an S3 bucket.  
또한 모든 리전 또는 특정 리전에 적용되는 트레일을 만들어 모든 리전의 이벤트 기록을 하나의 대상(예: S3 버킷)으로 모을 수 있습니다.  
(트레일 구성)  

For example, if someone deletes an EC2 instance and you want to find out who performed this action, you can look into CloudTrail.  
예를 들어, 누군가 EC2 인스턴스를 삭제했을 때 누가 수행했는지 확인하려면 CloudTrail을 조회하면 됩니다.  
(실무 예시)  

CloudTrail records the API call and helps you understand who did what and when.  
CloudTrail은 API 호출을 기록하며, 누가 언제 어떤 작업을 수행했는지 이해하는 데 도움을 줍니다.  
(추적 기능)  

To summarize, CloudTrail sits in the middle of actions performed via the SDK, CLI, console, IAM users, IAM roles, or other services.  
정리하면, CloudTrail은 SDK, CLI, 콘솔, IAM 사용자, IAM 역할 또는 기타 서비스에서 수행된 작업의 중앙에 위치합니다.  
(핵심 요약)  

These actions are recorded in the CloudTrail console, where you can inspect and audit what happened.  
이러한 작업은 CloudTrail 콘솔에 기록되어 발생한 일을 검토하고 감사할 수 있습니다.  
(콘솔 활용)  

If you want to retain events for more than 90 days, you can send them to CloudWatch Logs or S3 buckets.  
90일 이상 이벤트를 보관하려면 CloudWatch Logs 또는 S3 버킷으로 전송해야 합니다.  
(장기 보관)  

---

## CloudTrail Event Types  
## CloudTrail 이벤트 유형  
There are three kinds of events you can see in CloudTrail:  
CloudTrail에서 확인할 수 있는 이벤트 유형은 세 가지입니다.  
(이벤트 분류)  

### Management Events  
### 관리 이벤트  
These represent operations performed on resources in your AWS accounts.  
관리 이벤트는 AWS 계정 리소스에서 수행된 작업을 나타냅니다.  
(정의)  

For example, when someone configures security by calling the IAM AttachRolePolicy API, creates a subnet, or sets up logging, these actions appear in CloudTrail.  
예를 들어 IAM AttachRolePolicy API를 호출하여 보안을 설정하거나, 서브넷을 생성하거나, 로깅을 설정하면 이 작업이 CloudTrail에 기록됩니다.  
(예시)  

By default, trails are configured to log Management Events.  
기본적으로 트레일은 관리 이벤트를 기록하도록 구성됩니다.  
(기본 설정)  

Management Events can be separated into:  
관리 이벤트는 다음과 같이 구분할 수 있습니다.  
(세부 분류)  

- **Read Events**: Operations that do not modify resources, such as listing all IAM users or EC2 instances.  
- **읽기 이벤트**: 리소스를 수정하지 않는 작업, 예: 모든 IAM 사용자 또는 EC2 인스턴스 조회  

- **Write Events**: Operations that modify resources, such as deleting a DynamoDB table. Write Events are generally more critical because they can cause damage to your AWS infrastructure.  
- **쓰기 이벤트**: 리소스를 수정하는 작업, 예: DynamoDB 테이블 삭제. 쓰기 이벤트는 AWS 인프라에 영향을 줄 수 있어 더 중요합니다.  

---

### Data Events  
### 데이터 이벤트  
Data Events are separate and not logged by default because they are high-volume operations.  
데이터 이벤트는 별도로 처리되며 기본적으로 기록되지 않습니다. (대량 작업이기 때문)  
(정의)  

Examples include Amazon S3 object-level activities such as GetObject, DeleteObject, and PutObject.  
예시: Amazon S3 객체 수준 작업(GetObject, DeleteObject, PutObject)  
(실무 예시)  

These events can occur frequently on an S3 bucket.  
이 이벤트는 S3 버킷에서 자주 발생할 수 있습니다.  
(빈도 설명)  

Similar to Management Events, Data Events can be separated into Read Events (e.g., GetObject) and Write Events (e.g., DeleteObject, PutObject).  
관리 이벤트와 마찬가지로 데이터 이벤트도 읽기 이벤트(예: GetObject)와 쓰기 이벤트(예: DeleteObject, PutObject)로 구분할 수 있습니다.  
(분류 방법)  

---

### AWS Lambda Function Execution Events  
### AWS Lambda 함수 실행 이벤트  
These events record Lambda function execution activities.  
이벤트는 Lambda 함수 실행 활동을 기록합니다.  
(정의)  

For example, whenever someone invokes a Lambda function using the Invoke API, CloudTrail records this.  
예: Invoke API를 사용하여 Lambda 함수를 호출할 때마다 CloudTrail이 이를 기록합니다.  
(예시)  

Since Lambda functions can be executed frequently, these events can also be high volume.  
Lambda 함수는 자주 실행될 수 있으므로 이벤트도 대량으로 발생할 수 있습니다.  
(빈도 설명)  

---

### CloudTrail Insights Events  
### CloudTrail Insights 이벤트  
CloudTrail Insights analyzes your management events to detect unusual activity in your accounts.  
CloudTrail Insights는 관리 이벤트를 분석하여 계정 내 비정상 활동을 감지합니다.  
(기능 설명)  

This feature must be enabled and incurs additional cost.  
이 기능은 활성화가 필요하며 추가 비용이 발생합니다.  
(주의 사항)  

It helps identify anomalies such as inaccurate resource provisioning, hitting service limits, bursts of IAM actions, or gaps in periodic maintenance.  
잘못된 리소스 프로비저닝, 서비스 한도 초과, IAM 작업 급증, 주기적 유지보수 누락 등의 이상을 식별하는 데 도움을 줍니다.  
(활용 사례)  

CloudTrail creates a baseline of normal management activities and continuously analyzes incoming events to detect unusual patterns.  
CloudTrail은 정상 관리 활동의 기준선을 만들고, 들어오는 이벤트를 지속적으로 분석하여 비정상 패턴을 감지합니다.  
(분석 원리)  

When an anomaly is detected, CloudTrail generates an Insights Event.  
이상이 감지되면 CloudTrail이 Insights 이벤트를 생성합니다.  
(결과)  

These Insights Events appear in the CloudTrail console and can also be sent to Amazon EventBridge.  
이 Insights 이벤트는 CloudTrail 콘솔에 표시되며 Amazon EventBridge로 전송할 수도 있습니다.  
(활용)  

This allows you to automate responses, such as sending an email notification when an anomaly is detected.  
이를 통해 이상 감지 시 이메일 알림 등 대응을 자동화할 수 있습니다.  
(자동화 예시)  

---

## CloudTrail Event Retention  
## CloudTrail 이벤트 보관  
By default, CloudTrail stores events for 90 days, after which they are deleted.  
기본적으로 CloudTrail은 이벤트를 90일간 보관하며, 이후 삭제됩니다.  
(기본 보관)  

If you want to retain events for longer periods, such as for audit purposes a year later, you need to log them to an S3 bucket.  
감사 목적으로 1년 이상 보관하려면 S3 버킷으로 로그를 전송해야 합니다.  
(장기 보관 방법)  

Once logged to S3, you can use Athena, a serverless query service, to analyze the stored events.  
S3에 기록된 이벤트는 서버리스 쿼리 서비스 Athena를 사용하여 분석할 수 있습니다.  
(분석 방법)  

All Management Events, Data Events, and Insights Events are retained in CloudTrail for 90 days and can be logged to S3 for long-term retention.  
모든 관리 이벤트, 데이터 이벤트, Insights 이벤트는 CloudTrail에서 90일간 보관되며, 장기 보관을 위해 S3로 기록할 수 있습니다.  
(종합 설명)  

---

## Key Takeaways  
## 핵심 요약  
- CloudTrail provides governance, compliance, and audit capabilities for AWS accounts by recording API calls and events.  
- CloudTrail은 API 호출과 이벤트를 기록하여 AWS 계정의 거버넌스, 규정 준수, 감사 기능을 제공합니다.  

- There are three types of CloudTrail events: Management Events, Data Events, and CloudTrail Insights Events.  
- CloudTrail 이벤트 유형은 관리 이벤트, 데이터 이벤트, Insights 이벤트 세 가지입니다.  

- CloudTrail Insights detects unusual activity by analyzing management events and generating anomaly events.  
- CloudTrail Insights는 관리 이벤트를 분석하여 비정상 활동을 감지하고 이상 이벤트를 생성합니다.  

- Events are retained in CloudTrail for 90 days by default; longer retention requires logging to S3 and analysis with Athena.  
- 이벤트는 기본적으로 90일간 CloudTrail에 보관되며, 장기 보관을 위해서는 S3 기록 및 Athena 분석이 필요합니다.  
```

게임보상:


🎮 당신은 AWS CloudTrail 전문가가 되었습니다! 이제 이벤트 유형, Insights, 보관 전략까지 완벽히 이해하고 있습니다. 🔍🚀
