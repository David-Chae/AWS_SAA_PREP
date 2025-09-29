# ElastiCache Overview  
# 엘라스티캐시 개요  

---

Let's talk about Amazon ElastiCache.  
Amazon ElastiCache에 대해 이야기해봅시다.  
(ElastiCache 소개)  

Similar to how you get RDS to have managed relational databases, ElastiCache helps you get managed Redis or Memcached, which are cache technologies.  
RDS가 관리형 관계형 데이터베이스를 제공하는 것처럼, ElastiCache는 관리형 Redis 또는 Memcached(캐시 기술)를 제공합니다.  
(관리형 캐시 서비스)  

---

## What Are Caches?  
## 캐시란 무엇인가?  

Caches are in-memory databases with really high performance and low latency.  
캐시는 메모리 기반 데이터베이스로, 매우 높은 성능과 낮은 지연 시간을 제공합니다.  
(빠른 데이터 접근)  

They help reduce the load off of databases for read-intensive workloads.  
읽기 집중 워크로드에서 DB 부하를 줄이는 데 도움을 줍니다.  
(DB 부하 완화)  

The idea is that common queries are cached, so your database is not queried every time.  
자주 사용되는 쿼리를 캐싱하여 매번 DB를 조회하지 않도록 합니다.  
(쿼리 캐싱)  

Instead, your cache can be used to retrieve the results of these queries.  
대신 캐시에서 해당 쿼리 결과를 가져올 수 있습니다.  
(캐시 조회)  

Using a cache also helps make your application stateless by putting the state of your application into Amazon ElastiCache.  
캐시를 사용하면 애플리케이션 상태를 ElastiCache에 저장하여 애플리케이션을 무상태(stateless)로 만들 수 있습니다.  
(무상태 애플리케이션)  

Because we have the same benefits for RDS, AWS takes care of maintenance of the operating system, patching, optimization, setup, configuration, monitoring, failure recovery, and backups.  
RDS와 마찬가지로 AWS가 운영체제 유지보수, 패치, 최적화, 설정, 구성, 모니터링, 장애 복구, 백업을 관리합니다.  
(관리형 서비스 이점)  

However, using Amazon ElastiCache requires some heavy application code changes.  
그러나 ElastiCache를 사용하려면 애플리케이션 코드에 상당한 변경이 필요합니다.  
(코드 변경 필요)  

This is not something you just enable and off you go with a cache.  
단순히 활성화만 하면 되는 것이 아닙니다.  
(단순 설정 불가)  

You need to change your application to query the cache before or after querying the database.  
애플리케이션이 DB 조회 전후에 캐시를 조회하도록 코드 변경이 필요합니다.  
(캐시 로직 적용)  

We will see the strategies in a minute.  
곧 전략을 살펴보겠습니다.  
(전략 안내)  

---

## ElastiCache Architecture Example  
## 엘라스티캐시 아키텍처 예시  

Let's consider an example architecture involving Amazon ElastiCache, an RDS database, and your application.  
ElastiCache, RDS, 그리고 애플리케이션을 포함한 예시 아키텍처를 살펴봅시다.  
(아키텍처 구성)  

The application will query ElastiCache to see if the query has already been made.  
애플리케이션은 쿼리가 이미 캐시에 있는지 확인하기 위해 ElastiCache를 조회합니다.  
(캐시 확인)  

If it is stored in ElastiCache, this is called a cache hit, and the application gets the answer straight from ElastiCache, saving a trip to the database.  
캐시에 있다면 cache hit이며, 애플리케이션은 캐시에서 바로 결과를 가져와 DB 조회를 생략합니다.  
(캐시 히트)  

In case of a cache miss, the application fetches the data from the database.  
캐시 미스(cache miss)인 경우 애플리케이션은 DB에서 데이터를 가져옵니다.  
(캐시 미스 처리)  

Then, for other application instances where the same query will be made, the data can be written back into the cache so that the same query next time results in a cache hit.  
그 후 동일 쿼리를 수행할 다른 인스턴스를 위해 데이터를 캐시에 다시 쓰면, 다음번에는 cache hit가 발생합니다.  
(재사용 최적화)  

This helps relieve load from your RDS database.  
이로써 RDS DB의 부하를 줄일 수 있습니다.  
(DB 부하 감소)  

Because you are storing data in the cache, there must be a cache invalidation strategy to ensure that only the most current data is used.  
캐시에 데이터를 저장하기 때문에 최신 데이터만 사용하도록 캐시 무효화 전략이 필요합니다.  
(데이터 일관성 관리)  

This is the main difficulty around using caching technologies.  
이것이 캐시 기술 사용의 주요 어려움입니다.  
(캐시 사용 난점)  

---

## Using ElastiCache for User Sessions  
## 사용자 세션을 위한 ElastiCache 사용  

