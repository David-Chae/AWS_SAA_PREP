```markdown
# Direct Connect & Direct Connect Gateway  
# Direct Connect 및 Direct Connect 게이트웨이  

🎮 게임보상: "Direct Connect Badge" +750 XP  

---

## Introduction to AWS Direct Connect  
## AWS Direct Connect 소개  

AWS Direct Connect, often abbreviated as DX in exams, provides a dedicated private connection from a remote network directly into your Virtual Private Cloud (VPC).  
AWS Direct Connect(시험에서는 DX로 줄여서 표기)는 원격 네트워크에서 직접 Virtual Private Cloud(VPC)로 연결되는 전용 프라이빗 연결을 제공합니다.  

To establish this connection, you must set up a Direct Connect connection using an AWS Direct Connect location.  
이 연결을 설정하려면 AWS Direct Connect 위치를 사용하여 Direct Connect 연결을 구성해야 합니다.  

Additionally, a virtual private gateway must be configured on your VPC side to enable connectivity between your on-premises data center and AWS.  
또한, 온프레미스 데이터 센터와 AWS 간 연결을 가능하게 하려면 VPC 측에 가상 프라이빗 게이트웨이를 구성해야 합니다.  

The key idea is that on the same Direct Connect connection, you can access both public resources, such as Amazon S3, and private resources, such as EC2 instances, by using the public virtual interface (VIF) and the private VIF respectively.  
핵심 개념은 동일한 Direct Connect 연결을 통해 퍼블릭 VIF를 사용하면 Amazon S3와 같은 퍼블릭 리소스에, 프라이빗 VIF를 사용하면 EC2 인스턴스와 같은 프라이빗 리소스에 접근할 수 있다는 것입니다.  

---

## Use Cases for Direct Connect  
## Direct Connect 활용 사례  

**Increased Bandwidth Throughput:** Direct Connect offers higher bandwidth, which is beneficial when working with large data sets because the data does not traverse the public internet.  
**대역폭 증가:** Direct Connect는 더 높은 대역폭을 제공하며, 대용량 데이터 작업 시 유리합니다. 데이터가 공용 인터넷을 통과하지 않기 때문입니다.  

**Lower Cost:** Using a private connection reduces data transfer costs compared to public internet usage.  
**비용 절감:** 전용 연결을 사용하면 공용 인터넷 사용 대비 데이터 전송 비용이 줄어듭니다.  

**Consistent Network Experience:** Since Direct Connect is a private connection, it provides more consistent network performance, which is especially helpful for applications using real-time data feeds.  
**일관된 네트워크 경험:** Direct Connect는 프라이빗 연결이므로 네트워크 성능이 안정적이며, 실시간 데이터 피드를 사용하는 애플리케이션에 특히 유용합니다.  

**Hybrid Environments Support:** It facilitates connectivity between on-premises data centers and the cloud.  
**하이브리드 환경 지원:** 온프레미스 데이터 센터와 클라우드 간 연결을 용이하게 합니다.  

**Supports IPv4 and IPv6:** Direct Connect supports both IP protocols.  
**IPv4 및 IPv6 지원:** Direct Connect는 두 가지 IP 프로토콜을 모두 지원합니다.  

---

## Architecture of Direct Connect  
## Direct Connect 아키텍처  

Consider a scenario where you want to connect an AWS region to your corporate data center.  
AWS 리전을 기업 데이터 센터와 연결하려는 시나리오를 고려해봅시다.  

You begin by commissioning an AWS Direct Connect location, which are physical locations listed on the AWS website.  
먼저 AWS Direct Connect 위치를 설정하는데, 이는 AWS 웹사이트에 나열된 물리적 위치입니다.  

At this location, there are Direct Connect endpoints and customer or partner routers housed in cages that you rent.  
이 위치에는 Direct Connect 엔드포인트와 고객 또는 파트너 라우터가 케이지에 배치되어 있으며, 사용자가 이를 임대합니다.  

On your on-premises data center, you set up a customer router with a firewall.  
온프레미스 데이터 센터에서 방화벽이 있는 고객 라우터를 설정합니다.  

You then configure a private virtual interface (private VIF) to access your private resources within your VPC.  
그 후 VPC 내 프라이빗 리소스에 접근하기 위해 프라이빗 가상 인터페이스(private VIF)를 구성합니다.  

This private VIF connects through the Direct Connect location to a virtual private gateway attached to your VPC, enabling access to private subnets and EC2 instances.  
이 프라이빗 VIF는 Direct Connect 위치를 통해 VPC에 연결된 가상 프라이빗 게이트웨이와 연결되어 프라이빗 서브넷 및 EC2 인스턴스에 접근할 수 있게 합니다.  

All this communication happens privately without traversing the public internet.  
모든 통신은 공용 인터넷을 통과하지 않고 프라이빗하게 이루어집니다.  

Setting up this connection manually can take up to a month, but it ensures private connectivity.  
이 연결을 수동으로 설정하면 최대 한 달이 걸릴 수 있지만, 프라이빗 연결이 보장됩니다.  

Alternatively, to connect to public AWS services such as Amazon Glacier or Amazon S3, you set up a public virtual interface (public VIF).  
대안으로 Amazon Glacier나 Amazon S3 같은 퍼블릭 AWS 서비스에 연결하려면 퍼블릭 가상 인터페이스(public VIF)를 설정합니다.  

This public VIF follows the same path but connects directly to AWS without going through a virtual private gateway.  
이 퍼블릭 VIF는 동일한 경로를 따르지만 가상 프라이빗 게이트웨이를 거치지 않고 AWS에 직접 연결됩니다.  

---

## Connecting to Multiple VPCs Across Regions Using Direct Connect Gateway  
## Direct Connect 게이트웨이를 통한 다중 리전 VPC 연결  

If you want to connect your on-premises data center to one or more VPCs in different AWS regions, you must use a Direct Connect gateway.  
온프레미스 데이터 센터를 여러 AWS 리전의 하나 이상의 VPC와 연결하려면 Direct Connect 게이트웨이를 사용해야 합니다.  

For example, suppose you have two regions with two different VPCs, each having distinct CIDR blocks.  
예를 들어, 서로 다른 CIDR 블록을 가진 두 개의 VPC가 두 리전에 있다고 가정합니다.  

You establish a Direct Connect connection and use the private VIF to connect to the Direct Connect gateway.  
Direct Connect 연결을 설정하고 프라이빗 VIF를 사용하여 Direct Connect 게이트웨이에 연결합니다.  

This gateway then connects via private virtual interfaces to virtual private gateways in each region, enabling connectivity to multiple VPCs across regions.  
그 후 게이트웨이는 각 리전의 가상 프라이빗 게이트웨이에 프라이빗 VIF를 통해 연결되어 다중 리전 VPC 연결을 가능하게 합니다.  

---

## Direct Connect Connection Types  
## Direct Connect 연결 유형  

There are two main types of Direct Connect connections:  
Direct Connect 연결에는 두 가지 주요 유형이 있습니다.  

**Dedicated Connection:** Offers 1, 10, or 100 gigabits per second capacity with a physical Ethernet port dedicated to you.  
**전용 연결(Dedicated Connection):** 물리적 이더넷 포트가 전용으로 제공되며 1, 10 또는 100Gbps 용량을 지원합니다.  

You request this connection from AWS, and it is provisioned by an AWS Direct Connect partner.  
이 연결은 AWS에 요청하며 AWS Direct Connect 파트너가 프로비저닝합니다.  

**Hosted Connection:** Available in various capacities such as 50 megabits per second, 500 megabits per second, up to 10 gigabits per second.  
**호스티드 연결(Hosted Connection):** 50Mbps, 500Mbps부터 최대 10Gbps까지 다양한 용량으로 제공됩니다.  

These connections are requested via AWS Direct Connect partners and offer more flexibility with capacity on demand, allowing you to add or remove capacity as needed.  
이 연결은 AWS Direct Connect 파트너를 통해 요청하며, 필요에 따라 용량을 추가하거나 제거할 수 있어 유연성이 높습니다.  

Lead times for setting up either connection type are often longer than one month.  
두 연결 유형 모두 설정 리드타임은 일반적으로 한 달 이상 걸립니다.  

In exam scenarios where data transfer is required within a week, Direct Connect is typically not a viable option due to its long setup time unless an existing Direct Connect connection is already established.  
시험 시 일주일 내 데이터 전송이 필요할 경우, 기존 Direct Connect 연결이 없다면 설치 시간이 길어 일반적으로 적합하지 않습니다.  

---

## Security Considerations  
## 보안 고려사항  

Direct Connect does not provide encryption by default because it is a private connection.  
Direct Connect는 프라이빗 연결이므로 기본적으로 암호화를 제공하지 않습니다.  

If encryption is required, you can set up a VPN connection alongside Direct Connect to provide an IPsec encrypted private connection.  
암호화가 필요하면 Direct Connect와 함께 VPN 연결을 설정하여 IPsec 암호화된 프라이빗 연결을 제공할 수 있습니다.  

This adds an extra layer of security but increases complexity.  
이는 보안 레이어를 추가하지만 복잡성을 증가시킵니다.  

To implement this, you establish the Direct Connect location and then configure a VPN connection on top of it, ensuring that all traffic between your corporate data center and AWS is encrypted.  
이를 구현하려면 Direct Connect 위치를 설정한 후 그 위에 VPN 연결을 구성하여 온프레미스 데이터 센터와 AWS 간 모든 트래픽을 암호화합니다.  

---

## Resiliency Architectures for Direct Connect  
## Direct Connect의 복원력 아키텍처  

Two modes of resiliency are important to know for exams:  
시험에서 중요한 두 가지 복원력 모드가 있습니다.  

**High Resiliency:** Suitable for critical workloads.  
**고복원력(High Resiliency):** 중요한 워크로드에 적합합니다.  

This involves setting up multiple Direct Connect connections across two corporate data centers and two different Direct Connect locations.  
이는 두 개의 기업 데이터 센터와 두 개의 Direct Connect 위치에 걸쳐 여러 Direct Connect 연결을 설정하는 것을 포함합니다.  

Each location has a private VIF, providing redundancy so that if one Direct Connect location fails, the other can maintain connectivity.  
각 위치에는 프라이빗 VIF가 있어 한 Direct Connect 위치가 실패해도 다른 위치가 연결을 유지할 수 있도록 합니다.  

**Maximum Resiliency:** For maximum fault tolerance, you set up two Direct Connect locations, each with two independent connections.  
**최대 복원력(Maximum Resiliency):** 최대 내결함성을 위해 두 개의 Direct Connect 위치를 설정하고 각 위치에 두 개의 독립 연결을 구성합니다.  

This results in four connections across two locations, terminating on separate devices.  
이렇게 하면 두 위치에 걸쳐 총 네 개의 연결이 생성되며 서로 다른 장치에 종단됩니다.  

This architecture provides the highest level of resiliency and is often emphasized in exam contexts.  
이 아키텍처는 가장 높은 수준의 복원력을 제공하며, 시험에서 강조되는 부분입니다.  

---

## Conclusion  
## 결론  

AWS Direct Connect offers a private, high-bandwidth, and consistent network connection between on-premises data centers and AWS.  
AWS Direct Connect는 온프레미스 데이터 센터와 AWS 간 프라이빗하고, 고대역폭이며 안정적인 네트워크 연결을 제공합니다.  

It supports both private and public virtual interfaces, enables multi-region VPC connectivity through Direct Connect gateways, and offers different connection types with varying capacities and lead times.  
프라이빗 및 퍼블릭 VIF를 지원하며, Direct Connect 게이트웨이를 통해 다중 리전 VPC 연결을 가능하게 하고, 용량과 설정 시간에 따라 다양한 연결 유형을 제공합니다.  

Security can be enhanced with VPN overlays, and resiliency can be architected through multiple connections and locations.  
보안은 VPN 오버레이로 강화할 수 있으며, 복원력은 여러 연결과 위치를 통해 설계할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Direct Connect provides a dedicated private connection from on-premises data centers to AWS VPCs, improving bandwidth and network consistency.  
- AWS Direct Connect는 온프레미스 데이터 센터와 AWS VPC 간 전용 연결을 제공하여 대역폭과 네트워크 안정성을 향상시킵니다.  

- Direct Connect supports both private virtual interfaces (VIFs) for private resources and public VIFs for AWS public services.  
- Direct Connect는 프라이빗 리소스를 위한 프라이빗 VIF와 AWS 퍼블릭
```


서비스를 위한 퍼블릭 VIF를 모두 지원합니다.

* Direct Connect gateways enable connectivity to multiple VPCs across different AWS regions.

* Direct Connect 게이트웨이는 여러 AWS 리전의 VPC 연결을 가능하게 합니다.

* Resiliency can be enhanced by deploying multiple Direct Connect connections across different locations and devices.

* 다양한 위치와 장치에 여러 Direct Connect 연결을 배치하면 복원력을 향상시킬 수 있습니다.

```
```
