```md
# Amazon Managed Service for Apache Flink - Hands On
# Amazon Managed Service for Apache Flink - 실습
# → Apache Flink 실습 강의

## Introduction to Amazon Kinesis Data Analytics
## Amazon Kinesis Data Analytics 소개
# → Kinesis 데이터 분석 개요

In this lecture, we explore the options available within the Amazon Kinesis service for data analytics.  
이번 강의에서는 Amazon Kinesis 서비스 내 데이터 분석 옵션을 살펴봅니다.  
→ Kinesis 내 분석 옵션 탐색

Specifically, we focus on Kinesis Data Analytics, which provides capabilities for processing streaming data.  
특히 스트리밍 데이터 처리를 제공하는 Kinesis Data Analytics에 집중합니다.  
→ 스트리밍 처리 강조

Within Kinesis Data Analytics, there are two primary options:  
Kinesis Data Analytics에는 두 가지 주요 옵션이 있습니다.  
→ 옵션 구분

- Creating a streaming application.  
- 스트리밍 애플리케이션 생성  
→ 실시간 애플리케이션

- Using the Kinesis Data Analytics Studio.  
- Kinesis Data Analytics Studio 사용  
→ 대화형 개발 환경

The streaming application option leverages Apache Flink, an open-source stream processing framework.  
스트리밍 애플리케이션 옵션은 오픈소스 스트림 처리 프레임워크인 Apache Flink를 활용합니다.  
→ Flink 활용

When creating a streaming application, you select a supported Apache Flink runtime version and provide an application name.  
스트리밍 애플리케이션 생성 시, 지원되는 Apache Flink 런타임 버전을 선택하고 애플리케이션 이름을 지정합니다.  
→ 생성 단계 1

Subsequently, you enter production information to configure the application.  
그 다음, 애플리케이션을 구성하기 위해 프로덕션 정보를 입력합니다.  
→ 구성 단계 2

This process results in the creation of a streaming application that runs on AWS.  
이 과정을 통해 AWS에서 실행되는 스트리밍 애플리케이션이 생성됩니다.  
→ 애플리케이션 생성 완료

After creation, you upload your application code to the streaming application.  
생성 후에는 스트리밍 애플리케이션에 애플리케이션 코드를 업로드합니다.  
→ 코드 업로드

Since Apache Flink applications can be complex, initially, there may be no applications available.  
Apache Flink 애플리케이션은 복잡할 수 있어, 초기에는 애플리케이션이 없을 수 있습니다.  
→ 초기 상태 안내

Once uploaded, you can run and monitor the application using the Apache Flink dashboard.  
업로드 후, Apache Flink 대시보드를 사용하여 애플리케이션을 실행하고 모니터링할 수 있습니다.  
→ 실행 및 모니터링

The Kinesis Data Analytics Studio offers an alternative approach by providing a notebook environment.  
Kinesis Data Analytics Studio는 노트북 환경을 제공하여 대안적 접근 방식을 제공합니다.  
→ Studio 사용

This studio quickly creates a notebook where you can start running streaming applications, again leveraging Apache Flink.  
이 Studio에서는 노트북을 빠르게 생성하여 Apache Flink를 활용한 스트리밍 애플리케이션을 실행할 수 있습니다.  
→ 실시간 개발 환경

This option is suitable for interactive development and testing.  
이 옵션은 대화형 개발 및 테스트에 적합합니다.  
→ 사용 용도 안내

## SQL Applications in Kinesis Data Analytics
## Kinesis Data Analytics의 SQL 애플리케이션
# → SQL 애플리케이션

On the left-hand side of the Kinesis console, you can find the option for SQL applications under the legacy section.  
Kinesis 콘솔 왼쪽에서 레거시 섹션 아래 SQL 애플리케이션 옵션을 찾을 수 있습니다.  
→ 위치 안내

Although legacy SQL applications are still available, the recommended approach is to use Kinesis Data Analytics Studio with Apache Flink for new developments.  
레거시 SQL 애플리케이션은 여전히 존재하지만, 신규 개발에는 Apache Flink와 함께 Kinesis Data Analytics Studio 사용을 권장합니다.  
→ 권장 방식 안내

If you choose to create a legacy SQL application, you provide an application name and configure it accordingly.  
레거시 SQL 애플리케이션을 생성하려면 애플리케이션 이름을 지정하고 구성해야 합니다.  
→ 생성 절차

These applications can read data from sources such as Kinesis Data Firehose.  
이 애플리케이션은 Kinesis Data Firehose와 같은 데이터 소스를 읽을 수 있습니다.  
→ 데이터 입력

Once configured, you can write SQL queries for real-time analytics within the application.  
구성 후, 애플리케이션 내에서 실시간 분석을 위한 SQL 쿼리를 작성할 수 있습니다.  
→ 실시간 분석

## Summary
## 요약
# → 핵심 정리

This overview introduces the options available in Amazon Kinesis for data analytics, including streaming applications using Apache Flink and SQL applications.  
이 개요에서는 Apache Flink를 사용하는 스트리밍 애플리케이션과 SQL 애플리케이션을 포함하여 Amazon Kinesis의 데이터 분석 옵션을 소개합니다.  
→ 옵션 소개

While legacy SQL applications exist, the current recommendation is to use Kinesis Data Analytics Studio with Apache Flink for streaming data processing and analytics.  
레거시 SQL 애플리케이션이 존재하지만, 현재 권장 방법은 Apache Flink와 함께 Kinesis Data Analytics Studio를 사용하는 것입니다.  
→ 권장 방법 요약

This concludes the lecture on Amazon Managed Service for Apache Flink.  
이로써 Amazon Managed Service for Apache Flink 강의가 끝났습니다.  
→ 강의 종료

The next lecture will continue exploring related topics.  
다음 강의에서는 관련 주제를 계속 탐구합니다.  
→ 다음 강의 안내

## Key Takeaways
## 핵심 요약
# → 시험/실무 포인트

Amazon Kinesis offers two main options for data analytics: streaming applications leveraging Apache Flink and SQL applications.  
Amazon Kinesis는 Apache Flink를 활용한 스트리밍 애플리케이션과 SQL 애플리케이션이라는 두 가지 주요 데이터 분석 옵션을 제공합니다.  
→ 분석 옵션

Streaming applications use Apache Flink runtime versions and require uploading your application code.  
스트리밍 애플리케이션은 Apache Flink 런타임 버전을 사용하며 애플리케이션 코드를 업로드해야 합니다.  
→ 실행 준비

The Apache Flink dashboard allows monitoring of streaming applications.  
Apache Flink 대시보드를 통해 스트리밍 애플리케이션을 모니터링할 수 있습니다.  
→ 모니터링 기능

Kinesis Data Analytics Studio provides a notebook environment for running streaming applications with Apache Flink.  
Kinesis Data Analytics Studio는 Apache Flink를 사용한 스트리밍 애플리케이션 실행을 위한 노트북 환경을 제공합니다.  
→ Studio 환경 강조

Legacy SQL applications exist but the recommended approach is to use Kinesis Data Analytics Studio with Apache Flink.  
레거시 SQL 애플리케이션이 존재하지만, 권장 접근 방식은 Apache Flink와 함께 Kinesis Data Analytics Studio를 사용하는 것입니다.  
→ 권장 방식 강조

SQL applications can read from Kinesis Data Firehose and allow writing SQL queries for real-time analytics.  
SQL 애플리케이션은 Kinesis Data Firehose를 읽고 실시간 분석을 위한 SQL 쿼리를 작성할 수 있습니다.  
→ SQL 실시간 분석
```

🎮 **게임보상: Kinesis 스트림 분석 마스터! 🏆**
→ Apache Flink + Kinesis 실습 이해 완료!
