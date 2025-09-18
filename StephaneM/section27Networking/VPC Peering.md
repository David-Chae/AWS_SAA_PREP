```markdown
# VPC Peering  
# VPC 피어링  

🎮 게임보상: "Cloud Connector" +500 XP  

---

## Introduction to VPC Peering  
## VPC 피어링 소개  

Let us discuss VPC Peering.  
VPC 피어링에 대해 살펴보겠습니다.  

The idea is that we can create VPCs in different regions or different accounts, and we want to connect them together using the AWS network.  
다른 리전이나 다른 계정에 VPC를 생성하고, AWS 네트워크를 통해 서로 연결할 수 있다는 개념입니다.  

---

## Purpose of VPC Peering  
## VPC 피어링의 목적  

Why do we do this?  
왜 이렇게 할까요?  

We want to make them behave as if they were in the same network.  
서로 마치 같은 네트워크에 있는 것처럼 동작하게 만들고 싶기 때문입니다.  

This can be very specific.  
이 목적은 매우 구체적일 수 있습니다.  

For example, you could have a VPC in another region, in another account, or even within your same account, and you want to connect them.  
예를 들어, 다른 리전, 다른 계정, 또는 같은 계정 내의 VPC를 서로 연결하고 싶을 수 있습니다.  

---

## CIDR Requirements for Peering  
## 피어링을 위한 CIDR 요구사항  

In order for them to connect, remember, the VPC network CIDRs must be distant from each other.  
연결하려면 VPC 네트워크의 CIDR이 서로 겹치지 않아야 합니다.  

When we connect them together, if they have overlapping CIDRs, they will not be able to communicate.  
만약 CIDR이 겹치면 연결해도 통신할 수 없습니다.  

---

## Peering Connections and Transitivity  
## 피어링 연결과 전이성  

VPC peerings can happen between two VPCs, and they are not transitive.  
VPC 피어링은 두 VPC 간에 발생할 수 있으며, 전이(transitive)되지 않습니다.  

That means that each VPC that wants to communicate with another must have VPC peering enabled.  
즉, 서로 통신하려는 각 VPC는 개별적으로 VPC 피어링을 활성화해야 합니다.  

If you have three VPCs, A, B, and C, you can create a peering connection between A and B.  
세 개의 VPC, A, B, C가 있다면 A와 B 사이에 피어링 연결을 만들 수 있습니다.  

This allows you to connect them together.  
이렇게 하면 두 VPC가 서로 연결됩니다.  

You can create another peering connection between VPC B and C, and again, they can communicate together.  
B와 C 사이에도 피어링 연결을 만들면 서로 통신할 수 있습니다.  

However, even though A and B, and B and C, are connected, you still need to enable a VPC peering connection between A and C to have them communicate.  
하지만 A와 B, B와 C가 연결되어 있어도 A와 C가 통신하려면 A와 C 사이에도 피어링 연결을 만들어야 합니다.  

This is very important.  
이는 매우 중요한 포인트입니다.  

---

## Route Table Updates  
## 라우트 테이블 업데이트  

Even though your VPCs are peered with each other, you must also make sure that you update all the route tables in each VPC's subnets to ensure that instances in different VPCs can communicate with each other.  
VPC 간 피어링이 되어 있어도, 각 VPC 서브넷의 라우트 테이블을 업데이트해야 다른 VPC의 인스턴스끼리 통신이 가능합니다.  

---

## Account and Region Flexibility  
## 계정 및 리전 유연성  

VPC peering can happen within your own accounts, but they can also happen across accounts.  
VPC 피어링은 같은 계정 내에서뿐 아니라 다른 계정 간에도 가능합니다.  

If you want to connect a VPC from one account A to account B, you can, and also across regions.  
계정 A의 VPC를 계정 B의 VPC와 연결하거나, 리전을 넘어 연결하는 것도 가능합니다.  

This is very powerful.  
이는 매우 강력한 기능입니다.  

---

## Security Group References Across Peered VPCs  
## 피어링 VPC 간 보안 그룹 참조  

In security groups, we can reference other security groups.  
보안 그룹에서는 다른 보안 그룹을 참조할 수 있습니다.  

It is possible to reference a security group from a peered VPC across accounts in the same region.  
같은 리전의 다른 계정 피어링 VPC의 보안 그룹도 참조할 수 있습니다.  

This is powerful because we do not need to have the source as a CIDR or IP; we can also reference a security group.  
이렇게 하면 출발지 CIDR이나 IP를 따로 지정하지 않아도 되고, 보안 그룹을 참조할 수 있어 강력합니다.  

---

## Networking Diagram and Hands-On  
## 네트워킹 다이어그램 및 실습  

In our networking diagram, we are now going to add a VPC peering connection to connect our VPC to other VPCs.  
우리 네트워킹 다이어그램에서 VPC 피어링 연결을 추가하여 다른 VPC와 연결합니다.  

We will see this in the hands-on section.  
이는 실습 섹션에서 확인할 수 있습니다.  

That concludes the overview of VPC Peering.  
이로써 VPC 피어링 개요를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- VPC Peering allows the connection of VPCs across different regions and accounts using the AWS network.  
- VPC 피어링은 AWS 네트워크를 통해 서로 다른 리전과 계정의 VPC를 연결할 수 있습니다.  

- VPC Peering is not transitive; each pair of VPCs that need to communicate must have a direct peering connection.  
- VPC 피어링은 전이되지 않으므로, 통신이 필요한 VPC 쌍마다 직접 피어링 연결이 필요합니다.  

- Route tables in each VPC's subnets must be updated to enable communication between instances in different VPCs.  
- 다른 VPC의 인스턴스 간 통신을 위해 각 VPC 서브넷의 라우트 테이블을 업데이트해야 합니다.  

- Security groups from a peered VPC can be referenced, even across accounts in the same region.  
- 피어링된 VPC의 보안 그룹은 같은 리전 내 다른 계정에서도 참조할 수 있습니다.  
```
