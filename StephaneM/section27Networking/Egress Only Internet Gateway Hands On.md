```markdown
# Egress Only Internet Gateway Hands On  
# Egress Only 인터넷 게이트웨이 실습  

🎮 게임보상: "IPv6 Egress Master Badge" +650 XP  

---

## Creating an Egress Only Internet Gateway  
## Egress Only 인터넷 게이트웨이 생성  

I am currently in my VPC console.  
현재 VPC 콘솔에 접속해 있습니다.  

On the left-hand side, there is an option for Egress Only Internet Gateways.  
왼쪽 메뉴에 Egress Only 인터넷 게이트웨이 옵션이 있습니다.  

I can create one here.  
여기에서 새 게이트웨이를 생성할 수 있습니다.  

I will name it DemoEIGW.  
이 게이트웨이의 이름을 DemoEIGW로 지정하겠습니다.  

Next, I need to attach this gateway to my VPC.  
다음으로, 이 게이트웨이를 VPC에 연결해야 합니다.  

I will select my DemoVPC and create the Egress Only Internet Gateway.  
DemoVPC를 선택하고 Egress Only 인터넷 게이트웨이를 생성하겠습니다.  

It is now created and attached successfully.  
이제 게이트웨이가 성공적으로 생성되고 VPC에 연결되었습니다.  

---

## Configuring Route Tables for Private Subnets  
## 프라이빗 서브넷 라우트 테이블 구성  

To make the Egress Only Internet Gateway functional, I need to edit the route table.  
Egress Only 인터넷 게이트웨이를 작동시키려면 라우트 테이블을 편집해야 합니다.  

This route table must be associated with the private subnets, as it does not make sense to configure this for public subnets.  
이 라우트 테이블은 프라이빗 서브넷과 연결되어야 하며, 퍼블릭 서브넷에는 적용할 필요가 없습니다.  

I will edit the route table for the private subnets.  
프라이빗 서브넷용 라우트 테이블을 편집하겠습니다.  

In the routes section, I will add a route for all IPv6 traffic, represented as ::/0.  
라우트 섹션에서 모든 IPv6 트래픽(::/0)을 위한 라우트를 추가합니다.  

This route will redirect any IPv6 traffic to the Egress Only Internet Gateway.  
이 라우트는 모든 IPv6 트래픽을 Egress Only 인터넷 게이트웨이로 전달합니다.  

After saving these changes, the configuration is complete.  
변경 사항을 저장하면 구성은 완료됩니다.  

---

## Outcome  
## 결과  

Now, my EC2 instances located in the private subnets can access the internet over IPv6.  
이제 프라이빗 서브넷에 있는 EC2 인스턴스가 IPv6를 통해 인터넷에 접근할 수 있습니다.  

However, they remain unreachable from the internet, ensuring security while enabling outbound connectivity.  
그러나 인터넷에서는 접근할 수 없으므로, 아웃바운드 연결은 가능하면서도 보안은 유지됩니다.  

This was a simple and effective demonstration of setting up an Egress Only Internet Gateway.  
이번 실습은 Egress Only 인터넷 게이트웨이를 설정하는 간단하고 효과적인 방법을 보여주었습니다.  

I hope you found it helpful, and I will see you in the next lecture.  
도움이 되었기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created and attached an Egress Only Internet Gateway to a VPC.  
- VPC에 Egress Only 인터넷 게이트웨이를 생성하고 연결했습니다.  

- Edited the route table for private subnets to route IPv6 traffic (::/0) through the Egress Only Internet Gateway.  
- 프라이빗 서브넷 라우트 테이블을 편집하여 IPv6 트래픽(::/0)을 Egress Only 인터넷 게이트웨이로 라우팅했습니다.  

- Enabled instances in private subnets to access the internet over IPv6 while remaining unreachable from the internet.  
- 프라이빗 서브넷의 인스턴스가 IPv6로 인터넷에 접근 가능하면서도 인터넷에서 직접 접근 불가하도록 설정했습니다.  

- Demonstrated a straightforward setup process for Egress Only Internet Gateways.  
- Egress Only 인터넷 게이트웨이의 간단한 설정 과정을 시연했습니다.  
```
