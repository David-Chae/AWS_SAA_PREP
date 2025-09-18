```markdown
# NACL & Security Groups  
# NACL 및 보안 그룹  

🎮 게임보상: "Network Guardian" +500 XP  

---

## Introduction to Security Groups and Network ACLs (NACLs)  
## 보안 그룹과 네트워크 ACL(NACL) 소개  

In this lecture, we will explore Security Groups and Network ACLs, commonly referred to as NACLs.  
이번 강의에서는 보안 그룹(Security Groups)과 네트워크 ACL(Network ACL, NACL)에 대해 살펴봅니다.  

To understand their roles, let's consider an example involving a subnet and an EC2 instance.  
역할을 이해하기 위해, 서브넷과 EC2 인스턴스를 포함한 예제를 살펴보겠습니다.  

We know that a security group is attached to an EC2 instance, but there is an additional level of protection at the subnet level, which is the network ACL or NACL.  
보안 그룹은 EC2 인스턴스에 연결되어 있지만, 서브넷 수준에서도 추가적인 보호가 존재하며, 이를 네트워크 ACL(NACL)이라고 합니다.  

---

## Role of NACLs in Incoming Requests  
## NACL의 수신 요청 역할  

When a request is sent to your EC2 instance, from a network perspective, the request first reaches the NACL before entering the subnet.  
EC2 인스턴스로 요청이 들어올 때, 네트워크 관점에서 요청은 서브넷에 도달하기 전에 먼저 NACL을 통과합니다.  

The NACL has inbound rules defined, and if the request is not allowed by these rules, it is denied and does not proceed further.  
NACL에는 인바운드 규칙이 정의되어 있으며, 규칙에 따라 허용되지 않으면 요청이 거부되고 더 이상 진행되지 않습니다.  

If the request is allowed, it passes through to the subnet.  
요청이 허용되면 서브넷으로 전달됩니다.  

The NACL is stateless, meaning it does not keep track of connection states.  
NACL은 상태 비저장(stateless)이므로 연결 상태를 추적하지 않습니다.  

After passing the NACL, the request then reaches the security group inbound rules associated with the EC2 instance.  
NACL을 통과한 후, 요청은 EC2 인스턴스와 연결된 보안 그룹의 인바운드 규칙으로 전달됩니다.  

If the security group does not explicitly allow the request, it is denied.  
보안 그룹에서 명시적으로 요청을 허용하지 않으면 요청이 거부됩니다.  

---

## Stateful vs Stateless: Security Groups and NACLs  
## 상태 저장 vs 상태 비저장: 보안 그룹과 NACL  

Security groups are stateful, whereas NACLs are stateless.  
보안 그룹은 상태 저장(stateful)이며, NACL은 상태 비저장(stateless)입니다.  

This means that when a request passes through the inbound rules of a security group and reaches the EC2 instance, the instance can reply to the request.  
즉, 요청이 보안 그룹의 인바운드 규칙을 통과하여 EC2 인스턴스에 도달하면, 인스턴스가 요청에 응답할 수 있습니다.  

The outbound response is automatically allowed by the security group without evaluating outbound rules.  
보안 그룹은 아웃바운드 규칙을 평가하지 않고도 자동으로 응답 트래픽을 허용합니다.  

This is because the security group remembers the state of the connection.  
이는 보안 그룹이 연결 상태를 기억하기 때문입니다.  

In contrast, since NACLs are stateless, outbound rules are evaluated separately.  
반대로 NACL은 상태 비저장이므로 아웃바운드 규칙이 별도로 평가됩니다.  

If the outbound rules do not allow the response traffic, the response will be denied.  
아웃바운드 규칙이 응답 트래픽을 허용하지 않으면, 응답이 거부됩니다.  

---

## Outgoing Requests and Rule Evaluation  
## 발신 요청과 규칙 평가  

For outgoing requests initiated by the EC2 instance, such as connecting to www.google.com, the security group outbound rules are evaluated first to determine if the traffic is allowed out.  
EC2 인스턴스가 www.google.com과 같은 외부로 요청을 보낼 때, 먼저 보안 그룹 아웃바운드 규칙이 평가되어 트래픽이 허용되는지 확인합니다.  

If allowed, the request then passes through the NACL outbound rules.  
허용되면 요청은 NACL의 아웃바운드 규칙을 통과합니다.  

The request reaches the external destination, and when the response returns, the NACL inbound rules are evaluated because the NACL is stateless.  
요청이 외부 목적지에 도달하고 응답이 돌아올 때, NACL이 상태 비저장이므로 NACL의 인바운드 규칙이 평가됩니다.  

The security group inbound rules will allow the response automatically due to their stateful nature, so they do not affect the incoming response traffic in this scenario.  
보안 그룹은 상태 저장이므로 응답 트래픽을 자동으로 허용하며, 이 시나리오에서는 인바운드 응답 트래픽에 영향을 주지 않습니다.  

---

## Understanding Network Access Control Lists (NACLs)  
## 네트워크 접근 제어 목록(NACL) 이해  

NACLs act like firewalls controlling traffic to and from subnets.  
NACL은 서브넷으로 들어오고 나가는 트래픽을 제어하는 방화벽 역할을 합니다.  

Each subnet has one NACL associated with it, and new subnets are assigned the default NACL by default.  
각 서브넷에는 하나의 NACL이 연결되며, 새 서브넷은 기본적으로 기본 NACL이 할당됩니다.  

NACL rules are numbered from 1 to 32,000, where a lower number indicates higher precedence.  
NACL 규칙은 1부터 32,000까지 번호가 지정되며, 낮은 번호일수록 우선순위가 높습니다.  

The first matching rule determines whether the traffic is allowed or denied.  
첫 번째로 일치하는 규칙이 트래픽 허용 여부를 결정합니다.  

For example, if an allow rule has a priority of 100 and a deny rule for the same IP has a priority of 200, the allow rule takes precedence, and the traffic is permitted.  
예를 들어, 허용 규칙이 우선순위 100이고 같은 IP에 대한 거부 규칙이 200이면, 허용 규칙이 우선되어 트래픽이 허용됩니다.  

The default rule at the end denies all traffic if no other rules match.  
마지막 기본 규칙은 다른 규칙과 일치하지 않으면 모든 트래픽을 거부합니다.  

AWS recommends adding rules in increments of 100 to allow for easy insertion of new rules between existing ones.  
AWS는 기존 규칙 사이에 새 규칙을 쉽게 추가할 수 있도록 규칙 번호를 100 단위로 설정하는 것을 권장합니다.  

---

## Default NACL Behavior  
## 기본 NACL 동작  

Newly created NACLs deny all traffic by default.  
새로 생성된 NACL은 기본적으로 모든 트래픽을 거부합니다.  

However, the default NACL is an exception; it allows all inbound and outbound IPv4 traffic for the subnets it is associated with.  
하지만 기본 NACL은 예외로, 연결된 서브넷에 대해 모든 인바운드 및 아웃바운드 IPv4 트래픽을 허용합니다.  

This openness prevents initial connectivity issues when starting with AWS.  
이 개방성 덕분에 AWS 초기 사용 시 연결 문제를 방지할 수 있습니다.  

It is recommended not to modify the default NACL.  
기본 NACL은 수정하지 않는 것이 권장됩니다.  

Instead, create custom NACLs for specific security requirements.  
대신 특정 보안 요구사항에 맞는 커스텀 NACL을 생성하세요.  

If the exam mentions the default NACL, remember that it allows all inbound and outbound traffic for its associated subnets.  
시험에서 기본 NACL이 언급되면, 연결된 서브넷의 모든 인바운드 및 아웃바운드 트래픽을 허용한다는 점을 기억하세요.  

---

## Ephemeral Ports and Their Importance  
## 임시 포트(Ephemeral Port)와 중요성  

When a client connects to a server, both use IP addresses and ports.  
클라이언트가 서버에 연결할 때, 양쪽 모두 IP 주소와 포트를 사용합니다.  

Servers listen on well-known ports such as 80 for HTTP, 443 for HTTPS, and 22 for SSH.  
서버는 HTTP 80, HTTPS 443, SSH 22 등 잘 알려진 포트에서 수신합니다.  

Clients connect to these defined server ports.  
클라이언트는 이 정의된 서버 포트에 연결합니다.  

However, clients do not have open ports by default.  
하지만 클라이언트는 기본적으로 포트가 열려 있지 않습니다.  

When initiating a connection, a client opens an ephemeral port, which is a temporary port assigned for the duration of the connection.  
연결을 시작할 때, 클라이언트는 임시 포트를 열며, 연결 기간 동안 할당되는 임시 포트입니다.  

The range of ephemeral ports varies by operating system.  
임시 포트 범위는 운영체제마다 다릅니다.  

For example, Windows 10 uses ports from 49152 to 65535, while Linux typically uses ports from 32768 to 60999.  
예를 들어, Windows 10은 49152~65535, Linux는 일반적으로 32768~60999 포트를 사용합니다.  

The client sends its source IP and ephemeral port to the server, which uses this information to send the response back to the client on the same ephemeral port.  
클라이언트는 자신의 소스 IP와 임시 포트를 서버에 보내고, 서버는 동일한
```


