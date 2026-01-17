
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


Question 35
You are the solutions architect for an online booking system for vacations. The system uses Amazon Elastic Compute Cloud (EC2) instances on the frontend to poll an Amazon Simple Queue Service (SQS) queue. You have discovered that some bookings are being processed twice, causing customers to pay multiple times for the same reservation. This is creating significant problems for your customer service team. What should you do to prevent this issue from happening in the future?

Correct Answers
Use an Amazon Simple Queue Service (SQS) FIFO queue instead.

Rationale: FIFO queues support exactly-once processing and message deduplication with a five-minute dedupe window, eliminating duplicate message delivery and solving double processing issues.

Incorrect Answers
Replace SQS with Amazon Simple Workflow Service (SWF).

Rationale: Amazon Simple Workflow Service (SWF) is designed for complex workflow management; it does not prevent duplicate messages in the same way as FIFO SQS and may involve re-architecting the application.

Change the message size in Amazon Simple Queue Service (SQS).

Rationale: The message size is related to the amount of data that can be sent in a single message. Changing the message size doesn't address the issue of duplicate processing but can be relevant if you need to ensure that your messages can accommodate all necessary data.

Selected
Alter the visibility timeout of Amazon Simple Queue Service (SQS).

Rationale: The visibility timeout determines how long a message remains invisible in the queue after a worker starts processing it. Changing the visibility timeout can help in some scenarios, but it won't completely prevent duplicate processing. It's more about giving your workers additional time to process messages without them becoming visible to other workers.

이 문제는 **SQS의 전달 보장 모델을 정확히 이해하고 있는지**를 묻는 핵심 문제야.
핵심은 **“왜 중복 처리(duplicate processing)가 발생했는가”**와 **“그걸 구조적으로 없앨 수 있는가”**다.

---

# 🔑 Question 35 판단기준 (SQS 중복 처리 방지)

## 1️⃣ 문제에서 즉시 잡아야 할 핵심 신호

문제를 핵심 키워드로 압축하면:

* **EC2 workers**
* **polling SQS**
* **bookings processed twice**
* **customers charged multiple times**
* **prevent this issue in the future**

👉 여기서 가장 중요한 문장은
**“processed twice” + “prevent in the future”** 다.

이건 단순 튜닝 문제가 아니라
👉 **메시지 전달 보장 수준(Delivery semantics)** 문제다.

---

## 2️⃣ 1차 판단: SQS Standard의 본질

### SQS Standard Queue의 기본 특성

> **At-least-once delivery (최소 1회 전달)**

즉:

* 같은 메시지가 **두 번 이상 전달될 수 있음**
* AWS 시험에서는 이게 **의도된 동작**

👉 따라서 **Standard Queue를 쓰는 한, 중복 처리 가능성은 “버그가 아니라 설계 특성”**이다.

---

## 3️⃣ 정답으로 가는 핵심 판단 공식

### ✅ 이 문제의 핵심 공식

> **“중복 처리를 구조적으로 없애야 한다 = SQS FIFO”**

---

## 4️⃣ 왜 SQS FIFO Queue가 정답인가?

### 🔍 FIFO Queue의 결정적 차이

* **Exactly-once processing**
* **Message deduplication**
* **Ordering 보장**
* 5분 dedupe window 제공

👉 결과:

* 같은 예약 메시지가 **한 번만 처리**
* 결제 중복 발생 ❌
* 애플리케이션 로직 복잡도 ↓

👉 문제 요구사항과 **정확히 일치**

---

## 5️⃣ 오답들이 왜 틀렸는지 (판단기준으로 제거)

### ❌ Visibility Timeout 변경

**판단기준**

> “Visibility timeout은 ‘완화’이지 ‘해결’이 아니다”

* 처리 시간이 길 때 도움은 됨
* 하지만:

  * 워커 크래시
  * 네트워크 오류
  * 재시도 발생 시
    → **중복 전달 여전히 가능**

