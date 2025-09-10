# Amazon Data Firehose  
# 아마존 데이터 파이어호스  

---

## Introduction to Amazon Data Firehose  
## 아마존 데이터 파이어호스 소개  

Amazon Data Firehose is a service designed to send data from various sources into target destinations efficiently.  
아마존 데이터 파이어호스는 다양한 소스에서 데이터를 효율적으로 대상지로 전송하도록 설계된 서비스입니다.  

Data producers can include your applications, clients, or custom scripts.  
데이터 프로듀서는 애플리케이션, 클라이언트, 커스텀 스크립트를 포함할 수 있습니다.  

These producers use the AWS SDK or Kinesis agents to send data into Firehose.  
이 프로듀서들은 AWS SDK나 Kinesis 에이전트를 사용해 데이터를 Firehose로 전송합니다.  

Additionally, Firehose can pull data directly from services such as Kinesis Data Streams, Amazon CloudWatch Logs and Events, or AWS IoT.  
또한, Firehose는 Kinesis Data Streams, Amazon CloudWatch 로그 및 이벤트, AWS IoT와 같은 서비스에서 직접 데이터를 가져올 수도 있습니다.  

Firehose receives records either pushed from these services or pulled from sources like Kinesis Data Streams.  
Firehose는 이러한 서비스에서 푸시된 레코드 또는 Kinesis Data Streams와 같은 소스에서 가져온 레코드를 수신합니다.  

Once received, the records can optionally be transformed using an AWS Lambda function to perform data conversion or formatting.  
수신된 레코드는 선택적으로 AWS Lambda 함수를 사용해 데이터 변환이나 포맷팅을 수행할 수 있습니다.  

The data is accumulated into a buffer, which is flushed periodically to perform batch writing into various destinations.  
데이터는 버퍼에 누적되며, 주기적으로 플러시되어 다양한 대상지에 배치 쓰기를 수행합니다.  

---

## Supported Destinations  
## 지원 대상지  

Amazon Data Firehose supports multiple destination types:  
Amazon Data Firehose는 여러 대상지를 지원합니다:  

- AWS destinations such as Amazon S3, Amazon Redshift for analytics, and Amazon OpenSearch Service.  
- Amazon S3, 분석용 Amazon Redshift, Amazon OpenSearch Service와 같은 AWS 대상지  

- Third-party partner destinations including Datadog, Splunk, New Relic, and MongoDB.  
- Datadog, Splunk, New Relic, MongoDB 등 타사 파트너 대상지  

- Custom destinations via HTTP endpoint integration, allowing you to send data anywhere you require.  
- HTTP 엔드포인트 통합을 통한 커스텀 대상지, 원하는 곳으로 데이터 전송 가능  

Firehose also offers the option to write all data or only failed data to an Amazon S3 bucket for backup purposes.  
Firehose는 모든 데이터 또는 실패한 데이터만 Amazon S3 버킷에 백업 용도로 쓰는 옵션도 제공합니다.  

---

## Overview and Features  
## 개요 및 특징  

Previously known as Kinesis Data Firehose, Amazon Data Firehose has evolved to support more than just Kinesis.  
이전에는 Kinesis Data Firehose로 알려졌으며, 이제는 Kinesis 이상의 기능을 지원합니다.  

It is a fully managed service supporting destinations like Redshift, S3, and Amazon OpenSearch Service, as well as third-party services such as Splunk and custom HTTP endpoints.  
Redshift, S3, Amazon OpenSearch Service 같은 대상지와 Splunk, 커스텀 HTTP 엔드포인트 등 타사 서비스도 지원하는 완전 관리형 서비스입니다.  

Key features include automatic scaling, serverless operation, and a pay-for-what-you-use pricing model.  
주요 특징은 자동 확장, 서버리스 운영, 사용량 기반 과금 모델입니다.  

Amazon Data Firehose is a near real-time service.  
Amazon Data Firehose는 거의 실시간(nearly real-time) 서비스입니다.  

This is due to its internal buffering mechanism, which accumulates data based on size or time before flushing it to the destination.  
이는 내부 버퍼링 메커니즘 때문으로, 데이터를 크기나 시간 기준으로 누적 후 대상지로 플러시합니다.  

This buffering introduces a slight delay, distinguishing it from real-time streaming services.  
이 버퍼링 때문에 약간의 지연이 발생하며, 실제 실시간 스트리밍 서비스와 구분됩니다.  

