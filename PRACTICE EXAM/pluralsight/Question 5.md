Question 5
You work for a major gaming company. The company must distribute gaming traffic using the User Datagram Protocol (UDP) among multiple servers to ensure real-time gameplay and high availability. The application must also store matchmaking and session state data in a NoSQL database for scalability. Which solution supports both requirements?

Correct Answers
Selected
Network Load Balancer and Amazon DynamoDB.

Rationale: A Network Load Balancer supports UDP traffic, making it suitable for gaming workloads that require fast, connectionless communication. Amazon DynamoDB provides a fully managed NoSQL database that is highly scalable and widely used in the gaming industry for session state and matchmaking data.

Incorrect Answers
Application Load Balancer with Amazon Aurora.

Rationale: Application Load Balancers support only HTTP and HTTPS (Layer 7), not UDP, and Amazon Aurora is a relational database, not NoSQL, making this pairing unsuitable for the requirements.

Application Load Balancer with Microsoft SQL Server in RDS.

Rationale: Application Load Balancers do not support UDP, and Microsoft SQL Server in Amazon Relational Database Service (Amazon RDS) is a relational, not a NoSQL, database. This does not fulfill either need.

Network Load Balancer with Amazon Aurora Serverless.

Rationale: While the Network Load Balancer supports UDP, Amazon Aurora Serverless is a relational, not NoSQL, database, and is therefore not optimal for NoSQL gaming workloads.


아주 전형적인 **“네트워크 계층 + 데이터 모델 매칭 문제”**야.
이 문제는 지식 문제가 아니라 **신호를 보면 자동으로 조합이 결정되는 판단 문제**다.

아래 기준만 잡히면, 다음에 비슷한 문제는 **생각 없이도 정답이 남는다**.

---

# 🔑 Question 5 판단기준 (UDP + Gaming + NoSQL)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제는 이미 답을 둘로 쪼개서 주고 있다:

### 🔍 네트워크 쪽 신호

* **gaming traffic**
* **real-time gameplay**
* **User Datagram Protocol (UDP)**

### 🔍 데이터 쪽 신호

* **matchmaking**
* **session state**
* **NoSQL**
* **scalability**

👉 이 문제는 **“로드밸런서 1개 + 데이터베이스 1개”를 각각 고르는 문제**다.
서로 섞어서 고민하면 헷갈린다.

---

## 2️⃣ 1단계 판단: “UDP를 처리할 수 있는 로드밸런서는?”

### ✅ 판단 공식

> **“UDP = Layer 4 = Network Load Balancer”**

#### 왜냐하면:

* UDP는:

  * 연결 상태 없음
  * 패킷 기반
  * 포트 레벨에서 분산
* 이걸 처리하는 건 **L4 로드밸런서**

### ❌ 즉시 제거 규칙

* **Application Load Balancer**

  * HTTP / HTTPS 전용
  * Layer 7
  * ❌ UDP 미지원

👉 **문제에 UDP가 보이는 순간, ALB는 바로 제거**

---

## 3️⃣ 2단계 판단: “Gaming session / matchmaking 데이터는 어떤 DB?”

### 🔍 데이터 특성 다시 확인

* 세션 상태
* 매치메이킹
* 빠른 읽기/쓰기
* 수평 확장
* 구조 변경 가능

### ✅ 판단 공식

> **“Session / state / matchmaking = NoSQL = DynamoDB”**

#### 이유:

* 키-값 기반
* 초저지연
* 자동 확장
* 게임 산업에서 **표준 패턴**

### ❌ 즉시 제거 규칙

* **Aurora / SQL Server**

  * 관계형
  * 스키마 고정
  * 트랜잭션 중심
  * ❌ NoSQL 아님

👉 **문제에 ‘NoSQL’이 명시되어 있으면 관계형 DB는 전부 탈락**

---

## 4️⃣ 정답 조합이 자동으로 결정되는 과정

문제를 이렇게 쪼개면 된다:

| 요구사항        | 자동 매칭                     |
| ----------- | ------------------------- |
| UDP 분산      | **Network Load Balancer** |
| NoSQL 상태 저장 | **DynamoDB**              |

👉 그래서 정답은 **NLB + DynamoDB**

---

## 5️⃣ 오답들이 “전형적인 시험 미끼”인 이유

### ❌ ALB + Aurora / SQL Server

**탈락 이유 (2연타)**

* ALB ❌ UDP 미지원
* Aurora / SQL Server ❌ NoSQL 아님

👉 **두 요구사항 모두 실패**

---

### ❌ NLB + Aurora Serverless

**탈락 이유**

* NLB ✅ (UDP OK)
* Aurora Serverless ❌ (관계형)

👉 **네트워크는 맞았지만 데이터 모델에서 탈락**

---

## 6️⃣ 시험장에서 쓰는 초압축 판단 카드

시험 중에는 이렇게 처리하면 된다:

* UDP 보임 → **NLB**
* NoSQL 명시 → **DynamoDB**
* Gaming / real-time → **저지연 + 수평 확장**

👉 이 3개가 동시에 나오면
**NLB + DynamoDB 외에는 볼 필요 없음**

---

## 7️⃣ 이 문제의 상위 메타 판단 규칙 (매우 중요)

> **“AWS 시험에서 프로토콜은 로드밸런서를, 데이터 성격은 DB를 즉시 결정한다.”**

* TCP/UDP → NLB
* HTTP/HTTPS → ALB
* State / session → NoSQL
* Transaction / schema → RDB

이 규칙은 **수십 문제에 그대로 재사용된다**.

---

원하면 다음으로:

* 🔥 **ALB vs NLB vs Gateway Load Balancer 한 장 비교**
* 🔥 **Gaming / IoT / Streaming 패턴 전용 판단표**
* 🔥 **“UDP 나오면 무조건 제거 리스트”**

중에서 바로 이어서 설명해줄게.
