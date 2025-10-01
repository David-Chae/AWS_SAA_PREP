# S3 Storage Lens  
# S3 스토리지 렌즈  

---

## Introduction to S3 Storage Lens  
## S3 스토리지 렌즈 소개  

S3 Storage Lens is a service designed to help you understand, analyze, and optimize storage across your entire AWS Organization.  
S3 스토리지 렌즈는 전체 AWS 조직의 스토리지를 이해하고, 분석하며, 최적화하도록 도와주는 서비스입니다.  

It enables you to discover anomalies, identify cost efficiencies, and apply protection best practices throughout your organization.  
이를 통해 이상 현상을 발견하고, 비용 효율성을 식별하며, 조직 전반에 데이터 보호 모범 사례를 적용할 수 있습니다.  

You receive 30-day usage and activity metrics, which can be aggregated at various levels such as the organization, specific accounts, regions, buckets, or even prefixes.  
30일 동안의 사용량 및 활동 지표를 제공하며, 조직, 계정, 리전, 버킷 또는 프리픽스 단위로 집계할 수 있습니다.  

You have the option to create your own dashboard or use the default dashboard provided by the Storage Lens service.  
사용자는 자체 대시보드를 생성하거나 Storage Lens 서비스에서 제공하는 기본 대시보드를 사용할 수 있습니다.  

All these metrics and reports can be exported into an S3 bucket in either CSV or Parquet format, facilitating further analysis or integration with other tools.  
모든 지표와 보고서는 CSV 또는 Parquet 형식으로 S3 버킷에 내보낼 수 있어 추가 분석이나 다른 도구와의 통합이 용이합니다.  

---

## Summary of Storage Lens Features  
## 스토리지 렌즈 기능 요약  

Storage Lens takes into account multiple dimensions such as organization, accounts, regions, and buckets.  
스토리지 렌즈는 조직, 계정, 리전, 버킷 등 여러 차원을 고려합니다.  

It aggregates this data into reports that assist with analysis.  
이 데이터를 보고서로 집계하여 분석에 도움을 줍니다.  

These reports provide summary insights, data protection recommendations, and cost efficiency suggestions, enabling you to optimize your Amazon S3 usage.  
보고서는 요약 통찰, 데이터 보호 권장 사항, 비용 효율성 제안을 제공하여 Amazon S3 사용을 최적화할 수 있도록 합니다.  

---

## Default Dashboard Overview  
## 기본 대시보드 개요  

When using the S3 Storage Lens service, you have access to a default dashboard.  
S3 스토리지 렌즈 서비스를 사용할 때 기본 대시보드를 이용할 수 있습니다.  

This dashboard provides summarized insights and trends for both free and advanced metrics.  
이 대시보드는 무료 및 고급 지표에 대한 요약 통찰과 트렌드를 제공합니다.  

It displays data across multiple regions and accounts without requiring special filter setup, as it is pre-configured by Amazon S3.  
Amazon S3에서 사전 구성했기 때문에 별도의 필터 설정 없이 여러 리전과 계정의 데이터를 표시합니다.  

While you cannot delete the default dashboard, you can disable it if desired.  
기본 대시보드는 삭제할 수 없지만, 필요 시 비활성화할 수 있습니다.  

The user interface allows you to select the regions, accounts, buckets, storage classes, and other filters you want to analyze.  
UI를 통해 분석할 리전, 계정, 버킷, 스토리지 클래스 및 기타 필터를 선택할 수 있습니다.  

This configuration is centralized for ease of management.  
이 구성이 중앙 집중화되어 관리가 용이합니다.  

The dashboard provides information such as total storage, object count, average object size, number of buckets, and accounts.  
대시보드는 총 스토리지, 객체 수, 평균 객체 크기, 버킷 수, 계정 수 등의 정보를 제공합니다.  

It also allows detailed views per account or per region.  
또한 계정별 또는 리전별 상세 보기 기능을 제공합니다.  

---

## Available Metrics in Storage Lens  
## 스토리지 렌즈에서 제공되는 지표  

Understanding the types of metrics available in Storage Lens can help determine if it is the right service for your needs, especially for exam preparation.  
스토리지 렌즈에서 제공되는 지표 유형을 이해하면 필요에 맞는 서비스인지 판단하는 데 도움이 되며, 시험 준비에도 유용합니다.  

### Summary Metrics  
### 요약 지표  

These provide general insights about your S3 storage, such as storage bytes to know the size of your storage and object counts to know how many objects you have.  
이 지표는 스토리지 크기 및 객체 수와 같은 S3 스토리지에 대한 일반적인 통찰을 제공합니다.  

Use cases include identifying the fastest-growing or unused buckets and prefixes by monitoring changes in storage bytes and object counts.  
사용 사례: 스토리지 바이트 및 객체 수 변화를 모니터링하여 가장 빠르게 성장하거나 사용되지 않는 버킷과 프리픽스를 식별  

### Cost Optimization Metrics  
### 비용 최적화 지표  

These metrics provide insights to manage and optimize your storage costs.  
이 지표는 스토리지 비용을 관리하고 최적화하는 통찰을 제공합니다.  

They include data such as non-current version storage bytes, indicating how much space is taken by versioned objects that are not current, and incomplete multi-part upload storage bytes, which show space consumed by incomplete uploads that can be cleaned up.  
예: 현재가 아닌 버전의 스토리지 바이트(사용되지 않는 버전 객체 공간), 미완료 멀티파트 업로드 바이트(정리 가능한 업로드 공간)  

