# Amazon Data Firehose - Hands On  
# 아마존 데이터 파이어호스 - 실습  

---

## Introduction to Kinesis Data Firehose Delivery Streams  
## Kinesis Data Firehose 배달 스트림 소개  

In this session, we will practice using Kinesis Data Firehose with delivery streams.  
이번 세션에서는 Kinesis Data Firehose를 사용하여 배달 스트림을 실습합니다.  

Upon accessing the delivery streams section, we can create a new delivery stream.  
배달 스트림 섹션에 접속하면 새 배달 스트림을 생성할 수 있습니다.  

A detailed diagram illustrates how Kinesis Data Firehose operates.  
자세한 다이어그램은 Kinesis Data Firehose의 작동 방식을 보여줍니다.  

---

## Data Sources  
## 데이터 소스  

Data is ingested from producers, which can be either a Kinesis Data Stream, as in our use case, or Direct PUTs through Kinesis Data Agents, other AWS services such as CloudWatch, IoT Core, EventBridge, and also custom applications using the SDK that send data directly into Kinesis Data Firehose.  
데이터는 프로듀서에서 수집되며, 프로듀서는 Kinesis Data Stream(이 실습에서는 사용), Kinesis Data Agent를 통한 Direct PUT, CloudWatch, IoT Core, EventBridge 등의 AWS 서비스, 또는 SDK를 사용해 직접 Firehose로 데이터를 전송하는 커스텀 애플리케이션일 수 있습니다.  

Once data is ingested, it can be transformed using a Lambda function.  
데이터가 수집되면 Lambda 함수를 사용하여 변환할 수 있습니다.  

This transformation can include converting the record format or other processing before loading the data into target stores.  
이 변환 과정에는 레코드 포맷 변환이나 대상 저장소에 데이터를 로드하기 전의 기타 처리 작업이 포함될 수 있습니다.  

The data is then loaded into destinations such as Amazon S3, Amazon OpenSearch Service (formerly ElasticSearch), Amazon Redshift, or various HTTP endpoint destinations.  
그 후 데이터는 Amazon S3, Amazon OpenSearch Service(구 ElasticSearch), Amazon Redshift, 또는 다양한 HTTP 엔드포인트 대상지로 로드됩니다.  

In this example, our source will be a Kinesis Data Stream, and the destination will be Amazon S3.  
이 예제에서는 소스로 Kinesis Data Stream을 사용하고, 대상지는 Amazon S3로 설정합니다.  

It is important to remember the key destinations: OpenSearch Service, Redshift, and S3.  
주요 대상지인 OpenSearch Service, Redshift, S3를 기억하는 것이 중요합니다.  

There are also many third-party services and custom HTTP endpoints available, but these are less critical to memorize.  
또한 많은 타사 서비스와 커스텀 HTTP 엔드포인트가 있지만, 외우는 것이 필수적이지는 않습니다.  

---

## Creating a Delivery Stream  
## 배달 스트림 생성  

We select Amazon S3 as the destination.  
대상지로 Amazon S3를 선택합니다.  

For the source, we browse and choose our stream, which is the ARN DemoStream in this case.  
소스로는 ARN DemoStream 스트림을 선택합니다.  

The delivery stream name is automatically generated.  
배달 스트림 이름은 자동으로 생성됩니다.  

---

## Transform and Convert Records  
## 레코드 변환 및 포맷 변경  

Transforming source records using Lambda is optional but useful.  
Lambda를 사용한 소스 레코드 변환은 선택 사항이지만 유용합니다.  

Lambda functions are pieces of code that run in AWS and can perform operations such as filtering, decompressing, converting, or processing source records before delivery by Kinesis Data Firehose.  
Lambda 함수는 AWS에서 실행되는 코드 조각으로, Kinesis Data Firehose가 데이터를 전달하기 전 필터링, 압축 해제, 포맷 변환 또는 처리 등의 작업을 수행할 수 있습니다.  

---

### Record Format Conversion  
### 레코드 포맷 변환  

Depending on the destination, it can be beneficial to convert record formats into Parquet or ORC using advanced options.  
대상지에 따라, 고급 옵션을 사용하여 레코드 포맷을 Parquet 또는 ORC로 변환하는 것이 유리할 수 있습니다.  

This topic is more detailed in the AWS data and analytics certification and is beyond the current scope.  
이 주제는 AWS 데이터 및 분석 인증 과정에서 자세히 다루며, 현재 실습 범위를 벗어납니다.  

---

## Destination Configuration  
## 대상지 구성  

We choose an existing S3 bucket named demo-firehose-stephane-V3.  
기존 S3 버킷 demo-firehose-stephane-V3를 선택합니다.  

Dynamic partitioning is set to no, and no prefix is added to the bucket.  
동적 파티셔닝은 사용하지 않으며, 버킷에 접두사도 추가하지 않습니다.  

An error output prefix is also not configured to keep the setup simple.  
설정을 단순하게 유지하기 위해 오류 출력 접두사도 설정하지 않습니다.  

---

## Buffer Hints, Compression, and Encryption  
## 버퍼 힌트, 압축 및 암호화  

The buffer allows Kinesis Data Firehose to accumulate records before delivering them to the target.  
버퍼는 Kinesis Data Firehose가 데이터를 대상지로 전달하기 전에 레코드를 누적하도록 합니다.  

By default, the buffer size is five megabytes.  
기본 버퍼 크기는 5MB입니다.  

You can increase the buffer size for efficiency or decrease it for faster delivery.  
효율성을 위해 버퍼 크기를 늘리거나, 빠른 전달을 위해 줄일 수 있습니다.  

