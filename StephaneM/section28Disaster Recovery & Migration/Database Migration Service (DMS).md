```markdown
# Database Migration Service (DMS)  
# 데이터베이스 마이그레이션 서비스 (DMS)  

🎮 게임보상: "Database Migration Apprentice" +500 XP  

---

## Introduction to AWS Database Migration Service (DMS)  
## AWS 데이터베이스 마이그레이션 서비스(DMS) 소개  

Let's say you want to migrate a database from your on-premises systems to the AWS Cloud.  
온프레미스 시스템에서 AWS 클라우드로 데이터베이스를 마이그레이션하고 싶다고 가정해봅시다.  

In this case, you should use DMS, or Database Migration Service.  
이 경우 DMS(Database Migration Service)를 사용해야 합니다.  

It is a quick and secure database service that allows you to migrate your database from on-premises to AWS.  
DMS는 온프레미스 데이터베이스를 AWS로 빠르고 안전하게 마이그레이션할 수 있는 서비스입니다.  

The service is resilient and self-healing.  
이 서비스는 내구성이 강하고 자체 복구 기능을 제공합니다.  

Importantly, during the migration, the source database remains available.  
중요한 점은 마이그레이션 중에도 원본 데이터베이스는 계속 사용 가능하다는 것입니다.  

---

DMS supports many types of database engines.  
DMS는 다양한 데이터베이스 엔진을 지원합니다.  

It allows homogeneous migrations, such as Oracle to Oracle or PostgreSQL to PostgreSQL.  
동일 엔진 간 마이그레이션(예: Oracle → Oracle, PostgreSQL → PostgreSQL)도 가능합니다.  

It also supports heterogeneous migrations; for example, migrating from Microsoft SQL Server to Aurora.  
서로 다른 엔진 간 마이그레이션(예: Microsoft SQL Server → Aurora)도 지원합니다.  

Additionally, it supports continuous data replication using Change Data Capture (CDC).  
또한 Change Data Capture(CDC)를 사용한 지속적인 데이터 복제도 지원합니다.  

---

To use DMS, you need to create an EC2 instance.  
DMS를 사용하려면 EC2 인스턴스를 생성해야 합니다.  

This EC2 instance performs the replication tasks for you.  
이 EC2 인스턴스가 복제 작업을 수행합니다.  

Simply put, your source database may be on-premises, and you run an EC2 instance with the DMS software.  
즉, 원본 데이터베이스가 온프레미스에 있고, DMS 소프트웨어가 설치된 EC2 인스턴스를 실행합니다.  

This instance continuously pulls data from the source database and inserts it into the target database.  
이 인스턴스는 원본 데이터베이스에서 데이터를 지속적으로 가져와 대상 데이터베이스에 삽입합니다.  

---

## Supported Source and Target Databases  
## 지원되는 소스 및 대상 데이터베이스  

The sources can be on-premises databases or EC2 instance-based databases, including Oracle, Microsoft SQL Server, MySQL, MariaDB, PostgreSQL, MongoDB, SAP, and DB2.  
소스는 온프레미스 또는 EC2 기반 데이터베이스일 수 있으며, Oracle, Microsoft SQL Server, MySQL, MariaDB, PostgreSQL, MongoDB, SAP, DB2 등이 포함됩니다.  

It can also be Azure databases, such as Azure SQL Database.  
또한 Azure SQL Database와 같은 Azure 데이터베이스도 지원합니다.  

Additionally, Amazon RDS databases, including Aurora, Amazon S3, and DocumentDB, can be sources.  
추가로, Amazon RDS 데이터베이스(예: Aurora, Amazon S3, DocumentDB)도 소스로 사용 가능합니다.  

---

In terms of targets, there are various options as well.  
대상 데이터베이스도 다양한 옵션이 있습니다.  

Targets can be on-premises or EC2 instance databases such as Oracle, Microsoft SQL Server, MySQL, MariaDB, PostgreSQL, and SAP.  
대상은 온프레미스 또는 EC2 인스턴스 데이터베이스(Oracle, Microsoft SQL Server, MySQL, MariaDB, PostgreSQL, SAP 등)일 수 있습니다.  

Targets also include any database on Amazon RDS, Redshift, DynamoDB, Amazon S3, the open-source service Kinesis Data Streams, Apache Kafka, DocumentDB, Amazon Neptune, Redis, and Babelfish.  
대상에는 Amazon RDS, Redshift, DynamoDB, Amazon S3, Kinesis Data Streams, Apache Kafka, DocumentDB, Amazon Neptune, Redis, Babelfish도 포함됩니다.  

---

You do not need to remember all these databases, but the general idea is that DMS can help you take a database, for example, an on-premises database, and migrate it onto almost any database that AWS offers.  
모든 데이터베이스를 외울 필요는 없지만, 핵심 개념은 DMS를 사용하면 온프레미스 데이터베이스를 AWS에서 제공하는 거의 모든 데이터베이스로 마이그레이션할 수 있다는 점입니다.  

Understanding this concept gives you the general idea behind DMS.  
이 개념을 이해하면 DMS의 기본 원리를 알 수 있습니다.  

---

## Using AWS Schema Conversion Tool (SCT) for Heterogeneous Migrations  
## 서로 다른 엔진 마이그레이션을 위한 AWS SCT 사용  

What if the source and target databases do not have the same engine?  
원본과 대상 데이터베이스 엔진이 다르면 어떻게 해야 할까요?  

In that case, you need to use AWS SCT, the Schema Conversion Tool.  
이 경우 AWS SCT(Schema Conversion Tool)를 사용해야 합니다.  

It converts the database schema from one engine to another.  
SCT는 데이터베이스 스키마를 한 엔진에서 다른 엔진으로 변환합니다.  

For example, if you are migrating an OLTP database from SQL Server or Oracle to MySQL, PostgreSQL, or Aurora, SCT is required.  
예를 들어, OLTP 데이터베이스를 SQL Server 또는 Oracle에서 MySQL, PostgreSQL, Aurora로 마이그레이션할 때 SCT가 필요합니다.  

---

As illustrated, the source database engine differs from the target database engine.  
예시에서 볼 수 있듯, 소스 엔진과 대상 엔진이 다릅니다.  

DMS runs alongside SCT to perform the migration.  
DMS는 SCT와 함께 실행되어 마이그레이션을 수행합니다.  

It is important to know that you do not need to use SCT if you are migrating between the same database engine.  
동일한 엔진 간 마이그레이션 시 SCT를 사용할 필요가 없다는 점이 중요합니다.  

For instance, migrating from on-premises PostgreSQL to RDS PostgreSQL does not require SCT.  
예를 들어, 온프레미스 PostgreSQL → RDS PostgreSQL 마이그레이션은 SCT가 필요하지 않습니다.  

However, migrating from Oracle to PostgreSQL does require SCT.  
하지만 Oracle → PostgreSQL 마이그레이션에는 SCT가 필요합니다.  

Note that the database engine is PostgreSQL, but RDS is simply the platform used to run this database engine.  
데이터베이스 엔진은 PostgreSQL이지만, RDS는 단지 이 엔진을 실행하는 플랫폼임을 참고하세요.  

---

## Setting Up Continuous Replication with DMS  
## DMS를 이용한 지속적 복제 설정  

To set up continuous replication with DMS, consider a corporate data center with an Oracle database as the source and an Amazon RDS MySQL database as the target.  
DMS를 사용해 지속적 복제를 설정하려면, 소스로 Oracle 데이터베이스, 대상으로 Amazon RDS MySQL 데이터베이스가 있는 기업 데이터센터를 가정합니다.  

Since these are different database types, SCT is required for the migration to work.  
서로 다른 데이터베이스 유형이므로 마이그레이션을 위해 SCT가 필요합니다.  

The best practice is to set up a server with AWS SCT installed on-premises.  
최선의 방법은 온프레미스에 AWS SCT가 설치된 서버를 설정하는 것입니다.  

This server performs the schema conversion into the Amazon RDS MySQL database.  
이 서버는 Amazon RDS MySQL 데이터베이스로 스키마 변환을 수행합니다.  

Then, a DMS replication instance is set up to perform the full load and change data capture (CDC) for continuous replication.  
그런 다음, 지속적 복제를 위해 전체 로드와 CDC를 수행하는 DMS 복제 인스턴스를 설정합니다.  

The replication instance reads the source Oracle database on-premises and inserts the data into your private subnets in AWS.  
복제 인스턴스는 온프레미스 Oracle 데이터베이스를 읽고 데이터를 AWS의 프라이빗 서브넷에 삽입합니다.  

---

## Additional Features of DMS  
## DMS의 추가 기능  

DMS supports multi-AZ deployment.  
DMS는 다중 AZ 배포를 지원합니다.  

This means you can have a DMS replication instance in one Availability Zone (AZ) and a synchronous replication of that instance into another AZ, which acts as a standby replica.  
즉, 한 AZ에 DMS 복제 인스턴스를 두고, 이를 다른 AZ에 동기 복제하여 스탠바이 복제로 사용할 수 있습니다.  

This setup provides resilience to failure in a specific AZ, data redundancy, eliminates IO freezes, and minimizes latency spikes.  
이 설정은 특정 AZ 실패에 대한 내구성, 데이터 중복성 확보, IO 정지 제거, 지연 시간 급증 최소화를 제공합니다.  

---

This concludes the lecture on Database Migration Service.  
이로써 Database Migration Service 강의가 종료됩니다.  

Remember to use SCT whenever migrating between different database engines.  
서로 다른 데이터베이스 엔진 간 마이그레이션 시 SCT 사용을 잊지 마세요.  

DMS provides a resilient and efficient way to migrate and replicate databases in AWS.  
DMS는 AWS에서 데이터베이스를 효율적이고 내구성 있게 마이그레이션하고 복제할 수 있는 방법을 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Database Migration Service (DMS) enables quick, secure, and resilient migration of databases from on-premises to AWS while keeping the source database available.  
- DMS는 온프레미스 데이터베이스를 AWS로 빠르고 안전하게, 내구성 있게 마이그레이션하면서 원본 데이터베이스를 사용 가능하게 유지합니다.  

- DMS supports both homogeneous migrations (same engine) and heterogeneous migrations (different engines), with continuous data replication using Change Data Capture (CDC).  
- DMS는 동일 엔진 마이그레이션과 다른 엔진 마이그레이션 모두를 지원하며, CDC를 통한 지속적 데이터 복제를 제공합니다.  

- An EC2 instance running DMS software
```


performs the replication tasks between source and target databases.

* DMS 소프트웨어가 설치된 EC2 인스턴스가 소스와 대상 데이터베이스 간의 복제 작업을 수행합니다.

* When migrating between different database engines, AWS Schema Conversion Tool (SCT) is required to convert the database schema; it is not needed for migrations between the same engine.

* 서로 다른 엔진 간 마이그레이션 시 AWS SCT가 필요하며, 동일 엔진 간 마이그레이션에는 필요하지 않습니다.

* DMS supports multi-AZ deployments for high availability, data redundancy, and minimizing latency spikes.

* DMS는 고가용성, 데이터 중복성, 지연 시간 최소화를 위해 다중 AZ 배포를 지원합니다.

```