👉 **‘prevent in the future’ 요구 충족 ❌**

---

### ❌ Amazon SWF로 교체

**판단기준**

> “워크플로우 관리 ≠ 메시지 중복 방지”

* SWF:

  * 복잡한 상태 머신용
  * 재설계 필요
* 단순 예약 처리에는 과잉 설계

👉 **운영 복잡도 증가 + 문제 핵심 불일치**

---

### ❌ Message size 변경

**판단기준**

> “메시지 크기는 전달 횟수와 무관”

* payload 크기 문제 ❌
* 중복 처리 문제 ❌

👉 **문제의 원인과 완전히 무관**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. SQS
2. 중복 처리 발생
3. “앞으로 절대 안 생기게”

➡ **FIFO Queue**

그리고 즉시 제거:

* Visibility timeout 조정
* Message size
* SWF

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘중복 처리’는 튜닝이 아니라 ‘큐 타입 선택’ 문제다.”**

* Standard Queue → at-least-once
* FIFO Queue → exactly-once

👉 **튜닝 옵션은 보조 수단일 뿐, 보장 모델을 바꾸지 못한다**

---

## 8️⃣ 한 줄 요약

> **“SQS에서 중복 처리로 금전 문제가 발생한다 = FIFO Queue로 바꾼다.”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.




Question 37
A company has an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances hosting its retail sales application. Any significant downtime can result in large profit losses. The architecture includes an Application Load Balancer and an Amazon Relational Database Service (Amazon RDS) database in a Multi-AZ deployment. The company has an aggressive Recovery Time Objective (RTO) for disaster recovery. How long does an Amazon RDS Multi-AZ failover typically take to complete?

Correct Answers
One to two minutes.

Rationale: Amazon Relational Database Service (Amazon RDS) Multi-AZ failovers typically complete within 60 to 120 seconds. This is standard for Multi-AZ deployments and aligns with AWS documentation and typical RTO planning.

Incorrect Answers
Almost instantly.

Rationale: Failover is not instantaneous. There is always some delay due to DNS propagation, connection draining, and promotion of the standby instance, so it cannot be considered immediate.

Within an hour.

Rationale: Multi-AZ failovers are designed for high availability and typically finish within a few minutes, not up to an hour, which would be considered unacceptable for most production applications.

Selected
Under 10 minutes.

Rationale: While accurate that failover is often under 10 minutes, AWS documentation and real-world measurements show the process usually takes significantly less time.


이 문제는 **숫자를 외웠는지**를 묻는 게 아니라,
**RDS Multi-AZ의 “가용성 수준(RTO 범위)”를 정확히 감각적으로 알고 있느냐**를 보는 문제야.

핵심은 **“어떤 수준의 고가용성 기술인가?”**를 기준으로 시간을 판단하는 거다.

---

# 🔑 Question 37 판단기준 (RDS Multi-AZ Failover 시간)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 핵심 신호

문제에 이미 범위를 좁혀주는 단서가 다 들어 있다:

* **Auto Scaling + ALB**
* **RDS Multi-AZ**
* **aggressive RTO**
* **downtime = 큰 손실**

👉 이건
**“재해 복구(DR)” 문제가 아니라
“고가용성(HA) 장애 조치 시간”** 문제다.

---

## 2️⃣ 1차 판단 기준: “HA vs DR”

### 아주 중요한 구분

> **Multi-AZ = High Availability (HA)**
> **Cross-Region = Disaster Recovery (DR)**

* HA는:

  * 분 단위
  * 자동
  * 서비스 연속성 목적
* DR은:

  * 수십 분~시간 단위
  * 데이터 보호/지역 장애 목적

👉 문제는 **Multi-AZ**만 언급 → **분 단위가 정답 범위**

---

## 3️⃣ 정답으로 가는 핵심 판단 공식

### ✅ 이 문제의 결정 공식

