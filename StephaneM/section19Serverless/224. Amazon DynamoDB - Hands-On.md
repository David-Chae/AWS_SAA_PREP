# Amazon DynamoDB - Hands-On
# Amazon DynamoDB 실습
> DynamoDB 실습 안내. 서버리스 NoSQL 데이터베이스를 직접 경험합니다.

## Introduction to DynamoDB
## DynamoDB 소개
> DynamoDB를 처음 살펴봅니다. 아키텍처와 특징을 이해하는 것이 목표입니다.

Let's have a first look at DynamoDB. DynamoDB allows us to create tables directly without creating a separate database. This design makes DynamoDB a serverless database.
DynamoDB를 처음 살펴봅시다. DynamoDB는 별도의 데이터베이스를 생성하지 않고 테이블을 바로 만들 수 있습니다. 이런 설계 때문에 DynamoDB는 서버리스 데이터베이스로 분류됩니다.
> 핵심: 서버리스 특성 때문에 인프라 관리 필요 없음.

## Creating a Table
## 테이블 생성
> 테이블 생성 방법과 기본 키 선택 방법을 다룹니다.

To create a table, you simply click on "Create Table." There is no concept of creating a database first. You must create a table immediately. For example, the table name can be DemoTable.
테이블을 생성하려면 "Create Table"을 클릭하면 됩니다. 데이터베이스를 먼저 생성하는 개념은 없습니다. 바로 테이블을 만들어야 합니다. 예를 들어 테이블 이름은 `DemoTable`로 할 수 있습니다.
> 핵심: DynamoDB는 테이블 단위로 바로 시작.

When creating a table, you must choose a partition key and optionally a sort key. The combination of these two columns forms your primary key. To keep it simple, you can have userID as the partition key and no sort key.
테이블 생성 시 파티션 키를 선택해야 하고, 필요 시 정렬 키도 선택할 수 있습니다. 이 두 컬럼의 조합이 기본 키를 형성합니다. 간단히 하려면 `userID`를 파티션 키로 하고 정렬 키는 생략할 수 있습니다.
> 핵심: 파티션 키 + 정렬 키 = 기본 키

## Read and Write Capacity Settings
## 읽기 및 쓰기 용량 설정
> 용량 모드 선택과 시험 대비 포인트를 다룹니다.

This is an important aspect, especially from an exam perspective. You can customize the settings for read and write capacity with two options: on-demand or provisioned.
이 부분은 특히 시험 관점에서 중요합니다. 읽기/쓰기 용량을 두 가지 옵션으로 설정할 수 있습니다: 온디맨드(On-Demand) 또는 프로비저닝(Provisioned).
> 핵심: 시험에서 자주 출제되는 개념

### On-Demand Capacity
### 온디맨드 용량
On-demand capacity means you pay for the actual reads and writes your application performs. This is ideal for applications with unpredictable workloads. However, on-demand capacity is two to three times more expensive than provisioned capacity, so use it wisely.
온디맨드 용량은 실제 애플리케이션이 수행하는 읽기/쓰기에 대해서만 요금을 지불하는 방식입니다. 예측 불가능한 워크로드에 적합합니다. 하지만 프로비저닝 용량보다 2~3배 더 비싸므로 신중히 사용해야 합니다.
> 핵심: 유연하지만 비용 높음

### Provisioned Capacity
### 프로비저닝 용량
Provisioned capacity allows you to manage and optimize costs by allocating read and write capacity in advance. You specify read capacity units (RCUs) and write capacity units (WCUs). For example, you can provision 10 RCUs and 5 WCUs.
프로비저닝 용량은 읽기/쓰기 용량을 미리 할당하여 비용을 관리하고 최적화할 수 있습니다. 읽기 용량 단위(RCU)와 쓰기 용량 단위(WCU)를 지정합니다. 예: 10 RCU와 5 WCU를 설정.
> 핵심: 비용 최적화 가능, 워크로드 예측 필요

You can also enable auto-scaling for read and write capacities. If auto-scaling is off, you manually set the capacity units. If on, you specify minimum and maximum capacity units and a target utilization percentage (e.g., min 1, max 100, target utilization 70%). Auto-scaling then adjusts capacity to maintain the target utilization.
읽기/쓰기 용량에 대한 자동 스케일링도 활성화할 수 있습니다. 꺼져 있으면 용량 단위를 수동으로 설정해야 하고, 켜져 있으면 최소/최대 용량과 목표 사용률(예: 최소 1, 최대 100, 목표 사용률 70%)을 지정합니다. 자동 스케일링이 목표 사용률을 유지하도록 용량을 조정합니다.
> 핵심: 자동 스케일링 이해는 시험과 실무 모두 중요

For this demonstration, auto-scaling is turned off, and both read and write capacities are set to one unit each. These options are crucial to understand for the exam.
이 데모에서는 자동 스케일링을 끄고, 읽기/쓰기 용량을 각각 1단위로 설정했습니다. 시험 대비를 위해 이 옵션들을 이해하는 것이 중요합니다.
> 핵심: 기본 용량 설정 방법 이해

