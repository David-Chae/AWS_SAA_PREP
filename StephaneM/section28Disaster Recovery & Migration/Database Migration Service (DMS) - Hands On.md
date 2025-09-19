```markdown
# Database Migration Service (DMS) - Hands On  
# 데이터베이스 마이그레이션 서비스 (DMS) - 실습  

🎮 게임보상: "Database Migration Explorer" +500 XP  

---

## Introduction to AWS Database Migration Service (DMS)  
## AWS 데이터베이스 마이그레이션 서비스(DMS) 소개  

Let's explore the different options offered by the AWS Database Migration Service, or DMS.  
AWS Database Migration Service(DMS)가 제공하는 다양한 옵션을 살펴봅시다.  

We will begin by identifying the appropriate migration type needed for your use case.  
먼저 사용 사례에 적합한 마이그레이션 유형을 확인하는 것부터 시작합니다.  

---

## Discovery and Assessment with AWS DMS Fleet Advisor  
## AWS DMS Fleet Advisor를 이용한 발견 및 평가  

The first step is to discover and assess your on-premises database inventory using AWS DMS Fleet Advisor.  
첫 번째 단계는 AWS DMS Fleet Advisor를 사용하여 온프레미스 데이터베이스 인벤토리를 발견하고 평가하는 것입니다.  

This tool analyzes your databases and identifies potential migration paths.  
이 도구는 데이터베이스를 분석하고 잠재적인 마이그레이션 경로를 식별합니다.  

It provides results within hours, significantly reducing planning time without requiring third-party tools or hiring migration experts.  
몇 시간 내에 결과를 제공하며, 타사 도구나 마이그레이션 전문가를 고용하지 않고도 계획 시간을 크게 단축할 수 있습니다.  

---

## Schema Conversion  
## 스키마 변환  

The second option is to use the DMS Schema Conversion tool.  
두 번째 옵션은 DMS Schema Conversion Tool을 사용하는 것입니다.  

This tool converts database schemas from one database technology to another.  
이 도구는 데이터베이스 스키마를 한 데이터베이스 기술에서 다른 기술로 변환합니다.  

It helps you understand the types of transformations that can be performed during migration.  
마이그레이션 중 수행할 수 있는 변환 유형을 이해하는 데 도움을 줍니다.  

---

## Migration Options  
## 마이그레이션 옵션  

AWS DMS supports different migration types:  
AWS DMS는 다양한 마이그레이션 유형을 지원합니다.  

- **Homogeneous Data Migration:** Migrating between the same database technologies, such as Oracle to Oracle. This approach can leverage native database tools for faster migration.  
- **동일 엔진 마이그레이션(Homogeneous):** Oracle → Oracle과 같이 동일한 데이터베이스 기술 간 마이그레이션. 이 경우 네이티브 DB 도구를 활용해 빠르게 마이그레이션 가능.  

- **Heterogeneous Data Migration:** Migrating between different database technologies, for example, Oracle to Aurora or Oracle to PostgreSQL.  
- **서로 다른 엔진 마이그레이션(Heterogeneous):** Oracle → Aurora, Oracle → PostgreSQL 등 서로 다른 기술 간 마이그레이션.  

---

## Migration Methods  
## 마이그레이션 방법  

For heterogeneous migrations, two methods are available:  
서로 다른 엔진 간 마이그레이션에는 두 가지 방법이 있습니다.  

- **Instance-Based Migration:** Uses an EC2 instance managed by DMS to perform the migration. You manage the instance indirectly through DMS.  
- **인스턴스 기반 마이그레이션:** DMS가 관리하는 EC2 인스턴스를 사용하여 마이그레이션 수행. DMS를 통해 간접적으로 인스턴스를 관리합니다.  

- **Serverless Replication:** Requires no management of resources but does not support all database engines. It is recommended to try serverless replication first for its simplicity and ease of use. If unsupported, use instance-based migration.  
- **서버리스 복제(Serverless):** 리소스 관리 필요 없음. 하지만 모든 DB 엔진을 지원하지는 않음. 단순하고 사용이 편리하므로 서버리스 복제를 먼저 시도하고, 지원되지 않으면 인스턴스 기반 마이그레이션 사용 권장.  

---

## Creating a Replication Instance  
## 복제 인스턴스 생성  

When using instance-based migration, you create a replication instance with the following configurations:  
인스턴스 기반 마이그레이션을 사용할 때, 다음 구성으로 복제 인스턴스를 생성합니다.  

- **Name and Description:** Provide identifiers for your instance.  
- 이름 및 설명: 인스턴스 식별자를 제공합니다.  

- **Instance Size:** Choose based on data volume and load, ranging from t3.micro to larger instances.  
- 인스턴스 크기: 데이터 용량과 부하에 맞게 선택(t3.micro~대형 인스턴스).  

- **DMS Version:** Select the version and review release notes for updates.  
- DMS 버전: 버전을 선택하고 릴리즈 노트를 확인합니다.  

- **High Availability:** For production workloads, enable multi-Availability Zone (AZ) deployment to ensure resilience. For development or testing, single AZ may suffice.  
- 고가용성: 프로덕션 워크로드의 경우 다중 AZ 배포로 내구성 확보. 개발/테스트는 단일 AZ도 가능.  

- **Storage:** Specify the storage size for your EC2 instance.  
- 스토리지: EC2 인스턴스의 스토리지 크기 지정.  

- **Connectivity and Security:** Configure IP addresses, VPC, subnet groups, and public accessibility.  
- 연결 및 보안: IP, VPC, 서브넷 그룹, 공개 접근 설정.  

- **Advanced and Maintenance Settings:** Optional configurations for operating system maintenance and other advanced options.  
- 고급 및 유지보수 설정: OS 유지보수 및 기타 고급 옵션 선택 가능.  

Once configured, you can create the replication instance. Note that creating instances may incur costs.  
구성이 완료되면 복제 인스턴스를 생성할 수 있습니다. 인스턴스 생성 시 비용이 발생할 수 있습니다.  

---

## Defining Endpoints  
## 엔드포인트 정의  

After creating a replication instance, define endpoints to specify the source and target databases:  
복제 인스턴스를 생성한 후, 소스와 대상 데이터베이스를 지정하는 엔드포인트를 정의합니다.  

- **Source Endpoint:** Define where your source database is located.  
- 소스 엔드포인트: 원본 데이터베이스 위치 지정.  

- **Target Endpoint:** Define your target database location.  
- 대상 엔드포인트: 대상 데이터베이스 위치 지정.  

For databases hosted in Amazon RDS, you can select them easily through the interface. Otherwise, provide endpoint identifiers and select the appropriate database engine type.  
Amazon RDS에 호스팅된 DB는 UI를 통해 쉽게 선택 가능. 그 외는 엔드포인트 식별자를 제공하고 적절한 DB 엔진 유형 선택.  

Endpoint settings can be configured via a guided wizard or by providing JSON configurations. These settings include connection details specific to your database.  
엔드포인트 설정은 가이드 마법사 또는 JSON 구성으로 가능하며, DB 연결 정보가 포함됩니다.  

You can also test the connection from the replication instance to ensure connectivity.  
복제 인스턴스에서 연결 테스트를 수행해 연결 상태 확인 가능.  

---

## Creating Database Migration Tasks  
## 데이터베이스 마이그레이션 작업 생성  

With source and target endpoints defined, create a database migration task:  
소스 및 대상 엔드포인트 정의 후, 마이그레이션 작업을 생성합니다.  

- Select the replication instance to use.  
- 사용할 복제 인스턴스 선택.  

- Specify source and target endpoints.  
- 소스 및 대상 엔드포인트 지정.  

- Choose the migration type:  
- 마이그레이션 유형 선택:  

  - Migrate existing data only.  
  - 기존 데이터만 마이그레이션.  

  - Migrate existing data and replicate ongoing changes (continuous replication).  
  - 기존 데이터 및 실시간 변경 사항 복제(지속적 복제).  

  - Replicate data changes only.  
  - 데이터 변경 사항만 복제.  

Configure task settings either through a wizard or by providing JSON configurations. The JSON editor exposes many advanced settings for fine-tuning.  
작업 설정은 마법사 또는 JSON 구성으로 가능하며, JSON 편집기를 통해 세부 설정 조정 가능.  

Perform an assessment and finalize the configuration before creating the task.  
작업 생성 전 평가 수행 후 구성 완료.  

Note: Running migration tasks may incur costs.  
참고: 마이그레이션 작업 실행 시 비용 발생 가능.  

---

## Summary and Additional Features  
## 요약 및 추가 기능  

The typical DMS workflow involves creating a replication instance, defining endpoints, and configuring migration tasks.  
DMS 일반 워크플로우: 복제 인스턴스 생성 → 엔드포인트 정의 → 마이그레이션 작업 구성.  

AWS DMS is evolving towards serverless replication, allowing database-to-database migration without managing replication instances.  
AWS DMS는 서버리스 복제로 진화 중이며, 복제 인스턴스를 관리하지 않고도 DB 간 마이그레이션 가능.  

Additional features include schema conversion and Fleet Advisor recommendations.  
추가 기능: 스키마 변환 및 Fleet Advisor 추천.  

Homogeneous migrations can leverage native database tools for efficient data transfer.  
동일 엔진 마이그레이션은 네이티브 DB 도구를 활용해 효율적인 데이터 전송 가능.  

This overview provides sufficient understanding for exam preparation and practical use of AWS DMS.  
이 개요는 시험 준비 및 AWS DMS 실무 활용에 충분한 이해를 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Database Migration Service (DMS) offers discovery, schema conversion, and migration options.  
- AWS DMS는 발견, 스키마 변환, 마이그레이션 옵션을 제공합니다.  

- Migration types include homogeneous (same database technology) and heterogeneous (different database technologies).  
- 마이그레이션 유형: 동일 엔진(Homogeneous)과 다른 엔진(Heterogeneous).  

- Instance-based migration uses an EC2 instance managed by D
```


MS, while serverless migration requires no resource management but has engine support limitations.

* 인스턴스 기반 마이그레이션은 DMS 관리 EC2 사용, 서버리스 마이그레이션은 리소스 관리 불필요하지만 엔진 지원 제한 있음.

* DMS workflow involves creating a replication instance, defining source and target endpoints, and configuring migration tasks.

* DMS 워크플로우: 복제 인스턴스 생성 → 소스/대상 엔드포인트 정의 → 마이그레이션 작업 구성.

```
