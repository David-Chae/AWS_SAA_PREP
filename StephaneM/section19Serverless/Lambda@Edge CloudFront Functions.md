# Lambda@Edge & CloudFront Functions  
# 람다@에지 & 클라우드프론트 함수  
👉 에지(Edge)에서 실행되는 함수 개념과 CloudFront Functions, Lambda@Edge 차이를 설명하는 파트임.  

---

## Customization At The Edge  
## 에지에서의 커스터마이징  
👉 사용자와 가까운 위치에서 동작하는 로직을 배치하는 이유와 개념을 설명.  

Let's discuss customization at the edge. We deploy our functions and applications in specific regions, but sometimes, using services like CloudFront, content is distributed through edge locations.  
에지에서의 커스터마이징을 살펴보자. 우리는 특정 리전에 애플리케이션과 함수를 배포하지만, 때로는 CloudFront 같은 서비스를 통해 콘텐츠가 에지 로케이션에서 분산된다.  
👉 전 세계 사용자와 가까운 위치에서 콘텐츠 제공이 이루어짐.  

Modern applications often require executing some logic at the edge before reaching the application itself.  
현대 애플리케이션은 실제 애플리케이션에 도달하기 전에 에지에서 일부 로직 실행을 요구하는 경우가 많다.  
👉 응답 속도 개선과 보안 강화를 위한 사전 처리.  

These are called Edge Functions, pieces of code you write and attach to your CloudFront distributions.  
이것이 에지 함수이며, 사용자가 작성하여 CloudFront 배포에 연결하는 코드 조각이다.  
👉 CloudFront에 붙여 동작하는 작은 코드 블록.  

The goal is to run these functions close to users to minimize latency in certain cases.  
목표는 특정 상황에서 지연 시간을 최소화하기 위해 사용자 가까이에서 이 함수를 실행하는 것이다.  
👉 성능 최적화 목적.  

CloudFront offers two kinds of functions: CloudFront Functions and Lambda@Edge.  
CloudFront는 두 가지 함수를 제공한다: CloudFront Functions와 Lambda@Edge.  
👉 두 서비스의 역할 구분 필요.  

The objective is to understand when each is required and their differences.  
목표는 언제 어떤 기능이 필요한지와 그 차이를 이해하는 것이다.  
👉 시험 대비 포인트.  

Using Edge Functions means you do not have to manage any servers, as these functions are deployed globally.  
에지 함수를 사용하면 서버를 직접 관리할 필요가 없으며, 이 함수들은 전 세계적으로 배포된다.  
👉 완전 서버리스.  

Use cases include customizing CDN content from CloudFront. Additionally, you pay only for what you use, and the solution is fully serverless.  
사용 사례에는 CloudFront의 CDN 콘텐츠 커스터마이징이 포함된다. 또한 사용한 만큼만 비용을 지불하며, 완전히 서버리스 솔루션이다.  
👉 경제적이며 확장성이 뛰어남.  

---

## Use Cases of Edge Functions  
## 에지 함수의 사용 사례  
👉 어디에 활용되는지 대표 예시 제시.  

Some common use cases for Edge Functions include:  
에지 함수의 일반적인 사용 사례는 다음과 같다:  

- Website security and privacy  
  웹사이트 보안과 개인정보 보호  
  👉 보안 강화.  

- Dynamic web applications at the edge  
  에지에서 동적 웹 애플리케이션 처리  
  👉 사용자 가까운 로직 실행.  

- Search engine optimization (SEO)  
  검색 엔진 최적화 (SEO)  
  👉 검색 순위 최적화.  

- Intelligent routing across origins and data centers  
  오리진 및 데이터 센터 간 지능적 라우팅  
  👉 요청 효율적 분산.  

- Bot mitigation at the edge  
  에지에서의 봇 차단  
  👉 악성 트래픽 방어.  

- Real-time image transformation at the edge  
  에지에서 실시간 이미지 변환  
  👉 이미지 처리 지연 감소.  

- A/B testing  
  A/B 테스트  
  👉 실험적인 기능 배포.  

