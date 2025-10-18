# RDS Read Replicas vs Multi AZ  
# RDS 리드 리플리카 vs 멀티 AZ  

---

## Introduction to RDS Read Replicas and Multi AZ  
## RDS 리드 리플리카와 멀티 AZ 소개  

Understanding the difference between RDS Read Replicas and Multi AZ is extremely important for the exam.  
RDS 리드 리플리카와 멀티 AZ의 차이를 이해하는 것은 시험에서 매우 중요합니다.  
(중요성 강조)

This lecture is dedicated to explaining Read Replicas and Multi AZ, their use cases, and how they function.  
이번 강의에서는 리드 리플리카와 멀티 AZ, 사용 사례 및 동작 방식을 설명합니다.  
(강의 목표)

---

## RDS Read Replicas  
## RDS 리드 리플리카  

Read Replicas, as the name indicates, help you scale your read operations.  
리드 리플리카는 이름에서 알 수 있듯이 읽기 작업을 확장하는 데 도움을 줍니다.  
(기능 설명)

Consider an application connected to an RDS database instance that performs both reads and writes.  
읽기와 쓰기를 모두 수행하는 RDS 데이터베이스 인스턴스에 연결된 애플리케이션을 생각해보세요.  
(시나리오 설정)

When the main database instance cannot handle the volume of read requests, you can create up to 15 Read Replicas.  
주 데이터베이스 인스턴스가 읽기 요청을 감당할 수 없을 때, 최대 15개의 리드 리플리카를 생성할 수 있습니다.  
(한도 안내)

These replicas can be located within the same availability zone, across availability zones, or even across regions.  
리플리카는 동일 가용 영역, 다른 가용 영역 또는 다른 리전에도 위치할 수 있습니다.  
(배치 옵션)

These three deployment options are important to remember.  
이 세 가지 배치 옵션은 반드시 기억해야 합니다.  
(시험 대비)

The replication between the main RDS database instance and the Read Replicas is asynchronous.  
주 데이터베이스와 리드 리플리카 간의 복제는 비동기 방식입니다.  
(동작 방식)

This means the reads are eventually consistent.  
즉, 읽기 결과는 최종적으로 일관성을 갖게 됩니다.  
(설명)

For example, if your application reads from a Read Replica before it has had the chance to replicate the latest data, you may not get all the data immediately.  
예를 들어, 최신 데이터가 복제되기 전에 리드 리플리카에서 읽으면 모든 데이터를 즉시 얻지 못할 수 있습니다.  
(예시)

This is why it is called eventually consistent asynchronous replication.  
이 때문에 이를 최종 일관성을 가진 비동기 복제라고 부릅니다.  
(용어 정리)

Read Replicas are excellent for scaling read operations.  
리드 리플리카는 읽기 작업 확장에 매우 적합합니다.  
(장점)

Additionally, they can be promoted to become their own independent database.  
또한, 리플리카는 독립적인 데이터베이스로 승격될 수 있습니다.  
(기능)

Once promoted, the replica is no longer part of the replication mechanism and has its own lifecycle.  
승격되면 더 이상 복제 메커니즘에 속하지 않고 자체 수명을 갖습니다.  
(승격 의미)

When using Read Replicas, the main application must update its connection string to leverage the list of all Read Replicas available in the RDS cluster.  
리드 리플리카를 사용할 때는 메인 애플리케이션이 RDS 클러스터 내 모든 리드 리플리카 목록을 활용하도록 연결 문자열을 업데이트해야 합니다.  
(실무 팁)

---

## Use Case for Read Replicas  
## 리드 리플리카 사용 사례  

Consider a production database handling normal load with both reads and writes.  
읽기와 쓰기를 모두 처리하는 프로덕션 데이터베이스를 생각해보세요.  
(시나리오)

If a new team wants to run reporting and analytics on the data, connecting their reporting application directly to the main database instance could overload it and slow down the production application.  
새 팀이 데이터 분석 및 리포팅을 실행하려고 할 때, 리포팅 애플리케이션을 직접 메인 DB에 연결하면 과부하가 발생하고 프로덕션 애플리케이션이 느려질 수 있습니다.  
(문제 상황)

