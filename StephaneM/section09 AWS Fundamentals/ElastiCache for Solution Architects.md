# ElastiCache for Solution Architects  
# 솔루션 아키텍트를 위한 ElastiCache  

---

## ElastiCache Security Overview  
## ElastiCache 보안 개요  

ElastiCache supports IAM authentication for Redis only.  
ElastiCache는 Redis에 대해서만 IAM 인증을 지원합니다.  
(Redis 전용 IAM 인증)  

For other engines, authentication is handled via username and password.  
다른 엔진의 경우, 인증은 사용자 이름과 비밀번호로 처리됩니다.  
(다른 엔진 인증 방식)  

IAM policies on ElastiCache are used exclusively for AWS API-level security.  
ElastiCache에서 IAM 정책은 AWS API 수준 보안을 위해서만 사용됩니다.  
(IAM 정책 용도)  

Within Redis, there is a security feature called Redis AUTH, where you can set a password and a token when creating a Redis cluster.  
Redis에는 Redis AUTH라는 보안 기능이 있어, 클러스터 생성 시 비밀번호와 토큰을 설정할 수 있습니다.  
(Redis AUTH 설명)  

This provides an additional level of security for your cache on top of your security groups.  
이는 보안 그룹 위에 추가적인 캐시 보안을 제공합니다.  
(보안 강화)  

ElastiCache also supports SSL in-flight encryption to secure data transmission.  
ElastiCache는 SSL 전송 중 암호화를 지원하여 데이터 전송을 보호합니다.  
(전송 암호화)  

Memcached supports SASL-based authentication, which is a more advanced mechanism.  
Memcached는 보다 고급 인증 방식인 SASL 기반 인증을 지원합니다.  
(Memcached 인증)  

Remember, this is just a name for the authentication method used.  
기억하세요, 이것은 단지 사용된 인증 방식의 이름입니다.  
(인증 방식 명칭)  

---

## Summary of Security Options  
## 보안 옵션 요약  

When you have an EC2 instance as a client, you can use Redis AUTH to connect to a Redis cluster protected by a Redis security group, with in-flight encryption enabled.  
클라이언트가 EC2 인스턴스인 경우, Redis 보안 그룹으로 보호된 Redis 클러스터에 Redis AUTH와 전송 암호화를 사용해 연결할 수 있습니다.  
(EC2 연결)  

Alternatively, you can leverage IAM authentication for Redis.  
또는 Redis에 대해 IAM 인증을 활용할 수도 있습니다.  
(IAM 인증 선택)  

---

## Data Loading Patterns in ElastiCache  
## ElastiCache 데이터 로딩 패턴  

There are three primary patterns for loading data into ElastiCache:  
ElastiCache에 데이터를 로딩하는 주요 패턴은 세 가지입니다.  
(데이터 로딩 전략)  

- Lazy Loading: All read data is cached, but data can become stale in the cache.  
- Lazy Loading: 모든 읽기 데이터를 캐시에 저장하지만, 데이터가 오래되어 stale이 될 수 있음.  
(Lazy Loading)  

- Write Through: Data is added or updated in the cache whenever it is written to the database, ensuring no stale data.  
- Write Through: 데이터가 DB에 기록될 때마다 캐시에 추가/업데이트되어 stale 데이터가 없음.  
(Write Through)  

- Session Store: Using ElastiCache as a session store, where sessions can expire using the time-to-live (TTL) feature.  
- Session Store: ElastiCache를 세션 저장소로 사용, TTL 기능으로 세션 만료 가능.  
(Session Store)  

Caching is a complex topic.  
캐싱은 복잡한 주제입니다.  
(캐싱 주제)  

There is a famous quote in computer science: "There are only two hard things in computer science: caching invalidation and naming things."  
컴퓨터 과학의 유명한 말이 있습니다: "컴퓨터 과학에서 어려운 것은 단 두 가지, 캐시 무효화와 이름 짓기이다."  
(캐싱 어려움)  

This highlights the challenges involved in caching strategies.  
이는 캐싱 전략의 어려움을 강조합니다.  
(전략 어려움)  

---

## Lazy Loading Strategy Illustration  
## Lazy Loading 전략 예시  

