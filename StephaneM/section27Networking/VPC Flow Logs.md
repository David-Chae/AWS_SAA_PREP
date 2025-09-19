```markdown
# VPC Flow Logs  
# VPC 플로우 로그  

🎮 게임보상: "Flow Log Explorer Badge" +500 XP  

---

## Introduction to VPC Flow Logs  
## VPC 플로우 로그 소개  

VPC Flow Logs allow you to capture information from IP traffic going into interfaces.  
VPC 플로우 로그는 인터페이스로 들어오는 IP 트래픽 정보를 캡처할 수 있게 해줍니다.  

These interfaces can be at the VPC level, the subnet level, or the Elastic Network Interface (ENI) level.  
이 인터페이스는 VPC 수준, 서브넷 수준, 또는 Elastic Network Interface(ENI) 수준일 수 있습니다.  

There are three kinds of Flow Logs available.  
플로우 로그에는 세 가지 유형이 있습니다.  

They are very helpful to monitor and troubleshoot connectivity issues occurring within a VPC.  
이는 VPC 내에서 발생하는 연결 문제를 모니터링하고 문제 해결하는 데 매우 유용합니다.  

---

These logs can be sent to Amazon S3, CloudWatch Logs, and Kinesis Data Firehose.  
이 로그는 Amazon S3, CloudWatch Logs, Kinesis Data Firehose로 전송할 수 있습니다.  

They capture information for AWS managed interfaces such as Elastic Load Balancer (ELB), RDS, ElastiCache, Redshift, WorkSpaces, your NAT gateway, transit gateway, and so on.  
이 로그는 ELB, RDS, ElastiCache, Redshift, WorkSpaces, NAT 게이트웨이, 트랜짓 게이트웨이 등 AWS 관리 인터페이스의 정보를 캡처합니다.  

---

## Structure of a VPC Flow Log  
## VPC 플로우 로그 구조  

A VPC Flow Log has a specific format that includes fields such as version, account ID, interface ID, source address, destination address, source port, destination port, protocol, packets, bytes, start time, end time, action, and log status.  
VPC 플로우 로그는 버전, 계정 ID, 인터페이스 ID, 출발지/목적지 주소, 출발지/목적지 포트, 프로토콜, 패킷, 바이트, 시작/종료 시간, 액션, 로그 상태 등 특정 형식의 필드를 포함합니다.  

This metadata provides detailed information about the network packets going into your VPC.  
이 메타데이터는 VPC로 들어오는 네트워크 패킷에 대한 상세 정보를 제공합니다.  

---

## Key Information in Flow Logs  
## 플로우 로그의 주요 정보  

Source Address and Destination Address help identify problematic IPs.  
출발지 주소와 목적지 주소는 문제가 있는 IP를 식별하는 데 도움이 됩니다.  

For example, if an IP is repeatedly denied, it may indicate an issue or a potential attack from that IP.  
예를 들어, IP가 반복적으로 거부된다면 문제가 있거나 잠재적인 공격일 수 있습니다.  

Source Port and Destination Port help identify problematic ports.  
출발지 및 목적지 포트는 문제가 있는 포트를 식별하는 데 도움이 됩니다.  

Action indicates whether the traffic was accepted or rejected, reflecting success or failure at the Security Group (SG) or Network Access Control List (NACL) level.  
액션 필드는 트래픽이 허용되었는지 거부되었는지를 나타내며, SG 또는 NACL 수준에서 성공/실패를 반영합니다.  

This information can be used to perform analytics on usage patterns or detect malicious behavior such as port scans.  
이 정보는 사용 패턴 분석이나 포트 스캔과 같은 악성 행위 탐지에 사용할 수 있습니다.  

---

## Querying VPC Flow Logs  
## VPC 플로우 로그 조회  

There are two primary ways to query VPC Flow Logs:  
VPC 플로우 로그를 조회하는 주요 방법은 두 가지입니다.  

- Using Amazon Athena on logs stored in S3 for ad-hoc SQL queries.  
- S3에 저장된 로그를 Amazon Athena로 SQL 쿼리 수행  

- Using CloudWatch Logs Insights for streaming analysis and real-time querying.  
- CloudWatch Logs Insights로 스트리밍 분석 및 실시간 조회  

---

## Troubleshooting Security Group and NACL Issues Using Flow Logs  
## 플로우 로그로 SG 및 NACL 문제 해결  

To troubleshoot issues, focus on the action field in the flow logs.  
문제 해결 시, 플로우 로그의 액션 필드에 주목합니다.  

Remember that NACLs are stateless, whereas Security Groups are stateful.  
NACL은 상태 비저장(stateless)이고, Security Group은 상태 저장(stateful)임을 기억하세요.  

If you observe an inbound reject, it means the inbound request from outside to your EC2 instance was rejected.  
Inbound Reject가 관찰되면, 외부에서 EC2 인스턴스로 들어오는 요청이 거부된 것입니다.  

This could be due to either the NACL or the Security Group refusing the request.  
이는 NACL 또는 SG 중 하나가 요청을 거부했기 때문일 수 있습니다.  

If you see an inbound accept but an outbound reject, it indicates a NACL issue.  
Inbound Accept이지만 Outbound Reject이면 NACL 문제를 나타냅니다.  

This is because Security Groups are stateful; if inbound traffic is allowed, the outbound response is automatically allowed.  
SG는 상태 저장이므로, 인바운드 트래픽이 허용되면 아웃바운드 응답도 자동 허용됩니다.  

Similarly, for outgoing requests:  
마찬가지로 아웃바운드 요청의 경우:  

- An outbound reject indicates either a NACL or Security Group issue.  
- Outbound Reject는 NACL 또는 SG 문제를 나타냅니다.  

- An outbound accept with an inbound reject also points to a NACL issue.  
- Outbound Accept이지만 Inbound Reject이면 NACL 문제입니다.  

---

## Architectures for VPC Flow Logs  
## VPC 플로우 로그 아키텍처  

VPC Flow Logs can be configured to flow into CloudWatch Logs.  
VPC 플로우 로그는 CloudWatch Logs로 흐르도록 구성할 수 있습니다.  

Using CloudWatch Contributor Insights, you can identify the top 10 IP addresses contributing to the most network traffic on your VPC, ENI, or other interfaces.  
CloudWatch Contributor Insights를 사용하면 VPC, ENI, 기타 인터페이스에서 네트워크 트래픽이 가장 많은 상위 10개 IP를 식별할 수 있습니다.  

Additionally, you can set up metric filters in CloudWatch Logs to monitor specific protocols such as SSH or RDP.  
추가로, CloudWatch Logs에서 메트릭 필터를 설정해 SSH, RDP 등 특정 프로토콜을 모니터링할 수 있습니다.  

If there is an unusual increase in these protocols, a CloudWatch alarm can be triggered to send an alert via Amazon SNS, indicating potential suspicious activity on your network.  
이러한 프로토콜이 비정상적으로 증가하면 CloudWatch 알람이 트리거되어 Amazon SNS로 경고를 보내 잠재적인 네트워크 이상 활동을 알릴 수 있습니다.  

Alternatively, VPC Flow Logs can be sent to an S3 bucket for storage.  
또는 VPC 플로우 로그를 S3 버킷으로 전송해 저장할 수 있습니다.  

Using Amazon Athena, you can analyze these logs with SQL queries and visualize the results with Amazon QuickSight for deeper insights.  
Amazon Athena로 SQL 쿼리를 수행하고 Amazon QuickSight로 시각화하여 심층 분석할 수 있습니다.  

---

## Conclusion  
## 결론  

VPC Flow Logs provide valuable metadata about network traffic within your VPC, enabling monitoring, troubleshooting, and security analysis.  
VPC 플로우 로그는 VPC 내 네트워크 트래픽에 대한 귀중한 메타데이터를 제공하여 모니터링, 문제 해결, 보안 분석을 가능하게 합니다.  

By leveraging AWS services such as CloudWatch, Athena, and QuickSight, you can gain comprehensive insights into your network traffic patterns and potential security issues.  
CloudWatch, Athena, QuickSight 등 AWS 서비스를 활용하면 네트워크 트래픽 패턴과 잠재적 보안 문제를 포괄적으로 분석할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- VPC Flow Logs capture IP traffic information at the VPC, subnet, or ENI level to monitor and troubleshoot connectivity.  
- VPC 플로우 로그는 VPC, 서브넷, ENI 수준에서 IP 트래픽 정보를 캡처하여 연결 문제를 모니터링하고 해결  

- Flow Logs include metadata such as source/destination IPs and ports, protocol, action (accept/reject), and log status.  
- 플로우 로그는 출발지/목적지 IP 및 포트, 프로토콜, 액션(허용/거부), 로그 상태 등의 메타데이터 포함  

- Analyzing the action field helps identify security group and NACL issues based on inbound and outbound accept/reject patterns.  
- 액션 필드 분석으로 인바운드/아웃바운드 허용·거부 패턴 기반 SG 및 NACL 문제 식별  

- Flow Logs can be sent to Amazon S3, CloudWatch Logs, or Kinesis Data Firehose for storage and analysis using tools like Athena, CloudWatch Contributor Insights, and QuickSight.  
- 플로우 로그는 S3, CloudWatch Logs, Kinesis Data Firehose로 전송 가능하며 Athena, CloudWatch Contributor Insights, QuickSight로 분석 가능  
```
