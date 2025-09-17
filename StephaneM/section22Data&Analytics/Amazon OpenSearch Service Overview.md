```md
# Amazon OpenSearch Service Overview
# Amazon OpenSearch 서비스 개요
# → OpenSearch 기본 이해

## Introduction to Amazon OpenSearch Service
## Amazon OpenSearch 서비스 소개
# → ElasticSearch 후속 서비스

Amazon OpenSearch Service is the successor to what was previously known as Amazon ElasticSearch.  
Amazon OpenSearch Service는 이전에 Amazon ElasticSearch로 알려졌던 서비스의 후속입니다.  
→ ElasticSearch와 OpenSearch 관계 이해.

The name change occurred due to licensing issues.  
이 이름 변경은 라이선스 문제로 발생했습니다.  
→ 이름 변경 배경.

Unlike DynamoDB, where you can only query data by primary key or indexes, OpenSearch allows you to search any fields, including partial matches.  
DynamoDB와 달리, OpenSearch는 기본 키나 인덱스뿐만 아니라 모든 필드를 검색할 수 있으며, 부분 일치 검색도 가능합니다.  
→ OpenSearch 검색 유연성.

This makes it common to use OpenSearch to provide search capabilities to your applications.  
이 때문에 OpenSearch는 애플리케이션에 검색 기능을 제공할 때 자주 사용됩니다.  
→ 애플리케이션 검색 활용 사례.

OpenSearch is typically used as a complement to another database.  
OpenSearch는 일반적으로 다른 데이터베이스를 보완하는 용도로 사용됩니다.  
→ 보조 DB 활용.

While it is primarily designed for search, it also supports analytic queries.  
주로 검색용으로 설계되었지만, 분석 쿼리도 지원합니다.  
→ 분석 기능도 가능.

This dual functionality makes it versatile for various use cases.  
이 두 가지 기능 덕분에 다양한 사용 사례에 활용 가능합니다.  
→ 범용성 강조.

## Provisioning OpenSearch Clusters
## OpenSearch 클러스터 프로비저닝
# → 클러스터 구성 옵션 이해

There are two modes to provision an OpenSearch cluster:  
OpenSearch 클러스터를 프로비저닝하는 방법은 두 가지입니다.  
→ 두 가지 모드 포인트.

### Managed Cluster Option
### 관리형 클러스터 옵션
Physical instances are provisioned for you, and you can see them.  
물리적 인스턴스가 프로비저닝되며, 사용자가 이를 확인할 수 있습니다.  
→ 관리형 클러스터 이해.

### Serverless Cluster
### 서버리스 클러스터
Everything from scaling to operations is handled by AWS, providing a fully managed experience.  
스케일링부터 운영까지 모든 것을 AWS가 처리하여 완전히 관리되는 환경을 제공합니다.  
→ 서버리스 장점 이해.

OpenSearch has its own query language and does not natively support SQL.  
OpenSearch는 자체 쿼리 언어를 가지고 있으며 기본적으로 SQL을 지원하지 않습니다.  
→ 쿼리 언어 특징.

However, SQL compatibility can be enabled via a plugin.  
하지만 플러그인을 통해 SQL 호환성을 활성화할 수 있습니다.  
→ SQL 호환 옵션.

## Data Ingestion and Security
## 데이터 적재 및 보안
# → 데이터 입력과 보안 포인트

You can ingest data into OpenSearch from various sources such as Kinesis Data Firehose, IoT devices, CloudWatch Logs, or custom-built applications.  
Kinesis Data Firehose, IoT 디바이스, CloudWatch Logs, 커스텀 애플리케이션 등 다양한 소스에서 데이터를 OpenSearch에 적재할 수 있습니다.  
→ 데이터 적재 경로 이해.

Security is provided through integration with Cognito and IAM, along with encryption at rest and in transit.  
보안은 Cognito 및 IAM 통합과, 전송 및 저장 시 암호화를 통해 제공됩니다.  
→ 보안 구성 이해.

## Analytics and Visualization
## 분석 및 시각화
# → 분석/시각화 기능

OpenSearch supports analytics on top of the data it stores.  
OpenSearch는 저장된 데이터 위에서 분석을 지원합니다.  
→ 분석 기능.

You can use OpenSearch Dashboards to create visualizations, enabling deeper insights into your data.  
OpenSearch Dashboards를 사용하여 시각화를 생성하고, 데이터에 대한 더 깊은 통찰을 얻을 수 있습니다.  
→ Dashboards 활용.

## Common Usage Patterns
## 일반적인 사용 패턴
# → 실무 아키텍처 이해

A typical pattern involves using DynamoDB as the primary data store where users insert, delete, and update data.  
일반적인 패턴은 DynamoDB를 기본 데이터 저장소로 사용하며, 사용자가 데이터를 삽입, 삭제, 업데이트합니다.  
→ DynamoDB 역할 이해.

DynamoDB Streams capture these changes and trigger a Lambda function, which inserts the data into Amazon OpenSearch in real time.  
DynamoDB Streams가 이러한 변경을 포착하고 Lambda 함수를 트리거하여 데이터를 실시간으로 OpenSearch에 적재합니다.  
→ 스트림 + Lambda 연계 이해.

This setup enables your application to perform searches, such as partial matches on item names, to retrieve item IDs.  
이 구성으로 애플리케이션은 항목 이름 부분 일치 검색 등 검색 기능을 수행하여 item ID를 가져올 수 있습니다.  
→ 검색 활용.

Once the item ID is obtained, the application queries DynamoDB to retrieve the full item details.  
item ID를 얻으면 애플리케이션은 DynamoDB에서 전체 항목 세부 정보를 조회합니다.  
→ 검색 + 원본 데이터 조회 패턴 이해.

This pattern leverages OpenSearch for search capabilities while maintaining DynamoDB as the main data source.  
이 패턴은 검색 기능에는 OpenSearch를 사용하고, DynamoDB를 메인 데이터 소스로 유지합니다.  
→ 하이브리드 아키텍처 이해.

## Ingesting CloudWatch Logs into OpenSearch
## CloudWatch 로그를 OpenSearch에 적재
# → 로그 적재 패턴

There are two main methods to ingest CloudWatch Logs into OpenSearch:  
CloudWatch 로그를 OpenSearch에 적재하는 주요 방법은 두 가지입니다.  
→ 방법 구분.

Using a CloudWatch Log Subscription Filter that sends data in real time to a Lambda function managed by AWS, which then forwards the data to OpenSearch.  
CloudWatch Log Subscription Filter를 사용하여 데이터를 실시간으로 AWS 관리 Lambda 함수로 보내고, Lambda가 OpenSearch로 전달합니다.  
→ Lambda 활용 실시간 적재.

Using a CloudWatch Logs Subscription Filter with Kinesis Data Firehose, which reads from the subscription filter and inserts data into OpenSearch near real time.  
CloudWatch Logs Subscription Filter + Kinesis Data Firehose를 사용하여 구독 필터에서 읽은 데이터를 거의 실시간으로 OpenSearch에 적재합니다.  
→ Firehose 활용 패턴.

## Ingesting Kinesis Data Streams into OpenSearch
## Kinesis Data Streams를 OpenSearch에 적재
# → 데이터 스트림 처리

Two strategies exist for sending Kinesis Data Streams into OpenSearch:  
Kinesis Data Streams를 OpenSearch에 보내는 전략은 두 가지가 있습니다.  
→ 두 가지 전략.

Using Kinesis Data Firehose for near real-time ingestion, optionally applying data transformation via a Lambda function before sending data to OpenSearch.  
Kinesis Data Firehose를 사용하여 거의 실시간 적재하며, 필요 시 Lambda로 데이터 변환 후 OpenSearch로 보냅니다.  
→ 변환 + 적재 패턴 이해.

Using Kinesis Data Streams with a Lambda function that reads the data stream in real time and writes to OpenSearch with custom code.  
Kinesis Data Streams + Lambda를 사용하여 데이터 스트림을 실시간 읽고, OpenSearch에 커스텀 코드로 적재합니다.  
→ 실시간 스트림 + 커스텀 적재.

All these patterns are valid and provide flexibility in architecting solutions with Amazon OpenSearch.  
모든 패턴이 유효하며, OpenSearch 아키텍처 설계에 유연성을 제공합니다.  
→ 설계 유연성 강조.

## Conclusion
## 결론
# → 강의 요약

This concludes the lecture on Amazon OpenSearch Service.  
이로써 Amazon OpenSearch Service 강의를 마칩니다.  
→ 강의 종료.

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  
→ 마무리 인사.

## Key Takeaways
## 핵심 요약
# → 시험/실무 포인트

Amazon OpenSearch Service is the successor to Amazon ElasticSearch, renamed due to licensing issues.  
Amazon OpenSearch Service는 Amazon ElasticSearch의 후속이며, 라이선스 문제로 이름이 변경되었습니다.  
→ 정의 확인.

OpenSearch allows searching any fields, including partial matches, complementing databases like DynamoDB.  
OpenSearch는 모든 필드를 검색할 수 있으며, 부분 일치 검색도 가능하여 DynamoDB 같은 DB를 보완합니다.  
→ 기능 이해.

OpenSearch supports both managed and serverless cluster provisioning options.  
OpenSearch는 관리형 및 서버리스 클러스터 프로비저닝을 지원합니다.  
→ 클러스터 모드 이해.

Data ingestion into OpenSearch can be done via various AWS services such as DynamoDB Streams, CloudWatch Logs, Kinesis Data Firehose, and Lambda functions.  
OpenSearch로의 데이터 적재는 DynamoDB Streams, CloudWatch Logs, Kinesis Data Firehose, Lambda 등 다양한 AWS 서비스를 통해 가능합니다.  
→ 적재 방법 이해.
```

🎮 **게임보상: OpenSearch 탐험가! 🏆**
→ 검색, 분석, 로그 처리, 스트림 적재까지 완전 이해 완료!
