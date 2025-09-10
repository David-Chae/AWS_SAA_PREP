
# Amazon Kinesis Data Streams - Hands On  
# 아마존 키네시스 데이터 스트림 - 실습  

---

## Introduction to Kinesis Data Streams Hands-On  
## 키네시스 데이터 스트림 실습 소개  

Let's begin by practicing with Kinesis Data Streams.  
키네시스 데이터 스트림 실습을 시작해보겠습니다.  

We will open the Kinesis service and create our first Kinesis Data Stream.  
Kinesis 서비스를 열고 첫 번째 Kinesis 데이터 스트림을 생성합니다.  

Upon opening the Kinesis service, we see three options: Data Streams, Data Firehose, and Data Analytics.  
Kinesis 서비스를 열면 세 가지 옵션이 보입니다: 데이터 스트림, 데이터 파이어호스, 데이터 분석.  

So far, we are familiar only with Data Streams, so we will proceed with that.  
지금까지는 데이터 스트림만 익숙하므로, 이를 선택하여 진행합니다.  

We also see pricing information: for each shard, the cost is $0.05 per hour, plus additional charges for PUT requests or data sent into Kinesis Data Streams.  
또한 가격 정보도 보이는데, 샤드당 시간당 $0.05이며, PUT 요청이나 데이터 전송에 대한 추가 요금이 있습니다.  

---

## Creating a Data Stream  
## 데이터 스트림 생성  

We will create a Data Stream and name it DemoStream.  
데이터 스트림을 생성하고 이름을 DemoStream으로 지정합니다.  

Next, we define the data stream capacity. There are two modes:  
다음으로 데이터 스트림 용량을 정의합니다. 두 가지 모드가 있습니다:  

- On-demand mode  
- 온디맨드 모드  

- Provisioned mode  
- 프로비저닝 모드  

---

### On-demand Mode  
### 온디맨드 모드  

In On-demand mode, you do not need to manage capacity as it automatically scales.  
온디맨드 모드에서는 용량을 관리할 필요가 없으며 자동으로 확장됩니다.  

The maximum throughput is 200 megabytes per second and 200,000 records per second for writes, and a maximum read capacity of 400 megabytes per second per consumer if using the enhanced Fan-Out option.  
최대 처리량은 쓰기 시 초당 200MB 및 초당 200,000 레코드이며, 향상된 Fan-Out 옵션 사용 시 소비자당 최대 읽기 용량은 초당 400MB입니다.  

Pricing is pay-per-throughput, but there is no free tier.  
요금은 처리량 기준으로 부과되며, 무료 요금제는 없습니다.  

---

### Provisioned Mode  
### 프로비저닝 모드  

Provisioned mode requires you to provision shards manually.  
프로비저닝 모드에서는 샤드를 수동으로 설정해야 합니다.  

There is a Shard Estimator tool to help determine how many shards you need based on records per second, record size, and number of consumers.  
샤드 추정 도구를 사용하면 초당 레코드 수, 레코드 크기, 소비자 수를 기반으로 필요한 샤드 수를 계산할 수 있습니다.  

For this demo, we will set up one shard.  
이번 실습에서는 샤드 1개로 설정합니다.  

One shard provides 1 megabyte per second for writes and 2 megabytes per second for reads.  
샤드 1개는 쓰기 초당 1MB, 읽기 초당 2MB의 용량을 제공합니다.  

If you provision 10 shards, the capacity multiplies by 10.  
샤드 10개를 설정하면 용량이 10배 증가합니다.  

One shard is sufficient for this demo and is the cheapest option.  
샤드 1개면 충분하며, 비용이 가장 저렴합니다.  

Note that if you do not want to incur any charges during this course, avoid this hands-on exercise, as you will be charged for the shard, although we will delete it promptly after use.  
실습 중 요금 발생을 원하지 않으면 이 실습을 피하세요. 사용 후 즉시 삭제하더라도 샤드 요금이 부과됩니다.  

When ready, click Create data stream and wait for the stream to be created.  
준비가 되면 'Create data stream'를 클릭하고 스트림 생성 완료를 기다립니다.  

Our stream has been successfully created.  
스트림이 성공적으로 생성되었습니다.  

---

## Producers and Consumers  
## 프로듀서와 컨슈머  

For applications, producers have three recommended options:  
애플리케이션에서 프로듀서는 세 가지 권장 옵션이 있습니다:  

- Kinesis Agents  
- 키네시스 에이전트  

- SDK  
- SDK  

- Kinesis Producer Library (KPL)  
- 키네시스 프로듀서 라이브러리(KPL)  

