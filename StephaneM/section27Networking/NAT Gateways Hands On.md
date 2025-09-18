```markdown
# NAT Gateways Hands On  
# NAT 게이트웨이 실습  

🎮 게임보상: "Gateway Engineer" +400 XP  

---

## Introduction to NAT Gateway Setup  
## NAT 게이트웨이 설정 소개  

When NAT instances are stopped or terminated, internet access is lost.  
NAT 인스턴스가 중지되거나 종료되면 인터넷 접근이 불가능해집니다.  

For example, attempting to use curl to access external sites will fail.  
예를 들어, curl 명령으로 외부 사이트에 접속하려고 하면 실패합니다.  

To resolve this, we will set up a NAT Gateway.  
이를 해결하기 위해 NAT 게이트웨이를 설정할 것입니다.  

---

## Observing the Private Route Table  
## 프라이빗 라우트 테이블 관찰  

Refreshing the private route table reveals that the destination targeting the Elastic Network Interface (ENI) is a black hole.  
프라이빗 라우트 테이블을 새로 고침하면 Elastic Network Interface(ENI)를 대상으로 하는 경로가 블랙홀임을 확인할 수 있습니다.  

A black hole indicates that the route is inactive because the NAT instance has been stopped, so the route leads nowhere.  
블랙홀은 NAT 인스턴스가 중지되어 경로가 비활성화되었음을 의미하며, 트래픽이 어디로도 전달되지 않습니다.  

This highlights the advantage of using managed services like NAT Gateways over NAT instances.  
이는 NAT 게이트웨이와 같은 관리형 서비스를 NAT 인스턴스 대신 사용하는 장점을 보여줍니다.  

---

## Creating a NAT Gateway  
## NAT 게이트웨이 생성  

We will create a NAT Gateway named DemoNATGW.  
DemoNATGW라는 이름으로 NAT 게이트웨이를 생성합니다.  

When selecting a subnet for the NAT Gateway, it should be in a public subnet.  
NAT 게이트웨이에 서브넷을 선택할 때, 퍼블릭 서브넷이어야 합니다.  

For high availability, multiple subnets across availability zones are recommended, but we will start with one: PublicSubnetA.  
고가용성을 위해 여러 가용 영역의 서브넷을 추천하지만, 우선 하나의 퍼블릭 서브넷(PublicSubnetA)으로 시작합니다.  

The connectivity type is set to public.  
연결 유형은 퍼블릭으로 설정됩니다.  

Next, allocate an Elastic IP address to the NAT Gateway.  
다음으로 NAT 게이트웨이에 Elastic IP 주소를 할당합니다.  

Once the Elastic IP is allocated, proceed to create the NAT Gateway.  
Elastic IP를 할당한 후, NAT 게이트웨이를 생성합니다.  

The NAT Gateway creation process begins and may take some time to become active.  
NAT 게이트웨이 생성 과정이 시작되며, 활성 상태가 되기까지 시간이 걸릴 수 있습니다.  

---

## Updating the Private Route Table  
## 프라이빗 라우트 테이블 업데이트  

While the NAT Gateway is being created, edit the private route table.  
NAT 게이트웨이가 생성되는 동안 프라이빗 라우트 테이블을 편집합니다.  

Remove the black hole route that previously directed internet traffic to the stopped NAT instance.  
이전에 중지된 NAT 인스턴스로 인터넷 트래픽을 보내던 블랙홀 경로를 제거합니다.  

Instead, add a route that directs internet-bound traffic to the newly created NAT Gateway DemoNATGW.  
대신 새로 생성한 NAT 게이트웨이 DemoNATGW로 인터넷 트래픽을 보내는 경로를 추가합니다.  

Save the changes to activate the new route.  
변경 사항을 저장하여 새 경로를 활성화합니다.  

The NAT Gateway may take a few moments to become active.  
NAT 게이트웨이가 활성 상태가 되기까지 잠시 시간이 걸릴 수 있습니다.  

Once its state changes to active, the private subnet instances can send traffic through it to access the internet.  
상태가 활성으로 바뀌면, 프라이빗 서브넷의 인스턴스가 NAT 게이트웨이를 통해 인터넷에 접근할 수 있습니다.  

---

## Verifying Internet Connectivity  
## 인터넷 연결 확인  

After the NAT Gateway is active, verify internet connectivity from an instance in the private subnet.  
NAT 게이트웨이가 활성화된 후, 프라이빗 서브넷 인스턴스에서 인터넷 연결을 확인합니다.  

For example, running curl google.com or ping google.com should succeed, confirming that the NAT Gateway is functioning correctly.  
예를 들어 curl google.com이나 ping google.com 명령을 실행하면 성공하며, NAT 게이트웨이가 정상적으로 작동함을 확인할 수 있습니다.  

This setup does not require specifying security group rules for the NAT Gateway or making the instance public.  
이 구성에서는 NAT 게이트웨이에 대한 보안 그룹 규칙을 지정하거나 인스턴스를 퍼블릭으로 만들 필요가 없습니다.  

This configuration allows instances in private subnets to access the internet for tasks such as updating the operating system using commands like sudo yum update, without exposing the instances publicly.  
이 구성은 프라이빗 서브넷 인스턴스가 퍼블릭 노출 없이 sudo yum update와 같은 OS 업데이트 작업을 위해 인터넷에 접근할 수 있도록 합니다.  

---

## High Availability Considerations  
## 고가용성 고려사항  

Currently, we have created one NAT Gateway in a single availability zone.  
현재 한 가용 영역에 NAT 게이트웨이 하나를 생성했습니다.  

For high availability, it is recommended to create additional NAT Gateways in other availability zones and update the route tables accordingly.  
고가용성을 위해 다른 가용 영역에 추가 NAT 게이트웨이를 생성하고 라우트 테이블을 업데이트하는 것이 권장됩니다.  

This setup ensures resilience against failures affecting an entire availability zone.  
이 구성은 전체 가용 영역에 영향을 미치는 장애에 대비한 내결함성을 보장합니다.  

---

## Conclusion  
## 결론  

In this lecture, we created a NAT Gateway to replace a stopped NAT instance, updated the private route table to direct traffic through the NAT Gateway, and verified internet connectivity from a private subnet instance.  
이번 강의에서는 중지된 NAT 인스턴스를 대체할 NAT 게이트웨이를 생성하고, 프라이빗 라우트 테이블을 업데이트하여 트래픽이 NAT 게이트웨이를 통해 전달되도록 설정하며, 프라이빗 서브넷 인스턴스에서 인터넷 연결을 확인했습니다.  

This approach improves reliability and security by using managed services and avoiding public exposure of instances.  
이 접근 방식은 관리형 서비스를 사용하고 인스턴스를 퍼블릭에 노출하지 않음으로써 신뢰성과 보안을 향상시킵니다.  

---

## Key Takeaways  
## 핵심 요약  

- NAT instances can become black holes when stopped, causing loss of internet access.  
- NAT 인스턴스는 중지될 경우 블랙홀이 되어 인터넷 접근이 불가능해질 수 있습니다.  

- NAT Gateways provide a managed, highly available solution for internet access from private subnets.  
- NAT 게이트웨이는 프라이빗 서브넷의 인터넷 접근을 위해 관리형, 고가용성 솔루션을 제공합니다.  

- Creating a NAT Gateway involves selecting a public subnet and allocating an Elastic IP.  
- NAT 게이트웨이를 생성하려면 퍼블릭 서브넷을 선택하고 Elastic IP를 할당해야 합니다.  

- Updating the private route table to direct internet traffic to the NAT Gateway restores connectivity without exposing instances publicly.  
- 프라이빗 라우트 테이블을 업데이트하여 인터넷 트래픽을 NAT 게이트웨이로 전달하면, 인스턴스를 퍼블릭에 노출하지 않고도 연결성을 복원할 수 있습니다.  
```

