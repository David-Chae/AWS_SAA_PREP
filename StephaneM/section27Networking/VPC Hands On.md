```markdown
# VPC Hands On  
# VPC 실습  

🎮 게임보상: "VPC Creator" +300 XP  

---

## Creating Your First VPC  
## 첫 번째 VPC 생성  

Let's proceed to create our first Virtual Private Cloud (VPC).  
첫 번째 Virtual Private Cloud(VPC)를 생성해봅시다.  

Instead of launching the VPC Wizard, which would defeat the purpose of learning, we will create everything step-by-step manually.  
학습 목적을 살리기 위해 VPC 마법사를 사용하는 대신, 모든 것을 단계별로 수동으로 생성할 것입니다.  

I currently have one VPC available, but I will create a new one.  
현재 하나의 VPC가 존재하지만, 새로운 VPC를 생성할 것입니다.  

The name tag for this VPC will be DemoVPC.  
이 VPC의 이름 태그는 DemoVPC로 지정합니다.  

---

## Choosing an IPv4 CIDR Block  
## IPv4 CIDR 블록 선택  

We need to select an IPv4 CIDR block for the VPC.  
VPC에 사용할 IPv4 CIDR 블록을 선택해야 합니다.  

I will choose 10.0.0.0/16, which is an allowed range.  
허용된 범위인 10.0.0.0/16을 선택하겠습니다.  

Looking at the CIDR block, the first IP address is 10.0.0.0, and the last IP address is 10.0.255.255.  
CIDR 블록을 보면 첫 번째 IP는 10.0.0.0이고 마지막 IP는 10.0.255.255입니다.  

This range provides approximately 65,000 IP addresses.  
이 범위는 약 65,000개의 IP 주소를 제공합니다.  

If I were to choose a /15 CIDR block, it would be too large and not allowed.  
만약 /15 CIDR 블록을 선택하면 너무 커서 허용되지 않습니다.  

The /16 is the maximum size for your CIDR block in this context.  
이 문맥에서 /16이 CIDR 블록의 최대 크기입니다.  

For now, we will not assign any IPv6 CIDR block.  
현재로서는 IPv6 CIDR 블록을 할당하지 않습니다.  

We will explore IPv6 later in this section.  
이 섹션에서 IPv6는 나중에 다룰 예정입니다.  

---

## Tenancy Options  
## 테넌시 옵션  

Regarding tenancy, we have two options: Default or Dedicated.  
테넌시 옵션에는 Default와 Dedicated 두 가지가 있습니다.  

This setting defines how EC2 instances launch within this VPC.  
이 설정은 EC2 인스턴스가 VPC 내에서 어떻게 실행될지를 정의합니다.  

They can either run on dedicated hardware or shared hardware.  
전용 하드웨어에서 실행되거나 공유 하드웨어에서 실행될 수 있습니다.  

Dedicated hardware is very expensive, so we will use shared hardware by default.  
전용 하드웨어는 매우 비싸므로 기본적으로 공유 하드웨어를 사용합니다.  

Therefore, tenancy is set to Default.  
따라서 테넌시는 Default로 설정됩니다.  

The tag is set to DemoVPC, which is appropriate.  
태그는 DemoVPC로 설정되어 적절합니다.  

Now, let's create this VPC.  
이제 VPC를 생성해봅시다.  

The VPC has been created.  
VPC가 생성되었습니다.  

If we look at it, we see it has one IPv4 CIDR block and zero IPv6 CIDR blocks.  
확인해보면, IPv4 CIDR 블록 1개와 IPv6 CIDR 블록 0개가 있습니다.  

There is already a main route table and a main network ACL associated with it.  
이미 메인 라우트 테이블과 메인 네트워크 ACL이 연결되어 있습니다.  

These resources were created automatically behind the scenes when we created the VPC.  
이 리소스들은 VPC 생성 시 자동으로 생성된 것입니다.  

---

## Adding Additional CIDR Blocks  
## 추가 CIDR 블록 추가  

We can add other IPv4 CIDR blocks to the VPC.  
VPC에 다른 IPv4 CIDR 블록을 추가할 수 있습니다.  

Although the creation dialog allows specifying only one CIDR block, we can add more later.  
생성 창에서는 하나의 CIDR 블록만 지정 가능하지만, 나중에 추가할 수 있습니다.  

For example, by selecting Action and then Edit CIDRs, we can add a new IPv4 CIDR block such as 10.1.0.0/16, which is the next CIDR after the original one.  
예를 들어 Action → Edit CIDRs를 선택하면 원래 CIDR 이후의 10.1.0.0/16과 같은 새로운 IPv4 CIDR 블록을 추가할 수 있습니다.  

After adding the new CIDR block, we click Save.  
새 CIDR 블록을 추가한 후 저장(Save) 버튼을 클릭합니다.  

This way, the VPC can have two different CIDR blocks.  
이렇게 하면 VPC는 두 개의 서로 다른 CIDR 블록을 가질 수 있습니다.  

Similarly, we can add different IPv6 CIDR blocks if needed.  
필요하다면 IPv6 CIDR 블록도 마찬가지로 추가할 수 있습니다.  

To keep things simple, I will only have one IPv4 CIDR block for this demo.  
이번 데모에서는 단순히 IPv4 CIDR 블록 하나만 사용하겠습니다.  

However, it is important to note that you can have up to five IPv4 CIDR blocks within a single VPC, which is quite handy.  
하지만 한 VPC 내에서 최대 5개의 IPv4 CIDR 블록을 추가할 수 있다는 점은 유용합니다.  

This completes the creation of our DemoVPC.  
이로써 DemoVPC 생성이 완료되었습니다.  

This is the first step in our demonstration.  
이것이 실습의 첫 단계입니다.  

I hope you found this helpful.  
도움이 되었길 바랍니다.  

We will continue in the next lecture.  
다음 강의에서 계속 진행합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created a new VPC named DemoVPC with an IPv4 CIDR block of 10.0.0.0/16.  
- IPv4 CIDR 블록 10.0.0.0/16으로 DemoVPC라는 새로운 VPC를 생성했습니다.  

- Learned that /16 is the maximum size allowed for a CIDR block in this context.  
- 이 문맥에서 /16이 CIDR 블록의 최대 크기임을 배웠습니다.  

- Understood the difference between Default and Dedicated tenancy for EC2 instances within a VPC.  
- VPC 내 EC2 인스턴스의 Default와 Dedicated 테넌시 차이를 이해했습니다.  

- Discovered that multiple IPv4 CIDR blocks (up to five) can be added to a single VPC after creation.  
- 생성 후 단일 VPC에 여러 IPv4 CIDR 블록(최대 5개)을 추가할 수 있음을 알게 되었습니다.  
```

🎮 게임보상 완료: "VPC Creator" +300 XP 🏆
