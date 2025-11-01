# S3 Express One Zone  
# S3 익스프레스 원존  

---

## Introduction to S3 Express One Zone Storage Class  
## S3 익스프레스 원존 스토리지 클래스 소개  

In this lecture, we discuss one more storage class, the S3 Express One Zone.  
이번 강의에서는 또 다른 스토리지 클래스인 S3 Express One Zone에 대해 다룹니다.  

This storage class is somewhat different from the others, which is why it merits a separate lecture.  
이 클래스는 다른 스토리지 클래스와 다소 달라 별도의 강의가 필요합니다.  
👉 설명: 기존 클래스와 구조 및 성능이 달라 독립적으로 학습 필요.  

---

## The S3 Express One Zone storage class is a high-performance option designed specifically for a single availability zone type of storage.  
S3 Express One Zone 스토리지 클래스는 단일 가용 영역 전용으로 설계된 고성능 옵션입니다.  

---

## What Does Single Availability Zone Mean?  
## 단일 가용 영역(Single Availability Zone)이란 무엇인가?  

This means that your objects are stored not in the standard S3 bucket, but in what is called a directory bucket.  
이는 객체가 표준 S3 버킷이 아닌, 디렉터리 버킷이라고 불리는 특별한 버킷에 저장된다는 의미입니다.  

This is a special type of S3 bucket.  
특별한 유형의 S3 버킷입니다.  

Unlike standard buckets that are distributed across multiple availability zones, this bucket is located in a single availability zone only.  
표준 버킷은 여러 AZ에 분산되지만, 이 버킷은 단일 AZ에만 위치합니다.  

You get to choose which availability zone you want it to be in.  
사용자가 원하는 AZ를 선택할 수 있습니다.  

Therefore, it is a different kind of bucket, which is why there is a different kind of storage class as well.  
따라서 다른 형태의 버킷이므로, 별도의 스토리지 클래스가 존재합니다.  

---

## Performance Characteristics  
## 성능 특성  

Because the storage is confined to a single availability zone, you can handle hundreds of thousands of requests per second with single-digit millisecond latency, resulting in very high performance.  
단일 AZ에 저장되므로, 초당 수십만 요청을 단일 숫자 밀리초 지연으로 처리할 수 있어 매우 높은 성능을 제공합니다.  

You get about 10 times the performance of S3 Standard with approximately 50% lower cost.  
S3 Standard 대비 약 10배 성능에 비용은 약 50% 절감됩니다.  

---

## Durability and Availability  
## 내구성 및 가용성  

The durability is good; however, the availability is lower compared to standard S3 storage because instead of replication across three availability zones, the data resides in only one availability zone.  
내구성은 우수하지만, 표준 S3처럼 세 개 AZ에 복제되지 않고 단일 AZ에만 존재하므로 가용성은 낮습니다.  

If there is a problem in this single availability zone, you will be directly affected.  
단일 AZ에 문제가 생기면 서비스가 직접적으로 영향을 받습니다.  

---

## Use Case and Benefits  
## 사용 사례 및 장점  

The idea behind using S3 Express One Zone is to co-locate your storage and compute resources within the same availability zone.  
S3 Express One Zone 사용 아이디어는 스토리지와 컴퓨팅 자원을 동일 AZ에 배치하는 것입니다.  

This reduces latency and may also reduce networking costs.  
이를 통해 지연 시간을 줄이고 네트워크 비용도 절감할 수 있습니다.  

It is ideal for latency-sensitive applications, data-intensive applications, AI and machine learning training, financial modeling, media processing, and high-performance computing.  
지연에 민감한 애플리케이션, 데이터 집약적 애플리케이션, AI/ML 학습, 금융 모델링, 미디어 처리, HPC에 이상적입니다.  

---

## Integration with AWS Services  
## AWS 서비스 통합  

S3 Express One Zone is best integrated with services such as SageMaker Model Training, Athena, EMR, and Glue, which are data services that benefit from this storage class.  
S3 Express One Zone은 SageMaker 모델 학습, Athena, EMR, Glue 등 데이터 중심 서비스와 최적 통합됩니다.  

---

## Conclusion  
## 결론  

That concludes this lecture on the S3 Express One Zone storage class.  
이로써 S3 Express One Zone 스토리지 클래스 강의를 마칩니다.  

I hope you found it informative, and I look forward to seeing you in the next lecture.  
유익한 강의였길 바라며, 다음 강의에서 만나요.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Express One Zone is a high-performance storage class designed for a single availability zone.  
- S3 Express One Zone은 단일 AZ 전용 고성능 스토리지 클래스입니다.  

- It stores objects in a special directory bucket limited to one availability zone chosen by the user.  
- 객체를 사용자가 선택한 단일 AZ에 한정된 디렉터리 버킷에 저장합니다.  

- Offers about 10 times the performance of S3 Standard with approximately 50% lower cost.  
- S3 Standard 대비 약 10배 성능에 비용은 약 50% 절감됩니다.  

- Ideal for latency-sensitive and data-intensive applications such as AI/ML training and financial modeling.  
- AI/ML 학습, 금융 모델링 등 지연 민감 및 데이터 집약적 애플리케이션에 이상적입니다.  

🎮 **게임보상:**

* **S3 Express One Zone 강의 완료!**

  * 단일 AZ 이해 +10
  * 성능/비용 비교 +15
  * 사용 사례 이해 +15
    총 **40 XP 획득!** 🎉
