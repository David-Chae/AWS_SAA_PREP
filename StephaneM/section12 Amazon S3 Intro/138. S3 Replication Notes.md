# S3 Replication Notes  
# S3 복제 노트  

---

## Amazon S3 Replication Overview  
## Amazon S3 복제 개요  

After enabling replication, only new objects are replicated automatically.  
복제를 활성화한 후에는 새로 업로드되는 객체만 자동으로 복제됩니다.  
👉 설명: 기존 객체는 자동으로 복제되지 않으므로 추가 설정이 필요합니다.  

---

## Replicating Existing Objects  
## 기존 객체 복제  

To replicate existing objects, you need to use the S3 Batch Replication feature.  
기존 객체를 복제하려면 S3 배치 복제(S3 Batch Replication) 기능을 사용해야 합니다.  

This feature replicates existing objects as well as objects that have failed replication.  
이 기능은 기존 객체뿐 아니라 이전에 복제에 실패한 객체도 복제합니다.  
👉 설명: S3 Batch Replication은 복제를 놓친 객체까지 보완해주는 기능입니다.  

---

## Replicating Delete Operations  
## 삭제 작업 복제  

You can replicate delete markers from the source bucket to the target bucket.  
소스 버킷의 삭제 마커(delete marker)를 대상 버킷으로 복제할 수 있습니다.  

This is an optional setting.  
이 설정은 선택 사항입니다.  

However, deletions with version IDs are not replicated.  
단, 버전 ID가 있는 삭제는 복제되지 않습니다.  

This prevents permanent deletions from being replicated, which helps avoid malicious deletes happening from one bucket to another.  
이는 영구 삭제가 다른 버킷으로 복제되는 것을 방지하여 악의적인 삭제로부터 데이터를 보호합니다.  

---

## Replication Chaining  
## 복제 체이닝  

There is no chaining of replications.  
복제 체이닝은 지원되지 않습니다.  

For example, if bucket one replicates to bucket two, and bucket two replicates to bucket three, then objects from bucket one are not replicated into bucket three.  
예를 들어, 버킷1이 버킷2로 복제되고, 버킷2가 버킷3으로 복제되더라도, 버킷1의 객체는 버킷3으로 복제되지 않습니다.  
👉 설명: 중간 버킷을 거쳐 자동 복제되는 기능은 없습니다.  

---

I hope you found this information helpful. See you in the next lecture.  
이 정보가 도움이 되었길 바랍니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- After enabling replication, only new objects are replicated automatically.  
- 복제를 활성화한 후에는 새 객체만 자동으로 복제됩니다.  

- To replicate existing objects, use the S3 Batch Replication feature.  
- 기존 객체를 복제하려면 S3 배치 복제를 사용해야 합니다.  

- Delete markers can be optionally replicated from the source to the target bucket.  
- 삭제 마커는 선택적으로 소스 버킷에서 대상 버킷으로 복제할 수 있습니다.  

- Permanent deletions with version IDs are not replicated to prevent malicious deletes.  
- 버전 ID가 있는 영구 삭제는 악의적 삭제 방지를 위해 복제되지 않습니다.  

- Replication chaining is not supported; objects from the first bucket do not replicate to the third bucket through an intermediate bucket.  
- 복제 체이닝은 지원되지 않으며, 중간 버킷을 거쳐 첫 번째 버킷의 객체가 세 번째 버킷으로 복제되지 않습니다.  

---

🎮 **게임보상:**

* **“S3 복제 심화 학습 완료!”**

  * 기존 객체 복제 방법 이해 +25
  * 삭제 마커 복제 이해 +25
  * 복제 체이닝 제한 이해 +25
  * 실습 대비 개념 정리 +25

총 **100 XP 획득!** 🎉
