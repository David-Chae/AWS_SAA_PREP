```md
# DynamoDB
# 다이나모DB
# → AWS의 서버리스 NoSQL 데이터베이스 개념과 특징 정리

## Overview of Amazon DynamoDB
## 아마존 다이나모DB 개요
## → DynamoDB 기본 소개

Amazon DynamoDB is a proprietary technology from AWS.  
Amazon DynamoDB는 AWS 고유 기술입니다.  
→ AWS 전용 서버리스 데이터베이스.

It is a managed, serverless, NoSQL database that provides millisecond latency out of the box.  
관리형 서버리스 NoSQL 데이터베이스로, 기본적으로 밀리초 단위 지연 시간을 제공합니다.  
→ 빠른 데이터 접근 가능.
```

🎖️ **게임보상: DynamoDB 입문자 레벨업!**

---

```md
## Capacity Modes
## 용량 모드
## → DynamoDB의 확장 및 처리 모드

DynamoDB offers two capacity modes to choose from:  
DynamoDB는 선택 가능한 두 가지 용량 모드를 제공합니다.  
→ 애플리케이션 요구에 맞는 모드 선택 가능.

- Provisioned Capacity with optional auto scaling, which is ideal when you have a smooth workload that increases or decreases gradually over time.  
- Provisioned Capacity(자동 스케일링 선택 가능): 부하가 점진적으로 증가/감소하는 경우 이상적  
→ 예측 가능한 워크로드 최적화.

- On-Demand Capacity Mode, where you do not have to provision capacity. It scales automatically, making it suitable for unpredictable workloads or sudden steep spikes of demand on your database.  
- On-Demand Capacity: 용량 프로비저닝 불필요, 자동 확장, 예측 불가 부하나 급격한 트래픽에 적합  
→ 서버 관리 부담 최소화.
```

🎖️ **게임보상: DynamoDB 용량 마스터 레벨업!**

---

```md
## Use Cases and Features
## 사용 사례와 특징
## → DynamoDB 활용과 기능

DynamoDB can replace ElasticCache as a key-value store.  
DynamoDB는 키-값 저장소로 ElasticCache를 대체할 수 있습니다.  
→ 분산 캐시 용도로 활용 가능.

For example, it is a great way to store session data for your website, combined with a TTL feature to expire a row after a specific amount of time.  
예를 들어, TTL 기능을 사용해 일정 시간 후 데이터가 만료되도록 하여 웹사이트 세션 데이터를 저장할 수 있습니다.  
→ 세션 관리 최적화.
```

🎖️ **게임보상: DynamoDB 기능 숙련자 레벨업!**

---

```md
## Availability and Transactions
## 가용성과 트랜잭션
## → DynamoDB 안정성과 데이터 처리

DynamoDB is highly available across multiple availability zones by default.  
DynamoDB는 기본적으로 여러 가용 영역에서 높은 가용성을 제공합니다.  
→ 장애 대비 내구성 확보.

Reads and writes are fully decoupled, and it supports transactions on top of DynamoDB tables.  
읽기와 쓰기가 완전히 분리되며, 테이블 단위 트랜잭션을 지원합니다.  
→ 트랜잭션 관리 가능.
```

🎖️ **게임보상: DynamoDB 안정성 마스터 레벨업!**

---

```md
## DynamoDB Accelerator (DAX)
## 다이나모DB 가속기(DAX)
## → 마이크로초 읽기 성능 제공

You can create a read cache out of the box that is fully compatible with DynamoDB, called a DAX cluster (DynamoDB Accelerator).  
DAX 클러스터(DynamoDB Accelerator)로 DynamoDB 호환 읽기 캐시를 바로 생성할 수 있습니다.  
→ 읽기 성능 극대화.

The particularity of DAX is that it provides microsecond read latency.  
DAX의 특징은 마이크로초 단위 읽기 지연 시간을 제공한다는 점입니다.  
→ 초고속 읽기.
```

🎖️ **게임보상: DynamoDB 초고속 캐시 전문가 레벨업!**

---

```md
## Security, Authentication, and Authorization
## 보안, 인증, 권한 관리
## → IAM 기반 통합 관리

All security, authentication, and authorization are managed through IAM (Identity and Access Management).  
보안, 인증, 권한 관리는 모두 IAM(Identity and Access Management)을 통해 관리됩니다.  
→ 안전한 접근 관리.
```

🎖️ **게임보상: 보안 전문가 레벨업!**

---

```md
## Event Processing with DynamoDB Streams
## 다이나모DB 스트림을 활용한 이벤트 처리
## → 실시간 이벤트 처리

DynamoDB supports event processing capabilities through DynamoDB Streams, which stream all changes happening in your database.  
DynamoDB는 DynamoDB Streams를 통해 데이터베이스에서 발생하는 모든 변경 사항을 스트리밍할 수 있습니다.  
→ 실시간 변경 감지 가능.

You can integrate this with AWS Lambda, allowing Lambda to be invoked for every single change in your DynamoDB table.  
AWS Lambda와 통합 가능하며, 테이블 내 모든 변경 시 Lambda가 호출됩니다.  
→ 이벤트 기반 서버리스 처리.
```

🎖️ **게임보상: 이벤트 처리 마스터 레벨업!**

---

