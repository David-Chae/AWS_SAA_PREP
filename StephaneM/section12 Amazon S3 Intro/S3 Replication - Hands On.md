# S3 Replication - Hands On  
# S3 복제 실습  

---

## Introduction to Amazon S3 Replication  
## Amazon S3 복제 소개  

In this session, we will practice replication on Amazon S3.  
이번 세션에서는 Amazon S3에서 복제를 실습합니다.  
👉 설명: 실제 버킷을 만들어 복제 기능을 확인하는 단계입니다.  

The process begins by creating a new bucket, which will serve as the origin bucket for replication.  
복제 과정은 새로운 버킷을 생성하는 것으로 시작하며, 이 버킷이 원본 버킷 역할을 합니다.  

I will name this bucket s3-stephane-bucket-origin-v2 and set its region to eu-west-1.  
이 버킷 이름을 `s3-stephane-bucket-origin-v2`로 설정하고, 리전을 `eu-west-1`로 지정합니다.  

This bucket will act as the origin bucket from which data will be replicated to another bucket.  
이 버킷은 데이터를 다른 버킷으로 복제하는 원본 버킷 역할을 합니다.  

It is essential to enable versioning on the origin bucket because replication only works if versioning is enabled.  
복제를 위해서는 원본 버킷에 버전 관리를 활성화해야 합니다.  
👉 설명: 버전 관리가 없으면 복제가 작동하지 않습니다.  

After enabling versioning, the bucket is created successfully.  
버전 관리를 활성화한 후, 버킷이 성공적으로 생성됩니다.  

Next, open the origin bucket in a new tab and create a second bucket, which will serve as the target bucket for replication.  
다음으로, 원본 버킷을 새 탭에서 열고 복제 대상 버킷을 생성합니다.  

This bucket is named s3-stephane-bucket-replica-v2.  
대상 버킷 이름은 `s3-stephane-bucket-replica-v2`입니다.  

The target bucket's region can be the same as the origin bucket for same-region replication or a different region for cross-region replication.  
대상 버킷 리전은 동일 리전일 경우 SRR(동일 리전 복제), 다른 리전일 경우 CRR(교차 리전 복제)에 해당합니다.  

For example, the target bucket can be set to us-east-1 to replicate data from Europe to the US.  
예를 들어, 유럽에서 미국으로 데이터를 복제하려면 대상 버킷 리전을 `us-east-1`로 설정합니다.  

Enable versioning on the target bucket as well.  
대상 버킷에도 버전 관리를 활성화합니다.  

With both buckets versioned, the setup is ready for replication configuration.  
두 버킷 모두 버전 관리가 활성화되면 복제 설정 준비가 완료됩니다.  

---

## Uploading Files to the Origin Bucket  
## 원본 버킷에 파일 업로드  

Upload a file to the origin bucket to test replication.  
복제를 테스트하기 위해 원본 버킷에 파일을 업로드합니다.  

For example, upload a file named beach.jpg.  
예를 들어 `beach.jpg` 파일을 업로드합니다.  

This file is now present in the origin bucket but has not yet been replicated because replication is not configured.  
이 파일은 원본 버킷에 존재하지만, 복제 규칙이 설정되지 않았기 때문에 아직 복제되지 않습니다.  

---

## Configuring Replication Rules  
## 복제 규칙 설정  

To enable replication, navigate to the origin bucket's Management tab and scroll down to the Replication rules section.  
복제를 활성화하려면 원본 버킷의 Management 탭으로 이동하여 Replication rules 섹션까지 스크롤합니다.  

Initially, there are zero replication rules.  
초기 상태에서는 복제 규칙이 없습니다.  

Create a new replication rule named DemoReplicationRule.  
새 복제 규칙을 `DemoReplicationRule`로 생성합니다.  

Set the rule as enabled and apply it to all objects in the bucket.  
규칙을 활성화하고 버킷 내 모든 객체에 적용합니다.  

For the destination, specify a bucket within the same account.  
대상은 동일 계정 내 버킷으로 지정합니다.  

Enter the target bucket's name, which is s3-stephane-bucket-replica-v2.  
대상 버킷 이름으로 `s3-stephane-bucket-replica-v2`를 입력합니다.  

The destination region is automatically identified as us-east-1, indicating cross-region replication.  
대상 리전은 자동으로 `us-east-1`로 설정되어 CRR(교차 리전 복제)를 나타냅니다.  

An IAM role is required for replication.  
복제를 위해 IAM 역할이 필요합니다.  

Create a new role as prompted.  
프롬프트에 따라 새 역할을 생성합니다.  

The specific settings of the role are not critical for this demonstration.  
역할의 구체적인 설정은 이번 실습에서는 중요하지 않습니다.  

When enabling replication, you are prompted whether to replicate existing objects.  
복제를 활성화할 때 기존 객체를 복제할지 여부를 묻습니다.  

Replication only applies to new uploads from the moment it is set.  
복제는 설정 시점 이후의 새 업로드 객체에만 적용됩니다.  

To replicate existing objects, an S3 Batch Operation must be used separately.  
기존 객체를 복제하려면 S3 배치 작업(S3 Batch Operation)을 별도로 사용해야 합니다.  

For this setup, choose not to replicate existing objects and save the replication rule.  
이번 설정에서는 기존 객체 복제를 선택하지 않고 복제 규칙을 저장합니다.  

The replication rule is now active and ready.  
복제 규칙이 이제 활성화되어 준비되었습니다.  

