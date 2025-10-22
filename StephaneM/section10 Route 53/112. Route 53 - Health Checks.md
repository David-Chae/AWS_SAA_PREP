
# 🌍 Route 53 Health Check 쉽게 이해하기

---

## 1️⃣ 개요: “Route 53 헬스체크란?”

**Route 53 Health Check**는
AWS의 **DNS 서비스(Route 53)** 안에 있는 **“상태 점검 기능”**이에요.

쉽게 말해,
👉 “내 웹사이트나 서버가 지금 살아 있는지 죽었는지 자동으로 감시하는 도우미”입니다.

DNS는 원래 사용자를 “어디로 보낼지” 결정하죠.
그런데 만약 한 리전(region)의 서버가 죽어 있다면?
→ 헬스체크가 그걸 감지해서 “죽은 곳은 빼고, 살아있는 곳으로만” 트래픽을 보내줍니다.

> 💡 **즉, 헬스체크 = 트래픽을 ‘건강한 서버’로만 보내는 심장박동 모니터**라고 보면 됩니다.

---

## 2️⃣ 실제 예시로 보기

예를 들어,

* 미국(us-east-1) 리전과 유럽(eu-west-1) 리전에
  같은 웹서비스가 운영되고 있고
* Route 53이 `mydomain.com` 도메인을 관리한다고 해볼게요.

Route 53은 사용자의 위치를 보고
**지연 시간이 가장 짧은 리전**으로 연결시킵니다 (지연 시간 기반 라우팅).

그런데 만약 유럽 서버가 다운되면?
→ 헬스체크가 즉시 “비정상” 상태를 감지
→ Route 53은 자동으로 트래픽을 미국 서버로만 보내요.

✅ 결과:
사용자는 서버 장애를 **거의 모른 채로** 정상 접속 가능합니다.
이게 **자동 DNS 장애조치(Auto Failover)**의 핵심이에요.

---

## 3️⃣ 헬스체크의 세 가지 유형

| 유형                         | 설명                                                         | 예시                              |
| -------------------------- | ---------------------------------------------------------- | ------------------------------- |
| **1️⃣ 엔드포인트 헬스체크**         | 웹사이트, 서버, ALB 등 **공용 리소스의 상태**를 직접 확인                      | “내 웹사이트가 200 OK 응답을 주는지?”       |
| **2️⃣ 계산(계층형) 헬스체크**       | 여러 개의 헬스체크 결과를 조합해 하나로 판단                                  | “3개의 서버 중 2개 이상만 정상이어도 OK”      |
| **3️⃣ CloudWatch 알람 헬스체크** | **사설 리소스(VPC 내부 등)**는 외부에서 접근이 불가능하므로 CloudWatch 알람을 대신 사용 | “내 VPC EC2가 CPU 100%면 비정상으로 표시” |

---

## 4️⃣ 엔드포인트 헬스체크 작동 원리

### 🧠 기본 개념

* AWS는 전 세계에 **약 15개의 헬스체커(Health Checker)**를 두고 있어요.
* 이 헬스체커들이 주기적으로 (30초 or 10초마다)
  여러분의 웹주소로 요청을 보냅니다.

### 📡 작동 과정

1. 헬스체커가 웹서버(또는 ALB)에 접속
2. 응답코드(예: `200 OK`)를 받음
3. 일정 비율 이상(보통 18개 이상)이 정상 응답을 보고하면 → “정상(Healthy)”
   그렇지 않으면 → “비정상(Unhealthy)”

### ⚙️ 설정 포인트

* **주기**: 30초 (기본) / 10초(고속, 비용 높음)
* **프로토콜**: HTTP / HTTPS / TCP
* **검사 내용**: 응답 코드뿐 아니라 **응답 텍스트의 특정 문구**도 검사 가능 (5120바이트까지)

> 💬 비유하자면,
> “15명의 의사가 환자(서버)를 동시에 진찰해서,
> 18명 이상이 ‘건강하다’고 말하면 건강하다고 인정하는 시스템”이에요.

### ⚠️ 네트워크 주의사항

Route 53 헬스체커가 엔드포인트에 접근할 수 있어야 하므로,
**Route 53 Health Checker IP 범위를 보안그룹에서 허용**해야 합니다.

