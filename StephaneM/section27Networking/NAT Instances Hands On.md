```markdown
# NAT Instances Hands On  
# NAT 인스턴스 실습  

🎮 게임보상: "NAT Configurator" +350 XP  

---

## Creating a NAT Instance for Internet Access  
## 인터넷 접근을 위한 NAT 인스턴스 생성  

Let's proceed to create a NAT instance to provide internet access to our private subnets.  
프라이빗 서브넷에 인터넷 접근을 제공하기 위해 NAT 인스턴스를 생성해보겠습니다.  

To begin, click on "Launch instance" and type "NAT instance" to search for the appropriate Amazon Machine Image (AMI).  
먼저 "Launch instance"를 클릭하고 "NAT instance"를 입력하여 적합한 AMI(Amazon Machine Image)를 검색합니다.  

To find the NAT instance AMI, browse more AMIs and enter the search term "NAT". Press enter to view the results.  
NAT 인스턴스 AMI를 찾기 위해 "More AMIs"를 클릭하고 검색어로 "NAT"를 입력한 후 엔터를 눌러 결과를 확인합니다.  

There are approximately 40 results in the community AMIs section. Select the "Community AMI" tab to filter accordingly.  
커뮤니티 AMI 섹션에 약 40개의 결과가 있습니다. "Community AMI" 탭을 선택하여 필터링합니다.  

Look for NAT instances provided by AWS that specify the architecture as X86_64.  
AWS에서 제공하며 아키텍처가 X86_64로 지정된 NAT 인스턴스를 찾습니다.  

It is advisable to select a recent published date, for example, an AMI published in 2022 with a name similar to "Amazon AMI VPC NAT 2018".  
최근에 발행된 AMI를 선택하는 것이 좋습니다. 예를 들어 2022년에 발행된 "Amazon AMI VPC NAT 2018"과 유사한 이름의 AMI입니다.  

This ensures compatibility and recent updates.  
이렇게 하면 호환성과 최신 업데이트를 보장할 수 있습니다.  

Choose a suitable NAT instance AMI, such as the one mentioned, which appears recent enough.  
앞서 언급한 것과 같이 최신으로 보이는 적합한 NAT 인스턴스 AMI를 선택합니다.  

Note that NAT instances are somewhat deprecated, but this example will suffice for demonstration purposes.  
NAT 인스턴스는 다소 구식이지만, 데모 목적에는 충분합니다.  

---

## Select the instance type as T2 micro. For the key pair, use an existing demo key pair.  
## 인스턴스 유형을 T2 micro로 선택하고, 키 페어는 기존 데모 키 페어를 사용합니다.  

Next, configure the network settings by editing and creating a new security group.  
다음으로 네트워크 설정을 구성하며 새로운 보안 그룹을 생성하고 수정합니다.  

---

## Security Group Rules  
## 보안 그룹 규칙  

Allow SSH access from anywhere.  
SSH 접근을 어디서나 허용합니다.  

Add HTTP access with the source set to the VPC's CIDR block (e.g., 10.0.0.0/16).  
HTTP 접근을 추가하되 소스를 VPC CIDR 블록(예: 10.0.0.0/16)으로 설정합니다.  

Add HTTPS access from the same CIDR block.  
HTTPS 접근도 동일한 CIDR 블록에서 허용합니다.  

Finally, assign the NAT instance to the appropriate VPC, such as the demo VPC, and deploy it in a public subnet, for example, Public Subnet A.  
마지막으로 NAT 인스턴스를 적절한 VPC(예: Demo VPC)에 할당하고 퍼블릭 서브넷(예: Public Subnet A)에 배치합니다.  

Name the security group as "NAT instance SG" to keep roles organized.  
보안 그룹 이름을 "NAT instance SG"로 지정하여 역할을 명확히 합니다.  

After verifying all settings, launch the NAT instance.  
모든 설정을 확인한 후 NAT 인스턴스를 실행합니다.  

---

## Configuring the NAT Instance  
## NAT 인스턴스 구성  

Once the NAT instance is created, it is necessary to disable the source/destination check.  
NAT 인스턴스가 생성되면 source/destination 체크를 비활성화해야 합니다.  

This setting must be stopped because the NAT instance needs to receive and send traffic where the source or destination is not itself.  
NAT 인스턴스가 자신이 아닌 소스 또는 목적지 트래픽을 송수신해야 하므로 이 설정을 비활성화해야 합니다.  

This is crucial for NAT functionality.  
이것은 NAT 기능에 필수적입니다.  

Stop the instance to edit this setting, then disable the source/destination check and save the changes.  
이 설정을 수정하기 위해 인스턴스를 중지한 후, source/destination 체크를 비활성화하고 변경 사항을 저장합니다.  

This is a new feature that facilitates NAT instance usage.  
이는 NAT 인스턴스 사용을 용이하게 하는 새로운 기능입니다.  

---

## Routing Internet Traffic Through the NAT Instance  
## NAT 인스턴스를 통한 인터넷 트래픽 라우팅  

To enable private instances to access the internet, update the private subnet's route table.  
프라이빗 인스턴스가 인터넷에 접근할 수 있도록 프라이빗 서브넷의 라우트 테이블을 업데이트합니다.  

Edit the routes to add a rule that directs internet-bound traffic through the NAT instance.  
인터넷 트래픽을 NAT 인스턴스를 통해 라우팅하도록 규칙을 추가합니다.  

This means any EC2 instance within the subnet associated with this route table will send traffic destined for the internet via the NAT instance.  
이 라우트 테이블에 연결된 서브넷의 모든 EC2 인스턴스가 인터넷으로 향하는 트래픽을 NAT 인스턴스를 통해 보내게 됩니다.  

---

## Verifying Internet Access from Private Instances  
## 프라이빗 인스턴스에서 인터넷 접근 확인  

To verify the setup, SSH into the private instance by first connecting through the Bastion Host using EC2 Instance Connect.  
설정을 확인하려면 먼저 Bastion Host를 통해 SSH로 프라이빗 인스턴스에 접속합니다.  

Then, use the SSH command with the private IP of the private instance and the appropriate key pair to access it.  
그런 다음 프라이빗 인스턴스의 사설 IP와 적절한 키 페어를 사용하여 SSH로 접근합니다.  

Initially, pinging external sites such as google.com will fail because the NAT instance's security group does not allow ICMP traffic.  
처음에는 google.com과 같은 외부 사이트에 핑을 보내면 실패합니다. NAT 인스턴스의 보안 그룹이 ICMP 트래픽을 허용하지 않기 때문입니다.  

To fix this, edit the NAT instance's security group inbound rules to add a rule allowing ICMP (all types) from the VPC's CIDR block.  
이를 수정하려면 NAT 인스턴스의 보안 그룹 인바운드 규칙에서 VPC CIDR 블록에서 오는 모든 유형의 ICMP 트래픽을 허용하는 규칙을 추가합니다.  

After saving the updated security group rules, try pinging google.com again from the private instance.  
보안 그룹 규칙을 저장한 후 프라이빗 인스턴스에서 다시 google.com에 핑을 시도합니다.  

You should now receive replies, confirming internet connectivity.  
이제 응답을 받을 수 있으며, 인터넷 연결이 확인됩니다.  

Additionally, commands like curl google.com or curl example.com will return HTML content, demonstrating HTTP and HTTPS access.  
또한 curl google.com 또는 curl example.com 명령으로 HTML 콘텐츠를 받을 수 있어 HTTP/HTTPS 접근이 가능함을 보여줍니다.  

---

## Summary  
## 요약  

By configuring a NAT instance with appropriate security group rules, disabling source/destination checks, and updating the private subnet's route table, we have enabled instances in private subnets to access the internet without exposing them directly.  
적절한 보안 그룹 규칙 설정, source/destination 체크 비활성화, 프라이빗 서브넷 라우트 테이블 업데이트를 통해, 프라이빗 서브넷 인스턴스가 직접 공개되지 않고도 인터넷에 접근할 수 있도록 했습니다.  

The private instances do not have public IP addresses and require a Bastion Host for SSH access.  
프라이빗 인스턴스에는 퍼블릭 IP가 없으며, SSH 접근을 위해 Bastion Host가 필요합니다.  

In the next lecture, we will explore NAT gateways, which provide a more efficient and managed solution for internet access from private subnets.  
다음 강의에서는 프라이빗 서브넷의 인터넷 접근을 위한 더 효율적이고 관리되는 NAT 게이트웨이를 살펴봅니다.  

For now, the NAT instance can be stopped or terminated as it will no longer be used.  
현재는 NAT 인스턴스를 중지하거나 종료해도 됩니다. 더 이상 사용되지 않기 때문입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created a NAT instance to provide internet access to private subnets.  
- 프라이빗 서브넷에 인터넷 접근을 제공하기 위해 NAT 인스턴스를 생성했습니다.  

- Configured security group rules to allow SSH, HTTP, HTTPS, and ICMP traffic.  
- SSH, HTTP, HTTPS, ICMP 트래픽을 허용하도록 보안 그룹 규칙을 구성했습니다.  

- Disabled source/destination check on the NAT instance to enable proper traffic routing.  
- 올바른 트래픽 라우팅을 위해 NAT 인스턴스에서 source/destination 체크를 비활성화했습니다.  

- Updated private subnet route table to direct internet-bound traffic through the NAT instance.  
- 프라이빗 서브넷 라우트 테이블을 업데이트하여 인터넷 트래픽이 NAT 인스턴스를 통해 라우팅되도록 했습니다.  
```
