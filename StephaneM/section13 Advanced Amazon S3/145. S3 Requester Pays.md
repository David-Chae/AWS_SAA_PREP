# S3 Requester Pays  
# S3 요청자 부담(Requester Pays)  

---

## Introduction to S3 Requester Pays  
## S3 Requester Pays 소개  

Here is a feature that you may be tested on in the exam.  
다음은 시험에서 출제될 수 있는 기능입니다.  

This feature is called S3 Requester Pays.  
이 기능의 이름은 **S3 Requester Pays**입니다.  

The name itself is quite self-explanatory.  
이름 그대로 이해하기 쉽습니다.  

---

## Default Billing Model in Amazon S3  
## Amazon S3 기본 과금 모델  

In general, from what we have seen, the bucket owners pay for all of the Amazon S3 storage and also the data transfer costs associated with their buckets.  
일반적으로, 버킷 소유자가 해당 버킷의 저장 비용과 데이터 전송 비용을 모두 지불합니다.  

For example, if we have a set of buckets storing some objects, and a requester (a user) downloads a file from our bucket, then the networking cost is billed to the owner of the bucket and the objects.  
예를 들어, 버킷에 객체를 저장하고 있고, 사용자가 해당 객체를 다운로드하면, 네트워크 비용은 버킷 소유자에게 청구됩니다.  

---

## Enabling Requester Pays  
## Requester Pays 활성화  

However, if you have a lot of heavy files and some customers want to download them, you might want to enable Requester Pays buckets.  
하지만 큰 파일이 많고 일부 고객이 다운로드를 원한다면 Requester Pays를 활성화할 수 있습니다.  

In that case, the requester will pay instead of the bucket owner for the data download of the objects.  
이 경우, 다운로드 비용은 버킷 소유자가 아닌 요청자가 부담합니다.  

---

## Billing Responsibilities with Requester Pays  
## Requester Pays 시 과금 책임  

To clarify with an example, the owner still pays for the storage costs of the objects within the bucket.  
예시로, 버킷 소유자는 여전히 객체의 저장 비용을 지불합니다.  

However, when the requester downloads the object, the requester will be the one paying for the networking costs associated with that download.  
하지만 요청자가 객체를 다운로드하면, 네트워크 비용은 요청자가 지불합니다.  

---

## Use Case and Authentication Requirement  
## 사용 사례 및 인증 요구 사항  

The idea behind Requester Pays is very helpful if you want to start sharing large data sets with other AWS accounts.  
Requester Pays는 다른 AWS 계정과 큰 데이터를 공유할 때 유용합니다.  

For this to work, the requester must not be anonymous; they must be authenticated in AWS.  
이 기능을 사용하려면 요청자는 익명일 수 없으며 AWS에서 인증되어야 합니다.  

When the requester is authenticated, AWS knows to bill the requester for that specific download of the object.  
요청자가 인증되면, AWS는 해당 다운로드 비용을 요청자에게 청구합니다.  

---

## Summary  
## 요약  

This is a feature to remember as it can come up in exam scenarios.  
시험 문제에 나올 수 있는 기억할 기능입니다.  

It shifts the data transfer cost from the bucket owner to the requester, which is useful for sharing large datasets securely and cost-effectively.  
데이터 전송 비용을 버킷 소유자에서 요청자로 전환하여, 큰 데이터를 안전하고 비용 효율적으로 공유할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- By default, bucket owners pay for both storage and data transfer costs in Amazon S3.  
- 기본적으로 S3에서는 버킷 소유자가 저장 및 데이터 전송 비용을 모두 부담합니다.  

- Enabling Requester Pays shifts the data transfer cost to the requester instead of the bucket owner.  
- Requester Pays를 활성화하면 전송 비용이 버킷 소유자에서 요청자로 전환됩니다.  

- Requester Pays is useful for sharing large datasets with other AWS accounts.  
- Requester Pays는 큰 데이터를 다른 AWS 계정과 공유할 때 유용합니다.  

- The requester must be authenticated in AWS for billing to be correctly assigned.  
- 정확한 과금 처리를 위해 요청자는 AWS에서 인증되어야 합니다.  

🎮 **게임보상:**

* **S3 Requester Pays 학습 완료!**

  * 기본 과금 모델 이해 +10
  * 요청자 부담 전환 원리 이해 +15
  * 인증 필요성 이해 +10
    총 **35 XP 획득!** 🎉