임시 포트를 사용하여 응답을 클라이언트에 반환합니다.

---

## Example: Client-Server Communication and NACL Rules

## 예제: 클라이언트-서버 통신과 NACL 규칙

Consider a client connecting to a database in a private subnet, with a web subnet and a database subnet each having their own NACLs.
프라이빗 서브넷의 데이터베이스에 연결하는 클라이언트를 고려하며, 웹 서브넷과 데이터베이스 서브넷 각각은 자체 NACL을 가지고 있습니다.

When the client initiates a connection to the database on port 3306, the web subnet's NACL must allow outbound TCP traffic on port 3306 to the database subnet's CIDR block.
클라이언트가 3306 포트로 데이터베이스에 연결할 때, 웹 서브넷의 NACL은 데이터베이스 서브넷의 CIDR로 3306 포트 TCP 아웃바운드 트래픽을 허용해야 합니다.

Similarly, the database subnet's NACL must allow inbound TCP traffic on port 3306 from the web subnet's CIDR block.
마찬가지로, 데이터베이스 서브넷의 NACL은 웹 서브넷 CIDR로부터 3306 포트 TCP 인바운드 트래픽을 허용해야 합니다.

For the database to send the response back to the client, the database subnet's NACL must allow outbound TCP traffic on the ephemeral port range (e.g., 1024 to 65535) to the web subnet's CIDR.
데이터베이스가 클라이언트에 응답을 보내려면, 데이터베이스 서브넷의 NACL은 임시 포트 범위(예: 1024\~65535) TCP 아웃바운드를 웹 서브넷 CIDR로 허용해야 합니다.