Another architecture involves storing user sessions to make your application stateless.  
또 다른 아키텍처는 애플리케이션을 무상태로 만들기 위해 사용자 세션을 저장하는 것입니다.  
(세션 저장)  

When a user logs in to your application, the session data is written into Amazon ElastiCache.  
사용자가 애플리케이션에 로그인하면 세션 데이터가 ElastiCache에 저장됩니다.  
(세션 캐시)  

If the user is redirected to another instance of your application, the session can be retrieved directly from ElastiCache, so the user remains logged in without needing to log in again.  
사용자가 다른 애플리케이션 인스턴스로 이동해도, 세션을 ElastiCache에서 직접 가져와 로그인 상태를 유지합니다.  
(무상태 세션 유지)  

This approach makes your application stateless by storing session data in ElastiCache.  
이 방법은 세션 데이터를 ElastiCache에 저장하여 애플리케이션을 무상태로 만듭니다.  
(무상태 구현)  

---

## Comparing Redis and Memcached  
## Redis와 Memcached 비교  

### For Redis:  
### Redis 경우:  

- Supports multi-availability zones with auto-failover.  
- 자동 장애 조치를 지원하는 다중 가용 영역 지원.  

- Allows creation of read replicas to scale reads and provide high availability.  
- 읽기 확장과 고가용성을 위해 읽기 복제본 생성 가능.  

- Offers data durability using Append Only File (AOF) persistence.  
- AOF를 통한 데이터 내구성 제공.  

- Provides backup and restore features on the open source version.  
- 오픈소스 버전에서도 백업 및 복원 기능 제공.  

- Supports sets and sorted sets, useful for leaderboards and advanced cache features.  
- 집합(Set)과 정렬 집합(Sorted Set) 지원, 리더보드 등 고급 캐시 기능에 유용.  

I like to think of Redis as a node being replicated into another one, providing redundancy and high availability.  
Redis는 노드를 복제하여 중복성과 고가용성을 제공한다고 이해하면 됩니다.  
(노드 복제)  

Redis is evolving fast, so this is a simplification.  
Redis는 빠르게 발전하고 있으므로 단순화된 설명입니다.  
(참고)  

### For Memcached:  
### Memcached 경우:  

- Uses multiple nodes set up with data partitioning called sharding.  
- 샤딩(sharding)으로 데이터 분할된 다중 노드 사용.  

- Does not provide high availability or replication.  
- 고가용성이나 복제 기능 없음.  

- The serverless version offers backup and restore features, but the self-managed version on ElastiCache does not.  
- 서버리스 버전은 백업/복원 가능, 셀프 관리 버전은 불가.  

- Has a multi-threaded architecture, which may improve performance.  
- 멀티 스레드 아키텍처로 성능 향상 가능.  

I think of Memcached as multiple nodes next to each other, sharing the data through partitioning.  
Memcached는 여러 노드가 나란히 있어 데이터 파티셔닝으로 공유한다고 이해하면 됩니다.  
(데이터 분산)  

The exam may not ask many questions about choosing Redis versus Memcached, but it is good to know as a reference point based on the use case if it appears in the exam.  
시험에서는 Redis와 Memcached 선택에 대한 질문이 많지 않지만, 사용 사례 기반 참고 지식으로 알아두면 좋습니다.  
(시험 대비 참고)  

---

## Key Takeaways  
## 핵심 요약  

- Amazon ElastiCache provides managed Redis and Memcached caching services to reduce database load for read-intensive workloads.  
- Amazon ElastiCache는 읽기 집중 워크로드에서 DB 부하를 줄이기 위해 관리형 Redis와 Memcached 캐시 서비스를 제공합니다.  

- Caches are in-memory databases offering high performance and low latency, enabling stateless application architectures.  
- 캐시는 메모리 기반 DB로 높은 성능과 낮은 지연 시간을 제공하며, 무상태 애플리케이션 구현을 가능하게 합니다.  

- Cache hit and miss strategies optimize data retrieval, but require careful cache invalidation to maintain data consistency.  
- 캐시 히트/미스 전략은 데이터 조회를 최적화하지만, 데이터 일관성을 위해 캐시 무효화 전략이 필요합니다.  

- Redis supports multi-availability zones, replication, persistence, and advanced data structures, while Memcached offers sharding and multi-threading but lacks replication and durability features.  
- Redis는 다중 AZ, 복제, 내구성, 고급 데이터 구조를 지원하고, Memcached는 샤딩과 멀티 스레드만 제공하며 복제와 내구성 기능은 없습니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+500XP**
* 아이템: **"ElastiCache Guide Scroll"**
* 업적 달성: **"Cache Master"** 🗄️

이 MD 파일은 **ElastiCache 개요, 캐시 개념, 아키텍처, 세션 관리, Redis/Memcached 비교**까지 모든 핵심 내용을 포함하고 있어, 시험 대비와 실제 설계 참고 모두 가능합니다.