```md
## Integration with Kinesis Data Streams
## Kinesis 데이터 스트림과 통합
## → 장기 이벤트 처리 및 분석

Alternatively, instead of sending data to DynamoDB Streams, you can send data to Kinesis Data Streams.  
DynamoDB Streams 대신 Kinesis Data Streams로 데이터를 전송할 수도 있습니다.  
→ 유연한 이벤트 처리.

This allows you to use features like Kinesis Data Firehose or any integration leveraging Kinesis Data Streams.  
이를 통해 Kinesis Data Firehose 등 스트림 기반 다양한 기능 활용 가능  
→ 데이터 분석/보관 최적화.

For example, Kinesis Data Streams supports longer-term retention of up to one year.  
예를 들어, Kinesis Data Streams는 최대 1년간 장기 보관을 지원합니다.  
→ 장기 데이터 유지 가능.
```

🎖️ **게임보상: 이벤트/분석 전문가 레벨업!**

---

```md
## Global Tables
## 글로벌 테이블
## → 다중 리전 활성-활성 복제

DynamoDB offers a global table feature that allows active-active replication across multiple regions.  
DynamoDB는 다중 리전 간 활성-활성 복제를 지원하는 글로벌 테이블 기능을 제공합니다.  
→ 멀티 리전 동기화 가능.

This means anyone can read and write from any region, enabling true multi-region active-active database operations.  
즉, 어느 리전에서도 읽기/쓰기 가능하여 진정한 다중 리전 활성-활성 DB 운영 가능  
→ 고가용성 글로벌 운영.
```

🎖️ **게임보상: 글로벌 DB 전문가 레벨업!**

---

```md
## Backup Options
## 백업 옵션
## → 데이터 보호 및 복원

There are two backup options:  
백업 옵션은 두 가지가 있습니다.  

- Automated Backup: Enable point-in-time recovery to restore your table to any point within the last 35 days.  
- 자동 백업: 최근 35일 내 원하는 시점으로 복원 가능  
→ 포인트인타임 복원.

- On-Demand Backups: For longer-term retention, you can enable on-demand backups, which also restore to a new DynamoDB table.  
- 온디맨드 백업: 장기 보존 시 활용 가능, 새로운 테이블로 복원 가능  
→ 장기 데이터 보호.
```

🎖️ **게임보상: 백업/복원 전문가 레벨업!**

---

```md
## Export and Import Features
## 내보내기 및 가져오기 기능
## → S3 연동으로 데이터 이동 최적화

You can export your DynamoDB table to Amazon S3 without consuming any read capacity units within the point-in-time recovery window (up to 35 days).  
포인트인타임 복원 윈도우(최대 35일) 내 읽기 용량 소비 없이 DynamoDB 테이블을 S3로 내보낼 수 있습니다.  
→ 비용 효율적 데이터 이동.

Similarly, you can import data from S3 into a new table without using any write capacity units.  
마찬가지로 S3에서 새로운 테이블로 데이터를 가져올 때 쓰기 용량을 사용하지 않습니다.  
→ 비용 효율적 데이터 가져오기.
```

🎖️ **게임보상: 데이터 이동 마스터 레벨업!**

---

```md
## Use Cases Summary
## 사용 사례 요약
## → 시험 및 실무 포인트

From an exam perspective, DynamoDB is a great choice when you need to rapidly evolve schema with a flexible database schema.  
시험 관점에서, 유연한 스키마로 빠르게 진화하는 데이터베이스가 필요할 때 DynamoDB가 적합합니다.  
→ 서버리스 애플리케이션 최적화.

It is suitable for serverless application development when your data consists of small documents, typically in the hundreds of kilobytes maximum, or when you want a distributed serverless cache.  
데이터가 소규모 문서(수백 KB)로 구성되거나 분산 서버리스 캐시가 필요할 때 적합합니다.  
→ 서버리스 개발용 이상적.
```

🎖️ **게임보상: 서버리스 DB 전문가 레벨업!**

---

```md
## Key Takeaways
## 핵심 요약
## → 시험/실무 필수 포인트

- Amazon DynamoDB is a managed, serverless, NoSQL database offering millisecond latency.  
- Amazon DynamoDB는 밀리초 단위 지연 시간 제공, 서버리스 관리형 NoSQL DB입니다.  
→ 빠른 서버리스 DB.

- It offers two capacity modes: provisioned capacity with optional auto scaling, and on-demand capacity for unpredictable workloads.  
- Provisioned 및 On-Demand 모드 지원, 워크로드 특성에 맞게 선택 가능  
→ 유연한 확장.

- DynamoDB supports high availability across multiple availability zones and provides features like transactions, TTL for expiring data, and DAX for microsecond read latency.  
- 다중 AZ 고가용성, 트랜잭션, TTL, DAX 지원  
```


→ 안정성과 성능 확보.

* Integration with AWS services includes IAM for security, DynamoDB Streams for event processing with Lambda, and Kinesis Data Streams for extended data retention and processing.

* AWS 서비스 통합: IAM, DynamoDB Streams+Lambda, Kinesis Data Streams
  → 이벤트 처리 및 장기 보관 최적화.

* Global tables enable active-active replication across multiple regions.

* 글로벌 테이블: 다중 리전 활성-활성 복제 지원
  → 글로벌 고가용성.

* Backup options include point-in-time recovery for up to 35 days and on-demand backups for longer retention.

* 백업 옵션: 포인트인타임 복원(최대 35일), 온디맨드 백업(장기)
  → 데이터 보호.

* DynamoDB supports exporting and importing tables to and from Amazon S3 without consuming read capacity units.

* S3 연동 내보내기/가져오기 지원, 용량 소비 없음
  → 비용 효율적 데이터 이동.

* It is ideal for serverless applications requiring flexible schema and small document storage or as a distributed serverless cache.

* 서버리스 애플리케이션, 유연 스키마, 소규모 문서 저장 또는 분산 캐시용 적합
  → 서버리스 개발 최적화.

```

🎖️ **게임보상: DynamoDB 마스터 → AWS 서버리스 DB 챔피언 🏆🎮**
