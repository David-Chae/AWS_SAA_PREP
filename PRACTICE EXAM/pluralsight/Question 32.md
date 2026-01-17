Question 32
A company has an application for sharing static content, such as photos. As usage grows globally, the company faces higher latency for users. What AWS services can host a static website, serve content to worldwide users, and address latency and cost concerns?

Correct Answers
Use Amazon CloudFront to serve content globally by caching images from Amazon Simple Storage Service (Amazon S3) to reduce latency and cost.

Rationale: Amazon CloudFront is a content delivery network that delivers static content from edge locations close to users. It integrates seamlessly with Amazon S3, improving latency and minimizing data transfer costs.

Incorrect Answers
Use AWS Global Accelerator directing traffic to Application Load Balancers in each region, with EC2 instances accessing a shared Amazon Elastic File System volume.

Rationale: AWS Global Accelerator is designed for improving availability and performance of non-HTTP/S applications, but using EC2 and Amazon Elastic File System adds unnecessary complexity and cost for serving static content.

Selected
Host a static website on Amazon Simple Storage Service (Amazon S3) with cross-region replication and use Amazon Route 53 geolocation routing to serve users from the nearest region.

Rationale: S3 static website hosting supports basic static content delivery, but cross-region replication and Amazon Route 53 geolocation routing significantly increase management overhead and costs without delivering CDN-level latency improvements.

Use AWS CloudFormation to deploy static content hosted on Amazon Simple Storage Service (Amazon S3) to minimize latency and cost.

Rationale: AWS CloudFormation is an infrastructure automation tool, not a content delivery network or hosting service. It cannot reduce latency for end users or automate global content delivery for static content.

이 문제는 **“정적 콘텐츠 + 글로벌 사용자 + 지연시간/비용”**이라는 3요소를 정확히 매칭할 수 있는지를 보는 **전형적인 CDN 판단 문제**야.
핵심은 **무엇을 서빙하느냐(정적)** 와 **어디서 서빙하느냐(엣지)** 다.

---

# 🔑 Question 32 판단기준 (Static Content + Global + Latency/Cost)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제 문장을 구조적으로 분해하면 이렇게 된다:

* **static content (photos)**
* **users globally**
* **higher latency**
* **address latency and cost**
* **host a static website**

👉 이 조합이 나오면,
이건 **서버 아키텍처 문제가 아니라 “콘텐츠 전송 방식” 문제**다.

---

## 2️⃣ 1차 판단 분기: “서버를 늘릴까, 캐시를 가까이 둘까?”

### 핵심 분기 기준

> **정적 콘텐츠의 지연시간 문제는 ‘서버 수’가 아니라 ‘거리’ 문제다.**

* EC2 / ALB / EFS → 서버 중심 사고 ❌
* **CDN(엣지 캐시)** → 거리 문제 해결 ⭕

👉 **정적 + 글로벌 + 지연** = CDN이 거의 정답 영역

---

## 3️⃣ 정답으로 바로 가는 판단 공식

### ✅ 핵심 판단 공식

> **“정적 콘텐츠 + 글로벌 사용자 + 지연/비용 = CloudFront + S3”**

이 공식은 AWS 시험에서 거의 고정이다.

---

## 4️⃣ 왜 CloudFront + S3가 정답인가?

### 🔍 역할 분담이 완벽히 맞는다

* **Amazon S3**

  * 정적 파일 저장
  * 높은 내구성
  * 서버 관리 불필요
* **CloudFront**

  * 전 세계 엣지 로케이션에 캐시
  * 사용자와 가까운 곳에서 제공
  * 캐시로 **지연 감소 + S3 호출 비용 감소**

👉 **지연과 비용을 동시에 해결하는 유일한 조합**

---

## 5️⃣ 오답들이 왜 탈락하는지 (판단기준)

### ❌ S3 + Cross-Region Replication + Route 53

**판단기준**

> “Replication + DNS는 CDN이 아니다”

* Region 수만큼 운영 복잡도 증가
* 사용자와의 물리적 거리 문제 완전 해결 ❌
* 캐시 없음 → 반복 요청마다 S3 호출

👉 **글로벌 정적 콘텐츠 문제에서 ‘CDN 없는 설계’는 거의 항상 오답**

---

### ❌ Global Accelerator + ALB + EC2 + EFS

**판단기준**

> “Global Accelerator는 ‘정적 콘텐츠 CDN’이 아니다”

* 주 용도: TCP/UDP 애플리케이션 가속
* EC2 + EFS:

  * 서버 관리 필요
  * 비용 큼
  * 정적 콘텐츠에 과잉 설계

👉 **정적 콘텐츠 문제에 EC2가 보이면 거의 오답**

---

### ❌ CloudFormation 사용

**판단기준**

> “CloudFormation은 배포 도구이지, 성능 도구가 아니다”

* 인프라 자동화 ⭕
* 지연 감소 ❌
* 콘텐츠 전송 ❌

👉 **성능/지연 문제에서 IaC 도구는 정답이 될 수 없다**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 시험장에서 이렇게 처리하면 된다:

1. Static content
2. Global users
3. Latency + cost

➡ **CloudFront**

그리고 Origin으로:
➡ **S3**

즉시 제거:

* EC2 / EFS
* Cross-region replication
* Route 53 단독
* CloudFormation

---

## 7️⃣ 상위 메타 규칙 (다른 문제에도 그대로 적용)

> **“정적 콘텐츠의 글로벌 성능 문제는 ‘CDN’으로만 푼다.”**

* CDN = CloudFront
* Origin = S3
* 서버는 등장할수록 오답 확률 ↑

---

## 8️⃣ 한 줄 요약

> **“글로벌 사용자에게 정적 콘텐츠를 빠르고 싸게 = CloudFront + S3”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **CloudFront vs Global Accelerator 판단표**
* 🔥 **정적/동적 콘텐츠 구분 문제 모음**
* 🔥 **S3 Static Hosting 함정 패턴 정리**

중에서 바로 이어서 정리해줄게.
