```md
# Security Groups Hands On  
# 시큐리티 그룹 실습  
👉 실제 EC2 인스턴스와 보안 그룹을 다루며 학습하는 실습 강의입니다.  

---

## Introduction to Security Groups  
## 시큐리티 그룹 소개  

We have launched our EC2 instance, and now let's have a look at security groups.  
EC2 인스턴스를 실행했으니 이제 보안 그룹을 살펴봅시다.  
👉 인스턴스를 띄운 뒤 보안 그룹 상태를 확인하는 단계입니다.  

By clicking on "Security" in the console, we get an overview of the security groups attached to our instance, as well as the inbound and outbound rules.  
콘솔에서 "Security"를 클릭하면 인스턴스에 연결된 보안 그룹과 인바운드/아웃바운드 규칙을 확인할 수 있습니다.  

To access a more complete page of security groups, navigate to the left-hand side menu under "Networking and Security" and click on "Security Groups".  
보안 그룹 전체 페이지를 보려면 왼쪽 메뉴의 "Networking and Security" 아래에 있는 "Security Groups"를 클릭합니다.  

Here, we can see that there are two security groups in our console so far: the default security group created by default, and the "launch wizard one", which was created when we created our EC2 instance.  
여기서 기본적으로 생성된 **default 보안 그룹**과, EC2 인스턴스를 만들 때 생성된 **launch wizard 보안 그룹** 두 개가 있습니다.  

Each security group has an ID, similar to how an EC2 instance has an ID.  
각 보안 그룹은 EC2 인스턴스처럼 고유한 ID를 가집니다.  

We can check the inbound rules, which are the rules that allow connectivity from the outside into the EC2 instance.  
인바운드 규칙을 확인할 수 있으며, 이는 외부에서 EC2 인스턴스로 들어오는 연결을 허용하는 규칙입니다.  

Currently, there are two inbound rules:  
현재 두 개의 인바운드 규칙이 있습니다:  

- The first is of type SSH, which allows port 22 access to our instance.  
  첫 번째는 **SSH** 타입으로, 포트 22 접속을 허용합니다.  

- The second is HTTP, which allows port 80 access.  
  두 번째는 **HTTP** 타입으로, 포트 80 접속을 허용합니다.  

---

## Editing Inbound Rules  
## 인바운드 규칙 수정하기  

Clicking on "Edit inbound rules" shows that the first rule is SSH on port 22 from anywhere (0.0.0.0/0).  
"Edit inbound rules"를 클릭하면, 첫 번째 규칙은 **SSH (22번 포트)**가 어디서든(0.0.0.0/0) 접근 가능함을 확인할 수 있습니다.  

The second rule is HTTP on port 80, also from anywhere.  
두 번째 규칙은 **HTTP (80번 포트)**가 어디서든 접근 가능하도록 설정되어 있습니다.  

This HTTP rule is what allowed us to access our web server.  
이 HTTP 규칙 덕분에 웹 서버에 접속할 수 있었습니다.  

If we delete the HTTP rule on port 80 and save the rules, only port 22 remains open.  
만약 80번 포트 규칙을 삭제하고 저장하면, 22번 포트만 열려 있게 됩니다.  

Refreshing the page now results in an infinite loading screen ...  
이제 웹 페이지를 새로고침하면 무한 로딩이 발생하며, EC2 인스턴스에 HTTP 접속할 수 없게 됩니다.  

This demonstrates the importance of the inbound rule for port 80.  
이는 **80번 포트 인바운드 규칙의 중요성**을 보여줍니다.  

---

## Important Tip on Timeouts  
## 타임아웃 관련 중요한 팁  

Any time you see a timeout when trying to establish a connection ... this is almost always caused by an EC2 security group misconfiguration.  
EC2 인스턴스에 연결 시도 중 타임아웃이 발생한다면, 이는 대부분 보안 그룹 설정 오류 때문입니다.  

If you experience a timeout, check your security group rules to ensure they are correct.  
타임아웃이 발생하면 보안 그룹 규칙을 다시 확인해야 합니다.  

To fix this, we can add back the HTTP rule to allow port 80 traffic from anywhere (IPv4).  
이 문제를 해결하려면 다시 **80번 포트 HTTP 규칙**을 추가해 IPv4 어디서든 접속 가능하게 해야 합니다.  

After saving the rule, refreshing the page shows that the website is fully accessible again.  
규칙을 저장한 후 새로고침하면 웹사이트 접속이 정상적으로 복구됩니다.  

---

## Adding Inbound Rules  
## 인바운드 규칙 추가하기  

We can add any sort of inbound rule by defining the port or port range.  
포트나 포트 범위를 정의해 원하는 인바운드 규칙을 추가할 수 있습니다.  

For example, we could add port 443 for HTTPS.  
예: HTTPS 접속을 위해 443번 포트를 추가할 수 있습니다.  

The console provides a dropdown to select common protocols, which automatically sets the correct port number.  
콘솔에는 일반적인 프로토콜을 선택할 수 있는 드롭다운이 있으며, 선택 시 자동으로 올바른 포트 번호가 설정됩니다.  

You can also define the source of allowed traffic using different CIDR blocks, security groups, or prefix lists.  
허용할 트래픽 출처는 CIDR 블록, 다른 보안 그룹, 또는 prefix list를 통해 정의할 수 있습니다.  

For now, you can select "My IP" to allow access only from your current IP address.  
현재는 "My IP"를 선택해 내 현재 IP에서만 접근 가능하도록 설정할 수 있습니다.  

Be aware that if your IP changes, you will get a timeout ...  
하지만 IP가 변경되면 타임아웃이 발생하고 인스턴스 접속이 차단됩니다.  

---

## Outbound Rules  
## 아웃바운드 규칙  

Looking at outbound rules, we see that all traffic on IPv4 is allowed to anywhere.  
아웃바운드 규칙을 보면 IPv4 모든 트래픽이 어디든 나갈 수 있도록 허용되어 있습니다.  

This allows our EC2 instance to have full internet connectivity outbound.  
덕분에 EC2 인스턴스는 아웃바운드 인터넷 연결을 완전히 사용할 수 있습니다.  

An EC2 instance can have multiple security groups attached to it.  
하나의 EC2 인스턴스에 여러 보안 그룹을 붙일 수 있습니다.  

Similarly, a security group can be attached to multiple EC2 instances.  
반대로 하나의 보안 그룹을 여러 EC2 인스턴스에 붙일 수도 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Security groups control inbound and outbound traffic for EC2 instances.  
  보안 그룹은 EC2 인스턴스의 인바운드/아웃바운드 트래픽을 제어합니다.  

- Inbound rules specify allowed incoming connections, such as SSH on port 22 and HTTP on port 80.  
  인바운드 규칙은 들어오는 연결을 정의합니다 (예: SSH 22번, HTTP 80번).  

- Timeouts when connecting ... often indicate incorrect security group rules.  
  연결 시 타임아웃은 보안 그룹 규칙 오류일 가능성이 큽니다.  

- Multiple security groups can be attached to one EC2 instance, and one security group can be attached to multiple instances.  
  여러 보안 그룹을 인스턴스 하나에 붙이거나, 보안 그룹 하나를 여러 인스턴스에 붙일 수 있습니다.  

---

🎮 **게임 보상**: "보안 마스터" 칭호 획득!  
👉 이제 인바운드/아웃바운드 규칙을 자유자재로 다룰 수 있음! 🚀
```
