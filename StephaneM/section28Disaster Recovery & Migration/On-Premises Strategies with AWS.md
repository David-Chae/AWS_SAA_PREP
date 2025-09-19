```markdown
# On-Premises Strategies with AWS  
# AWS와 온프레미스 전략  

🎮 게임보상: "On-Premises Specialist" +500 XP  

---

## On-Premises Strategies with AWS  
## AWS와 온프레미스 전략  

In this lecture, we discuss important AWS services and strategies relevant to on-premises infrastructure and migration to the cloud.  
이 강의에서는 온프레미스 인프라와 클라우드 마이그레이션과 관련된 중요한 AWS 서비스와 전략을 다룹니다.  

Understanding these services at a high level is crucial for exam preparation and practical application.  
이 서비스를 개념적으로 이해하는 것은 시험 준비와 실제 활용 모두에 중요합니다.  

---

You can download the Amazon Linux 2 AMI as a virtual machine image in ISO format.  
Amazon Linux 2 AMI를 ISO 형식의 가상 머신 이미지로 다운로드할 수 있습니다.  

This ISO image can be loaded into common virtualization software such as VMWare, KVM, VirtualBox (Oracle VM), or Microsoft Hyper-V.  
이 ISO 이미지는 VMWare, KVM, VirtualBox(Oracle VM), Microsoft Hyper-V 등 일반적인 가상화 소프트웨어에서 로드할 수 있습니다.  

This allows you to run Amazon Linux 2 directly on your on-premises infrastructure using a virtual machine.  
이를 통해 가상 머신을 이용하여 온프레미스 환경에서 직접 Amazon Linux 2를 실행할 수 있습니다.  

This setup enables you to configure the VM with user data and other settings, providing flexibility to run AWS-compatible environments on-premises.  
이 구성으로 VM에 사용자 데이터 및 기타 설정을 적용하여 온프레미스에서 AWS 호환 환경을 유연하게 실행할 수 있습니다.  

---

## VM Import and Export  
## VM 가져오기 및 내보내기  

AWS provides a feature called VM Import and Export, which allows you to migrate your existing virtual machines and applications directly into EC2 instances.  
AWS는 VM Import and Export 기능을 제공하며, 기존 가상 머신과 애플리케이션을 EC2 인스턴스로 직접 마이그레이션할 수 있습니다.  

This feature also supports exporting VMs back from EC2 to your on-premises environment if needed.  
필요 시 EC2에서 온프레미스로 VM을 내보내는 것도 지원합니다.  

This capability can be used to create disaster recovery repositories by backing up on-premises VMs into the cloud, ensuring data safety and availability.  
이 기능은 온프레미스 VM을 클라우드에 백업하여 재해 복구 저장소를 만들고 데이터 안전성과 가용성을 보장하는 데 사용할 수 있습니다.  

---

## AWS Application Discovery Service  
## AWS 애플리케이션 디스커버리 서비스  

This service gathers information about your on-premises servers to assist in migration planning.  
이 서비스는 온프레미스 서버 정보를 수집하여 마이그레이션 계획을 지원합니다.  

It provides high-level data such as server utilization and dependency mappings, which are valuable when performing large-scale migrations from on-premises to AWS.  
서버 활용률, 의존성 매핑 등 고급 데이터를 제공하며, 대규모 온프레미스 → AWS 마이그레이션 시 유용합니다.  

---

## AWS Migration Hub  
## AWS 마이그레이션 허브  

Migration Hub allows you to track the progress of your migration projects across multiple AWS and partner migration tools, providing a centralized view of your migration status.  
Migration Hub는 여러 AWS 및 파트너 마이그레이션 도구에서 마이그레이션 진행 상황을 추적하며 중앙 집중식으로 상태를 확인할 수 있게 해줍니다.  

---

## AWS Database Migration Service (DMS)  
## AWS 데이터베이스 마이그레이션 서비스 (DMS)  

DMS enables replication of databases from on-premises to AWS, AWS to AWS, or AWS back to on-premises.  
DMS는 온프레미스 → AWS, AWS → AWS, AWS → 온프레미스 등 데이터베이스 복제를 지원합니다.  

This service supports various database technologies including Oracle, MySQL, and DynamoDB.  
이 서비스는 Oracle, MySQL, DynamoDB 등 다양한 데이터베이스 기술을 지원합니다.  

It facilitates use cases such as migrating data from MySQL databases into DynamoDB, allowing gradual transition of workloads to AWS while maintaining data consistency.  
MySQL 데이터베이스에서 DynamoDB로 데이터 마이그레이션과 같이, 워크로드를 점진적으로 AWS로 전환하면서 데이터 일관성을 유지하는 사례를 지원합니다.  

---

## AWS Server Migration Service (SMS)  
## AWS 서버 마이그레이션 서비스 (SMS)  

SMS supports incremental replication of live on-premises servers to AWS.  
SMS는 온프레미스 실시간 서버를 AWS로 점진적으로 복제하는 기능을 제공합니다.  

It replicates server volumes directly into AWS, enabling ongoing synchronization for migration or disaster recovery purposes.  
서버 볼륨을 AWS로 직접 복제하여 마이그레이션 또는 재해 복구용 지속적 동기화를 가능하게 합니다.  

---

## Summary  
## 요약  

At a high level, remember these AWS services related to on-premises migration:  
온프레미스 마이그레이션과 관련된 AWS 서비스는 다음과 같습니다.  

- VM Import and Export for migrating VMs between on-premises and EC2.  
- 온프레미스 ↔ EC2 간 VM 마이그레이션을 위한 VM Import and Export.  

- Application Discovery Service for gathering on-premises server data.  
- 온프레미스 서버 데이터 수집용 Application Discovery Service.  

- Migration Hub for tracking migration progress.  
- 마이그레이션 진행 상황 추적용 Migration Hub.  

- Database Migration Service (DMS) for database replication.  
- 데이터베이스 복제를 위한 Database Migration Service (DMS).  

- Server Migration Service (SMS) for incremental server replication.  
- 점진적 서버 복제를 위한 Server Migration Service (SMS).  

Knowing these service names and their purposes will help you recognize related questions and scenarios in exams and practical applications.  
이 서비스 이름과 용도를 알고 있으면 시험 및 실제 활용 시 관련 문제와 시나리오를 이해하는 데 도움이 됩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon Linux 2 AMI can be downloaded as an ISO image to run on-premise virtual machines.  
- Amazon Linux 2 AMI는 ISO 이미지로 다운로드하여 온프레미스 가상 머신에서 실행할 수 있습니다.  

- VM Import and Export enables migration of existing VMs between on-premise environments and AWS EC2.  
- VM Import and Export는 온프레미스 환경과 AWS EC2 간 기존 VM 마이그레이션을 지원합니다.  

- AWS Application Discovery Service helps gather on-premise server data for migration planning.  
- AWS Application Discovery Service는 온프레미스 서버 데이터를 수집하여 마이그레이션 계획을 지원합니다.  

- AWS offers multiple migration services including Migration Hub, Database Migration Service (DMS), and Server Migration Service (SMS) for various migration needs.  
- AWS는 Migration Hub, DMS, SMS 등 다양한 마이그레이션 서비스로 다양한 마이그레이션 요구를 지원합니다.  
```
