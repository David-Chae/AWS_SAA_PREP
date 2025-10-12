# Application Load Balancer (ALB)  
# 애플리케이션 로드 밸런서 (ALB)  
→ ALB에 대한 소개와 주요 특징을 다룹니다.  

## Introduction to Application Load Balancer (ALB)  
## ALB 소개  
→ 이제 두 번째 로드 밸런서 유형인 ALB를 살펴봅니다.  

Now, let's get into the second kind of load balancers we'll see: the Application Load Balancer. It is a layer seven only load balancer, which means it operates at the HTTP layer.  
이제 우리가 살펴볼 두 번째 로드 밸런서는 ALB입니다. ALB는 OSI 7계층 전용 로드 밸런서로, HTTP 계층에서 동작합니다.  
→ ALB는 L7(애플리케이션 계층)에서 동작하며, HTTP/HTTPS 트래픽을 세밀하게 제어할 수 있습니다.  

It allows you to route to multiple HTTP applications across machines. These machines are grouped in something called a target group.  
ALB는 여러 HTTP 애플리케이션을 머신 간에 라우팅할 수 있으며, 이러한 머신들은 타겟 그룹(target group)이라는 단위로 묶입니다.  
→ 핵심은 **타겟 그룹**이라는 개념으로, 여러 애플리케이션을 구분해서 관리할 수 있습니다.  

This concept will become clearer once we get into the hands-on section.  
이 개념은 실습 섹션에 들어가면 더 명확해질 것입니다.  
→ 나중에 실습을 통해 타겟 그룹이 실제로 어떻게 동작하는지 확인하게 됩니다.  

The Application Load Balancer allows you to load balance multiple applications on the same EC2 instance, which is useful when using containers and ECS, as we will see.  
ALB는 동일한 EC2 인스턴스에서 여러 애플리케이션을 로드 밸런싱할 수 있습니다. 이는 컨테이너나 ECS를 사용할 때 매우 유용합니다.  
→ 도커, ECS 같은 **컨테이너 기반 환경**에서 특히 강력합니다.  

It supports HTTP/2 and WebSockets protocols. Additionally, it supports redirect functionality, such as automatically redirecting traffic from HTTP to HTTPS at the load balancer level.  
HTTP/2와 WebSockets 프로토콜을 지원하며, HTTP 트래픽을 HTTPS로 자동 리디렉션하는 기능도 제공합니다.  
→ 최신 웹 프로토콜과 보안 강화를 위한 기능을 지원합니다.  

---

## Routing Capabilities of ALB  
## ALB의 라우팅 기능  
→ ALB의 핵심은 **다양한 조건 기반 라우팅**입니다.  

ALB supports route-based routing, which means you can route traffic based on different target groups.  
ALB는 경로 기반 라우팅을 지원하여 트래픽을 다른 타겟 그룹으로 보낼 수 있습니다.  
→ URL 경로나 호스트명을 기준으로 분기 처리 가능합니다.  

For example, you can route requests based on the path in your URL, such as example.com/users and example.com/posts.  
예: URL 경로 `/users`와 `/posts`에 따라 각각 다른 타겟 그룹으로 라우팅할 수 있습니다.  

You can also route based on the hostname of the URL.  
URL의 호스트명을 기준으로도 라우팅할 수 있습니다.  
→ 예: `one.example.com` → 그룹 A, `other.example.com` → 그룹 B.  

Furthermore, routing can be based on query strings and headers.  
쿼리 스트링(query string)과 헤더(header) 기반 라우팅도 가능합니다.  
→ 예: `/reserves?id=123&order=false` → 특정 그룹으로 연결.  

---

## Application Load Balancers in Microservices  
## 마이크로서비스에서의 ALB 활용  
→ **마이크로서비스 및 컨테이너 환경**에 최적화된 로드 밸런서입니다.  

Application Load Balancers are ideal when you have microservices and container-based applications.  
ALB는 마이크로서비스와 컨테이너 기반 애플리케이션에 이상적입니다.  

They have port mapping features that allow redirection to dynamic ports on ECS instances.  
포트 매핑 기능을 통해 ECS 인스턴스의 동적 포트로도 트래픽을 라우팅할 수 있습니다.  
→ ECS와의 통합성이 강력합니다.  

---

## Example Architecture  
## 예시 아키텍처  
→ 실제 사용 예를 통해 구조를 이해합니다.  

Consider an external Application Load Balancer that is public-facing.  
퍼블릭에 노출된 외부 ALB를 고려해봅시다.  

Behind it, there is a first target group made of EC2 instances routing traffic for the /user route.  
그 뒤에는 `/user` 요청을 처리하는 EC2 타겟 그룹이 있습니다.  

There is also a second target group, also made of EC2 instances, which serves a search application.  
또 다른 타겟 그룹은 `/search` 요청을 처리하는 검색 애플리케이션을 담당합니다.  

Both are behind the same Application Load Balancer, which intelligently routes requests.  
이 두 애플리케이션은 동일한 ALB 뒤에 있으며, ALB가 URL 경로에 따라 트래픽을 분산시킵니다.  

---

## Target Groups  
## 타겟 그룹  
→ ALB의 핵심 구성 단위입니다.  

Target groups can consist of:  
타겟 그룹은 다음으로 구성될 수 있습니다:  

- EC2 instances (often with Auto Scaling)  
- EC2 인스턴스 (오토 스케일링과 함께)  

- ECS tasks  
- ECS 태스크  

- Lambda functions  
- 람다 함수  

- Private IP addresses  
- 사설 IP 주소  

Health checks are performed at the target group level.  
헬스 체크는 타겟 그룹 단위로 수행됩니다.  

---

## Advanced Routing Example  
## 고급 라우팅 예제  
→ 복잡한 시나리오에도 유연하게 대응 가능합니다.  

Imagine an ALB with two target groups: EC2 and on-prem private servers.  
ALB가 두 개의 타겟 그룹(EC2와 온프레미스 서버)을 가진다고 가정합시다.  

You can use query string rules like ?platform=mobile or ?platform=desktop.  
쿼리 스트링 `?platform=mobile` → 모바일 그룹, `?platform=desktop` → 데스크톱 그룹으로 라우팅할 수 있습니다.  

---

## Additional ALB Features  
## 추가 기능  
→ 실무에서 자주 쓰이는 중요한 기능들입니다.  

- ALB provides a fixed hostname.  
- ALB는 고정된 호스트명을 제공합니다.  

- Client IP is preserved in `X-Forwarded-For`.  
- 실제 클라이언트 IP는 `X-Forwarded-For` 헤더에 기록됩니다.  

- Client port and protocol are available via `X-Forwarded-Port` and `X-Forwarded-Proto`.  
- 클라이언트 포트와 프로토콜은 `X-Forwarded-Port`, `X-Forwarded-Proto`에서 확인할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  
→ ALB의 장점을 간단히 정리합니다.  

- Operates at **Layer 7**, supports HTTP, HTTP/2, WebSockets  
- **7계층에서 동작**, HTTP, HTTP/2, WebSockets 지원  

- Supports **path, host, query string, header-based routing**  
- 경로, 호스트, 쿼리, 헤더 기반 라우팅 지원  

- Target groups = EC2, ECS, Lambda, private IPs  
- 타겟 그룹 = EC2, ECS, Lambda, 사설 IP  

- Features: HTTP→HTTPS redirection, client IP preservation  
- 주요 기능: HTTP→HTTPS 자동 리디렉션, 클라이언트 IP 보존  
