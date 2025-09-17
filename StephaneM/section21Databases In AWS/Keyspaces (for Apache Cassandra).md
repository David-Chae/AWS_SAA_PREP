```md
# Keyspaces (for Apache Cassandra)
# Keyspaces (Apache Cassandra용)
# → AWS에서 제공하는 Cassandra 관리형 서비스

## Introduction to Amazon Keyspaces
## Amazon Keyspaces 소개
## → Keyspaces 기본 개념

Amazon Keyspaces is a managed Apache Cassandra service provided by AWS.  
Amazon Keyspaces는 AWS에서 제공하는 관리형 Apache Cassandra 서비스입니다.  
→ Cassandra를 AWS 클라우드에서 바로 사용 가능.

Cassandra is an open-source NoSQL distributed database.  
Cassandra는 오픈소스 NoSQL 분산 데이터베이스입니다.  
→ 시험 포인트: Cassandra = 분산형 NoSQL.

With Amazon Keyspaces, you get Cassandra directly managed on the cloud by AWS.  
Amazon Keyspaces를 사용하면 Cassandra가 AWS 클라우드에서 직접 관리됩니다.  
→ 서버 관리 필요 없음, 완전 관리형 서비스.

Amazon Keyspaces is a serverless service that is scalable, highly available, and fully managed by AWS.  
Amazon Keyspaces는 서버리스 서비스로, 확장 가능하고, 고가용성이며 AWS가 완전히 관리합니다.  
→ 확장성과 안정성 시험 포인트.

It automatically scales tables up and down based on the application's traffic.  
애플리케이션 트래픽에 따라 테이블을 자동으로 확장하거나 축소합니다.  
→ 자동 스케일링 기능 강조.

The data in tables is replicated three times across multiple Availability Zones (AZs) to ensure durability and availability.  
테이블의 데이터는 내구성과 가용성을 위해 여러 가용 영역(AZ)에 걸쳐 세 번 복제됩니다.  
→ 고가용성 및 내구성 확보.

To perform queries on Amazon Keyspaces, you use the Cassandra Query Language (CQL).  
Amazon Keyspaces에서 쿼리를 수행하려면 Cassandra Query Language(CQL)를 사용합니다.  
→ 익숙한 Cassandra 문법 사용 가능.

This allows you to interact with the database using familiar Cassandra syntax.  
이를 통해 친숙한 Cassandra 구문으로 데이터베이스와 상호작용할 수 있습니다.  
→ 개발자 친화적 인터페이스 강조.

Thanks to this architecture, Amazon Keyspaces provides single-digit millisecond latency at any scale and can handle thousands of requests per second.  
이 구조 덕분에 Amazon Keyspaces는 어떤 규모에서도 단일 숫자 밀리초 지연을 제공하며 초당 수천 건의 요청을 처리할 수 있습니다.  
→ 성능 시험 포인트: 고속 읽기/쓰기.

## Capacity Modes
## 용량 모드
## → DynamoDB와 유사한 확장 옵션

Amazon Keyspaces offers two capacity modes, similar to DynamoDB:  
Amazon Keyspaces는 DynamoDB와 유사하게 두 가지 용량 모드를 제공합니다.  
→ 시험 대비: 용량 모드 연관 기억.

- On-demand mode  
- 온디맨드 모드  
→ 수요 기반 자동 확장, 트래픽 불규칙한 경우 적합.

- Provisioned mode with auto-scaling  
- 자동 스케일링이 가능한 프로비저닝 모드  
→ 트래픽이 예측 가능한 경우 적합.

These modes allow you to choose how you want to manage capacity and scaling based on your application's needs.  
이 모드를 통해 애플리케이션 요구 사항에 따라 용량과 스케일링을 관리할 수 있습니다.  
→ 확장 전략 선택 중요.

## Security and Data Protection Features
## 보안 및 데이터 보호 기능
## → 시험 포인트: 암호화, 백업, 복구

Amazon Keyspaces provides encryption features to secure your data.  
Amazon Keyspaces는 데이터를 보호하기 위해 암호화 기능을 제공합니다.  
→ 암호화 필수 포인트.

It also supports backup and Point-In-Time Recovery (PITR) for up to 35 days.  
또한 최대 35일 동안 백업과 시점 복구(Point-In-Time Recovery, PITR)를 지원합니다.  
→ 시험 포인트: PITR 35일.

## Use Cases
## 사용 사례
## → 시험 대비 연관 기억

Common use cases for Amazon Keyspaces include storing IoT device information and time-series data.  
Amazon Keyspaces의 일반적인 사용 사례는 IoT 장치 정보와 시계열 데이터 저장입니다.  
→ 시험 포인트: IoT, 시계열 데이터.

From an exam perspective, whenever you see Apache Cassandra, you should associate it with Amazon Keyspaces.  
시험 관점에서 Apache Cassandra가 나오면 Amazon Keyspaces와 연관 지어 생각하세요.  
→ 핵심 시험 전략.

This concludes the short lecture on Amazon Keyspaces.  
이로써 Amazon Keyspaces 강의를 마칩니다.  
→ 강의 종료 안내.

## Key Takeaways
## 핵심 요약
## → 시험/실무 필수 포인트

Amazon Keyspaces is a managed Apache Cassandra service on AWS.  
Amazon Keyspaces는 AWS에서 제공하는 관리형 Apache Cassandra 서비스입니다.  
→ 기본 정의 기억.

It is serverless, scalable, highly available, and fully managed by AWS.  
서버리스, 확장 가능, 고가용성, 완전 관리형 서비스입니다.  
→ 핵심 특징 요약.

Keyspaces automatically scales tables based on application traffic and replicates data across multiple availability zones.  
Keyspaces는 애플리케이션 트래픽에 따라 테이블을 자동으로 확장하며, 데이터를 여러 AZ에 복제합니다.  
→ 성능 및 내구성 포인트.

It supports Cassandra Query Language (CQL) with single-digit millisecond latency and thousands of requests per second.  
단일 숫자 밀리초 지연과 초당 수천 건의 요청을 처리하며 CQL을 지원합니다.  
→ 성능 및 쿼리 언어 시험 포인트.

Offers two capacity modes: on-demand and provisioned with auto-scaling, similar to DynamoDB.  
온디맨드와 자동 스케일링 프로비저닝 두 가지 용량 모드를 제공합니다.  
→ 용량 관리 시험 포인트.

Provides encryption, backup, and Point-In-Time Recovery up to 35 days.  
암호화, 백업, 시점 복구(PITR) 최대 35일을 제공합니다.  
→ 보안 및 데이터 보호 시험 포인트.

Common use cases include storing IoT device information and time-series data.  
사용 사례로는 IoT 장치 정보와 시계열 데이터 저장이 있습니다.  
→ 시험 실무 연관.

For exam purposes, associating Apache Cassandra with Amazon Keyspaces is sufficient.  
시험 관점에서는 Apache Cassandra = Amazon Keyspaces로 기억하면 충분합니다.  
→ 핵심 시험 전략.
```

🎮 **게임보상: Keyspaces/NoSQL 전문가 등극! 🏆**
→ Cassandra 연관 문제, 서버리스 NoSQL 문제 자신감 UP.