> **“RDS Multi-AZ 장애 조치 시간 = 약 1~2분”**

이건 AWS 시험에서 **사실상 기준값**처럼 쓰인다.

---

## 4️⃣ 왜 “1~2분”이 정답인가?

### 🔍 Multi-AZ failover에서 실제로 일어나는 단계

1. Primary DB 장애 감지
2. Standby DB를 Primary로 승격
3. **DB Endpoint의 DNS(CNAME) 전환**
4. 애플리케이션 재연결

이 과정 때문에:

* **즉시(0초)** ❌
* **수십 분/시간** ❌
* **짧은 분 단위(보통 60~120초)** ⭕

👉 그래서 AWS 문서/시험 기준값이 **1~2분**

---

## 5️⃣ 오답들이 왜 틀렸는지 (판단기준으로 제거)

### ❌ Almost instantly

**판단 기준**

> “DNS가 개입되면 ‘즉시’는 불가능”

* DNS 전환
* 커넥션 재시도
* 내부 상태 전환

👉 **‘즉시’라는 표현은 시험에서 거의 항상 미끼**

---

### ❌ Under 10 minutes

**판단 기준**

> “너무 넓은 범위는 시험에서 오답”

* 사실일 수는 있지만
* **RTO 질문은 ‘대표값’을 묻는다**

👉 시험은 **‘정확한 클래스’**를 원한다

---

### ❌ Within an hour

**판단 기준**

> “시간 단위면 DR이지 HA가 아니다”

* Multi-AZ 설계 목적과 정면 충돌

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. RDS Multi-AZ
2. Aggressive RTO
3. High availability

➡ **1~2 minutes**

그리고 즉시 제거:

* instantly
* tens of minutes
* hours

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘고가용성’은 항상 ‘분 단위’,
> ‘재해 복구’는 ‘수십 분~시간 단위’다.”**

| 기술              | 장애 범위  | 시간 감각    |
| --------------- | ------ | -------- |
| RDS Multi-AZ    | AZ     | **1–2분** |
| Read Replica    | 수동     | 수 분~     |
| Cross-Region DR | Region | 수십 분~시간  |

---

## 8️⃣ 한 줄 요약

> **“RDS Multi-AZ failover 시간 = 약 1~2분”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **RDS/Aurora 가용성·복구 시간 비교표**
* 🔥 **RTO/RPO 숫자 감각 문제 전용 요약**
* 🔥 **‘aggressive RTO’가 나오면 바로 고르는 기준표**

이어서 정리해줄게.

Question 41
You are a solutions architect working for a biotech company that has a large private cloud deployment using VMware. You have been tasked to set up a disaster recovery solution on AWS. What is the simplest way to achieve this?

Correct Answers
Selected
Purchase VMware Cloud on AWS, leveraging VMware disaster recovery technologies and the speed of AWS cloud to protect your virtual machines.

Rationale: VMware Cloud on AWS is a managed service jointly engineered by AWS and VMware, enabling seamless integration of on-premises VMware workloads with AWS infrastructure. It supports built-in VMware disaster recovery tools, simplifies operations, and eliminates the need for custom EC2 or manual vCenter deployments.

Incorrect Answers
Deploy an Amazon Elastic Compute Cloud (EC2) instance into a private subnet and install VMware vCenter on it.

Rationale: Manually installing vCenter on a single EC2 instance does not provide an integrated, supported, or scalable solution. This approach adds complexity and lacks redundancy, manageability, and vendor support for disaster recovery.

Use the VMware landing page on AWS to provision an EC2 instance with VMware vCenter installed on it.

Rationale: There is no official AWS or VMware landing page or automated method to directly provision EC2 with vCenter pre-installed as a DR solution. Disaster recovery still requires proper integration with VMware Cloud on AWS or equivalent service.

Deploy an Amazon Elastic Compute Cloud (EC2) instance into a public subnet and install VMware vCenter on it.