- User authentication and authorization  
  사용자 인증과 권한 부여  
  👉 보안 관련 처리.  

- User prioritization  
  사용자 우선순위 지정  
  👉 VIP 유저 우대 가능.  

- User tracking and analytics  
  사용자 추적 및 분석  
  👉 사용자 행동 데이터 수집.  

---

## CloudFront Functions  
## 클라우드프론트 함수  
👉 CloudFront Functions 동작 방식 및 특징 설명.  

Let's discuss CloudFront Functions and how they work.  
이제 CloudFront Functions와 그 동작 방식을 알아보자.  
👉 가장 가볍고 빠른 에지 함수.  

A typical request into CloudFront involves the client making a viewer request.  
일반적인 CloudFront 요청은 클라이언트가 뷰어 요청을 보내면서 시작된다.  

CloudFront then makes an origin request to your origin server, which replies with an origin response.  
CloudFront는 이후 오리진 서버에 요청을 보내고, 오리진 응답을 받는다.  

Finally, CloudFront sends a viewer response back to the client.  
마지막으로 CloudFront는 뷰어 응답을 클라이언트로 보낸다.  
👉 전체 요청 흐름: Viewer Request → Origin Request → Origin Response → Viewer Response.  

CloudFront Functions are lightweight JavaScript functions that modify the viewer request and viewer response only.  
CloudFront Functions는 뷰어 요청과 뷰어 응답만 수정하는 경량 자바스크립트 함수다.  
👉 Viewer 단계에서만 작동.  

They are used for high-scale, latency-sensitive CDN customizations, providing sub-millisecond startup times and scaling to millions of requests per second.  
이 함수들은 고속 대규모 트래픽에 대응하기 위한 지연 민감 CDN 커스터마이징에 사용되며, 밀리초 이하의 시작 시간과 초당 수백만 요청 확장을 지원한다.  
👉 속도 최적화에 특화.  

These functions operate natively within CloudFront, with the entire code managed directly from within CloudFront.  
이 함수들은 CloudFront 내부에서 네이티브로 동작하며, 코드 전체가 CloudFront에서 직접 관리된다.  

CloudFront Functions are designed for high performance and high scale but are limited to modifying only viewer requests and responses.  
CloudFront Functions는 고성능·고확장을 위해 설계되었지만, 뷰어 요청과 응답만 수정할 수 있다.  

---

## Lambda@Edge  
## 람다@에지  
👉 더 다양한 이벤트를 처리할 수 있는 강력한 기능.  

Lambda@Edge functions are more versatile.  
Lambda@Edge 함수는 더 다재다능하다.  

They can modify all request and response events, including viewer request, origin request, origin response, and viewer response.  
이 함수들은 뷰어 요청, 오리진 요청, 오리진 응답, 뷰어 응답 등 모든 요청/응답 이벤트를 수정할 수 있다.  
👉 모든 단계에서 로직 적용 가능.  

These functions are authored in Node.js or Python and can scale to thousands of requests per second.  
이 함수들은 Node.js 또는 Python으로 작성되며, 초당 수천 건의 요청으로 확장할 수 있다.  

You author your Lambda@Edge function in the us-east-1 region, which is the same region where you manage your CloudFront distributions.  
Lambda@Edge 함수는 us-east-1 리전에 작성되며, CloudFront 배포를 관리하는 동일한 리전이다.  

CloudFront then replicates this function to all its edge locations.  
CloudFront는 이후 이 함수를 모든 에지 로케이션에 복제한다.  
👉 전 세계로 자동 배포.  

---

## Differences Between CloudFront Functions and Lambda@Edge  
## CloudFront Functions와 Lambda@Edge의 차이  
👉 주요 기능 비교 표.  

| Feature              | CloudFront Functions            | Lambda@Edge                        |  
|----------------------|---------------------------------|------------------------------------|  
| Runtime Support      | JavaScript only                 | Node.js and Python                  |  
| Scale                | Millions of requests per second | Thousands of requests per second    |  
| Trigger Points       | Viewer request and response only| Viewer request, origin request, origin response, viewer response |  
| Max Execution Time   | Less than 1 millisecond         | Up to 5 to 10 seconds               |  