Use cases for cost optimization metrics include identifying buckets with failed multi-part uploads and objects that could be transitioned to lower-cost storage classes.  
비용 최적화 지표 사용 사례: 실패한 멀티파트 업로드 버킷 식별, 낮은 비용 스토리지 클래스로 전환 가능한 객체 식별  

### Data Protection Metrics  
### 데이터 보호 지표  

These provide insights into data protection features such as the count of buckets with versioning enabled, MFA delete enabled, SSE-KMS enabled, and cross-region replication rules.  
버전 관리 활성화, MFA 삭제 활성화, SSE-KMS 활성화, 크로스 리전 복제 규칙 등 데이터 보호 기능 통찰 제공  

Use cases include identifying buckets that do not follow your data protection best practices.  
사용 사례: 데이터 보호 모범 사례를 따르지 않는 버킷 식별  

### Access Management Metrics  
### 접근 관리 지표  

These metrics provide insights into S3 bucket ownership settings, helping you identify which ownership configurations your buckets currently use.  
버킷 소유권 설정에 대한 통찰을 제공하여 현재 버킷이 사용하는 소유권 구성을 식별  

### Event Metrics  
### 이벤트 지표  

These provide insights into S3 event notifications, including how many buckets have event notifications configured.  
S3 이벤트 알림 통찰 제공, 알림이 구성된 버킷 수 포함  

### Performance Metrics  
### 성능 지표  

These metrics give insights into S3 transfer acceleration, showing how many buckets have transfer acceleration enabled.  
S3 전송 가속 통찰 제공, 가속이 활성화된 버킷 수 표시  

### Activity Metrics  
### 활동 지표  

These include information about all requests such as GET and PUT requests, the number of bytes downloaded, and more.  
GET/PUT 요청, 다운로드된 바이트 수 등 모든 요청 정보 포함  

### HTTP Status Code Metrics  
### HTTP 상태 코드 지표  

Metrics around HTTP status codes such as 200 OK, 403 Forbidden, and others help you understand the type of usage your buckets are receiving.  
200 OK, 403 Forbidden 등 HTTP 상태 코드 관련 지표를 통해 버킷 사용 유형 이해  

---

## Free vs. Paid Metrics  
## 무료 vs 유료 지표  

Storage Lens offers two categories of metrics: free and paid.  
스토리지 렌즈는 무료 지표와 유료 지표 두 가지를 제공합니다.  

The free metrics include around 28 usage metrics and are automatically available to all customers, with data retention for 14 days.  
무료 지표는 약 28개의 사용량 지표를 포함하며 모든 고객에게 자동 제공, 데이터 보존 기간 14일  

Advanced metrics and recommendations are part of the paid offering.  
고급 지표와 권장 사항은 유료 제공 항목입니다.  

These include additional metrics such as activity, advanced cost optimization, advanced data protection, and HTTP status codes.  
추가 지표: 활동, 고급 비용 최적화, 고급 데이터 보호, HTTP 상태 코드  

These metrics can also be published to CloudWatch at no additional charge.  
이 지표는 추가 비용 없이 CloudWatch에 게시 가능  

Paid metrics allow you to collect data at the prefix level within your S3 buckets, and the data retention period extends to 15 months.  
유료 지표는 S3 버킷의 프리픽스 수준 데이터 수집 가능, 데이터 보존 기간 최대 15개월  

---

## Conclusion  
## 결론  

S3 Storage Lens is a very helpful service for managing and optimizing your Amazon S3 storage.  
S3 스토리지 렌즈는 Amazon S3 스토리지를 관리하고 최적화하는 데 매우 유용한 서비스입니다.  

It is important to remember the differences between free and paid metrics, the default dashboard's coverage across multiple accounts and regions, and the comprehensive insights it provides into your object storage, including encryption status.  
무료 및 유료 지표 차이, 기본 대시보드의 여러 계정/리전 커버리지, 객체 스토리지에 대한 종합 통찰(암호화 상태 포함)을 기억하는 것이 중요합니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Storage Lens provides comprehensive metrics to analyze and optimize storage across an entire AWS Organization.  
- S3 스토리지 렌즈는 전체 AWS 조직의 스토리지를 분석하고 최적화할 수 있는 종합 지표 제공

* It offers both free and advanced paid metrics, including cost optimization, data protection, access management, and performance insights.

* 비용 최적화, 데이터 보호, 접근 관리, 성능 통찰 등 무료 및 유료 고급 지표 제공

* The default dashboard aggregates data across multiple accounts and regions and cannot be deleted but can be disabled.

* 기본 대시보드는 여러 계정과 리전의 데이터를 집계하며 삭제할 수 없지만 비활성화 가능

* Metrics and reports can be exported in CSV or Parquet format and are available for different retention periods depending on the metric type.

* 지표와 보고서는 CSV 또는 Parquet 형식으로 내보낼 수 있으며, 지표 유형에 따라 데이터 보존 기간이 다름

🎮 **게임보상:**  
- **S3 Storage Lens 학습 완료!**  
  - 서비스 개념 +10  
  - 지표 유형 이해 +15  
  - 무료/유료 차이 이해 +10  
총 **35 XP 획득!** 🎉
