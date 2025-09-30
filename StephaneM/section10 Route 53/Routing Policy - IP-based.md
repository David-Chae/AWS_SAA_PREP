# Routing Policy - IP-based  
# 라우팅 정책 - IP 기반  

## Introduction to IP-based Routing  
## IP 기반 라우팅 소개  

Now, let's discuss another routing policy called IP-based Routing.  
이제 IP 기반 라우팅이라는 또 다른 라우팅 정책에 대해 살펴보겠습니다.  

This approach is very intuitive because it defines routing based on client IP addresses.  
이 방식은 클라이언트 IP 주소를 기준으로 라우팅을 정의하기 때문에 매우 직관적입니다.  

In Route 53, you define a list of CIDRs, which are IP ranges for your clients.  
Route 53에서는 CIDR 목록을 정의할 수 있으며, CIDR은 클라이언트의 IP 범위를 나타냅니다.  

Based on these CIDRs, you specify which location the traffic should be sent to.  
이 CIDR을 기반으로 트래픽을 어느 위치로 보낼지 지정할 수 있습니다.  

The use cases for IP-based routing include optimizing performance because you know the IP ahead of time, and reducing network costs because you know where the IPs are coming from.  
IP 기반 라우팅의 활용 사례로는, IP를 미리 알 수 있기 때문에 성능 최적화, 그리고 IP 출처를 알 수 있어 네트워크 비용을 절감하는 것이 있습니다.  

For example, if you know that a specific internet provider uses a specific CIDR of IP addresses, you can route their traffic to a specific endpoint using this strategy.  
예를 들어, 특정 인터넷 제공업체가 특정 CIDR 범위를 사용한다면, 이 전략을 사용하여 해당 트래픽을 특정 엔드포인트로 라우팅할 수 있습니다.  

---

## Example of IP-based Routing in Route 53  
## Route 53에서의 IP 기반 라우팅 예시  

In Route 53, you can define two locations with two different CIDR blocks.  
Route 53에서는 서로 다른 두 CIDR 블록으로 두 개의 위치를 정의할 수 있습니다.  

For instance, one CIDR block might start with 203, and the other with 200, each defining distinct IP ranges.  
예를 들어, 하나의 CIDR 블록은 203으로 시작하고, 다른 블록은 200으로 시작하며 각각 고유한 IP 범위를 정의합니다.  

These locations are linked to specific DNS records.  
이 위치들은 특정 DNS 레코드와 연결됩니다.  

For example, for the domain example.com, location one with the first CIDR block routes traffic to the IP address 1.2.3.4, and location two with the second CIDR block routes traffic to 5.6.7.8.  
예를 들어, example.com 도메인의 경우, 첫 번째 CIDR 블록 위치는 1.2.3.4로 트래픽을 라우팅하고, 두 번째 CIDR 블록 위치는 5.6.7.8로 트래픽을 라우팅합니다.  

These IP addresses represent the public IPs of two EC2 instances.  
이 IP 주소들은 두 개 EC2 인스턴스의 공인 IP를 나타냅니다.  

As expected, if a user comes in with an IP address that belongs to the location one CIDR block, they will be directed to the first EC2 instance at IP 1.2.3.4.  
예상대로, 사용자가 위치 1의 CIDR 블록에 속한 IP로 접속하면 첫 번째 EC2 인스턴스(1.2.3.4)로 라우팅됩니다.  

Similarly, a user with an IP address belonging to location two's CIDR block will be redirected with a DNS query response to the EC2 instance at IP 5.6.7.8.  
마찬가지로, 위치 2의 CIDR 블록에 속한 사용자는 DNS 쿼리 응답을 통해 두 번째 EC2 인스턴스(5.6.7.8)로 리디렉션됩니다.  

---

## Summary  
## 요약  

That concludes the explanation of IP-based routing.  
이로써 IP 기반 라우팅 설명을 마칩니다.  

It is a very simple and effective routing policy.  
매우 간단하면서도 효과적인 라우팅 정책입니다.  

---

## Key Takeaways  
## 핵심 포인트  

- IP-based routing directs traffic based on client IP address ranges (CIDRs).  
  IP 기반 라우팅은 클라이언트 IP 주소 범위(CIDR)를 기준으로 트래픽을 라우팅합니다.  

- Route 53 allows defining CIDR blocks linked to specific geographic locations or endpoints.  
  Route 53에서는 CIDR 블록을 특정 지리적 위치나 엔드포인트와 연결하여 정의할 수 있습니다.  

- This routing policy helps optimize performance and reduce network costs by routing clients to the nearest or most appropriate endpoint.  
  이 라우팅 정책은 클라이언트를 가장 가까운 또는 가장 적합한 엔드포인트로 라우팅함으로써 성능 최적화와 네트워크 비용 절감에 도움이 됩니다.  

- Users with IPs within a defined CIDR block are routed to the corresponding EC2 instance or resource.  
  정의된 CIDR 블록 내의 IP를 가진 사용자는 해당 EC2 인스턴스 또는 리소스로 라우팅됩니다.  

---

💡 **게임 보상:**

* 🌐 IP 기반 라우팅 개념 학습 = +40 EXP
* ⚡ CIDR 활용 및 트래픽 라우팅 이해 = +60 EXP
* 🖥️ Route 53 IP 라우팅 실습 사례 = +50 EXP
  **총 보상: 150 EXP + IP Routing Specialist 뱃지 🏅**