---

## 5️⃣ 계산 헬스체크 (Calculated Health Check)

이건 “**여러 헬스체크를 모아 판단하는 상위 헬스체크**”예요.

예를 들어,

* EC2 인스턴스 3개를 각각 따로 모니터링 중
* 그런데 전체 서비스는 “3개 중 2개만 살아 있으면 정상”

→ 이럴 때 “부모 헬스체크”를 만들고
논리식(AND, OR, NOT)을 조합해
“2개 이상 정상일 때 전체 정상”으로 판단하게 할 수 있습니다.

> ⚙️ 최대 256개의 자식 헬스체크를 묶을 수 있어요.

---

## 6️⃣ 사설 리소스 모니터링 (Private Resources)

### 🔒 문제

Route 53 헬스체커는 “공용 인터넷”에서 작동하므로
VPC 내부나 On-premise 같은 “비공개 네트워크”에는 접근할 수 없어요.

### 💡 해결

1. **CloudWatch Metric**으로 사설 리소스 상태를 추적 (예: EC2 CPU 사용률, 응답 지연 등)
2. **CloudWatch Alarm**을 설정해서 “이상이 있으면 경보 상태로”
3. 그 알람을 Route 53 Health Check와 연결

→ CloudWatch Alarm이 “비정상 상태”로 바뀌면,
Route 53도 그 리소스를 “Unhealthy”로 간주.

결과적으로 **사설 리소스도 간접적으로 헬스체크** 가능해집니다.

> 🔁 CloudWatch ↔ Route 53 연동을 통해
> 내부 서버 상태를 외부 DNS 라우팅에 반영하는 셈이죠.

---

## 🧾 핵심 요약

| 구분          | 설명                                |
| ----------- | --------------------------------- |
| **역할**      | 서버나 앱의 상태를 실시간으로 확인하고 DNS 라우팅에 반영 |
| **공용 리소스**  | 직접 헬스체커 요청으로 확인                   |
| **사설 리소스**  | CloudWatch Alarm을 통해 간접 확인        |
| **자동 장애조치** | 비정상 서버로 트래픽이 안 가게 자동 전환           |
| **종류**      | 엔드포인트 / 계산 / CloudWatch 알람형       |

---

## 🪶 한 줄 요약

> **Route 53 Health Check = 내 서버를 24시간 진단해서,
> 죽은 서버로는 절대 트래픽을 보내지 않게 해주는 DNS 의사** 🩺

---

원하신다면 다음 단계로
👉 “Route 53 헬스체크 + 라우팅 정책(지연시간·가중치·Failover) 통합 동작 원리”
버전을 심화 설명드릴 수 있습니다.
바로 이어서 갈까요?



# Route 53 - Health Checks  
# Route 53 - 헬스체크  
👉 Route 53에서 공용 및 일부 사설 리소스를 모니터링하는 방법을 학습합니다.  

---

## Introduction to Route 53 Health Checks  
## Route 53 헬스체크 소개  
Health checks in Route 53 provide a mechanism to monitor the health of mainly public resources, although there is also a way to monitor private resources, which we will explore in this lecture.  
Route 53 헬스체크는 주로 공용 리소스 상태를 모니터링하는 기능을 제공하며, 사설 리소스 모니터링 방법도 이 강의에서 다룹니다.  

For example, consider two public load balancers located in different regions.  
예: 서로 다른 리전에 배치된 두 개의 공용 로드 밸런서를 고려합니다.  

Behind these load balancers, our application is running in both regions, forming a multi-region setup to ensure high availability at the regional level.  
이 로드 밸런서 뒤에는 두 리전 모두에 애플리케이션이 실행되어 리전 단위 고가용성 환경을 구성합니다.  

We use Route 53 to create DNS records so that when users access our URL, such as mydomain.com, they are directed to the closest load balancer.  
Route 53을 사용하여 DNS 레코드를 생성하고, 사용자가 `mydomain.com`에 접속할 때 가장 가까운 로드 밸런서로 연결되도록 합니다.  

This is typically implemented using a latency-based routing policy.  
보통 지연 시간 기반 라우팅 정책을 사용하여 구현합니다.  

