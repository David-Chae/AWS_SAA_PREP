# S3 Storage Classes Overview  
# S3 스토리지 클래스 개요  

---

## Overview of Amazon S3 Storage Classes  
## Amazon S3 스토리지 클래스 개요  

Amazon S3 provides various storage classes to accommodate different data access needs and cost considerations.  
Amazon S3는 데이터 접근 패턴과 비용 고려에 맞춰 다양한 스토리지 클래스를 제공합니다.  
👉 설명: 데이터 사용 빈도, 비용, 내구성에 따라 적절한 스토리지 클래스를 선택할 수 있습니다.  

These include:  
이 클래스에는 다음이 포함됩니다:  

- Amazon S3 Standard - General Purpose  
- Amazon S3 Standard - 일반 용도  

- Amazon S3 Infrequent Access (Standard-IA)  
- Amazon S3 Infrequent Access (Standard-IA) - 자주 접근하지 않는 데이터용  

- Amazon S3 One Zone-Infrequent Access (One Zone-IA)  
- Amazon S3 One Zone-Infrequent Access (One Zone-IA) - 단일 AZ 저장  

- Glacier Instant Retrieval  
- Glacier Instant Retrieval - 즉시 검색 가능 아카이브  

- Glacier Flexible Retrieval  
- Glacier Flexible Retrieval - 유연한 검색 아카이브  

- Glacier Deep Archive  
- Glacier Deep Archive - 장기 보관용 아카이브  

- Amazon S3 Intelligent-Tiering  
- Amazon S3 Intelligent-Tiering - 자동 계층 조정 스토리지  

This lecture will cover each of these classes in depth, which is essential knowledge for the exam.  
이번 강의에서는 각 스토리지 클래스를 상세히 다룹니다. 시험에 꼭 필요한 내용입니다.  

When creating an object in Amazon S3, you can select its storage class.  
S3 객체를 생성할 때 스토리지 클래스를 선택할 수 있습니다.  

Additionally, you can manually modify the storage class later.  
추가로, 나중에 수동으로 스토리지 클래스를 변경할 수도 있습니다.  

Amazon S3 Lifecycle configurations allow automatic movement of objects between storage classes based on defined rules.  
S3 라이프사이클(Lifecycle) 설정을 통해 정의된 규칙에 따라 객체를 자동으로 다른 스토리지 클래스로 이동시킬 수 있습니다.  

---

## Durability and Availability Concepts  
## 내구성(Durability)과 가용성(Availability) 개념  

Before discussing the storage classes, it is important to understand the concepts of durability and availability:  
스토리지 클래스를 논의하기 전에 내구성과 가용성 개념을 이해하는 것이 중요합니다.  

Durability refers to the likelihood of losing an object stored in Amazon S3.  
내구성은 S3에 저장된 객체를 잃을 가능성을 의미합니다.  

Amazon S3 offers extremely high durability, known as "11 nines," which means 99.999999999% durability.  
S3는 "11 9"로 불리는 매우 높은 내구성을 제공합니다. 즉, 99.999999999% 내구성을 의미합니다.  

Availability indicates how readily the service can be accessed and varies by storage class.  
가용성은 서비스 접근 가능성을 의미하며, 스토리지 클래스에 따라 달라집니다.  

Amazon S3's 11 nines durability means that if you store 10 million objects, you can expect to lose only one object every 10,000 years on average.  
S3의 11 9 내구성은 1,000만 개 객체를 저장하면 평균 10,000년마다 한 개만 손실될 수 있음을 의미합니다.  

This durability level is consistent across all storage classes.  
이 내구성 수준은 모든 스토리지 클래스에서 동일합니다.  

Availability depends on the storage class.  
가용성은 스토리지 클래스에 따라 달라집니다.  

For example, S3 Standard has 99.99% availability, which translates to approximately 53 minutes of downtime per year.  
예를 들어, S3 Standard는 99.99% 가용성을 제공하며, 연간 약 53분 정도 다운타임이 발생할 수 있습니다.  

This means occasional errors may occur when accessing the service, which should be considered when developing applications.  
즉, 서비스 접근 시 간헐적 오류가 발생할 수 있으므로 애플리케이션 개발 시 이를 고려해야 합니다.  

---

## Amazon S3 Standard  
## Amazon S3 Standard  

Designed for frequently accessed data.  
자주 접근하는 데이터용으로 설계됨.  

Default storage class.  
기본 스토리지 클래스.  

Provides low latency and high throughput.  
낮은 지연과 높은 처리량 제공.  

Can sustain two concurrent facility failures within AWS.  
AWS 내에서 동시 2개 시설 장애도 견딜 수 있음.  

Use cases include big data analytics, mobile and gaming applications, and content distribution.  
사용 사례: 빅데이터 분석, 모바일/게임 앱, 콘텐츠 배포 등.  

---

## Amazon S3 Infrequent Access (Standard-IA)  
## Amazon S3 Infrequent Access (Standard-IA)  

Intended for data accessed less frequently but requiring rapid access when needed.  
접근 빈도는 낮지만 필요 시 빠르게 접근해야 하는 데이터용.  

Lower cost than S3 Standard but incurs retrieval fees.  
S3 Standard보다 비용 저렴하지만 조회 시 요금 발생.  

Offers 99.9% availability.  
가용성 99.9% 제공.  

Common use cases include disaster recovery and backups.  
사용 사례: 재해 복구, 백업 등.  

---

## Amazon S3 One Zone-Infrequent Access (One Zone-IA)  
## Amazon S3 One Zone-Infrequent Access (One Zone-IA)  

Stores data in a single Availability Zone (AZ).  
데이터를 단일 AZ에 저장.  

