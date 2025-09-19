```markdown
# Disaster Recovery in AWS  
# AWS에서의 재해 복구  

🎮 게임보상: "Cloud Resilience Master" +600 XP  

---

## Introduction to Disaster Recovery  
## 재해 복구 소개  

Disaster recovery is a critical topic for solutions architects, especially in the context of AWS.  
재해 복구는 솔루션 아키텍트에게 매우 중요한 주제이며, 특히 AWS 환경에서 중요합니다.  

The AWS disaster recovery white paper is a valuable resource, but this lecture summarizes the key concepts with clear graphs and diagrams to simplify understanding.  
AWS 재해 복구 백서는 귀중한 자료이지만, 이 강의에서는 이해를 돕기 위해 주요 개념을 명확한 그래프와 다이어그램으로 요약합니다.  

Disaster recovery questions are common in exams and essential knowledge for solutions architects.  
재해 복구 관련 질문은 시험에서 자주 나오며, 솔루션 아키텍트에게 필수적인 지식입니다.  

---

## What is a Disaster?  
## 재해란 무엇인가?  

A disaster is any event that negatively impacts a company's business continuity or finances.  
재해는 회사의 비즈니스 연속성이나 재정에 부정적인 영향을 미치는 모든 사건을 말합니다.  

Disaster recovery involves preparing for and recovering from such events to minimize their impact.  
재해 복구는 이러한 사건에 대비하고 복구하여 영향을 최소화하는 과정을 포함합니다.  

---

## Types of Disaster Recovery  
## 재해 복구 유형  

There are several disaster recovery approaches:  
재해 복구에는 여러 접근 방식이 있습니다.  

**On-premise to on-premise**: Traditional method with multiple data centers, such as one in California and another in Seattle. This approach is very expensive.  
**온프레미스 → 온프레미스**: 캘리포니아와 시애틀 등 여러 데이터센터를 활용하는 전통적인 방식으로 비용이 매우 높습니다.  

**Hybrid recovery**: Using an on-premise data center as the primary site and the cloud as a backup.  
**하이브리드 복구**: 온프레미스 데이터센터를 주 사이트로, 클라우드를 백업으로 사용하는 방식입니다.  

**Full cloud**: Using AWS cloud regions, for example, replicating from one AWS region to another for disaster recovery.  
**풀 클라우드**: AWS 클라우드 리전을 활용하여 한 리전에서 다른 리전으로 데이터를 복제하는 방식입니다.  

---

## Key Terms: RPO and RTO  
## 핵심 용어: RPO와 RTO  

Before diving into disaster recovery strategies, it is important to understand two key terms:  
재해 복구 전략을 논의하기 전에 두 가지 핵심 용어를 이해하는 것이 중요합니다.  

**Recovery Point Objective (RPO)**: Defines how far back in time you can recover data after a disaster. It relates to how often backups are run.  
**복구 지점 목표(RPO)**: 재해 발생 후 데이터를 얼마나 이전 시점으로 복구할 수 있는지 정의합니다. 백업 수행 주기와 관련이 있습니다.  

For example, if backups occur every hour, the maximum data loss is one hour.  
예를 들어, 백업을 매시간 수행한다면 최대 데이터 손실은 1시간입니다.  

**Recovery Time Objective (RTO)**: Defines how quickly you can recover and resume operations after a disaster. It represents the acceptable downtime.  
**복구 시간 목표(RTO)**: 재해 발생 후 얼마나 빨리 복구하고 운영을 재개할 수 있는지 정의하며, 허용 가능한 다운타임을 나타냅니다.  

Optimizing for lower RPO and RTO usually increases costs.  
RPO와 RTO를 낮추도록 최적화하면 일반적으로 비용이 증가합니다.  

---

## Disaster Recovery Strategies Overview  
## 재해 복구 전략 개요  

There are four main disaster recovery strategies, each with different RTO and cost implications:  
주요 재해 복구 전략은 4가지이며, 각 전략은 RTO와 비용에 차이가 있습니다.  

- **Backup and Restore**: Highest RTO and RPO, but lowest cost.  
- **백업 및 복원**: 가장 높은 RTO와 RPO, 그러나 가장 저렴한 비용.  

- **Pilot Light**: Lower RTO and RPO than Backup and Restore, moderate cost.  
- **파일럿 라이트**: 백업 및 복원보다 낮은 RTO와 RPO, 중간 수준 비용.  

- **Warm Standby**: Further reduced RTO and RPO, higher cost.  
- **웜 스탠바이**: 더 낮은 RTO와 RPO, 비용 증가.  

- **Multi-Site (Hot Site)**: Lowest RTO and RPO, highest cost.  
- **멀티 사이트(핫 사이트)**: 가장 낮은 RTO와 RPO, 가장 높은 비용.  

The faster the recovery, the more expensive the strategy.  
복구 속도가 빠를수록 전략 비용이 증가합니다.  

---

## Backup and Restore  
## 백업 및 복원  

This strategy involves backing up data from a corporate data center to AWS cloud storage such as S3, Glacier, or using Snowball for large data transfers.  
이 전략은 기업 데이터센터의 데이터를 AWS 클라우드 스토리지(S3, Glacier)로 백업하거나 대용량 데이터 전송 시 Snowball을 사용하는 방식입니다.  

For example, sending data weekly via Snowball results in an RPO of about one week.  
예를 들어, 매주 Snowball로 데이터를 전송하면 RPO는 약 1주가 됩니다.  

Using AWS snapshots for EBS volumes, Redshift, or RDS can reduce RPO to 24 hours or less depending on snapshot frequency.  
EBS, Redshift, RDS 스냅샷을 사용하면 스냅샷 주기에 따라 RPO를 24시간 이하로 줄일 수 있습니다.  

Restoration involves recreating infrastructure using AMIs or snapshots, which can take significant time, resulting in high RTO.  
복원은 AMI 또는 스냅샷을 사용하여 인프라를 재구성하는 과정을 포함하며, 시간이 많이 걸려 높은 RTO를 초래합니다.  

This approach is cost-effective since infrastructure is only created when needed, and costs are mainly for storage.  
이 접근 방식은 인프라를 필요할 때만 생성하므로 비용 효율적이며, 비용은 주로 스토리지에 해당됩니다.  

---

## Pilot Light  
## 파일럿 라이트  

Pilot Light keeps a minimal version of the application running in the cloud, typically the critical core systems such as the database.  
파일럿 라이트는 클라우드에서 애플리케이션 최소 버전을 실행하며, 주로 데이터베이스와 같은 핵심 시스템을 유지합니다.  

For example, continuous data replication from an on-premise database to an AWS RDS instance that is always running.  
예를 들어, 온프레미스 데이터베이스에서 AWS RDS 인스턴스로 데이터를 지속적으로 복제합니다.  

In case of disaster, non-critical components like EC2 instances are created and started.  
재해 발생 시, EC2 인스턴스와 같은 비핵심 구성 요소를 생성하고 시작합니다.  

Route 53 can be used to fail over DNS to the cloud environment.  
Route 53을 사용하여 DNS를 클라우드 환경으로 페일오버할 수 있습니다.  

This approach lowers RPO and RTO compared to Backup and Restore while managing costs by running only critical systems continuously.  
이 방식은 백업 및 복원보다 RPO와 RTO를 낮추며, 핵심 시스템만 지속적으로 실행하여 비용을 관리합니다.  

---

## Warm Standby  
## 웜 스탠바이  

Warm Standby maintains a full but scaled-down version of the production environment running in the cloud.  
웜 스탠바이는 클라우드에서 전체 생산 환경을 축소하여 실행합니다.  

Components such as reverse proxies, app servers, and databases run at minimum capacity and replicate data continuously.  
리버스 프록시, 앱 서버, 데이터베이스 등 구성 요소는 최소 용량으로 실행되며 데이터를 지속적으로 복제합니다.  

Route 53 directs traffic to the corporate data center under normal conditions but can fail over to the cloud ELB and scaled-up EC2 Auto Scaling groups during a disaster.  
Route 53은 평상시 트래픽을 기업 데이터센터로 라우팅하지만, 재해 발생 시 클라우드 ELB와 EC2 Auto Scaling 그룹으로 페일오버할 수 있습니다.  

This strategy reduces RPO and RTO further but increases costs due to always running infrastructure.  
이 전략은 RPO와 RTO를 더 낮추지만, 항상 인프라를 실행하기 때문에 비용이 증가합니다.  

---

## Multi-Site / Hot Site  
## 멀티 사이트 / 핫 사이트  

This approach runs full production-scale environments simultaneously on-premise and in AWS.  
이 접근 방식은 온프레미스와 AWS에서 전체 생산 환경을 동시에 실행합니다.  

Data replication keeps both sites synchronized.  
데이터 복제는 두 사이트를 동기화 상태로 유지합니다.  

Route 53 can route requests actively to both sites (active-active setup).  
Route 53은 요청을 두 사이트로 동시에 라우팅할 수 있습니다(액티브-액티브 설정).  

Failover is nearly instantaneous with minimal downtime (low RTO).  
페일오버는 거의 즉시 이루어지며 다운타임이 최소화됩니다(낮은 RTO).  

This method is very expensive but provides the highest availability and fastest recovery.  
이 방법은 비용이 매우 높지만 가장 높은 가용성과 빠른 복구를 제공합니다.  

---

## All-Cloud Multi-Region Setup  
## 올-클라우드 다중 리전 설정  

In an all-cloud scenario, a multi-region architecture can be used.  
올-클라우드 환경에서는 다중 리전 아키텍처를 사용할 수 있습니다.  

For example, an Aurora global database replicates data between regions.  
예를 들어, Aurora 글로벌 데이터베이스는 리전 간 데이터를 복제합니다.  

Both regions can serve production traffic, and failover can be performed to another region quickly to maintain availability.  
두 리전 모두 프로덕션 트래픽을 처리하며, 가용성을 유지하기 위해 다른 리전으로 신속하게 페일오버할 수 있습니다.  

---

## Disaster Recovery Tips  
## 재해 복구 팁  

- Use EBS snapshots, RDS automated snapshots, and backups regularly.  
- EBS 스냅샷, RDS 자동 스냅샷, 백업을 정기적으로 사용하세요.  

- Store backups in S3, S3 Infrequent Access, or Glacier with lifecycle policies.  
- 백업을 S3, S3 IA, Glacier에 라이프사이클 정책과 함께 저장하세요.  

- Use Cross-Region Replication to keep backups in multiple regions.  
- 다중 리전 복제를 사용하여 백업을 여러 리전에 보관하세요.  

- For on-premise to cloud data transfer, use AWS Snowball or Storage Gateway.  
- 온프레미스 → 클라우드 데이터 전송 시 AWS Snowball 또는 Storage Gateway 사용.  

- Use Route 53 for DNS failover between regions.  
- 리전 간 DNS 페일오버에 Route 53 사용.  

- Enable multi-AZ deployments for RDS, ElastiCache, EFS, and S3 for high availability.  
- 높은 가용성을 위해 RDS, ElastiCache, EFS, S3의 다중 AZ 배포 활성화.  

- For network resilience, use Direct Connect with site-to-site VPN as a backup.  
- 네트워크 복원력 확보를 위해 Direct Connect + Site-to-Site VPN 백업 사용.  

- Use database replication tools or Storage Gateway for on-premise to cloud replication.  
- 온프레미스 → 클라우드 복제를 위해 DB 복제 툴 또는 Storage Gateway 사용.  

- Autom
```


