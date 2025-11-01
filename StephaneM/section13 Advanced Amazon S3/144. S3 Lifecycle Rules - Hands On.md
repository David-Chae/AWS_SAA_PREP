# S3 Lifecycle Rules - Hands On  
# S3 라이프사이클 규칙 실습  

---

## Creating a Lifecycle Rule in S3  
## S3에서 라이프사이클 규칙 생성  

Let's proceed to create a lifecycle rule for our buckets.  
이제 버킷에 대한 라이프사이클 규칙을 생성해보겠습니다.  

Navigate under the Management tab and initiate the creation of a lifecycle rule.  
Management 탭으로 이동하여 라이프사이클 규칙 생성을 시작합니다.  

This rule will be named demo rule, and it will apply to all objects within the buckets.  
규칙 이름은 demo rule로 지정하며, 버킷 내 모든 객체에 적용됩니다.  

Confirm and acknowledge the rule creation.  
규칙 생성을 확인하고 승인합니다.  

---

## Overview of Lifecycle Rule Actions  
## 라이프사이클 규칙 동작 개요  

There are five different rule actions available:  
사용 가능한 규칙 동작은 다섯 가지입니다:  

1. Move current versions of objects between storage classes.  
1. 현재 버전 객체를 다른 스토리지 클래스로 이동  

2. Move non-current versions of objects between storage classes.  
2. 비현재 버전 객체를 다른 스토리지 클래스로 이동  

3. Expire current versions of objects.  
3. 현재 버전 객체 만료 설정  

4. Permanently delete non-current versions of objects.  
4. 비현재 버전 객체 영구 삭제  

5. Delete expired objects, delete markers, or incomplete multi-part uploads.  
5. 만료된 객체, 삭제 마커, 미완료 멀티파트 업로드 삭제  

Let's examine each of these use cases in detail.  
각 사용 사례를 자세히 살펴보겠습니다.  

---

## Moving Current Version Objects Between Storage Classes  
## 현재 버전 객체를 스토리지 클래스 간 이동  

This applies when you have a versioned bucket.  
이 규칙은 버전 관리가 활성화된 버킷에 적용됩니다.  

The current version refers to the most recent version displayed to the user.  
현재 버전은 사용자에게 표시되는 최신 버전을 의미합니다.  

For example, you can transition objects to the Standard-Infrequent Access (Standard IA) storage class after 30 days.  
예: 객체를 30일 후 Standard-IA로 전환 가능  

Then, after 60 days, move them to Intelligent Tiering.  
그 후 60일 후 Intelligent-Tiering으로 이동  

Following that, transition to Glacier Instant Retrieval after 90 days, then to Glacier Flexible Retrieval after 180 days, and finally to Glacier Deep Archive after 365 days.  
이어 90일 후 Glacier Instant Retrieval, 180일 후 Glacier Flexible Retrieval, 365일 후 Glacier Deep Archive로 전환  

You can configure as many transitions as needed in this sequence.  
필요한 만큼 전환 단계를 추가 설정할 수 있습니다.  

Remember to acknowledge the changes after setting them.  
설정 후 반드시 변경 사항을 확인하고 승인하세요.  

---

## Moving Non-Current Versions Between Storage Classes  
## 비현재 버전 객체를 스토리지 클래스 간 이동  

Non-current versions refer to objects that have been overridden by newer versions.  
비현재 버전은 새 버전에 의해 덮어써진 객체를 의미합니다.  

For these, you might want to move them to Glacier Flexible Retrieval after 90 days, assuming they will not be needed for retrieval after that period.  
예: 90일 후 Glacier Flexible Retrieval로 이동, 이후 조회가 필요 없다고 가정  

Additional transitions can be added as necessary.  
필요 시 추가 전환 단계도 설정 가능합니다.  

---

## Expiration and Deletion Policies  
## 만료 및 삭제 정책  

You can set expiration for current versions of objects, for example, after 700 days.  
현재 버전 객체는 700일 후 만료 설정 가능  

Similarly, non-current versions can be permanently deleted after 700 days.  
비현재 버전 객체도 700일 후 영구 삭제 가능  

These policies help manage storage costs by removing outdated data automatically.  
이 정책들은 오래된 데이터를 자동 제거하여 스토리지 비용 관리에 도움을 줍니다.  

---

## Reviewing Lifecycle Transitions and Expiration Actions  
## 라이프사이클 전환 및 만료 동작 검토  

The lifecycle rule interface provides a timeline view showing what will happen to both current and non-current versions of your objects.  
라이프사이클 규칙 인터페이스는 현재 버전과 비현재 버전 객체에 대해 발생할 동작을 타임라인으로 시각화합니다.  

This visualization helps ensure your transitions and expiration policies are configured correctly.  
이 시각화를 통해 전환과 만료 정책이 올바르게 설정되었는지 확인할 수 있습니다.  

Once satisfied with the configuration, proceed to create the rule.  
설정이 완료되면 규칙 생성을 진행합니다.  

This rule will operate in the background, automating the management of your objects across storage classes.  
이 규칙은 백그라운드에서 실행되어 객체의 스토리지 클래스 관리를 자동화합니다.  

---

## Conclusion  
## 결론  

You have now learned how to automate the movement of objects between different AWS S3 storage classes using lifecycle rules.  
이제 라이프사이클 규칙을 사용해 AWS S3 객체를 다양한 스토리지 클래스 간 자동 이동하는 방법을 배웠습니다.  

This automation helps optimize storage costs and manage data lifecycle efficiently.  
이 자동화는 스토리지 비용 최적화 및 데이터 라이프사이클 관리 효율성을 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created a lifecycle rule in S3 to automate object transitions between storage classes.  
- S3에서 객체 전환 자동화를 위한 라이프사이클 규칙 생성  

- Managed both current and non-current object versions with specific transition and expiration policies.  
- 현재 버전과 비현재 버전을 전환 및 만료 정책으로 관리  

- Utilized multiple storage classes including Standard IA, Intelligent Tiering, Glacier Instant Retrieval, Glacier Flexible Retrieval, and Deep Archive.  
- Standard IA, Intelligent-Tiering, Glacier Instant Retrieval, Glacier Flexible Retrieval, Deep Archive 등 다양한 스토리지 클래스 활용  

- Set expiration and permanent deletion timelines for objects to optimize storage costs.  
- 스토리지 비용 최적화를 위해 객체 만료 및 영구 삭제 일정 설정  

🎮 **게임보상:**

* **S3 Lifecycle 규칙 실습 완료!**

  * 현재/비현재 버전 관리 +20
  * 자동 전환 및 삭제 정책 설정 +15
  * 다양한 스토리지 클래스 활용 +15
    총 **50 XP 획득!** 🎉