## Indexes
## 인덱스
Indexes are an important feature but will be discussed in the next lecture. For now, we will skip them.
인덱스는 중요한 기능이지만 다음 강의에서 다룹니다. 현재는 생략합니다.
> 핵심: 다음 강의 내용

## Capacity Calculator
## 용량 계산기
To determine the appropriate read and write capacity for your application, there is a capacity calculator available. This is more relevant for the developer exam and will not be covered here.
애플리케이션에 적합한 읽기/쓰기 용량을 결정하려면 용량 계산기를 사용할 수 있습니다. 개발자 시험과 관련 있으며 여기서는 다루지 않습니다.
> 핵심: 시험용 참고 자료

## Pricing Information
## 가격 정보
With one read capacity unit and one write capacity unit, the estimated cost for this table is approximately 71 cents per month. This gives insight into DynamoDB pricing.
읽기 1단위, 쓰기 1단위 기준으로, 이 테이블의 예상 비용은 월 약 $0.71입니다. DynamoDB 가격 구조를 이해하는 데 도움됩니다.
> 핵심: 비용 감각 익히기

## Encryption
## 암호화
Encryption at rest is enabled before creating the table to ensure data security.
데이터 보안을 위해 테이블 생성 전에 저장 시 암호화를 활성화합니다.
> 핵심: 데이터 보호

## Inserting Items into the Table
## 테이블에 항목 삽입
Once the table is created, you can view and insert items. For example, create an item with userID as stephane_123 and add attributes such as name with value "Stephane Maarek", favorite movie as "Memento", and favorite number as 42.
테이블 생성 후, 항목을 보고 삽입할 수 있습니다. 예: `userID = stephane_123`로 항목을 만들고, `name = "Stephane Maarek"`, `favorite movie = "Memento"`, `favorite number = 42`를 속성으로 추가합니다.
> 핵심: 항목 삽입 방법 이해

Similarly, you can create another item with userID as alice_456, name as "Alice Doe", favorite movie as "Pocahontas", and add an age attribute with value 23.
유사하게 `userID = alice_456` 항목을 만들고, `name = "Alice Doe"`, `favorite movie = "Pocahontas"`, `age = 23` 속성을 추가할 수 있습니다.
> 핵심: 여러 항목 삽입 가능

## Flexible Attributes
## 유연한 속성
In DynamoDB, items do not need to have the same attributes. Each item can have different attributes, which demonstrates the power of DynamoDB as a NoSQL database compared to traditional SQL databases.
DynamoDB에서는 항목마다 동일한 속성을 가질 필요가 없습니다. 각 항목이 서로 다른 속성을 가질 수 있으며, 이는 전통적 SQL 대비 NoSQL의 유연성을 보여줍니다.
> 핵심: NoSQL 특징 강조

## Summary
## 요약
Now, the table contains items for Alice and Stephane. There are many options available in DynamoDB, which will be explored in the next lecture. The key points covered here include setting read and write capacity units or using on-demand mode, and inserting data into the DynamoDB table.
현재 테이블에는 Alice와 Stephane의 항목이 있습니다. DynamoDB에는 많은 옵션이 있으며, 다음 강의에서 더 탐구할 예정입니다. 여기서 다룬 핵심 포인트는 읽기/쓰기 용량 설정, 온디맨드 모드 사용, 테이블에 데이터 삽입입니다.
> 핵심: 실습 요약

I hope you found this introduction helpful. See you in the next lecture.
이 소개가 도움이 되었기를 바랍니다. 다음 강의에서 만나요.
> 핵심: 마무리 인사

## Key Takeaways
## 핵심 요약
DynamoDB tables are created without a separate database layer, emphasizing its serverless nature.
DynamoDB 테이블은 별도 데이터베이스 없이 생성되며, 서버리스 특성을 강조합니다.
Primary keys in DynamoDB consist of a partition key and an optional sort key.
DynamoDB의 기본 키는 파티션 키와 선택적 정렬 키로 구성됩니다.
Read and write capacity can be configured as on-demand or provisioned, with auto-scaling options available.
읽기/쓰기 용량은 온디맨드 또는 프로비저닝으로 설정할 수 있으며, 자동 스케일링 옵션도 사용 가능합니다.
DynamoDB allows flexible item attributes, enabling different items to have different sets of attributes.
DynamoDB는 항목마다 서로 다른 속성을 가질 수 있는 유연성을 제공합니다.

```


🎮 **게임 보상 포인트:**

* DynamoDB 서버리스 특성 이해 + 기본 키 구성 = 10 XP
* 읽기/쓰기 용량 모드 이해 = 15 XP
* 항목 삽입과 유연한 속성 이해 = 20 XP

총: **45 XP**