All are available on GitHub.  
모든 옵션은 GitHub에서 사용할 수 있습니다.  

The SDK allows low-level producer development, while the KPL offers a higher-level API.  
SDK는 저수준 프로듀서 개발을 지원하며, KPL은 고수준 API를 제공합니다.  

Consumers include Kinesis Data Analytics, Kinesis Data Firehose, Kinesis Client Library, and Lambda (not shown in the console options).  
컨슈머에는 Kinesis Data Analytics, Kinesis Data Firehose, Kinesis Client Library, Lambda가 포함됩니다(콘솔 옵션에는 표시되지 않음).  

You can monitor your Kinesis Data Streams to see how many records are being sent.  
키네시스 데이터 스트림에서 전송되는 레코드 수를 모니터링할 수 있습니다.  

You can also scale the stream by adjusting the number of shards, add tags, and configure enhanced Fan-Out for consumer applications.  
샤드 수 조정, 태그 추가, 컨슈머용 향상된 Fan-Out 구성으로 스트림 확장이 가능합니다.  

For now, we will keep it simple and use the SDK for producing and consuming data.  
우선 SDK를 사용해 데이터를 생성하고 소비하는 단순한 방법으로 진행합니다.  

---

## Using AWS CLI in CloudShell  
## CloudShell에서 AWS CLI 사용  

We will open a CLI environment using AWS CloudShell, which provides a preconfigured command line interface in AWS.  
AWS CloudShell을 열어 CLI 환경을 사용합니다. CloudShell은 사전 구성된 AWS CLI 환경을 제공합니다.  

This avoids local configuration and is free to use.  
로컬 환경 설정이 필요 없고 무료로 사용할 수 있습니다.  

Alternatively, you could use your own terminal or CLI if preconfigured.  
사전 구성된 경우 로컬 터미널이나 CLI를 사용할 수도 있습니다.  

---

## AWS CLI Versions  
## AWS CLI 버전  

There are two types of commands to write to Kinesis Data Stream depending on your AWS CLI version: version 1 or version 2.  
AWS CLI 버전에 따라 Kinesis 데이터 스트림에 데이터를 쓰는 명령어가 두 가지 유형이 있습니다: 버전 1 또는 버전 2.  

You can check your version by running:  
버전을 확인하려면 다음을 실행합니다:  

