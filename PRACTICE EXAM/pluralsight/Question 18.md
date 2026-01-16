## Question 18
You lead a small development team at a Limited Liability Company (LLC). Your team is planning the development of a full-stack web application that uses Next.js with server-side rendering (SSR) on the frontend. The team wants to use AWS for hosting and deployment but lacks in-depth experience with AWS infrastructure. To reduce operational complexity, the team prefers a managed service that simplifies both development and deployment of their application. Which AWS service should the team select to meet these requirements?

Correct Answers
AWS Amplify.

Rationale: AWS Amplify is a fully managed service designed to simplify the development, deployment, and hosting of full-stack web applications, including native support for Next.js with server side rendering (SSR). It is optimized for teams that want to avoid complex AWS infrastructure management.

Incorrect Answers
Selected
Amazon Elastic Kubernetes Service (Amazon EKS) with Amazon DynamoDB.

Rationale: Amazon Elastic Kubernetes Service (Amazon EKS) is a powerful managed Kubernetes platform but requires significant container, networking, and operational expertise, making it unsuitable for teams seeking simplicity.

AWS AppSync.

Rationale: AWS AppSync is a managed service for building GraphQL APIs and connecting to data sources, but it does not manage or deploy entire full-stack applications or provide SSR hosting for Next.js out of the box.

AWS Lambda with Amazon Relational Database Service (Amazon RDS).

Rationale: This is a complex architecture, especially with their limited experience. Furthermore, it does not provide any frontend capabilities. There is a simpler, managed solution.


이 문제는 **기술 깊이가 아니라 “팀 상황 + 운영 복잡도”를 읽는 판단 문제**야.
핵심은 **“무엇을 만들고 싶은가”보다 “누가, 어떤 수준으로 운영하길 원하는가”**다.

---

# 🔑 Question 18 판단기준 (Next.js SSR + 최소 운영)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제 문장을 압축하면 이렇게 된다:

* **small development team**
* **lacks in-depth AWS experience**
* **reduce operational complexity**
* **managed service**
* **full-stack web application**
* **Next.js with SSR**

👉 이 조합이 나오면, 이미 답은 **“인프라를 거의 안 만지게 해주는 서비스”**다.

---

## 2️⃣ 1차 판단 공식: “팀 역량 + 운영 선호”

### ✅ 판단 공식 (아주 중요)

> **“AWS 경험 부족 + 운영 단순화 = Amplify”**

AWS 시험에서는 이 공식이 거의 고정이다.

---

## 3️⃣ 왜 AWS Amplify가 정답인가?

### 🔍 Amplify가 이 문제에 딱 맞는 이유

* **Next.js SSR 공식 지원**
* Git 기반 CI/CD 자동화
* Frontend + Backend 통합 관리
* 인프라 구성 거의 필요 없음
* 소규모 팀 / 스타트업에 최적화

👉 이 문제의 요구사항을 그대로 매칭하면:

| 요구사항            | Amplify |
| --------------- | ------- |
| Full-stack      | ✅       |
| Next.js SSR     | ✅       |
| Managed service | ✅       |
| Low ops         | ✅       |
| AWS 경험 부족       | ✅       |

---

## 4️⃣ 오답들이 왜 전부 탈락하는지 (판단 기준)

### ❌ Amazon EKS + DynamoDB

**왜 틀렸는가?**

* EKS = Kubernetes
* Kubernetes = 운영 지옥
* 컨테이너, 네트워크, 보안, 배포 전부 직접 관리

**판단 기준**

> “EKS는 단순화가 아니라 *복잡화* 도구”

👉 **small team + low ops** 문구가 보이면 EKS는 즉시 제거

---

### ❌ AWS AppSync

**왜 틀렸는가?**

* AppSync = GraphQL API 서비스
* Frontend 배포 ❌
* SSR ❌
* Full-stack 관리 ❌

**판단 기준**

> “API 서비스는 앱 호스팅 서비스가 아니다”

---

### ❌ Lambda + RDS

**왜 틀렸는가?**

* 프런트엔드 배포 불포함
* 아키텍처 직접 설계 필요
* DB 운영, 네트워크, 보안 고려 필요

**판단 기준**

> “여러 서비스 조합이 필요하면 ‘운영 단순화’ 요구에 어긋남”

---

## 5️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 시험장에서 이렇게 처리하면 된다:

1. Next.js + SSR
2. Full-stack
3. Small team
4. Low ops
5. Managed

➡ **AWS Amplify**

그리고 동시에 제거:

* EKS
* Lambda 조합
* API 전용 서비스

---

## 6️⃣ 이 문제의 상위 메타 규칙 (다른 문제에도 그대로 적용)

> **“AWS 시험에서 ‘운영 단순화’는 항상 ‘고수준 매니지드 서비스’를 뜻한다.”**

* Amplify > EKS
* Fargate > EC2
* DynamoDB > 직접 운영 DB
* S3 + CloudFront > 직접 웹서버

👉 **팀이 작고 경험이 적을수록 서비스 수준은 높아진다**

---

## 7️⃣ 한 줄 요약

> **“Next.js SSR + 소규모 팀 + 운영 단순화 = AWS Amplify”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **Amplify vs Lambda@Edge vs S3+CloudFront 비교**
* 🔥 **‘small team / startup’ 키워드가 나올 때 자동 선택표**
* 🔥 **Next.js SSR 아키텍처 패턴 문제 모음**

중에서 바로 이어서 정리해줄게.
