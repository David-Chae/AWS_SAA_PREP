# S3 Replication  
# S3 복제  

---

## Introduction to Amazon S3 Replication  
## Amazon S3 복제 소개  

Now, let us discuss Amazon S3 Replication.  
이제 Amazon S3 복제 기능에 대해 알아보겠습니다.  
👉 설명: S3 복제는 데이터의 안전성과 가용성을 높이는 방법 중 하나입니다.  

There are two types of replication available.  
복제에는 두 가지 유형이 있습니다.  

- Cross-Region Replication (CRR)  
- 크로스 리전 복제(CRR)  

- Same-Region Replication (SRR)  
- 동일 리전 복제(SRR)  

---

## Concept of S3 Replication  
## S3 복제 개념  

The concept involves having an S3 bucket in one region and a target S3 bucket in another region.  
한 리전에 소스 S3 버킷을 두고, 다른 리전에 대상 S3 버킷을 두는 것이 기본 개념입니다.  

The goal is to establish asynchronous replication between these two buckets.  
목표는 두 버킷 사이에 비동기 복제를 설정하는 것입니다.  
👉 설명: 비동기 복제는 실시간이 아닌 백그라운드에서 데이터가 복사됨.  

To enable replication, versioning must be activated on both the source and the destination buckets.  
복제를 활성화하려면 소스와 대상 버킷 모두에서 버전 관리가 활성화되어 있어야 합니다.  

For Cross-Region Replication (CRR), the two regions must be different.  
CRR의 경우, 두 리전이 서로 달라야 합니다.  

For Same-Region Replication (SRR), the two regions are the same.  
SRR의 경우, 두 리전이 동일합니다.  

It is possible for these buckets to reside in different AWS accounts.  
이 버킷들은 서로 다른 AWS 계정에 존재할 수도 있습니다.  

The copying process occurs asynchronously, with the replication mechanism operating behind the scenes in the background.  
복사 과정은 비동기적으로 진행되며, 복제 메커니즘은 백그라운드에서 자동으로 작동합니다.  

To make replication work, you must grant proper IAM permissions to the S3 service.  
복제를 작동시키려면 S3 서비스에 적절한 IAM 권한을 부여해야 합니다.  

This allows it to read from and write to the specified buckets.  
이를 통해 S3가 지정된 버킷에서 데이터를 읽고 쓸 수 있게 됩니다.  

---

## Use Cases for S3 Replication  
## S3 복제 사용 사례  

The use cases for replication are diverse:  
복제의 사용 사례는 다양합니다.  

### Cross-Region Replication (CRR)  
### 크로스 리전 복제(CRR)  

- Useful for compliance requirements.  
- 규정 준수 요구 사항에 유용합니다.  

- Provides lower latency access to data by placing it in another region.  
- 데이터를 다른 리전에 두어 지연 시간을 줄입니다.  

- Enables replication of data across different AWS accounts.  
- 서로 다른 AWS 계정 간 데이터 복제를 가능하게 합니다.  

### Same-Region Replication (SRR)  
### 동일 리전 복제(SRR)  

- Helpful for aggregating logs across multiple S3 buckets.  
- 여러 S3 버킷의 로그를 집계하는 데 도움이 됩니다.  

- Facilitates live replication between production and test accounts, allowing for a dedicated test environment.  
- 프로덕션 계정과 테스트 계정 간 실시간 복제를 가능하게 하여 전용 테스트 환경을 제공합니다.  

---

## Conclusion  
## 결론  

That concludes the discussion on replication.  
이로써 S3 복제에 대한 설명을 마칩니다.  

We will continue with practical examples in the next lecture.  
다음 강의에서는 실습 예제를 통해 이어서 설명할 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 Replication comes in two types: Cross-Region Replication (CRR) and Same-Region Replication (SRR).  
- Amazon S3 복제는 두 가지 유형이 있습니다: 크로스 리전 복제(CRR)와 동일 리전 복제(SRR).  

- Versioning must be enabled on both source and destination buckets for replication to function.  
- 복제를 사용하려면 소스와 대상 버킷 모두에서 버전 관리가 활성화되어야 합니다.  

- Proper IAM permissions are required to allow S3 to read and write between buckets.  
- S3가 버킷 간 데이터를 읽고 쓸 수 있도록 적절한 IAM 권한이 필요합니다.  

- CRR is useful for compliance, lower latency, and cross-account replication; SRR is useful for log aggregation and live replication between environments.  
- CRR은 규정 준수, 낮은 지연 시간, 계정 간 복제에 유용하며, SRR은 로그 집계 및 환경 간 실시간 복제에 유용합니다.  

---

🎮 **게임보상:**

* **“S3 복제 학습 완료!”**

  * CRR & SRR 이해 +25
  * 버전 관리 필요성 이해 +25
  * IAM 권한 역할 이해 +25
  * 실습 대비 개념 정리 +25

총 **100 XP 획득!** 🎉
