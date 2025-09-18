```markdown
# NAT Gateways  
# NAT 게이트웨이  

🎮 게임보상: "Gateway Architect" +350 XP  

---

## Introduction to NAT Gateways  
## NAT 게이트웨이 소개  

So now that we have talked about NAT instances, let's look at NAT Gateways.  
이제 NAT 인스턴스에 대해 이야기했으므로 NAT 게이트웨이를 살펴보겠습니다.  

NAT Gateways are much better. They are managed instances that are always running and have higher bandwidth.  
NAT 게이트웨이는 훨씬 더 우수합니다. 항상 실행 중인 관리형 인스턴스이며, 대역폭이 더 높습니다.  

They offer high availability and require no administration.  
높은 가용성을 제공하며 관리가 필요 없습니다.  

You pay per hour of usage and bandwidth for the NAT Gateway.  
NAT 게이트웨이는 사용 시간과 대역폭에 따라 요금이 부과됩니다.  

The NAT Gateway is created in a specific Availability Zone (AZ) and inherits an Elastic IP address.  
NAT 게이트웨이는 특정 가용 영역(AZ)에 생성되며 Elastic IP 주소를 할당받습니다.  

It cannot be used with an instance within the same subnet.  
동일 서브넷 내의 인스턴스와는 함께 사용할 수 없습니다.  

Therefore, the NAT Gateway can only be helpful if accessed from another subnet.  
따라서 다른 서브넷에서 접근할 때만 유용합니다.  

We create a NAT Gateway in a public subnet and connect it to instances in private subnets.  
퍼블릭 서브넷에 NAT 게이트웨이를 생성하고 이를 프라이빗 서브넷의 인스턴스와 연결합니다.  

The routing works such that traffic goes from the private subnets to the NAT Gateway, then to the internet gateway.  
라우팅은 프라이빗 서브넷에서 NAT 게이트웨이를 거쳐 인터넷 게이트웨이로 트래픽이 전달되도록 구성됩니다.  

Note that a NAT Gateway cannot work without an internet gateway.  
NAT 게이트웨이는 인터넷 게이트웨이 없이는 작동하지 않습니다.  

The bandwidth of a NAT Gateway is five gigabits per second, automatically scaling up to 100 gigabits per second.  
NAT 게이트웨이의 기본 대역폭은 초당 5Gb이며, 자동으로 최대 100Gb까지 확장됩니다.  

You do not need to manage any security groups for the NAT Gateway, which means you do not need to configure ports to enable connectivity.  
NAT 게이트웨이는 보안 그룹을 관리할 필요가 없으므로 연결을 위해 포트를 설정할 필요가 없습니다.  

---

## Example Setup  
## 예제 설정  

Currently, we have a private instance in a private subnet that cannot access the internet.  
현재 프라이빗 서브넷에 인터넷에 접근할 수 없는 프라이빗 인스턴스가 있습니다.  

We create the NAT Gateway in the public subnet.  
퍼블릭 서브넷에 NAT 게이트웨이를 생성합니다.  

Since the public subnet is already connected to the internet gateway, the NAT Gateway will have internet connectivity.  
퍼블릭 서브넷이 이미 인터넷 게이트웨이에 연결되어 있으므로 NAT 게이트웨이는 인터넷에 접근할 수 있습니다.  

Then, we edit the routes of the private subnet to connect our instance to the NAT Gateway.  
그런 다음 프라이빗 서브넷의 라우트를 수정하여 인스턴스가 NAT 게이트웨이에 연결되도록 합니다.  

---

## High Availability of NAT Gateways  
## NAT 게이트웨이의 고가용성  

The NAT Gateway is resilient only within a single Availability Zone.  
NAT 게이트웨이는 단일 가용 영역 내에서만 내결함성을 가집니다.  

It is redundant within that AZ, but if the AZ goes down, you need multiple NAT Gateways in multiple AZs to achieve fault tolerance.  
해당 AZ 내에서는 중복성을 가지지만, AZ가 다운되면 여러 AZ에 NAT 게이트웨이를 배치해야 내결함성을 확보할 수 있습니다.  

For example, if we have one NAT Gateway in one AZ, we create a second NAT Gateway in another AZ.  
예를 들어, 한 AZ에 NAT 게이트웨이가 하나 있다면 다른 AZ에 두 번째 NAT 게이트웨이를 생성합니다.  

Each network traffic is confined to its AZ.  
각 네트워크 트래픽은 해당 AZ 내에서만 전달됩니다.  

If an AZ goes down, all instances in that AZ become unreachable, but the NAT Gateway in the other AZ continues to work.  
AZ가 다운되면 해당 AZ의 모든 인스턴스는 접근 불가가 되지만, 다른 AZ의 NAT 게이트웨이는 계속 작동합니다.  

There is no need to connect the NAT Gateways together through route tables.  
NAT 게이트웨이를 라우트 테이블을 통해 서로 연결할 필요는 없습니다.  

---

## Differences Between NAT Gateways and NAT Instances  
## NAT 게이트웨이와 NAT 인스턴스의 차이점  

The NAT Gateway is highly available within a specific AZ.  
NAT 게이트웨이는 특정 AZ 내에서 고가용성을 제공합니다.  

To get high availability across AZs, you need to create another NAT Gateway in another AZ.  
AZ 전체에서 고가용성을 얻으려면 다른 AZ에 NAT 게이트웨이를 추가로 생성해야 합니다.  

For NAT instances, you would need scripts to manage failover between instances and overall management.  
NAT 인스턴스는 인스턴스 간 장애 조치 및 전체 관리를 위해 스크립트가 필요합니다.  

The bandwidth for a NAT Gateway is up to 100 gigabits per second per gateway.  
NAT 게이트웨이의 대역폭은 게이트웨이당 최대 100Gbps입니다.  

For NAT instances, bandwidth depends on the instance type; higher instance types provide more throughput.  
NAT 인스턴스는 인스턴스 유형에 따라 대역폭이 달라집니다. 고사양 인스턴스가 더 많은 처리량을 제공합니다.  

NAT Gateways are managed services, whereas NAT instances require you to manage software updates and patches.  
NAT 게이트웨이는 관리형 서비스이며, NAT 인스턴스는 소프트웨어 업데이트와 패치를 직접 관리해야 합니다.  

Cost for NAT Gateways is per hour plus data transfer.  
NAT 게이트웨이는 시간당 요금과 데이터 전송 요금이 부과됩니다.  

For NAT instances, cost depends on the instance type and size, plus network data transfer out to the internet.  
NAT 인스턴스는 인스턴스 유형과 크기, 인터넷으로 나가는 네트워크 트래픽에 따라 비용이 결정됩니다.  

NAT Gateways have a public Elastic IP address, which is beneficial.  
NAT 게이트웨이는 퍼블릭 Elastic IP 주소를 가지고 있어 유용합니다.  

NAT instances also have public IPs if configured.  
NAT 인스턴스도 설정 시 퍼블릭 IP를 가질 수 있습니다.  

Security groups are not used for NAT Gateways, which simplifies management.  
NAT 게이트웨이는 보안 그룹을 사용하지 않아 관리가 간단합니다.  

For NAT instances, you need to configure security groups carefully to allow the right ports.  
NAT 인스턴스는 올바른 포트를 허용하도록 보안 그룹을 신중하게 구성해야 합니다.  

NAT Gateways cannot be used as bastion hosts, whereas NAT instances can be used as bastion hosts if desired.  
NAT 게이트웨이는 Bastion Host로 사용할 수 없지만, NAT 인스턴스는 필요시 Bastion Host로 사용할 수 있습니다.  

There are many more differences between NAT Gateways and NAT instances.  
NAT 게이트웨이와 NAT 인스턴스 간에는 더 많은 차이점이 있습니다.  

From an exam perspective, this information should be sufficient to understand when to choose a NAT Gateway versus a NAT instance.  
시험 관점에서 NAT 게이트웨이와 NAT 인스턴스를 언제 선택해야 하는지 이해하는 데 충분합니다.  

This concludes the lecture on NAT Gateways. I hope you found it helpful, and I will see you in the next lecture.  
이로써 NAT 게이트웨이에 대한 강의를 마칩니다. 유익했기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- NAT Gateways provide a managed, high-bandwidth, and highly available solution for enabling internet access from private subnets.  
- NAT 게이트웨이는 프라이빗 서브넷의 인터넷 접근을 위해 관리형, 고대역폭, 고가용성 솔루션을 제공합니다.  

- NAT Gateways are deployed in public subnets and route traffic from private subnets to the internet gateway.  
- NAT 게이트웨이는 퍼블릭 서브넷에 배치되며, 프라이빗 서브넷 트래픽을 인터넷 게이트웨이로 라우팅합니다.  

- High availability for NAT Gateways requires deploying multiple gateways in different Availability Zones.  
- NAT 게이트웨이의 고가용성은 서로 다른 AZ에 여러 게이트웨이를 배치해야 달성할 수 있습니다.  

- NAT Gateways require no security group management and cannot be used as bastion hosts, unlike NAT instances.  
- NAT 게이트웨이는 보안 그룹 관리가 필요 없으며, NAT 인스턴스와 달리 Bastion Host로 사용할 수 없습니다.  
```