Rationale: Placing vCenter in a public subnet increases security risks and does not provide integration with AWS-managed DR capabilities. This method is not recommended, not managed, and is operationally complex.


이 문제는 **기술 선택 문제가 아니라 “전환 비용·운영 복잡도·호환성”을 한 번에 판단할 수 있는지**를 보는 문제야.
핵심은 **이미 VMware를 쓰고 있다는 사실을 얼마나 강하게 존중하느냐**다.

---

# 🔑 Question 41 판단기준 (VMware 기반 DR on AWS)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제에 이미 정답 방향이 명확하게 들어 있다:

* **large private cloud deployment using VMware**
* **disaster recovery**
* **simplest way**
* **on AWS**

👉 이 네 가지가 동시에 나오면,
이건 **“VMware → AWS로 갈아타라”**가 아니라
👉 **“VMware를 그대로 AWS로 확장하라”**는 문제다.

---

## 2️⃣ 1차 판단 기준: “이기종 전환이냐, 동일 기술 확장이냐”

### 아주 중요한 분기

> **기존 스택이 크고 안정적일수록, DR에서는 ‘변환’보다 ‘연장’이 정답이다.**

* 기존: VMware
* 요구: DR
* 조건: simplest

👉 **EC2 네이티브로 재설계 ❌**
👉 **VMware 호환 DR ⭕**

---

## 3️⃣ 정답으로 가는 핵심 판단 공식

### ✅ 판단 공식 (이 문제의 본질)

> **“대규모 VMware 환경 + DR + 최소 변경 = VMware Cloud on AWS”**

이 공식은 AWS 시험에서 거의 고정이다.

---

## 4️⃣ 왜 VMware Cloud on AWS가 정답인가?

### 🔍 VMware Cloud on AWS의 핵심 가치

* **기존 VMware 그대로 사용**

  * vSphere
  * vCenter
  * vSAN
  * NSX
* AWS 인프라 위에서 **완전 관리형**
* VMware DR 도구 그대로 사용 가능
* VM 변환/재작성 불필요

👉 결과적으로:

* 재설계 ❌
* 마이그레이션 리스크 ❌
* 운영 학습 비용 ❌

➡ **“simplest way” 조건에 정확히 부합**

---

## 5️⃣ 오답들이 왜 탈락하는지 (판단기준으로 제거)

### ❌ EC2에 vCenter 수동 설치 (Private / Public subnet 공통)

**판단 기준**

> “수동 설치 = 관리형 아님 = 복잡도 증가”

* 단일 EC2:

  * SPOF 발생
  * 고가용성 없음
* VMware 공식 지원 ❌
* AWS-VMware 통합 ❌

👉 **DR 문제에서 ‘수동 설치’는 거의 항상 오답**

---

### ❌ VMware landing page로 EC2 프로비저닝

**판단 기준**

> “존재하지 않는 서비스/방식은 시험 미끼”

* AWS에도
* VMware에도
* 그런 공식 방식 없음

👉 **시험에서 ‘그럴듯한 설명 + 실체 없음’ = 즉시 제거**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. 기존 VMware 대규모 환경
2. DR 필요
3. simplest way

➡ **VMware Cloud on AWS**

그리고 즉시 제거:

* EC2에 수동 설치
* Public subnet 배치
* 비공식/가상 서비스

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘기존 엔터프라이즈 스택’이 강조되면, ‘재작성’이 아니라 ‘관리형 통합 서비스’가 정답이다.”**

* VMware → VMware Cloud on AWS
* Oracle → RDS for Oracle / EC2 Oracle
* SAP → SAP on AWS

👉 **‘기존 투자 보호’가 핵심 키워드**

---

## 8️⃣ 한 줄 요약

