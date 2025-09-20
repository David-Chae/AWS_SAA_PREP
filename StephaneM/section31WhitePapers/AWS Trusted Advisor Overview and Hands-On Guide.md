```markdown
# AWS Trusted Advisor Overview and Hands-On Guide  
# AWS Trusted Advisor 개요 및 실습 가이드  
🎮 **보상: "Trusted Advisor 탐험가" 뱃지 획득!**  

---

## Introduction to AWS Trusted Advisor  
## AWS Trusted Advisor 소개  
AWS Trusted Advisor is a service that provides a high-level assessment of your AWS account.  
AWS Trusted Advisor는 AWS 계정을 고수준에서 평가해 주는 서비스입니다.  

It does not require any installation and offers recommendations based on various checks performed on your account.  
설치가 필요 없으며, 계정에 대한 다양한 검사를 기반으로 권장 사항을 제공합니다.  

---

## Types of Checks  
## 검사 유형  
Trusted Advisor performs checks such as:  
Trusted Advisor는 다음과 같은 검사를 수행합니다:  

- Whether you have EBS Public Snapshots.  
- EBS 공개 스냅샷이 있는지 여부  
- Whether you have RDS Public Snapshots.  
- RDS 공개 스냅샷이 있는지 여부  
- Whether root accounts are being used for your AWS accounts.  
- 루트 계정을 AWS 계정에 사용 중인지 여부  

These checks help identify potential security and operational issues.  
이 검사는 잠재적인 보안 및 운영 문제를 식별하는 데 도움을 줍니다.  

---

## Categories of Checks  
## 검사 카테고리  
The checks are grouped into six categories:  
검사는 6가지 카테고리로 분류됩니다:  

- Cost Optimization  
- 비용 최적화  
- Performance  
- 성능  
- Security  
- 보안  
- Fault Tolerance  
- 내결함성  
- Service Limits  
- 서비스 한도  
- Operational Excellence  
- 운영 우수성  

---

## Access Levels  
## 접근 레벨  
There are three sets of checks:  
검사에는 세 가지 세트가 있습니다:  

- Core set of checks  
- 핵심 검사 세트  
- Full set of checks  
- 전체 검사 세트  

To access the full set of checks, you must have a Business or Enterprise support plan.  
전체 검사 세트에 접근하려면 Business 또는 Enterprise 지원 플랜이 필요합니다.  

Additionally, with these plans, you gain programmatic access to Trusted Advisor through the AWS Support API.  
이 플랜을 사용하면 AWS Support API를 통해 Trusted Advisor에 프로그램 방식으로 접근할 수 있습니다.  

---

## Using AWS Trusted Advisor  
## AWS Trusted Advisor 사용  
Upon accessing Trusted Advisor, you will see recommendations for your account.  
Trusted Advisor에 접근하면 계정에 대한 권장 사항을 확인할 수 있습니다.  

For example, it may indicate zero recommended actions but suggest investigations that require your attention.  
예를 들어, 권장 작업이 0개일 수 있지만, 주의를 기울여야 하는 검토 사항을 제시할 수 있습니다.  

In one case, a bucket was found to allow global access, which requires verification to ensure it is intentional.  
한 사례에서는 버킷이 전 세계 접근을 허용하고 있어, 의도된 설정인지 확인이 필요했습니다.  

Additionally, security group rules may allow unrestricted access to specific ports, which should be reviewed carefully.  
또한, 보안 그룹 규칙이 특정 포트에 대해 무제한 접근을 허용할 수 있으므로 주의 깊게 검토해야 합니다.  

---

## Support Plan Limitations  
## 지원 플랜 제한 사항  
If you do not have the appropriate support plan, many Trusted Advisor checks will be unavailable.  
적절한 지원 플랜이 없으면 많은 Trusted Advisor 검사를 사용할 수 없습니다.  

For instance, categories such as Cost Optimization, Performance, Fault Tolerance, and Operational Excellence will not display any checks without upgrading your support plan.  
예를 들어, 비용 최적화, 성능, 내결함성, 운영 우수성 카테고리는 플랜 업그레이드 없이는 검사가 표시되지 않습니다.  

Only basic security checks are accessible without the Business or Enterprise support plan.  
Business 또는 Enterprise 플랜이 없으면 기본 보안 검사만 접근 가능합니다.  

---

## Security Checks Available Without Full Support  
## 전체 지원 없이 접근 가능한 보안 검사  
The accessible security checks include:  
접근 가능한 보안 검사는 다음과 같습니다:  

- Bucket Permissions  
- 버킷 권한  
- Security Group Ports  
- 보안 그룹 포트  
- EBS Public Snapshots  
- EBS 공개 스냅샷  
- RDS Public Snapshots  
- RDS 공개 스냅샷  

More advanced security checks require an upgraded support plan.  
더 고급 보안 검사는 지원 플랜 업그레이드가 필요합니다.  

---

## Service Limits Monitoring  
## 서비스 한도 모니터링  
Trusted Advisor also allows you to monitor service limits directly.  
Trusted Advisor는 서비스 한도를 직접 모니터링할 수도 있습니다.  

You can review limits for:  
다음 서비스 한도를 검토할 수 있습니다:  

- Auto Scaling Groups  
- 오토스케일링 그룹  
- CloudFormation Stacks  
- CloudFormation 스택  
- DynamoDB Read and Write Capacity  
- DynamoDB 읽기 및 쓰기 용량  

This helps ensure you do not exceed your AWS service quotas.  
이를 통해 AWS 서비스 할당량을 초과하지 않도록 보장할 수 있습니다.  

---

## Summary  
## 요약  
While Trusted Advisor offers limited functionality without a paid support plan, it provides valuable insights into your AWS account's security and operational status.  
유료 지원 플랜이 없으면 기능이 제한적이지만, Trusted Advisor는 AWS 계정의 보안 및 운영 상태에 대한 중요한 인사이트를 제공합니다.  

Upgrading your support plan unlocks comprehensive checks and programmatic access, enhancing your ability to optimize and secure your AWS environment.  
지원 플랜을 업그레이드하면 포괄적인 검사와 프로그램 접근이 가능해져 AWS 환경 최적화 및 보안 강화 능력이 향상됩니다.  

This knowledge is essential for understanding how Trusted Advisor fits into AWS account management and is useful for exam preparation.  
이 지식은 Trusted Advisor가 AWS 계정 관리에서 어떤 역할을 하는지 이해하고 시험 준비에 유용합니다.  

---

## Key Takeaways  
## 핵심 요약  
- AWS Trusted Advisor provides a high-level assessment of your AWS account without requiring installation.  
- AWS Trusted Advisor는 설치 없이 AWS 계정을 고수준에서 평가합니다.  

- It performs checks grouped into six categories: cost optimization, performance, security, fault tolerance, service limits, and operational excellence.  
- 검사는 6가지 카테고리로 그룹화되어 수행됩니다: 비용 최적화, 성능, 보안, 내결함성, 서비스 한도, 운영 우수성.  

- Access to the full set of Trusted Advisor checks requires a Business or Enterprise support plan.  
- 전체 Trusted Advisor 검사에 접근하려면 Business 또는 Enterprise 지원 플랜이 필요합니다.  

- Programmatic access to Trusted Advisor is available through the AWS Support API with the appropriate support plan.  
- 적절한 지원 플랜이 있으면 AWS Support API를 통해 Trusted Advisor에 프로그램 방식으로 접근할 수 있습니다.  

🎮 **보상: "Trusted Advisor 전문가" 뱃지 획득!**
```
