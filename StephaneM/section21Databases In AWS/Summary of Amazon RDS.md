## **Amazon RDS를 아주 쉽게 이해하기**

### **1. RDS가 뭐야?**

AWS가 **데이터베이스를 대신 설치하고, 대신 관리해주는 서비스**야.
집에서 컴퓨터에 DB를 직접 설치해서 돌리는 게 아니라, **AWS가 알아서 서버 세팅·백업·보안·업데이트까지 관리**해주는 느낌.

지원하는 DB 종류도 다양해:
PostgreSQL, MySQL, Oracle, SQL Server, MariaDB 등.

---

## **2. 어떤 것을 직접 정해야 해?**

RDS를 쓸 때는 두 가지를 골라야 해:

### ✔ **① 인스턴스(서버) 크기**

→ 마치 카페에서 테이블 크기를 고르는 것처럼,
“얼마나 큰 컴퓨터 파워가 필요하냐”를 정하는 것.

### ✔ **② 저장 공간(EBS) 타입과 크기**

→ SSD냐 HDD냐 같은 느낌.
저장 공간은 부족하면 **자동으로 늘어나도록(auto-scaling)** 옵션도 가능.

---

## **3. 읽기 부하가 많으면: ‘Read Replica’**

서비스 사용자가 많아져서 **조회(SELECT)** 요청이 많아지면
본 DB에 트래픽이 몰릴 수 있어.
그럴 땐 **읽기 전용 복제본(Read Replica)** 을 만들어서 부담을 나눠.

* 원본: 쓰기/읽기
* 복제본: 읽기 전용

예: 쇼핑몰에서 *판매 통계* 같은 분석을 할 때 원본 DB를 건드리지 않고 복제본에서 조회함.

---

## **4. 장애 대비: Multi-AZ**

멀티 AZ는 **재해복구용 예비 DB(standby)** 를 만드는 기능이야.

* 평소에는 예비 DB에 접근 불가
* 원본이 죽었을 때만 자동으로 예비 DB로 넘어감

즉, **고가용성(다운타임 최소화)** 을 위한 장치.

---

## **5. 보안은 이렇게 관리돼**

데이터베이스 보안 관련 기능들:

* **IAM**: 접근 권한 관리
* **유저명 + 비밀번호**, 혹은 일부 엔진은 **IAM 인증**도 가능
* **Security Group**: DB에 들어올 수 있는 네트워크 제한
* **KMS 암호화**: 저장된 데이터 암호화
* **SSL/TLS 암호화**: 전송 중인 데이터 보호

---

## **6. 백업**

자동으로 백업이 되고, **최대 35일**까지 기록을 보관할 수 있어.

* 원하는 시점으로 복원(Point-in-Time Restore) 가능
* 이 과정은 “새로운 DB 인스턴스”로 복구됨
* 장기 보관이 필요하면 **수동 스냅샷**을 찍어서 영구 저장 가능

---

## **7. 유지보수**

AWS가 DB 엔진 업데이트나 보안 패치를 자동으로 해줘.
이때 **일시적인 다운타임이 발생할 수 있음**.

---

## **8. 고급 기능**

* **RDS Proxy**: DB 연결을 효율적으로 관리해주는 중간 서버 같은 것
* IAM 인증 강화 & Secrets Manager와 연동 가능
* **RDS Custom**: Oracle/SQL Server만 가능한 “서버에 직접 손대는 모드”
  (특수한 설정이 필요할 때 사용)

---

## **9. 언제 쓰는 서비스인가?**

주로 **전통적인 관계형 DB(SQL)** 이 필요한 경우:

* 금융 거래
* 주문 처리 시스템
* 로그인/회원 DB
* 예약 시스템
* 애플리케이션 백엔드

즉, **OLTP(트랜잭션 중심 업무)** 에 적합.

---

## **한 줄 요약**

**Amazon RDS는 AWS가 데이터베이스 설치·운영·백업·보안까지 대신 해주는 서비스이며, 개발자는 SQL 쿼리만 신경 쓰면 되도록 만들어진 ‘관리형 DB 서비스’다.**


# Summary of Amazon RDS
# Amazon RDS 요약
# → Amazon RDS의 핵심 개념을 정리하는 섹션입니다.

## Summary of Amazon RDS
## Amazon RDS 요약
## → 반복된 제목. RDS 전체 요약에 집중합니다.

This section provides a summary of the key concepts learned about Amazon RDS.  
이 섹션은 Amazon RDS에 대해 배운 핵심 개념을 요약합니다.  
→ 시험 대비 및 복습용 핵심 포인트.