However, if one region becomes unavailable, we want to ensure users are not routed to that region.  
하지만 특정 리전이 비활성화되면 사용자가 해당 리전으로 연결되지 않도록 해야 합니다.  

To achieve this, we create health checks in Route 53 for each region, such as one for us-east-1 and another for eu-west-1.  
이를 위해 각 리전에 대해 Route 53 헬스체크를 생성합니다. (예: us-east-1, eu-west-1)  

These health checks are associated with the corresponding Route 53 DNS records to enable automated DNS failover, ensuring traffic is only routed to healthy endpoints.  
이 헬스체크들은 해당 DNS 레코드와 연결되어 자동 DNS 장애 조치를 가능하게 하고, 트래픽이 건강한 엔드포인트로만 전달되도록 합니다.  

---

## Types of Health Checks  
## 헬스체크 유형  
There are three types of health checks available in Route 53:  
Route 53에는 3가지 헬스체크 유형이 있습니다:  

1. **Endpoint Health Checks**: Monitor a public endpoint such as an application, server, or AWS resource.  
   **엔드포인트 헬스체크**: 애플리케이션, 서버, AWS 리소스 등 공용 엔드포인트 모니터링.  
2. **Calculated Health Checks**: Monitor other health checks and combine their results.  
   **계산 헬스체크**: 다른 헬스체크 결과를 조합하여 모니터링.  
3. **CloudWatch Alarm Health Checks**: Monitor CloudWatch Alarms, useful for private resources.  
   **CloudWatch 알람 헬스체크**: CloudWatch 알람 모니터링, 사설 리소스 모니터링에 유용.  

Each health check produces its own metric, which can be viewed in CloudWatch metrics for monitoring and alerting purposes.  
각 헬스체크는 자체 메트릭을 생성하며, CloudWatch에서 모니터링 및 알람 확인 가능.  

---

## How Endpoint Health Checks Work  
## 엔드포인트 헬스체크 작동 방식  
Consider a health check monitoring an Application Load Balancer (ALB) in the eu-west-1 region.  
eu-west-1 리전의 ALB를 모니터링하는 헬스체크를 고려합니다.  

AWS health checkers, approximately 15 in number, are distributed globally and send requests to the public endpoint.  
전 세계에 약 15개의 AWS 헬스체커가 분포하며, 공용 엔드포인트로 요청을 보냅니다.  

If the endpoint responds with a 200 OK status code or another code defined in the health check configuration, the resource is considered healthy.  
엔드포인트가 200 OK 또는 헬스체크 설정에 정의된 코드로 응답하면 리소스가 정상으로 간주됩니다.  

The health check configuration allows setting thresholds for healthy or unhealthy status, as well as intervals for checks.  
헬스체크 설정에서는 정상/비정상 임계값과 체크 주기를 설정할 수 있습니다.  

There are two interval options:  
체크 주기는 두 가지 옵션이 있습니다:  

- Regular health checks every 30 seconds.  
  일반 헬스체크: 30초마다  
- Fast health checks every 10 seconds, which incur higher costs.  
  빠른 헬스체크: 10초마다 (비용 증가)  

Supported protocols include HTTP, HTTPS, and TCP.  
지원 프로토콜: HTTP, HTTPS, TCP  

The health check is considered healthy if more than 18 of the global health checkers report the endpoint as healthy; otherwise, it is deemed unhealthy.  
전 세계 헬스체커 중 18개 이상이 정상으로 보고하면 정상, 아니면 비정상으로 간주.  

You can select which geographic locations to use for the health checks.  
헬스체크를 수행할 지리적 위치 선택 가능.  

The health check passes only if the response status code is in the 2xx or 3xx range from the load balancer.  
응답 상태 코드가 2xx 또는 3xx 범위일 때만 헬스체크 정상 통과.  

Additionally, health checks can inspect the first 5120 bytes of a text-based response to look for specific strings, providing more granular health verification.  
텍스트 기반 응답의 처음 5120바이트를 검사하여 특정 문자열 확인 → 세밀한 상태 검증 가능.  

From a network perspective, it is essential that the Route 53 health checkers can access your Application Load Balancer or other endpoints.  
네트워크 관점: Route 53 헬스체커가 ALB 등 엔드포인트에 접근 가능해야 함.  

