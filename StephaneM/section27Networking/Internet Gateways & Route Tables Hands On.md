```markdown
# Internet Gateways & Route Tables Hands On  
# 인터넷 게이트웨이와 라우트 테이블 실습  

🎮 게임보상: "Internet Pathfinder" +350 XP  

---

## Verifying Internet Access for EC2 Instances  
## EC2 인스턴스의 인터넷 접근 확인  

First, let's ensure that our EC2 instances in these subnets do not have internet access.  
먼저, 이 서브넷의 EC2 인스턴스가 인터넷 접근이 없는지 확인해봅시다.  

To verify this, we will launch an instance into these subnets.  
이를 확인하기 위해, 서브넷에 EC2 인스턴스를 실행합니다.  

I am clicking on Launch Instances in the EC2 console.  
EC2 콘솔에서 "Launch Instances"를 클릭합니다.  

Scrolling down, I select Amazon Linux 2, instance type t2.micro.  
스크롤 다운하여 Amazon Linux 2와 인스턴스 타입 t2.micro를 선택합니다.  

I will not select a key pair for this instance.  
이 인스턴스에는 키 페어를 선택하지 않습니다.  

For network settings, I will edit them.  
네트워크 설정은 수동으로 편집합니다.  

In the network settings, I choose the VPC named DemoVPC.  
네트워크 설정에서 DemoVPC를 선택합니다.  

From there, I can select any subnet, for example, public subnet A.  
그 후, 원하는 서브넷을 선택합니다. 예를 들어, 퍼블릭 서브넷 A를 선택합니다.  

This subnet has 251 IP addresses available, so I can launch my instance here.  
이 서브넷에는 251개의 IP가 있어 인스턴스를 실행할 수 있습니다.  

Notice that the setting Auto-assign Public IP is currently disabled.  
자동 퍼블릭 IP 할당 설정이 현재 비활성화되어 있는 것을 확인합니다.  

To obtain a public IPv4 address, this setting must be enabled.  
퍼블릭 IPv4 주소를 받으려면 이 설정을 활성화해야 합니다.  

However, it is disabled by default here.  
하지만 기본적으로 여기서는 비활성화 상태입니다.  

If you select a subnet directly, this setting is enabled by default for public subnets.  
서브넷을 직접 선택하면, 퍼블릭 서브넷에서는 기본적으로 이 설정이 활성화됩니다.  

To enable auto-assigned public IPv4 addresses for our public subnets, go to the subnet settings.  
퍼블릭 서브넷의 자동 퍼블릭 IPv4 할당을 활성화하려면, 서브넷 설정으로 이동합니다.  

For public subnet A, select Actions and then Edit subnet settings.  
퍼블릭 서브넷 A에서 "Actions"를 클릭하고 "Edit subnet settings"를 선택합니다.  

Enable Auto-assign public IPv4 address and save.  
"Auto-assign public IPv4 address"를 활성화하고 저장합니다.  

Repeat this for public subnet B.  
퍼블릭 서브넷 B에서도 반복합니다.  

After enabling this setting for the public subnets, refresh the instance launch page.  
퍼블릭 서브넷에서 이 설정을 활성화한 후, 인스턴스 실행 페이지를 새로고침합니다.  

When selecting DemoVPC and public subnet A, the Auto-assign Public IP setting is now enabled by default.  
DemoVPC와 퍼블릭 서브넷 A를 선택하면, 자동 퍼블릭 IP 할당이 기본적으로 활성화됩니다.  

This modification in subnet settings is reflected in the EC2 launch console.  
서브넷 설정 변경 사항이 EC2 실행 콘솔에 반영됩니다.  

Create a new security group and add an SSH rule on port 22 to allow SSH access to the EC2 instance.  
새로운 보안 그룹을 만들고, SSH 포트 22 규칙을 추가하여 EC2 인스턴스에 SSH 접근을 허용합니다.  

The rest of the settings look good, so proceed to launch the instance.  
나머지 설정은 문제 없으므로 인스턴스를 실행합니다.  

The instance is now running and has been assigned a public IPv4 address.  
인스턴스가 실행되었으며 퍼블릭 IPv4 주소가 할당되었습니다.  

Although the instance has a public IPv4 address, it does not have internet connectivity.  
퍼블릭 IPv4 주소가 있어도, 인터넷 연결은 되지 않습니다.  

To verify, attempt to connect to the instance using EC2 Instance Connect.  
확인하려면 EC2 Instance Connect로 연결을 시도합니다.  

Despite opening the SSH rule, there is a problem connecting to the instance.  
SSH 규칙을 열었음에도 인스턴스 연결에 문제가 있습니다.  

This indicates that the instance's network settings are not correctly configured.  
이는 인스턴스의 네트워크 설정이 올바르게 구성되지 않았음을 의미합니다.  

This is where the Internet Gateway comes into play.  
이때 인터넷 게이트웨이가 필요합니다.  

Navigate to the VPC console and observe that there is no internet gateway attached to our VPC.  
VPC 콘솔로 이동하면, VPC에 인터넷 게이트웨이가 연결되지 않은 것을 확인할 수 있습니다.  

If you remove the filter, you can see an internet gateway attached to the default VPC.  
필터를 제거하면, 기본 VPC에는 인터넷 게이트웨이가 연결되어 있는 것을 볼 수 있습니다.  

Create a new internet gateway named DemoIGW.  
DemoIGW라는 이름으로 새로운 인터넷 게이트웨이를 생성합니다.  

After creation, it is in a detached state.  
생성 후에는 분리 상태(detached)입니다.  

Attach this internet gateway to the DemoVPC.  
이 인터넷 게이트웨이를 DemoVPC에 연결합니다.  

Now, the internet gateway is attached to our VPC, providing internet access capability.  
이제 인터넷 게이트웨이가 VPC에 연결되어 인터넷 접근이 가능해졌습니다.  

Try connecting again to the EC2 instance using EC2 Instance Connect.  
다시 EC2 Instance Connect로 인스턴스에 연결을 시도합니다.  

The connection still fails.  
연결은 여전히 실패합니다.  

This is because, even though we have an internet gateway, we need to configure routing to use it.  
인터넷 게이트웨이가 있어도, 이를 사용하도록 라우팅을 구성해야 하기 때문입니다.  

Examine the route tables.  
라우트 테이블을 확인합니다.  

The default route table is associated with subnets that do not have explicit route table associations.  
기본 라우트 테이블은 명시적 서브넷 연결이 없는 서브넷과 연결됩니다.  

Currently, the main route table is associated with four subnets, but we prefer explicit subnet associations.  
현재 메인 라우트 테이블은 4개의 서브넷과 연결되어 있지만, 명시적 서브넷 연결이 더 좋습니다.  

Create two route tables: one named PublicRouteTable assigned to the VPC for public subnets, and another named PrivateRouteTable assigned to the VPC for private subnets.  
두 개의 라우트 테이블을 생성합니다: PublicRouteTable은 퍼블릭 서브넷용, PrivateRouteTable은 프라이빗 서브넷용으로 VPC에 할당합니다.  

This allows us to assign subnets to the appropriate route tables explicitly.  
이렇게 하면 서브넷을 적절한 라우트 테이블에 명시적으로 연결할 수 있습니다.  

Edit the subnet associations for the PublicRouteTable and add all public subnets.  
PublicRouteTable의 서브넷 연결을 편집하고 모든 퍼블릭 서브넷을 추가합니다.  

Similarly, edit the subnet associations for the PrivateRouteTable and add the private subnets A and B.  
마찬가지로 PrivateRouteTable의 서브넷 연결을 편집하고 프라이빗 서브넷 A와 B를 추가합니다.  

Now, both route tables have two subnets associated with them, and the main route table has no subnet associations.  
이제 두 라우트 테이블 모두 2개의 서브넷과 연결되며, 메인 라우트 테이블은 서브넷과 연결되지 않습니다.  

Focus on the PublicRouteTable since our EC2 instance was launched into a public subnet associated with this route table.  
EC2 인스턴스가 이 라우트 테이블과 연결된 퍼블릭 서브넷에 생성되었으므로, PublicRouteTable에 집중합니다.  

Edit the routes in the public route table.  
퍼블릭 라우트 테이블에서 라우트를 편집합니다.  

Currently, there is a route for the VPC CIDR block (10.0.0.0/16) targeting local, which routes traffic within the VPC.  
현재 VPC CIDR 블록(10.0.0.0/16)에 대한 로컬 경로가 있어 VPC 내부 트래픽을 라우팅합니다.  

Add a new route with destination 0.0.0.0/0 representing all IP addresses outside the VPC.  
VPC 외부 모든 IP(0.0.0.0/0)를 대상으로 하는 새 경로를 추가합니다.  

Set the target to the internet gateway we created earlier (DemoIGW).  
대상을 앞서 생성한 인터넷 게이트웨이(DemoIGW)로 설정합니다.  

This means that any traffic not destined for the local VPC will be routed to the internet gateway.  
즉, 로컬 VPC가 아닌 모든 트래픽은 인터넷 게이트웨이로 라우팅됩니다.  

Save the route changes.  
라우트 변경 사항을 저장합니다.  

With this configuration, our EC2 instance should now have internet access.  
이 구성으로 EC2 인스턴스가 인터넷에 연결될 수 있습니다.  

Try connecting again using EC2 Instance Connect.  
다시 EC2 Instance Connect로 연결을 시도합니다.  

This time, the connection is successful, and the instance is connected to the internet.  
이번에는 연결이 성공하여 인스턴스가 인터넷에 연결되었습니다.  

For example, you can ping google.com from the instance and receive responses, confirming internet connectivity.  
예를 들어, 인스턴스에서 google.com에 핑을 보내 응답을 받으면 인터넷 연결이 확인됩니다.  

This setup provides internet access to
```