Here, the buffer size is set to 1 MB for speed.  
이번 실습에서는 빠른 전달을 위해 버퍼 크기를 1MB로 설정합니다.  

The buffer interval controls how quickly data is flushed if the buffer size is not reached.  
버퍼 간격은 버퍼 크기가 도달하지 않았을 때 데이터를 얼마나 빨리 플러시할지를 결정합니다.  

For example, a 300-second interval means the buffer flushes every five minutes regardless of size.  
예를 들어, 300초 간격이면 버퍼는 크기와 관계없이 5분마다 플러시됩니다.  

We set the buffer interval to 60 seconds to ensure data is delivered at least every minute.  
이번 실습에서는 최소 1분마다 데이터를 전달하도록 60초로 설정합니다.  

Compression options include GZIP, Snappy, Zip, or Hadoop-Compatible Snappy, which help save storage space by compressing data before storing it in Amazon S3.  
압축 옵션에는 GZIP, Snappy, Zip, Hadoop 호환 Snappy가 있으며, Amazon S3에 저장하기 전에 데이터를 압축해 저장 공간을 절약할 수 있습니다.  

Encryption can also be enabled for securing records.  
레코드 보안을 위해 암호화도 활성화할 수 있습니다.  

An IAM role is automatically created with the necessary permissions to write to Amazon S3 and read from the Kinesis Data Stream.  
S3 쓰기 및 Kinesis Data Stream 읽기 권한을 가진 IAM 역할이 자동으로 생성됩니다.  

This role enables Kinesis Data Firehose to interact with the target buckets securely.  
이 역할은 Kinesis Data Firehose가 대상 버킷과 안전하게 상호작용할 수 있도록 합니다.  

After configuring these settings, we create the delivery stream.  
설정 후 배달 스트림을 생성합니다.  

Once active, metrics become available to monitor data flow, which is useful in production environments.  
활성화되면 데이터 흐름 모니터링을 위한 지표가 제공되며, 이는 운영 환경에서 유용합니다.  

---

## Testing Data Flow  
## 데이터 흐름 테스트  

Our Kinesis Data Firehose source is the Kinesis Data Stream named DemoStream.  
Kinesis Data Firehose 소스는 DemoStream이라는 Kinesis Data Stream입니다.  

To activate Firehose, new data must be sent to the stream after setup.  
Firehose를 활성화하려면 설정 후 스트림에 새로운 데이터를 전송해야 합니다.  

Using CloudShell, we send test data to the DemoStream.  
CloudShell을 사용해 DemoStream으로 테스트 데이터를 전송합니다.  

The data includes events such as user signup, user login, and user logout.  
데이터에는 사용자 가입, 로그인, 로그아웃 이벤트가 포함됩니다.  

After sending three records, we check the Amazon S3 bucket.  
세 개의 레코드를 전송한 후 Amazon S3 버킷을 확인합니다.  

Initially, there are zero objects because the buffer interval is 60 seconds.  
처음에는 버퍼 간격이 60초이므로 객체가 없습니다.  

We wait for the buffer to flush the data into S3.  
버퍼가 데이터를 S3로 플러시할 때까지 기다립니다.  

After more than 60 seconds, refreshing the S3 bucket shows the new data files partitioned by date.  
60초 이상 지난 후 S3 버킷을 새로고침하면 날짜별로 파티셔닝된 새 데이터 파일이 나타납니다.  

Opening a file reveals the records with user signup, login, and logout events.  
파일을 열면 사용자 가입, 로그인, 로그아웃 이벤트 레코드가 확인됩니다.  

This confirms that Kinesis Data Firehose is working correctly and delivering data to Amazon S3 as expected.  
이는 Kinesis Data Firehose가 정상 작동하며 데이터를 예상대로 Amazon S3로 전달함을 확인시켜줍니다.  

---

## Cleanup  
## 정리  

To avoid incurring charges, it is important to delete the delivery stream and the DemoStream after finishing the demo.  
비용 발생을 방지하려면 실습 후 배달 스트림과 DemoStream을 삭제하는 것이 중요합니다.  

This prevents ongoing costs associated with running these services.  
이렇게 하면 해당 서비스를 계속 사용하는 데 따른 비용이 발생하지 않습니다.  

This concludes the lecture on using Amazon Kinesis Data Firehose with delivery streams.  
이로써 배달 스트림을 사용한 Amazon Kinesis Data Firehose 실습 강의를 마칩니다.  

Thank you for following along.  
참여해주셔서 감사합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Kinesis Data Firehose ingests data from various sources including Kinesis Data Streams, AWS services, and custom applications.  
- Kinesis Data Firehose는 Kinesis Data Streams, AWS 서비스, 커스텀 애플리케이션 등 다양한 소스에서 데이터를 수집합니다.  

- Data can be transformed using Lambda functions before delivery to destinations such as Amazon S3, OpenSearch Service, and Redshift.  
- 데이터는 Amazon S3, OpenSearch Service, Redshift 등의 대상지로 전달되기 전에 Lambda 함수를 사용해 변환할 수 있습니다.  

- Buffer size and interval settings control how frequently data is delivered to the target, balancing efficiency and latency.  
- 버퍼 크기와 간격 설정은 데이터 전달 빈도를 조절하여 효율성과 지연 시간의 균형을 맞춥니다.  

- Compression and encryption options help optimize storage costs and secure data in transit and at rest.  
- 압축 및 암호화 옵션은 저장 비용을 최적화하고 데이터 전송 및 저장 시 보안을 강화합니다.  
