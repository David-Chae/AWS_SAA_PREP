# S3 Batch Operations  
# S3 배치 작업  

---

## Introduction to S3 Batch Operations  
## S3 배치 작업 소개  

S3 Batch Operations allow you to perform bulk operations on existing S3 objects with a single request.  
S3 배치 작업을 사용하면 단일 요청으로 기존 S3 객체에 대해 대량 작업을 수행할 수 있습니다.  

This feature enables efficient management of large numbers of objects without the need for scripting individual operations.  
이 기능을 통해 개별 작업을 스크립팅할 필요 없이 많은 객체를 효율적으로 관리할 수 있습니다.  

---

## Use Cases for S3 Batch Operations  
## S3 배치 작업 사용 사례  

- Modify all the object metadata and properties of many S3 objects at once.  
- 여러 S3 객체의 메타데이터와 속성을 한 번에 수정  
- Copy objects between S3 buckets as a batch operation.  
- S3 버킷 간 객체를 배치 작업으로 복사  
- Encrypt all unencrypted objects in your S3 buckets.  
- 버킷 내 암호화되지 않은 모든 객체를 암호화  
- Modify Access Control Lists (ACLs) or tags for multiple objects.  
- 여러 객체의 ACL 또는 태그 수정  
- Restore many objects simultaneously from S3 Glacier.  
- S3 Glacier에서 많은 객체를 동시에 복원  
- Invoke a Lambda function to perform custom actions on every object in the batch.  
- 배치 내 모든 객체에 대해 사용자 정의 작업을 수행하도록 Lambda 함수 호출  

The core idea is that you can perform any operation you want on a list of objects.  
핵심 아이디어는 객체 목록에 원하는 모든 작업을 수행할 수 있다는 것입니다.  

Therefore, a batch job consists of three main components:  
따라서 배치 작업은 세 가지 주요 구성 요소로 이루어집니다:  

1. A list of objects.  
1. 객체 목록  
2. The action to perform on those objects.  
2. 객체에 수행할 작업  
3. Optional parameters related to the action.  
3. 작업 관련 선택적 매개변수  

---

## Advantages of Using S3 Batch Operations  
## S3 배치 작업 사용 장점  

Why use S3 Batch Operations instead of scripting these tasks yourself?  
왜 직접 스크립트 작성 대신 S3 배치 작업을 사용할까요?  

- Management of retries is handled automatically.  
- 재시도 관리를 자동으로 처리  
- You can track the progress of the batch job.  
- 배치 작업 진행 상황 추적 가능  
- Completion notifications can be sent upon job completion.  
- 작업 완료 시 완료 알림 전송 가능  
- Detailed reports are generated for auditing and verification.  
- 감사 및 검증을 위한 상세 보고서 생성  

---

## Generating the Object List for Batch Operations  
## 배치 작업을 위한 객체 목록 생성  

To generate the list of objects to pass to S3 Batch Operations, you can use the following approach:  
S3 배치 작업에 전달할 객체 목록을 생성하려면 다음 방법을 사용할 수 있습니다:  

- Use S3 Inventory to obtain a comprehensive list of objects in an S3 bucket.  
- S3 인벤토리를 사용하여 버킷 내 전체 객체 목록 획득  
- Use Athena to query and filter this list to select the specific objects you want to include in the batch operation.  
- Athena를 사용하여 목록을 쿼리하고 필터링하여 배치 작업에 포함할 객체 선택  

This filtered list is then passed to the batch operation along with the desired action and any necessary parameters.  
이 필터링된 목록은 원하는 작업과 필요한 매개변수와 함께 배치 작업에 전달됩니다.  

---

## Example Use Case  
## 예시 사용 사례  

A common scenario is to find all unencrypted objects using S3 Inventory and then encrypt them all at once using an S3 Batch Operation.  
일반적인 시나리오는 S3 인벤토리를 사용하여 암호화되지 않은 모든 객체를 찾고 S3 배치 작업으로 한 번에 암호화하는 것입니다.  

This approach streamlines the process of securing your data at scale.  
이 접근 방식은 대규모 데이터 보안 작업을 간소화합니다.  

---

## Summary  
## 요약  

This concludes the lecture on S3 Batch Operations.  
이로써 S3 배치 작업에 대한 강의를 마칩니다.  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Batch Operations allow bulk actions on existing S3 objects with a single request.  
- S3 배치 작업은 단일 요청으로 기존 S3 객체에 대해 대량 작업을 수행할 수 있습니다.  

- Common use cases include modifying metadata, copying objects, encrypting unencrypted objects, modifying ACLs or tags, restoring from Glacier, and invoking Lambda functions.  
- 일반적인 사용 사례: 메타데이터 수정, 객체 복사, 암호화되지 않은 객체 암호화, ACL 또는 태그 수정, Glacier에서 복원, Lambda 함수 호출  

- A batch job consists of a list of objects, the action to perform, and optional parameters.  
- 배치 작업은 객체 목록, 수행할 작업, 선택적 매개변수로 구성됩니다.  

- S3 Batch Operations provide management of retries, progress tracking, completion notifications, and report generation.  
- S3 배치 작업은 재시도 관리, 진행 상황 추적, 완료 알림, 보고서 생성을 제공합니다.  

- S3 Inventory combined with Athena can be used to generate and filter the list of objects for batch processing.  
- S3 인벤토리와 Athena를 결합하면 배치 처리를 위한 객체 목록 생성 및 필터링에 활용할 수 있습니다.  

🎮 **게임보상:**

* **S3 Batch Operations 학습 완료!**

  * 배치 작업 기본 개념 +10
  * 활용 사례 이해 +15
  * 객체 목록 생성 & Athena 활용 +10
    총 **35 XP 획득!** 🎉
