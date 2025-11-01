# S3 Lifecycle Rules (with S3 Analytics)  
# S3 라이프사이클 규칙 (S3 분석 포함)  

---

## S3 Lifecycle Rules and Storage Class Transitions  
## S3 라이프사이클 규칙 및 스토리지 클래스 전환  

Let's discuss how to move objects between different storage classes in Amazon S3 by transitioning them automatically.  
이번에는 Amazon S3에서 객체를 자동으로 다른 스토리지 클래스로 전환하여 이동하는 방법을 다룹니다.  

The following diagram illustrates the possible transitions:  
다음 다이어그램은 가능한 전환을 보여줍니다:  

- From Standard to Standard-Infrequent Access (Standard IA), Intelligent Tiering, or One-Zone IA.  
- Standard에서 Standard-IA, Intelligent-Tiering, 또는 One-Zone IA로 전환 가능  

- From One-Zone IA to Flexible Retrieval or Deep Archive.  
- One-Zone IA에서 Flexible Retrieval 또는 Deep Archive로 전환 가능  

All possible permutations of transitions are shown in this graph.  
모든 가능한 전환 조합이 이 그래프에 표시됩니다.  

If you know your objects will be infrequently accessed, move them to Standard IA.  
객체가 자주 접근되지 않을 경우 Standard IA로 이동하세요.  

For archiving purposes, move objects into Glacier tiers or the Deep Archive tier.  
아카이빙 목적으로는 Glacier 계층 또는 Deep Archive 계층으로 이동시키세요.  

While moving these objects can be done manually, automation is possible using lifecycle rules.  
객체 이동을 수동으로 할 수도 있지만, 라이프사이클 규칙을 사용하면 자동화가 가능합니다.  

---

## Components of Lifecycle Rules  
## 라이프사이클 규칙 구성 요소  

Lifecycle rules consist of multiple components:  
라이프사이클 규칙은 여러 구성 요소로 이루어집니다:  

- **Transition actions:** Configure objects to transition to another storage class.  
- **전환 동작:** 객체를 다른 스토리지 클래스로 전환하도록 설정  

For example, move to Standard IA 60 days after creation or to Glacier for archiving after six months.  
예: 생성 후 60일 후 Standard IA로 이동, 6개월 후 아카이빙을 위해 Glacier로 이동  

- **Expiration actions:** Configure objects to be deleted after a specified time.  
- **만료 동작:** 지정된 기간 후 객체를 삭제하도록 설정  

For example, delete access log files after 365 days or delete old versions of files if versioning is enabled.  
예: 액세스 로그를 365일 후 삭제, 버전 관리 활성화 시 오래된 버전 삭제  

- **Incomplete multipart uploads:** Delete incomplete multipart uploads older than a specified period, such as two weeks.  
- **미완료 멀티파트 업로드:** 지정 기간(예: 2주) 이상된 미완료 멀티파트 업로드 삭제  

Rules can be applied to entire buckets, specific prefixes (paths within buckets), or specific object tags.  
규칙은 버킷 전체, 특정 접두사(버킷 내 경로), 또는 객체 태그별로 적용 가능  

For example, you can apply a rule only to objects tagged for the finance department.  
예: 재무 부서 태그가 있는 객체에만 규칙 적용 가능  

---

## Example Scenario: Managing Source Images and Thumbnails  
## 예제 시나리오: 원본 이미지 및 썸네일 관리  

Consider an application running on EC2 that creates thumbnails after profile photos are uploaded to Amazon S3.  
EC2에서 실행되는 앱이 프로필 사진 업로드 후 썸네일을 생성한다고 가정  

Thumbnails can be easily recreated from the original photos and only need to be kept for 60 days.  
썸네일은 원본 사진에서 쉽게 재생성 가능하며 60일만 보관하면 됨  

The source images should be immediately retrievable for 60 days, after which retrieval can take up to six hours.  
원본 이미지는 처음 60일 동안 즉시 접근 가능, 이후 접근 시간은 최대 6시간  

---

## Design Approach  
## 설계 접근법  

Store source images in the Standard storage class with a lifecycle configuration to transition them to Glacier after 60 days.  
원본 이미지는 Standard 클래스에 저장하고 60일 후 Glacier로 전환되도록 라이프사이클 설정  

