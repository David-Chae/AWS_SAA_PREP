````markdown
# NACL & Security Groups Hands On  
# NACL 및 보안 그룹 실습  

🎮 게임보상: "Firewall Explorer" +500 XP  

---

## Introduction to Network ACLs  
## 네트워크 ACL 소개  

Let's examine our network ACLs.  
우리의 네트워크 ACL을 살펴보겠습니다.  

On the left-hand side, navigate to the Network ACLs section.  
왼쪽 메뉴에서 Network ACLs 섹션으로 이동합니다.  

For our VPC subnets, there is a default network ACL associated with four subnets.  
우리 VPC 서브넷에는 네 개의 서브넷과 연결된 기본 네트워크 ACL이 있습니다.  

It is important to note that this default NACL allows all inbound and outbound traffic on all ports everywhere.  
기본 NACL은 모든 포트의 모든 인바운드 및 아웃바운드 트래픽을 허용한다는 점이 중요합니다.  

The last rule denies traffic, but it never takes effect because the preceding allow rule has higher precedence.  
마지막 규칙은 트래픽을 거부하지만, 앞서 있는 허용 규칙이 우선하므로 실제로는 적용되지 않습니다.  

---

## Setting Up a Web Server on the Bastion Host  
## 배스천 호스트에서 웹 서버 설정  

Next, let's proceed to our EC2 instances and select the Bastion host.  
다음으로 EC2 인스턴스로 이동하여 배스천 호스트를 선택합니다.  

We will start an HTTP server on this instance to test connectivity.  
연결 테스트를 위해 이 인스턴스에서 HTTP 서버를 시작합니다.  

Connect to the instance and install the HTTPD package using the following command:  
인스턴스에 연결하고 다음 명령으로 HTTPD 패키지를 설치합니다:  

