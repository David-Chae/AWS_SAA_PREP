# Amazon DynamoDB - Advanced Features
# Amazon DynamoDB - 고급 기능
> DynamoDB의 시험 대비 고급 기능들을 실습 중심으로 다룹니다.

## Advanced Features of Amazon DynamoDB
## Amazon DynamoDB의 고급 기능
> 성능 향상, 실시간 처리, 글로벌 복제, 데이터 수명 관리 등 중요한 기능들을 설명합니다.

In this lecture, we will discuss advanced features of Amazon DynamoDB that are important for the exam. These features enhance performance, enable real-time processing, support global replication, and provide data lifecycle management.
이번 강의에서는 시험에서 중요한 Amazon DynamoDB의 고급 기능을 다룹니다. 이 기능들은 성능을 향상시키고, 실시간 처리를 가능하게 하며, 글로벌 복제를 지원하고, 데이터 수명 관리를 제공합니다.
> 핵심: 시험 포인트 + 실무 활용

## DynamoDB Accelerator (DAX)
## DynamoDB 가속기 (DAX)
> 메모리 캐시를 이용해 읽기 성능을 극대화합니다.

DynamoDB Accelerator, or DAX, is a fully-managed, highly available, and seamless in-memory cache for DynamoDB. It is designed to alleviate read congestion on your DynamoDB tables by caching data, thereby providing microsecond latency for cached reads.
DynamoDB Accelerator(DAX)는 완전관리형, 고가용성, 원활한 메모리 캐시로 DynamoDB 테이블의 읽기 병목을 줄이고, 캐시된 읽기에 마이크로초 수준의 지연을 제공합니다.
> 핵심: 읽기 성능 극대화

One key advantage of DAX is that it does not require any changes to your application logic because the DAX cluster is compatible with existing DynamoDB APIs. You create a DAX cluster composed of several cache nodes and connect your application to this cluster. Behind the scenes, the DAX cluster connects to your DynamoDB table.
DAX의 주요 장점은 기존 DynamoDB API와 호환되므로 애플리케이션 로직 변경이 필요 없다는 점입니다. 여러 캐시 노드로 구성된 DAX 클러스터를 만들고, 애플리케이션을 연결하면 클러스터가 내부적으로 DynamoDB 테이블에 연결됩니다.
> 핵심: 애플리케이션 수정 없이 캐싱 가능

The cache has a default time-to-live (TTL) of five minutes, which can be adjusted as needed.
캐시의 기본 TTL(Time-to-Live)은 5분이며, 필요에 따라 조정할 수 있습니다.
> 핵심: 캐시 수명 조정 가능

It is important to note that DAX and Amazon ElastiCache serve complementary purposes. DAX is optimized for caching individual objects or query results from DynamoDB, while ElastiCache is better suited for storing aggregation results or large computations performed on DynamoDB data.
DAX와 Amazon ElastiCache는 보완적인 목적을 가지고 있습니다. DAX는 DynamoDB의 개별 객체나 쿼리 결과 캐싱에 최적화되어 있으며, ElastiCache는 집계 결과나 대규모 계산 결과 저장에 더 적합합니다.
> 핵심: 용도별 캐시 선택 이해

## Stream Processing with DynamoDB
## DynamoDB 스트림 처리
> 테이블 변경 사항을 실시간으로 처리합니다.

DynamoDB supports stream processing by capturing a stream of all modifications—creates, updates, and deletes—on your tables. This feature enables real-time reactions to changes, such as sending welcome emails when new users are added, performing usage analytics, inserting data into derivative tables, implementing cross-region replication, or invoking AWS Lambda functions on table changes.
DynamoDB는 테이블의 모든 변경 사항(생성, 수정, 삭제)을 캡처하여 스트림 처리 기능을 지원합니다. 이를 통해 신규 사용자 환영 이메일 전송, 사용 분석, 파생 테이블 데이터 삽입, 지역 간 복제, Lambda 함수 호출 등 실시간 반응이 가능합니다.
> 핵심: 실시간 이벤트 처리

There are two main options for stream processing:
스트림 처리에는 두 가지 주요 옵션이 있습니다:
> 핵심: 선택지 이해

DynamoDB Streams: Offers 24-hour retention, supports a limited number of consumers, and integrates well with Lambda triggers.
DynamoDB Streams: 24시간 데이터 보존, 제한된 소비자 지원, Lambda 트리거와 잘 통합됨.
> 핵심: 단기간 실시간 처리

Kinesis Data Streams: Provides up to one year of retention, supports a higher number of consumers, and offers extensive processing options including Lambda functions, Kinesis Data Analytics, Kinesis Data Firehose, and AWS Glue streaming ETLs.
Kinesis Data Streams: 최대 1년 데이터 보존, 더 많은 소비자 지원, Lambda, Kinesis Data Analytics, Kinesis Data Firehose, AWS Glue 스트리밍 ETL 등 다양한 처리 옵션 제공.
> 핵심: 장기 보관 + 확장 처리

