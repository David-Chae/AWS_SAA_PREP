# Amazon RDS Overview  
# 아마존 RDS 개요  

---

## Overview of AWS RDS  
## AWS RDS 개요  

Amazon RDS stands for Relational Database Service.  
Amazon RDS는 관계형 데이터베이스 서비스(Relational Database Service)를 의미합니다.  
(정의)

It is a managed database service designed for databases that use SQL as their query language.  
SQL을 쿼리 언어로 사용하는 데이터베이스용으로 설계된 관리형 데이터베이스 서비스입니다.  
(설명)

SQL is a structured language widely used to query databases and is supported by many database engines.  
SQL은 데이터베이스 쿼리에 널리 사용되는 구조화된 언어로, 많은 데이터베이스 엔진에서 지원됩니다.  
(기초 정보)

With RDS, you can create databases in the cloud that are managed by AWS, providing numerous benefits.  
RDS를 사용하면 AWS가 관리하는 클라우드 데이터베이스를 생성할 수 있으며, 다양한 장점을 제공합니다.  
(장점 안내)

The types of database engines managed by AWS include:  
AWS에서 관리하는 데이터베이스 엔진 유형은 다음과 같습니다.  
(엔진 목록)

- PostgreSQL  
- PostgreSQL  

- MySQL  
- MySQL  

- MariaDB  
- MariaDB  

- Oracle  
- Oracle  

- Microsoft SQL Server  
- Microsoft SQL Server  

- IBM DB2  
- IBM DB2  

- Aurora, which is a proprietary database engine from AWS that will be studied in depth.  
- Aurora: AWS 고유의 데이터베이스 엔진으로, 심층 학습할 예정입니다.  

---

## Advantages of Using Amazon RDS  
## 아마존 RDS 사용 장점  

Why use RDS instead of deploying your own database service on an EC2 instance?  
EC2에 직접 데이터베이스를 배포하는 대신 RDS를 사용하는 이유는 무엇일까요?  
(비교)

Although deploying on EC2 is possible, RDS is a managed service that provides many additional features beyond just hosting a database:  
EC2 배포도 가능하지만, RDS는 데이터베이스 호스팅 외에도 다양한 관리 기능을 제공합니다.  
(관리 기능 강조)

- Fully automated provisioning of the database.  
- 데이터베이스 완전 자동 프로비저닝  

- Automated patching of the underlying operating system.  
- 기본 OS 자동 패치  

- Continuous backups with the ability to restore to a specific timestamp, known as Point in Time Restore.  
- 특정 시점으로 복원 가능한 지속적 백업(Point in Time Restore)  

- Monitoring dashboards to view database performance.  
- 데이터베이스 성능 모니터링 대시보드 제공  

- Support for read replicas to improve read performance.  
- 읽기 성능 향상을 위한 Read Replica 지원  

- Multi-AZ deployments for disaster recovery.  
- 재해 복구용 다중 가용 영역(Multi-AZ) 배포  

- Maintenance windows for upgrades.  
- 업그레이드용 유지보수 윈도우  

- Scaling capabilities both vertically (increasing instance type) and horizontally (adding read replicas).  
- 수직(인스턴스 유형 증가) 및 수평(읽기 복제본 추가) 확장 기능  

- Storage backed by Elastic Block Store (EBS).  
- EBS 기반 스토리지  

One limitation is that you cannot SSH into the RDS instances because AWS manages the underlying infrastructure.  
제한점: AWS가 인프라를 관리하기 때문에 RDS 인스턴스에 SSH로 접근할 수 없습니다.  

---

## RDS Storage Auto Scaling Feature  
## RDS 스토리지 자동 확장 기능  

A notable feature of RDS is Storage Auto Scaling.  
RDS의 주요 기능 중 하나는 스토리지 자동 확장(Storage Auto Scaling)입니다.  
(기능 소개)

When creating an RDS database, you specify the initial storage size, for example, 20 gigabytes.  
RDS 데이터베이스 생성 시 초기 스토리지 크기(예: 20GB)를 지정합니다.  
(설정)

If your database usage grows and you approach the storage limit, RDS can automatically increase the storage size without requiring manual intervention or downtime.  
데이터베이스 사용량이 증가하여 스토리지 한계에 가까워지면 RDS가 수동 개입이나 다운타임 없이 자동으로 스토리지를 증가시킵니다.  
(자동 확장 설명)

This feature is especially useful for applications with unpredictable workloads.  
예측 불가능한 워크로드를 가진 애플리케이션에 특히 유용합니다.  
(적용 대상)

The auto scaling triggers when:  
자동 확장은 다음 조건에서 발생합니다.  
(조건)

- Free storage is less than 10% of the allocated storage.  
- 남은 스토리지가 할당량의 10% 미만일 때  

- The low storage condition persists for more than five minutes.  
- 낮은 스토리지 상태가 5분 이상 지속될 때  

- At least six hours have passed since the last storage modification.  
- 마지막 스토리지 변경 후 최소 6시간 경과  

You must set a maximum storage threshold to prevent unlimited growth.  
무제한 증가를 방지하려면 최대 스토리지 한도를 설정해야 합니다.  
(제한 설정)

Storage Auto Scaling supports all database engines managed by RDS.  
스토리지 자동 확장은 RDS에서 관리하는 모든 데이터베이스 엔진을 지원합니다.  
(호환성)

---

## Summary  
## 요약  

Amazon RDS provides a fully managed relational database service with automated provisioning, maintenance, backups, scaling, and monitoring.  
Amazon RDS는 프로비저닝, 유지보수, 백업, 스케일링, 모니터링이 자동화된 관리형 관계형 데이터베이스 서비스를 제공합니다.  
(서비스 요약)

Its Storage Auto Scaling feature helps maintain database availability by automatically increasing storage as needed.  
스토리지 자동 확장 기능은 필요에 따라 스토리지를 자동 증가시켜 데이터베이스 가용성을 유지하는 데 도움을 줍니다.  
(기능 요약)

While you do not have direct access to the underlying instances, the managed service benefits simplify database administration significantly.  
기본 인스턴스에 직접 접근할 수 없지만, 관리형 서비스 혜택으로 데이터베이스 관리가 크게 간소화됩니다.  
(장점 요약)

---

## Key Takeaways  
## 핵심 요약  

- Amazon RDS is a managed relational database service supporting multiple SQL database engines.  
- Amazon RDS는 여러 SQL 데이터베이스 엔진을 지원하는 관리형 관계형 데이터베이스 서비스입니다.  

- RDS automates provisioning, OS patching, backups, monitoring, scaling, and disaster recovery features.  
- RDS는 프로비저닝, OS 패치, 백업, 모니터링, 스케일링, 재해 복구 기능을 자동화합니다.  

- Storage Auto Scaling allows automatic storage increase based on usage thresholds without downtime.  
- 스토리지 자동 확장은 다운타임 없이 사용량 임계치에 따라 스토리지를 자동 증가시킵니다.  

- RDS does not provide SSH access to underlying instances but offers many managed service benefits.  
- RDS는 기본 인스턴스에 SSH 접근은 제공하지 않지만, 다양한 관리형 서비스 혜택을 제공합니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+200XP**
* 아이템: **"RDS 마스터 키" (+20% DB 관리 효율)**
* 업적 달성: **"클라우드 DB 기초 완료"** 🏆

RDS 구조와 스토리지 자동 확장을 실습 자료와 연결하면 **실제 배포 환경 관리 능력** 향상에 도움이 됩니다.
