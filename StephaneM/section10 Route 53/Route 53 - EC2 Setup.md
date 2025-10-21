# Route 53 - EC2 Setup  
# Route 53 - EC2 설정  

---

## Introduction  
## 소개  

Let's get started with setting up our AWS environment. Before using Route 53, we will create three EC2 instances in different regions, as well as one Application Load Balancer (ALB).  
AWS 환경 설정을 시작해봅시다. Route 53을 사용하기 전에, 서로 다른 리전에 EC2 인스턴스 3개와 하나의 애플리케이션 로드 밸런서(ALB)를 생성하겠습니다.  

---

## Launching EC2 Instances  
## EC2 인스턴스 실행  

First, in one of the regions, navigate to the EC2 instances section and launch a new instance. Select Amazon Linux 2 as the operating system and choose a T2 micro instance type. No key pair is needed since we will use EC2 Instance Connect if necessary. For network settings, create a security group that allows SSH and HTTP access from anywhere.  
먼저 한 리전에서 EC2 인스턴스 섹션으로 이동하여 새 인스턴스를 시작합니다. 운영체제로 Amazon Linux 2를 선택하고, 인스턴스 유형은 T2 micro를 선택합니다. 필요 시 EC2 Instance Connect를 사용할 것이므로 키 페어는 필요하지 않습니다. 네트워크 설정에서는 어디서든 SSH와 HTTP 접근을 허용하는 보안 그룹을 생성합니다.  

```
#!/bin/bash
# install httpd (Linux 3 version)
yum update -y
yum install -y httpd
systemctl start -y httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f) in AZ $EC2_AVAIL_ZONE </h1>" > /var/www/html/index.html
```

In the advanced details section, specify a bootstrap user data script. To do this, copy the entire script from your Route 53 user script and paste it here. This script will display "hello world" from the instance, along with the availability zone where the instance was launched, using the environment variable EC2_AVAILABILITY_ZONE. This provides additional information about the EC2 instance.  
고급 세부 정보 섹션에서 부트스트랩 사용자 데이터 스크립트를 지정합니다. Route 53 사용자 스크립트 전체를 복사해 붙여넣습니다. 이 스크립트는 인스턴스에서 "hello world"와 함께 EC2_AVAILABILITY_ZONE 환경 변수를 사용하여 해당 인스턴스가 실행된 가용 영역 정보를 표시합니다. 이렇게 하면 EC2 인스턴스의 추가 정보를 확인할 수 있습니다.  

Launch the instance. Once launched, it will appear in your instances list.  
인스턴스를 시작합니다. 실행되면 인스턴스 목록에 나타납니다.  

Repeat the process in another region, for example, Northern Virginia (US East 1). Launch an instance with the same settings: no key pair, HTTP allowed, and the same EC2 user data script in the advanced details. Launch the instance.  
이 과정을 다른 리전, 예를 들어 노던 버지니아(US East 1)에서도 반복합니다. 동일한 설정(키 페어 없음, HTTP 허용, 동일한 사용자 데이터 스크립트)으로 인스턴스를 시작합니다.  

Finally, launch a third instance in a different region, such as Singapore. Use the T2 micro instance type, no key pair, allow HTTP from anywhere, and paste the same user data script in advanced details. Launch the instance.  
마지막으로, 싱가포르 같은 또 다른 리전에 세 번째 인스턴스를 시작합니다. T2 micro 인스턴스 유형을 선택하고, 키 페어 없음, 어디서든 HTTP 허용, 동일한 사용자 데이터 스크립트를 고급 설정에 붙여넣고 시작합니다.  

Now, you have three EC2 instances running in three different regions: Frankfurt, Northern Virginia, and Singapore.  
이제 프랑크푸르트, 노던 버지니아, 싱가포르 세 리전에서 각각 EC2 인스턴스가 실행 중입니다.  

---

## Creating an Application Load Balancer (ALB)  
## 애플리케이션 로드 밸런서(ALB) 생성  

Next, create a load balancer in one of the regions, for example, Frankfurt. Choose to create an Application Load Balancer and provide a unique name, such as DemoRoute53ALB. Set it to be internet-facing and use IPv4.  
다음으로, 예를 들어 프랑크푸르트 리전에 로드 밸런서를 생성합니다. Application Load Balancer를 선택하고 DemoRoute53ALB 같은 고유한 이름을 지정합니다. 인터넷 연결 방식으로 설정하고 IPv4를 사용합니다.  

For subnet mapping, select three subnets. For the security group, select the one created earlier that allows SSH and HTTP access. This ensures HTTP is enabled for the load balancer. Set the listener protocol to HTTP on port 80, and forward traffic to a new target group based on instances. Name the target group demo-tg-route53.  
서브넷 매핑에서는 세 개의 서브넷을 선택합니다. 보안 그룹은 앞에서 만든 SSH와 HTTP를 허용하는 그룹을 선택합니다. 이렇게 하면 로드 밸런서가 HTTP를 사용할 수 있습니다. 리스너 프로토콜은 HTTP(포트 80)로 설정하고, 인스턴스를 기반으로 새로운 타겟 그룹으로 트래픽을 전달합니다. 타겟 그룹 이름은 demo-tg-route53으로 지정합니다.  

