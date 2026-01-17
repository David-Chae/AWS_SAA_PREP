Question 34
You are the solutions architect for a social media website that uses an Amazon DynamoDB table on the backend. Monitoring reveals that the table begins to throttle requests during peak load, which is slowing down the application. You have been asked to address the throttling, improve performance, and reduce operational complexity. What should you do?

Correct Answers
Selected
Use Amazon DynamoDB auto scaling.

Rationale: Amazon DynamoDB auto scaling automatically manages read and write capacity to match traffic, fixes throttling, and reduces operational complexity by removing the need for manual scaling adjustments.

Incorrect Answers
Put the DynamoDB table behind an Auto Scaling group.

Rationale: Amazon EC2 Auto Scaling groups manage EC2 instances, not DynamoDB capacity; placing tables behind one does not affect DynamoDB throughput or simplify operations.

Migrate the database to Amazon Relational Database Service (Amazon RDS) for MySQL with Multi-AZ.

Rationale: Migrating to Amazon Relational Database Service (Amazon RDS) for MySQL would not fix DynamoDB throttling and increases operational complexity by switching database types and management models.

Create an Amazon Aurora read replica and spread the load between DynamoDB and Aurora.

Rationale: Aurora read replicas are used for read scaling within Aurora clusters. Spreading load between DynamoDB and Aurora is not technically feasible or supported.


이 문제는 **“DynamoDB 성능 문제를 어떻게 가장 AWS답게, 가장 단순하게 해결하느냐”**를 묻는 전형적인 판단 문제야.
핵심은 **병목의 원인 + 요구 조건(성능 개선 + 운영 단순화)**를 정확히 매칭하는 것.

---

# 🔑 Question 34 판단기준 (DynamoDB Throttling 해결)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제의 핵심 키워드를 그대로 뽑아보면:

* **Amazon DynamoDB**
* **table begins to throttle requests**
* **during peak load**
* **improve performance**
* **reduce operational complexity**

👉 이 다섯 가지가 동시에 나오면,
이건 **아키텍처 변경 문제가 아니라 “용량 관리 방식” 문제**다.

---

## 2️⃣ 1차 판단: “왜 throttling이 발생하는가?”

### DynamoDB에서 throttling의 원인

> **프로비저닝된 읽기/쓰기 용량이 트래픽보다 부족할 때**

* 테이블은 살아 있음
* 애플리케이션도 정상
* 단지 **피크 트래픽을 감당 못함**

👉 즉, **스케일링 방식이 문제**이지,
👉 **DynamoDB 자체가 잘못된 선택이 아님**

---

## 3️⃣ 정답으로 바로 가는 핵심 판단 공식

### ✅ 판단 공식 (이 문제의 본질)

> **“DynamoDB + throttling + 피크 트래픽 + 운영 단순화 = DynamoDB Auto Scaling”**

이 공식은 거의 암기 수준으로 써도 된다.

---

## 4️⃣ 왜 DynamoDB Auto Scaling이 정답인가?

### 🔍 Auto Scaling이 해결하는 것

* 트래픽 증가 시:

  * Read / Write Capacity Units 자동 증가
* 트래픽 감소 시:

  * 용량 자동 감소 → 비용 절감
* 사람 개입 ❌
* 스크립트 ❌
* 수동 모니터링 ❌

👉 **성능 문제 해결 + 운영 복잡도 감소**를 동시에 만족

---

## 5️⃣ 오답들이 왜 틀렸는지 (판단기준으로 제거)

### ❌ DynamoDB를 Auto Scaling Group 뒤에 둔다

**판단기준**

> “Auto Scaling Group은 EC2 전용 개념”

* DynamoDB는:

  * 서버 없음
  * 인스턴스 없음
* ASG와 개념적으로 연결 불가

👉 **리소스 타입 불일치 → 즉시 제거**

---

### ❌ RDS MySQL로 마이그레이션

**판단기준**

> “문제는 DynamoDB 선택이 아니라 용량 설정이다”

* DB 타입 변경:

  * 운영 복잡도 증가
  * 확장성 저하
* throttling 직접 해결 ❌

👉 **‘운영 단순화’ 요구와 정면 충돌**

---

### ❌ Aurora Read Replica로 부하 분산

**판단기준**

> “DynamoDB와 Aurora는 부하를 나눌 수 없다”

* 서로 다른 DB 엔진
* 데이터 일관성 불가
* 아키텍처적으로 성립 안 함

👉 **기술적으로 말이 안 되는 선택지**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. DynamoDB
2. Throttling
3. Peak load
4. Low ops

➡ **Auto Scaling**

그리고 즉시 제거:

* EC2 ASG
* RDS/Aurora 마이그레이션
* 혼합 DB 아키텍처

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“Managed NoSQL에서 성능 문제는 ‘용량 자동화’로 해결한다.”**

* DynamoDB → Auto Scaling / On-Demand
* RDS → Instance class / Read Replica
* ElastiCache → Node scaling

👉 **서비스를 바꾸기 전에, 먼저 ‘해당 서비스의 자동화 기능’을 본다**

---

## 8️⃣ 한 줄 요약

> **“DynamoDB가 throttling 된다 = Auto Scaling으로 용량을 자동 조절한다.”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.