> **“대규모 VMware 환경에서 가장 쉬운 AWS DR = VMware Cloud on AWS”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **VMware Cloud on AWS vs EC2 마이그레이션 비교**
* 🔥 **DR 시나리오별 ‘simplest / cheapest / fastest’ 선택표**
* 🔥 **하이브리드·DR 문제에서 자주 나오는 함정 패턴**

이어서 정리해줄게.

---



Question 44
You are working as a solutions architect for an online travel company. Your application is going to use an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances, but you need to decouple components and store messages due to high traffic volume. Which AWS service can you add to meet this requirement?

Correct Answers
Selected
Implement Amazon Simple Queue Service (Amazon SQS) for message storage during high-volume traffic.

Rationale: Amazon Simple Queue Service (Amazon SQS) is a fully managed message queue service designed for decoupling and buffering communications in distributed, auto-scaled applications. It is reliable, cost-effective, scalable, and purpose-built for asynchronous message storage and processing.

Incorrect Answers
Implement Amazon ElastiCache as a storage location for messages when high volumes of traffic are present.

Rationale: Amazon ElastiCache is an in-memory cache solution, not a message queue. While it can temporarily buffer data, it is not designed for durable message storage or decoupled asynchronous processing in autoscaled environments.

Configure Amazon Relational Database Service (Amazon RDS) read replicas as a storage location for messages during high volumes of traffic.

Rationale: Amazon RDS read replicas provide read scalability for relational databases but are not designed as a message buffering or queueing solution. Using them for message queuing is not maintainable or efficient at high scale.

Implement Amazon Simple Workflow Service (Amazon SWF), which initiates an AWS Lambda function to process the messages during high volume traffic loads.

Rationale: Amazon Simple Workflow Service (Amazon SWF) is an orchestration service for managing stateful, long-running workflows. It is not a simple message buffer or decoupling mechanism for high-volume transactional message ingestion.




이 문제는 **“트래픽 급증 상황에서 컴포넌트를 어떻게 느슨하게 결합(decouple)하느냐”**를 묻는 **전형적인 메시징 패턴 판단 문제**야.
핵심은 **Auto Scaling 환경에서 ‘완충(buffer)’ 역할을 누가 맡느냐**다.

---

# 🔑 Question 44 판단기준 (Decoupling + High Traffic)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제의 핵심 키워드를 그대로 정리해보면:

* **Auto Scaling group of EC2**
* **high traffic volume**
* **decouple components**
* **store messages**

👉 이 네 가지가 동시에 나오면,
이건 **데이터 저장 문제도, 캐시 문제도 아닌 “비동기 메시징” 문제**다.

---

## 2️⃣ 1차 판단 기준: “왜 decoupling이 필요한가?”

### 핵심 이유

> **트래픽이 몰릴 때, 생산자(producer)와 소비자(consumer)를 직접 연결하면 시스템이 같이 무너진다.**

* EC2가 Auto Scaling으로 늘어남
* 요청 폭주
* 즉시 처리 못 하면:

  * 타임아웃
  * 장애 전파
  * 사용자 오류

👉 그래서 중간에 **큐(queue)** 가 필요하다.

---

## 3️⃣ 정답으로 바로 가는 핵심 판단 공식

### ✅ 이 문제의 핵심 공식

> **“Decouple + High traffic + Message storage = SQS”**

AWS 시험에서 이 공식은 거의 고정이다.

---

## 4️⃣ 왜 Amazon SQS가 정답인가?

### 🔍 SQS의 역할이 문제 요구와 정확히 일치

* **비동기 메시지 큐**
* 트래픽 스파이크 시:

  * 메시지를 **안전하게 버퍼링**
  * 소비자는 자기 속도로 처리
* EC2 Auto Scaling과 자연스럽게 연동
* 완전 관리형 (운영 부담 최소)

👉 **decoupling + buffering + scale**
👉 이 3가지를 동시에 만족하는 서비스가 SQS다.

---

## 5️⃣ 오답들이 왜 탈락하는지 (판단기준으로 제거)

