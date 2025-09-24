# Private vs Public vs Elastic IP  
# 프라이빗 vs 퍼블릭 vs 엘라스틱 IP  
→ IP 주소의 종류와 차이를 설명하는 주제.

---

## Introduction to Private and Public IP  
## 프라이빗 및 퍼블릭 IP 소개  
→ 프라이빗 IP와 퍼블릭 IP 개념을 이해하는 부분.

We are now exploring the important concept of Private and Public IP addresses. Although this topic may be basic for some, it is essential to ensure everyone understands it clearly.  
우리는 이제 프라이빗 및 퍼블릭 IP 주소라는 중요한 개념을 탐구합니다. 일부 사람들에게는 기초적일 수 있지만 모두가 명확히 이해해야 하는 주제입니다.  
→ 기본 개념 같아도 네트워킹의 핵심이므로 반드시 알아야 함.

Networking involves IP addresses, primarily IPv4 and IPv6. IPv4 is the most common format, consisting of four numbers separated by three dots.  
네트워킹은 주로 IPv4와 IPv6의 IP 주소를 포함합니다. IPv4는 가장 일반적인 형식으로, 세 개의 점으로 구분된 네 개의 숫자로 구성됩니다.  
→ 흔히 보는 192.168.0.1 같은 주소가 IPv4.

IPv6 is less common, featuring a longer string of numbers and letters.  
IPv6는 덜 일반적이며, 더 긴 숫자와 문자 조합으로 되어 있습니다.  
→ 차세대 규격으로 주소 고갈 문제를 해결하려고 나옴.

In this course, we will focus on IPv4, but be aware that AWS supports IPv6 as well.  
이 과정에서는 IPv4에 초점을 맞추지만, AWS도 IPv6를 지원한다는 점을 알아두세요.  
→ AWS는 둘 다 지원하지만 실습은 IPv4 기준.

---

## IPv4 remains the most widely used format online.  
## IPv4는 여전히 온라인에서 가장 널리 사용되는 형식입니다.  
→ 인터넷에서 기본적으로 쓰이는 규격임.

IPv6 is more prevalent in the Internet of Things (IoT) domain and addresses many issues not relevant to us currently.  
IPv6는 IoT(사물인터넷) 분야에서 더 보편화되어 있으며, 현재 우리에게 직접적인 관련은 없는 문제들을 해결합니다.  
→ IoT에서 더 많이 쓰임.

IPv4 allows for approximately 3.7 billion different public addresses, which is nearing exhaustion.  
IPv4는 약 37억 개의 퍼블릭 주소를 제공하며, 거의 고갈 상태에 있습니다.  
→ 그래서 IPv6 필요성이 커짐.

Each number in an IPv4 address can range from zero to 255, separated by dots, resulting in this large number of unique addresses.  
IPv4 주소의 각 숫자는 0에서 255 사이의 값일 수 있으며, 점으로 구분되어 이렇게 많은 고유 주소를 만듭니다.  
→ 0~255 조합 덕분에 주소 개수가 제한됨.

---

## Public IP Addresses  
## 퍼블릭 IP 주소  
→ 인터넷에서 접근 가능한 주소.

For example, a web server with a public IP address, such as an EC2 instance, can communicate with other servers using their public IPs.  
예를 들어, 퍼블릭 IP 주소를 가진 웹 서버(예: EC2 인스턴스)는 다른 서버와 퍼블릭 IP를 통해 통신할 수 있습니다.  
→ 서버 간 인터넷 통신에 필요.

Public IPs enable servers to talk to one another over the internet, which is essential for many applications.  
퍼블릭 IP는 서버들이 인터넷을 통해 서로 통신할 수 있게 하며, 이는 많은 애플리케이션에 필수적입니다.  
→ 웹사이트, API 등에서 반드시 필요.

---

## Private IP Addresses and Networks  
## 프라이빗 IP 주소와 네트워크  
→ 내부 네트워크 전용 주소.

Companies often have private networks with private IP ranges.  
기업은 종종 프라이빗 IP 범위를 가진 사설 네트워크를 보유합니다.  
→ 사내망 같은 환경.

Private IPs are defined in a specific way, allowing all computers within that private network to communicate with each other using their private IPs.  
프라이빗 IP는 특정 방식으로 정의되어 있으며, 네트워크 내 모든 컴퓨터가 서로 프라이빗 IP로 통신할 수 있게 합니다.  
→ 내부 통신 전용.

When these networks connect to the internet through an internet gateway, the instances gain access to other servers and services on the internet.  
이러한 네트워크가 인터넷 게이트웨이를 통해 인터넷에 연결되면, 인스턴스는 다른 서버 및 서비스에 접근할 수 있습니다.  
→ NAT/게이트웨이 통해 외부 접속 가능.

This pattern is common in AWS environments.  
이 패턴은 AWS 환경에서 일반적입니다.  
→ AWS도 내부망+게이트웨이 구조.

---

## Differences Between Public and Private IPs  
## 퍼블릭과 프라이빗 IP의 차이  
→ 핵심 비교.

**Public IP:** The machine is identifiable on the internet, and the public IP must be unique globally.  
**퍼블릭 IP:** 인터넷에서 식별 가능하며, 전 세계적으로 고유해야 합니다.  
→ 같은 퍼블릭 IP는 중복 불가.

**Private IP:** The machine is identifiable only within the private network, and the IP must be unique only within that private network.  
**프라이빗 IP:** 사설 네트워크 내에서만 식별 가능하며, 해당 네트워크 안에서만 고유해야 합니다.  
→ 서로 다른 회사에서 같은 사설 IP 사용해도 문제 없음.

