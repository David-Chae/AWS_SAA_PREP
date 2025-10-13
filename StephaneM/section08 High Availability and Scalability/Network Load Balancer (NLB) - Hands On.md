# Network Load Balancer (NLB) - Hands On  
# 네트워크 로드 밸런서(NLB) - 실습  
→ 이번에는 네트워크 로드 밸런서를 직접 만들어보는 실습을 진행합니다.  

---

## Creating a Network Load Balancer  
## 네트워크 로드 밸런서 생성하기  
→ 로드 밸런서를 만드는 단계에 들어갑니다.  

Let's proceed to create a Network Load Balancer (NLB). We will name this load balancer DemoNLB. It will be an internet-facing load balancer using IPv4 addressing.  
네트워크 로드 밸런서(NLB)를 만들겠습니다. 이름은 `DemoNLB`로 하고, 인터넷에 연결되는 IPv4 방식의 로드 밸런서로 설정합니다.  

For the network mapping, we will use the existing Virtual Private Cloud (VPC). We will select all three availability zones (AZs) available, each associated with a subnet. AWS assigns a fixed IPv4 address for each AZ enabled for the NLB. Alternatively, if you have Elastic IPs, you could assign one per availability zone.  
네트워크 매핑에서는 기존 VPC를 사용합니다. 사용 가능한 3개의 가용 영역(AZ)을 모두 선택하고, 각 영역에는 서브넷을 연결합니다. NLB는 각 AZ에 고정 IPv4 주소를 할당합니다. Elastic IP가 있다면 AZ마다 할당할 수도 있습니다.  

---

## Configuring Security Groups  
## 보안 그룹 설정  
→ 네트워크 보안을 위해 반드시 필요한 단계입니다.  

Next, we will attach a security group to our Network Load Balancer. This is a recommended practice. We will create a new security group named demo-sg-nlb. For inbound rules, we will allow HTTP traffic on port 80 from anywhere. Outbound rules will remain as default.  
NLB에 보안 그룹을 연결합니다. 이는 권장되는 방법입니다. `demo-sg-nlb`라는 새 보안 그룹을 만들고, 인바운드 규칙은 포트 80(HTTP)을 모든 위치에서 허용합니다. 아웃바운드 규칙은 기본값으로 둡니다.  

After creating the security group, we will refresh the list and select demo-sg-nlb, removing the default security group. Similar to Application Load Balancers, Network Load Balancers also use security groups to control traffic.  
보안 그룹을 만든 후 목록을 새로고침하여 `demo-sg-nlb`를 선택하고 기본 보안 그룹은 제거합니다. ALB와 마찬가지로 NLB도 트래픽 제어에 보안 그룹을 사용합니다.  

---

## Listener and Target Group Setup  
## 리스너 및 대상 그룹 설정  
→ 실제 트래픽을 받을 대상 인스턴스들을 묶는 과정입니다.  

For listeners and routing, we will use the TCP protocol on port 80. We need to create a target group for the NLB. This target group will be named demo-tg-nlb and will target instances using TCP on port 80 within the same VPC.  
리스너 및 라우팅은 TCP 프로토콜을 포트 80에서 사용합니다. 이를 위해 NLB용 대상 그룹을 만듭니다. 이름은 `demo-tg-nlb`이고, 동일 VPC 내에서 포트 80 TCP를 사용하는 인스턴스를 대상으로 합니다.  

For health checks, we have options including TCP, HTTP, or HTTPS. Since our EC2 instances run an HTTP application, we will use HTTP for health checks. The advanced health check settings are configured with a healthy threshold of 2, a timeout of 2 seconds, and an interval of 5 seconds.  
헬스 체크는 TCP, HTTP, HTTPS 중 선택할 수 있습니다. 여기서는 EC2가 HTTP 애플리케이션을 실행하므로 HTTP를 사용합니다. 고급 설정은 정상 임계값 2회, 타임아웃 2초, 간격 5초로 설정합니다.  

We will then register our two available EC2 instances as targets in the target group. After registration, the target group demo-tg-nlb is created and ready for use.  
두 개의 EC2 인스턴스를 대상 그룹에 등록합니다. 등록이 끝나면 `demo-tg-nlb` 그룹이 생성되어 사용 준비가 됩니다.  

---

## Finalizing Network Load Balancer Creation  
## 네트워크 로드 밸런서 생성 완료  
→ 모든 구성이 끝나면 실제로 동작을 확인하는 단계입니다.  

We navigate back to the Network Load Balancer page, refresh, and select the newly created target group demo-tg-nlb. After completing the configuration, we create the Network Load Balancer and switch to its details page to monitor provisioning.  
NLB 페이지로 돌아가 새로 만든 `demo-tg-nlb`를 선택합니다. 설정을 완료하고 로드 밸런서를 만든 뒤 세부 정보 페이지에서 프로비저닝 과정을 확인합니다.  

