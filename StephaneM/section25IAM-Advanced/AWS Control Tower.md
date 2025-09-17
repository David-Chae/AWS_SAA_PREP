```markdown
# AWS Control Tower  
# AWS 컨트롤 타워  

## Introduction to AWS Control Tower  
## AWS 컨트롤 타워 소개  

AWS Control Tower is a service designed to simplify the setup and governance of secure and compliant multi-account AWS environments based on best practices.  
AWS 컨트롤 타워는 보안과 규정을 준수하는 다계정 AWS 환경을 모범 사례 기반으로 쉽게 설정하고 관리할 수 있도록 설계된 서비스입니다.  
(다계정 환경 설정과 거버넌스 단순화 강조)  

To create these accounts, Control Tower leverages the AWS Organizations service. Accounts are automatically created, and we will explore how to ensure they remain secure and compliant.  
이 계정들을 생성하기 위해 컨트롤 타워는 AWS Organizations 서비스를 활용합니다. 계정은 자동으로 생성되며, 이를 안전하고 규정을 준수하도록 유지하는 방법을 살펴봅니다.  
(AWS Organizations와 연계된 계정 생성)  

## Benefits of Using AWS Control Tower  
## AWS 컨트롤 타워 사용의 장점  

- Automates environment setup with just a few clicks.  
- 몇 번의 클릭만으로 환경 설정을 자동화합니다.  
(설정 자동화)  

- Allows pre-configuration of all desired settings.  
- 원하는 모든 설정을 사전 구성할 수 있습니다.  
(사전 설정 가능)  

- Enables ongoing policy management through guardrails.  
- 가드레일을 통해 지속적인 정책 관리를 가능하게 합니다.  
(정책 관리)  

- Detects policy violations and can remediate them automatically.  
- 정책 위반을 감지하고 자동으로 수정할 수 있습니다.  
(자동 위반 감지 및 대응)  

- Provides an interactive dashboard to monitor compliance across all accounts.  
- 모든 계정의 규정 준수 상태를 모니터링할 수 있는 대시보드를 제공합니다.  
(모니터링 대시보드)  

Control Tower functions as an additional layer on top of AWS Organizations, enhancing multi-account management capabilities.  
컨트롤 타워는 AWS Organizations 위에 추가 계층으로 작동하며, 다계정 관리 기능을 강화합니다.  
(Organizations 위 기능 강화)  

## Understanding Guardrails  
## 가드레일 이해  

When managing multiple AWS accounts, you may want to enforce restrictions or monitor compliance uniformly across all accounts. Guardrails provide ongoing governance within your Control Tower environment to achieve this.  
다계정 AWS를 관리할 때, 모든 계정에서 일관되게 제한을 적용하거나 규정 준수를 모니터링하고 싶을 수 있습니다. 가드레일은 컨트롤 타워 환경 내에서 지속적인 거버넌스를 제공합니다.  
(가드레일 목적 설명)  

There are two types of guardrails:  
가드레일에는 두 가지 유형이 있습니다:  

### Preventive Guardrails  
### 예방 가드레일  

These guardrails prevent accounts from performing certain actions and are restrictive in nature. They are implemented using Service Control Policies (SCPs) from AWS Organizations and applied across all accounts.  
이 가드레일은 계정이 특정 작업을 수행하지 못하도록 제한하며, 본질적으로 제약적입니다. AWS Organizations의 서비스 제어 정책(SCP)을 사용하여 구현되고 모든 계정에 적용됩니다.  
(SCP 기반 제한)  

For example, a preventive guardrail can restrict the AWS regions where accounts are allowed to operate, such as limiting usage to only the us-east-1 and eu-west-2 regions.  
예를 들어, 예방 가드레일은 계정이 운영할 수 있는 AWS 리전을 제한할 수 있으며, 예를 들어 us-east-1과 eu-west-2 리전만 허용하도록 설정할 수 있습니다.  
(리전 제한 사례)  

Behind the scenes, Control Tower instructs AWS Organizations to enforce these SCPs.  
백그라운드에서 컨트롤 타워는 AWS Organizations에 이러한 SCP를 적용하도록 지시합니다.  
(자동 적용)  

### Detective Guardrails  
### 탐지 가드레일  

Detective guardrails focus on detecting non-compliance rather than preventing actions. They utilize the AWS Config service to monitor resources and configurations.  
탐지 가드레일은 작업을 제한하기보다는 규정 위반을 감지하는 데 중점을 둡니다. AWS Config 서비스를 사용하여 리소스와 구성 상태를 모니터링합니다.  
(규정 준수 감지)  

For instance, a detective guardrail can identify untagged resources within accounts. Control Tower sets up AWS Config on all member accounts, which continuously evaluates compliance against defined rules.  
예를 들어, 탐지 가드레일은 태그가 없는 리소스를 식별할 수 있습니다. 컨트롤 타워는 모든 계정에 AWS Config를 설정하여 정의된 규칙에 대해 지속적으로 규정 준수를 평가합니다.  
(태그 미등록 리소스 감지)  

If non-compliance is detected, such as untagged resources, AWS Config triggers an SNS topic notification. Administrators can receive alerts, or the SNS topic can invoke a Lambda function to automatically remediate the issue, for example, by adding the required tags to resources.  
태그가 없는 리소스와 같은 규정 위반이 감지되면 AWS Config가 SNS 주제 알림을 트리거합니다. 관리자는 경고를 받을 수 있으며, SNS 주제가 Lambda 함수를 호출하여 자동으로 문제를 수정할 수도 있습니다.  
(자동 수정 예시)  

## Summary  
## 요약  

AWS Control Tower facilitates the creation of new AWS accounts and enforces governance through preventive and detective guardrails. These mechanisms help maintain the security and compliance of your AWS environments efficiently.  
AWS 컨트롤 타워는 새로운 AWS 계정 생성을 지원하고, 예방 및 탐지 가드레일을 통해 거버넌스를 시행합니다. 이러한 메커니즘은 AWS 환경의 보안과 규정 준수를 효율적으로 유지하는 데 도움을 줍니다.  
(효율적 거버넌스 강조)  

Thank you for reviewing this lecture on AWS Control Tower. We will continue exploring related topics in the next session.  
AWS 컨트롤 타워 강의를 검토해주셔서 감사합니다. 다음 세션에서 관련 주제를 계속 탐구하겠습니다.  
(강의 종료)  

## Key Takeaways  
## 핵심 요약  

- AWS Control Tower simplifies the setup and governance of secure, compliant multi-account AWS environments.  
- AWS 컨트롤 타워는 보안과 규정을 준수하는 다계정 AWS 환경의 설정과 거버넌스를 단순화합니다.  

- It automates account creation using AWS Organizations and applies configurations through guardrails.  
- AWS Organizations를 사용해 계정 생성을 자동화하고, 가드레일을 통해 설정을 적용합니다.  

- Preventive guardrails use Service Control Policies (SCPs) to restrict actions across accounts.  
- 예방 가드레일은 서비스 제어 정책(SCP)을 사용해 계정 전반의 작업을 제한합니다.  

- Detective guardrails utilize AWS Config to monitor compliance and can trigger automated remediation via SNS and Lambda.  
- 탐지 가드레일은 AWS Config를 사용해 규정 준수를 모니터링하며, SNS와 Lambda를 통해 자동 수정 트리거가 가능합니다.  
```

게임보상: 🏰 AWS Control Tower 지배자! 예방 & 탐지 가드레일 마스터! 🚀🎮
