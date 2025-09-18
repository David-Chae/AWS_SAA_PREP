```markdown
# Amazon GuardDuty  
# 아마존 가드듀티  

🎮 게임보상: "Threat Detection Specialist" +500 XP  

---

## Introduction to Amazon GuardDuty  
## 아마존 가드듀티 소개  

Amazon GuardDuty helps you perform intelligent threat discovery to protect your AWS accounts.  
Amazon GuardDuty는 AWS 계정을 보호하기 위해 지능적인 위협 탐지를 수행하는 데 도움을 줍니다.  

It achieves this by employing machine learning algorithms, performing anomaly detection, and utilizing third-party data to identify threats.  
머신러닝 알고리즘을 사용하고, 이상 탐지를 수행하며, 타사 데이터를 활용하여 위협을 식별함으로써 이를 달성합니다.  

Enabling GuardDuty is straightforward with just one click, followed by a 30-day trial period.  
GuardDuty 활성화는 한 번의 클릭으로 간단히 이루어지며, 이후 30일 무료 체험이 제공됩니다.  

There is no need to install any software to start using it.  
사용을 시작하기 위해 별도의 소프트웨어 설치가 필요하지 않습니다.  

---

## Input Data Sources Analyzed by GuardDuty  
## GuardDuty가 분석하는 입력 데이터 소스  

GuardDuty examines various input data sources to detect suspicious activities:  
GuardDuty는 의심스러운 활동을 탐지하기 위해 다양한 입력 데이터 소스를 분석합니다.  

- **CloudTrail Event Logs**: It monitors for unusual API calls or unauthorized deployments.  
- **CloudTrail 이벤트 로그**: 비정상적인 API 호출이나 승인되지 않은 배포를 모니터링합니다.  

  This includes both management events, such as creating a VPC subnet, and data events, such as S3 operations like GetObject, ListObjects, and DeleteObjects.  
  여기에는 VPC 서브넷 생성과 같은 관리 이벤트와, S3의 GetObject, ListObjects, DeleteObjects 같은 데이터 이벤트가 포함됩니다.  

- **VPC Flow Logs**: It analyzes unusual internet traffic and identifies suspicious IP addresses.  
- **VPC 플로우 로그**: 비정상적인 인터넷 트래픽을 분석하고 의심스러운 IP 주소를 식별합니다.  

- **DNS Logs**: It detects EC2 instances sending encoded data within DNS queries, which may indicate compromise.  
- **DNS 로그**: DNS 쿼리 내에서 인코딩된 데이터를 전송하는 EC2 인스턴스를 탐지하며, 이는 침해를 나타낼 수 있습니다.  

Additionally, there are optional features to analyze other data sources such as EKS audit logs, RDS and Aurora login events, EBS volumes, Lambda network activity, and S3 data events.  
추가적으로 EKS 감사 로그, RDS 및 Aurora 로그인 이벤트, EBS 볼륨, Lambda 네트워크 활동, S3 데이터 이벤트 등 다른 데이터 소스를 분석하는 선택적 기능도 있습니다.  

---

## Integration with Amazon EventBridge  
## 아마존 이벤트브릿지와 통합  

GuardDuty findings generate events in Amazon EventBridge.  
GuardDuty 탐지 결과는 Amazon EventBridge에서 이벤트를 생성합니다.  

You can configure EventBridge rules to automatically notify you when findings occur.  
EventBridge 규칙을 설정하여 탐지가 발생할 때 자동으로 알림을 받을 수 있습니다.  

These rules can target various AWS services, including AWS Lambda functions and SNS topics, enabling automated responses or notifications.  
이 규칙은 AWS Lambda 함수와 SNS 주제 등 다양한 AWS 서비스 대상으로 설정할 수 있어, 자동 응답이나 알림이 가능하게 합니다.  

---

## GuardDuty and Cryptocurrency Attack Protection  
## GuardDuty와 암호화폐 공격 보호  

GuardDuty includes dedicated findings to protect against cryptocurrency attacks.  
GuardDuty는 암호화폐 공격으로부터 보호하기 위한 전용 탐지를 포함합니다.  

It analyzes all input data sources to detect such attacks effectively, providing enhanced security for your AWS environment.  
모든 입력 데이터 소스를 분석하여 이러한 공격을 효과적으로 탐지하며, AWS 환경의 보안을 강화합니다.  

---

## Summary of GuardDuty Features  
## GuardDuty 기능 요약  

- **Mandatory Input Data**: VPC flow logs, CloudTrail logs, and DNS logs are always analyzed by GuardDuty.  
- **필수 입력 데이터**: VPC 플로우 로그, CloudTrail 로그, DNS 로그는 항상 GuardDuty에서 분석됩니다.  

- **Optional Input Data**: You can enable additional features to analyze S3 logs, EBS volumes, Lambda network activity, RDS and Aurora login activity, EKS logs, and runtime monitoring.  
- **선택적 입력 데이터**: 추가 기능을 활성화하면 S3 로그, EBS 볼륨, Lambda 네트워크 활동, RDS 및 Aurora 로그인 활동, EKS 로그, 런타임 모니터링을 분석할 수 있습니다.  

- **Findings and Automation**: When GuardDuty detects findings, it creates events in Amazon EventBridge.  
- **탐지 및 자동화**: GuardDuty가 탐지를 수행하면 Amazon EventBridge에서 이벤트를 생성합니다.  

  These events can trigger automated workflows, such as Lambda functions or SNS notifications, through EventBridge rules.  
  이 이벤트들은 EventBridge 규칙을 통해 Lambda 함수나 SNS 알림과 같은 자동화된 워크플로를 트리거할 수 있습니다.  

GuardDuty continues to evolve, with more features likely to be added over time.  
GuardDuty는 계속 발전 중이며, 시간이 지나면서 더 많은 기능이 추가될 가능성이 있습니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on Amazon GuardDuty.  
이로써 Amazon GuardDuty 강의를 마칩니다.  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon GuardDuty provides intelligent threat discovery to protect AWS accounts using machine learning, anomaly detection, and third-party data.  
- Amazon GuardDuty는 머신러닝, 이상 탐지, 타사 데이터를 활용하여 AWS 계정을 보호하는 지능적 위협 탐지를 제공합니다.  

- It analyzes multiple input data sources including CloudTrail event logs, VPC flow logs, DNS logs, and optional sources like EKS audit logs, RDS/Aurora login events, EBS, Lambda, and S3 data events.  
- CloudTrail 이벤트 로그, VPC 플로우 로그, DNS 로그와 EKS 감사 로그, RDS/Aurora 로그인 이벤트, EBS, Lambda, S3 데이터 이벤트 등 선택적 데이터 소스를 분석합니다.  

- GuardDuty findings can trigger automated responses through Amazon EventBridge rules targeting AWS Lambda functions or SNS topics.  
- GuardDuty 탐지 결과는 AWS Lambda 함수나 SNS 주제를 대상으로 하는 EventBridge 규칙을 통해 자동 응답을 트리거할 수 있습니다.  

- It includes dedicated detection for cryptocurrency attacks, enhancing security against such threats.  
- 암호화폐 공격 전용 탐지를 포함하여, 이러한 위협에 대한 보안을 강화합니다.  
```

🎮 게임보상 완료: "AWS Security Analyst" +1000 XP 🏆
