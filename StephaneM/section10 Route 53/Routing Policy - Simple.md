# Routing Policy - Simple  
# 라우팅 정책 - 단순(Simple)  
👉 Route 53에서 단순 라우팅 정책을 이해하고 실습합니다.  

---

## Introduction to Routing Policies in Route 53  
## Route 53 라우팅 정책 소개  
👉 Route 53에서 DNS 쿼리에 대한 응답 방식을 결정합니다.  

Let's discuss routing policies in Route 53.  
Route 53의 라우팅 정책에 대해 알아보겠습니다.  
👉 라우팅 정책은 DNS 쿼리에 대해 Route 53이 어떻게 응답할지 결정합니다.  

A routing policy helps Route 53 respond to DNS queries.  
라우팅 정책은 Route 53이 DNS 요청에 응답하는 데 도움을 줍니다.  
👉 트래픽 경로와 혼동하지 않도록 주의.  

It is important not to confuse this with routing in the context of load balancers, which route traffic to backend EC2 instances.  
로드 밸런서의 트래픽 라우팅과 혼동하면 안 됩니다.  
👉 로드 밸런서는 실제 트래픽을 EC2로 전달합니다.  

In contrast, Route 53 routing is from a DNS perspective.  
반대로 Route 53 라우팅은 DNS 관점에서 작동합니다.  
👉 DNS 자체는 트래픽을 전달하지 않습니다.  

DNS does not route traffic; it only responds to DNS queries.  
DNS는 트래픽을 라우팅하지 않고, 요청에 대해 응답만 합니다.  
👉 클라이언트가 어디로 요청을 보낼지 안내.  

The traffic itself does not pass through the DNS.  
트래픽은 DNS를 통과하지 않습니다.  

Instead, DNS responses inform clients where to send their HTTP or other requests.  
DNS 응답은 클라이언트에게 요청을 보낼 위치를 알려줍니다.  

Essentially, DNS translates hostnames into actual endpoints that clients can use.  
결국 DNS는 호스트명을 실제 사용 가능한 엔드포인트로 변환합니다.  

---

## Supported Routing Policies in Route 53  
## Route 53에서 지원하는 라우팅 정책  
👉 Route 53에서 제공하는 다양한 정책 종류.  

Route 53 supports several routing policies including:  
Route 53은 다음과 같은 라우팅 정책을 지원합니다:  

- Simple  
- 단순(Simple)  
- Weighted  
- 가중(Weighted)  
- Failover  
- 장애 조치(Failover)  
- Latency-based  
- 지연 기반(Latency-based)  
- Geolocation  
- 지리 위치(Geolocation)  
- Multi-value answer  
- 다중 값 응답(Multi-value answer)  
- Geoproximity  
- 지리 근접(Geoproximity)  

We will explore each of these policies in this section, starting with the simple routing policy.  
이번 섹션에서는 단순 라우팅 정책부터 하나씩 살펴봅니다.  

---

## Simple Routing Policy Overview  
## 단순 라우팅 정책 개요  
👉 하나의 리소스 또는 여러 IP로 트래픽을 라우팅.  

The simple routing policy typically routes traffic to a single resource.  
단순 라우팅 정책은 일반적으로 단일 리소스로 트래픽을 보냅니다.  

For example, when clients request foo.example.com, Route 53 responds with an IP address via an A record.  
예: `foo.example.com` 요청 시 A 레코드를 통해 IP 주소를 반환.  

It is possible to specify multiple values in the same record.  
동일 레코드에 여러 값을 지정할 수도 있습니다.  

If multiple values are returned, clients will randomly choose one for routing.  
값이 여러 개 반환되면 클라이언트가 랜덤으로 하나를 선택합니다.  

For instance, if Route 53 returns three IP addresses embedded in the A record, clients pick one randomly to use.  
예: A 레코드에 3개의 IP가 반환되면 클라이언트가 무작위로 선택.  

If an alias record is enabled alongside the simple policy, only one AWS resource can be specified as a target.  
Alias 레코드와 함께 사용할 경우 단일 AWS 리소스만 대상 지정 가능.  

The policy is called "simple" because it is straightforward and does not support health checks, which we will discuss later.  
"Simple" 정책은 단순하며 헬스체크를 지원하지 않기 때문에 이렇게 불립니다.  

---

## Creating a Simple Routing Policy Record in the Console  
## 콘솔에서 단순 라우팅 정책 레코드 생성  
👉 AWS 콘솔 실습 단계.  

