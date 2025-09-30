# Routing Policy - Latency  
# 라우팅 정책 - 지연 시간(Latency) 기반  
👉 지연 시간 기반 라우팅 정책을 이해하고 실습합니다.  

---

## Introduction to Latency-Based Routing Policy  
## 지연 시간 기반 라우팅 정책 소개  
👉 사용자를 가장 낮은 지연 시간을 제공하는 리소스로 라우팅합니다.  

Let's discuss a routing policy that is straightforward to understand: the latency-based routing policy.  
이해하기 쉬운 라우팅 정책: 지연 시간 기반 라우팅 정책에 대해 알아봅니다.  

The core idea is to redirect users to the resource that offers the lowest latency, essentially the closest resource to them.  
핵심 아이디어: 사용자를 가장 낮은 지연 시간을 가진 리소스로 연결, 즉 사용자와 가장 가까운 리소스.  

This approach is particularly beneficial when latency is the primary concern for your websites or applications.  
웹사이트나 앱에서 지연 시간이 중요할 때 매우 유용합니다.  

Latency is measured based on how quickly users can connect to the closest identified AWS region for a given record.  
지연 시간은 사용자가 특정 레코드의 가장 가까운 AWS 리전에 얼마나 빨리 연결되는지 기준으로 측정.  

For example, if a user is in Germany and the lowest latency is to a resource in the US, the user will be redirected there.  
예: 사용자가 독일에 있고, 가장 낮은 지연 시간 리소스가 미국이라면 미국으로 라우팅.  

This routing policy can be combined with health checks, which will be covered in the next lecture.  
헬스체크와 결합 가능하며, 이는 다음 강의에서 다룸.  

---

## Understanding Latency Routing with a Global Map  
## 전 세계 지도 기반 지연 시간 라우팅 이해  
👉 글로벌 사용자 위치에 따라 최적 리소스로 연결.  

Consider deploying your applications in two different parts of the world: one in us-east-1 and another in ap-southeast-1.  
앱을 두 개 리전(us-east-1, ap-southeast-1)에 배포한다고 가정.  

Users are distributed globally, and Route 53 evaluates latency to determine routing.  
사용자가 전 세계에 분포, Route 53이 지연 시간을 평가하여 라우팅 결정.  

Users closest to and with the lowest latency to the Application Load Balancer (ALB) in us-east-1 will be redirected there, while others will be directed to ap-southeast-1.  
us-east-1 ALB에 가장 가까운 사용자/낮은 지연 사용자 → us-east-1, 그 외 → ap-southeast-1.  

---

## Creating Latency-Based Records in Route 53 Console  
## Route 53 콘솔에서 지연 시간 기반 레코드 생성  
👉 실습: 지연 시간 레코드 생성.  

Let's put this into practice by creating new DNS records in the Route 53 console.  
Route 53 콘솔에서 새 DNS 레코드 생성 실습.  

The record name will be latency.stephanetheteacher.com.  
레코드 이름: `latency.stephanetheteacher.com`.  

The first value corresponds to the ap-southeast-1 region. Paste the IP address associated with this region.  
첫 번째 값: `ap-southeast-1` 리전 IP.  

Set the routing policy to Latency.  
라우팅 정책: Latency로 설정.  

Since the record uses an IP address, specify the region explicitly as ap-southeast-1 (Singapore) because the alias cannot infer the region from the IP.  
IP 기반 레코드이므로 리전을 명시적으로 `ap-southeast-1`로 지정.  

Optionally, associate a health check and assign a record ID, here named ap-southeast-1.  
옵션: 헬스체크 연결, 레코드 ID 지정(`ap-southeast-1`).  

Next, add another record:  
다음, 다른 레코드 추가:  

The record name remains latency.  
레코드 이름은 동일(`latency`).  

The value corresponds to us-east-1; paste the respective IP address.  
값: `us-east-1` IP.  

Set the routing policy to Latency.  
라우팅 정책: Latency.  

Specify the region as us-east-1.  
리전: `us-east-1`.  

Assign a record ID, for example, us-east-1.  
레코드 ID: `us-east-1`.  

Finally, add a third record for eu-central-1:  
마지막으로 eu-central-1 레코드 추가:  

Use the same record name latency.  
레코드 이름: 동일(`latency`).  

