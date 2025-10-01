# AWS Global Accelerator - Hands On  
# AWS 글로벌 액셀러레이터 - 실습  

---

## Introduction to AWS Global Accelerator Hands-On  
## AWS 글로벌 액셀러레이터 실습 소개  

In this hands-on session, we will explore AWS Global Accelerator.  
이번 실습 세션에서는 AWS 글로벌 액셀러레이터를 직접 탐험합니다.  
> 실습을 통해 기능 이해와 구성 경험 획득.  

Please note that this hands-on exercise is not free.  
이 실습은 무료가 아님을 유의하세요.  
> 사용 시 소액 요금 발생 가능.  

If you prefer not to incur any charges, you should avoid using the service.  
비용을 원치 않는 경우 서비스 사용을 피하세요.  

However, if you are willing to spend a few cents, you can proceed with me to create and configure a Global Accelerator.  
몇 센트 정도의 비용을 감수할 경우, 저와 함께 Global Accelerator를 생성하고 구성할 수 있습니다.  

No matter which AWS region you select, for example Frankfurt, when you log into AWS Global Accelerator, you will be automatically redirected to the US West (Oregon) region.  
선택한 AWS 리전에 관계없이, 예를 들어 프랑크푸르트를 선택해도 AWS Global Accelerator에 로그인하면 자동으로 US West(오리건) 리전으로 리디렉션됩니다.  
> Global Accelerator는 글로벌 서비스이며 중앙 집중형으로 관리됩니다.  

This is because Global Accelerator is a global service, and its configuration is centralized in a single region.  
Global Accelerator는 글로벌 서비스이며 구성은 단일 리전에서 중앙 관리됩니다.  

---

## Preparing EC2 Instances for Global Accelerator  
## Global Accelerator용 EC2 인스턴스 준비  

Before creating a Global Accelerator, we need to set up our application endpoints.  
Global Accelerator를 생성하기 전에 애플리케이션 엔드포인트를 설정해야 합니다.  

Let's start by launching EC2 instances in different regions.  
먼저 여러 리전에 EC2 인스턴스를 시작합니다.  

---

### Launching an EC2 Instance in US East (N. Virginia)  
### 미국 동부(버지니아 북부) EC2 인스턴스 시작  

Navigate to the EC2 service.  
EC2 서비스로 이동합니다.  

Select the US East (N. Virginia) region.  
미국 동부(버지니아 북부) 리전을 선택합니다.  

Launch an Amazon Linux 2 AMI instance of type t2.micro.  
t2.micro 타입의 Amazon Linux 2 AMI 인스턴스를 시작합니다.  

Configure instance details to launch one instance.  
한 개의 인스턴스를 시작하도록 세부 설정을 구성합니다.  

Add user data to serve a simple HTTP response indicating the region, for example, "Hello from host name in US East 1".  
간단한 HTTP 응답을 제공하는 유저 데이터를 추가하여 리전을 표시합니다. 예: "Hello from host name in US East 1".  

Configure storage and tags as needed.  
필요에 따라 스토리지와 태그를 구성합니다.  

Create a new security group allowing HTTP traffic from anywhere (port 80, TCP).  
어디서든 HTTP 트래픽을 허용하는 새 보안 그룹 생성 (포트 80, TCP).  

Name the security group "Global Accelerator Demo".  
보안 그룹 이름을 "Global Accelerator Demo"로 설정합니다.  

Proceed without selecting a key pair since SSH access is not required.  
SSH 접속이 필요 없으므로 키 페어 선택 없이 진행합니다.  

Launch the instance.  
인스턴스를 시작합니다.  

---

### Launching an EC2 Instance in Asia Pacific (Mumbai)  
### 아시아 태평양(뭄바이) EC2 인스턴스 시작  

Switch to the Asia Pacific (Mumbai) region (ap-south-1).  
아시아 태평양(뭄바이) 리전(ap-south-1)으로 전환합니다.  

Repeat the same steps as for US East 1:  
US East 1과 동일한 단계를 반복합니다.  

- Launch a t2.micro Amazon Linux 2 AMI instance.  
- t2.micro Amazon Linux 2 AMI 인스턴스를 시작합니다.  

- Add user data with a message like "Hello from AP South 1".  
- "Hello from AP South 1" 메시지를 포함한 유저 데이터를 추가합니다.  

- Create a security group named "Global Accelerator Demo" allowing HTTP traffic from anywhere.  
- 어디서든 HTTP 트래픽 허용 보안 그룹 "Global Accelerator Demo" 생성.  

- Proceed without a key pair.  
- 키 페어 없이 진행합니다.  

- Launch the instance.  
- 인스턴스를 시작합니다.  

Once both instances are running, you can verify their HTTP responses by opening their public DNS or IP addresses in a browser.  
두 인스턴스가 실행되면, 브라우저에서 퍼블릭 DNS 또는 IP로 HTTP 응답을 확인할 수 있습니다.  

