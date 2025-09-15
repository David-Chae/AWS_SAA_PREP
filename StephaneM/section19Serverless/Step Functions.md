# Step Functions
# 스텝 함수

## Introduction to AWS Step Functions
## AWS Step Functions 소개
> AWS Step Functions는 서버리스 시각적 워크플로우를 구성할 수 있게 해주는 서비스입니다. 주로 Lambda 함수의 오케스트레이션에 사용됩니다.

AWS Step Functions provide a way to build serverless visual workflows that perform orchestration, typically of your Lambda functions.
AWS Step Functions는 Lambda 함수 등 서버리스 리소스의 오케스트레이션을 수행하는 시각적 워크플로우를 구성할 수 있는 방법을 제공합니다.
> 핵심: 서버리스 워크플로우 시각화 + 오케스트레이션 기능

You design a graph where, at each step, you define what happens next in case of success or failure.
각 단계에서 성공 또는 실패 시 다음 동작을 정의하는 그래프를 설계합니다.
> 핵심: 상태 전환 기반 워크플로우 설계

This approach allows you to create complex workflows within AWS, enabling sophisticated orchestration capabilities.
이를 통해 AWS 내에서 복잡한 워크플로우를 만들고 정교한 오케스트레이션을 구현할 수 있습니다.
> 핵심: 복잡한 서버리스 작업 자동화 가능

## Features of Step Functions
## Step Functions 주요 기능
> Step Functions의 내부 기능 이해

Step Functions include internal features such as sequencing, parallel functions, conditions, timeouts, and error handling.
Step Functions는 순차 실행, 병렬 함수, 조건문, 타임아웃, 오류 처리 등의 기능을 제공합니다.
> 핵심: 워크플로우 관리의 핵심 기능

These features facilitate robust workflow management.
이 기능들은 안정적인 워크플로우 관리를 돕습니다.
> 핵심: 신뢰성 있는 워크플로우 구현

## Integration with AWS Services
## AWS 서비스 통합
> 다양한 AWS 서비스와 연결 가능

Step Functions do not only orchestrate Lambda functions; they also integrate with EC2 instances, ECS tasks, on-premises servers, API Gateway, SQS queues, DynamoDB, and many other AWS services.
Step Functions는 Lambda 함수뿐만 아니라 EC2, ECS, 온프레미스 서버, API Gateway, SQS 큐, DynamoDB 등 다양한 AWS 서비스와 통합됩니다.
> 핵심: Lambda 외 다양한 서비스 오케스트레이션 가능

## Human Approval in Workflows
## 워크플로우에서 사람 승인 기능
> 인간의 승인 단계 포함 가능

Within a Step Function workflow, it is possible to implement a human approval feature.
Step Function 워크플로우 내에서 사람 승인 기능을 구현할 수 있습니다.
> 핵심: 자동화 중에도 의사결정 통합 가능

For example, a workflow can pause at a certain point for a human to review the results.
예를 들어, 특정 단계에서 워크플로우가 일시 중지되어 사람이 결과를 검토하도록 할 수 있습니다.
> 핵심: 중간 점검 단계 설정 가능

If the human approves by saying "Yes," the workflow continues; if "No," it fails.
승인이 "Yes"이면 워크플로우 계속 진행, "No"이면 실패 처리.
> 핵심: 조건부 진행 제어

This capability enhances control and decision-making within automated workflows.
이 기능은 자동화된 워크플로우에서 제어력과 의사결정 능력을 향상시킵니다.
> 핵심: 자동화 + 수동 의사결정 결합

## Use Cases of Step Functions
## Step Functions 활용 사례
> 실무 활용 예시

Use cases for Step Functions are manifold, including order fulfillment, data processing, web applications, or any complex workflow that benefits from a visual graph representation for clarity and management.
Step Functions 활용 사례: 주문 처리, 데이터 처리, 웹 애플리케이션 등 복잡한 워크플로우 시각화가 유용한 모든 경우.
> 핵심: 복잡한 작업 시각화 + 관리 용이

This concludes the introduction to AWS Step Functions.
AWS Step Functions 소개를 마칩니다.
> 핵심: 기본 개념 이해 완료

The next lecture will continue exploring this topic.
다음 강의에서 Step Functions를 더 심화해서 탐구합니다.
> 핵심: 심화 학습 예고

## Key Takeaways
## 핵심 요약
- AWS Step Functions enable building serverless visual workflows for orchestration.
- AWS Step Functions는 서버리스 시각적 워크플로우를 구축해 오케스트레이션 가능
- They support sequencing, parallel execution, conditions, timeouts, and error handling.
- 순차 실행, 병렬 실행, 조건, 타임아웃, 오류 처리 기능 지원
- Step Functions integrate with many AWS services beyond Lambda, including EC2, ECS, API Gateway, and SQS.
- Lambda 외에도 EC2, ECS, API Gateway, SQS 등 다양한 AWS 서비스와 통합
- Human approval steps can be incorporated within workflows for decision-making.
- 인간 승인 단계를 워크플로우에 포함시켜 의사결정 가능

```

🎮 **게임 보상 포인트:**

* Step Functions 개념 학습 = 10 XP
* 주요 기능 이해 (병렬, 조건, 타임아웃, 오류 처리) = 10 XP
* AWS 서비스 통합 개념 = 10 XP
* 인간 승인 기능 이해 = 10 XP
  총: **40 XP**