Paste the IP address for eu-central-1.  
IP: `eu-central-1`.  

Set the routing policy to Latency.  
라우팅 정책: Latency.  

Specify the region as eu-central-1.  
리전: `eu-central-1`.  

Assign a record ID, such as eu-central-1.  
레코드 ID: `eu-central-1`.  

After creating these three records successfully, you can test the latency-based routing.  
3개 레코드 생성 후 지연 시간 기반 라우팅 테스트 가능.  

Currently, being in Europe, accessing the URL should route you to the instance in Europe (eu-central-1).  
현재 유럽 위치이면 URL 접속 시 유럽 인스턴스(eu-central-1)로 라우팅.  

Upon visiting the URL, you should receive a response such as "Hello World" from the IP in eu-central-1c.  
접속 시 eu-central-1c IP에서 "Hello World" 응답 확인.  

Using CloudShell, performing a dig command on the domain returns a single IP address corresponding to the European instance.  
CloudShell에서 dig 명령 실행 시 유럽 인스턴스 IP 반환.  

Refreshing the page repeatedly will yield the same response as long as the latency remains unchanged.  
페이지 새로고침 반복 시 지연 시간 변하지 않으면 동일 응답 유지.  

---

## Testing Latency Routing with VPN  
## VPN으로 지연 시간 라우팅 테스트  
👉 VPN 사용으로 다른 지역 시뮬레이션.  

To test if the latency record is functioning correctly, use a VPN to simulate different geographic locations.  
VPN으로 다른 지역 위치를 시뮬레이션해 지연 시간 레코드 확인.  

For example, connecting through a VPN in Canada will make your latency closest to the US region.  
예: 캐나다 VPN 연결 → 미국 리전이 가장 낮은 지연 시간.  

Refreshing the page should then return "Hello World" from the US instance (us-east-1).  
페이지 새로고침 → 미국 인스턴스(us-east-1) "Hello World" 응답.  

Changing the location via VPN clears the DNS cache's TTL on your local machine, allowing the new routing to take effect immediately.  
VPN으로 위치 변경 → 로컬 DNS 캐시 TTL 초기화, 즉시 새로운 라우팅 적용.  

However, running the dig command from CloudShell, which is located in Europe, will still return the European IP address because CloudShell's location has not changed.  
하지만 CloudShell(Europe)에서 dig 실행 시 유럽 IP 반환, CloudShell 위치는 변경되지 않음.  

Similarly, testing from Hong Kong, which is close to Singapore, should route you to the ap-southeast-1 region.  
홍콩에서 테스트 시 → ap-southeast-1로 라우팅.  

Refreshing the page will return "Hello World" from ap-southeast-1b, confirming that the latency records are working effectively.  
페이지 새로고침 → ap-southeast-1b "Hello World", 레코드 정상 작동 확인.  

Latency-based routing policies are highly effective and commonly used to optimize user experience by minimizing latency.  
지연 시간 기반 라우팅은 사용자 경험 최적화에 매우 효과적.  

Thank you for following along, and I look forward to seeing you in the next lecture.  
참여 감사합니다. 다음 강의에서 만나요.  

---

## Key Takeaways  
## 핵심 포인트  
Latency-based routing policies redirect users to the resource with the lowest latency, improving user experience.  
지연 시간 기반 라우팅은 가장 낮은 지연 시간 리소스로 사용자 라우팅 → UX 향상.  

Latency is measured by how quickly users connect to the closest AWS region associated with the record.  
지연 시간 = 사용자가 레코드 관련 가장 가까운 AWS 리전에 연결되는 속도.  

Route 53 evaluates user locations globally to route traffic to the nearest available resource.  
Route 53은 글로벌 사용자 위치 평가 → 가장 가까운 리소스로 트래픽 전달.  

Testing latency routing can be done effectively using VPNs to simulate different geographic locations.  
VPN으로 지리적 위치 시뮬레이션 → 지연 시간 라우팅 테스트 가능.  

---

💡 **게임 보상:**

* 🌍 글로벌 지연 시간 라우팅 이해 = +50 EXP
* 🖥️ VPN 테스트로 지역별 라우팅 확인 = +50 EXP
* ⚡ 최적 UX 제공 라우팅 학습 = +100 EXP
  **총 보상: 200 EXP + Latency Routing 마스터 뱃지 🏅**