our public subnets via the public route table.
이 설정으로 퍼블릭 라우트 테이블을 통해 퍼블릭 서브넷이 인터넷에 연결됩니다.

We have not yet configured internet access for private EC2 instances.
프라이빗 EC2 인스턴스의 인터넷 접근은 아직 구성하지 않았습니다.

This will be covered in the next lectures.
이는 다음 강의에서 다룹니다.

---

## Key Takeaways

## 핵심 요약

* EC2 instances in subnets do not have internet access by default unless configured.

* 서브넷의 EC2 인스턴스는 기본적으로 인터넷 접근이 없으며, 별도 구성해야 합니다.

* Auto-assigning public IPv4 addresses must be enabled in subnet settings for public subnets.

* 퍼블릭 서브넷에서는 자동 퍼블릭 IPv4 할당을 활성화해야 합니다.

* An internet gateway must be created and attached to the VPC to provide internet access.

* 인터넷 접근을 위해 인터넷 게이트웨이를 생성하고 VPC에 연결해야 합니다.

* Route tables must be explicitly associated with subnets and configured with routes directing traffic to the internet gateway for external connectivity.

* 라우트 테이블은 서브넷과 명시적으로 연결하고, 외부 트래픽이 인터넷 게이트웨이로 향하도록 라우팅을 구성해야 합니다.

```

🎮 게임보상 완료: "Internet Pathfinder" +350 XP 🏆  
