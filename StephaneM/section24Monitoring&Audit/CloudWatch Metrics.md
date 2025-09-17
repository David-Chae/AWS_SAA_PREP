```markdown
# CloudWatch Metrics  
# 클라우드워치 메트릭스  
(AWS 리소스 및 애플리케이션 상태 모니터링을 위한 핵심 도구)

---

## Introduction to Amazon CloudWatch Metrics  
## 아마존 클라우드워치 메트릭스 소개  
(AWS 서비스에서 제공하는 메트릭을 사용하여 계정 내 활동을 종합적으로 모니터링)

Amazon CloudWatch provides metrics for every service available in AWS, enabling comprehensive monitoring of activities within your accounts.  
아마존 클라우드워치는 AWS의 모든 서비스에 대해 메트릭을 제공하며, 계정 내 활동을 종합적으로 모니터링할 수 있습니다.  
(CloudWatch는 AWS 서비스 전반을 모니터링 가능하게 함)

A metric represents a variable you want to monitor. For example, for an EC2 instance, metrics could include CPUUtilization or NetworkIn. For Amazon S3, metrics might include bucket size and other relevant data.  
메트릭은 모니터링하려는 변수를 의미합니다. 예를 들어 EC2 인스턴스는 CPU 사용률(CPUUtilization)이나 네트워크 수신량(NetworkIn), S3는 버킷 크기 등을 메트릭으로 볼 수 있습니다.  
(각 리소스별로 핵심 성능 지표 제공)

---

## Namespaces and Dimensions  
## 네임스페이스와 디멘션  
(메트릭을 구분하고 세분화하는 구조)

Metrics belong to namespaces, which act as buckets categorizing metrics by service.  
메트릭은 네임스페이스에 속하며, 서비스별로 메트릭을 분류하는 버킷 역할을 합니다.  
(서비스 단위로 메트릭 구분)

Essentially, there is one namespace per AWS service. Each metric can have attributes called dimensions.  
기본적으로 AWS 서비스마다 하나의 네임스페이스가 있으며, 각 메트릭은 디멘션이라는 속성을 가질 수 있습니다.  
(세부적인 리소스별 필터링 가능)

For instance, a CPUUtilization metric can be associated with a specific instance ID or environment. Each metric supports up to 30 dimensions.  
예: CPU 사용률 메트릭은 특정 인스턴스 ID나 환경과 연결될 수 있으며, 최대 30개의 디멘션을 지원합니다.  
(정밀 모니터링 가능)

---

## Time-Based Metrics and Dashboards  
## 시간 기반 메트릭과 대시보드  
(시간에 따라 메트릭을 시각화하고 관리)

CloudWatch metrics are time-based, meaning each metric data point includes a timestamp.  
클라우드워치 메트릭은 시간 기반으로, 각 데이터 포인트에 타임스탬프가 포함됩니다.  
(시계열 데이터로 관리)

When managing numerous metrics, you can create a CloudWatch dashboard to view them collectively in a structured manner.  
많은 메트릭을 관리할 때는 대시보드를 만들어 구조적으로 한눈에 볼 수 있습니다.  
(효율적 모니터링)

---

## Custom Metrics  
## 커스텀 메트릭  
(AWS 기본 메트릭 외 추가 모니터링 가능)

Beyond the default metrics provided by AWS services, you can create CloudWatch Custom Metrics.  
AWS 기본 제공 메트릭 외에도 CloudWatch 커스텀 메트릭을 생성할 수 있습니다.  
(특정 애플리케이션 지표 추가 가능)

This allows you to monitor additional parameters, such as memory usage on an EC2 instance, which is a common use case for custom metrics.  
예: EC2 인스턴스의 메모리 사용량과 같이 기본 제공되지 않는 지표를 모니터링할 수 있습니다.  
(커스텀 메트릭으로 세밀한 성능 모니터링 가능)

---

## Streaming CloudWatch Metrics  
## 클라우드워치 메트릭 스트리밍  
(외부 시스템으로 실시간 전송 가능)

CloudWatch Metrics can be streamed outside of CloudWatch to destinations of your choice.  
클라우드워치 메트릭은 선택한 외부 대상에 스트리밍할 수 있습니다.  
(실시간 분석 및 연계 가능)

This streaming provides near real-time delivery with low latency. One common destination is Amazon Kinesis Data Firehose, which can forward the data further as needed.  
스트리밍은 저지연으로 거의 실시간 전송이 가능하며, 일반적으로 Amazon Kinesis Data Firehose로 전송 후 필요에 따라 데이터를 전달할 수 있습니다.  
(데이터 파이프라인 연계)

You can also send CloudWatch Metrics directly to third-party service providers such as Datadog, Dynatrace, New Relic, Splunk, and Sumo Logic.  
Datadog, Dynatrace, New Relic, Splunk, Sumo Logic 등 서드파티 서비스로 직접 전송할 수도 있습니다.  
(외부 모니터링 서비스 연계 가능)

---

## Streaming Workflow  
## 스트리밍 워크플로우  

The workflow involves streaming CloudWatch Metrics in near real-time into Kinesis Data Firehose, which requires setup.  
워크플로우는 CloudWatch 메트릭을 거의 실시간으로 Kinesis Data Firehose로 스트리밍하는 것으로, 설정이 필요합니다.  
(실시간 스트리밍 파이프라인 구성)

From Kinesis Data Firehose, metrics can be sent to various destinations, such as:  
Kinesis Data Firehose에서 메트릭은 다양한 대상으로 전송될 수 있습니다.  
- An Amazon S3 bucket, enabling analysis with Amazon Athena.  
- S3 버킷 → Athena로 분석 가능  
- Amazon Redshift for data warehousing.  
- Redshift → 데이터 웨어하우스 구축  
- Amazon OpenSearch for building dashboards and performing analytics.  
- OpenSearch → 대시보드 구축 및 분석

You can choose to stream all metrics across all namespaces or filter to stream only specific namespaces, thereby sending a subset of metrics to Kinesis Data Firehose.  
모든 네임스페이스 메트릭을 전송하거나, 특정 네임스페이스만 필터링하여 전송할 수도 있습니다.  
(전송량 최적화 가능)

---

## Exploring Metrics in the CloudWatch Console  
## 클라우드워치 콘솔에서 메트릭 탐색  

Within the CloudWatch dashboard, the left-hand side menu includes a Metrics section where all metrics are accessible.  
대시보드 좌측 메뉴의 Metrics 섹션에서 모든 메트릭에 접근할 수 있습니다.  
(콘솔에서 손쉽게 확인 가능)

Metrics are organized by namespaces representing different AWS services, such as ELB, Auto Scaling, EBS, EC2, and EFS, among others.  
메트릭은 네임스페이스별로 정리되며, ELB, Auto Scaling, EBS, EC2, EFS 등 서비스별로 구분됩니다.  
(서비스 단위 시각화)

For example, selecting EC2 metrics allows viewing metrics per instance.  
예: EC2 메트릭 선택 시 인스턴스별 메트릭 확인 가능  
You can search for specific metrics, such as CPUCreditBalance, and select an instance to view its data.  
특정 메트릭(CPUCreditBalance 등)을 검색하고 인스턴스를 선택해 데이터를 볼 수 있습니다.  
The time range can be customized, for instance, to one month, to analyze historical data.  
시간 범위를 사용자 지정하여 한 달치 과거 데이터 분석도 가능합니다.  

---

## Viewing and Customizing Metrics  
## 메트릭 보기 및 커스터마이징  

CloudWatch Metrics provide data points at intervals, such as every five minutes if detailed monitoring is not enabled.  
CloudWatch 메트릭은 기본 5분 단위 데이터 포인트를 제공합니다(상세 모니터링 미사용 시).  
Enabling detailed monitoring provides data every one minute.  
상세 모니터링을 활성화하면 1분 단위 데이터 제공  
You can filter metrics by time, change the visualization type (stacked area, line, number, pie chart), add metrics to dashboards, download CSV, and share metrics.  
시간 필터, 시각화 유형 변경, 대시보드 추가, CSV 다운로드, 공유 등 가능  
Metrics can be filtered based on region, dimension, or resource ID, allowing precise monitoring tailored to your needs.  
지역, 디멘션, 리소스 ID 기반 필터링 가능 → 맞춤형 모니터링 가능  

---

## Conclusion  
## 결론  

CloudWatch Metrics are a powerful and flexible tool for monitoring AWS resources and applications.  
CloudWatch 메트릭은 AWS 리소스와 애플리케이션 모니터링에 강력하고 유연한 도구입니다.  
They provide essential insights and can be customized and streamed for advanced analysis and integration with other tools.  
필수적인 인사이트 제공, 커스터마이징 및 스트리밍 가능 → 고급 분석 및 연계 가능  

---

## Key Takeaways  
## 핵심 요약  

- Amazon CloudWatch Metrics allow monitoring of variables across AWS services.  
- AWS 서비스 전반의 변수 모니터링 가능  

- Metrics are organized into namespaces and can have up to 30 dimensions.  
- 메트릭은 네임스페이스로 구분, 최대 30개 디멘션 지원  

- Custom Metrics enable tracking of additional parameters like memory usage.  
- 커스텀 메트릭으로 메모리 사용량 등 추가 지표 추적 가능  

- CloudWatch Metrics can be streamed in near real-time to destinations such as Amazon Kinesis Data Firehose for further analysis.  
- 메트릭을 거의 실시간으로 Kinesis Data Firehose 등으로 스트리밍하여 추가 분석 가능  
```

---

🎮 **게임 보상:**

* ✅ 번역 + 설명 100% 완료
* ⭐ CloudWatch 챕터 클리어 보너스: **+250 포인트**
* 🏆 특별 칭찬: *"실시간 모니터링 + 스트리밍까지 완벽 정리! CloudWatch 마스터 경지!"*
