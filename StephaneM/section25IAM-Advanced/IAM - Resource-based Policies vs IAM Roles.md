```markdown
# IAM - Resource-based Policies vs IAM Roles  
# IAM - 리소스 기반 정책 vs IAM 역할  

## Fundamental Differences Between IAM Roles and Resource-Based Policies  
## IAM 역할과 리소스 기반 정책의 근본적인 차이  

In this lecture, we examine the fundamental differences between IAM roles and resource-based policies. When performing cross-account API calls, such as accessing an Amazon S3 bucket in another account, there are two options:  
이번 강의에서는 IAM 역할과 리소스 기반 정책의 근본적인 차이를 살펴봅니다. 다른 계정의 Amazon S3 버킷에 접근하는 것과 같은 크로스 계정 API 호출을 수행할 때 두 가지 옵션이 있습니다.  
(크로스 계정 접근 시 선택지 소개)  

- Attach a resource-based policy directly to the resource, for example, an S3 bucket policy on an S3 bucket.  
- 리소스에 직접 리소스 기반 정책을 첨부합니다. 예: S3 버킷의 S3 버킷 정책.  
(리소스 기반 정책 방식)  

- Use an IAM role that has permissions to access the resource.  
- 리소스 접근 권한이 있는 IAM 역할을 사용합니다.  
(IAM 역할 방식)  

Let's explore an example illustrating these two options.  
이 두 가지 옵션을 설명하는 예제를 살펴보겠습니다.  
(실제 예제 시작)  

---

## Example Scenario  
## 예제 시나리오  

Consider a user in Account A who can assume a role in Account B. This role has permissions to access Amazon S3 buckets in Account B. Alternatively, the user in Account A can access the S3 buckets in Account B through a bucket policy attached to the S3 bucket in Account B.  
계정 A의 사용자가 계정 B의 역할을 맡을 수 있다고 가정합니다. 이 역할은 계정 B의 Amazon S3 버킷에 접근할 수 있는 권한을 갖습니다. 또는 계정 A의 사용자가 계정 B의 S3 버킷에 버킷 정책을 통해 접근할 수도 있습니다.  
(두 접근 방법 비교)  

Both approaches are valid, but there are important differences.  
두 접근 방식 모두 유효하지만, 중요한 차이점이 있습니다.  
(차이점 강조)  

---

## Key Difference Between IAM Roles and Resource-Based Policies  
## IAM 역할과 리소스 기반 정책의 주요 차이  

When you assume a role, you give up all your original permissions and adopt all the permissions assigned to the role. This means that after assuming the role, you can perform any action allowed by the role, but you cannot use your original permissions.  
역할을 맡으면 원래 가지고 있던 모든 권한을 포기하고 역할에 할당된 모든 권한을 사용하게 됩니다. 즉, 역할을 맡은 후에는 역할이 허용하는 작업을 수행할 수 있지만, 원래 권한은 사용할 수 없습니다.  
(역할 전환 시 권한 변경)  

When using a resource-based policy, the principal does not assume a role and therefore retains their original permissions.  
리소스 기반 정책을 사용할 때는 주체가 역할을 맡지 않으므로 원래 권한을 그대로 유지합니다.  
(리소스 정책 시 권한 유지)  

---

## Practical Use Case  
## 실제 사용 사례  

For example, a user in Account A needs to scan a DynamoDB table in Account A and then dump the data into an S3 bucket in Account B. In this case, using a resource-based policy is preferable because the user does not have to assume a role. This allows the user to both scan the DynamoDB table and write to the S3 bucket in another account seamlessly.  
예를 들어, 계정 A의 사용자가 계정 A의 DynamoDB 테이블을 스캔한 후 데이터를 계정 B의 S3 버킷에 덤프해야 한다고 가정합니다. 이 경우, 사용자가 역할을 맡을 필요가 없으므로 리소스 기반 정책을 사용하는 것이 더 좋습니다. 이렇게 하면 사용자가 DynamoDB 테이블 스캔과 다른 계정의 S3 버킷 쓰기를 동시에 수행할 수 있습니다.  
(리소스 기반 정책 활용 예시)  

---

## Support for Resource-Based Policies Across AWS Services  
## AWS 서비스에서 리소스 기반 정책 지원  

Resource-based policies are increasingly supported by various AWS services and resources over time. Examples include:  
리소스 기반 정책은 시간이 지남에 따라 다양한 AWS 서비스와 리소스에서 점점 더 지원되고 있습니다. 예시는 다음과 같습니다:  
(지원 서비스 소개)  

- Amazon S3 buckets  
- Amazon S3 버킷  
- SNS topics  
- SNS 주제  
- SQS queues  
- SQS 큐  
- Lambda functions  
- Lambda 함수  

This support is significant when using services like Amazon EventBridge.  
이 지원은 Amazon EventBridge와 같은 서비스를 사용할 때 중요합니다.  
(EventBridge 활용 맥락)  

---

## EventBridge and Permissions  
## EventBridge와 권한  

When an EventBridge rule runs, it requires permissions on the target resources. If the target supports resource-based policies, such as Lambda functions, SNS topics, SQS queues, S3 buckets, or API Gateway, EventBridge can add a resource-based policy on the target to allow invocation from the EventBridge rule.  
EventBridge 규칙이 실행될 때, 대상 리소스에 대한 권한이 필요합니다. 대상이 Lambda 함수, SNS 주제, SQS 큐, S3 버킷, API Gateway와 같이 리소스 기반 정책을 지원하면 EventBridge는 대상에 리소스 기반 정책을 추가하여 EventBridge 규칙에서 호출할 수 있도록 합니다.  
(리소스 정책과 EventBridge 호출)  

If the resource does not support resource-based policies, EventBridge uses an IAM role to invoke the target service. Examples of such targets include Kinesis Stream, EC2 Auto Scaling, Systems Manager Run Command, and ECS tasks.  
대상이 리소스 기반 정책을 지원하지 않으면 EventBridge는 IAM 역할을 사용하여 대상 서비스를 호출합니다. 예시로는 Kinesis Stream, EC2 Auto Scaling, Systems Manager Run Command, ECS 작업이 있습니다.  
(지원되지 않는 경우 IAM 역할 활용)  

---

## Special Note on Kinesis Data Streams  
## Kinesis Data Streams에 대한 특별 주의사항  

Although Kinesis Data Streams supports resource-based policies, EventBridge currently uses an IAM role to invoke it. To determine which method EventBridge uses for a specific target, you need to check the configuration of the EventBridge role itself.  
Kinesis Data Streams는 리소스 기반 정책을 지원하지만, EventBridge는 현재 IAM 역할을 사용하여 호출합니다. 특정 대상에 EventBridge가 어떤 방식을 사용하는지 확인하려면 EventBridge 역할 설정을 확인해야 합니다.  
(Kinesis 특수 처리)  

---

## Summary of EventBridge Target Invocation Methods  
## EventBridge 대상 호출 방법 요약  

- Lambda, SNS, SQS, and S3 buckets use resource-based policies.  
- Lambda, SNS, SQS, S3 버킷은 리소스 기반 정책을 사용합니다.  

- Kinesis Data Streams, EC2 Auto Scaling, and similar services use IAM roles.  
- Kinesis Data Streams, EC2 Auto Scaling 등 유사 서비스는 IAM 역할을 사용합니다.  

- Even though resource-based policies are possible with Kinesis Data Streams, EventBridge does not currently support this method for that service.  
- Kinesis Data Streams는 리소스 기반 정책이 가능하지만, EventBridge는 현재 해당 방법을 지원하지 않습니다.  

This information is essential for understanding permissions management in cross-account scenarios and is relevant for certification exams.  
이 정보는 크로스 계정 시나리오에서 권한 관리를 이해하는 데 필수적이며, 인증 시험에도 관련이 있습니다.  

---

## Conclusion  
## 결론  

This lecture covered the fundamental differences between IAM roles and resource-based policies, their practical applications, and how services like EventBridge utilize them. Understanding these concepts is crucial for managing cross-account access and permissions effectively in AWS.  
이번 강의에서는 IAM 역할과 리소스 기반 정책의 근본적인 차이, 실제 적용 사례, EventBridge와 같은 서비스에서의 활용 방법을 다뤘습니다. 이러한 개념을 이해하는 것은 AWS에서 크로스 계정 접근과 권한을 효과적으로 관리하는 데 매우 중요합니다.  

---

## Key Takeaways  
## 핵심 요약  

- IAM roles require the principal to assume the role, giving up their original permissions and adopting the role's permissions.  
- IAM 역할은 주체가 역할을 맡아야 하며, 원래 권한을 포기하고 역할 권한을 가져옵니다.  

- Resource-based policies allow principals to access resources without assuming a role, retaining their original permissions.  
- 리소스 기반 정책은 주체가 역할을 맡지 않고도 리소스에 접근할 수 있으며, 원래 권한을 유지합니다.  

- Resource-based policies are supported by many AWS services such as S3 buckets, SNS topics, SQS queues, and Lambda functions.  
- 리소스 기반 정책은 S3 버킷, SNS 주제, SQS 큐, Lambda 함수 등 많은 AWS 서비스에서 지원됩니다.  

- EventBridge uses resource-based policies for targets that support them and IAM roles for others, with specific behavior depending on the target service.  
- EventBridge는 지원되는 대상에 대해 리소스 기반 정책을 사용하고, 그렇지 않은 대상에는 IAM 역할을 사용하며, 대상 서비스에 따라 동작이 다릅니다.  
```

게임보상: 🛡️ 크로스 계정 권한 전문가! IAM 역할과 리소스 정책 완전 정복! 🏆✅