```bash
sudo yum install -y httpd
````

HTTPD 설치 명령입니다.

After installation, enable and start the HTTPD service with these commands:
설치 후, 다음 명령으로 HTTPD 서비스를 활성화하고 시작합니다:

```bash
sudo systemctl enable httpd
sudo systemctl start httpd
```

서비스 활성화 및 시작 명령입니다.

Then, create a simple web page by echoing "hello world" into the index.html file:
그런 다음, index.html 파일에 "hello world"를 작성하여 간단한 웹 페이지를 생성합니다:

```bash
sudo su -c 'echo "hello world" > /var/www/html/index.html'
```

간단한 웹 페이지 생성 명령입니다.

---

## Configuring Security Group for HTTP Access

## HTTP 접속을 위한 보안 그룹 구성

Ensure that the Bastion host's security group allows HTTP traffic.
배스천 호스트의 보안 그룹이 HTTP 트래픽을 허용하는지 확인합니다.

Currently, only port 22 (SSH) is allowed.
현재는 포트 22(SSH)만 허용되어 있습니다.

Edit the inbound rules to add an HTTP rule from anywhere and save the changes.
인바운드 규칙을 편집하여 어디서나 HTTP 접속을 허용하도록 추가하고 변경 사항을 저장합니다.

After updating the security group, access the Bastion host's public IP address in a browser.
보안 그룹 업데이트 후, 브라우저에서 배스천 호스트의 공용 IP에 접속합니다.

You should see the "hello world" message, confirming HTTP connectivity.
"hello world" 메시지가 표시되면 HTTP 연결이 확인된 것입니다.

---

## Modifying Network ACL Inbound Rules

## 네트워크 ACL 인바운드 규칙 수정

Now, let's examine the default NACL's inbound rules.
이제 기본 NACL의 인바운드 규칙을 살펴보겠습니다.

Currently, all traffic is allowed from anywhere.
현재는 모든 트래픽이 어디서나 허용되어 있습니다.

We will add a new rule with rule number 80 to deny HTTP traffic from anywhere.
규칙 번호 80으로 어디서나 오는 HTTP 트래픽을 거부하는 새 규칙을 추가합니다.

Save the changes and sort the rules by rule number to observe precedence.
변경 사항을 저장하고 규칙 번호별로 정렬하여 우선순위를 확인합니다.

With this deny rule in place, refreshing the Bastion host's web page results in an infinite loading timeout.
이 거부 규칙이 적용되면, 배스천 호스트의 웹 페이지를 새로 고치면 무한 로딩 타임아웃이 발생합니다.

This demonstrates that the NACL acted as a firewall and blocked the HTTP request.
이는 NACL이 방화벽 역할을 하여 HTTP 요청을 차단했음을 보여줍니다.

---

## Adjusting Rule Precedence in Network ACLs

## 네트워크 ACL 규칙 우선순위 조정

Next, change the deny HTTP rule's number to 140 and save.
다음으로, HTTP 거부 규칙 번호를 140으로 변경하고 저장합니다.

Since rule 140 has lower precedence than the existing allow rule at 100, refreshing the page now successfully loads the "hello world" message.
규칙 140은 기존 허용 규칙 100보다 우선순위가 낮기 때문에 페이지를 새로 고치면 "hello world" 메시지가 정상적으로 로드됩니다.

This illustrates that rule numbers determine precedence, with lower numbers evaluated first.
이는 규칙 번호가 우선순위를 결정하며, 낮은 번호가 먼저 평가됨을 보여줍니다.

---

## Demonstrating Statelessness of Network ACLs

## 네트워크 ACL 상태 비저장 성격 시연

Let's explore the stateless nature of NACLs.
NACL의 상태 비저장 특성을 살펴봅시다.

Edit the outbound rules and change the rule that currently allows all traffic to deny all traffic instead.
아웃바운드 규칙을 편집하여 현재 모든 트래픽을 허용하는 규칙을 모두 거부하도록 변경합니다.

Although the inbound rule allows HTTP traffic, the outbound deny rule blocks return traffic.
인바운드 규칙이 HTTP 트래픽을 허용해도, 아웃바운드 거부 규칙 때문에 반환 트래픽이 차단됩니다.

Refreshing the Bastion host's web page now results in infinite loading due to the blocked return traffic.
반환 트래픽이 차단되므로 배스천 호스트 웹 페이지 새로 고침 시 무한 로딩이 발생합니다.

This confirms that NACLs are stateless and require explicit rules for both inbound and outbound traffic.
이는 NACL이 상태 비저장이며, 인바운드와 아웃바운드 모두에 명시적 규칙이 필요함을 확인시켜줍니다.

---

## Relationship Between Security Groups and Network ACLs

## 보안 그룹과 네트워크 ACL 관계

It is important to note that security groups and network ACLs work together.
보안 그룹과 NACL은 함께 작동한다는 점이 중요합니다.

Even if the security group allows traffic, the NACL can block it.
보안 그룹이 트래픽을 허용해도 NACL이 차단할 수 있습니다.

Therefore, both must be configured correctly to avoid network issues.
따라서 네트워크 문제를 방지하려면 두 가지를 모두 올바르게 구성해야 합니다.

---

## Security Group Stateful Behavior

## 보안 그룹 상태 저장 특성

Revert the NACL outbound rule to allow all traffic.
NACL 아웃바운드 규칙을 모든 트래픽 허용으로 되돌립니다.

Now, modify the security group's outbound rules by removing all outbound permissions.
이제 보안 그룹 아웃바운드 규칙에서 모든 아웃바운드 권한을 제거합니다.

Despite this, refreshing the Bastion host's web page still works because security groups are stateful and allow return traffic automatically.
그럼에도 배스천 호스트 웹 페이지 새로 고침이 작동하는 이유는, 보안 그룹이 상태 저장이므로 반환 트래픽을 자동으로 허용하기 때문입니다.

However, if the EC2 instance initiates a connection to an external service, such as Google, it will be denied due to the lack of outbound rules.
하지만 EC2 인스턴스가 Google과 같은 외부 서비스에 연결을 시도하면, 아웃바운드 규칙이 없으므로 연결이 거부됩니다.

If outbound rules were added to allow such connections, return traffic would be permitted because of the stateful nature of security groups.
이러한 연결을 허용하는 아웃바운드 규칙을 추가하면, 보안 그룹의 상태 저장 특성 덕분에 반환 트래픽은 허용됩니다.

---

## Conclusion

## 결론

To restore full functionality, ensure HTTP is allowed from anywhere in both the security group and NACL outbound rules.
완전한 기능 복원을 위해, 보안 그룹과 NACL 아웃바운드 규칙 모두에서 HTTP를 어디서나 허용하도록 합니다.

Understanding the differences between EC2 security groups and network ACLs is crucial for effective network security management.
EC2 보안 그룹과 NACL의 차이를 이해하는 것은 효과적인 네트워크 보안 관리에 필수적입니다.

---

## Key Takeaways

## 핵심 요약

* Network ACLs (NACLs) are stateless firewalls associated with subnets, controlling inbound and outbound traffic.

* NACL은 서브넷과 연결된 상태 비저장 방화벽으로 인바운드와 아웃바운드 트래픽을 제어합니다.

* Default NACLs allow all inbound and outbound traffic and are associated with all subnets by default.

* 기본 NACL은 모든 인바운드 및 아웃바운드 트래픽을 허용하며, 기본적으로 모든 서브넷과 연결됩니다.

* Rule precedence in NACLs is determined


by rule numbers; lower numbers have higher priority.

* NACL의 규칙 우선순위는 규칙 번호로 결정되며, 낮은 번호가 더 높은 우선순위를 갖습니다.

* Security groups are stateful, allowing return traffic automatically, whereas NACLs are stateless and require explicit rules for return traffic.

* 보안 그룹은 상태 저장이므로 반환 트래픽을 자동으로 허용하지만, NACL은 상태 비저장이므로 반환 트래픽에 대한 명시적 규칙이 필요합니다.

```