You should see the respective "Hello from" messages indicating the region of each instance.  
각 인스턴스의 리전을 표시하는 "Hello from" 메시지를 확인할 수 있습니다.  

---

## Creating the AWS Global Accelerator  
## AWS 글로벌 액셀러레이터 생성  

Navigate to the Global Accelerator service in the AWS Management Console.  
AWS 관리 콘솔에서 Global Accelerator 서비스로 이동합니다.  

Click on "Create Accelerator".  
"Create Accelerator"를 클릭합니다.  

Provide a name for the accelerator, for example, "My First Accelerator".  
액셀러레이터 이름을 지정합니다. 예: "My First Accelerator".  

Click "Next" to configure the listener.  
"Next"를 클릭하여 리스너를 구성합니다.  

---

## Configuring the Listener  
## 리스너 구성  

Set the listener port to 80.  
리스너 포트를 80으로 설정합니다.  

Choose TCP as the protocol since HTTP traffic runs over TCP.  
HTTP 트래픽은 TCP를 사용하므로 프로토콜을 TCP로 선택합니다.  

Optionally, enable client affinity to maintain session stickiness by source IP.  
선택적으로 클라이언트 IP 기반 세션 스티키니스를 위해 Client Affinity를 활성화합니다.  

Click "Next" to configure endpoint groups.  
"Next"를 클릭하여 엔드포인트 그룹을 구성합니다.  

---

## Adding Endpoint Groups  
## 엔드포인트 그룹 추가  

Add an endpoint group for the US East (N. Virginia) region.  
미국 동부(버지니아 북부) 리전에 엔드포인트 그룹 추가.  

Set the traffic dial to 100 (full traffic).  
트래픽 다이얼을 100으로 설정(전체 트래픽).  

Configure health checks on port 80 using TCP protocol.  
포트 80 TCP로 헬스체크 구성.  

Set the health check interval to 10 seconds and threshold count to 3.  
헬스체크 간격 10초, 임계값 3으로 설정.  

Add another endpoint group for the Asia Pacific (Mumbai) region.  
아시아 태평양(뭄바이) 리전에 엔드포인트 그룹 추가.  

Set the traffic dial to 100.  
트래픽 다이얼을 100으로 설정.  

Configure health checks on HTTP protocol with path "/".  
HTTP 프로토콜, 경로 "/"로 헬스체크 구성.  

Set the health check interval to 30 seconds and threshold count to 3.  
헬스체크 간격 30초, 임계값 3으로 설정.  

---

## Adding Endpoints to Endpoint Groups  
## 엔드포인트 그룹에 엔드포인트 추가  

For each endpoint group, add the corresponding EC2 instance as an endpoint.  
각 엔드포인트 그룹에 해당 EC2 인스턴스를 엔드포인트로 추가합니다.  

Assign weights to control traffic distribution if desired.  
원하면 트래픽 분배를 위해 가중치를 할당합니다.  

After adding endpoints, click "Create Accelerator".  
엔드포인트 추가 후 "Create Accelerator" 클릭.  

The accelerator will be created with two static anycast IP addresses and an associated DNS name.  
액셀러레이터가 두 개의 고정 애니캐스트 IP와 연결된 DNS 이름과 함께 생성됩니다.  

The status will initially show as "Deploying".  
상태는 처음에 "Deploying"으로 표시됩니다.  

---

## Monitoring Accelerator Health  
## 액셀러레이터 헬스 모니터링  

After a few minutes, the health checks will update the status of each endpoint.  
몇 분 후, 헬스체크가 각 엔드포인트 상태를 업데이트합니다.  

Healthy endpoints will be marked as "Healthy".  
정상 엔드포인트는 "Healthy"로 표시됩니다.  

Unhealthy endpoints will be marked as "Unhealthy".  
비정상 엔드포인트는 "Unhealthy"로 표시됩니다.  

This health status determines how traffic is routed by the Global Accelerator.  
헬스 상태에 따라 Global Accelerator가 트래픽 라우팅 방식을 결정합니다.  

---

## Testing Global Accelerator Routing  
## 글로벌 액셀러레이터 라우팅 테스트  

Access the Global Accelerator's DNS name or static IP addresses from different locations.  
다양한 위치에서 글로벌 액셀러레이터의 DNS 이름 또는 고정 IP에 접속합니다.  

Traffic will be routed to the closest healthy endpoint based on latency.  
트래픽은 지연 시간을 기준으로 가장 가까운 정상 엔드포인트로 라우팅됩니다.  

For example, from Europe, traffic may route to the US East 1 instance.  
예: 유럽에서 트래픽은 US East 1 인스턴스로 라우팅될 수 있습니다.  

From locations closer to Mumbai, traffic will route to the Mumbai instance.  
뭄바이에 가까운 위치에서는 트래픽이 뭄바이 인스턴스로 라우팅됩니다.  

You can simulate this by using a VPN to change your apparent location and refreshing the page to observe the response region.  
VPN을 사용해 위치를 변경하고 페이지를 새로고침하여 응답 지역을 확인하며 시뮬레이션 가능합니다.  