Machines on private networks connect to the internet through a NAT device and an internet gateway acting as a proxy.  
프라이빗 네트워크의 장비는 NAT 장치와 인터넷 게이트웨이를 통해 인터넷에 접속합니다.  
→ 직접 못 나가고 NAT 통해야 함.

Only specific IP ranges are designated for private IPs.  
프라이빗 IP는 특정한 IP 대역만 지정되어 있습니다.  
→ RFC1918 정의된 대역 (예: 10.x.x.x, 192.168.x.x).

---

## Elastic IP Addresses in AWS  
## AWS의 엘라스틱 IP  
→ 고정 퍼블릭 IP 개념.

When an EC2 instance is stopped and started, its public IP address changes.  
EC2 인스턴스를 중지 후 재시작하면 퍼블릭 IP 주소가 변경됩니다.  
→ IP 고정 필요성 발생.

If a fixed public IP is required for an instance, an Elastic IP can be used.  
인스턴스에 고정 퍼블릭 IP가 필요하다면 엘라스틱 IP를 사용할 수 있습니다.  
→ 고정 주소 할당 가능.

An Elastic IP is a public IPv4 address that you own as long as you do not delete it.  
엘라스틱 IP는 삭제하지 않는 한 소유할 수 있는 퍼블릭 IPv4 주소입니다.  
→ 사용자 계정에 귀속됨.

It can be attached to only one instance at a time.  
한 번에 한 인스턴스에만 연결할 수 있습니다.  
→ 중복 불가, 단일 바인딩.

Elastic IPs allow you to mask instance or software failures by quickly moving the IP from one instance to another.  
엘라스틱 IP를 통해 한 인스턴스에서 다른 인스턴스로 IP를 빠르게 이동시켜 장애를 가릴 수 있습니다.  
→ 무중단 서비스에 활용.

However, Elastic IPs are limited to five per AWS account by default, and this limit can be increased upon request.  
그러나 엘라스틱 IP는 기본적으로 계정당 5개로 제한되며, 요청 시 늘릴 수 있습니다.  
→ 남용 방지.

Their use is generally discouraged as they often represent poor architectural decisions.  
엘라스틱 IP는 종종 잘못된 아키텍처 설계를 의미하기 때문에 일반적으로 사용을 권장하지 않습니다.  
→ AWS Best Practice는 DNS 권장.

Instead, it is recommended to use random public IPs with DNS names assigned to them.  
대신 임의의 퍼블릭 IP에 DNS 이름을 할당해 사용하는 것이 권장됩니다.  
→ Route 53 같은 DNS 서비스 활용.

Alternatively, using a Load Balancer without public IPs is considered the best practice in AWS.  
또는 퍼블릭 IP 없이 로드 밸런서를 사용하는 것이 AWS의 모범 사례로 간주됩니다.  
→ 고가용성 + 확장성 확보.

---

## Hands-On Overview  
## 실습 개요  
→ 직접 관찰할 부분.

By default, an EC2 machine comes with a private IP for the internal AWS network and a public IP for the World Wide Web.  
기본적으로 EC2 머신은 내부 AWS 네트워크용 프라이빗 IP와 월드와이드웹용 퍼블릭 IP를 가집니다.  
→ 기본적으로 두 가지 다 할당됨.

When connecting via SSH to an EC2 instance, you cannot use the private IP unless you are on the same network or connected through a VPN.  
EC2 인스턴스에 SSH로 연결할 때 같은 네트워크나 VPN을 사용하지 않으면 프라이빗 IP를 사용할 수 없습니다.  
→ 외부에서는 퍼블릭 IP로만 접속 가능.

Without a VPN, the public IP must be used.  
VPN이 없으면 퍼블릭 IP를 반드시 사용해야 합니다.  
→ AWS 콘솔에서 제공되는 퍼블릭 IP 이용.

Note that if the instance is stopped and started, the public IP may change.  
인스턴스를 중지 후 재시작하면 퍼블릭 IP가 변경될 수 있다는 점을 유의하세요.  
→ Elastic IP 필요성 재강조.

We will now observe these behaviors in a hands-on session.  
이제 이러한 동작을 실습에서 관찰해 보겠습니다.  
→ 곧 실습 진행 예정.

---

## Key Takeaways  
## 핵심 요약  
→ 정리 포인트.

- IPv4 is the most common IP format, consisting of four numbers separated by dots, allowing approximately 3.7 billion unique public addresses.  
- IPv4는 네 개의 숫자를 점으로 구분한 가장 일반적인 형식이며, 약 37억 개의 고유 퍼블릭 주소를 제공합니다.  
→ 주소 한정적.

- Public IPs are unique across the internet and allow machines to be accessible globally, while private IPs are unique only within a private network.  
- 퍼블릭 IP는 인터넷 전역에서 고유하며 전 세계 어디서나 접근 가능하지만, 프라이빗 IP는 사설망 내에서만 고유합니다.  
→ 공개 vs 내부 차이.

- Private IPs enable communication within a private network and connect to the internet via NAT devices and internet gateways.  
- 프라이빗 IP는 내부 통신이 가능하며, NAT와 인터넷 게이트웨이를 통해 인터넷에 연결됩니다.  
→ NAT의 역할 중요.

- Elastic IPs are static public IPv4 addresses in AWS that can be reassigned to different instances but are limited in number and generally discouraged in favor of DNS or load balancers.  
- 엘라스틱 IP는 고정 퍼블릭 IPv4 주소로 재할당 가능하지만 개수 제한이 있으며, 일반적으로 DNS나 로드 밸런서 사용이 권장됩니다.  
→ Best Practice: DNS/Load Balancer 활용.
