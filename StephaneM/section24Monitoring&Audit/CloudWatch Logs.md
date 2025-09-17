```markdown
# CloudWatch Logs  
# 클라우드워치 로그  
→ AWS 내에서 애플리케이션 로그를 저장하고 분석하기 위한 서비스임을 소개하는 제목.  

---

## Introduction to CloudWatch Logs  
## 클라우드워치 로그 소개  
→ CloudWatch Logs의 기본 개념과 역할을 설명하는 섹션.  

CloudWatch Logs is the ideal service for storing your application logs within AWS.  
클라우드워치 로그는 AWS 내에서 애플리케이션 로그를 저장하기에 최적의 서비스입니다.  
→ 로그 중앙화 및 관리 기능 제공.  

To begin using CloudWatch Logs, you first define log groups.  
클라우드워치 로그를 사용하려면 먼저 로그 그룹을 정의해야 합니다.  
→ 로그를 카테고리별로 모아두는 단위.  

These log groups can be named as you wish, typically representing one of your applications.  
이 로그 그룹은 원하는 이름을 지정할 수 있으며, 일반적으로 하나의 애플리케이션을 나타냅니다.  
→ 예: 쇼핑몰 서비스용 로그 그룹.  

Within each log group, there are multiple log streams.  
각 로그 그룹에는 여러 로그 스트림이 있습니다.  
→ 세부 단위 로그 모음.  

These log streams represent individual log instances within an application, such as specific log files or containers that are part of a cluster.  
이 로그 스트림은 애플리케이션 내 개별 로그 인스턴스를 나타내며, 예를 들어 특정 로그 파일이나 클러스터 내 컨테이너입니다.  
→ 로그 그룹 안의 세부 실행 단위 기록.  

You also define your log expiration policy.  
또한 로그 만료 정책을 정의할 수 있습니다.  
→ 로그를 얼마나 오래 보관할지 설정.  

Logs can be retained indefinitely, meaning they never expire, or you can set expiration periods ranging from one day up to ten years.  
로그는 무기한 보관할 수도 있고, 1일에서 10년까지 보관 기간을 설정할 수도 있습니다.  
→ 장기 보관 vs 단기 보관 옵션.  

CloudWatch Logs can be sent to various destinations.  
클라우드워치 로그는 다양한 목적지로 전송될 수 있습니다.  
→ 로그 활용도를 높이는 기능.  

For example, you can export logs in batch to Amazon S3 or stream them into Kinesis Data Streams, Kinesis Data Firehose, AWS Lambda, or Amazon OpenSearch Service.  
예를 들어 로그를 일괄적으로 Amazon S3에 내보내거나 Kinesis Data Streams, Kinesis Data Firehose, AWS Lambda, Amazon OpenSearch Service로 스트리밍할 수 있습니다.  
→ 배치 처리 vs 실시간 스트리밍.  

All logs are encrypted by default, and you can configure your own KMS-based encryption with custom keys if desired.  
모든 로그는 기본적으로 암호화되며, 필요시 KMS 기반 사용자 지정 키 암호화를 설정할 수 있습니다.  
→ 보안 강화 옵션.  

---

## Sources of Log Data  
## 로그 데이터의 소스  
→ 로그를 클라우드워치에 보내는 방법과 데이터 출처 설명.  

Logs can be sent to CloudWatch Logs using the SDK, the CloudWatch Logs Agent, or the CloudWatch Unified Agent.  
SDK, CloudWatch Logs Agent, 또는 CloudWatch Unified Agent를 통해 로그를 클라우드워치 로그로 보낼 수 있습니다.  
→ 다양한 전송 방식 존재.  

The CloudWatch Unified Agent is the current recommended agent, as the CloudWatch Logs Agent is now deprecated.  
현재는 CloudWatch Logs Agent가 사용 중지되었으므로 Unified Agent를 권장합니다.  
→ 최신 방식 사용 권장.  

Various AWS services send logs directly to CloudWatch Logs:  
여러 AWS 서비스는 로그를 클라우드워치 로그로 직접 전송합니다:  

Elastic Beanstalk collects application logs directly.  
Elastic Beanstalk는 애플리케이션 로그를 직접 수집합니다.  

ECS sends logs from containers.  
ECS는 컨테이너에서 로그를 전송합니다.  

Lambda sends logs from functions.  
Lambda는 함수에서 로그를 전송합니다.  

VPC Flow Logs provide metadata on network traffic.  
VPC Flow Logs는 네트워크 트래픽의 메타데이터를 제공합니다.  

API Gateway logs all requests.  
API Gateway는 모든 요청을 기록합니다.  

CloudTrail sends logs based on filters.  
CloudTrail은 필터를 기반으로 로그를 전송합니다.  

Route53 logs all DNS queries.  
Route53은 모든 DNS 쿼리를 기록합니다.  

---

## Querying Logs with CloudWatch Logs Insights  
## 클라우드워치 로그 인사이트로 로그 쿼리  
→ 로그 분석을 위한 쿼리 도구 설명.  

CloudWatch Logs Insights is a querying capability within CloudWatch Logs that allows you to write queries against your log data.  
클라우드워치 로그 인사이트는 로그 데이터를 대상으로 쿼리를 작성할 수 있는 기능입니다.  
→ SQL 유사 쿼리 기능.  

You specify the timeframe for your query, and the service returns results with visualizations.  
쿼리 시간 범위를 지정하면 서비스가 시각화된 결과를 반환합니다.  
→ 데이터 분석 효율 증가.  

You can also view the specific log lines that contributed to the visualization.  
또한 시각화에 기여한 특정 로그 라인을 확인할 수 있습니다.  
→ 원인 추적 가능.  

These visualizations can be exported as results or added to dashboards for easy rerunning.  
이 시각화 결과는 내보내거나 대시보드에 추가해 재사용할 수 있습니다.  
→ 반복적인 분석 자동화.  

CloudWatch Logs Insights provides many simple queries in the console...  
클라우드워치 로그 인사이트는 콘솔에서 다양한 간단한 쿼리를 제공합니다...  
→ 예: 최근 25개 이벤트 찾기, 오류 건수 세기, 특정 IP 검색 등.  

It uses a purpose-built query language where all fields are automatically detected from the logs.  
로그에서 모든 필드가 자동으로 탐지되는 전용 쿼리 언어를 사용합니다.  
→ 학습 부담 감소.  

You can filter... calculate aggregate statistics... query multiple log groups simultaneously...  
조건 기반 필터링, 집계 통계 계산, 여러 로그 그룹 동시 쿼리도 가능합니다.  
→ 멀티 계정/멀티 그룹 지원.  

Note that CloudWatch Logs Insights is a query engine for historical data and is not a real-time engine.  
클라우드워치 로그 인사이트는 과거 데이터를 위한 쿼리 엔진이며 실시간 엔진은 아닙니다.  
→ 실시간 분석이 아니라 배치 분석 도구임.  

---

## Exporting CloudWatch Logs  
## 클라우드워치 로그 내보내기  
→ 로그를 다른 서비스로 보내는 방법 설명.  

CloudWatch Logs can be exported to several destinations. The first is Amazon S3...  
클라우드워치 로그는 여러 목적지로 내보낼 수 있습니다. 첫 번째는 Amazon S3입니다...  
→ 배치로 내보내며 최대 12시간 소요.  

For real-time or near real-time processing, you use CloudWatch Logs subscriptions.  
실시간 또는 준실시간 처리를 위해서는 클라우드워치 로그 구독을 사용합니다.  
→ 스트리밍 방식.  

Subscription filters...  
구독 필터는 로그 이벤트를 실시간으로 Kinesis, Firehose, Lambda 등으로 보냅니다.  
→ 데이터 파이프라인 연결.  

Aggregation across accounts and regions is possible.  
여러 계정 및 리전의 로그를 하나로 집계할 수 있습니다.  
→ 중앙 집중형 로그 관리 가능.  

---

## Cross-Account Log Streaming Setup  
## 교차 계정 로그 스트리밍 설정  
→ 다른 계정 간 로그 스트리밍 방법 설명.  

To enable cross-account log streaming, you use what are called destinations...  
교차 계정 로그 스트리밍을 사용하려면 "목적지"를 사용합니다...  
→ 송신 계정과 수신 계정 구조.  

Destination policies and IAM roles must be set correctly.  
목적지 접근 정책과 IAM 역할을 올바르게 설정해야 합니다.  
→ 권한 관리 중요.  

Once these configurations are in place, you can send CloudWatch Logs data from one account into another.  
이 구성이 완료되면 한 계정의 로그를 다른 계정으로 전송할 수 있습니다.  
→ 멀티 계정 환경에서 활용 가능.  

---

## Conclusion  
## 결론  

This concludes the lecture on CloudWatch Logs...  
클라우드워치 로그에 대한 강의를 마칩니다...  
→ 로그 저장, 쿼리, 내보내기, 교차 계정 집계까지 다룸.  

---

## Key Takeaways  
## 핵심 요약  

- CloudWatch Logs stores application logs in AWS, organized into log groups and log streams.  
- 클라우드워치 로그는 로그 그룹과 스트림으로 애플리케이션 로그를 저장합니다.  

- Logs retention policies can be set from one day to ten years or indefinitely.  
- 로그 보관 정책은 1일~10년 또는 무기한으로 설정 가능합니다.  

- Logs can be exported in batch to Amazon S3 or streamed in near real-time...  
- 로그는 S3로 배치 내보내기 또는 Kinesis, Firehose, Lambda, OpenSearch로 실시간 스트리밍 가능합니다.  

- CloudWatch Logs Insights provides a query engine for analyzing log data...  
- 클라우드워치 로그 인사이트는 로그 데이터를 분석하는 쿼리 엔진과 시각화 기능을 제공합니다.  

---

🎉 **게임 보상**  
당신은 **+120 XP** 🏆를 획득했습니다!  
🔥 "로그 마스터" 업적 해제: CloudWatch Logs의 핵심 기능 완벽 정리 성공!  
```