ate recovery with CloudFormation, Elastic Beanstalk, CloudWatch alarms, and AWS Lambda.

* CloudFormation, Elastic Beanstalk, CloudWatch 알람, Lambda로 복구 자동화.

* Automate disaster recovery processes to improve success rates.

* 재해 복구 프로세스를 자동화하여 성공률 향상.

---

## Chaos Testing

## 카오스 테스트

To ensure disaster recovery readiness, simulate failures regularly.
재해 복구 준비 상태를 보장하기 위해 정기적으로 장애를 시뮬레이션하세요.

Netflix's Simian Army randomly terminates EC2 instances in production to test infrastructure resilience.
Netflix Simian Army는 프로덕션에서 EC2 인스턴스를 무작위 종료하여 인프라 복원력을 테스트합니다.

This practice helps verify that systems can survive failures and recover automatically, ensuring robust disaster recovery.
이 실습은 시스템이 장애를 견디고 자동으로 복구할 수 있는지 검증하여 강력한 재해 복구를 보장합니다.

---

## Conclusion

## 결론

Disaster recovery is vital for maintaining business continuity.
재해 복구는 비즈니스 연속성을 유지하는 데 필수적입니다.

Understanding RPO and RTO helps in selecting the appropriate strategy balancing cost and recovery speed.
RPO와 RTO를 이해하면 비용과 복구 속도의 균형을 맞춘 적절한 전략 선택이 가능합니다.

