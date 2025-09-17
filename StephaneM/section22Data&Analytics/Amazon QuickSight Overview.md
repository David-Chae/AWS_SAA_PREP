```md
# Amazon QuickSight Overview
# Amazon QuickSight 개요
# → QuickSight 기본 이해

Now let's talk about Amazon QuickSight.  
이제 Amazon QuickSight에 대해 이야기해보겠습니다.  
→ 주제 소개.

Amazon QuickSight is a serverless, machine-powered business intelligence service.  
Amazon QuickSight는 서버리스 방식으로 동작하는 머신 기반 비즈니스 인텔리전스 서비스입니다.  
→ 정의와 특징.

When you hear business intelligence, it means you are going to create interactive dashboards.  
비즈니스 인텔리전스라고 하면, 인터랙티브한 대시보드를 만들 수 있다는 의미입니다.  
→ 목적 이해.

This is what QuickSight looks like: you can create dashboards connected to data sources that you own, enabling you to create visually appealing visuals.  
QuickSight는 이렇게 생겼습니다: 사용자가 소유한 데이터 소스에 연결된 대시보드를 만들어 시각적으로 매력적인 시각화를 생성할 수 있습니다.  
→ 대시보드 기능 강조.

QuickSight is fast, automatically scalable, embeddable in websites, and offers per-session pricing.  
QuickSight는 빠르고 자동으로 스케일링되며, 웹사이트에 임베드 가능하고 세션 단위 과금 모델을 제공합니다.  
→ 성능과 비용 모델 설명.

Use cases for QuickSight include business analytics, building visualizations, and performing ad-hoc visual analysis to gain business insights using data.  
QuickSight의 사용 사례에는 비즈니스 분석, 시각화 생성, 데이터 기반 즉석 시각적 분석을 통해 인사이트 도출이 포함됩니다.  
→ 활용 사례.

You can connect to many data sources such as RDS, Aurora, Athena, Redshift, S3, and more.  
RDS, Aurora, Athena, Redshift, S3 등 다양한 데이터 소스에 연결할 수 있습니다.  
→ 데이터 소스 연결 가능성 강조.

There is something called the SPICE engine, which is an in-memory computation engine that works only if you import data directly into Amazon QuickSight.  
SPICE 엔진이라는 것이 있는데, 이는 인메모리 계산 엔진으로 QuickSight로 데이터를 직접 가져올 때만 작동합니다.  
→ SPICE 엔진 정의.

It does not work if QuickSight is connected to another database.  
QuickSight가 다른 데이터베이스에 연결된 경우에는 SPICE가 작동하지 않습니다.  
→ SPICE 제한 사항.

QuickSight has user-level features; in the Enterprise edition, you can set up column-level security (CLS) to prevent certain columns from being displayed to users without sufficient access rights.  
QuickSight에는 사용자 수준 기능이 있으며, 엔터프라이즈 에디션에서는 접근 권한이 없는 사용자에게 특정 열이 표시되지 않도록 컬럼 수준 보안(CLS)을 설정할 수 있습니다.  
→ 보안 기능 강조.

## QuickSight Integrations
## QuickSight 통합
# → 연동 가능 서비스

QuickSight integrates with many AWS data sources such as:  
QuickSight는 다음과 같은 많은 AWS 데이터 소스와 통합됩니다:  
→ AWS 연동 예시

- RDS databases  
- RDS 데이터베이스  
→ 관계형 DB

- Aurora  
- Aurora  
→ AWS 관계형 DB

- Redshift (a data warehousing service)  
- Redshift (데이터 웨어하우스 서비스)  
→ 대용량 분석 DB

- Athena for ad-hoc queries on Amazon S3  
- Amazon S3에 대한 즉석 쿼리를 위해 Athena  
→ 서버리스 분석

- Amazon S3 for data import  
- 데이터 가져오기용 Amazon S3  
→ 원본 데이터

- OpenSearch  
- OpenSearch  
→ 검색/분석 엔진

- Timestream for optimized time series data visualization  
- 시간 시계열 데이터 시각화를 최적화한 Timestream  
→ 시계열 데이터

It also integrates with third-party software as a service data sources supported by QuickSight, including Salesforce and Jira.  
또한 QuickSight가 지원하는 SaaS 외부 데이터 소스(Salesforce, Jira 등)와도 통합됩니다.  
→ SaaS 연동

Additionally, it supports third-party databases like Teradata and on-premises databases using the JDBC protocol.  
추가적으로 Teradata 같은 서드파티 DB와 JDBC 프로토콜을 사용하는 온프레미스 DB도 지원합니다.  
→ 외부 DB 지원

You can import data sources directly into QuickSight, such as Excel files, CSV files, JSON documents, TSV, or EFS CLF log formats.  
Excel, CSV, JSON, TSV, EFS CLF 로그 형식 등 데이터를 QuickSight로 직접 가져올 수 있습니다.  
→ 직접 가져오기 가능 파일 형식

When data is imported, you can leverage the SPICE engine for very fast in-memory computation.  
데이터를 가져오면 SPICE 엔진을 활용해 매우 빠른 인메모리 계산이 가능합니다.  
→ SPICE 장점 강조

Common exam scenarios include using QuickSight with Athena or QuickSight with Redshift, though any integration is possible.  
시험에서는 QuickSight를 Athena 또는 Redshift와 함께 사용하는 시나리오가 흔하지만, 모든 통합이 가능합니다.  
→ 시험 포인트

## QuickSight Users, Groups, Dashboards, and Analyses
## QuickSight 사용자, 그룹, 대시보드, 분석
# → 사용자/그룹/대시보드 구조

QuickSight has users, available in the Standard version, and groups of users, available only in the Enterprise version.  
QuickSight에는 Standard 버전에서 사용자가 있고, Enterprise 버전에서만 그룹 기능이 있습니다.  
→ 버전별 기능 차이

These users and groups exist within QuickSight and are not equivalent to IAM users, which are used only for administration.  
이 사용자와 그룹은 QuickSight 내부에 존재하며, IAM 사용자(관리용)와는 다릅니다.  
→ 사용자 개념 구분

You define users and groups within QuickSight, then create dashboards.  
QuickSight 내에서 사용자와 그룹을 정의한 후 대시보드를 생성합니다.  
→ 생성 과정

A dashboard is a read-only snapshot of an analysis that can be shared.  
대시보드는 분석의 읽기 전용 스냅샷으로, 공유가 가능합니다.  
→ 대시보드 정의

It preserves the configuration of the analysis, including filters, parameters, controls, and sorting options.  
필터, 파라미터, 컨트롤, 정렬 옵션 등 분석 구성을 그대로 유지합니다.  
→ 분석 구성 유지

An analysis is more complete, but you can share either the analysis or the dashboard with specific users or groups.  
분석은 더 완전하지만, 분석 전체 또는 대시보드를 특정 사용자나 그룹과 공유할 수 있습니다.  
→ 공유 옵션

To share, you must first publish your dashboards.  
공유하려면 먼저 대시보드를 게시해야 합니다.  
→ 게시 필요

Users with access to dashboards can also see the underlying data.  
대시보드 접근 권한이 있는 사용자는 기본 데이터도 볼 수 있습니다.  
→ 데이터 접근 권한 이해

In summary, you create analyses or dashboards in QuickSight and share them with specified users and groups.  
요약하면, QuickSight에서 분석 또는 대시보드를 만들고 지정된 사용자 및 그룹과 공유합니다.  
→ 핵심 사용 방법

That covers everything you need to know about QuickSight for the exam.  
이것으로 QuickSight 시험 대비 필수 내용을 모두 다뤘습니다.  
→ 시험 요약

## Key Takeaways
## 핵심 요약
# → 시험/실무 포인트

Amazon QuickSight is a serverless, machine-powered business intelligence service for creating interactive dashboards.  
Amazon QuickSight는 서버리스 방식으로 동작하는 머신 기반 비즈니스 인텔리전스 서비스로, 인터랙티브 대시보드 생성에 사용됩니다.  
→ 정의 포인트

QuickSight integrates with various AWS data sources like RDS, Aurora, Athena, Redshift, S3, and third-party sources.  
QuickSight는 RDS, Aurora, Athena, Redshift, S3 및 외부 데이터 소스와 통합됩니다.  
→ 데이터 연동 포인트

The SPICE engine enables fast, in-memory computation when data is imported directly into QuickSight.  
SPICE 엔진은 데이터를 QuickSight로 직접 가져올 때 빠른 인메모리 계산을 가능하게 합니다.  
→ SPICE 장점

QuickSight supports user and group management within the service, with dashboards as read-only snapshots of analyses that can be shared securely.  
QuickSight는 서비스 내 사용자 및 그룹 관리 기능을 지원하며, 대시보드는 분석의 읽기 전용 스냅샷으로 안전하게 공유할 수 있습니다.  
→ 사용자/보안 관리
```

🎮 **게임보상: QuickSight 데이터 시각화 마스터! 🏆**
→ SPICE, 대시보드, 사용자 관리, AWS 연동까지 완벽 이해 완료!