For detailed explanations, it is recommended to revisit the previous lectures.  
자세한 설명은 이전 강의를 다시 보는 것이 좋습니다.  
→ 요약은 개괄적이며 세부는 강의 참고.

This summary highlights the essential points you should know about Amazon RDS.  
이 요약은 Amazon RDS에서 반드시 알아야 할 핵심 포인트를 강조합니다.  
→ 시험이나 실무에서 꼭 필요한 지식 정리.

```
🎖️ **게임 보상: DB 전략가 → RDS 초보자 레벨업!**
```

Amazon RDS is a managed service supporting several database engines including PostgreSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, and a custom version of RDS.  
Amazon RDS는 PostgreSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, 그리고 맞춤형 RDS 버전을 지원하는 관리형 서비스입니다.  
→ 다양한 DB 엔진을 통합적으로 지원.

When using Amazon RDS, you need to provision an RDS instance size as well as an EBS volume type and size.  
Amazon RDS를 사용할 때는 인스턴스 크기와 EBS 볼륨 종류 및 크기를 프로비저닝해야 합니다.  
→ 기본 리소스 설정 필요.

Although provisioning is required, there is auto-scaling capability available for the storage layer.  
프로비저닝이 필요하지만, 스토리지 계층은 자동 확장이 가능합니다.  
→ 스토리지 관리 부담 완화.

Amazon RDS supports read replicas to scale read capabilities.  
Amazon RDS는 읽기 성능 확장을 위해 읽기 복제본을 지원합니다.  
→ 트래픽 분산에 유리.

If applications need to run analytics against a production database, it is preferable to create a read replica to offload those queries.  
프로덕션 DB에서 분석을 수행해야 한다면 읽기 복제본을 만들어 쿼리 부하를 분산하는 것이 좋습니다.  
→ 운영 DB 안정성 보장.

For high availability, you can use Multi-AZ deployments to have a standby database.  
고가용성을 위해 Multi-AZ 배포를 사용하면 대기 DB를 둘 수 있습니다.  
→ 장애 대비 기능.

This standby database is available only in case of disaster and cannot be used to perform queries.  
이 대기 DB는 재해 발생 시에만 사용 가능하며 쿼리를 실행할 수는 없습니다.  
→ 평상시에는 읽기 불가.

```
🎖️ **게임 보상: RDS 초보자 → RDS 엔지니어 레벨업!**
```

## Security in Amazon RDS
## Amazon RDS의 보안
## → RDS에서 보안을 어떻게 다루는지 설명합니다.

Security for your RDS database is managed through IAM.  
RDS 데이터베이스의 보안은 IAM을 통해 관리됩니다.  
→ 접근 제어 기반.

You can use username and password authentication to connect to your database, and for some engines, IAM authentication is also supported.  
사용자명/비밀번호 인증을 사용할 수 있고, 일부 엔진에서는 IAM 인증도 지원합니다.  
→ 인증 방식 다양화.

Network security is enforced using security groups.  
네트워크 보안은 보안 그룹을 통해 강제됩니다.  
→ AWS VPC 보안 연동.

Encryption at rest is handled by AWS Key Management Service (KMS), and intrinsic encryption is available using SSL and TLS protocols.  
저장 데이터 암호화는 KMS로 처리되고, 전송 중 암호화는 SSL/TLS 프로토콜로 가능합니다.  
→ 데이터 보호 이중화.

```
🎖️ **게임 보상: RDS 엔지니어 → RDS 보안 전문가 레벨업!**
```

## Backup and Recovery
## 백업과 복구
## → 데이터 안전성을 보장하는 기능입니다.

Amazon RDS provides automated backups with a retention period of up to 35 days.  
Amazon RDS는 최대 35일간 유지되는 자동 백업을 제공합니다.  
→ 단기 복구 보장.

Using automated backups, you can perform point-in-time restores to any moment within the retention window.  
자동 백업을 통해 보존 기간 내 원하는 시점으로 복원할 수 있습니다.  
→ 세밀한 복구 가능.

This process creates a new database instance from the backup.  
이 과정은 백업으로부터 새 DB 인스턴스를 생성합니다.  
→ 원본 DB를 건드리지 않고 복구.

For longer-term backup retention, manual database snapshots can be created and stored indefinitely.  
장기 보관을 위해 수동 DB 스냅샷을 만들어 무기한 저장할 수 있습니다.  
→ 영구 보관 기능.

```
🎖️ **게임 보상: RDS 보안 전문가 → RDS 백업 마스터 레벨업!**
```