## Architectural Overview of DynamoDB Streams
## DynamoDB 스트림 아키텍처 개요
> 스트림 처리 구조와 데이터 흐름 이해

Your application performs create, update, and delete operations on a DynamoDB table. These changes are captured either by DynamoDB Streams or Kinesis Data Streams.
애플리케이션이 DynamoDB 테이블에 생성, 수정, 삭제 작업을 수행하면, 이 변경 사항은 DynamoDB Streams 또는 Kinesis Data Streams에 의해 캡처됩니다.
> 핵심: 데이터 흐름 이해

If using Kinesis Data Streams, you can leverage Kinesis Data Firehose to deliver data to destinations such as Amazon Redshift for analytics, Amazon S3 for archiving, or Amazon OpenSearch for indexing and search.
Kinesis Data Streams를 사용하면 Kinesis Data Firehose를 통해 데이터를 Amazon Redshift(분석), Amazon S3(아카이빙), Amazon OpenSearch(인덱싱/검색) 등으로 전달할 수 있습니다.
> 핵심: 스트림 -> 분석/저장 연계

With DynamoDB Streams, a processing layer can consume the stream using the DynamoDB Kinesis Client Library (KCL) Adapter, running on EC2 instances or Lambda functions. This layer can perform notifications via Amazon SNS, filter and transform data into another DynamoDB table, or send data to Amazon OpenSearch.
DynamoDB Streams를 사용하면 처리 계층이 KCL(Adapter)을 이용해 스트림을 소비하고, EC2 또는 Lambda에서 실행할 수 있습니다. 이를 통해 SNS 알림, 데이터 필터링/변환, 다른 DynamoDB 테이블로 전송, OpenSearch로 전송 등이 가능합니다.
> 핵심: 실시간 데이터 처리 응용

Additional processing options include EC2 instances reading from Kinesis Data Streams and using Kinesis Data Analytics for complex transformations.
추가 옵션으로 EC2에서 Kinesis Data Streams를 읽고 Kinesis Data Analytics로 복잡한 변환을 수행할 수 있습니다.
> 핵심: 고급 데이터 변환

## Global Tables
## 글로벌 테이블
> 다중 리전 복제를 통한 낮은 지연 읽기/쓰기

DynamoDB global tables replicate data across multiple AWS regions, such as US-East-1 and AP-Southeast-2. This replication is two-way, allowing applications to read and write to the table in any region with low latency.
DynamoDB 글로벌 테이블은 US-East-1, AP-Southeast-2 등 여러 AWS 리전에 데이터를 복제합니다. 양방향 복제를 통해 어떤 리전에서도 저지연 읽기/쓰기가 가능합니다.
> 핵심: 글로벌 애플리케이션 지원

Global tables use active-active replication, and enabling them requires activating DynamoDB Streams, which serve as the underlying infrastructure for cross-region replication.
글로벌 테이블은 액티브-액티브 복제를 사용하며, 활성화하려면 DynamoDB Streams를 활성화해야 합니다. 스트림이 리전 간 복제의 기반이 됩니다.
> 핵심: 활성화 조건 이해

## Time To Live (TTL)
## TTL(Time To Live)
> 지정된 시간 후 항목 자동 삭제

TTL is a feature that automatically deletes items from a DynamoDB table after a specified expiry timestamp. For example, a table named SessionData might include an attribute ExpTime containing the TTL timestamp.
TTL은 지정된 만료 시간 이후 DynamoDB 테이블 항목을 자동으로 삭제하는 기능입니다. 예: `SessionData` 테이블에 `ExpTime` 속성으로 TTL 타임스탬프를 지정.
> 핵심: 데이터 수명 자동 관리

When the current epoch time exceeds the ExpTime value, the item expires and is deleted through a background process.
현재 시간(epoch)이 `ExpTime`를 초과하면 항목이 만료되어 백그라운드 프로세스로 삭제됩니다.
> 핵심: 자동 삭제 메커니즘 이해

Use cases for TTL include:
TTL 사용 사례:
> 핵심: 활용 예시

- Retaining only the most current items in a table.
- 테이블에 최신 항목만 유지
- Complying with regulatory requirements by deleting data after a certain period, such as two years.
- 법규 준수를 위해 일정 기간(예: 2년) 후 데이터 삭제
- Managing web sessions by storing session data centrally for a limited time, such as two hours, after which the session expires if not renewed.
- 웹 세션 관리: 세션 데이터를 제한 시간(예: 2시간) 동안 중앙 저장 후 만료

## Backup and Disaster Recovery
## 백업 및 재해 복구
> 안정적인 데이터 보호 및 복원

DynamoDB offers multiple backup options:
DynamoDB는 여러 백업 옵션을 제공합니다.
> 핵심: 데이터 보호