Therefore, you must allow incoming requests from the Route 53 health checkers' IP address ranges, which are publicly documented.  
따라서 공개된 Route 53 헬스체커 IP 범위에서의 인바운드 요청 허용 필요.  

---

## Calculated Health Checks  
## 계산 헬스체크  
Calculated health checks combine the results of multiple child health checks into a single parent health check.  
계산 헬스체크: 여러 자식 헬스체크 결과를 하나의 부모 헬스체크로 결합.  

For example, if you have three EC2 instances, you can create three child health checks, each monitoring one instance.  
예: EC2 인스턴스 3개 → 각 인스턴스별 자식 헬스체크 3개 생성.  

The parent health check aggregates these child health checks using logical conditions such as OR, AND, or NOT.  
부모 헬스체크는 OR, AND, NOT 등의 논리 조건으로 자식 헬스체크 결과를 통합.  

You can monitor up to 256 child health checks and specify how many must pass for the parent to be considered healthy.  
최대 256개 자식 헬스체크 모니터링 가능, 부모 정상 판단 조건 지정 가능.  

A common use case is to create a parent health check to perform maintenance on your website without causing all health checks to fail simultaneously.  
웹사이트 유지보수 시 모든 헬스체크가 동시에 실패하지 않도록 부모 헬스체크 생성이 일반적인 활용 사례.  

---

## Monitoring Private Resources  
## 사설 리소스 모니터링  
Monitoring private resources is challenging because Route 53 health checkers operate from the public internet and cannot access private endpoints within a VPC or on-premises environment.  
사설 리소스 모니터링은 어려움: Route 53 헬스체커는 공용 인터넷에서 작동 → VPC 또는 온프레미스 사설 엔드포인트 접근 불가.  

To monitor private resources, you create a CloudWatch Metric that tracks the health of the resource, such as an EC2 instance in a private subnet.  
사설 리소스 모니터링 방법: CloudWatch Metric 생성 → 사설 서브넷 EC2 인스턴스 상태 추적.  

Then, you configure a CloudWatch Alarm on this metric.  
이 Metric에 CloudWatch 알람 설정.  

This CloudWatch Alarm is then associated with a Route 53 health check.  
CloudWatch 알람을 Route 53 헬스체크와 연동.  

When the alarm enters the alarm state, the health check is marked unhealthy, effectively monitoring the private resource's health through CloudWatch integration.  
알람 상태 → 헬스체크 비정상 표시 → CloudWatch 통합을 통한 사설 리소스 모니터링.  

---

## Conclusion  
## 결론  
This concludes the lecture on Route 53 health checks.  
Route 53 헬스체크 강의 종료.  

We covered how to monitor public endpoints, combine health checks, and monitor private resources using CloudWatch Alarms integrated with Route 53 health checks.  
공용 엔드포인트 모니터링, 헬스체크 결합, CloudWatch 알람을 통한 사설 리소스 모니터링 학습 완료.  

---

## Key Takeaways  

핵심 포인트
Route 53 health checks monitor the health of public and private resources to enable automated DNS failover.
Route 53 헬스체크: 공용/사설 리소스 모니터링 → 자동 DNS 장애 조치 지원.

There are three types of health checks: endpoint health checks, calculated health checks, and CloudWatch Alarm-based health checks.
헬스체크 유형: 엔드포인트, 계산, CloudWatch 알람 기반.

Endpoint health checks use global AWS health checkers to verify resource availability via HTTP, HTTPS, or TCP protocols.
엔드포인트 헬스체크: 글로벌 AWS 헬스체커 → HTTP/HTTPS/TCP로 리소스 가용성 확인.

Private resource health monitoring is achieved by integrating CloudWatch Metrics and Alarms with Route 53 health checks.
사설 리소스 모니터링: CloudWatch Metric/Alarm + Route 53 헬스체크 통합.

---

💡 **게임 보상:**  
- 🏥 헬스체크 개념 이해 = +50 EXP  
- 🌐 엔드포인트 & 사설 리소스 모니터링 = +50 EXP  
- ⚙️ 계산 헬스체크 활용법 학습 = +100 EXP  
**총 보상: 200 EXP + Route 53 Health Master 뱃지 🏅**

---
