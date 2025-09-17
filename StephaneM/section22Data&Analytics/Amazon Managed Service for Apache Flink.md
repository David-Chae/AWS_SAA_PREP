```md
# Amazon Managed Service for Apache Flink
# → 아마존 관리형 Apache Flink 서비스 개요

## Introduction to Amazon Managed Service for Apache Flink
## Amazon Managed Service for Apache Flink 소개
# → 서비스 소개

Let's discuss the Amazon Managed Service for Apache Flink.  
Amazon Managed Service for Apache Flink에 대해 알아봅시다.  
→ 소개

Previously, it was called Kinesis Data Analytics for Apache Flink, but it has since been renamed to simply Managed Service for Apache Flink.  
이전에는 Kinesis Data Analytics for Apache Flink라고 불렸지만, 현재는 Managed Service for Apache Flink로 이름이 변경되었습니다.  
→ 이름 변경 히스토리

## What is Apache Flink?
## Apache Flink란 무엇인가?
# → Apache Flink 정의

Apache Flink is a framework typically used with Java, SQL, or Scala languages.  
Apache Flink는 주로 Java, SQL, 또는 Scala 언어와 함께 사용되는 프레임워크입니다.  
→ 사용 언어

It is designed for processing data streams in real time.  
실시간 데이터 스트림 처리용으로 설계되었습니다.  
→ 목적 강조

## Data Sources for Flink
## Flink용 데이터 소스
# → 데이터 입력

Amazon Managed Service for Apache Flink can read data from Kinesis Data Streams or Amazon MSK, which is Apache Kafka.  
Amazon Managed Service for Apache Flink는 Kinesis Data Streams 또는 Amazon MSK(Apache Kafka)를 읽을 수 있습니다.  
→ 입력 소스

Amazon MSK is a managed service for Apache Kafka, a real-time data streaming platform, but it is not an AWS service itself.  
Amazon MSK는 Apache Kafka의 관리형 서비스로, 실시간 데이터 스트리밍 플랫폼이지만 자체적으로 AWS 서비스는 아닙니다.  
→ MSK 설명

## Features of Amazon Managed Service for Apache Flink
## Amazon Managed Service for Apache Flink 특징
# → 서비스 기능

Thanks to this managed service, you can run any Apache Flink application on a managed cluster within AWS.  
이 관리형 서비스를 통해 AWS 관리 클러스터에서 Apache Flink 애플리케이션을 실행할 수 있습니다.  
→ 클러스터 관리

AWS provisions the compute resources for you, provides access to parallel computation, and supports automatic scaling.  
AWS가 컴퓨팅 리소스를 제공하며, 병렬 연산 접근과 자동 확장을 지원합니다.  
→ 리소스 관리 및 확장성

Additionally, AWS manages your application backups, implemented as checkpoints and snapshots.  
또한 AWS는 체크포인트와 스냅샷 형태로 애플리케이션 백업을 관리합니다.  
→ 백업 관리

## Flexibility in Data Transformation
## 데이터 변환의 유연성
# → 데이터 처리 자유도

You can use any Apache Flink-supported programming features to transform your data streams.  
Apache Flink에서 지원하는 모든 프로그래밍 기능을 사용해 데이터 스트림을 변환할 수 있습니다.  
→ 변환 자유도

This gives you freedom regarding the types of transformations you want to perform on your streams.  
즉, 스트림에 수행할 변환 유형에 대한 자유를 제공합니다.  
→ 실무 유연성 강조

## Important Note on Data Sources
## 데이터 소스 관련 중요 사항
# → 시험 포인트

While Flink can read from Kinesis Data Streams, it cannot read from Amazon Data Firehose.  
Flink는 Kinesis Data Streams는 읽을 수 있지만, Amazon Data Firehose는 읽을 수 없습니다.  
→ 제한 사항

This is an important detail that could be tested in exams.  
이는 시험에서 출제될 수 있는 중요한 세부사항입니다.  
→ 시험 포인트 강조

## Summary
## 요약
# → 핵심 정리

In summary, Amazon Managed Service for Apache Flink is used exclusively for processing data streams in real time, leveraging the power of Apache Flink on AWS-managed infrastructure.  
요약하면, Amazon Managed Service for Apache Flink는 AWS 관리형 인프라에서 Apache Flink의 힘을 활용하여 실시간 데이터 스트림 처리를 위해 사용됩니다.  
→ 목적 및 사용 환경 정리

## Key Takeaways
## 핵심 요약
# → 시험/실무 포인트

Amazon Managed Service for Apache Flink is a managed service for running Apache Flink applications on AWS.  
Amazon Managed Service for Apache Flink는 AWS에서 Apache Flink 애플리케이션을 실행하기 위한 관리형 서비스입니다.  
→ 관리형 서비스 강조

Flink is a framework primarily using Java, SQL, or Scala for real-time data stream processing.  
Flink는 주로 Java, SQL, Scala를 사용하는 실시간 데이터 스트림 처리 프레임워크입니다.  
→ 처리 프레임워크

The service provisions compute resources, supports parallel computation, automatic scaling, and manages application backups via checkpoints and snapshots.  
이 서비스는 컴퓨팅 리소스를 제공하고, 병렬 연산, 자동 확장을 지원하며 체크포인트와 스냅샷으로 애플리케이션 백업을 관리합니다.  
→ 기능 요약

Flink can read data from Kinesis Data Streams and Amazon MSK (Apache Kafka), but not from Amazon Data Firehose.  
Flink는 Kinesis Data Streams와 Amazon MSK(Apache Kafka)를 읽을 수 있지만, Amazon Data Firehose는 읽을 수 없습니다.  
→ 데이터 소스 제한
```

🎮 **게임보상: Apache Flink 스트림 마스터! 🏆**
→ 실시간 데이터 처리 및 관리형 Flink 이해 완료!
