```markdown
# AWS Network Firewall  
# AWS 네트워크 방화벽  

🎮 게임보상: "AWS Firewall Defender" +550 XP  

---

## Overview of AWS Network Protection Options  
## AWS 네트워크 보호 옵션 개요  

So far, we have explored several ways to protect your network on AWS.  
지금까지 AWS에서 네트워크를 보호하는 여러 방법을 살펴보았습니다.  

These include Network Access Control Lists, Amazon VPC security groups, and AWS WAF.  
여기에는 네트워크 ACL, Amazon VPC 보안 그룹, AWS WAF가 포함됩니다.  

AWS WAF protects against malicious HTTP requests targeting specific services.  
AWS WAF는 특정 서비스를 대상으로 하는 악성 HTTP 요청으로부터 보호합니다.  

Additionally, AWS Shield and Shield Advanced provide protection against Distributed Denial of Service (DDoS) attacks.  
또한 AWS Shield 및 Shield Advanced는 분산 서비스 거부(DDoS) 공격으로부터 보호합니다.  

AWS Firewall Manager helps manage rules for WAF, Shield, and other services across multiple accounts.  
AWS Firewall Manager는 WAF, Shield 및 기타 서비스 규칙을 여러 계정에서 관리할 수 있도록 도와줍니다.  

---

## Introducing AWS Network Firewall  
## AWS 네트워크 방화벽 소개  

What if you want to protect your entire VPC in a sophisticated manner?  
전체 VPC를 정교하게 보호하고 싶다면 어떻게 해야 할까요?  

This is where AWS Network Firewall comes in.  
바로 이때 AWS Network Firewall이 등장합니다.  

It is designed to protect your entire VPC with a firewall that surrounds it completely.  
이 방화벽은 VPC 전체를 완전히 둘러싸며 보호하도록 설계되었습니다.  

The AWS Network Firewall provides protection from layer 3 through layer 7.  
AWS Network Firewall은 3계층부터 7계층까지 보호를 제공합니다.  

This means you can inspect any kind of traffic in any direction, including VPC to VPC traffic, outbound traffic to the internet, inbound traffic from the internet, and traffic to and from Direct Connect and Site-to-Site VPN connections.  
즉, VPC 간 트래픽, 인터넷으로 나가는 아웃바운드 트래픽, 인터넷에서 들어오는 인바운드 트래픽, Direct Connect 및 Site-to-Site VPN 트래픽 등 모든 방향의 트래픽을 검사할 수 있습니다.  

---

## Traffic Coverage  
## 트래픽 범위  

The firewall protects all traffic coming in and out of the internet, peered VPCs, Direct Connect, and Site-to-Site VPN connections.  
이 방화벽은 인터넷, 피어링 VPC, Direct Connect, Site-to-Site VPN 트래픽의 모든 인바운드 및 아웃바운드 트래픽을 보호합니다.  

You define rules to control all network activity within these scopes.  
사용자는 이러한 범위 내 모든 네트워크 활동을 제어하기 위해 규칙을 정의할 수 있습니다.  

---

## Architecture and Management  
## 아키텍처 및 관리  

Internally, AWS Network Firewall uses the AWS Gateway Load Balancer.  
AWS Network Firewall 내부적으로 AWS Gateway Load Balancer를 사용합니다.  

Instead of setting up third-party appliances to inspect traffic, AWS manages its own appliances for this purpose.  
트래픽을 검사하기 위해 서드파티 장치를 설정하는 대신, AWS가 자체 장치를 관리합니다.  

This allows you to have your own firewall rules while relying on AWS-managed infrastructure.  
이를 통해 AWS 관리 인프라를 활용하면서 사용자가 자체 방화벽 규칙을 설정할 수 있습니다.  

These firewall rules can also be centrally managed across multiple accounts and many VPCs using the AWS Firewall Manager service.  
이 방화벽 규칙은 AWS Firewall Manager 서비스를 사용하여 여러 계정과 VPC에서 중앙 관리할 수도 있습니다.  

---

## Fine-Grained Control  
## 세부 규칙 제어  

AWS Network Firewall supports thousands of rules at the VPC level.  
AWS Network Firewall은 VPC 수준에서 수천 개의 규칙을 지원합니다.  

You can filter traffic by IP address and port, supporting tens of thousands of IPs.  
IP 주소와 포트별로 트래픽을 필터링할 수 있으며, 수만 개의 IP를 지원합니다.  

Protocol filtering is also available; for example, you can disable the SMB protocol for outbound communication.  
프로토콜 필터링도 가능하며, 예를 들어 아웃바운드 통신에서 SMB 프로토콜을 비활성화할 수 있습니다.  

Domain-level filtering is supported as well.  
도메인 수준 필터링도 지원됩니다.  

For instance, you can allow outbound traffic only to your corporate domain or to approved third-party software repositories.  
예를 들어, 아웃바운드 트래픽을 기업 도메인이나 승인된 서드파티 소프트웨어 저장소로만 허용할 수 있습니다.  

General pattern matching with regular expressions is also possible.  
정규 표현식을 사용한 일반 패턴 매칭도 가능합니다.  

You can configure the firewall to allow, drop, or alert on traffic that matches the rules you have set up.  
설정한 규칙에 맞는 트래픽을 허용, 차단 또는 알림으로 설정할 수 있습니다.  

---

## Intrusion Prevention and Logging  
## 침입 방지 및 로깅  

AWS Network Firewall includes active flow inspection, providing intrusion prevention capabilities similar to those available with the Gateway Load Balancer, but fully managed by AWS.  
AWS Network Firewall은 능동적 플로우 검사를 포함하며, Gateway Load Balancer에서 제공하는 것과 유사한 침입 방지 기능을 AWS가 완전히 관리합니다.  

All rule matches can be sent to Amazon S3, CloudWatch Logs, and Kinesis Data Firehose for further analysis and monitoring.  
모든 규칙 일치 항목은 Amazon S3, CloudWatch Logs, Kinesis Data Firehose로 전송하여 추가 분석 및 모니터링이 가능합니다.  

---

## Summary  
## 요약  

In summary, AWS Network Firewall is a firewall service implemented at the VPC level.  
요약하면, AWS Network Firewall은 VPC 수준에서 구현된 방화벽 서비스입니다.  

It enables traffic filtering and flow inspection with fine-grained control and centralized management.  
세부 규칙 제어와 중앙 관리 기능으로 트래픽 필터링과 플로우 검사를 수행할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Network Firewall protects entire VPCs with sophisticated, layer 3 to layer 7 traffic inspection.  
- AWS Network Firewall은 정교한 3~7계층 트래픽 검사를 통해 VPC 전체를 보호합니다.  

- It supports inspection of traffic in all directions: VPC to VPC, outbound to internet, inbound from internet, Direct Connect, and Site-to-Site VPN.  
- 모든 방향의 트래픽 검사 지원: VPC 간, 인터넷 아웃바운드, 인터넷 인바운드, Direct Connect, Site-to-Site VPN.  

- The firewall uses AWS Gateway Load Balancer with AWS-managed appliances, eliminating the need for third-party devices.  
- AWS 관리 장치와 함께 AWS Gateway Load Balancer를 사용하므로 서드파티 장치가 필요 없습니다.  

- Fine-grained control is available with thousands of rules filtering by IP, port, protocol, domain, and pattern matching, with options to allow, drop, or alert on traffic.  
- 수천 개 규칙으로 IP, 포트, 프로토콜, 도메인, 패턴 매칭을 통한 세부 제어 가능하며 트래픽 허용, 차단, 알림 설정 가능.  

- Rule matches can be logged and analyzed via Amazon S3, CloudWatch Logs, and Kinesis Data Firehose.  
- 규칙 일치 항목은 Amazon S3, CloudWatch Logs, Kinesis Data Firehose로 로깅 및 분석 가능.  

- AWS Firewall Manager enables centralized management of firewall rules across multiple accounts and VPCs.  
- AWS Firewall Manager를 통해 여러 계정과 VPC에 걸쳐 방화벽 규칙을 중앙 관리할 수 있습니다.  
```
