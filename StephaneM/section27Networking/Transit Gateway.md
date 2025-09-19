```markdown
# Transit Gateway  
# 트랜싯 게이트웨이  

🎮 게임보상: "Transit Master Badge" +500 XP  

---

## Introduction to AWS Network Topologies  
## AWS 네트워크 토폴로지 소개  

Common network topologies in AWS can become quite complicated.  
AWS에서 일반적인 네트워크 토폴로지는 상당히 복잡해질 수 있습니다.  

For example, when you have many VPCs and want to peer them together, establish VPN connections, and use Direct Connect gateways to connect to multiple VPCs simultaneously, the network topology can become very complex.  
예를 들어, 여러 VPC를 피어링하고, VPN 연결을 설정하며, Direct Connect 게이트웨이를 사용하여 동시에 여러 VPC에 연결하려고 하면 네트워크 토폴로지가 매우 복잡해질 수 있습니다.  

---

## AWS Transit Gateway Overview  
## AWS 트랜싯 게이트웨이 개요  

To solve these complexities, AWS introduced the Transit Gateway.  
이러한 복잡성을 해결하기 위해 AWS는 트랜싯 게이트웨이를 도입했습니다.  

It provides a transitive peering connection between thousands of VPCs, your on-premises data center, site-to-site VPNs, and Direct Connect connections in a hub-and-spoke star topology.  
트랜싯 게이트웨이는 허브 앤 스포크(Hub-and-Spoke) 스타 토폴로지에서 수천 개의 VPC, 온프레미스 데이터 센터, 사이트 간 VPN, Direct Connect 연결 간의 전이적(Transitive) 피어링 연결을 제공합니다.  

---

## Transit Gateway Architecture  
## 트랜싯 게이트웨이 아키텍처  

Consider a diagram where the Transit Gateway is at the center, connecting multiple VPCs.  
트랜싯 게이트웨이가 중앙에 위치하고 여러 VPC를 연결하는 다이어그램을 생각해보세요.  

In this setup, you do not need to peer the VPCs together individually; they are connected transitively through the Transit Gateway.  
이 구성에서는 VPC를 개별적으로 피어링할 필요가 없으며, 트랜싯 게이트웨이를 통해 전이적으로 연결됩니다.  

This allows all the VPCs to communicate with each other seamlessly.  
이를 통해 모든 VPC가 서로 원활하게 통신할 수 있습니다.  

You can also connect a Direct Connect gateway to the Transit Gateway, enabling a Direct Connect connection to many different VPCs simultaneously.  
또한 Direct Connect 게이트웨이를 트랜싯 게이트웨이에 연결하여, 여러 VPC에 동시에 Direct Connect 연결을 제공할 수 있습니다.  

Alternatively, if you prefer site-to-site VPN connections, you can connect your customer gateway and VPN connection into the Transit Gateway, granting access to all attached VPCs.  
또는 사이트 간 VPN 연결을 선호한다면, 고객 게이트웨이와 VPN 연결을 트랜싯 게이트웨이에 연결하여 연결된 모든 VPC에 접근할 수 있습니다.  

---

## Features and Capabilities  
## 기능 및 특징  

Transit Gateway is a regional resource that supports cross-region functionality.  
트랜싯 게이트웨이는 리전별 리소스로, 크로스 리전 기능을 지원합니다.  

You can share your Transit Gateway across AWS accounts using the Resource Access Manager.  
리소스 액세스 매니저(Resource Access Manager)를 사용하여 트랜싯 게이트웨이를 여러 AWS 계정과 공유할 수 있습니다.  

Additionally, Transit Gateways can be peered across regions.  
또한 트랜싯 게이트웨이는 리전 간 피어링도 지원합니다.  

---

## Routing Control  
## 라우팅 제어  

To define which VPCs or connections can communicate, you create route tables for your Transit Gateway.  
어떤 VPC나 연결이 통신할 수 있는지 정의하려면 트랜싯 게이트웨이에 라우트 테이블을 생성합니다.  

This allows you to limit communication between VPCs and connections, providing full control over the routing of all traffic within the Transit Gateway to enhance network security.  
이를 통해 VPC 간 및 연결 간 통신을 제한하고, 트랜싯 게이트웨이 내 모든 트래픽의 라우팅을 완전히 제어하여 네트워크 보안을 강화할 수 있습니다.  

Transit Gateway works with Direct Connect gateways and VPN connections.  
트랜싯 게이트웨이는 Direct Connect 게이트웨이와 VPN 연결과 함께 작동합니다.  

Notably, it is the only AWS service that supports IP multicast.  
특히 IP 멀티캐스트를 지원하는 유일한 AWS 서비스입니다.  

If you encounter IP multicast in an exam, remember that Transit Gateway is the service to use.  
시험에서 IP 멀티캐스트가 나오면 트랜싯 게이트웨이를 사용해야 함을 기억하세요.  

---

## Increasing VPN Bandwidth with ECMP  
## ECMP를 통한 VPN 대역폭 증가  

Another use case for Transit Gateway is increasing the bandwidth of your site-to-site VPN connection using Equal-Cost Multi-Path (ECMP) routing.  
트랜싯 게이트웨이의 또 다른 사용 사례는 ECMP(Equal-Cost Multi-Path) 라우팅을 사용하여 사이트 간 VPN 연결의 대역폭을 증가시키는 것입니다.  

ECMP is a routing strategy that forwards packets over multiple best paths simultaneously.  
ECMP는 패킷을 여러 최적 경로를 통해 동시에 전달하는 라우팅 전략입니다.  

---

## ECMP Use Case  
## ECMP 사용 사례  

By creating multiple site-to-site VPN connections to a Transit Gateway, you can increase the bandwidth of your connection to AWS.  
트랜싯 게이트웨이에 여러 사이트 간 VPN 연결을 생성하면 AWS로의 연결 대역폭을 증가시킬 수 있습니다.  

For example, consider a Transit Gateway attached to four VPCs and connected to a corporate data center via site-to-site VPN.  
예를 들어, 네 개의 VPC에 연결되고 사이트 간 VPN을 통해 기업 데이터 센터에 연결된 트랜싯 게이트웨이를 생각해보세요.  

When establishing a site-to-site VPN connection, there are two tunnels: one for outbound traffic and one for inbound traffic.  
사이트 간 VPN 연결을 설정하면 두 개의 터널이 생성됩니다: 아웃바운드 트래픽용과 인바운드 트래픽용.  

When connecting a VPN directly to a VPC, both tunnels are used as part of a single connection.  
VPN을 VPC에 직접 연결하면 두 터널이 단일 연결의 일부로 사용됩니다.  

However, with a Transit Gateway, both tunnels can be used simultaneously, and you can create multiple site-to-site VPN attachments, effectively creating multiple tunnels.  
하지만 트랜싯 게이트웨이를 사용하면 두 터널을 동시에 사용할 수 있으며, 여러 사이트 간 VPN 연결을 생성하여 사실상 여러 터널을 만들 수 있습니다.  

For example, with two site-to-site VPN attachments to a Transit Gateway, you have four tunnels in total.  
예를 들어, 트랜싯 게이트웨이에 두 개의 사이트 간 VPN 연결을 만들면 총 네 개의 터널이 생깁니다.  

This setup increases the throughput of your connection, which is not possible when connecting your corporate data center directly to a VPC.  
이 구성은 연결의 처리량을 증가시키며, 이는 기업 데이터 센터를 VPC에 직접 연결할 때는 불가능합니다.  

---

## VPN Throughput Limits  
## VPN 처리량 제한  

A VPN connection to a virtual private gateway provides one tunnel, effectively one connection to one VPC, with a maximum throughput of 1.5 Gbps.  
가상 프라이빗 게이트웨이에 대한 VPN 연결은 하나의 터널, 즉 하나의 VPC에 대한 단일 연결을 제공하며 최대 처리량은 1.5Gbps입니다.  

In contrast, a VPN connection to a Transit Gateway supports multiple VPCs transitively and provides 2.5 Gbps throughput per site-to-site VPN connection due to ECMP utilizing both tunnels.  
반면, 트랜싯 게이트웨이에 대한 VPN 연결은 여러 VPC를 전이적으로 지원하며, ECMP가 두 터널을 활용하기 때문에 사이트 간 VPN 연결당 2.5Gbps 처리량을 제공합니다.  

You can add multiple site-to-site VPN connections to a Transit Gateway, such as two or three, to double or triple your throughput using ECMP.  
트랜싯 게이트웨이에 여러 사이트 간 VPN 연결을 추가하면 ECMP를 사용하여 처리량을 두 배 또는 세 배로 늘릴 수 있습니다.  

This is an important concept for exams.  
이는 시험에서 중요한 개념입니다.  

Note that when setting up this architecture, you will incur costs for each gigabyte of data transferred through the Transit Gateway, so there is an added cost associated with this performance optimization.  
이 아키텍처를 설정할 때, 트랜싯 게이트웨이를 통해 전송되는 데이터 기가바이트당 비용이 발생하므로, 성능 최적화와 관련된 추가 비용이 있다는 점을 유의하세요.  

---

## Sharing Direct Connect Connections Across Accounts  
## 계정 간 Direct Connect 연결 공유  

You can share your Direct Connect connection between multiple AWS accounts using the Transit Gateway.  
트랜싯 게이트웨이를 사용하여 여러 AWS 계정 간 Direct Connect 연결을 공유할 수 있습니다.  

The setup involves establishing a Direct Connect connection between your corporate data center and a Direct Connect location, then setting up Transit Gateways in the VPCs across different accounts.  
이 설정은 기업 데이터 센터와 Direct Connect 위치 간 연결을 설정한 후, 서로 다른 계정의 VPC에 트랜싯 게이트웨이를 설정하는 것을 포함합니다.  

You connect the Direct Connect location to a Direct Connect gateway, which is then connected to the Transit Gateway.  
Direct Connect 위치를 Direct Connect 게이트웨이에 연결한 다음, 이 게이트웨이를 트랜싯 게이트웨이에 연결합니다.  

This architecture allows sharing a Direct Connect connection across multiple accounts and multiple VPCs, which is very convenient and efficient.  
이 아키텍처는 여러 계정과 VPC 간에 Direct Connect 연결을 공유할 수 있게 해주어 매우 편리하고 효율적입니다.  

---

## Conclusion  
## 결론  

These architectures involving Transit Gateway can appear in exams, so it is important to understand how they work.  
트랜싯 게이트웨이를 포함한 이러한 아키텍처는 시험에 출제될 수 있으므로, 작동 방식을 이해하는 것이 중요합니다.  

This concludes the lecture on Transit Gateway.  
이로써 트랜싯 게이트웨이 강의를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Transit Gateway simplifies complex network topologies by enabling transitive peering between thousands of VPCs, on-premises data centers, site-to-site VPNs, and Direct Connect connections in a hub-and-spoke star configuration.  
- AWS 트랜싯 게이트웨이는 허브 앤 스포크 스타 구성에서 수천 개의 VPC, 온프레미스 데이터 센터, 사이트 간 VPN 및 Direct Connect 연결 간 전이적 피어링을 가능하게 하여 복잡한 네트워크 토폴로지를 단순화합니다.  

- Transit Gateway is a regional resource that supports cross-region peering and resource sharing across AWS accounts using the Resource Access Manager.  
- 트랜싯 게이트웨이는 리전별 리소스로, 리소스 액세스 매니저를 사용하여 크로스 리전 피어링 및 계정 간 리소스 공유를 지원합니다.  

- Route tables within the Transit Gateway control which VPCs and connections can communicate, providing granular network security.  
- 트랜싯 게이트웨이의 라우트 테이블은 어떤 VPC와 연결이 통신할 수 있는지 제어하며, 세분화된 네트워크 보안을 제공합니다.  

- Transit Gateway supports IP multicast and enables bandwidth scaling for site-to-site VPN connections using Equal-Cost Multi-Path (ECMP) routing.  
- 트랜싯 게이트웨이는 IP 멀티캐스트를 지원하며 ECMP 라우팅을 사용하여 사이트 간 VPN 연결의 대역폭을 확장할 수 있습니다.  

- Multiple site-to-site VPN connections can be attached to a Transit Gateway to increase throughput beyond the 1.5 Gbps limit of a single VPN connection to a virtual private gateway.  
- 여러 사이트 간 VPN 연결을 트랜싯 게이트웨이에 연결하여, 가상 프라이빗 게이트웨이에 대한 단일 VPN 연결의 1.5Gbps 한계를 초과하는 처리량을 확보할 수 있습니다.  

- Direct Connect connections can be shared across multiple AWS accounts and VPCs through the Transit Gateway, facilitating efficient network architecture and cost optimization.  
- Direct Connect 연결은 트랜싯 게이트웨이를 통해 여러 AWS 계정과 VPC 간에 공유할 수 있어 효율적인 네트워크 아키텍처와 비용 최적화를 지원합니다.  
```
