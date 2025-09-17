# Summary of Amazon RDS
# Amazon RDS 요약
# → Amazon RDS의 핵심 개념을 정리하는 섹션입니다.

## Summary of Amazon RDS
## Amazon RDS 요약
## → 반복된 제목. RDS 전체 요약에 집중합니다.

This section provides a summary of the key concepts learned about Amazon RDS.  
이 섹션은 Amazon RDS에 대해 배운 핵심 개념을 요약합니다.  
→ 시험 대비 및 복습용 핵심 포인트.

For detailed explanations, it is recommended to revisit the previous lectures.  
자세한 설명은 이전 강의를 다시 보는 것이 좋습니다.  
→ 요약은 개괄적이며 세부는 강의 참고.

This summary highlights the essential points you should know about Amazon RDS.  
이 요약은 Amazon RDS에서 반드시 알아야 할 핵심 포인트를 강조합니다.  
→ 시험이나 실무에서 꼭 필요한 지식 정리.

```
🎖️ **게임 보상: DB 전략가 → RDS 초보자 레벨업!**
```

Amazon RDS is a managed service supporting several database engines including PostgreSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, and a custom version of RDS.  
Amazon RDS는 PostgreSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, 그리고 맞춤형 RDS 버전을 지원하는 관리형 서비스입니다.  
→ 다양한 DB 엔진을 통합적으로 지원.

When using Amazon RDS, you need to provision an RDS instance size as well as an EBS volume type and size.  
Amazon RDS를 사용할 때는 인스턴스 크기와 EBS 볼륨 종류 및 크기를 프로비저닝해야 합니다.  
→ 기본 리소스 설정 필요.

Although provisioning is required, there is auto-scaling capability available for the storage layer.  
프로비저닝이 필요하지만, 스토리지 계층은 자동 확장이 가능합니다.  
→ 스토리지 관리 부담 완화.

Amazon RDS supports read replicas to scale read capabilities.  
Amazon RDS는 읽기 성능 확장을 위해 읽기 복제본을 지원합니다.  
→ 트래픽 분산에 유리.

If applications need to run analytics against a production database, it is preferable to create a read replica to offload those queries.  
프로덕션 DB에서 분석을 수행해야 한다면 읽기 복제본을 만들어 쿼리 부하를 분산하는 것이 좋습니다.  
→ 운영 DB 안정성 보장.

For high availability, you can use Multi-AZ deployments to have a standby database.  
고가용성을 위해 Multi-AZ 배포를 사용하면 대기 DB를 둘 수 있습니다.  
→ 장애 대비 기능.

This standby database is available only in case of disaster and cannot be used to perform queries.  
이 대기 DB는 재해 발생 시에만 사용 가능하며 쿼리를 실행할 수는 없습니다.  
→ 평상시에는 읽기 불가.

```
🎖️ **게임 보상: RDS 초보자 → RDS 엔지니어 레벨업!**
```

## Security in Amazon RDS
## Amazon RDS의 보안
## → RDS에서 보안을 어떻게 다루는지 설명합니다.

Security for your RDS database is managed through IAM.  
RDS 데이터베이스의 보안은 IAM을 통해 관리됩니다.  
→ 접근 제어 기반.

You can use username and password authentication to connect to your database, and for some engines, IAM authentication is also supported.  
사용자명/비밀번호 인증을 사용할 수 있고, 일부 엔진에서는 IAM 인증도 지원합니다.  
→ 인증 방식 다양화.

Network security is enforced using security groups.  
네트워크 보안은 보안 그룹을 통해 강제됩니다.  
→ AWS VPC 보안 연동.

Encryption at rest is handled by AWS Key Management Service (KMS), and intrinsic encryption is available using SSL and TLS protocols.  
저장 데이터 암호화는 KMS로 처리되고, 전송 중 암호화는 SSL/TLS 프로토콜로 가능합니다.  
→ 데이터 보호 이중화.

```
🎖️ **게임 보상: RDS 엔지니어 → RDS 보안 전문가 레벨업!**
```

## Backup and Recovery
## 백업과 복구
## → 데이터 안전성을 보장하는 기능입니다.

Amazon RDS provides automated backups with a retention period of up to 35 days.  
Amazon RDS는 최대 35일간 유지되는 자동 백업을 제공합니다.  
→ 단기 복구 보장.

Using automated backups, you can perform point-in-time restores to any moment within the retention window.  
자동 백업을 통해 보존 기간 내 원하는 시점으로 복원할 수 있습니다.  
→ 세밀한 복구 가능.

This process creates a new database instance from the backup.  
이 과정은 백업으로부터 새 DB 인스턴스를 생성합니다.  
→ 원본 DB를 건드리지 않고 복구.

For longer-term backup retention, manual database snapshots can be created and stored indefinitely.  
장기 보관을 위해 수동 DB 스냅샷을 만들어 무기한 저장할 수 있습니다.  
→ 영구 보관 기능.

```
🎖️ **게임 보상: RDS 보안 전문가 → RDS 백업 마스터 레벨업!**
```
