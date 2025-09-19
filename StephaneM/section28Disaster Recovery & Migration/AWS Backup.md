```markdown
# AWS Backup  
# AWS 백업  

🎮 게임보상: "Backup Master" +500 XP  

---

## Introduction to AWS Backup  
## AWS 백업 소개  

AWS Backup is a fully managed service that allows you to centrally manage and automate backups across all your AWS services.  
AWS Backup는 모든 AWS 서비스에 걸쳐 백업을 중앙에서 관리하고 자동화할 수 있는 완전 관리형 서비스입니다.  

The list of supported services is continuously expanding.  
지원되는 서비스 목록은 지속적으로 확장되고 있습니다.  

The main idea is to provide a central place to manage backups without the need to create custom scripts or perform manual processes.  
핵심 아이디어는 사용자 정의 스크립트 작성이나 수동 작업 없이 백업을 관리할 수 있는 중앙 장소를 제공하는 것입니다.  

This central view helps you maintain a consistent backup strategy.  
이 중앙 뷰는 일관된 백업 전략을 유지하는 데 도움이 됩니다.  

---

## Supported Services  
## 지원 서비스  

AWS Backup supports a wide range of services, including:  
AWS Backup는 다음을 포함한 다양한 서비스를 지원합니다.  

- Amazon EC2  
- Amazon EBS  
- Amazon S3  
- Amazon RDS and all supported database engines  
- Aurora  
- DynamoDB  
- DocumentDB  
- Amazon Neptune  
- Amazon EFS  
- Amazon FSx, including Lustre and Windows File Server  
- AWS Storage Gateway, such as the Volume Gateway  

This list may grow over time, but the core concepts of database backup and the most important services are covered here.  
이 목록은 시간이 지나면서 늘어날 수 있지만, 데이터베이스 백업의 핵심 개념과 가장 중요한 서비스는 여기서 다룹니다.  

---

## Backup Features  
## 백업 기능  

AWS Backup supports several important features:  
AWS Backup는 여러 중요한 기능을 지원합니다.  

- Cross-region backups: You can push your backups to another AWS region for disaster recovery strategies, all managed in one place.  
- 지역 간 백업: 백업을 다른 AWS 리전으로 전송하여 재해 복구 전략을 적용할 수 있으며, 모두 한 곳에서 관리됩니다.  

- Cross-account backups: If you use multiple AWS accounts, backups can be managed across them.  
- 계정 간 백업: 여러 AWS 계정을 사용하는 경우, 백업을 계정 간 관리할 수 있습니다.  

- Point-in-time recovery: Supported for services like Aurora.  
- 시점 복구: Aurora와 같은 서비스에서 지원됩니다.  

- On-demand and scheduled backups: You can create backups manually or according to a schedule.  
- 수동 및 예약 백업: 백업을 수동으로 생성하거나 예약에 따라 자동 생성할 수 있습니다.  

- Tag-based backup policies: Allows you to back up only resources with specific tags, such as "production".  
- 태그 기반 백업 정책: "production"과 같은 특정 태그가 있는 리소스만 백업하도록 설정할 수 있습니다.  

You can create backup policies known as Backup Plans, where you define:  
Backup Plans라 불리는 백업 정책을 만들어 다음을 정의할 수 있습니다.  

- The backup frequency (e.g., every 12 hours, weekly, monthly, or using cron expressions)  
- 백업 빈도 (예: 12시간마다, 주간, 월간 또는 cron 표현식 사용)  

- The backup window  
- 백업 수행 시간(백업 윈도우)  

- Transition of backups to cold storage after a specified time (days, weeks, months, or years)  
- 지정된 시간(일, 주, 월, 년) 후 백업을 콜드 스토리지로 전환  

- The retention period for backups (days, weeks, months, or years)  
- 백업 보존 기간(일, 주, 월, 년)  

---

## Using AWS Backup  
## AWS 백업 사용법  

To use AWS Backup, you create a backup plan and assign specific AWS resources that are important to you.  
AWS Backup를 사용하려면 백업 계획을 생성하고 중요한 AWS 리소스를 할당합니다.  

Once configured, your data is automatically backed up to Amazon S3 in an internal bucket specific to AWS Backup.  
설정이 완료되면 데이터가 AWS Backup 전용 내부 버킷에 자동으로 Amazon S3로 백업됩니다.  

This process simplifies backup management and ensures your data is securely stored.  
이 과정은 백업 관리를 단순화하고 데이터가 안전하게 저장되도록 보장합니다.  

---

## Vault Lock Feature  
## 볼트 락 기능  

AWS Backup includes a feature called Vault Lock, which enforces a WORM (Write Once Read Many) policy.  
AWS Backup에는 Vault Lock이라는 기능이 있으며, WORM(Write Once Read Many) 정책을 적용합니다.  

This means that all backups stored in your Backup Vault cannot be deleted.  
즉, Backup Vault에 저장된 모든 백업은 삭제할 수 없습니다.  

This policy provides an additional layer of defense against inadvertent or malicious delete operations or updates that could shorten or alter the retention period.  
이 정책은 실수나 악의적인 삭제 또는 보존 기간을 단축하거나 변경할 수 있는 업데이트로부터 추가적인 방어층을 제공합니다.  

Even the root user cannot delete backups when Vault Lock is enabled, offering strong guarantees on the safety of your backups.  
Vault Lock이 활성화되면 루트 사용자조차 백업을 삭제할 수 없어, 백업 안전성에 대한 강력한 보장을 제공합니다.  

---

## Conclusion  
## 결론  

That covers the essential information about the AWS Backup service.  
AWS Backup 서비스의 핵심 정보를 다루었습니다.  

It is a comprehensive and supportive addition to AWS services, providing centralized, automated, and secure backup management.  
AWS 서비스에 포괄적이고 보조적인 기능을 제공하며, 중앙 집중식, 자동화, 안전한 백업 관리를 제공합니다.  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
관심 가져주셔서 감사하며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Backup is a fully managed service that centralizes and automates backups across numerous AWS services.  
- AWS Backup는 여러 AWS 서비스에 걸친 백업을 중앙에서 관리하고 자동화하는 완전 관리형 서비스입니다.  

- It supports a wide range of services including EC2, EBS, S3, RDS, Aurora, DynamoDB, DocumentDB, Neptune, EFS, FSx, Windows File Server, and Storage Gateway.  
- EC2, EBS, S3, RDS, Aurora, DynamoDB, DocumentDB, Neptune, EFS, FSx, Windows File Server, Storage Gateway 등 다양한 서비스를 지원합니다.  

- Features include cross-region and cross-account backups, point-in-time recovery, on-demand and scheduled backups, and tag-based backup policies.  
- 기능에는 지역 간/계정 간 백업, 시점 복구, 수동 및 예약 백업, 태그 기반 백업 정책이 포함됩니다.  

- The Vault Lock feature enforces a WORM (Write Once Read Many) policy, preventing deletion or alteration of backups, even by the root user, enhancing backup security.  
- Vault Lock 기능은 WORM 정책을 적용하여 루트 사용자조차 백업 삭제나 변경을 방지하며, 백업 보안을 강화합니다.  
```
