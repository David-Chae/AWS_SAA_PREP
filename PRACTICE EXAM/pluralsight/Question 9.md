## Question 9
You are designing a relational database solution for a financial services organization. The database must remain highly available within the Oregon Region and recover quickly if an Availability Zone becomes unavailable. Which AWS solution best meets these requirements?

### Correct Answers
Selected
Enable Multi-AZ deployment for the Amazon RDS instance.

Rationale: Amazon RDS Multi-AZ automatically provisions a synchronous standby in another Availability Zone within the same region. It supports automatic failover with minimal downtime during AZ outages, aligning with high availability needs.

Incorrect Answers
Use an Amazon Aurora global database.

Rationale: Aurora global databases provide cross-region disaster recovery, not intra-region high availability. They are designed to withstand regional outages, which is not the requirement in this scenario.

Create a read replica in the US East (N. Virginia) Region.

Rationale: Read replicas support cross-region read scalability and disaster recovery but do not enable automatic failover within a single region or for write workloads.

Deploy separate RDS instances in multiple regions and switch traffic manually during outages.

Rationale: This approach introduces manual failover and complexity, which do not align with requirements for quick recovery and high availability within a single region.

이 문제는 **RDS 가용성 계층을 정확히 구분할 수 있는지**를 보는 아주 정직한 문제야.
핵심은 **“어디까지의 장애를 막으려는가”**를 정확히 읽는 거다.

---

# 🔑 Question 9 판단기준 (RDS 고가용성: Region vs AZ)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제에 이미 답이 숨어 있다. 밑줄 치듯이 보자.

* **relational database**
* **highly available**
* **within the Oregon Region**
* **recover quickly if an Availability Zone becomes unavailable**

👉 이 네 문장이 동시에 나오면, 이건 **“AZ 장애 대응용 고가용성”** 문제다.
**Region 장애 대응 문제가 아니다.**

---

## 2️⃣ 1차 분기 기준: “AZ 장애냐, Region 장애냐?”

### ✅ 판단 공식 (매우 중요)

> **“AZ 장애 = Multi-AZ”**
> **“Region 장애 = Cross-Region / Global”**

이 문제는 명확하게:

* **within the Oregon Region**
* **AZ becomes unavailable**

👉 따라서 **Region 밖으로 나가는 선택지는 전부 과잉 설계(overkill)** 이고 오답.

---

## 3️⃣ 왜 정답이 RDS Multi-AZ인가?

### 🔍 RDS Multi-AZ가 하는 일

* 같은 **Region**
* 다른 **Availability Zone**
* **동기식(synchronous) 복제**
* **자동 failover**
* **DNS 엔드포인트 자동 전환**

👉 결과:

* AZ 하나가 죽어도
* 몇 분 이내 자동 복구
* 애플리케이션 수정 없음

### ✅ 정답 공식

> **“단일 Region + AZ 장애 자동 복구 = RDS Multi-AZ”**

---

## 4️⃣ 오답들이 왜 틀렸는지 “판단 기준”으로 정리

### ❌ Aurora Global Database

**왜 틀렸는가?**

* 목적: **Region 장애 대응**
* 구조: Primary Region + Secondary Region
* 비용/복잡도 큼

👉 **문제에 ‘Region outage’라는 말이 없으면 Global은 오답**

**판단 기준**

> “Global / cross-region이 보이는데, 문제는 AZ만 말한다 → 오답”

---

### ❌ Read Replica in 다른 Region

**왜 틀렸는가?**

* Read Replica:

  * **비동기**
  * **읽기 전용**
  * **자동 failover 아님**

👉 금융 시스템에서:

* write workload 있음
* 자동 복구 필요

**판단 기준**

> “read replica = 확장/DR, HA 아님”

---

### ❌ 수동으로 Region 전환

**왜 틀렸는가?**

* manual switch
* 운영 개입 필요
* 복구 느림

👉 문제 조건:

* **recover quickly**
* **high availability**

**판단 기준**

> “manual 이라는 단어가 암시되면 HA 문제에서 탈락”

---

## 5️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 보면, 머릿속에서 이렇게 자동으로 돌아가야 한다:

1. Relational DB
2. High availability
3. Within one Region
4. AZ 장애

➡ **Multi-AZ**

그리고 동시에 제거:

* Global
* Cross-region
* Manual
* Read replica

---

## 6️⃣ 이 문제의 상위 메타 규칙 (다른 문제에도 그대로 적용)

> **“AWS 시험에서 ‘가용성’은 항상 ‘장애 범위’로 정의된다.”**

| 장애 범위    | 정답 패턴                    |
| -------- | ------------------------ |
| Instance | Auto Scaling             |
| AZ       | **Multi-AZ**             |
| Region   | Global DB / Cross-Region |
| Global   | Multi-Region + DNS       |

👉 **범위를 넘는 설계는 거의 항상 오답**

---

## 7️⃣ 한 줄로 요약

> **“Region 안에서 AZ 하나 죽는 걸 막고 싶다 = RDS Multi-AZ”**

이 문장이 자동으로 떠오르면,
이 문제는 **0.5초 만에 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **Multi-AZ vs Read Replica vs Global DB 한 장 비교**
* 🔥 **‘가용성’ 키워드별 자동 매칭 표**
* 🔥 **금융/규제 문제에서 자주 나오는 함정 패턴**

중에서 바로 이어서 설명해줄게.
