```md
# Amazon Timestream
# 아마존 타임스트림
# → AWS에서 제공하는 시계열(Time Series) 데이터베이스

## Introduction to Amazon Timestream
## Amazon Timestream 소개
## → 타임스트림 기본 개념

Amazon Timestream is a time series database.  
Amazon Timestream은 시계열 데이터베이스입니다.  
→ 시간 기반 데이터를 전문적으로 다루는 DB.

It is fully managed, fast, scalable, and serverless.  
완전 관리형, 빠르고, 확장 가능하며 서버리스입니다.  
→ 관리 부담 최소화, 서버리스 환경 강조.

## What is a Time Series?
## 시계열이란?
## → 시험 포인트

A time series is a collection of points that include a time component.  
시계열은 시간 구성 요소를 포함하는 데이터 점들의 모음입니다.  
→ 시간 순서 기반 데이터 이해.

For example, a graph by year represents a time series.  
예를 들어, 연도별 그래프는 시계열 데이터를 나타냅니다.  
→ 시계열 데이터 예시.

## Features of Amazon Timestream
## Amazon Timestream 특징
## → 시험 대비 기능 정리

Automatically adjusts the database capacity up and down to scale.  
데이터베이스 용량을 자동으로 확장/축소합니다.  
→ 서버리스 자동 스케일링 강조.

Can store and analyze trillions of events per day.  
하루에 수조 건의 이벤트를 저장하고 분석할 수 있습니다.  
→ 고성능 및 대용량 처리 시험 포인트.

Designed to be faster and more cost-effective than relational databases for time series data.  
시계열 데이터에서는 관계형 데이터베이스보다 빠르고 비용 효율적으로 설계되었습니다.  
→ 타임스트림 장점 강조.

## Capabilities
## 기능
## → 실무/시험 핵심

Supports scheduled queries.  
스케줄링된 쿼리를 지원합니다.  
→ 정기 분석 가능.

Allows records with multiple measures.  
여러 측정값을 가진 레코드를 허용합니다.  
→ 복합 데이터 저장 가능.

Provides full SQL compatibility.  
완전한 SQL 호환성을 제공합니다.  
→ 기존 SQL 지식 활용 가능.

Recent data is kept in memory for fast access.  
최근 데이터는 메모리에 유지되어 빠른 접근이 가능합니다.  
→ 실시간 분석 최적화.

Historical data is stored in a cost-optimized storage tier.  
과거 데이터는 비용 최적화 스토리지 계층에 저장됩니다.  
→ 비용 효율적 장기 저장.

Includes time series analytics functions to analyze data and find patterns in near real time.  
시계열 분석 기능을 제공하여 데이터를 분석하고 실시간에 가까운 패턴을 발견할 수 있습니다.  
→ 실시간 데이터 분석 기능 시험 포인트.

## Security
## 보안
## → 시험 대비

Amazon Timestream supports encryption both in transit and at rest, consistent with other AWS databases.  
Amazon Timestream은 전송 중 및 저장 시 암호화를 지원합니다.  
→ AWS DB 공통 보안 기능.

## Use Cases
## 사용 사례
## → 시험/실무 연관

Amazon Timestream is suitable for:  
Amazon Timestream은 다음과 같은 용도에 적합합니다.  
→ IoT, 실시간 분석 강조

- Internet of Things (IoT) applications.  
- IoT 애플리케이션  
→ IoT 센서 데이터 저장.

- Operational applications.  
- 운영 애플리케이션  
→ 운영 모니터링.

- Real-time analytics.  
- 실시간 분석  
→ 빠른 패턴 탐지.

- Any application involving time series data.  
- 시계열 데이터를 사용하는 모든 애플리케이션  
→ 일반적인 시계열 DB 활용.

## Architecture and Integrations
## 아키텍처 및 통합
## → 시험 대비 AWS 통합

Amazon Timestream can receive data from various sources:  
Amazon Timestream은 다양한 소스로부터 데이터를 받을 수 있습니다.  

- AWS IoT (Internet of Things).  
- AWS IoT (사물인터넷)  

- Kinesis Data Streams via AWS Lambda.  
- AWS Lambda를 통한 Kinesis Data Streams  

- Prometheus and Telegraf integrations.  
- Prometheus 및 Telegraf 통합  

- Kinesis Data Analytics for Apache Flink.  
- Apache Flink용 Kinesis Data Analytics  

- Amazon MSK (Managed Streaming for Apache Kafka).  
- Amazon MSK (Managed Streaming for Apache Kafka)  

It can connect to and be used by:  
다음과 연결하여 사용할 수 있습니다.  

- Amazon QuickSight for building dashboards.  
- 대시보드 생성을 위한 Amazon QuickSight  

- Amazon SageMaker for machine learning.  
- 기계학습을 위한 Amazon SageMaker  

- Grafana.  
- Grafana  

- Any application compatible with JDBC and SQL, due to its standard JDBC connection.  
- 표준 JDBC 연결 덕분에 JDBC/SQL 호환 애플리케이션  

## Summary
## 요약
## → 시험 포인트: 정의 및 장점

For exam purposes, it is important to remember what Amazon Timestream is at a high level.  
시험 관점에서 Amazon Timestream의 높은 수준 정의를 기억하는 것이 중요합니다.  

It is a specialized time series database designed for speed, scalability, and cost-effectiveness, with broad integration capabilities within the AWS ecosystem.  
속도, 확장성, 비용 효율성을 위해 설계된 시계열 전문 DB로, AWS 생태계와 폭넓게 통합 가능합니다.  

## Key Takeaways
## 핵심 요약
## → 시험/실무 핵심

Amazon Timestream is a fully managed, fast, scalable, and serverless time series database.  
Amazon Timestream은 완전 관리형, 빠르고, 확장 가능하며 서버리스 시계열 DB입니다.  

It automatically scales capacity and can store and analyze trillions of events per day.  
자동으로 용량을 조정하며 하루 수조 건의 이벤트를 저장하고 분석할 수 있습니다.  

Timestream offers full SQL compatibility, scheduled queries, and time series analytics functions.  
SQL 호환성, 스케줄링 쿼리, 시계열 분석 기능을 제공합니다.  

It integrates with various AWS services and supports encryption in transit and at rest.  
다양한 AWS 서비스와 통합되며, 전송 중 및 저장 시 암호화를 지원합니다.  
```

🎮 **게임보상: Timestream 마스터! ⏱️**
→ 시험 대비: IoT, 실시간 분석, 시계열 DB 자신감 상승!
