# Choosing the Right Database
# 올바른 데이터베이스 선택하기
# → 이 문서는 다양한 AWS 데이터베이스 중 어떤 것을 선택해야 하는지 개요를 설명합니다.

## Introduction to Choosing the Right Database
## 올바른 데이터베이스 선택하기 소개
## → 시험이나 실무에서 워크로드에 맞는 DB를 고르는 기초 개념입니다.

In this section, we provide a quick introduction to selecting the appropriate database for your workload.  
이번 섹션에서는 워크로드에 맞는 적절한 데이터베이스를 선택하는 방법을 간단히 소개합니다.  
→ 상황별 맞춤 DB 선택의 중요성을 강조합니다.

At the exam, you will need to choose the right database from many managed options available on AWS.  
시험에서는 AWS에서 제공하는 여러 관리형 옵션 중 적절한 DB를 선택해야 합니다.  
→ 시험 문제는 서비스 특성 파악 능력을 테스트합니다.

The decision primarily depends on the architecture and requirements posed by the question.  
선택은 주로 문제에서 제시하는 아키텍처와 요구사항에 달려 있습니다.  
→ 요구사항 분석이 핵심입니다.

```
🎖️ **게임 보상: DB 선택 초급자 → DB 견습생으로 레벨업!**
```

## Key Considerations for Database Selection
## 데이터베이스 선택 시 주요 고려 사항
## → DB를 선택할 때 반드시 체크해야 할 질문 목록입니다.

When choosing a database, consider the following factors:  
데이터베이스를 선택할 때는 다음 요소들을 고려하세요.  
→ 하나씩 확인하며 최적의 DB를 좁혀갑니다.

- Is the workload write-heavy, read-heavy, or balanced?  
  워크로드가 쓰기 위주인지, 읽기 위주인지, 균형 잡혀 있는지?  
  → 트랜잭션 패턴 파악.

- Will the workload change or fluctuate during the day?  
  워크로드가 하루 중 변하거나 변동이 있는지?  
  → 트래픽 변동성 확인.

- How much data will be stored and for how long?  
  얼마나 많은 데이터를 얼마나 오랫동안 저장해야 하는지?  
  → 데이터 용량/보관 주기 파악.

- Will the data grow over time?  
  데이터가 시간이 지나면서 늘어나는지?  
  → 확장성 필요성 판단.

- What is the average object size?  
  평균 객체 크기는 얼마인지?  
  → 저장 효율과 성능에 영향.

- How often and in what manner will the data be accessed?  
  데이터가 얼마나 자주, 어떤 방식으로 접근되는지?  
  → 액세스 패턴 분석.

- What are the data durability requirements?  
  데이터 내구성 요구사항은 무엇인지?  
  → 데이터 손실 허용 여부 결정.

- What is the source of truth for your data?  
  데이터의 "최종 진실 소스"는 무엇인지?  
  → 기준 데이터 위치 명확히.

- Are there latency requirements?  
  지연 시간 요구사항이 있는지?  
  → 실시간 처리 여부 고려.

- How many concurrent users will access the database?  
  동시 접속자가 몇 명인지?  
  → 동시성 처리 성능 요구.

- What is the data model?  
  데이터 모델은 무엇인지?  
  → 관계형, 문서형, 그래프형 등 구조 확인.

- How will you query the data? Are joins needed?  
  데이터를 어떻게 쿼리할 것인지? 조인이 필요한가?  
  → SQL/NoSQL 여부 결정.

- Is the data structured or semi-structured?  
  데이터가 정형인지 반정형인지?  
  → 스키마 설계 방식 차이.

- Do you require a strong schema or more flexibility?  
  강력한 스키마가 필요한지, 유연성이 더 중요한지?  
  → RDB vs NoSQL 선택 포인트.

- Will you include reporting on top of your database?  
  DB 위에서 리포팅 기능이 필요한가?  
  → 분석/BI 연동 여부.

- Do you need search capabilities?  
  검색 기능이 필요한가?  
  → 검색엔진 결합 고려.

- Do you prefer a relational database or NoSQL?  
  관계형 DB를 선호하는가, NoSQL을 선호하는가?  
  → 설계 철학 차이.

- Are there any licensing costs?  
  라이선스 비용이 드는가?  
  → 비용 최적화 고려.

- Do you want to switch to cloud-native databases such as Aurora?  
  Aurora 같은 클라우드 네이티브 DB로 전환하고 싶은가?  
  → 최신 아키텍처 도입 여부.

```
🎖️ **게임 보상: DB 견습생 → DB 전략가로 레벨업!**
```
