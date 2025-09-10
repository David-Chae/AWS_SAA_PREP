# Amazon Kinesis Data Streams  
# 아마존 키네시스 데이터 스트림  

---

## Introduction to Amazon Kinesis Data Streams  
## 아마존 키네시스 데이터 스트림 소개  

Amazon Kinesis Data Streams is a service used to collect and store streaming data in real time.  
아마존 키네시스 데이터 스트림은 실시간으로 스트리밍 데이터를 수집하고 저장하는 서비스입니다.  

The key term to focus on is "real time."  
여기서 핵심 용어는 "실시간(real time)"입니다.  

---

## What is Real-Time Data?  
## 실시간 데이터란 무엇인가?  

Real-time data is data that is created and used immediately.  
실시간 데이터는 생성되자마자 즉시 사용되는 데이터를 의미합니다.  

Examples include:  
예시로는 다음과 같습니다:  

- Click streams generated whenever users click on a website.  
- 사용자가 웹사이트를 클릭할 때 생성되는 클릭 스트림.  

- Data from internet-connected devices, such as a connected bicycle.  
- 인터넷 연결 장치에서 수집되는 데이터, 예: 연결된 자전거.  

- Metrics and logs from servers that need to be used directly.  
- 서버에서 직접 사용해야 하는 메트릭과 로그 데이터.  

---

## Producers Sending Data to Kinesis Data Streams  
## 키네시스 데이터 스트림으로 데이터를 전송하는 프로듀서  

To send data into Kinesis Data Streams, producers are used.  
키네시스 데이터 스트림에 데이터를 보내기 위해 프로듀서를 사용합니다.  

Producers can be:  
프로듀서에는 다음이 포함될 수 있습니다:  

- Applications: Code written to take data from websites or devices and send it into Kinesis Data Streams.  
- 애플리케이션: 웹사이트나 장치에서 데이터를 가져와 키네시스로 전송하는 코드.  

- Kinesis Agents: Installed on servers to act as producers for metrics and logs.  
- 키네시스 에이전트: 서버에 설치되어 메트릭과 로그 데이터를 프로듀서 역할로 전송.  

Data is sent into Kinesis Data Streams in real time as it happens.  
데이터는 발생 즉시 실시간으로 키네시스 데이터 스트림에 전송됩니다.  

This allows consumer applications to consume and leverage the data immediately.  
이를 통해 컨슈머 애플리케이션이 데이터를 즉시 활용할 수 있습니다.  

---

## Consumers of Kinesis Data Streams  
## 키네시스 데이터 스트림의 컨슈머  

Consumers can be:  
컨슈머는 다음과 같습니다:  

- Applications that read data from Kinesis Data Streams (requiring code to be written).  
- 키네시스 데이터 스트림에서 데이터를 읽는 애플리케이션(코드 작성 필요).  

- AWS Lambda functions that can read from the streams.  
- 스트림에서 데이터를 읽을 수 있는 AWS Lambda 함수.  

- Amazon Data Firehose (covered in a future lecture).  
- 아마존 데이터 파이어호스(Amazon Data Firehose, 추후 강의에서 다룸).  

- Analytics services such as the Managed Service for Apache Flink.  
- Apache Flink 관리형 서비스와 같은 분석 서비스.  

---

## Features of Kinesis Data Streams  
## 키네시스 데이터 스트림 특징  

- Data retention on the stream can last up to 365 days.  
- 스트림의 데이터 보존 기간은 최대 365일입니다.  

- Because data is persisted, consumers can reprocess or replay data.  
- 데이터가 저장되므로, 컨슈머는 데이터를 재처리하거나 재생(replay)할 수 있습니다.  

- Once data is sent into Kinesis Data Streams, it cannot be deleted manually; it expires based on retention time.  
- 데이터가 키네시스로 전송되면 수동 삭제가 불가능하며, 보존 기간에 따라 만료됩니다.  

- Data records up to one megabyte can be sent.  
- 최대 1MB 크기의 데이터 레코드를 전송할 수 있습니다.  

- Typical use cases involve many small real-time data points.  
- 일반적인 사용 사례는 많은 작은 실시간 데이터 포인트입니다.  

---

## Data Ordering and Partitioning  
## 데이터 순서 및 파티셔닝  

Data is ordered if two data points share the same Partition ID.  
두 데이터 포인트가 동일한 파티션 ID를 가지면 데이터가 순서대로 정렬됩니다.  