---

## Testing Replication  
## 복제 테스트  

Check the target bucket; initially, no objects are replicated.  
대상 버킷을 확인하면 초기에는 복제된 객체가 없습니다.  

Upload a new file, for example, coffee.jpg, to the origin bucket.  
원본 버킷에 새 파일(`coffee.jpg`)을 업로드합니다.  

After uploading, the file appears in the origin bucket with a version ID.  
업로드 후 파일이 버전 ID와 함께 원본 버킷에 나타납니다.  

After a short delay, refresh the target bucket.  
잠시 기다린 후 대상 버킷을 새로고침합니다.  

The coffee.jpg file appears with the same version ID as in the origin bucket, confirming successful replication.  
`coffee.jpg` 파일이 원본과 동일한 버전 ID로 나타나 성공적으로 복제되었음을 확인합니다.  

To replicate the previously uploaded beach.jpg file, upload a new version of it.  
이전에 업로드한 `beach.jpg`를 복제하려면 새 버전을 업로드합니다.  

This creates a new version in the origin bucket, which will then replicate to the target bucket.  
이렇게 하면 원본 버킷에 새 버전이 생성되고 대상 버킷으로 복제됩니다.  

---

## Delete Marker Replication  
## 삭제 마커 복제  

An important setting for replication is the delete marker replication.  
복제의 중요한 설정 중 하나는 삭제 마커(delete marker) 복제입니다.  

By default, delete markers are not replicated.  
기본적으로 삭제 마커는 복제되지 않습니다.  

However, enabling this feature allows delete markers to be replicated from the origin bucket to the target bucket.  
하지만 이 기능을 활성화하면 원본 버킷의 삭제 마커를 대상 버킷으로 복제할 수 있습니다.  

Enable delete marker replication in the replication rule settings and save the changes.  
복제 규칙 설정에서 삭제 마커 복제를 활성화하고 변경 사항을 저장합니다.  

Now, when a file is deleted in the origin bucket, a delete marker is created due to versioning.  
이제 원본 버킷에서 파일을 삭제하면, 버전 관리 덕분에 삭제 마커가 생성됩니다.  

For example, deleting the coffee.jpg file in the origin bucket creates a delete marker.  
예를 들어, 원본 버킷에서 `coffee.jpg`를 삭제하면 삭제 마커가 생성됩니다.  

After a short delay, refreshing the target bucket shows that the delete marker has been replicated.  
잠시 후 대상 버킷을 새로고침하면 삭제 마커가 복제된 것을 확인할 수 있습니다.  

If you do not show versions, the file appears deleted in both buckets.  
버전을 표시하지 않으면, 두 버킷 모두에서 파일이 삭제된 것처럼 보입니다.  

Showing versions reveals the delete markers in both origin and target buckets.  
버전을 표시하면 원본과 대상 버킷 모두에서 삭제 마커를 확인할 수 있습니다.  

---

## Permanent Deletes Are Not Replicated  
## 영구 삭제는 복제되지 않음  

If a specific version of a file is permanently deleted in the origin bucket, this deletion is not replicated to the target bucket.  
원본 버킷에서 파일의 특정 버전을 영구 삭제하면, 이 삭제는 대상 버킷으로 복제되지 않습니다.  

For example, permanently deleting a version of beach.jpg in the origin bucket does not remove it from the target bucket.  
예를 들어, 원본 버킷에서 `beach.jpg`의 특정 버전을 영구 삭제해도 대상 버킷에서는 삭제되지 않습니다.  

Only delete markers are replicated, not permanent deletions of specific versions.  
삭제 마커만 복제되며, 특정 버전의 영구 삭제는 복제되지 않습니다.  

This distinction is important for managing replicated data.  
이는 복제된 데이터를 관리할 때 중요한 구분입니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on Amazon S3 replication.  
이로써 Amazon S3 복제 강의가 끝났습니다.  

We have covered creating origin and target buckets with versioning enabled, configuring replication rules including cross-region replication, uploading files to trigger replication, and understanding delete marker replication versus permanent deletes.  
버전 관리를 활성화한 원본/대상 버킷 생성, 복제 규칙 설정(교차 리전 포함), 파일 업로드로 복제 트리거, 삭제 마커 복제와 영구 삭제 차이 이해를 다뤘습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 replication requires versioning to be enabled on both origin and target buckets.  
- Amazon S3 복제를 위해서는 원본과 대상 버킷 모두 버전 관리가 활성화되어야 합니다.  

- Replication rules can be configured to replicate all objects from the source bucket to the destination bucket.  
- 복제 규칙을 설정하여 원본 버킷의 모든 객체를 대상 버킷으로 복제할 수 있습니다.  

- Cross-region replication is possible by selecting different regions for origin and target buckets.  
- 원본과 대상 버킷의 리전을 다르게 선택하면 교차 리전 복제가 가능합니다.  

- Delete markers can be replicated if enabled, but permanent deletions of specific versions are not replicated.

* 삭제 마커는 활성화 시 복제되지만, 특정 버전의 영구 삭제는 복제되지 않습니다.

---

🎮 **게임보상:**  
- **“S3 복제 실습 완료!”**  
  - 원본/대상 버킷 생성 +25  
  - 복제 규칙 설정 이해 +25  
  - 파일 업로드 및 버전 확인 +25  
  - 삭제 마커 vs 영구 삭제 이해 +25  

총 **100 XP 획득!** 🎉
```
