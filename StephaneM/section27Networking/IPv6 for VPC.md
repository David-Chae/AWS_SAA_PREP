```markdown
# IPv6 for VPC  
# VPC용 IPv6  

🎮 게임보상: "IPv6 Explorer Badge" +500 XP  

---

## Introduction to IPv6  
## IPv6 소개  

We have discussed IPv4 extensively in this course. Now, let's focus on IPv6.  
이 과정에서 우리는 IPv4를 광범위하게 다루었습니다. 이제 IPv6에 집중해봅시다.  

The reason for this shift is that IPv4 was originally designed to provide approximately 4.3 billion addresses at the time of its creation.  
이 전환의 이유는 IPv4가 처음 설계될 당시 약 43억 개의 주소만 제공하도록 설계되었기 때문입니다.  

The engineers who developed this protocol never anticipated that all these addresses would be used up, but it turned out that very soon, they would be exhausted.  
이 프로토콜을 개발한 엔지니어들은 이 주소들이 모두 사용될 것이라고 예상하지 못했지만, 곧 주소가 고갈될 것임이 밝혀졌습니다.  

Therefore, a new IP addressing scheme was necessary, which is IPv6, the successor to IPv4.  
따라서 새로운 IP 주소 체계가 필요했으며, 그것이 IPv4의 후속인 IPv6입니다.  

IPv6 is designed to provide, wait for it, 3.4×10^38 unique IP addresses. This is an enormous number of IP addresses.  
IPv6는 무려 3.4×10^38개의 고유 IP 주소를 제공하도록 설계되었습니다. 이는 엄청난 수의 IP 주소입니다.  

In AWS, every IPv6 address is public and internet-routable.  
AWS에서 모든 IPv6 주소는 공개적이며 인터넷에서 라우팅 가능합니다.  

The IPv6 address format consists of eight groups of hexadecimal numbers, each group separated by colons. Each group ranges from 0000 to ffff.  
IPv6 주소 형식은 16진수 숫자 8개 그룹으로 구성되며, 각 그룹은 콜론으로 구분됩니다. 각 그룹은 0000부터 ffff까지의 값을 가집니다.  

You do not need to memorize exactly how an IPv6 address is formed, but here are some examples to give you an idea of what an IPv6 address looks like.  
IPv6 주소가 정확히 어떻게 형성되는지 암기할 필요는 없지만, 주소 형태를 이해할 수 있도록 몇 가지 예시를 보여드립니다.  

IPv6 addresses can take multiple forms.  
IPv6 주소는 여러 형태를 가질 수 있습니다.  

---

## IPv6 in AWS VPCs  
## AWS VPC에서의 IPv6  

Why is IPv6 important? Because we can enable IPv6 support in our Virtual Private Cloud (VPC).  
IPv6가 중요한 이유는 VPC에서 IPv6 지원을 활성화할 수 있기 때문입니다.  

IPv4 can never be disabled for your VPC and subnets, but you can enable IPv6, which are public IP addresses, to operate in dual-stack mode.  
VPC와 서브넷에서는 IPv4를 비활성화할 수 없지만, 공개 IP인 IPv6를 활성화하여 듀얼 스택 모드로 운영할 수 있습니다.  

This means that your EC2 instances launched in your VPC will have at least a private internal IPv4 address and a public IPv6 address.  
즉, VPC에서 시작된 EC2 인스턴스는 최소한 내부용 IPv4 주소와 공개용 IPv6 주소를 갖게 됩니다.  

They can communicate using either IPv4 or IPv6 to the internet through an internet gateway.  
인스턴스는 인터넷 게이트웨이를 통해 IPv4 또는 IPv6를 사용해 인터넷과 통신할 수 있습니다.  

For example, an EC2 instance has a private IPv4 address and a public IPv6 address by default.  
예를 들어, EC2 인스턴스는 기본적으로 내부 IPv4 주소와 공개 IPv6 주소를 가집니다.  

If it wants to access the internet, it can do so through the internet gateway.  
인터넷에 접속하려면 인터넷 게이트웨이를 통해 가능합니다.  

The internet gateway provides connectivity for both IPv4 and IPv6.  
인터넷 게이트웨이는 IPv4와 IPv6 모두에 대한 연결을 제공합니다.  

Consequently, the EC2 instance will be publicly accessible because it has a public IPv6 address, and the internet gateway facilitates internet connectivity.  
결과적으로, EC2 인스턴스는 공개 IPv6 주소를 가지고 있으며, 인터넷 게이트웨이가 인터넷 연결을 가능하게 하기 때문에 공개적으로 접근 가능합니다.  

---

## IPv6 Troubleshooting Scenario  
## IPv6 문제 해결 시나리오  

Here is an exam scenario related to IPv6 troubleshooting.  
다음은 IPv6 문제 해결과 관련된 시험 시나리오입니다.  

As mentioned, IPv4 cannot be disabled for your VPC and subnets.  
앞서 언급했듯이, VPC와 서브넷에서는 IPv4를 비활성화할 수 없습니다.  

If you have an IPv6-enabled VPC and cannot launch an EC2 instance in your subnets, it is not because the instance cannot acquire an IPv6 address.  
IPv6가 활성화된 VPC에서 서브넷에 EC2 인스턴스를 시작할 수 없다면, 이는 인스턴스가 IPv6 주소를 얻지 못해서가 아닙니다.  

The IPv6 address space is very large, and there will be enough IPv6 addresses for your EC2 instances.  
IPv6 주소 공간은 매우 크므로, EC2 인스턴스에 충분한 IPv6 주소가 제공됩니다.  

Instead, the issue is that there are no available IPv4 addresses left in your subnets.  
문제는 서브넷 내 사용 가능한 IPv4 주소가 남아 있지 않다는 것입니다.  

The solution is to create an IPv4 CIDR block in your subnet.  
해결 방법은 서브넷에 IPv4 CIDR 블록을 추가하는 것입니다.  

Consider a VPC that has both IPv4 and IPv6 address spaces.  
IPv4와 IPv6 주소 공간을 모두 가진 VPC를 가정해봅시다.  

You continue launching EC2 instances that receive private IPv4 and public IPv6 addresses.  
계속해서 내부 IPv4와 공개 IPv6 주소를 받는 EC2 인스턴스를 시작합니다.  

Once the IPv4 address space is exhausted, if a user tries to create a new EC2 instance, they will receive an error.  
IPv4 주소 공간이 고갈되면, 사용자가 새 EC2 인스턴스를 생성하려고 하면 오류가 발생합니다.  

This error is not due to running out of IPv6 addresses but because the IPv4 address space within the subnets or VPC has been depleted.  
이 오류는 IPv6 주소 부족 때문이 아니라, 서브넷 또는 VPC 내 IPv4 주소 공간이 고갈되었기 때문입니다.  

In such a case, you add a new IPv4 CIDR block within your VPC and subnets.  
이 경우, VPC와 서브넷에 새로운 IPv4 CIDR 블록을 추가합니다.  

This allows you to start launching new EC2 instances that will receive IPv4 addresses from the new range.  
이렇게 하면 새 IPv4 범위에서 주소를 받아 새로운 EC2 인스턴스를 시작할 수 있습니다.  

This approach helps you work around the IPv4 exhaustion issue.  
이 방법은 IPv4 고갈 문제를 해결하는 데 도움이 됩니다.  

---

## Conclusion  
## 결론  

That concludes the theory on IPv6 in AWS.  
이로써 AWS에서의 IPv6 이론 설명을 마칩니다.  

In the next lecture, we will engage in a practical session to reinforce this knowledge.  
다음 강의에서는 이 지식을 강화하기 위해 실습 세션을 진행할 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- IPv6 was introduced as a successor to IPv4 due to IPv4 address exhaustion.  
- IPv4 주소 고갈 문제로 IPv4의 후속으로 IPv6가 도입되었습니다.  

- IPv6 provides approximately 3.4×10^38 unique IP addresses, all public and internet-routable in AWS.  
- IPv6는 약 3.4×10^38개의 고유 IP 주소를 제공하며, AWS에서 모두 공개적이고 인터넷에서 라우팅 가능합니다.  

- VPCs in AWS operate in dual-stack mode, supporting both IPv4 and IPv6 simultaneously.  
- AWS의 VPC는 듀얼 스택 모드로 운영되어 IPv4와 IPv6를 동시에 지원합니다.  

- IPv4 addresses cannot be disabled in VPCs; running out of IPv4 addresses in subnets can prevent launching new EC2 instances even if IPv6 addresses are available.  
- VPC에서 IPv4는 비활성화할 수 없으며, 서브넷에서 IPv4 주소가 부족하면 IPv6 주소가 있어도 새 EC2 인스턴스 시작이 불가능합니다.  
```