AWS provides multiple strategies and tools to implement effective disaster recovery.
AWS는 효과적인 재해 복구를 구현할 수 있는 다양한 전략과 도구를 제공합니다.

Automation and chaos testing further enhance preparedness and resilience.
자동화와 카오스 테스트는 준비성과 복원력을 더욱 강화합니다.

---

## Key Takeaways

## 핵심 요약

* Disaster recovery is essential for business continuity and involves preparing for and recovering from events that negatively impact operations.

* 재해 복구는 비즈니스 연속성에 필수적이며, 운영에 부정적 영향을 미치는 사건에 대비하고 복구하는 과정을 포함합니다.

* Recovery Point Objective (RPO) defines the acceptable amount of data loss, while Recovery Time Objective (RTO) defines acceptable downtime.

* RPO는 허용 가능한 데이터 손실량을 정의하고, RTO는 허용 가능한 다운타임을 정의합니다.

* AWS disaster recovery strategies include Backup and Restore, Pilot Light, Warm Standby, and Multi-Site/Hot Site, each balancing cost and recovery speed.

* AWS 재해 복구 전략에는 백업 및 복원, 파일럿 라이트, 웜 스탠바이, 멀티 사이트/핫 사이트가 있으며, 각각 비용과 복구 속도의 균형을 고려합니다.

* Automation and chaos testing, such as Netflix's Simian Army, help ensure infrastructure resilience and effective disaster recovery.

* Netflix Simian Army와 같은 자동화 및 카오스 테스트는 인프라 복원력과 효과적인 재해 복구를 보장하는 데 도움을 줍니다.

```
