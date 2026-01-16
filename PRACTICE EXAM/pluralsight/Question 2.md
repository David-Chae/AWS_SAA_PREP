Question 2
A company has an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances hosting its retail sales application. Any significant downtime can result in significant profit loss. The solution architecture also includes an Application Load Balancer and an Amazon Relational Database Service (Amazon RDS) database in a Multi-AZ deployment. What occurs automatically to maintain high availability if the primary database instance fails?

Correct Answers
Selected
The CNAME is switched from the primary database instance to the secondary.

Rationale: When a Multi-AZ Amazon RDS deployment detects a primary instance failure, the system automatically updates the DNS record to point the database endpoint's CNAME to the standby (secondary) instance, minimizing downtime.

Incorrect Answers
The Elastic IP address for the primary database is moved to the secondary database.

Rationale: Amazon RDS does not use Elastic IP addresses for failover or instance endpoint management. RDS endpoints are managed through DNS names, not static IP addresses.

A Lambda function kicks off a CloudFormation template to deploy a backup database.

Rationale: Amazon RDS Multi-AZ failover is automatic; no AWS Lambda or CloudFormation workflow is required to stand up a new instance during a failover event.

Route 53 points the CNAME to the secondary database instance.

Rationale: Amazon RDS automatically manages the DNS name at the AWS RDS service level, not through Amazon Route 53 configuration or manual DNS record updates for endpoints.

좋은 문제야. 이건 **RDS 고가용성 문제의 대표적인 “판단 기준 암기형”**이라서,
아래 기준만 잡히면 **다시는 헷갈릴 일이 없다**.

---

# 🔑 Question 2 판단기준 (RDS Multi-AZ Failover)

## 1️⃣ 문제를 보면 가장 먼저 잡아야 할 핵심 신호

문제에서 이미 **정답의 80%를 알려줌**:

* **Amazon RDS**
* **Multi-AZ deployment**
* **high availability**
* **primary database instance fails**
* **What occurs automatically**

👉 이 다섯 단어가 동시에 나오면,
**“AWS가 자동으로 처리하는 RDS 표준 장애 조치 메커니즘”**을 묻는 문제다.

---

## 2️⃣ 가장 중요한 1줄 판단 공식

> **“RDS Multi-AZ 장애 조치는 인프라 이동이 아니라 DNS 전환이다.”**

이 한 문장이 이 문제의 전부다.

---

## 3️⃣ 왜 정답이 “CNAME 전환”인가?

### 🔍 RDS Multi-AZ의 구조를 정확히 이해해야 한다

* RDS Multi-AZ는:

  * **Primary DB**
  * **Standby DB (다른 AZ)**
* 두 인스턴스는 **동기식 복제**
* 애플리케이션은 **단 하나의 DB Endpoint**만 사용

이 Endpoint는:

* **고정 IP ❌**
* **Elastic IP ❌**
* **Route 53 레코드 ❌**
* ✅ **AWS가 관리하는 DNS 이름(CNAME)**

---

### 🔄 장애 발생 시 실제로 일어나는 일

1. Primary DB 장애 감지
2. Standby DB를 **새 Primary로 승격**
3. **DB Endpoint의 CNAME이 자동으로 Standby를 가리키도록 변경**
4. 애플리케이션은 **같은 endpoint로 재연결**

👉 그래서 정답은:

> **“The CNAME is switched from the primary database instance to the secondary.”**

---

## 4️⃣ 오답들이 왜 “전형적인 미끼”인지

### ❌ Elastic IP 이동

**판단 기준**

> “Elastic IP = EC2 전용 개념”

* RDS는 **EIP를 쓰지 않는다**
* RDS는 **IP 기반 접근 자체를 노출하지 않는다**

👉 **EIP 보이면 RDS 문제에서 바로 제거**

---

### ❌ Lambda + CloudFormation

**판단 기준**

> “RDS Multi-AZ는 완전 자동이다”

* 장애 조치에:

  * Lambda ❌
  * CloudFormation ❌
  * 사용자 개입 ❌

👉 “자동(automatically)” + “Multi-AZ” = **사용자 워크플로우 전부 오답**

---

### ❌ Route 53이 CNAME 변경

**판단 기준**

> “RDS Endpoint DNS는 Route 53 콘솔에서 만지지 않는다”

* Route 53은:

  * 웹 트래픽
  * 글로벌 라우팅
  * 사용자 DNS 관리용
* **RDS 내부 엔드포인트는 AWS RDS 서비스가 직접 관리**

👉 “Route 53이 DB 엔드포인트를 바꾼다”는 문장은 거의 항상 오답

---

## 5️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 **시험장에서 이렇게 처리하면 된다**:

* ✔ RDS + Multi-AZ + failover
* ✔ “자동으로 무엇이 일어나는가?”

👉 **DNS(CNAME) 전환**

그리고 동시에:

* ❌ EIP
* ❌ Route 53 수동 설정
* ❌ Lambda / CloudFormation
  → 전부 즉시 제거

---

## 6️⃣ 이 문제의 상위 메타 규칙 (다른 문제에도 그대로 적용됨)

> **“Managed Service의 고가용성은 ‘리소스 이동’이 아니라 ‘엔드포인트 추상화’로 해결한다.”**

* RDS → DNS
* ALB → Target health check
* S3 → 내부 복제
* DynamoDB → 내부 파티션

👉 **AWS 시험은 ‘사용자가 뭘 안 해도 되는가’를 고르는 시험**

---

원하면 다음으로:

* 🔥 **RDS / Aurora / DynamoDB 장애 조치 비교표**
* 🔥 **“DNS 전환 vs 리소스 이동” 구분 문제 모음**
* 🔥 **이 문제랑 헷갈리는 Read Replica / Multi-AZ 구분 공식**

중에서 바로 이어서 설명해줄게.
