```markdown
# Caching Strategies in AWS  
# AWS에서의 캐싱 전략  

Let's discuss caching strategies on AWS and their implications.  
AWS에서의 캐싱 전략과 그 영향에 대해 살펴봅시다.  

Consider a typical solution architecture, which may vary for your use case.  
일반적인 솔루션 아키텍처를 고려해보면, 이는 사용 사례에 따라 달라질 수 있습니다.  

We have CloudFront in front of an API Gateway, which is in front of our application logic.  
CloudFront가 API Gateway 앞에 있고, API Gateway가 애플리케이션 로직 앞에 있습니다.  

This application logic could be hosted on EC2 instances or AWS Lambda functions.  
이 애플리케이션 로직은 EC2 인스턴스나 AWS Lambda 함수에서 호스팅될 수 있습니다.  

Our application stores and accesses data from a database, and may also use an internal cache such as Redis, Memcached, or DAX.  
애플리케이션은 데이터베이스에 데이터를 저장하고 조회하며, Redis, Memcached, DAX 같은 내부 캐시도 사용할 수 있습니다.  

This setup handles dynamic routes or dynamic content.  
이 구조는 동적 라우트나 동적 콘텐츠를 처리합니다.  

Additionally, there is a static content route where clients access CloudFront, which sources data from Amazon S3.  
또한 정적 콘텐츠 경로가 있어서, 클라이언트는 CloudFront를 통해 Amazon S3에서 데이터를 가져옵니다.  

This architecture is common and well-known.  
이 아키텍처는 흔히 사용되고 잘 알려져 있습니다.  

---

## Edge Caching with CloudFront  
## CloudFront를 활용한 엣지 캐싱  

CloudFront performs caching at the edge, meaning it caches content as close as possible to users.  
CloudFront는 엣지에서 캐싱을 수행하여, 사용자와 최대한 가까운 곳에 콘텐츠를 캐시합니다.  

When caching is enabled in CloudFront and users hit the cache, they receive responses immediately, resulting in very fast performance.  
CloudFront에서 캐싱이 활성화되고 사용자가 캐시를 조회하면 즉시 응답을 받아 매우 빠른 성능을 제공합니다.  

However, since caching is at the edge, there is a possibility that backend data has changed, and the cached content may be outdated.  
하지만 캐싱이 엣지에서 이루어지므로 백엔드 데이터가 변경되었을 경우 캐시된 콘텐츠가 오래될 수 있습니다.  

To mitigate this, a Time To Live (TTL) can be configured to ensure the cache is refreshed frequently, allowing new data to be picked up from the backend.  
이를 완화하기 위해 TTL을 설정하여 캐시를 주기적으로 새로고침하고, 백엔드의 새로운 데이터를 가져오도록 할 수 있습니다.  

This creates a balance between caching at the edge and caching within the application logic.  
이 방식은 엣지 캐싱과 애플리케이션 로직 내 캐싱 간의 균형을 맞추게 합니다.  

---

## Regional Caching with API Gateway  
## API Gateway를 활용한 리전 캐싱  

API Gateway also provides caching capabilities, which do not require CloudFront to be used.  
API Gateway도 캐싱 기능을 제공하며, CloudFront와는 독립적으로 사용할 수 있습니다.  

API Gateway is a regional service, so caching here is regional.  
API Gateway는 리전 단위 서비스이므로 캐싱도 리전 기반입니다.  

This means there is network latency between clients and the API Gateway.  
즉, 클라이언트와 API Gateway 사이에는 네트워크 지연이 발생할 수 있습니다.  

If the cache is hit at the API Gateway, the response is served from the cache, reducing load on the backend.  
API Gateway에서 캐시가 적중되면 응답이 캐시에서 제공되어 백엔드의 부하가 줄어듭니다.  

This caching layer sits between the clients and the application logic, improving performance by reducing repeated calls to the backend services.  
이 캐싱 계층은 클라이언트와 애플리케이션 로직 사이에 위치하여 백엔드 서비스로의 반복 호출을 줄여 성능을 향상시킵니다.  

---

## Application-Level Caching  
## 애플리케이션 레벨 캐싱  

Typically, application logic itself does not perform caching, but it can utilize external caches such as Redis, Memcached, or DAX (for DynamoDB).  
일반적으로 애플리케이션 로직 자체는 캐싱을 수행하지 않지만, Redis, Memcached, DAX 같은 외부 캐시를 활용할 수 있습니다.  

The purpose of this caching is to avoid repeatedly hitting the database, which generally lacks caching capabilities.  
이 캐싱의 목적은 캐싱 기능이 없는 데이터베이스에 반복적으로 접근하는 것을 피하는 것입니다.  

By storing frequent or complex query results in a shared cache accessible by the application logic, we reduce pressure on the database and augment read capacity.  
자주 쓰이는 쿼리 결과나 복잡한 쿼리 결과를 공유 캐시에 저장하면 데이터베이스 부하를 줄이고 읽기 용량을 확장할 수 있습니다.  

This improves overall application performance and scalability.  
이는 애플리케이션 전체 성능과 확장성을 개선합니다.  

---

## Considerations and Trade-offs  
## 고려사항과 트레이드오프  

It is important to note that Amazon S3 and many databases do not have built-in caching capabilities.  
Amazon S3와 많은 데이터베이스는 자체 캐싱 기능을 제공하지 않는다는 점에 유의해야 합니다.  

As we move along the caching layers—from edge caching to application-level caching—the computational cost and latency generally increase.  
캐싱 계층이 엣지 → 리전 → 애플리케이션으로 내려갈수록 연산 비용과 지연 시간이 증가하는 경향이 있습니다.  

There is no single correct way to implement caching; it depends on your application's goals and architecture.  
캐싱을 구현하는 정답은 없으며, 애플리케이션의 목표와 아키텍처에 따라 달라집니다.  

Key decisions include:  
중요한 결정 사항은 다음과 같습니다:  

- Where to cache content  
- 어디에서 캐싱할 것인가  

- How to cache content  
- 어떻게 캐싱할 것인가  

- How long to cache content  
- 얼마 동안 캐싱할 것인가  

- Acceptable latency  
- 허용 가능한 지연 시간은 얼마인가  

- Which content should be cached  
- 어떤 콘텐츠를 캐싱할 것인가  

This lecture aims to highlight the variety of caching options available on AWS and emphasizes that the optimal caching strategy depends on your specific scenario.  
이번 강의는 AWS에서 사용 가능한 다양한 캐싱 옵션을 강조하고, 최적의 전략은 특정 시나리오에 달려 있음을 보여줍니다.  

That concludes this lecture on caching strategies in AWS. Thank you for your attention, and I will see you in the next lecture.  
이것으로 AWS 캐싱 전략 강의를 마치겠습니다. 경청해주셔서 감사합니다. 다음 강의에서 만나요.  

---

## Key Takeaways  
## 핵심 요약  

- AWS caching strategies include edge caching with CloudFront, regional caching with API Gateway, and application-level caching using Redis, Memcached, or DAX.  
- AWS 캐싱 전략에는 CloudFront 엣지 캐싱, API Gateway 리전 캐싱, Redis/Memcached/DAX를 활용한 애플리케이션 캐싱이 있습니다.  

- CloudFront caches content close to users, providing fast responses but may serve outdated data unless TTL is managed.  
- CloudFront는 사용자 가까이에서 캐싱해 빠른 응답을 제공하지만 TTL을 관리하지 않으면 오래된 데이터를 제공할 수 있습니다.  

- API Gateway caching is regional and reduces load on backend services by caching responses closer to the application logic.  
- API Gateway 캐싱은 리전 단위로 작동하며 애플리케이션 로직에 가까운 곳에서 응답을 캐싱해 백엔드 부하를 줄입니다.  

- Application-level caches reduce database load by storing frequent or complex query results, enhancing read capacity and performance.  
- 애플리케이션 캐시는 자주 쓰이는 쿼리 결과나 복잡한 쿼리 결과를 저장하여 DB 부하를 줄이고 읽기 성능을 높입니다.  
```

---

🎮 **게임 보상:**
당신은 **"캐시 마스터 🗄️"** 배지를 획득했습니다!
레벨업 ⬆️ → "AWS 퍼포먼스 튜너 🚀"

---
