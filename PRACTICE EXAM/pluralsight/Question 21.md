## Question 21
You work for a real estate company that has many different batch processes to automate, such as patch management and data synchronization. You need to automate these tasks and integrate the processes with AWS services. You also want the solution to be serverless if possible. Which AWS service should you use?

Correct Answers
Selected
AWS Step-Functions

Rationale: AWS Step Functions is a serverless orchestration service that allows you to coordinate multiple AWS services into automated workflows. It is purpose-built for automating batch and business processes in a serverless manner.

Incorrect Answers
AWS X-Ray

Rationale: AWS X-Ray is a distributed tracing and debugging service for applications. It does not automate processes or provide orchestration of batch operations.

AWS Batch Manager

Rationale: AWS Batch Manager is not an AWS service. The correct managed AWS batch processing solution is AWS Batch, which is not serverless and not named "Batch Manager."

AWS Batch Assist

Rationale: AWS Batch Assist is not a real AWS service. AWS Batch exists as a managed batch computing service, but "Assist" is not a component nor a feature, and AWS Batch is not inherently serverless.

이 문제는 **서비스 이름을 아느냐**가 아니라,
**“이 업무의 성격이 무엇인가”를 정확히 분류할 수 있느냐**를 보는 판단 문제야.

핵심은 **Batch 작업 + 자동화 + 서버리스 + AWS 서비스 연계** 이 네 가지를 동시에 만족하는지다.

---

# 🔑 Question 21 판단기준 (Batch 자동화 + Serverless)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 **결정 신호**

문제를 압축하면 이렇게 된다:

* **many different batch processes**
* **automate**
* **patch management**
* **data synchronization**
* **integrate with AWS services**
* **serverless if possible**

👉 이건 “컴퓨팅 파워” 문제가 아니라
👉 **“작업 흐름을 어떻게 묶고 자동화하느냐”** 문제다.

---

## 2️⃣ 1차 판단 분기: “실행” vs “조율(오케스트레이션)”

### 매우 중요한 구분

> **Batch 작업을 ‘실행’하는 서비스**와
> **Batch 작업을 ‘조율’하는 서비스**는 다르다.

이 문제는:

* 개별 작업 실행 ❌
* **여러 작업을 순서/조건/에러 처리까지 포함해 자동화** ⭕

👉 즉, **Orchestration 문제**다.

---

## 3️⃣ 정답으로 바로 가는 판단 공식

### ✅ 핵심 판단 공식

> **“Serverless + Batch/업무 프로세스 자동화 + AWS 서비스 연계 = Step Functions”**

이 공식은 AWS 시험에서 거의 고정이다.

---

## 4️⃣ 왜 AWS Step Functions가 정답인가?

### 🔍 Step Functions의 역할을 정확히 보면

* 서버리스 (인프라 관리 없음)
* 여러 AWS 서비스 호출 가능

  * Lambda
  * SSM
  * ECS
  * Batch
  * SNS/SQS 등
* 조건 분기, 재시도, 에러 처리, 병렬 실행 지원
* **패치 관리, 데이터 동기화 같은 배치 업무에 최적**

👉 “많은 배치 프로세스를 자동화”라는 말은
👉 **상태 머신(State Machine)** 이 필요하다는 뜻이다.

---

## 5️⃣ 오답들이 왜 즉시 탈락하는지 (판단 기준)

### ❌ AWS X-Ray

**판단 기준**

> “X-Ray = 관측/추적, 자동화 아님”

* 디버깅 도구
* 워크플로우 실행 ❌
* 배치 조율 ❌

👉 **관측(Observability) 서비스는 자동화 문제에서 항상 탈락**

---

### ❌ AWS Batch Manager / Batch Assist

**판단 기준**

> “존재하지 않는 서비스 이름은 시험 미끼”

* AWS Batch는 있음
* Batch Manager / Assist ❌

👉 **시험에서 ‘그럴듯한 이름’은 거의 항상 함정**

---

### (보너스) 만약 AWS Batch가 선택지에 있었다면?

**왜 그래도 Step Functions가 더 적합한가**

* AWS Batch:

  * 대규모 컴퓨팅 작업 실행용
  * 서버리스 ❌ (컴퓨팅 리소스 관리 필요)
* Step Functions:

  * 배치 작업 “조율”
  * 서버리스 ⭕

👉 **Patch / Sync 같은 운영 배치는 Batch보다 Step Functions**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 시험장에서 이렇게 처리하면 된다:

1. Batch 작업
2. 자동화
3. 여러 AWS 서비스 연계
4. Serverless 선호

➡ **AWS Step Functions**

그리고 즉시 제거:

* X-Ray (추적)
* 존재 안 하는 서비스
* “컴퓨팅 실행” 위주 서비스

---

## 7️⃣ 이 문제의 상위 메타 규칙 (아주 중요)

> **“AWS 시험에서 ‘자동화’는 거의 항상 ‘오케스트레이션’을 의미한다.”**

* Orchestration → Step Functions
* Execution → Lambda / Batch
* Observation → CloudWatch / X-Ray

👉 **자동화 = 순서 + 조건 + 상태**

---

## 8️⃣ 한 줄 요약

> **“서버리스로 배치 프로세스를 자동화하고 AWS 서비스를 묶고 싶다 = Step Functions”**

이 문장이 자동으로 떠오르면,
이 문제는 **0.5초 컷**이다.

---

원하면 다음으로:

* 🔥 **Step Functions vs Batch vs Lambda 비교**
* 🔥 **‘자동화’ 키워드 문제 전용 판단표**
* 🔥 **패치 관리/운영 자동화 문제 모음**

중에서 이어서 정리해줄게.