### ❌ ElastiCache

**판단기준**

> “Cache ≠ Queue”

* ElastiCache:

  * 빠른 조회용
  * 휘발성(in-memory)
* 메시지:

  * 내구성 필요
  * 재시도/보장 필요

👉 **‘store messages’라는 단어가 나오면 Cache는 오답**

---

### ❌ RDS Read Replica

**판단기준**

> “DB는 메시지 큐가 아니다”

* Read Replica:

  * 읽기 확장용
  * 트랜잭션 메시지 버퍼 ❌
* 고트래픽 시:

  * 락
  * 비용 폭증

👉 **메시징에 DB 쓰면 시험에서 거의 항상 오답**

---

### ❌ Amazon SWF

**판단기준**

> “Workflow ≠ Message buffer”

* SWF:

  * 장기 상태 관리
  * 오케스트레이션
* 단순 메시지 저장/전달에는 과잉 설계

👉 **‘high-volume traffic’ 문제에 workflow 서비스는 오답**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 처리하면 된다:

1. Auto Scaling
2. High traffic
3. Decouple
4. Message storage

➡ **SQS**

그리고 즉시 제거:

* Cache
* Database
* Workflow orchestration

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘decouple’이라는 단어는 거의 항상 SQS/SNS를 의미한다.”**

* Decouple + buffer → **SQS**
* Decouple + fan-out → SNS (+ SQS)
* Workflow/state → Step Functions / SWF

👉 **단어 하나가 서비스 하나를 가리킨다**

---

## 8️⃣ 한 줄 요약

> **“Auto Scaling 환경에서 고트래픽을 완충하고 컴포넌트를 분리한다 = SQS”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

Question 45
You are restructuring your infrastructure to enhance the resilience of your web application by decoupling its components. To achieve precise, once-only processing and maintain message order, which type of Amazon Simple Queue Service (SQS) queue should you select?

Correct Answers
Selected
Amazon SQS FIFO queue

Rationale: FIFO (First-In-First-Out) queues delivers messages exactly once and in the precise order in which they were sent, meeting requirements for exactly-once processing and strict message.

Incorrect Answers
Amazon SQS standard queue

Rationale: A standard queue offers at-least-once delivery and best-effort ordering, so it can deliver duplicates and does not guarantee message order.

Amazon SQS dead-letter queue

Rationale: Amazon SQS supports dead-letter queues (DLQ), which other queues (source queues) can target for messages that can't be processed (consumed) successfully. It is not suitable to allow your messages to be processed exactly once and in order.

Amazon SQS LIFO queue

Rationale: There is no such feature as an Amazon SQS LIFO (Last in First Out) queue. SQS only offers standard and FIFO queues



이 문제는 **SQS의 전달 보장 모델과 순서 보장 요구를 정확히 구분할 수 있는지**를 묻는 **정석 판단 문제**야.
핵심은 **“정확히 한 번(Exactly-once)”과 “순서 보장(Ordering)”이 동시에 필요한가**다.

---

# 🔑 Question 45 판단기준 (SQS Queue 선택)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제의 요구사항을 그대로 추리면:

* **decoupling** (컴포넌트 분리)
* **precise, once-only processing**
* **maintain message order**

👉 이 세 가지가 동시에 나오면,
이건 **성능 튜닝이나 설정 문제가 아니라 ‘큐 타입 선택’ 문제**다.

---

## 2️⃣ 1차 판단 기준: “전달 보장 수준(Delivery Semantics)”

### SQS의 두 가지 핵심 모델

AWS 시험에서 이 구분은 매우 중요하다.

| 큐 타입               | 전달 보장         | 순서 보장       |
| ------------------ | ------------- | ----------- |
| **Standard Queue** | At-least-once | Best-effort |
| **FIFO Queue**     | Exactly-once  | Strict FIFO |

👉 문제 요구:

* **once-only processing**
* **message order 유지**