Instead, a Read Replica is created to handle the new workload.  
대신, 새로운 작업을 처리하기 위해 리드 리플리카를 생성합니다.  
(해결책)

The reporting application reads from the Read Replica, keeping the production application unaffected.  
리포팅 애플리케이션은 리드 리플리카에서 읽고, 프로덕션 애플리케이션에는 영향을 주지 않습니다.  
(장점)

It is important to ensure that Read Replicas are used only for SELECT statements, which are read operations.  
리드 리플리카는 SELECT 구문, 즉 읽기 작업에만 사용해야 합니다.  
(제약)

Keywords such as INSERT, UPDATE, or DELETE, which modify the database, cannot be executed on Read Replicas.  
INSERT, UPDATE, DELETE 같은 데이터베이스를 수정하는 키워드는 리드 리플리카에서 실행할 수 없습니다.  
(제약)

---

## Networking Costs Associated with Read Replicas  
## 리드 리플리카 관련 네트워크 비용  

In AWS, data transfer between availability zones usually incurs a cost.  
AWS에서는 가용 영역 간 데이터 전송에 일반적으로 비용이 발생합니다.  
(기본 규칙)

However, there are exceptions for managed services like RDS.  
하지만 RDS 같은 관리형 서비스는 예외가 있습니다.  
(예외 안내)

If your Read Replica is in a different availability zone but within the same region, you do not pay for the replication traffic.  
리드 리플리카가 동일 리전 내 다른 가용 영역에 있으면 복제 트래픽 비용이 발생하지 않습니다.  
(예시)

For example, replication traffic between us-east-1a and us-east-1b is free because RDS is a managed service.  
예를 들어, us-east-1a와 us-east-1b 간 복제 트래픽은 무료입니다.  
(구체적 사례)

However, if you use a cross-region Read Replica, such as between us-east-1 and eu-west-1, the replication traffic will incur network fees.  
하지만 리전을 넘는 리드 리플리카(us-east-1 → eu-west-1)를 사용하면 네트워크 비용이 발생합니다.  
(주의 사항)

---

## RDS Multi AZ  
## RDS 멀티 AZ  

Multi AZ is primarily used for disaster recovery.  
멀티 AZ는 주로 재해 복구에 사용됩니다.  
(목적)

The application performs reads and writes to a Master database instance located in availability zone A.  
애플리케이션은 가용 영역 A의 마스터 DB 인스턴스에 읽기/쓰기를 수행합니다.  
(설정)

There is synchronous replication to a standby instance in availability zone B.  
가용 영역 B의 스탠바이 인스턴스로 동기 복제가 수행됩니다.  
(동작 방식)

Every change made to the Master is synchronously replicated to the standby instance.  
마스터에서 이루어진 모든 변경 사항이 스탠바이 인스턴스로 동기 복제됩니다.  
(동기화)

This means that when the application writes to the Master, the change must also be replicated to the standby before it is accepted.  
즉, 애플리케이션이 마스터에 쓰기를 수행할 때, 변경 사항이 스탠바이에 복제되어야 승인됩니다.  
(제약)

The setup provides a single DNS name for the database.  
이 설정은 데이터베이스에 단일 DNS 이름을 제공합니다.  
(접근 방식)

The application connects to this DNS name, and in case of a failure with the Master, there is an automatic failover to the standby database.  
애플리케이션은 DNS 이름에 연결하며, 마스터 장애 시 스탠바이 DB로 자동 장애 조치(failover)가 발생합니다.  
(장점)

This increases availability and is the reason it is called Multi AZ.  
이는 가용성을 높이며, 이를 멀티 AZ라고 부르는 이유입니다.  
(이유 설명)

Failover can occur if an entire availability zone is lost, or if there is a network, instance, or storage failure on the Master database.  
전체 가용 영역이 손실되거나 마스터 DB에서 네트워크/인스턴스/스토리지 장애가 발생하면 장애 조치가 수행됩니다.  
(조건)

