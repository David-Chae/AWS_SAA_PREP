
## **AWS Snow Family 개요**

### **AWS Snowball 개요**

AWS Snowball은 **안전하고 휴대 가능한 장치**로, 엣지(Edge) 환경에서 데이터를 수집하고 처리하거나, AWS로 데이터를 마이그레이션할 때 사용됩니다. 특히 **페타바이트 단위의 대용량 데이터**를 옮길 때 유용합니다.

---

### **Snowball Edge 장치 종류**

1. **Edge Storage Optimized**

   * 용량: 210TB
   * 주로 **대용량 데이터 저장**에 적합

2. **Edge Compute Optimized**

   * 용량: 28TB
   * **컴퓨팅 작업** 중심으로 설계
   * EC2 인스턴스나 Lambda 함수를 장치에서 바로 실행 가능

> 주요 차이점: **저장 용량과 용도**

---

### **데이터 마이그레이션의 어려움**

네트워크를 통해 대용량 데이터를 전송하는 것은 매우 시간이 걸립니다.

* 예시: 1Gbps 연결로 100TB 전송 → 약 12일 소요
* 문제점:

  * 제한된 연결 및 대역폭
  * 높은 네트워크 비용
  * 다른 애플리케이션과 대역폭 공유
  * 연결 불안정

> 데이터 전송이 1주 이상 걸리거나 어려움이 예상되면 Snowball 사용을 권장

---

### **Snowball 데이터 마이그레이션 과정**

1. Amazon S3에 직접 업로드하지 않고, **물리적 Snowball 장치**를 인프라로 받음
2. 데이터를 장치에 로드 후 AWS로 배송
3. AWS에서 Snowball 장치 데이터를 **S3 버킷**으로 가져옴

> 이렇게 하면 네트워크를 포화시키지 않고 대용량 데이터를 효율적으로 마이그레이션 가능

---

### **엣지 컴퓨팅 활용 사례**

Snowball은 인터넷 연결이 제한적이거나 없는 **원격 환경**에서도 데이터 처리 가능

* 예: 도로 위 트럭, 해상 선박, 광산 기지 등
* Compute Optimized 장치를 사용해 **장치에서 바로 EC2/Lambda 실행** 가능
* 데이터 처리 후 AWS로 전송 가능
* 용도: 데이터 전처리, 머신러닝, 미디어 트랜스코딩 등

---

### **요약**

AWS Snowball은 주로 두 가지 용도로 사용됩니다.

1. **데이터 마이그레이션**: 네트워크 대역폭에 의존하지 않고 대용량 데이터를 효율적으로 전송
2. **엣지 컴퓨팅**: 원격/오프라인 환경에서 장치 자체적으로 데이터 처리

> 다양한 시나리오에서 데이터 문제를 해결할 수 있는 **다목적 솔루션**

---

### **핵심 포인트**

* Snowball은 **안전하고 휴대 가능한 장치**로, 엣지에서 데이터 수집, 처리 및 AWS 간 데이터 이동 가능
* 장치 종류:

  * **Edge Storage Optimized**: 210TB, 저장 중심
  * **Edge Compute Optimized**: 28TB, 컴퓨팅 중심
* 대역폭이 제한적이거나 연결이 불안정한 환경에서 **물리적 데이터 이동**이 효율적
* 원격/오프라인 환경에서 Snowball 장치로 **엣지 컴퓨팅** 수행 가능 (EC2/Lambda 실행)

# AWS Snow Family Overview

## AWS Snowball Overview
AWS Snowball is a highly secure and portable device that enables you to collect and process data at the edge and migrate data in and out of AWS. It is particularly useful when migrating large volumes of data, such as petabytes.

## Snowball Edge Device Types
There are two types of Snowball edge devices:

- **Edge Storage Optimized**: Offers 210 terabytes of storage.
- **Edge Compute Optimized**: Provides 28 terabytes of storage and is designed primarily for compute tasks.

> The main difference between these devices lies in their storage capacity and intended use cases.

## Data Migration Challenges
Transferring large amounts of data over a network can be time-consuming. For example, transferring 100 terabytes over a one gigabit per second connection would take approximately 12 days. Challenges include:

- Limited connectivity and bandwidth
- High network costs
- Bandwidth sharing with other applications
- Unstable connections

> When data transfer takes over a week or faces such challenges, using a Snowball device is recommended.

## Snowball Data Migration Process
Instead of uploading data directly to Amazon S3, which may consume all your bandwidth, you receive a physical Snowball device at your infrastructure. You load the device with your data and then ship it back to AWS. AWS then imports the data from the Snowball device into an Amazon S3 bucket. This approach efficiently handles large data migrations without saturating your network.

## Edge Computing Use Case
Snowball devices also support edge computing scenarios where data is processed as it is created at remote or disconnected locations, such as trucks on the road, ships at sea, or mining stations. These locations may have limited or no internet access and limited compute power.

In such cases, the **Compute Optimized Snowball device** is used. It allows running EC2 instances or Lambda functions directly on the device to process data locally. After processing, data can be sent back to AWS. This enables pre-processing, machine learning, or media transcoding at the edge.

## Summary
The AWS Snowball service is primarily used for two purposes:

- **Data migrations**: Efficiently transferring large volumes of data to and from AWS without relying solely on network bandwidth.
- **Edge computing**: Processing data locally in remote or disconnected environments using Snowball devices with compute capabilities.

> This makes Snowball a versatile solution for handling data challenges in various scenarios.

## Key Takeaways
- AWS Snowball is a secure, portable device designed for data collection, processing at the edge, and data migration in and out of AWS.
- There are two Snowball edge device types: **Edge Storage Optimized** with 210 terabytes of storage, and **Edge Compute Optimized** with 28 terabytes, tailored for storage and compute use cases respectively.
- Data migration over networks with limited bandwidth or unstable connections can be time-consuming; Snowball devices offer an efficient alternative by physically transferring data.
- Edge computing use cases involve processing data locally on Snowball devices in remote or disconnected locations, enabling running EC2 instances or Lambda functions at the edge.