➡ **Standard는 구조적으로 탈락**

---

## 3️⃣ 정답으로 바로 가는 핵심 판단 공식

### ✅ 이 문제의 결정 공식

> **“Exactly-once + Ordering = SQS FIFO Queue”**

이 공식은 **암기 수준**으로 써도 된다.

---

## 4️⃣ 왜 SQS FIFO Queue가 정답인가?

### 🔍 FIFO Queue의 결정적 특성

* 메시지 **중복 제거(deduplication)** 내장
* **정확히 한 번만 처리**
* **전송 순서 보장**
* 메시지 그룹(Message Group ID) 기반 순서 제어

👉 **정합성(consistency)과 무결성(integrity)** 이 중요한 시스템에 최적

---

## 5️⃣ 오답들이 왜 틀렸는지 (판단기준으로 제거)

### ❌ SQS Standard Queue

**판단기준**

> “Standard = 중복 가능 + 순서 보장 없음”

* 빠르고 확장성 좋음
* 하지만:

  * duplicate 가능
  * ordering 보장 ❌

👉 **정확성 요구가 나오면 즉시 탈락**

---

### ❌ Dead-Letter Queue (DLQ)

**판단기준**

> “DLQ는 큐 타입이 아니라 ‘보조 큐’다”

* 실패 메시지 보관용
* 원본 큐의 전달 보장과 무관

👉 **Exactly-once / ordering 요구와 직접적 관계 없음**

---

### ❌ LIFO Queue

**판단기준**

> “존재하지 않는 서비스/기능은 시험 미끼”

* SQS에는:

  * Standard
  * FIFO
    만 존재

👉 **모르는 큐 타입 이름이 나오면 거의 항상 오답**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. Decouple
2. Once-only
3. Ordering

➡ **FIFO Queue**

그리고 즉시 제거:

* Standard
* DLQ
* 존재하지 않는 타입

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘정확성’이 나오면 성능보다 보장을 우선한다.”**

* 정확성/순서 → FIFO
* 처리량/확장성 → Standard

👉 **둘 중 하나만 선택해야 한다**

---

## 8️⃣ 한 줄 요약

> **“정확히 한 번 처리 + 순서 보장 = Amazon SQS FIFO Queue”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **SQS Standard vs FIFO 선택 기준표**
* 🔥 **메시지 중복/순서 함정 문제 모음**
* 🔥 **결제·예약·정산 시스템 큐 설계 패턴**

이어서 정리해줄게.



Question 54
You have a website running on an Amazon Elastic Compute Cloud (EC2) instance. The website is a static HTML site and does not require a database connection. After the site goes viral, the EC2 instance fails under the increased load. You need to ensure that service outages like this do not recur. Which architecture provides the best resiliency?

Correct Answers
Selected
Host the static website on Amazon Simple Storage Service (Amazon S3).

Rationale: Amazon Simple Storage Service (Amazon S3) provides virtually unlimited scale, built-in high availability, and resilience. S3 static website hosting can handle viral traffic without requiring server management or scaling.

Incorrect Answers
Increase the size of the Amazon Elastic Compute Cloud (EC2) instance so it can cope with the load.

Rationale: Upgrading an instance only temporarily boosts capacity. It still leaves a single point of failure and finite scalability, so viral events can lead to another outage.

Migrate the website to AWS CloudFormation.

Rationale: AWS CloudFormation is an infrastructure-as-code tool for provisioning resources, not a hosting service. It does not deliver resiliency by itself or solve scaling challenges for static sites.

Add another Amazon Elastic Compute Cloud (EC2) instance in the same availability zone and place the two instances behind an application load balancer.

Rationale: Adding another instance with a load balancer improves availability, but hosting static content on EC2 remains less resilient and less scalable than using Amazon S3. True resiliency requires eliminating compute/server dependencies.