This allows related data points to be grouped in time by sharing the same Partition ID.  
같은 파티션 ID를 공유하여 관련 데이터 포인트를 시간 순으로 그룹화할 수 있습니다.  

---

## Security Features  
## 보안 기능  

- At-rest encryption using AWS Key Management Service (KMS).  
- AWS KMS를 사용한 데이터 저장 시 암호화.  

- In-flight encryption using HTTPS.  
- HTTPS를 사용한 전송 중 데이터 암호화.  

---

## Optimized Producer and Consumer Applications  
## 최적화된 프로듀서 및 컨슈머 애플리케이션  

- Use the Kinesis Producer Library (KPL) to write optimized producer applications for high throughput.  
- Kinesis Producer Library(KPL)를 사용하여 높은 처리량을 위한 최적화된 프로듀서 애플리케이션 작성.  

- Use the Kinesis Client Library (KCL) to write optimized consumer applications.  
- Kinesis Client Library(KCL)를 사용하여 최적화된 컨슈머 애플리케이션 작성.  

---

## Capacity Modes of Kinesis Data Streams  
## 키네시스 데이터 스트림 용량 모드  

Kinesis Data Streams offers two capacity modes:  
키네시스 데이터 스트림은 두 가지 용량 모드를 제공합니다:  

### Provisioned Mode  
### 프로비저닝 모드  

- You choose the number of shards in your stream.  
- 스트림의 샤드 수를 선택합니다.  

- A shard represents the size of your stream.  
- 샤드는 스트림의 크기를 나타냅니다.  

- You can have from one to 1,000 shards.  
- 1~1,000개의 샤드를 가질 수 있습니다.  

- Each shard provides:  
- 각 샤드는 다음을 제공합니다:  

  - 1 megabyte per second or 1,000 records per second of write capacity.  
  - 초당 1MB 또는 초당 1,000 레코드 쓰기 용량.  

  - 2 megabytes per second of read capacity.  
  - 초당 2MB 읽기 용량.  

- To send 10,000 records per second or 10 megabytes per second, you need 10 shards.  
- 초당 10,000 레코드 또는 10MB를 전송하려면 10개의 샤드가 필요합니다.  

- You can manually scale the number of shards up or down.  
- 샤드 수를 수동으로 조정할 수 있습니다.  

- Monitoring throughput is necessary to determine the required number of shards.  
- 필요한 샤드 수를 결정하려면 처리량 모니터링이 필요합니다.  

- You pay for each shard provisioned per hour.  
- 프로비저닝된 샤드마다 시간당 요금이 부과됩니다.  

### On-Demand Mode  
### 온디맨드 모드  

- No need to provision or manage capacity.  
- 용량을 사전에 설정하거나 관리할 필요가 없습니다.  

- Default capacity provision is about 4,000 records per second or 4 megabytes per second.  
- 기본 용량은 초당 약 4,000 레코드 또는 4MB입니다.  

- Kinesis Data Streams automatically scales based on observed throughput over the past 30 days.  
- 키네시스 데이터 스트림은 지난 30일 관찰된 처리량을 기반으로 자동 확장됩니다.  

- You pay per stream per hour and are billed based on the amount of data ingested and egressed.  
- 스트림별 시간당 요금을 지불하며, 입력 및 출력된 데이터 양에 따라 청구됩니다.  

---

## Conclusion  
## 결론  

This concludes the overview of Amazon Kinesis Data Streams.  
이로써 아마존 키네시스 데이터 스트림 개요를 마칩니다.  

It is a powerful service for real-time data streaming with flexible capacity modes and strong security features.  
유연한 용량 모드와 강력한 보안 기능을 갖춘 실시간 데이터 스트리밍 서비스입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon Kinesis Data Streams is a real-time service for collecting and storing streaming data.  
- 아마존 키네시스 데이터 스트림은 실시간 스트리밍 데이터를 수집하고 저장하는 서비스입니다.  

- Producers send data into Kinesis Data Streams, which can be applications or Kinesis Agents.  
- 프로듀서는 애플리케이션 또는 Kinesis 에이전트를 통해 데이터를 스트림으로 전송합니다.  

- Data retention can last up to 365 days, allowing for replay and reprocessing of data.  
- 데이터 보존 기간은 최대 365일이며, 재생 및 재처리가 가능합니다.  

- Kinesis Data Streams offers two capacity modes: Provisioned (manual shard scaling) and On-demand (automatic scaling).  
- 키네시스 데이터 스트림은 두 가지 용량 모드를 제공합니다: 프로비저닝(수동 샤드 조정) 및 온디맨드(자동 확장).  
