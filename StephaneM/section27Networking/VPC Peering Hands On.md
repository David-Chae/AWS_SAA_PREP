```markdown
# VPC Peering Hands On  
# VPC 피어링 실습  

🎮 게임보상: "VPC Connector" +500 XP  

---

## Introduction to VPC Peering  
## VPC 피어링 소개  

In this session, we will explore how to peer two Virtual Private Clouds (VPCs) together.  
이번 세션에서는 두 개의 가상 프라이빗 클라우드(VPC)를 피어링하는 방법을 살펴봅니다.  

Specifically, we will peer a demo VPC with the default VPC that was created with the AWS account.  
특히, AWS 계정 생성 시 기본으로 제공되는 VPC와 데모 VPC를 피어링할 것입니다.  

The goal is to enable communication between these two isolated networks.  
목표는 두 개의 격리된 네트워크 간 통신을 가능하게 하는 것입니다.  

---

To begin, we will verify that the two VPCs are currently not connected.  
먼저, 두 VPC가 현재 연결되어 있지 않음을 확인합니다.  

This will be demonstrated by launching an EC2 instance in the default VPC and attempting to communicate with an instance in the demo VPC.  
기본 VPC에 EC2 인스턴스를 실행하고, 데모 VPC의 인스턴스와 통신을 시도하여 이를 확인합니다.  

---

I will launch an EC2 instance in the default VPC using the EC2 management console.  
EC2 관리 콘솔을 통해 기본 VPC에 EC2 인스턴스를 실행합니다.  

During the launch, I will select the demo key pair, although it will not be needed for this demonstration.  
실행 시 데모 키 페어를 선택하지만, 이 실습에서는 실제로 필요하지 않습니다.  

The instance will be placed in the default VPC, and a security group named launch-wizard-2 with SSH access will be assigned.  
인스턴스는 기본 VPC에 배치되며, SSH 접근이 가능한 launch-wizard-2 보안 그룹이 할당됩니다.  

---

Once the instance is launched, we will have two instances: one in the demo VPC, which we will refer to as the BastionHost, and the other in the default VPC, which we will call the default VPC instance.  
인스턴스 실행 후, 두 개의 인스턴스가 있습니다. 하나는 데모 VPC의 BastionHost, 다른 하나는 기본 VPC 인스턴스입니다.  

Our objective is to verify connectivity between these two instances.  
목표는 두 인스턴스 간 연결을 확인하는 것입니다.  

---

Examining the private IPv4 addresses of both instances, we observe that the BastionHost has an IP address in the 10.0.0.0/16 range, while the default VPC instance has an IP address in the 172.31.36.159 range.  
두 인스턴스의 사설 IPv4 주소를 확인하면, BastionHost는 10.0.0.0/16 범위, 기본 VPC 인스턴스는 172.31.36.159 범위를 갖습니다.  

This indicates that they reside in different VPCs with distinct CIDR blocks.  
이는 서로 다른 CIDR 블록을 가진 다른 VPC에 존재함을 의미합니다.  

---

We will now connect to the default VPC instance using EC2 Instance Connect and also connect to the BastionHost instance.  
이제 EC2 Instance Connect를 사용하여 기본 VPC 인스턴스와 BastionHost 인스턴스에 접속합니다.  

From the BastionHost, we perform a curl request to the default VPC instance's private IP address on port 80, which returns a "hello world" response, confirming connectivity from BastionHost to default VPC instance.  
BastionHost에서 기본 VPC 인스턴스의 사설 IP로 포트 80에 curl 요청을 보내면 "hello world" 응답이 반환되어 BastionHost에서 기본 VPC 인스턴스로의 연결이 확인됩니다.  

---

However, when we attempt the same curl request from the default VPC instance to the BastionHost's private IP address, the request times out.  
하지만 기본 VPC 인스턴스에서 BastionHost 사설 IP로 같은 curl 요청을 시도하면, 요청이 시간 초과됩니다.  

This demonstrates that, by default, instances in separate VPCs cannot communicate with each other due to network isolation.  
이는 기본적으로 서로 다른 VPC의 인스턴스가 네트워크 격리로 인해 통신할 수 없음을 보여줍니다.  

---

## Creating a VPC Peering Connection  
## VPC 피어링 연결 생성  

To enable communication between these two VPCs, we need to create a VPC peering connection.  
두 VPC 간 통신을 가능하게 하려면 VPC 피어링 연결을 생성해야 합니다.  

This is done by navigating to the VPC console and selecting "Peering Connections".  
VPC 콘솔에서 "Peering Connections"를 선택하여 수행합니다.  

We create a new peering connection named "demo peering connection".  
"demo peering connection"이라는 새 피어링 연결을 생성합니다.  

---

We specify the requester VPC as the demo VPC and the accepter VPC as the default VPC.  
요청자 VPC는 데모 VPC, 수락자 VPC는 기본 VPC로 지정합니다.  

Both VPCs are in the same AWS account and region.  
두 VPC는 동일한 AWS 계정과 리전에 있습니다.  

It is important to note that the CIDR blocks of the two VPCs do not overlap, which is a requirement for peering connections.  
두 VPC의 CIDR 블록이 겹치지 않아야 한다는 점이 중요합니다. 이는 피어링 연결 요구사항입니다.  

---

After creating the peering connection, its status is "pending acceptance."  
피어링 연결 생성 후, 상태는 "pending acceptance"입니다.  

Since both VPCs are in the same account, we can accept the peering request ourselves.  
두 VPC가 같은 계정에 있으므로 직접 피어링 요청을 수락할 수 있습니다.  

Once accepted, the status changes to active.  
수락하면 상태가 active로 변경됩니다.  

---

Important: To enable traffic to flow across the VPC peering connection, you must add routes to the route tables of one or both VPCs.  
중요: VPC 피어링을 통해 트래픽이 흐르도록 하려면, 하나 또는 두 VPC의 라우트 테이블에 경로를 추가해야 합니다.  

Simply establishing the peering connection is not sufficient.  
피어링 연결만 생성하는 것으로는 충분하지 않습니다.  

---

## Updating Route Tables  
## 라우트 테이블 업데이트  

We proceed to update the route tables to allow traffic to route between the two VPCs.  
두 VPC 간 트래픽 경로를 허용하도록 라우트 테이블을 업데이트합니다.  

First, we identify the main route table associated with the default VPC.  
먼저, 기본 VPC와 연결된 메인 라우트 테이블을 확인합니다.  

We then add a route with the destination set to the CIDR block of the demo VPC and the target set to the peering connection.  
데모 VPC의 CIDR을 대상으로, 피어링 연결을 대상으로 하는 경로를 추가합니다.  

Next, we update the route table associated with the demo VPC.  
다음으로 데모 VPC와 연결된 라우트 테이블을 업데이트합니다.  

We add a route with the destination set to the CIDR block of the default VPC and the target set to the same peering connection.  
기본 VPC CIDR을 대상으로, 동일한 피어링 연결을 대상으로 하는 경로를 추가합니다.  

This establishes bidirectional routing between the two VPCs.  
이로써 두 VPC 간 양방향 라우팅이 설정됩니다.  

---

After updating both route tables, we test connectivity again by performing a curl request from the default VPC instance to the BastionHost's private IP address.  
두 라우트 테이블 업데이트 후, 기본 VPC 인스턴스에서 BastionHost 사설 IP로 curl 요청을 보내 연결을 다시 테스트합니다.  

This time, the request succeeds and returns "hello world," confirming that the VPC peering connection is operational.  
이번에는 요청이 성공하며 "hello world"가 반환되어 VPC 피어링 연결이 정상 동작함을 확인합니다.  

---

## Conclusion  
## 결론  

In summary, VPC peering enables private communication between two VPCs by establishing a peering connection and updating route tables accordingly.  
요약하면, VPC 피어링은 피어링 연결 생성과 라우트 테이블 업데이트를 통해 두 VPC 간 사설 통신을 가능하게 합니다.  

This allows instances in different VPCs to communicate as if they were on the same network, while maintaining network isolation from other VPCs.  
이를 통해 서로 다른 VPC의 인스턴스가 마치 같은 네트워크에 있는 것처럼 통신하면서, 다른 VPC와는 네트워크 격리를 유지할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- VPC peering allows two VPCs to communicate privately as if they are within the same network.  
- VPC 피어링은 두 VPC가 마치 동일한 네트워크 내에 있는 것처럼 사설 통신을 가능하게 합니다.  

- Creating a VPC peering connection requires selecting requester and accepter VPCs with non-overlapping CIDR blocks.  
- VPC 피어링 연결 생성 시, CIDR이 겹치지 않는 요청자와 수락자 VPC를 선택해야 합니다.  

- After establishing a peering connection, route tables in both VPCs must be updated to enable traffic flow.  
- 피어링 연결 후, 두 VPC의 라우트 테이블을 업데이트하여 트래픽 흐름을 활성화해야 합니다.  

- Even with peering, security groups and network ACLs must allow the desired traffic between instances.  
- 피어링이 있어도, 인스턴스 간 원하는 트래픽이 흐르도록 보안 그룹과 네트워크 ACL도 적절히 설정되어야 합니다.  
```

