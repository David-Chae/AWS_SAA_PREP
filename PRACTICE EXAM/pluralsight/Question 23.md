Question 23
Your company is building out a second AWS Region. To follow best practices, it has used AWS CloudFormation to simplify the migration. However, when running the CloudFormation template in the new region, the template continues to reference the Amazon Machine Image (AMI) from the original region. What is the best solution to have the correct AMI automatically selected whenever the template is deployed in a new region?

Correct Answers
Create a mapping in the template. Define the unique AMI value per region.

Rationale: Using the Mappings section in the template, you can map each AWS Region to its specific AMI ID. When the template is deployed, the correct AMI for the target region is selected automatically using !FindInMap with AWS::Region.

Incorrect Answers
Selected
Create a condition in the template to automatically select the correct AMI ID.

Rationale: Conditions in CloudFormation control resource creation or configuration, not dynamic value lookup by region. They are not used to select region-specific AMIs automatically.

Create a Parameter section in the template. Whenever the template is run, fill in the correct AMI ID.

Rationale: Parameters require manual entry or automated injection at stack launch, increasing the risk of errors and reducing automation. This does not achieve fully automated regional selection.

Update the AMI in the old region, as AMIs are universal.

Rationale: AMIs are region-specific resources. An AMI in one region cannot be referenced in another region using the same ID. AMIs must be copied between regions as needed.

이건 **CloudFormation의 “값 선택 책임이 어디에 있느냐”**를 정확히 구분하는 문제다.
아래 판단기준만 잡히면, 같은 유형은 다시 틀릴 일이 없다.

---

# 🔑 Question 23 판단기준 (CloudFormation + Region별 AMI)

## 1️⃣ 문제에서 가장 먼저 잡아야 할 핵심 신호

문제에 이미 답의 범위가 명확히 들어 있다:

* **second AWS Region**
* **CloudFormation**
* **AMI가 기존 Region을 참조**
* **자동으로(correct AMI automatically selected)**
* **best practices**

👉 이건 “AMI를 바꾸는 방법” 문제가 아니라
👉 **“Region이 바뀌면 CloudFormation이 스스로 다른 값을 선택해야 하는 상황”**이다.

---

## 2️⃣ CloudFormation에서 값이 결정되는 3가지 도구의 역할 구분

이 문제를 풀려면, CloudFormation 구성 요소의 **역할 차이**를 정확히 알아야 한다.

### 🔹 Parameters

* 사람이 **입력**하거나 외부에서 주입
* 값이 실행 시마다 달라질 수 있음
* ❌ 자동 선택 아님

👉 **자동화·베스트 프랙티스 요구가 있으면 탈락**

---

### 🔹 Conditions

* 리소스를 **만들지 / 말지** 결정
* if/else처럼 **존재 여부 제어**
* ❌ 값 lookup 용도 아님

👉 **“값을 고른다”는 요구와 역할 불일치**

---

### 🔹 Mappings

* **고정된 기준 → 고정된 값** 테이블
* 대표적인 기준: Region, AZ, 환경(dev/prod)
* CloudFormation이 **스스로 조회**

👉 **Region별 AMI 선택에 정확히 맞는 도구**

---

## 3️⃣ 정답으로 가는 핵심 판단 공식

### ✅ 이 문제의 핵심 공식

> **“Region마다 값이 다르고, 자동으로 선택돼야 한다 = Mappings”**

이 공식 하나면 끝이다.

---

## 4️⃣ 왜 Mappings가 정답인가?

### 🔍 AMI의 본질적 특성

* AMI는 **Region 종속**
* 같은 OS라도 Region마다 **AMI ID 다름**
* 배포 시점에 **현재 Region**을 기준으로 선택해야 함

### 🔍 Mappings의 동작 방식

1. Region → AMI ID 매핑 테이블 정의
2. `AWS::Region` pseudo parameter로 현재 Region 감지
3. `!FindInMap`으로 해당 Region의 AMI 선택

👉 **사람 개입 없음 + 자동 + 확장 가능**

---

## 5️⃣ 오답들이 왜 틀렸는지 (판단기준으로 제거)

### ❌ Condition 사용

**판단기준**

> “Condition은 ‘값 선택’이 아니라 ‘존재 제어’다”

* Region이 늘어날수록 조건 폭증
* 구조적으로 잘못된 접근

---

### ❌ Parameter 사용

**판단기준**

> “Parameter = 수동 또는 외부 입력”

* 자동 선택 아님
* 실수 가능성 증가
* best practice 위배

---

### ❌ AMI는 universal

**판단기준**

> “AMI는 Region마다 ID가 다르다”

* 사실 자체가 틀린 선택지
* 시험에서 자주 나오는 **개념 오류 미끼**

---

## 6️⃣ 시험장에서 바로 쓰는 초압축 판단 카드

이 문제를 보면 머릿속에서 이렇게 자동으로 떠야 한다:

1. CloudFormation
2. Region별로 값 다름
3. 자동 선택 필요

➡ **Mappings**

그리고 동시에 제거:

* Parameter
* Condition
* “AMI는 공통”

---

## 7️⃣ 상위 메타 규칙 (다른 문제에도 그대로 적용)

> **“CloudFormation에서 환경/Region에 따라 값이 달라지면, 거의 항상 Mappings다.”**

* AMI
* Instance type
* Region별 리소스 ID
* 환경별 설정 값

---

## 8️⃣ 한 줄 요약

> **“CloudFormation에서 Region별 AMI 자동 선택 = Mappings + AWS::Region”**

이 문장이 자동으로 떠오르면,
이 문제는 **생각할 필요 없이 정답 확정**이다.

---

원하면 다음으로:

* 🔥 **Mappings vs Parameters vs Conditions 함정 비교**
* 🔥 **CloudFormation 시험 단골 판단 공식 10개**
* 🔥 **AMI/Region 관련 오답 패턴 모음**

중에서 바로 이어서 정리해줄게.