In the lazy loading strategy, your application first attempts to retrieve data from the ElastiCache cache.  
Lazy Loading 전략에서 애플리케이션은 먼저 ElastiCache 캐시에서 데이터를 조회합니다.  
(Lazy Loading 시작)  

If there is a cache hit, the data is returned directly.  
캐시 히트가 발생하면 데이터가 바로 반환됩니다.  
(캐시 히트)  

If there is a cache miss, the application reads from the database and then writes the data to the cache.  
캐시 미스 발생 시, 애플리케이션이 DB에서 읽고 캐시에 기록합니다.  
(캐시 미스)  

This approach loads data into ElastiCache only when it is not already cached.  
이 접근법은 캐시에 없을 때만 데이터를 로드합니다.  
(데이터 로딩 방식)  

---

## Redis Use Case: Gaming Leaderboard  
## Redis 사용 사례: 게임 리더보드  

A key use case for Redis, which is important for the exam, is creating a gaming leaderboard.  
Redis의 중요한 사용 사례는 게임 리더보드 생성입니다.  
(사용 사례)  

This is a complex scenario where you want to determine who is number one, number two, and number three at any moment in time for your game.  
게임에서 현재 1위, 2위, 3위를 실시간으로 확인하고 싶을 때 사용됩니다.  
(실시간 순위)  

Redis provides a feature called Sorted Sets, which guarantees both uniqueness and element ordering.  
Redis는 Sorted Sets라는 기능을 제공하며, 요소의 고유성과 순서를 보장합니다.  
(Sorted Sets)  

Each time an element is added, it is ranked in real time and inserted in the correct order.  
요소가 추가될 때마다 실시간으로 순위가 매겨지고 올바른 위치에 삽입됩니다.  
(실시간 순위 업데이트)  

With a Redis cluster, you can create a real-time leaderboard showing the top players.  
Redis 클러스터를 통해 상위 플레이어를 실시간으로 표시하는 리더보드를 생성할 수 있습니다.  
(리더보드 구현)  

The Redis cache maintains the leaderboard, allowing clients to access it directly through Amazon ElastiCache using Redis.  
Redis 캐시가 리더보드를 유지하여 클라이언트가 Redis를 통해 ElastiCache에서 직접 접근할 수 있습니다.  
(리더보드 접근)  

This eliminates the need to program leaderboard functionality on the application side.  
애플리케이션 측에서 리더보드 기능을 구현할 필요가 없습니다.  
(애플리케이션 부담 감소)  

Leveraging Redis Sorted Sets provides real-time access to the leaderboard, which is a valuable feature that may appear on the exam.  
Redis Sorted Sets를 사용하면 실시간 리더보드 접근이 가능하며, 시험에서도 중요하게 다뤄질 수 있습니다.  
(시험 대비)  

---

## Conclusion  
## 결론  

This concludes the lecture on ElastiCache security and use cases.  
이로써 ElastiCache 보안과 사용 사례 강의가 종료됩니다.  
(강의 종료)  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  
(감사 인사)  

---

## Key Takeaways  
## 핵심 요약  

- ElastiCache supports IAM authentication for Redis, while other engines use username and password.  
- ElastiCache는 Redis에 대해 IAM 인증을 지원하며, 다른 엔진은 사용자 이름과 비밀번호를 사용합니다.  
- Redis provides additional security with Redis AUTH and supports SSL in-flight encryption.  
- Redis는 Redis AUTH로 추가 보안을 제공하며, SSL 전송 암호화를 지원합니다.  
- Memcached supports SASL-based authentication, an advanced mechanism.  
- Memcached는 고급 인증 방식인 SASL 기반 인증을 지원합니다.  
- Three main caching patterns are Lazy Loading, Write Through, and using ElastiCache as a session store.  
- 주요 캐싱 패턴은 Lazy Loading, Write Through, Session Store입니다.  
- Redis Sorted Sets enable real-time gaming leaderboards with unique, ordered elements.  
- Redis Sorted Sets는 고유하고 순서 있는 요소로 실시간 게임 리더보드를 구현할 수 있습니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+500XP**
* 아이템: **"Redis Security Scroll"**
* 업적 달성: **"Cache Security Expert"** 🛡️

이 MD 파일은 **ElastiCache 보안, 인증, 데이터 로딩 패턴, Redis 실시간 리더보드 사례**까지 시험과 실무에 바로 활용할 수 있도록 구성했습니다.