---

## Supported Data Formats and Transformations  
## 지원 데이터 포맷 및 변환  

Firehose supports various incoming data formats including CSV, JSON, Parquet, Avro, text, and binary data.  
Firehose는 CSV, JSON, Parquet, Avro, 텍스트, 바이너리 데이터 등 다양한 입력 포맷을 지원합니다.  

It can convert data to Parquet or ORC formats and apply compression methods such as gzip or snappy.  
데이터를 Parquet 또는 ORC 포맷으로 변환하고 gzip, snappy와 같은 압축 방법을 적용할 수 있습니다.  

For custom data transformations, AWS Lambda can be used.  
커스텀 데이터 변환에는 AWS Lambda를 사용할 수 있습니다.  

For example, you can convert data from CSV to JSON format before sending it to Amazon S3.  
예를 들어, Amazon S3로 전송하기 전에 CSV 데이터를 JSON 포맷으로 변환할 수 있습니다.  

---

## Comparison: Kinesis Data Streams vs Amazon Data Firehose  
## 비교: Kinesis 데이터 스트림 vs 아마존 데이터 파이어호스  

| Feature | Kinesis Data Streams | Amazon Data Firehose |  
|---------|----------------------|----------------------|  
| Purpose | Streaming data collection | Loading streaming data into destinations |  
| 용도 | 스트리밍 데이터 수집 | 스트리밍 데이터를 대상지로 로딩 |  
| Developer Effort | Requires writing producer and consumer code | Fully managed, no code required |  
| 개발자 작업 | 프로듀서 및 컨슈머 코드 작성 필요 | 완전 관리형, 코드 필요 없음 |  
| Latency | Real-time | Near real-time |  
| 지연 | 실시간 | 거의 실시간 |  
| Modes | Provisioned and on-demand | Fully serverless with automatic scaling |  
| 모드 | 프로비저닝 및 온디맨드 | 서버리스, 자동 확장 |  
| Data Storage | Up to one year with replay capability | No data storage or replay |  
| 데이터 저장 | 최대 1년, 재처리 가능 | 데이터 저장 및 재처리 없음 |  

Kinesis Data Streams is a real-time streaming service requiring custom code for producers and consumers, supporting data storage and replay.  
Kinesis Data Streams는 실시간 스트리밍 서비스로, 프로듀서 및 컨슈머를 위한 커스텀 코드가 필요하며, 데이터 저장과 재처리를 지원합니다.  

In contrast, Amazon Data Firehose is a fully managed service focused on loading streaming data into destinations with automatic scaling and no data storage.  
반면 Amazon Data Firehose는 자동 확장과 데이터 저장 없이 스트리밍 데이터를 대상지로 로딩하는 완전 관리형 서비스입니다.  

---

## Conclusion  
## 결론  

Amazon Data Firehose simplifies the process of loading streaming data into various destinations with minimal management overhead.  
Amazon Data Firehose는 최소한의 관리로 스트리밍 데이터를 다양한 대상지로 로딩하는 과정을 단순화합니다.  

Its near real-time delivery, support for multiple data formats, and integration with AWS Lambda for transformations make it a versatile tool for data ingestion pipelines.  
거의 실시간 전달, 다양한 데이터 포맷 지원, AWS Lambda와의 통합을 통한 변환 기능은 데이터 수집 파이프라인에서 다목적 도구로 활용될 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon Data Firehose is a fully managed, serverless service for loading streaming data into various destinations.  
- Amazon Data Firehose는 스트리밍 데이터를 다양한 대상지로 로딩하는 완전 관리형 서버리스 서비스입니다.  

- It supports near real-time data delivery with buffering based on size or time before batch writing.  
- 배치 쓰기 전 크기나 시간 기준 버퍼링으로 거의 실시간 데이터 전달을 지원합니다.  

- Firehose can ingest data from multiple sources, transform data using AWS Lambda, and deliver to AWS services or third-party destinations.  
- Firehose는 여러 소스에서 데이터를 수집하고, AWS Lambda를 이용해 변환하며, AWS 서비스 또는 타사 대상지로 전달할 수 있습니다.  

- Unlike Kinesis Data Streams, Firehose does not store data or support replay, focusing on automatic scaling and ease of use.  
- Kinesis Data Streams와 달리 Firehose는 데이터 저장이나 재처리를 지원하지 않으며, 자동 확장과 사용 편의성에 중점을 둡니다.  