Continuous Backups with Point-in-Time Recovery (PITR): Optionally enabled to retain backups for the last 35 days. PITR allows recovery to any point within this window and creates a new table upon recovery.
PITR: 선택적으로 활성화하여 최근 35일간 백업 유지. 원하는 시점으로 복원 가능하며, 복원 시 새 테이블 생성.
> 핵심: 시점 복원

On-Demand Backups: Retained until explicitly deleted, suitable for long-term backups.
온디맨드 백업: 명시적으로 삭제할 때까지 유지, 장기 백업에 적합.
> 핵심: 필요 시 수동 백업

These backup operations do not affect the performance or latency of your DynamoDB tables.
백업 작업은 DynamoDB 테이블 성능이나 지연에 영향을 주지 않습니다.
> 핵심: 성능 유지

For enhanced backup management, you can use the AWS Backup Service, which supports lifecycle policies and cross-region backup copying for disaster recovery. Recoveries from these backups also create new tables.
강화된 백업 관리: AWS Backup Service 사용 가능, 라이프사이클 정책 및 리전 간 백업 복사 지원. 복원 시 새 테이블 생성.
> 핵심: 백업 자동화 + 재해 복구

## Integration Between DynamoDB and Amazon S3
## DynamoDB와 Amazon S3 통합
> 데이터 이동 및 분석 지원

You can export DynamoDB tables to Amazon S3 by enabling point-in-time recovery and exporting data within the last 35 days. This export does not impact the read capacity or performance of the DynamoDB table.
PITR을 활성화하면 최근 35일간 데이터를 Amazon S3로 내보낼 수 있습니다. 이 작업은 읽기 용량이나 성능에 영향을 주지 않습니다.
> 핵심: S3로 안전하게 데이터 이동

Exported data can be analyzed using Amazon Athena or retained for auditing and big data transformations. The export format can be DynamoDB JSON or the ION format.
내보낸 데이터는 Amazon Athena로 분석하거나 감사, 빅데이터 변환용으로 보관 가능. 형식: DynamoDB JSON 또는 ION.
> 핵심: 분석/감사 활용

Similarly, you can import data from Amazon S3 into a new DynamoDB table using CSV, JSON, or ION formats. This import does not consume write capacity and creates a new table. Any import errors are logged in Amazon CloudWatch Logs.
마찬가지로 Amazon S3 데이터를 CSV, JSON, ION 형식으로 새로운 DynamoDB 테이블로 가져올 수 있습니다. 쓰기 용량을 사용하지 않으며, 오류는 CloudWatch Logs에 기록됩니다.
> 핵심: 데이터 복원 및 신규 테이블 생성

This concludes our overview of advanced features in Amazon DynamoDB. These features provide powerful tools for caching, stream processing, global replication, data lifecycle management, backup, and integration with other AWS services.
이상으로 DynamoDB 고급 기능 개요를 마칩니다. 캐싱, 스트림 처리, 글로벌 복제, 데이터 수명 관리, 백업, AWS 서비스 통합 기능을 제공하는 강력한 도구들입니다.
> 핵심: 강의 마무리

## Key Takeaways
## 핵심 요약
DynamoDB Accelerator (DAX) is a fully-managed, highly available, in-memory cache for DynamoDB that provides microsecond latency for cached data without requiring application logic changes.
DAX: 완전관리형, 고가용성 메모리 캐시, 애플리케이션 수정 없이 마이크로초 지연 제공
DynamoDB Streams enable real-time processing of table modifications with integration options including Lambda triggers and Kinesis Data Streams for extended retention and processing capabilities.
DynamoDB Streams: 실시간 테이블 변경 처리, Lambda 트리거 및 Kinesis Data Streams 통합 가능
Global tables provide active-active replication across multiple AWS regions, allowing low-latency reads and writes globally, relying on DynamoDB Streams for replication.
글로벌 테이블: 여러 리전 액티브-액티브 복제, 낮은 지연 읽기/쓰기 가능, DynamoDB Streams 기반
Time To Live (TTL) automatically deletes expired items based on a timestamp attribute, useful for session management and regulatory compliance.
TTL: 만료 항목 자동 삭제, 세션 관리 및 규제 준수에 유용
DynamoDB supports continuous backups with point-in-time recovery and on-demand backups, which do not impact table performance.
DynamoDB 백업: PITR 및 온디맨드 백업 지원, 성능 영향 없음
Integration with Amazon S3 allows exporting and importing DynamoDB tables for analytics, auditing, and ETL processes without affecting table capacity.
Amazon S3 통합: 테이블 용량 영향 없이 데이터 내보내기/가져오기 가능, 분석/감사/ETL 활용

```


🎮 **게임 보상 포인트:**

* DAX 이해 + 적용 = 15 XP
* 스트림 처리 구조 및 Kinesis 이해 = 20 XP
* 글로벌 테이블 + TTL 활용 = 15 XP
* 백업 & S3 통합 이해 = 20 XP

총: **70 XP**