Register the EC2 instance you created earlier with this target group. It will initially show as pending. Review the targets to confirm one target is registered, then create the target group.  
앞에서 생성한 EC2 인스턴스를 이 타겟 그룹에 등록합니다. 처음에는 대기(pending) 상태로 표시됩니다. 대상 목록을 확인하여 하나의 인스턴스가 등록된 것을 확인한 뒤 타겟 그룹을 생성합니다.  

Refresh the load balancers list and select the newly created target group demo-tg-route53. Everything should look good. Proceed to create the load balancer and view its details once created.  
로드 밸런서 목록을 새로고침하고 demo-tg-route53 타겟 그룹을 선택합니다. 설정이 잘 되었는지 확인한 후 로드 밸런서를 생성하고, 생성이 완료되면 세부 정보를 확인합니다.  

---

## Verifying Instances and Load Balancer  
## 인스턴스와 로드 밸런서 검증  

To verify that everything is working properly, select one EC2 instance and copy its public IP address. Access the instance via HTTP using the IP address. You should see a message such as "hello world from AZ EU Central 1B," indicating the instance is running and the user data script executed correctly.  
모든 것이 제대로 작동하는지 확인하려면 하나의 EC2 인스턴스를 선택하고 퍼블릭 IP 주소를 복사합니다. 해당 IP로 HTTP 접속하면 "hello world from AZ EU Central 1B" 같은 메시지가 표시됩니다. 이는 인스턴스가 실행 중이며 사용자 데이터 스크립트가 정상 실행되었음을 의미합니다.  

Repeat this verification for the other two instances by copying their public IPs and accessing them via HTTP. The messages should indicate their respective availability zones, such as "hello from US East 1A" and "hello from AP Southeast 1B."  
다른 두 인스턴스도 동일하게 퍼블릭 IP를 복사해 HTTP로 접속합니다. "hello from US East 1A", "hello from AP Southeast 1B"와 같이 각자의 가용 영역이 표시됩니다.  

Finally, check the Application Load Balancer's DNS name to confirm it has been provisioned. Refresh the page if necessary. The ALB should be accessible and display the message from the registered EC2 instance, confirming the setup is complete.  
마지막으로, 애플리케이션 로드 밸런서의 DNS 이름을 확인하여 프로비저닝 되었는지 확인합니다. 필요하면 페이지를 새로고침합니다. ALB가 정상적으로 접속 가능하고 등록된 EC2 인스턴스의 메시지를 표시하면 설정이 완료된 것입니다.  

---

## Summary  
## 요약  

All three EC2 instances and the Application Load Balancer have been properly set up and are functioning as expected. Keep this information handy for future reference.  
세 개의 EC2 인스턴스와 애플리케이션 로드 밸런서가 정상적으로 설정되었고 기대한 대로 작동합니다. 향후 참고를 위해 이 정보를 잘 보관하세요.  

---

## Key Takeaways  
## 핵심 정리  

- Launched three EC2 instances in different AWS regions with Amazon Linux 2 and T2 micro instance type.  
- Amazon Linux 2와 T2 micro 인스턴스 유형으로 AWS의 서로 다른 리전에 EC2 인스턴스 3개를 실행했습니다.  

- Configured security groups to allow SSH and HTTP access from anywhere.  
- 보안 그룹을 설정해 어디서든 SSH와 HTTP 접근을 허용했습니다.  

- Used a bootstrap user data script to display instance-specific information including availability zone.  
- 사용자 데이터 스크립트를 사용해 인스턴스 가용 영역 정보를 포함한 메시지를 표시했습니다.  

- Created an Application Load Balancer (ALB) in Frankfurt, configured with a target group including one EC2 instance.  
- 프랑크푸르트 리전에 ALB를 생성하고 EC2 인스턴스를 포함한 타겟 그룹으로 구성했습니다.  

- Verified instances and ALB by accessing their public IPs and DNS names, confirming correct setup and connectivity.  
- 퍼블릭 IP와 ALB DNS 이름으로 인스턴스와 로드 밸런서를 검증해 설정 및 연결을 확인했습니다.  

---

🎮 **게임 보상 지급**  
- 경험치: **+350XP**  
- 아이템: **"ALB Guardian Shield" 🛡️**  
- 업적 달성: **"Multi-Region EC2 Master"** 🌍  


👉 이 문서는 EC2 인스턴스 3개와 ALB를 다중 리전에 배포하고 검증하는 과정을 단계별로 설명했습니다.

원하시면 제가 이 과정을 **Route 53 레코드와 연계**해서 실제로 ALB와 글로벌 DNS 라우팅을 연결하는 부분까지 확장해드릴까요?