Correspondingly, the web subnet's NACL must allow inbound TCP traffic on the ephemeral port range from the database subnet's CIDR.
마찬가지로, 웹 서브넷의 NACL은 데이터베이스 서브넷 CIDR로부터 임시 포트 범위 TCP 인바운드를 허용해야 합니다.

This example highlights the importance of correctly configuring ephemeral port ranges in NACLs to allow return traffic.
이 예제는 NACL에서 임시 포트 범위를 올바르게 구성하여 반환 트래픽을 허용하는 것이 중요함을 보여줍니다.

---

## Managing Multiple NACLs and Subnets

## 다중 NACL과 서브넷 관리

When multiple NACLs and subnets are involved, each NACL combination must be allowed within the rules.
다수의 NACL과 서브넷이 관련된 경우, 각 NACL 조합이 규칙 내에서 허용되어야 합니다.

Since NACLs use CIDR blocks, and each subnet has its own CIDR, it is essential to update all relevant NACL rules to ensure that the combinations of connections between subnets are permitted.
NACL은 CIDR 블록을 사용하고, 각 서브넷은 자체 CIDR을 가지므로, 서브넷 간 연결 조합이 허용되도록 모든 관련 NACL 규칙을 업데이트하는 것이 중요합니다.

---

## Summary: Differences Between Security Groups and NACLs

