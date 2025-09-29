# RDS Custom for Oracle and Microsoft SQL Server  
# Oracle 및 Microsoft SQL Server용 RDS Custom  

---

## Introduction to RDS Custom  
## RDS Custom 소개  

In this lecture, we will discuss RDS Custom.  
이번 강의에서는 RDS Custom에 대해 설명합니다.  
(강의 주제 소개)

We know that with standard RDS, we do not have access to the underlying operating system or customization options.  
표준 RDS에서는 기본 운영체제나 사용자 지정 옵션에 접근할 수 없다는 것을 알고 있습니다.  
(표준 RDS 제한)

However, with RDS Custom, we actually do have such access.  
하지만 RDS Custom을 사용하면 이러한 접근이 가능합니다.  
(RDS Custom 장점)

RDS Custom supports two database types: Oracle and Microsoft SQL Server.  
RDS Custom은 Oracle과 Microsoft SQL Server 두 가지 DB 유형을 지원합니다.  
(지원 DB 유형)

Thanks to RDS Custom, we have access to the operating system and database customization capabilities.  
RDS Custom 덕분에 운영체제와 DB 커스터마이징 기능에 접근할 수 있습니다.  
(사용자 정의 가능)

With standard RDS, we still benefit from automated setup, operations, and scaling of the database within AWS.  
표준 RDS에서는 AWS 내에서 DB 자동 설정, 운영, 확장 등의 혜택이 있습니다.  
(표준 RDS 장점)

However, the RDS Custom option provides additional capabilities.  
그러나 RDS Custom 옵션은 추가 기능을 제공합니다.  
(추가 기능)

The "custom" aspect of RDS Custom means that we have access to the underlying database and operating system.  
RDS Custom의 "Custom"이라는 의미는 기본 DB와 운영체제에 접근할 수 있다는 뜻입니다.  
(커스터마이징 의미)

This allows us to configure internal settings, install patches, and enable native features.  
이를 통해 내부 설정 구성, 패치 설치, 기본 기능 활성화가 가능합니다.  
(활용 예시)

We can also access the underlying EC2 instance behind RDS using SSH or the SSM Session Manager.  
SSH 또는 SSM Session Manager를 통해 RDS 뒤의 EC2 인스턴스에도 접근할 수 있습니다.  
(직접 접근 방법)

This provides direct control over the environment hosting the database.  
DB를 호스팅하는 환경을 직접 제어할 수 있습니다.  
(관리 자유도)

Here is an example of my EC2 instance.  
다음은 제 EC2 인스턴스 예시입니다.  
(예시 안내)

As a user, if it is using Amazon RDS Custom, we can apply customizations and SSH into it.  
사용자는 Amazon RDS Custom을 사용하면 커스터마이징 적용 및 SSH 접속이 가능합니다.  
(실습 가능)

---

## Recommendations for Customization  
## 커스터마이징 권장 사항  

To perform any customization, it is recommended to deactivate the automation mode.  
커스터마이징을 수행할 때는 자동화 모드를 비활성화하는 것이 좋습니다.  
(안전 조치)

This ensures that RDS does not perform any automation, maintenance, or scaling while you are making your changes.  
변경 중 RDS가 자동화, 유지보수, 확장을 수행하지 않도록 보장합니다.  
(안정성 확보)

It is also important because you may accidentally break things.  
실수로 문제가 발생할 수 있기 때문에 중요합니다.  
(주의 사항)

Since you have access to the underlying EC2 instance, it is much safer to take a database snapshot beforehand.  
기본 EC2 인스턴스에 접근할 수 있으므로, 사전에 DB 스냅샷을 만드는 것이 안전합니다.  
(사전 백업 권장)

Otherwise, you will not be able to recover from your actions.  
그렇지 않으면 작업 복구가 불가능할 수 있습니다.  
(복구 불가)

---

## Summary: RDS vs. RDS Custom  
## 요약: RDS vs. RDS Custom  

Standard RDS manages your entire database and operating system.  
표준 RDS는 DB와 운영체제 전체를 관리합니다.  
(표준 RDS 특징)

Everything is managed by AWS, and you do not have to do anything.  
모든 것이 AWS에 의해 관리되므로 사용자가 따로 할 필요가 없습니다.  
(관리 자동화)

RDS Custom is available only for Oracle and Microsoft SQL Server.  
RDS Custom은 Oracle과 Microsoft SQL Server에서만 사용 가능합니다.  
(제한 사항)

It provides full administrative access to the underlying operating system and the database.  
기본 운영체제와 DB에 대한 전체 관리 권한을 제공합니다.  
(관리 자유도)

This concludes the lecture on RDS Custom.  
이로써 RDS Custom 강의를 마칩니다.  
(강의 종료)

I hope you found it informative, and I will see you in the next lecture.  
유익했기를 바라며, 다음 강의에서 뵙겠습니다.  
(마무리 인사)

---

## Key Takeaways  
## 핵심 요약  

- RDS Custom provides access to the underlying operating system and database customization for Oracle and Microsoft SQL Server.  
- RDS Custom은 Oracle 및 Microsoft SQL Server의 기본 운영체제와 DB 커스터마이징 접근을 제공합니다.  

- Unlike standard RDS, RDS Custom allows SSH or SSM Session Manager access to the EC2 instance behind the database.  
- 표준 RDS와 달리, RDS Custom은 DB 뒤 EC2 인스턴스에 SSH 또는 SSM Session Manager 접근이 가능합니다.  

- It is recommended to deactivate automation mode and take a database snapshot before performing customizations to avoid potential issues.  
- 잠재적 문제 방지를 위해 커스터마이징 전 자동화 모드 비활성화 및 DB 스냅샷 권장.  

- Standard RDS manages the entire database and operating system without user intervention, while RDS Custom offers full administrative access for advanced configurations.  
- 표준 RDS는 사용자 개입 없이 전체 DB와 운영체제를 관리하지만, RDS Custom은 고급 구성에 대한 전체 관리 권한을 제공합니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+250XP**
* 아이템: **"RDS Custom 키트" (+15% 관리 효율)**
* 업적 달성: **"고급 DB 관리 마스터"** 🏅

이 자료를 통해 **RDS Custom 접근권한, 커스터마이징, SSH/SSM 관리** 개념을 학습할 수 있습니다.