```bash
aws --version
````

In CloudShell, AWS CLI version 2 is installed by default.
CloudShell에는 기본적으로 AWS CLI 버전 2가 설치되어 있습니다.

We will use version 2 commands for this demo.
이번 실습에서는 버전 2 명령어를 사용합니다.

---

## Sending a Record to Kinesis Data Stream

## Kinesis 데이터 스트림에 레코드 전송

To send a record, use the put-record API.
레코드를 전송하려면 put-record API를 사용합니다.

You need to specify:
다음 정보를 지정해야 합니다:

* The stream name (in this case, DemoStream)

* 스트림 이름(이번 경우 DemoStream)

* A partition key (e.g., user1)

* 파티션 키(예: user1)

* The data payload (e.g., users signup)

* 데이터 페이로드(예: users signup)

* The option --cli-binary-format raw-in-base64-out because we are sending text data

* 텍스트 데이터를 전송하므로 --cli-binary-format raw-in-base64-out 옵션 사용

Example command:
명령어 예시:

```bash
aws kinesis put-record --stream-name DemoStream --partition-key user1 --data "users signup" --cli-binary-format raw-in-base64-out
```

The CloudShell automatically uses your IAM credentials and default region (e.g., us-east-1).
CloudShell은 IAM 자격 증명과 기본 리전(e.g., us-east-1)을 자동으로 사용합니다.

After running the command, you will receive a success message with the shard ID and sequence number.
명령 실행 후 샤드 ID와 시퀀스 번호가 포함된 성공 메시지를 받습니다.

You can send multiple messages, such as user signup, user login, and user logout to simulate activity in the stream.
여러 메시지(user signup, user login, user logout)를 보내 스트림 활동을 시뮬레이션할 수 있습니다.

---

## Monitoring Stream Metrics

## 스트림 메트릭 모니터링

If you wait a bit and check the monitoring tab, you will see metrics such as the number of put records.
잠시 기다린 후 모니터링 탭을 확인하면 put 레코드 수와 같은 메트릭을 볼 수 있습니다.

Note that CloudWatch metrics may take some time to update.
CloudWatch 메트릭은 업데이트되는 데 시간이 걸릴 수 있습니다.

---

## Consuming Data from Kinesis Data Stream

## Kinesis 데이터 스트림에서 데이터 소비

To consume data, first describe the stream to get shard information:
데이터를 소비하려면 먼저 스트림을 설명하여 샤드 정보를 확인합니다:

```bash
aws kinesis describe-stream --stream-name DemoStream
```

The output includes a StreamDescription with shard IDs, for example, shardId-0000000000000.
출력에는 샤드 ID(shardId-0000000000000 등)가 포함된 StreamDescription이 있습니다.

You will need this shard ID to read from the stream.
스트림에서 읽으려면 이 샤드 ID가 필요합니다.

When using the CLI or SDK at a low level, you must specify the shard ID.
저수준 CLI 또는 SDK 사용 시 샤드 ID를 지정해야 합니다.

Higher-level libraries like the Kinesis Client Library handle this automatically.
Kinesis Client Library 같은 고수준 라이브러리는 이를 자동으로 처리합니다.

---

## Getting a Shard Iterator

## 샤드 이터레이터 가져오기

To read records, obtain a shard iterator with the following command:
레코드를 읽으려면 다음 명령어로 샤드 이터레이터를 가져옵니다:

```bash
aws kinesis get-shard-iterator --stream-name DemoStream --shard-id shardId-0000000000000 --shard-iterator-type TRIM_HORIZON
```

The TRIM\_HORIZON shard iterator type


reads from the very beginning of the stream, retrieving all records sent so far.
TRIM\_HORIZON 샤드 이터레이터는 스트림의 처음부터 읽어 지금까지 전송된 모든 레코드를 가져옵니다.

Alternatively, you can use LATEST to read only new records from the time the command is run.
또는 LATEST를 사용해 명령 실행 시점 이후의 새 레코드만 읽을 수 있습니다.

This command returns a ShardIterator string, which you use to fetch records.
이 명령은 ShardIterator 문자열을 반환하며, 이를 사용해 레코드를 가져옵니다.

---

## Retrieving Records

## 레코드 가져오기

Use the get-records command with the shard iterator to retrieve records:
샤드 이터레이터를 사용하여 get-records 명령으로 레코드를 가져옵니다:

```bash
aws kinesis get-records --shard-iterator <ShardIterator>
```

The response includes a batch of records with partition keys and base64-encoded data, along with timestamps.
응답에는 파티션 키와 base64 인코딩된 데이터, 타임스탬프가 포함된 레코드 배치가 반환됩니다.

To read the data, decode the base64-encoded strings using an online decoder or programmatically.
데이터를 읽으려면 base64 인코딩 문자열을 온라인 디코더나 프로그램으로 디코딩합니다.

For example, decoding the data reveals messages like user signup and user login, matching what was sent.
예: 디코딩하면 user signup, user login 등 전송된 메시지가 확인됩니다.

The response also includes a NextShardIterator value, which you use in subsequent get-records calls to continue reading from where you left off.
응답에는 NextShardIterator 값도 포함되어 있으며, 이후 get-records 호출 시 이 값을 사용해 이어서 읽습니다.

This iteration must be managed in your code.
이터레이션 관리는 코드에서 직접 처리해야 합니다.

---

## Summary

## 요약

We have successfully produced data to and consumed data from a Kinesis Data Stream using AWS CLI in CloudShell.
CloudShell의 AWS CLI를 사용하여 Kinesis 데이터 스트림에 데이터를 생성하고 소비하는 데 성공했습니다.

This low-level approach requires managing shard iterators manually.
저수준 접근 방식은 샤드 이터레이터를 수동으로 관리해야 합니다.

For more advanced consumption, consider using the Kinesis Client Library.
더 고급 소비를 위해 Kinesis Client Library 사용을 고려하세요.

Keep the stream open as we will use it for Kinesis Data Firehose in the next lecture.
다음 강의에서 Kinesis Data Firehose 실습에 사용하므로 스트림을 그대로 유지합니다.

---

## Key Takeaways

## 핵심 요약

* Created and configured a Kinesis Data Stream named DemoStream with one shard.

* 샤드 1개로 DemoStream Kinesis 데이터 스트림 생성 및 구성 완료.

* Explored the differences between On-demand and Provisioned modes for stream capacity.

* 스트림 용량 모드인 온디맨드와 프로비저닝 모드의 차이점 학습.

* Used AWS CLI in CloudShell to produce and consume records from the Kinesis Data Stream.

* CloudShell AWS CLI를 사용하여 Kinesis 데이터 스트림에서 레코드 생성 및 소비.

* Demonstrated decoding base64-encoded data retrieved from the stream to verify message content.

* 스트림에서 가져온 base64 인코딩 데이터를 디코딩하여 메시지 내용 검증.