Store thumbnails in One-Zone IA since they are infrequently accessed and easily recreated.  
썸네일은 One-Zone IA에 저장, 접근 빈도 낮고 쉽게 재생성 가능  

Use a prefix to differentiate between source images and thumbnails.  
접두사를 사용해 원본 이미지와 썸네일 구분  

Configure a lifecycle rule to expire (delete) thumbnails after 60 days.  
썸네일은 60일 후 만료(삭제)되도록 라이프사이클 규칙 설정  

---

## Example Scenario: Recovering Deleted Objects with Versioning  
## 예제 시나리오: 버전 관리로 삭제된 객체 복구  

A company policy requires that deleted S3 objects be recoverable immediately for 30 days, and thereafter recoverable within 48 hours for up to 365 days.  
회사 정책상 삭제된 객체는 처음 30일간 즉시 복구 가능, 이후 48시간 내 최대 365일까지 복구 가능  

---

## Implementation  
## 구현  

Enable S3 versioning to keep object versions. Deleted objects are hidden by a delete marker and can be recovered.  
S3 버전 관리를 활성화하여 객체 버전 유지. 삭제된 객체는 삭제 마커로 숨겨지며 복구 가능  

Create a lifecycle rule to transition non-current versions of objects to Standard IA.  
비현재 버전을 Standard IA로 전환하는 라이프사이클 규칙 생성  

Later, transition these non-current versions to Glacier Deep Archive for archival purposes.  
나중에 비현재 버전을 아카이빙을 위해 Glacier Deep Archive로 전환  

---

## Determining Optimal Transition Timing with Amazon S3 Analytics  
## Amazon S3 Analytics로 최적 전환 시점 결정  

To determine the optimal number of days to transition an object from one storage class to another, use Amazon S3 Analytics.  
객체를 다른 스토리지 클래스로 전환할 최적 일수를 결정하려면 S3 Analytics 사용  

This service provides recommendations for transitions between Standard and Standard IA storage classes.  
이 서비스는 Standard와 Standard IA 전환에 대한 권장 사항 제공  

Note that it does not support One-Zone IA or Glacier.  
One-Zone IA와 Glacier는 지원하지 않음  

S3 Analytics runs on your buckets and generates a CSV report with statistics and recommendations.  
S3 Analytics는 버킷에서 실행되며 통계 및 권장 사항이 포함된 CSV 보고서 생성  

The report updates daily and typically takes 24 to 48 hours to start providing data analysis.  
보고서는 매일 업데이트되며, 데이터 분석 제공 시작까지 일반적으로 24~48시간 소요  

This report is a valuable first step to create or improve lifecycle rules that make sense for your usage patterns.  
이 보고서는 사용 패턴에 맞는 라이프사이클 규칙 생성 또는 개선을 위한 유용한 첫 단계  

---

## Conclusion  
## 결론  

This concludes the lecture on S3 lifecycle rules and analytics.  
이로써 S3 라이프사이클 규칙 및 분석 강의를 마칩니다  

These features help automate storage management, optimize costs, and ensure compliance with data retention policies.  
이 기능들은 스토리지 관리 자동화, 비용 최적화, 데이터 보존 정책 준수를 지원  

---

## Key Takeaways  
## 핵심 요약  

- S3 lifecycle rules automate transitions of objects between storage classes based on specified criteria.  
- S3 라이프사이클 규칙은 지정 기준에 따라 객체를 스토리지 클래스 간 자동 전환  

- Lifecycle rules can include transition actions, expiration actions, and can be scoped by prefixes or object tags.  
- 라이프사이클 규칙은 전환 동작, 만료 동작 포함 가능하며 접두사나 객체 태그별 적용 가능  

- Versioning combined with lifecycle rules allows management of non-current object versions and recovery of deleted objects.  
- 버전 관리와 라이프사이클 규칙 결합 시 비현재 버전 관리 및 삭제 객체 복구 가능  

- Amazon S3 Analytics provides recommendations to optimize lifecycle transitions between Standard and Standard IA storage classes.  
- S3 Analytics는 Standard와 Standard IA 간 라이프사이클 전환 최적화 권장 사항 제공  

🎮 **게임보상:**

* **S3 Lifecycle 규칙 강의 완료!**

  * 전환/만료 동작 이해 +15
  * 버전 관리 활용 +15
  * S3 Analytics 최적화 +10
    총 **40 XP 획득!** 🎉
