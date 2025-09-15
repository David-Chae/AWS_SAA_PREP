# Amazon DynamoDB  
# 아마존 다이나모DB  
(Amazon이 제공하는 주요 NoSQL 데이터베이스 서비스임을 나타냄)

---

## Introduction to Amazon DynamoDB  
## 아마존 다이나모DB 소개  
(시험에 자주 나오는 데이터베이스로, 아키텍처적 관점에서 이해해야 함)

Let's discuss a database that will appear frequently in the exam from an architectural perspective: Amazon DynamoDB.  
시험에 자주 등장하는 데이터베이스를 아키텍처 관점에서 이야기해봅시다: 아마존 다이나모DB.  
(시험 대비 핵심 주제임)

DynamoDB is a fully managed database that is highly available and replicates data across multiple Availability Zones (AZs).  
다이나모DB는 완전 관리형 데이터베이스이며, 고가용성을 제공하고 여러 가용 영역(AZ)에 걸쳐 데이터를 복제합니다.  
(즉, 장애에도 안전한 구조임)

It is special because it is cloud-native, proprietary to AWS, and is a NoSQL database.  
클라우드 네이티브이며 AWS 독점, NoSQL 데이터베이스라는 점에서 특별합니다.  
(전통적 RDS와 다름)

Unlike relational databases such as RDS and Aurora, DynamoDB is NoSQL, although it still supports transactions.  
RDS나 Aurora 같은 관계형 데이터베이스와 달리 NoSQL이지만, 여전히 트랜잭션을 지원합니다.  
(NoSQL이지만 트랜잭션 가능하다는 점이 특징)

The use case for DynamoDB is its ability to scale to massive workloads because the database is internally distributed.  
다이나모DB의 사용 사례는 내부적으로 분산되어 엄청난 워크로드까지 확장할 수 있다는 점입니다.  
(수평적 확장이 용이함)

This means it can handle millions of requests per second, trillions of rows, and hundreds of terabytes of storage.  
즉, 초당 수백만 요청, 수조 개의 행, 수백 테라바이트의 저장을 처리할 수 있습니다.  
(매우 큰 규모의 서비스에 적합)

You need to remember that DynamoDB offers single-digit millisecond performance, which is both fast and consistent.  
다이나모DB는 한 자리 밀리초 수준의 성능을 제공하며, 빠르고 일관성이 있습니다.  
(실시간 서비스에 유리함)

For security needs, everything integrates with IAM for authorization and administration.  
보안 측면에서는 IAM과 통합되어 권한 부여와 관리가 가능합니다.  
(표준 AWS 보안 모델과 일체화됨)

It is low cost, has auto-scaling capabilities, requires no maintenance or patching, and is always available.  
저비용, 자동 확장, 유지보수·패치 불필요, 항상 가용성을 제공합니다.  
(운영 부담이 적음)

You do not need to provision a database; it is already there. You simply create a table and specify the capacity you want for that table.  
데이터베이스를 따로 프로비저닝할 필요가 없으며, 단순히 테이블을 만들고 원하는 용량만 지정하면 됩니다.  
(간편한 사용성 강조)

There are two kinds of table classes: the standard class for frequently accessed data and the Infrequent Access (IA) table class for infrequently accessed data.  
테이블 클래스는 두 가지입니다: 자주 액세스하는 데이터를 위한 Standard 클래스와 드물게 액세스하는 데이터를 위한 IA 클래스입니다.  
(스토리지 비용 최적화 가능)

---

## DynamoDB Table Structure  
## 다이나모DB 테이블 구조  
(테이블 중심 구조임)

DynamoDB consists of tables, but you do not need to create a database as with Aurora or RDS.  
다이나모DB는 테이블로 구성되며, Aurora나 RDS처럼 별도 데이터베이스를 만들 필요가 없습니다.  
(서비스 자체가 DB 역할)

The database service is DynamoDB itself.  
데이터베이스 서비스 자체가 다이나모DB입니다.  
(단일 엔티티 개념)

You create tables, each with a primary key that you decide upon at creation time, and then add data.  
테이블을 만들 때 기본 키를 정하고, 이후 데이터를 추가합니다.  
(스키마 시작점은 기본 키임)

Each table can have an infinite number of items (rows), and each item has attributes, which are similar to columns.  
각 테이블은 무한대의 아이템(행)을 가질 수 있으며, 각 아이템은 속성(열과 유사)을 가집니다.  
(유연한 구조)