Once the Network Load Balancer is active, we test it by entering its URL in a web browser. Initially, it may not work because the target instances are still undergoing health checks and are marked as unhealthy.  
NLB가 활성화되면 웹 브라우저에서 URL을 입력해 테스트합니다. 처음에는 인스턴스들이 헬스 체크 중이라 비정상으로 표시되어 작동하지 않을 수 있습니다.  

---

## Troubleshooting Health Check Failures  
## 헬스 체크 실패 문제 해결  
→ 정상 작동을 위해 EC2 보안 그룹 설정을 점검해야 합니다.  

Checking the security groups of the EC2 instances reveals that HTTP traffic is allowed only from the Application Load Balancer's security group. To fix this, we must allow HTTP traffic from the Network Load Balancer's security group as well.  
EC2 인스턴스 보안 그룹을 확인하면 HTTP 트래픽이 ALB 보안 그룹에서만 허용되고 있습니다. 이를 해결하려면 NLB 보안 그룹에서도 허용해야 합니다.  

By adding a rule to allow HTTP traffic from the demo-sg-nlb security group, the Network Load Balancer can communicate with the EC2 instances, enabling successful health checks.  
`demo-sg-nlb` 보안 그룹에서 HTTP 트래픽을 허용하는 규칙을 추가하면, NLB가 EC2 인스턴스와 통신할 수 있어 헬스 체크가 성공합니다.  

After a short wait, the instances become healthy. Refreshing the Network Load Balancer URL now returns the "Hello World" response from one of the instances. Repeated refreshes show the IP address changing, confirming that load balancing is functioning across the two instances.  
잠시 후 인스턴스들이 정상 상태가 됩니다. NLB URL을 새로고침하면 인스턴스 중 하나에서 "Hello World" 응답을 반환합니다. 여러 번 새로고침하면 IP가 바뀌는 것을 확인할 수 있으며, 이는 로드 밸런싱이 작동하고 있음을 보여줍니다.  

---

## Summary and Cleanup  
## 요약 및 정리  
→ 실습 후에는 반드시 자원을 정리해야 비용이 발생하지 않습니다.  

We have seen how Network Load Balancer security groups work similarly to Application Load Balancers. It is important to adjust EC2 instance security groups to allow traffic from the NLB, not just the ALB.  
NLB 보안 그룹이 ALB와 유사하게 작동하는 것을 확인했습니다. EC2 보안 그룹은 ALB뿐 아니라 NLB 트래픽도 허용해야 합니다.  

To avoid incurring costs, it is recommended to delete the created resources after use. This includes the Network Load Balancer DemoNLB, the target group demo-tg-nlb, and optionally the security group demo-sg-nlb.  
불필요한 비용을 피하려면 사용 후 생성된 리소스를 삭제해야 합니다. 여기에는 `DemoNLB`, `demo-tg-nlb`, 필요 시 `demo-sg-nlb`가 포함됩니다.  

This concludes the hands-on session on creating and configuring a Network Load Balancer.  
이것으로 NLB 생성 및 설정 실습을 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  
→ 주요 학습 포인트를 정리합니다.  

- Created a Network Load Balancer (NLB) named DemoNLB with internet-facing IPv4 configuration.  
  인터넷 연결 가능한 IPv4 기반의 `DemoNLB`를 생성함.  

- Configured security groups to allow HTTP traffic on port 80 from anywhere and specifically allowed NLB traffic to EC2 instances.  
  보안 그룹에서 포트 80 HTTP 트래픽을 전 세계에 허용하고, NLB 트래픽도 EC2로 전달되도록 구성함.  

- Set up a target group for the NLB with TCP protocol on port 80 and HTTP health checks.  
  포트 80 TCP 기반의 대상 그룹을 만들고 HTTP 헬스 체크를 설정함.  

- Troubleshot health check failures by adjusting EC2 instance security group rules to accept traffic from the NLB.  
  EC2 보안 그룹을 수정하여 NLB 트래픽을 허용해 헬스 체크 실패 문제를 해결함.  

- Verified load balancing by observing changing IP addresses serving the "Hello World" response.  
  "Hello World" 응답 시 IP 주소가 바뀌는 것을 통해 로드 밸런싱 동작을 확인함.  

- Recommended deleting created resources after use to avoid unnecessary costs.  
  비용 절감을 위해 사용 후 리소스를 삭제할 것을 권장함.  

---

👉 게임 보상: 🏆 **“로드 밸런서 정복자” 칭호 획득!** 🎮
