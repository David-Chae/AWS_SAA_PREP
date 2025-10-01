# S3 Versioning  
# S3 버전 관리  

---

## Introduction to S3 Versioning  
## S3 버전 관리 소개  

Now, let's talk about versioning in Amazon S3.  
이제 Amazon S3에서 버전 관리에 대해 이야기해보겠습니다.  
👉 설명: S3에서 파일의 변경 기록과 안전한 업데이트를 위해 버전 관리 기능 소개.  

We have seen how to create a website, but it would be beneficial to update it in a safe way.  
웹사이트 생성 방법을 배웠지만, 안전하게 업데이트하는 방법도 중요합니다.  
👉 설명: 실수로 파일을 덮어쓰거나 삭제하지 않도록 대비.  

Versioning your files in Amazon S3 is a feature you need to enable at the bucket level.  
S3에서 파일 버전 관리는 버킷 수준에서 활성화해야 하는 기능입니다.  
👉 설명: 버전 관리는 개별 파일이 아니라 버킷 전체에 적용됨.  

For example, consider a bucket with versioning enabled.  
예를 들어, 버전 관리가 활성화된 버킷을 생각해봅시다.  
👉 설명: 버전 관리 기능 작동 예시 소개.  

Whenever a user uploads a file, it creates a version of that file at the selected key.  
사용자가 파일을 업로드하면, 해당 키에 새로운 버전이 생성됩니다.  
👉 설명: 업로드마다 고유 버전 생성.  

If the same key is uploaded again, instead of overwriting, it creates version two, then version three, and so on.  
같은 키로 다시 업로드하면 덮어쓰지 않고 두 번째 버전, 세 번째 버전… 순서대로 생성됩니다.  
👉 설명: 이전 버전 유지, 안전한 변경 관리 가능.  

---

## Benefits of Versioning  
## 버전 관리의 장점  

It is best practice to version your buckets.  
버킷에 버전 관리를 활성화하는 것이 권장됩니다.  
👉 설명: 안정성과 데이터 복구 측면에서 모범 사례.  

The primary reasons include:  
주요 이유는 다음과 같습니다:  
👉 설명: 버전 관리의 구체적 이점 소개.  

- Protection against unintended deletes.  
- 의도치 않은 삭제로부터 보호.  
👉 설명: 삭제 시 삭제 마커 생성으로 이전 버전 복원 가능.  

For instance, deleting a file version actually adds a delete marker, allowing you to restore previous versions.  
예를 들어, 파일 버전을 삭제하면 삭제 마커가 생성되어 이전 버전을 복원할 수 있습니다.  
👉 설명: 안전한 삭제 처리 메커니즘.  

- Ability to roll back to a previous version.  
- 이전 버전으로 되돌릴 수 있는 기능.  
👉 설명: 실수나 문제 발생 시 이전 상태 복구 가능.  

If you want to revert to the state from two days ago, you can take that file and roll it back.  
예를 들어, 2일 전 상태로 되돌리려면 해당 파일을 선택하여 복원 가능.  
👉 설명: 특정 시점으로의 롤백 가능성 설명.  

---

## Important Notes on Versioning  
## 버전 관리 시 주의 사항  

There are some important notes to be aware of:  
유의해야 할 중요한 사항은 다음과 같습니다:  
👉 설명: 기능 사용 전 주의 사항 정리.  

- Any file that was not versioned prior to enabling versioning will have a null version.  
- 버전 활성화 이전에 존재한 파일은 null 버전으로 간주됩니다.  
👉 설명: 이전 파일과 신규 파일 버전 관리 차이 이해 필요.  

- Suspending versioning does not delete previous versions, making it a safe operation.  
- 버전 관리를 일시 중지해도 기존 버전은 삭제되지 않아 안전한 작업입니다.  
👉 설명: 데이터 안전성을 유지하며 기능 일시 중지 가능.  

---

## Demonstration in the AWS Console  
## AWS 콘솔에서 실습  

Now, let's go into the AWS console and see how we can use versioning.  
이제 AWS 콘솔에서 버전 관리 기능을 어떻게 사용하는지 살펴보겠습니다.  
👉 설명: 콘솔 실습 예고, 실습 단계 진행 준비.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 versioning must be enabled at the bucket level to track file versions.  
- S3 버전 관리는 파일 버전을 추적하기 위해 버킷 수준에서 활성화해야 합니다.  

- Versioning protects against unintended deletes by using delete markers.  
- 버전 관리는 삭제 마커를 사용해 의도치 않은 삭제로부터 보호합니다.  

- Users can roll back to previous versions of files easily.  
- 사용자는 이전 버전으로 쉽게 되돌릴 수 있습니다.  

- Suspending versioning does not delete existing versions, ensuring data safety.  
- 버전 관리 일시 중지는 기존 버전을 삭제하지 않아 데이터 안전성이 보장됩니다.  

---

🎮 **게임보상:**

* **“S3 버전 관리 실습 준비 완료!”**

  * 버킷 버전 관리 이해 +25
  * 삭제 보호 및 롤백 이해 +25
  * 버전 관리 주의 사항 확인 +25
  * AWS 콘솔 실습 준비 완료 +25

총 **100 XP 획득!** 🎉
