```markdown
# Site-to-Site VPN, Virtual Private Gateway & Customer Gateway Hands-On  
# 사이트 간 VPN, 가상 프라이빗 게이트웨이(VGW) 및 고객 게이트웨이(CGW) 실습  

🎮 게임보상: "VPN Hands-On Badge" +700 XP  

---

## Introduction to Site-to-Site VPN in AWS  
## AWS에서 사이트 간 VPN 소개  

Let's explore how to create a site-to-site VPN connection in AWS.  
AWS에서 사이트 간 VPN 연결을 생성하는 방법을 살펴보겠습니다.  

This process involves several components and steps to securely connect your on-premises network to AWS.  
이 과정은 온프레미스 네트워크를 AWS와 안전하게 연결하기 위해 여러 구성 요소와 단계가 필요합니다.  

---

## Customer Gateway  
## 고객 게이트웨이(CGW)  

First, scroll down to the VPN section and click on "Customer Gateways."  
먼저, VPN 섹션으로 스크롤한 후 "Customer Gateways"를 클릭합니다.  

The initial step in establishing a site-to-site VPN connection is to create a customer gateway, which represents the device hosted on your on-premises network.  
사이트 간 VPN 연결을 설정하는 첫 단계는 온프레미스 네트워크에 호스팅된 장치를 나타내는 고객 게이트웨이를 생성하는 것입니다.  

You create this gateway on-premises and can name it, for example, "AWS."  
이 게이트웨이는 온프레미스에서 생성하며, 예를 들어 이름을 "AWS"로 지정할 수 있습니다.  

Next, you specify a BGP ASN (Border Gateway Protocol Autonomous System Number) for your gateway device.  
다음으로 게이트웨이 장치에 대해 BGP ASN(Border Gateway Protocol 자율 시스템 번호)을 지정합니다.  

This is an advanced setting and is not mandatory to know for basic setup.  
이는 고급 설정이며, 기본 설정에는 필수 사항이 아닙니다.  

You must also specify the IP address of your customer gateway device's external interface.  
또한 고객 게이트웨이 장치의 외부 인터페이스 IP 주소를 지정해야 합니다.  

This IP address allows AWS to reach your on-premises infrastructure.  
이 IP 주소는 AWS가 온프레미스 인프라에 접근할 수 있도록 합니다.  

Additionally, you specify a Certificate ARN (Amazon Resource Name), which enables AWS to connect securely to your VPN device on-premises and establish a secure connection.  
또한 Certificate ARN(Amazon Resource Name)을 지정하여 AWS가 온프레미스 VPN 장치에 안전하게 연결하고 보안 연결을 설정할 수 있게 합니다.  

Note that creating a customer gateway requires an existing on-premises infrastructure, so this demonstration will not include creating one.  
고객 게이트웨이를 생성하려면 기존 온프레미스 인프라가 필요하므로 이 실습에서는 생성 과정을 포함하지 않습니다.  

---

## Virtual Private Gateway  
## 가상 프라이빗 게이트웨이(VGW)  

Next, you create a Virtual Private Gateway on the AWS side.  
다음으로 AWS 측에서 가상 프라이빗 게이트웨이(VGW)를 생성합니다.  

This gateway is created using an ASN number and represents the AWS endpoint of the VPN connection.  
이 게이트웨이는 ASN 번호를 사용하여 생성되며 VPN 연결의 AWS 엔드포인트를 나타냅니다.  

This gateway acts as the counterpart to your customer gateway and facilitates the VPN connection from AWS to your on-premises network.  
이 게이트웨이는 고객 게이트웨이의 대응 장치 역할을 하며 AWS에서 온프레미스 네트워크로의 VPN 연결을 지원합니다.  

---

## Establishing the Site-to-Site VPN Connection  
## 사이트 간 VPN 연결 설정  

After creating both the customer gateway and the virtual private gateway, the next step is to connect them by creating a site-to-site VPN connection.  
고객 게이트웨이와 가상 프라이빗 게이트웨이를 모두 생성한 후, 다음 단계는 사이트 간 VPN 연결을 생성하여 두 게이트웨이를 연결하는 것입니다.  

To do this, click on "Create VPN Connection."  
이를 위해 "Create VPN Connection"을 클릭합니다.  

Select the type as "Virtual private gateway," then specify the virtual private gateway you created earlier.  
유형을 "Virtual private gateway"로 선택하고 이전에 생성한 가상 프라이빗 게이트웨이를 지정합니다.  

Next, specify the customer gateway you created.  
다음으로 생성한 고객 게이트웨이를 지정합니다.  

There are several options related to routing, IPv4, tunneling, and other configurations, but these details are generally not required for basic understanding or exam purposes.  
라우팅, IPv4, 터널링 및 기타 설정과 관련된 옵션이 있지만, 기본 이해나 시험 목적에는 일반적으로 필요하지 않습니다.  

Finally, create the VPN connection to link the two gateways securely.  
마지막으로 두 게이트웨이를 안전하게 연결하기 위해 VPN 연결을 생성합니다.  

---

## Summary  
## 요약  

To summarize, establishing a site-to-site VPN connection between your on-premises network and AWS involves three main steps:  
요약하면, 온프레미스 네트워크와 AWS 간 사이트 간 VPN 연결을 설정하는 주요 단계는 세 가지입니다.  

1. Creating a customer gateway representing your on-premises device.  
1. 온프레미스 장치를 나타내는 고객 게이트웨이 생성  

2. Creating a virtual private gateway on the AWS side.  
2. AWS 측에서 가상 프라이빗 게이트웨이 생성  

3. Connecting these two gateways using a site-to-site VPN connection.  
3. 사이트 간 VPN 연결을 통해 두 게이트웨이 연결  

This process enables secure communication between your local infrastructure and AWS resources.  
이 과정은 로컬 인프라와 AWS 리소스 간 안전한 통신을 가능하게 합니다.  

---

## Key Takeaways  
## 핵심 요약  

- To establish a site-to-site VPN connection in AWS, you must first create a customer gateway representing your on-premises device.  
- AWS에서 사이트 간 VPN 연결을 설정하려면 먼저 온프레미스 장치를 나타내는 고객 게이트웨이를 생성해야 합니다.  

- A virtual private gateway is created on the AWS side to facilitate the connection.  
- 연결을 용이하게 하기 위해 AWS 측에서 가상 프라이빗 게이트웨이를 생성합니다.  

- The site-to-site VPN connection links the customer gateway and the virtual private gateway.  
- 사이트 간 VPN 연결은 고객 게이트웨이와 가상 프라이빗 게이트웨이를 연결합니다.  

- Understanding the creation and connection of these gateways is essential for AWS VPN setup, while detailed routing and tunneling options are generally out of scope for basic hands-on and exam purposes.  
- 이러한 게이트웨이 생성 및 연결 과정을 이해하는 것은 AWS VPN 설정에 필수적이며, 상세한 라우팅 및 터널링 옵션은 기본 실습과 시험 범위에서는 일반적으로 제외됩니다.  
```