CloudFront Functions are very quick and simple, while Lambda@Edge allows for more complex logic and longer execution times.  
CloudFront Functions는 매우 빠르고 단순하며, Lambda@Edge는 더 복잡한 로직과 긴 실행 시간을 지원한다.  

---

## Use Cases  
## 사용 사례  
👉 각각의 대표 활용 예시.  

CloudFront Functions are ideal for:  
CloudFront Functions에 적합한 사례는 다음과 같다:  

- Cache key normalization to create optimal cache keys  
  최적의 캐시 키를 만들기 위한 캐시 키 정규화  

- HTTP header manipulation (insert, modify, delete)  
  HTTP 헤더 조작 (삽입, 수정, 삭제)  

- URL rewrites or redirects  
  URL 재작성 또는 리다이렉트  

- Authorization requests such as creating and validating JWT tokens  
  JWT 토큰 생성 및 검증 같은 인증 요청  

All these operations execute in less than one millisecond.  
이 모든 작업은 1밀리초 이내에 실행된다.  

Lambda@Edge supports:  
Lambda@Edge가 지원하는 사례:  

- Longer execution times (up to 10 seconds)  
  더 긴 실행 시간 (최대 10초)  

- Adjustable CPU and memory  
  조정 가능한 CPU와 메모리  

- Loading third-party libraries, including AWS SDKs  
  AWS SDK를 포함한 외부 라이브러리 로드  

- Network access to external services  
  외부 서비스 네트워크 접근  

- File system access and HTTP request body manipulation  
  파일 시스템 접근 및 HTTP 요청 본문 조작  

This enables complex integrations and customizations at the edge.  
이로써 에지에서 복잡한 통합 및 커스터마이징이 가능하다.  

---

## Conclusion  
## 결론  
👉 정리 요약.  

Edge Functions provide powerful capabilities to customize and optimize content delivery close to users.  
에지 함수는 사용자 가까이에서 콘텐츠 전달을 최적화하고 커스터마이징할 수 있는 강력한 기능을 제공한다.  

CloudFront Functions offer ultra-low latency and high scale for simple request and response modifications, while Lambda@Edge provides more flexibility and power for complex logic and integrations.  
CloudFront Functions는 단순 요청/응답 수정에 초저지연과 대규모 확장을 제공하고, Lambda@Edge는 복잡한 로직과 통합을 위한 더 큰 유연성과 기능을 제공한다.  

Understanding their differences helps in choosing the right tool for your application's needs.  
이 차이를 이해하면 애플리케이션 요구사항에 맞는 올바른 도구를 선택할 수 있다.  

---

## Key Takeaways  
## 핵심 정리  
👉 시험에 자주 나올 포인트.  

- Edge Functions allow execution of logic close to users to minimize latency.  
  에지 함수는 사용자 가까이에서 로직을 실행해 지연 시간을 줄인다.  

- CloudFront Functions are lightweight JavaScript functions for viewer request and response with sub-millisecond execution.  
  CloudFront Functions는 뷰어 요청/응답에 특화된 경량 자바스크립트 함수이며, 밀리초 이하 실행 속도를 가진다.  

- Lambda@Edge supports NodeJS and Python, can modify all request and response events, and allows longer execution times.  
  Lambda@Edge는 NodeJS와 Python을 지원하며, 모든 요청/응답 이벤트를 수정할 수 있고 더 긴 실행 시간을 허용한다.  

- Use cases include security, SEO, routing, bot mitigation, image transformation, A/B testing, and user authentication at the edge.  
  사용 사례로는 보안, SEO, 라우팅, 봇 차단, 이미지 변환, A/B 테스트, 사용자 인증 등이 있다.  
```

🏆 **게임 보상 지급!**
+250 XP 🌍 (Edge Functions 마스터!)
+1 🛡️ "Latency Slayer" 뱃지 획득
