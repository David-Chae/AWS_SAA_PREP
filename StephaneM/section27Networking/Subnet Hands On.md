```markdown
# Subnet Hands On  
# 서브넷 실습  

🎮 게임보상: "Subnet Builder" +300 XP  

---

## Creating Subnets in a VPC  
## VPC에서 서브넷 생성  

Let's proceed to create our subnets.  
이제 서브넷을 생성해 보겠습니다.  

On the left-hand side, navigate to the Subnets section.  
왼쪽 메뉴에서 "Subnets" 섹션으로 이동합니다.  

Initially, there are three subnets belonging to the previous VPC.  
초기에는 이전 VPC에 속한 세 개의 서브넷이 있습니다.  

To focus on a specific VPC, we can filter the view accordingly.  
특정 VPC에 집중하려면 뷰를 필터링할 수 있습니다.  

To filter by VPC, refresh the page first.  
VPC별 필터링을 위해 먼저 페이지를 새로 고침합니다.  

Then, click on "Select a VPC" and choose the DemoVPC to filter all views by this VPC, reducing noise in the user interface.  
그 다음 "Select a VPC"를 클릭하고 DemoVPC를 선택하면 모든 뷰가 이 VPC 기준으로 필터링되어 UI가 간결해집니다.  

After filtering, you will notice that there are zero subnets associated with this specific VPC.  
필터링 후, 이 특정 VPC와 연결된 서브넷이 없음을 확인할 수 있습니다.  

---

## Creating Public Subnets  
## 퍼블릭 서브넷 생성  

We will create a subnet by selecting the DemoVPC as the VPC.  
DemoVPC를 선택하여 서브넷을 생성합니다.  

Next, specify the subnet settings including the subnet name.  
다음으로 서브넷 이름을 포함한 설정을 지정합니다.  

The first subnet will be named PublicSubnetA because it is placed in Availability Zone (AZ) A.  
첫 번째 서브넷은 AZ A에 위치하므로 PublicSubnetA로 명명합니다.  

Specify the AZ as eu-central-1a corresponding to AZ A.  
AZ를 AZ A에 해당하는 eu-central-1a로 지정합니다.  

Then, select an IPv4 CIDR block. For this public subnet, we will use 10.0.0.0/24.  
그 다음 IPv4 CIDR 블록을 선택합니다. 이 퍼블릭 서브넷은 10.0.0.0/24를 사용합니다.  

This subnet size is appropriate because public subnets typically require fewer IP addresses, usually reserved for load balancers or front-facing infrastructure.  
퍼블릭 서브넷은 일반적으로 적은 IP 주소만 필요하며, 주로 로드 밸런서나 프론트엔드 인프라용이므로 이 크기가 적절합니다.  

A smaller subnet size is beneficial here.  
작은 서브넷 크기가 여기서 유리합니다.  

The /24 CIDR block corresponds to 256 IP addresses, where only the last octet can vary, ranging from .0 to .255.  
/24 CIDR 블록은 256개의 IP 주소를 가지며, 마지막 옥텟만 변경 가능하여 .0에서 .255까지 범위가 됩니다.  

This range provides sufficient IPs for the intended public subnet use case.  
이 범위는 의도된 퍼블릭 서브넷 용도로 충분한 IP를 제공합니다.  

Next, add a second public subnet named PublicSubnetB in AZ eu-central-1b.  
다음으로 두 번째 퍼블릭 서브넷 PublicSubnetB를 AZ eu-central-1b에 추가합니다.  

For the IPv4 CIDR block, choose 10.0.1.0/24, which is the next sequential range after the first subnet.  
IPv4 CIDR 블록으로는 첫 번째 서브넷 다음 연속 범위인 10.0.1.0/24를 선택합니다.  

This ensures no overlapping IP addresses between the subnets.  
이렇게 하면 두 서브넷 간 IP 주소가 겹치지 않습니다.  

You can verify the IP range for this subnet as starting from 10.0.1.0 to 10.0.1.255.  
이 서브넷의 IP 범위가 10.0.1.0부터 10.0.1.255임을 확인할 수 있습니다.  

This setup creates two public subnets distributed across two availability zones.  
이 구성으로 두 개의 퍼블릭 서브넷이 두 개의 가용 영역에 분산됩니다.  

---

## Creating Private Subnets  
## 프라이빗 서브넷 생성  

Now, let's create private subnets.  
이제 프라이빗 서브넷을 생성해 보겠습니다.  

The first private subnet will be named PrivateSubnetA.  
첫 번째 프라이빗 서브넷은 PrivateSubnetA로 명명합니다.  

For this subnet, select a larger IPv4 CIDR block, such as 10.0.16.0/20.  
이 서브넷은 더 큰 IPv4 CIDR 블록인 10.0.16.0/20을 선택합니다.  

This subnet size accommodates 4,096 IP addresses, ranging from 10.0.16.0 to 10.0.31.255.  
이 서브넷 크기는 4,096개의 IP 주소를 수용하며, 10.0.16.0부터 10.0.31.255까지 범위입니다.  

Next, add another private subnet named PrivateSubnetB in AZ eu-central-1b.  
다음으로 PrivateSubnetB를 AZ eu-central-1b에 추가합니다.  

Assign the IPv4 CIDR block 10.0.32.0/20, which is the next logical range following the previous private subnet.  
IPv4 CIDR 블록으로 이전 프라이빗 서브넷 다음 범위인 10.0.32.0/20을 지정합니다.  

This ensures no IP address overlap.  
이렇게 하면 IP 주소가 겹치지 않습니다.  

---

## Finalizing Subnet Creation  
## 서브넷 생성 완료  

We have now defined four subnets: two public and two private, each distributed across two availability zones.  
이제 두 개의 퍼블릭과 두 개의 프라이빗 서브넷, 총 네 개를 정의했으며, 각 서브넷은 두 가용 영역에 분산됩니다.  

Proceed to create all four subnets.  
네 개의 서브넷을 모두 생성합니다.  

Since there are no overlapping IP addresses, the creation will be successful.  
IP 주소가 겹치지 않으므로 생성이 성공적으로 완료됩니다.  

On the right-hand side, observe the number of available IP addresses for each subnet.  
오른쪽에서 각 서브넷의 사용 가능한 IP 주소 수를 확인합니다.  

For example, the public subnet shows 251 available IP addresses, and the private subnet shows 4,091.  
예를 들어, 퍼블릭 서브넷은 251개의 IP, 프라이빗 서브넷은 4,091개의 IP를 표시합니다.  

This is because five IP addresses are reserved by each subnet, so the available IPs equal the size of the CIDR block minus five.  
각 서브넷에서 5개의 IP가 예약되어 있으므로 사용 가능한 IP는 CIDR 블록 크기에서 5를 뺀 값입니다.  

Distributing subnets across two availability zones, eu-central-1a and eu-central-1b, enhances high availability for resources deployed within these subnets.  
서브넷을 두 가용 영역(eu-central-1a, eu-central-1b)에 분산하면 이 서브넷 내 리소스의 고가용성이 향상됩니다.  

However, at this stage, no configurations have been made to designate subnets as public or private.  
하지만 현재 단계에서는 서브넷을 퍼블릭 또는 프라이빗으로 지정하는 설정은 아직 없습니다.  

They currently appear identical.  
현재 모두 동일하게 표시됩니다.  

This distinction will be addressed in future lectures.  
이 구분은 이후 강의에서 다룰 예정입니다.  

This concludes the subnet creation setup.  
이로써 서브넷 생성 설정이 완료됩니다.  

Thank you for following along, and I look forward to seeing you in the next lecture.  
함께 따라와 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created and configured subnets within a specific VPC for organized network segmentation.  
- 특정 VPC 내에서 서브넷을 생성하고 구성하여 체계적인 네트워크 분할을 구현했습니다.  

- Defined public subnets with smaller CIDR blocks suitable for front-facing infrastructure.  
- 프론트엔드 인프라에 적합한 작은 CIDR 블록을 가진 퍼블릭 서브넷을 정의했습니다.  

- Established private subnets with larger CIDR blocks to accommodate more IP addresses.  
- 더 많은 IP를 수용할 수 있는 큰 CIDR 블록을 가진 프라이빗 서브넷을 생성했습니다.  

- Distributed subnets across multiple availability zones to enhance high availability.  
- 서브넷을 여러 가용 영역에 분산하여 고가용성을 강화했습니다.  
```

🎮 게임보상 완료: "Subnet Builder" +300 XP 🏆