---

## Testing Health Check Failover  
## 헬스체크 장애 조치 테스트  

To test failover, modify the security group of an endpoint to block health check traffic.  
장애 조치를 테스트하려면 엔드포인트 보안 그룹을 수정하여 헬스체크 트래픽을 차단합니다.  

For example, remove the HTTP inbound rule from the Mumbai instance's security group.  
예: 뭄바이 인스턴스 보안 그룹에서 HTTP 인바운드 규칙 제거.  

The health check will fail, and the endpoint will be marked "Unhealthy".  
헬스체크가 실패하고 엔드포인트는 "Unhealthy"로 표시됩니다.  

Traffic will automatically be routed to the other healthy endpoint, such as US East 1.  
트래픽은 자동으로 다른 정상 엔드포인트(예: US East 1)로 라우팅됩니다.  

This demonstrates the Global Accelerator's ability to route traffic away from unhealthy endpoints.  
이로써 Global Accelerator가 비정상 엔드포인트를 회피해 트래픽을 라우팅하는 기능을 확인할 수 있습니다.  

---

## Cleaning Up Resources  
## 리소스 정리  

To avoid incurring charges, terminate both EC2 instances in US East 1 and Mumbai regions.  
비용 발생 방지를 위해 US East 1과 뭄바이 리전의 EC2 인스턴스를 종료합니다.  

Disconnect any VPN connections to reduce latency.  
지연 시간을 줄이기 위해 VPN 연결을 해제합니다.  

Disable and delete the Global Accelerator from the AWS Management Console.  
AWS 관리 콘솔에서 글로벌 액셀러레이터를 비활성화 후 삭제합니다.  

Deleting the accelerator requires first disabling it, then confirming deletion by typing "delete".  
액셀러레이터 삭제는 먼저 비활성화 후 "delete" 입력으로 삭제 확인이 필요합니다.  

---

## AWS Global Accelerator Pricing

Overview

## AWS 글로벌 액셀러레이터 요금 개요

There is a fixed hourly fee for each accelerator running in your account, approximately $0.025 per hour.
계정 내 각 액셀러레이터 실행 시 시간당 약 $0.025의 고정 요금이 있습니다.

Data transfer fees vary by region and destination, ranging from $0.01 to $0.08 per gigabyte.
데이터 전송 요금은 리전과 목적지에 따라 다르며, GB당 $0.01~$0.08 범위입니다.

For example, data transfer in Australia costs about $0.08 per gigabyte.
예: 호주 내 데이터 전송 비용은 GB당 약 $0.08입니다.

Global Accelerator is a premium service with associated costs but provides significant benefits for global application performance and availability.
Global Accelerator는 비용이 발생하는 프리미엄 서비스이지만, 글로벌 애플리케이션 성능과 가용성에 큰 이점을 제공합니다.

---

## Conclusion

## 결론

In this hands-on session, we successfully created and tested an AWS Global Accelerator with EC2 instances in multiple regions.
이번 실습에서는 여러 리전 EC2 인스턴스를 활용해 AWS 글로벌 액셀러레이터를 생성하고 테스트했습니다.

We observed how Global Accelerator routes traffic based on endpoint health and client location.
엔드포인트 헬스와 클라이언트 위치 기반으로 트래픽이 라우팅되는 것을 확인했습니다.

Finally, we cleaned up all resources to avoid unnecessary charges.
마지막으로 불필요한 비용을 방지하기 위해 모든 리소스를 정리했습니다.

Thank you for following along, and I will see you in the next lecture.
참여해주셔서 감사합니다. 다음 강의에서 뵙겠습니다.

---

## Key Takeaways

## 핵심 요약

* AWS Global Accelerator provides static anycast IP addresses to improve application availability and performance globally.

* 글로벌 액셀러레이터는 고정 애니캐스트 IP를 제공하여 글로벌 애플리케이션 가용성과 성능을 개선합니다.

* Global Accelerator configurations are managed in a single global region regardless of the user's selected region.

* 글로벌 액셀러레이터 구성은 사용자가 선택한 리전에 관계없이 단일 글로벌 리전에서 관리됩니다.

* Health checks monitor endpoint availability, automatically routing traffic away from unhealthy endpoints.

* 헬스체크는 엔드포인트 상태를 모니터링하며, 비정상 엔드포인트를 회피해 트래픽을 자동으로 라우팅합니다.

* Proper cleanup of resources, including EC2 instances and accelerators, is essential to avoid unnecessary charges.

* EC2 인스턴스와 액셀러레이터를 포함한 리소스 정리가 비용 발생 방지를 위해 필수적입니다.

🎮 **게임보상:**  
- AWS Global Accelerator Hands-On 실습 완료 +20 XP  
- 엔드포인트 그룹과 헬스체크 이해 +15 XP  
- Failover 기능 및 라우팅 이해 +15 XP  
- 리소스 정리 및 비용 관리 이해 +10 XP  
총 **60 XP 획득!** 🎉