The standby database becomes the new Master without requiring manual intervention in the application, as long as the application retries the connection.  
애플리케이션이 연결을 재시도하면, 스탠바이 DB가 새로운 마스터가 되며 수동 개입이 필요 없습니다.  
(자동 전환)

Multi AZ is not used for scaling.  
멀티 AZ는 스케일링 용도가 아닙니다.  
(목적 구분)

The standby database is only for failover purposes; it cannot be read from or written to during normal operation.  
스탠바이 DB는 장애 조치 전용이며, 정상 운영 중에는 읽기/쓰기가 불가능합니다.  
(제약)

---

## Combining Read Replicas and Multi AZ  
## 리드 리플리카와 멀티 AZ 결합  

It is possible to configure Read Replicas as Multi AZ for disaster recovery.  
리드 리플리카를 멀티 AZ로 구성하여 재해 복구를 할 수 있습니다.  
(설정 가능)

This is a common exam question.  
이는 시험에서 자주 나오는 질문입니다.  
(시험 대비)

---

## Transitioning from Single AZ to Multi AZ  
## 싱글 AZ → 멀티 AZ 전환  

A common exam question is how to convert an RDS database from Single AZ to Multi AZ.  
싱글 AZ RDS를 멀티 AZ로 전환하는 방법은 시험에서 흔히 출제됩니다.  
(시험 대비)

This operation is zero downtime, meaning you do not need to stop the database.  
이 작업은 무중단(Zero Downtime)이며, 데이터베이스를 중지할 필요가 없습니다.  
(편리함)

You simply modify the database instance and enable Multi AZ.  
데이터베이스 인스턴스를 수정하고 멀티 AZ를 활성화하면 됩니다.  
(간단한 절차)

Behind the scenes, RDS takes a snapshot of the main database and restores it into a new standby database.  
RDS는 내부적으로 마스터 DB 스냅샷을 찍고
```


새 스탠바이 DB로 복원합니다.
(작업 과정)

Once restored, synchronization is established between the Master and standby databases.
복원 후, 마스터와 스탠바이 DB 간 동기화가 이루어집니다.
(완료 과정)

The standby catches up to the Master, completing the Multi AZ setup.
스탠바이가 마스터와 동기화되면 멀티 AZ 설정이 완료됩니다.
(완료)

---

## Conclusion

## 결론

This concludes the lecture on the differences between RDS Read Replicas and Multi AZ.
이로써 RDS 리드 리플리카와 멀티 AZ의 차이 강의를 마칩니다.
(강의 종료)

Understanding these concepts is essential for the exam, as many questions will focus on them.
이 개념들을 이해하는 것은 시험에서 매우 중요하며, 많은 문제가 관련됩니다.
(시험 대비)

---

## Key Takeaways

## 핵심 요약

* RDS Read Replicas are used to scale read operations and support asynchronous replication.

* RDS 리드 리플리카는 읽기 작업을 확장하고 비동기 복제를 지원합니다.

* Multi AZ deployments provide synchronous replication for high availability and disaster recovery.

* 멀티 AZ 배포는 고가용성과 재해 복구를 위해 동기 복제를 제공합니다.

* Read Replicas can be promoted to standalone databases and can be configured as Multi AZ.

* 리드 리플리카는 독립 데이터베이스로 승격할 수 있으며, 멀티 AZ로 구성할 수도 있습니다.

* Transitioning from Single AZ to Multi AZ is a zero downtime operation involving snapshot and standby creation.

* 싱글 AZ에서 멀티 AZ로 전환하는 작업은 무중단이며, 스냅샷과 스탠바이 DB 생성이 포함됩니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+250XP**  
- 아이템: **"RDS 재해복구 열쇠" (+15% 가용성 증가)**  
- 업적 달성: **"RDS 확장 전략 마스터"** 🏆  

이 자료를 숙지하면 **읽기 확장, 장애 복구, 멀티 AZ 설정** 이해도를 높여 시험과 실무 모두에 도움이 됩니다.