이 문제는 **“정적(static) 콘텐츠의 장애 원인을 어디서 제거해야 하는가”**를 묻는 **아키텍처 사고 전환 문제**야.
핵심은 **서버를 더 튼튼하게 만들 것인가, 서버 자체를 없앨 것인가**다.

---

# 🔑 Question 54 판단기준 (Static Website Resiliency)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제에 이미 정답 방향이 명확히 들어 있다:

* **static HTML site**
* **does not require a database**
* **EC2 instance fails under load**
* **goes viral**
* **ensure outages do not recur**
* **best resiliency**

👉 이 키워드 조합은 한 가지를 의미한다:

> **“컴퓨팅(EC2)이 병목이자 단일 장애 지점(SPOF)”**

---

## 2️⃣ 1차 판단 기준: “이 사이트에 서버가 필요한가?”

### 아주 중요한 질문

> **정적 사이트에 서버가 필요한가? → 아니다**

* 동적 처리 ❌
* 데이터베이스 ❌
* 세션 ❌
* 연산 ❌

👉 서버(EC2)를 쓰는 순간:

* 스케일 한계 발생
* 장애 지점 생성
* 운영 부담 증가

---

## 3️⃣ 정답으로 바로 가는 핵심 판단 공식

### ✅ 이 문제의 핵심 공식

> **“정적 사이트 + 트래픽 폭증 + 최고 탄력성 = S3 Static Website Hosting”**

이 공식은 AWS 시험에서 **거의 절대 규칙**이다.

---

## 4️⃣ 왜 Amazon S3가 “가장 높은 복원력”인가?

### 🔍 S3의 본질적 강점

* 서버 없음 (Serverless)
* 자동 확장 (무제한에 가까움)
* 다중 AZ에 자동 복제
* 트래픽 급증에 **설계상으로 강함**

👉 **장애 원인 자체(EC2)를 제거**하는 구조

---

## 5️⃣ 오답들이 왜 탈락하는지 (판단기준으로 제거)

### ❌ EC2 인스턴스 크기 증가

**판단기준**

> “Scale up ≠ Resiliency”

* 단일 인스턴스
* 단일 장애 지점 유지
* 트래픽이 더 커지면 또 실패

👉 **근본 원인 해결 아님**

---

### ❌ CloudFormation으로 마이그레이션

**판단기준**

> “IaC는 배포 도구이지 실행 플랫폼이 아니다”

* CloudFormation:

  * 리소스 생성 자동화 ⭕
  * 트래픽 처리 ❌
  * 가용성 제공 ❌

👉 **성능/복원력 문제에서 IaC는 오답**

---

### ❌ EC2 두 대 + ALB

**판단기준**

> “정적 콘텐츠에 EC2가 남아 있으면 불완전한 해결”

* 가용성은 좋아짐 ⭕
* 하지만:

  * 서버 운영 필요
  * 확장 지연
  * 비용 증가

👉 **‘best resiliency’ 요구에는 미달**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

시험 중 이렇게 생각하면 된다:

1. Static site
2. Viral traffic
3. EC2 down
4. Best resiliency

➡ **S3**

그리고 즉시 제거:

* EC2 scaling
* EC2 + ALB
* IaC 도구

---

## 7️⃣ 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘정적 콘텐츠의 최고 복원력’은 항상 ‘서버 제거’다.”**

* EC2 → 제거
* Auto Scaling → 불필요
* Load Balancer → 불필요
* **S3 (± CloudFront)** → 정답

👉 **서버가 남아 있으면 SPOF 가능성 존재**

---

## 8️⃣ 한 줄 요약

> **“바이럴 트래픽에도 절대 안 죽는 정적 사이트 = Amazon S3”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **S3 Static Hosting vs EC2 vs ALB 비교표**
* 🔥 **정적/동적 사이트 아키텍처 판단 맵**
* 🔥 **‘best resiliency’ 키워드 문제 모음**

이어서 정리해줄게.