## 요약: 보안 그룹과 NACL의 차이점

* Security groups operate at the instance level, while NACLs operate at the subnet level.

* 보안 그룹은 인스턴스 수준에서 작동하며, NACL은 서브넷 수준에서 작동합니다.

* Security groups support allow rules only; NACLs support both allow and deny rules, enabling blocking of specific IP addresses.

* 보안 그룹은 허용 규칙만 지원하며, NACL은 허용 및 거부 규칙 모두를 지원하여 특정 IP를 차단할 수 있습니다.

* Security groups are stateful, automatically allowing return traffic regardless of rules; NACLs are stateless, requiring evaluation of inbound and outbound rules separately.

* 보안 그룹은 상태 저장이므로 규칙과 상관없이 반환 트래픽을 자동으로 허용하며, NACL은 상태 비저장이므로 인바운드 및 아웃바운드 규칙을 별도로 평가해야 합니다.

* For security groups, all rules are evaluated to decide whether to allow traffic; for NACLs, the rule with the highest priority (lowest number) that matches is applied first.

* 보안 그룹은 모든 규칙을 평가하여 트래픽 허용 여부를 결정하며, NACL은 일치하는 규칙 중 우선순위가 가장 높은(번호가 가장 낮은) 규칙이 먼저 적용됩니다.

* Security groups apply to specific EC2 instances as assigned; NACLs apply to all EC2 instances within the associated subnet.

* 보안 그룹은 지정된 EC2 인스턴스에 적용되고, NACL은 연결된 서브넷 내 모든 EC2 인스턴스에 적용됩니다.

---

## Conclusion

## 결론

This concludes the lecture on Security Groups and Network ACLs.
이번 강의는 보안 그룹과 NACL에 대한 강의를 마칩니다.

Understanding the distinctions between stateful security groups and stateless NACLs, as well as the importance of ephemeral ports, is crucial for effective network security management in AWS environments.
상태 저장 보안 그룹과 상태 비저장 NACL의 차이, 그리고 임시 포트의 중요성을 이해하는 것은 AWS 환경에서 효과적인 네트워크 보안 관리에 매우 중요합니다.

---

## Key Takeaways

## 핵심 요약

* Network ACLs (NACLs) provide an additional stateless layer of security at the subnet level, while security groups are stateful and operate at the instance level.

* NACL은 서브넷 수준에서 상태 비저장 추가 보안 계층을 제공하며, 보안 그룹은 상태 저장이며 인스턴스 수준에서 작동합니다.

* NACLs evaluate inbound and outbound rules separately for each request, requiring explicit rules for both directions, especially considering ephemeral ports.

* NACL은 요청별로 인바운드와 아웃바운드 규칙을 별도로 평가하며, 특히 임시 포트를 고려하여 양방향 규칙을 명시해야 합니다.

* Security groups automatically allow return traffic due to their stateful nature, simplifying rule management for EC2 instances.

* 보안 그룹은 상태 저장이므로 반환 트래픽을 자동으로 허용하며, EC2 인스턴스 규칙 관리를 단순화합니다.

* Proper configuration of ephemeral port ranges in NACLs is crucial for allowing return traffic between subnets, especially in multi-subnet architectures.

* 다중 서브넷 아키텍처에서 NACL의 임시 포트 범위를 올바르게 구성하는 것은 서브넷 간 반환 트래픽 허용에 매우 중요합니다.

```