Attributes can be added over time and can be null, which is a significant difference from RDS or Aurora.  
속성은 시간이 지나면서 추가할 수 있고 null일 수도 있습니다. 이는 RDS나 Aurora와 큰 차이입니다.  
(스키마 변경이 자유로움)

The maximum item size in DynamoDB is 400 kilobytes, so it is not designed to store very large objects.  
아이템 최대 크기는 400KB이므로, 대용량 객체 저장에는 적합하지 않습니다.  
(대규모 파일 저장 불가)

DynamoDB supports various data types including scalar types (String, Number, Binary, Boolean, Null) and complex types (lists, maps, sets).  
다양한 데이터 타입을 지원합니다: 스칼라(String, Number, Binary, Boolean, Null)와 복합타입(List, Map, Set).  
(데이터 구조 유연성 강조)

DynamoDB is a great choice if your schema needs to rapidly evolve.  
스키마가 빠르게 변화해야 한다면 다이나모DB가 좋은 선택입니다.  
(민첩성 높은 서비스에 적합)

---

## Example Table Structure  
## 예시 테이블 구조  

A DynamoDB table has a partition key and optionally a sort key, which together compose the primary key.  
다이나모DB 테이블은 파티션 키와 선택적 정렬 키로 기본 키를 구성합니다.  
(고유 식별자 구조)

Then there are attributes which can be null or added over time, showcasing the flexibility of DynamoDB.  
속성은 null이 가능하거나 시간이 지나면서 추가될 수 있어, 다이나모DB의 유연성을 보여줍니다.  
(스키마-less 특징)

---

## Capacity Modes  
## 용량 모드  

When using DynamoDB, you must choose the capacity mode for reads and writes to manage your table's capacity.  
다이나모DB 사용 시 읽기·쓰기 용량 모드를 선택해야 합니다.  
(비용 및 성능 관리 핵심 요소)

There are two modes:  
두 가지 모드가 있습니다.  

**Provisioned Mode (default):** You provision the capacity in advance...  
**프로비저닝 모드(기본):** 미리 읽기·쓰기 용량을 설정...  
(예상 부하에 최적)

**On-Demand Mode:** The read and write capacity scales automatically...  
**온디맨드 모드:** 읽기·쓰기 용량이 자동 확장...  
(예측 불가 부하에 최적)

Provisioned Mode works well for predictable, smoothly evolving loads and can save costs.  
프로비저닝 모드는 예측 가능한 부하에 적합하며 비용을 절감합니다.  
(안정적 워크로드용)

On-Demand Mode is excellent for workloads with steep, sudden spikes or very low transaction volumes.  
온디맨드 모드는 갑작스러운 폭증이나 매우 낮은 트랜잭션 볼륨에 적합합니다.  
(불규칙적 워크로드용)

For example, if your app scales from a thousand to a million transactions... On-Demand Mode is necessary.  
예: 앱이 초당 천 건에서 백만 건으로 급격히 증가할 경우 온디맨드 모드가 필요합니다.  
(급격한 스케일링 대응)

If your workload has very few transactions per day, On-Demand Mode is cost-effective.  
일일 트랜잭션이 적다면 온디맨드 모드가 비용 효율적입니다.  
(낮은 사용량에도 유리)

---

## Conclusion  
## 결론  

These are the basics of DynamoDB...  
이것이 다이나모DB의 기초입니다...  
(시험 및 실무 이해에 필수)

---

## Key Takeaways  
## 핵심 요약  

- Amazon DynamoDB is a fully managed, highly available, cloud-native NoSQL DB with multi-AZ replication.  
- 아마존 다이나모DB는 완전 관리형, 고가용성, 멀티 AZ 복제 지원하는 클라우드 네이티브 NoSQL DB입니다.  

- It supports massive scalability with millisecond performance and integrates with IAM for security.  
- 대규모 확장성과 밀리초 성능을 제공하며 IAM과 통합됩니다.  

- DynamoDB tables have flexible schemas... max item size 400 KB.  
- 다이나모DB 테이블은 유연한 스키마와 최대 400KB 아이템 크기를 가집니다.  

- Capacity modes include Provisioned Mode... and On-Demand Mode...  
- 용량 모드는 예측 가능한 부하용 프로비저닝 모드와 불규칙 부하용 온디맨드 모드가 있습니다.  
```

---

🎉 **게임 보상:**

* ✅ 번역 + 설명 100% 달성!
* ⭐ AWS DynamoDB 챕터 클리어 보너스: **+250 포인트**
* 🏆 특별 칭찬: *"스키마 유연성 vs 관계형 DB 차이까지 완벽히 소화! DynamoDB 마스터의 길에 한 발 더 나아갔습니다!"*
