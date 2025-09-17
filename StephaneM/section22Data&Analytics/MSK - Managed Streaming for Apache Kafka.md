```md
# MSK - Managed Streaming for Apache Kafka
# MSK - Apache Kafka 관리형 스트리밍
# → Amazon MSK 개요

## Introduction to Amazon MSK
## Amazon MSK 소개
# → MSK 기본 개념

Amazon Managed Streaming for Apache Kafka, also known as Amazon MSK, is an analytics service provided by AWS.  
Amazon MSK(Amazon Managed Streaming for Apache Kafka)는 AWS에서 제공하는 분석 서비스입니다.  
→ MSK 정의

Kafka is an alternative to Amazon Kinesis, and both allow for data streaming.  
Kafka는 Amazon Kinesis의 대안이며, 두 서비스 모두 데이터 스트리밍을 지원합니다.  
→ 스트리밍 비교

## Features of Amazon MSK
## Amazon MSK의 특징
# → 주요 기능

MSK enables users to obtain a fully managed Kafka cluster on AWS.  
MSK를 사용하면 AWS에서 완전 관리형 Kafka 클러스터를 얻을 수 있습니다.  
→ 관리형 클러스터 제공

It allows for the creation, updating, and deletion of clusters on the fly.  
클러스터를 즉시 생성, 업데이트, 삭제할 수 있습니다.  
→ 클러스터 관리 유연성

MSK manages Kafka broker nodes and Zookeeper broker nodes within your cluster, and you can deploy the cluster in your VPC across multiple Availability Zones, up to three for high availability.  
MSK는 클러스터 내 Kafka 브로커 노드와 Zookeeper 브로커 노드를 관리하며, VPC 내 여러 가용 영역(AZ)에 최대 3개까지 클러스터를 배포해 고가용성을 지원합니다.  
→ HA 구성 설명

MSK provides automatic recovery from common Kafka failures, and data is stored on EBS volumes for as long as required.  
MSK는 일반 Kafka 오류 발생 시 자동 복구 기능을 제공하며, 데이터는 필요한 기간 동안 EBS 볼륨에 저장됩니다.  
→ 내결함성 및 저장

Setting up Apache Kafka can be challenging, but with Amazon MSK, it is possible to deploy Kafka on AWS with a single click.  
Apache Kafka 설치는 어렵지만, Amazon MSK를 사용하면 AWS에서 한 번의 클릭으로 Kafka를 배포할 수 있습니다.  
→ 배포 간편화

## MSK Serverless
## MSK 서버리스
# → 서버리스 옵션

MSK Serverless allows you to run Apache Kafka on MSK without provisioning servers or managing capacity.  
MSK 서버리스는 서버를 프로비저닝하거나 용량을 관리하지 않고도 Apache Kafka를 실행할 수 있게 해줍니다.  
→ 서버리스 개념

MSK automatically provisions resources and scales compute and storage as needed.  
MSK는 자동으로 리소스를 프로비저닝하고, 필요에 따라 컴퓨팅과 스토리지를 확장합니다.  
→ 자동 스케일링

## Understanding Apache Kafka
## Apache Kafka 이해
# → Kafka 개요

Apache Kafka is a platform for streaming data.  
Apache Kafka는 스트리밍 데이터를 처리하는 플랫폼입니다.  
→ 스트리밍 플랫폼

A Kafka cluster consists of multiple brokers.  
Kafka 클러스터는 여러 브로커로 구성됩니다.  
→ 브로커 구조

Producers ingest data from sources such as Kinesis, IoT, or RDS and send it to a Kafka topic.  
프로듀서는 Kinesis, IoT, RDS 등의 소스에서 데이터를 받아 Kafka 토픽으로 전송합니다.  
→ 데이터 흐름 설명

This topic is fully replicated across other brokers.  
이 토픽은 다른 브로커에 완전히 복제됩니다.  
→ 토픽 복제

Kafka topics provide real-time streaming of data, and consumers pull data from these topics to process or send to destinations such as EMR, S3, SageMaker, Kinesis, or RDS.  
Kafka 토픽은 데이터를 실시간 스트리밍하며, 컨슈머는 이 데이터를 가져와 처리하거나 EMR, S3, SageMaker, Kinesis, RDS 등으로 전송합니다.  
→ 데이터 소비

## Kafka vs. Kinesis Data Streams
## Kafka vs. Kinesis 데이터 스트림
# → 비교

There are several differences between Kinesis Data Streams and Amazon MSK:  
Kinesis Data Streams와 Amazon MSK 간에는 몇 가지 차이점이 있습니다.  
→ 비교 항목

- Kinesis Data Streams have a 1 MB message limit, which is the default in MSK, but MSK can be configured for higher message retention, such as 10 MB.  
- Kinesis는 메시지 크기 제한이 1MB이며, MSK는 기본값도 1MB지만, 10MB 등 더 큰 메시지 보존으로 구성할 수 있습니다.  
→ 메시지 크기 차이

- Kinesis uses Data Streams with Shards, while MSK uses Kafka Topics with Partitions. The concepts are similar.  
- Kinesis는 샤드가 있는 데이터 스트림을 사용하고, MSK는 파티션이 있는 Kafka 토픽을 사용합니다. 개념은 유사합니다.  
→ 구조 비교

- To scale Kinesis Data Streams, you perform Shard Splitting or Merging. In MSK, you can only add partitions to scale a topic; partitions cannot be removed.  
- Kinesis 데이터 스트림 확장은 샤드 분할/병합으로 수행하고, MSK는 파티션 추가로 토픽을 확장하며, 제거는 불가합니다.  
→ 확장 방법 비교

- Kinesis Data Streams provide in-flight encryption, while MSK offers either plain text or TLS in-flight encryption.  
- Kinesis 데이터 스트림은 전송 중 암호화를 제공하고, MSK는 평문 또는 TLS 전송 암호화를 제공합니다.  
→ 전송 중 암호화

- Both Kinesis and MSK provide at-rest encryption.  
- Kinesis와 MSK 모두 저장 시 암호화를 제공합니다.  
→ 저장 암호화

- In MSK, you can retain data for as long as you want, even over a year, as long as you pay for the underlying EBS storage.  
- MSK에서는 원하는 만큼 데이터를 보존할 수 있으며, 1년 이상도 가능하며, EBS 스토리지 비용을 지불하면 됩니다.  
→ 장기 보존 가능

## Producing and Consuming Data with MSK
## MSK 데이터 생산 및 소비
# → 데이터 입출력

To produce data to MSK, you need to create a Kafka Producer.  
MSK에 데이터를 생산하려면 Kafka 프로듀서를 생성해야 합니다.  
→ 생산자 생성

To consume data from MSK, there are several options:  
MSK에서 데이터를 소비하려면 여러 옵션이 있습니다.  
→ 소비 방법

- Use Kinesis Data Analytics for Apache Flink to read directly from the MSK cluster.  
- Apache Flink용 Kinesis Data Analytics를 사용해 MSK 클러스터에서 직접 읽기  
→ Flink 활용

- Use AWS Glue to perform streaming ETL jobs, powered by Apache Spark Streaming.  
- AWS Glue를 사용하여 Apache Spark Streaming 기반 스트리밍 ETL 수행  
→ Glue 활용

- Use Lambda functions to have Amazon MSK as an event source.  
- Lambda 함수를 사용하여 MSK를 이벤트 소스로 사용  
→ Lambda 이벤트

- Write your own Kafka consumer and run it on platforms such as Amazon EC2, ECS, or EKS clusters.  
- Kafka 컨슈머를 직접 작성하고 Amazon EC2, ECS, EKS 등에서 실행  
→ 커스텀 소비자

Once you understand these concepts, you are well-prepared for Amazon MSK at the exam level.  
이 개념들을 이해하면, 시험 수준에서 Amazon MSK를 충분히 준비한 것입니다.  
→ 시험 대비

## Key Takeaways
## 핵심 요약
# → 시험/실무 포인트

Amazon MSK provides a fully managed Apache Kafka cluster on AWS, simplifying deployment and management.  
Amazon MSK는 AWS에서 완전 관리형 Apache Kafka 클러스터를 제공하며, 배포 및 관리를 간소화합니다.  
→ 관리형 Kafka 강조

MSK Serverless allows running Apache Kafka without provisioning or managing servers, with automatic scaling of compute and storage.  
MSK 서버리스는 서버 프로비저닝이나 관리 없이 Apache Kafka를 실행하며, 컴퓨팅과 스토리지를 자동으로 확장합니다.  
→ 서버리스 강조

Kafka and Kinesis are both streaming data solutions, but differ in scaling, message limits, and partition management.  
Kafka와 Kinesis는 모두 스트리밍 데이터 솔루션이지만, 확장, 메시지 제한, 파티션 관리에서 차이가 있습니다.  
→ 핵심 차이

Data can be produced to MSK using Kafka Producers and consumed using various AWS services or custom consumers.  
데이터는 Kafka 프로듀서를 통해 MSK에 생산하고, 다양한 AWS 서비스 또는 커스텀 컨슈머를 통해 소비할 수 있습니다.  
→ 입출력 정리
```

🎮 **게임보상: Kafka 스트리밍 마스터! 🏆**
→ MSK 실습 및 이론 완벽 이해 완료