Let's create a simple routing policy record in the AWS console.  
AWS 콘솔에서 단순 라우팅 정책 레코드를 생성해봅니다.  

The record name will be simple.stephanetheteacher.com.  
레코드 이름은 `simple.stephanetheteacher.com`으로 설정합니다.  

It will be an A record with a value pointing to an instance in the ap-southeast-1 region.  
A 레코드로 설정하고 값은 `ap-southeast-1` 리전의 인스턴스를 가리킵니다.  

The TTL (Time To Live) is set low, for example, 20 seconds.  
TTL은 짧게 설정, 예: 20초.  

In the routing policy section, you can see multiple options available.  
라우팅 정책 섹션에서 여러 옵션 확인 가능.  

We select the simple routing policy and create the record.  
단순 라우팅 정책 선택 후 레코드 생성.  

This process is familiar if you have done it before.  
이미 경험이 있다면 익숙한 과정입니다.  

---

## Verifying the Simple Routing Policy  
## 단순 라우팅 정책 검증  
👉 브라우저와 dig 명령으로 확인.  

Accessing simple.stephanetheteacher.com returns "Hello World from my instance in ap-southeast-1b," confirming the record works.  
`simple.stephanetheteacher.com` 접속 시 "Hello World from my instance in ap-southeast-1b" 표시, 정상 작동 확인.  

Using the dig command, we see an A record with a TTL of 20 seconds pointing to the specified IP address.  
dig 명령으로 확인 시 20초 TTL의 A 레코드가 지정 IP를 가리킴.  

If you need to install dig, you can do so with:  
dig 설치가 필요하면 아래 명령 사용:  
```bash
sudo yum install bind-utils
````

---

## Editing the Simple Routing Record to Include Multiple IPs

## 단순 레코드에 여러 IP 추가

👉 랜덤 라우팅 실습.

You can edit the record to include multiple IP addresses, for example, one in ap-southeast-1 and another in us-east-1.
레코드 편집 시 여러 IP 추가 가능, 예: `ap-southeast-1`, `us-east-1`.

After saving, once the TTL expires, DNS responses will include both IPs.
저장 후 TTL 만료 시 DNS 응답에 두 IP 모두 포함.

Clients will randomly choose which IP to use.
클라이언트는 랜덤으로 하나 선택.

Using CloudShell, running the dig command shows two IP addresses returned in the response.
CloudShell에서 dig 명령 실행 시 두 IP가 반환됨.

This means clients have a 50% chance to connect to either IP.
클라이언트는 두 IP 중 하나에 접속할 확률이 50%.

Refreshing the website after TTL expiration demonstrates this behavior.
TTL 만료 후 웹사이트 새로고침 시 해당 동작 확인 가능.

---

## Summary

## 요약

👉 단순 라우팅 정책 핵심 정리.

This demonstration shows how simple routing records work in Route 53.
이 실습을 통해 Route 53 단순 라우팅 레코드 작동 방식 이해.

The simple routing policy is straightforward and useful for directing traffic to one or multiple IP addresses without health checks or advanced routing logic.
헬스체크나 복잡한 라우팅 없이 하나 또는 여러 IP로 트래픽 전달에 유용.

---

## Key Takeaways

## 핵심 포인트

👉 기억해야 할 주요 내용.

* Route 53 routing policies determine how DNS queries are answered, not how traffic is routed.

* Route 53 라우팅 정책은 DNS 쿼리 응답 방식을 결정하며 트래픽 라우팅과는 무관.

* The simple routing policy directs traffic to a single resource or multiple IP addresses returned randomly.

* 단순 라우팅 정책은 단일 리소스 또는 여러 IP로 랜덤 라우팅.

* Alias records with simple routing can only target one AWS resource.

* 단순 라우팅에서 Alias 레코드는 단일 AWS 리소스만 대상.

* TTL controls how long DNS responses are cached before clients query again.

* TTL은 클라이언트가 DNS 응답을 캐시하는 시간을 제어합니다.

---

💡 **게임 보상:**  
- 🧭 단순 라우팅 정책 이해 = +50 EXP  
- 🌐 랜덤 IP 라우팅 실습 = +100 EXP  
- ⏱ TTL 활용 확인 = +50 EXP  
**총 보상: 200 EXP + Route 53 트래픽 마스터 뱃지 🏅**