Provides high durability within that AZ but data loss can occur if the AZ is destroyed.  
해당 AZ 내에서는 높은 내구성 제공, 그러나 AZ가 파괴되면 데이터 손실 가능.  

Offers 99.5% availability.  
가용성 99.5% 제공.  

Suitable for secondary backup copies of on-premises data or data that can be recreated.  
온프레미스 데이터의 2차 백업이나 재생 가능한 데이터에 적합.  

---

## Glacier Storage Classes  
## Glacier 스토리지 클래스  

Glacier storage classes are low-cost options designed for archiving and backup, with retrieval costs and varying retrieval times.  
Glacier 클래스는 저비용 아카이빙/백업용으로 설계되었으며, 조회 비용과 조회 시간이 클래스별로 다릅니다.  

### Glacier Instant Retrieval  
### Glacier 즉시 조회  

Provides millisecond retrieval.  
밀리초 단위 조회 제공.  

Ideal for data accessed approximately once a quarter.  
분기별 1회 정도 접근하는 데이터에 적합.  

Minimum storage duration is 90 days.  
최소 저장 기간 90일.  

### Glacier Flexible Retrieval  
### Glacier 유연 조회  

Formerly known as Amazon S3 Glacier.  
이전 명칭: Amazon S3 Glacier.  

Offers three retrieval options:  
세 가지 조회 옵션 제공:  

- Expedited: 1 to 5 minutes  
- 빠른 조회: 1~5분  

- Standard: 3 to 5 hours  
- 표준 조회: 3~5시간  

- Bulk: 5 to 12 hours (free)  
- 대용량 조회: 5~12시간 (무료)  

Minimum storage duration is 90 days.  
최소 저장 기간 90일.  

### Glacier Deep Archive  
### Glacier Deep Archive  

Designed for long-term storage.  
장기 보관용 설계.  

Retrieval options:  
조회 옵션:  

- Standard: 12 hours  
- 표준 조회: 12시간  

- Bulk: 48 hours  
- 대용량 조회: 48시간  

Minimum storage duration is 180 days.  
최소 저장 기간 180일.  

Lowest cost storage option.  
가장 저렴한 스토리지 옵션.  

---

## Amazon S3 Intelligent-Tiering  
## Amazon S3 Intelligent-Tiering  

Automatically moves objects between access tiers based on usage patterns.  
사용 패턴에 따라 객체를 자동으로 액세스 계층 간 이동.  

Incurs a small monthly monitoring and auto-tiering fee.  
소액의 월간 모니터링 및 자동 계층 비용 발생.  

No retrieval charges.  
조회 요금 없음.  

Access tiers include:  
액세스 계층 포함:  

- Frequent Access (default)  
- 자주 접근(기본)  

- Infrequent Access (objects not accessed for 30 days)  
- 드물게 접근(30일 동안 접근하지 않은 객체)  

- Archive Instant Access (objects not accessed for 90 days)  
- 아카이브 즉시 접근(90일 동안 접근하지 않은 객체)  

- Archive Access (optional, configurable from 90 to 700+ days)  
- 아카이브 접근(선택, 90~700일 이상 설정 가능)  

- Deep Archive Access (optional, configurable from 180 to 700+ days)  
- 딥 아카이브 접근(선택, 180~700일 이상 설정 가능)  

This class allows users to "set and forget" while S3 optimizes storage costs automatically.  
사용자는 “설정 후 잊기”만 하면 되고, S3가 자동으로 스토리지 비용을 최적화합니다.  

---

## Summary and Comparison  
## 요약 및 비교  

All storage classes provide 11 nines durability.  
모든 스토리지 클래스는 11 9 내구성을 제공합니다.  

Availability decreases as the number of Availability Zones decreases.  
AZ 수가 줄어들수록 가용성 감소.  

Minimum storage durations vary by class.  
최소 저장 기간은 클래스별로 다름.  

Pricing varies by storage class and region; understanding class names helps interpret pricing.  
가격은 클래스와 리전별로 다르며, 클래스 명을 이해하면 가격 해석에 도움이 됩니다.  

It is recommended to review diagrams and pricing charts to understand these differences, though memorization is not required.  
차이 이해를 위해 다이어그램과 가격표 확인 권장, 암기는 필요 없음.  

This concludes the lecture on Amazon S3 storage classes.  
이로써 Amazon S3 스토리지 클래스 강의가 끝났습니다.  

Understanding these classes will help you choose the appropriate storage option based on your data access patterns and cost requirements.  
각 클래스 이해는 데이터 접근 패턴과 비용 요구에 맞는 스토리지 선택에 도움이 됩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 offers multiple storage classes tailored for different access patterns and cost requirements.  
- Amazon S3는 다양한 접근 패턴과 비용 요구에 맞춘 여러 스토리지 클래스를 제공합니다.  

- All S3 storage classes provide 11 nines (99.999999999%) durability.  
- 모든 S3 스토리지 클래스는 11 9(99.999999999%) 내구성을 제공합니다.  

- Availability varies by storage class, with S3 Standard offering 99.99% availability and others lower depending on redundancy.  
- 가용성은 클래스별로 다르며, S3 Standard는 99.99%, 다른 클래스는 중복성에 따라 낮음.  

- Lifecycle configurations and Intelligent-Tiering automate data movement between storage classes to optimize cost and access.  
- 라이프사이클 설정과 Intelligent-Tiering은 비용과 접근성을 최적화하기 위해 스토리지 클래스 간 객체 이동을 자동화합니다.

---

🎮 **게임보상:**  
- **“S3 스토리지 클래스 학습 완료!”**  
  - 모든 클래스 이해 +30  
  - 내구성/가용성 개념 이해 +20  
  - Glacier와 Intelligent-Tiering 이해 +30  
  - 요약/비교 이해 +20  

총 **100 XP 획득!** 🎉
