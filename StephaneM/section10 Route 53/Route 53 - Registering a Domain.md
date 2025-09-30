# Route 53 - Registering a Domain  
# Route 53 - 도메인 등록  

## Introduction to Route 53 Domain Registration  
## Route 53 도메인 등록 소개  

We are now in Route 53, and we will be registering domains. Currently, there is one hosted zone and one domain in my account because I have used it before. You should have none at this point. Let's proceed to register a domain.  
지금 우리는 Route 53에 있으며, 도메인을 등록할 예정입니다. 제 계정에는 이미 하나의 호스티드 존과 도메인이 있습니다. 하지만 여러분은 아마 없을 겁니다. 이제 도메인을 등록해봅시다.  

On the left-hand side, click on Register Domains. You will see a new console experience. If you do not have it, you can switch to the new console by clicking the appropriate option. I will use the new console as this is the direction moving forward.  
왼쪽 메뉴에서 "Register Domains"를 클릭하세요. 새로운 콘솔 화면이 나타납니다. 만약 해당 화면이 없으면 옵션을 눌러 새 콘솔로 전환할 수 있습니다. 앞으로는 이 새 콘솔을 사용할 예정입니다.  

Here, you can enter a domain name. For example, I have registered stephanetheteacher.com previously. You will have nothing initially. To get started with Route 53, you need to register your own domain.  
여기서 원하는 도메인 이름을 입력할 수 있습니다. 예를 들어, 저는 stephanetheteacher.com을 등록한 적이 있습니다. 처음에는 아무것도 없을 겁니다. Route 53을 시작하려면 도메인을 등록해야 합니다.  

Please note that registering a domain will cost money. If you do not want to pay approximately $12 per year for a domain name, you may choose not to proceed with this section.  
도메인 등록에는 비용이 든다는 점을 주의하세요. 연간 약 $12 정도의 비용을 지불하고 싶지 않다면 이 과정을 진행하지 않아도 됩니다.  

To register a domain, enter a domain name that no one else has chosen before. The goal is to select a unique domain name.  
도메인을 등록하려면 아직 아무도 선택하지 않은 고유한 도메인 이름을 입력해야 합니다.  

Once you enter a domain name, the system will check its availability. For example, I found a domain available for $13 per year. I will select it, and it will be added to my basket. Then, proceed to checkout.  
도메인 이름을 입력하면 시스템이 사용 가능 여부를 확인합니다. 예를 들어, 연간 $13에 등록 가능한 도메인을 찾았습니다. 이를 선택하면 장바구니에 담기고, 결제 단계로 진행합니다.  

On the checkout page, you can choose the duration of registration, such as one year. You may also enable or disable auto-renewal. If you intend to keep the domain, it is advisable to leave auto-renewal enabled to prevent losing the domain. If you do not want to keep it after the year, you can disable auto-renewal.  
결제 페이지에서 등록 기간(예: 1년)을 선택할 수 있습니다. 자동 갱신 옵션을 켜거나 끌 수도 있습니다. 도메인을 계속 유지하려면 자동 갱신을 켜두는 것이 좋습니다. 그렇지 않다면 꺼도 됩니다.  

Keeping auto-renewal on is important because if you lose the domain, someone else could buy it, which is undesirable.  
자동 갱신은 매우 중요합니다. 도메인을 잃으면 다른 사람이 구매할 수 있기 때문입니다.  

After setting the duration and auto-renewal preferences, click Next to proceed to the contact information page. This information is pre-populated from your account, but you can enter your own details if desired.  
기간과 자동 갱신을 설정한 뒤, "Next"를 클릭하면 연락처 정보 페이지로 이동합니다. 기본적으로 계정 정보가 채워져 있지만, 원한다면 직접 수정할 수 있습니다.  

The admin contact and tech contact can be the same as the registrant contact.  
관리자 연락처와 기술 담당 연락처는 등록자 연락처와 동일하게 설정할 수 있습니다.  

It is important to enable privacy protection. This feature prevents you from receiving spam and hides your real contact information such as your personal address and phone number from the internet.  
개인정보 보호 기능을 반드시 켜는 것이 좋습니다. 이를 통해 스팸을 방지하고 주소, 전화번호 같은 개인정보가 공개되지 않게 할 수 있습니다.  

After enabling privacy protection, click Next to reach the review page. Ensure all information is correct, then check the terms and conditions. When you submit, you will be charged the registration fee (e.g., $13). Please do not proceed if you do not wish to pay this amount.  
개인정보 보호를 켠 후 "Next"를 클릭하면 검토 페이지로 이동합니다. 모든 정보가 정확한지 확인하고, 약관에 동의한 후 제출하면 등록비(예: $13)가 청구됩니다. 비용을 지불하기 싫다면 진행하지 마세요.  

The domain registration process will take some time, ranging from a few minutes to a few hours. Once complete, you can verify the registration by navigating to Hosted Zones on the left-hand side and selecting your domain name.  
도메인 등록은 몇 분에서 몇 시간까지 걸릴 수 있습니다. 완료되면 왼쪽 메뉴의 "Hosted Zones"에서 도메인을 확인할 수 있습니다.  

In the hosted zone, you will see DNS records. Typically, you should have two records: the NS (Name Server) record and the SOA (Start of Authority) record. I have four records because of previous usage.  
호스티드 존에는 DNS 레코드가 표시됩니다. 보통 NS(네임 서버) 레코드와 SOA(권한 시작) 레코드 두 개가 있습니다. 저는 이전 사용 기록 때문에 네 개가 있습니다.  

The NS record indicates that AWS DNS servers should be used to resolve DNS queries. This means that Route 53 is now the source of truth for your DNS records.  
NS 레코드는 AWS DNS 서버가 질의를 해석한다는 의미입니다. 즉, Route 53이 이제 DNS 기록의 최종 권한자가 된 것입니다.  

Any DNS records you add, such as A records or CNAMEs, will be managed within Route 53. I will teach you how to add these records in the next lecture.  
추가하는 모든 DNS 레코드(A, CNAME 등)는 Route 53에서 관리됩니다. 다음 강의에서 추가 방법을 배울 것입니다.  

With the domain registered and hosted zone configured, you are ready to proceed with hands-on activities.  
도메인이 등록되고 호스티드 존이 구성되었으므로 이제 실습을 진행할 준비가 되었습니다.  

I hope you found this lecture helpful. See you in the next lecture.  
이 강의가 도움이 되었기를 바랍니다. 다음 강의에서 만나요.  

---

## Key Takeaways  
## 핵심 정리  

- Registered a domain using AWS Route 53 through the new console experience.  
- 새 콘솔을 통해 AWS Route 53에서 도메인을 등록하는 방법을 배웠습니다.  

- Learned the importance of enabling auto-renewal to retain domain ownership.  
- 도메인 소유권 유지를 위해 자동 갱신을 켜는 것이 중요함을 배웠습니다.  

- Understood the significance of privacy protection to hide personal contact information.  
- 개인정보 보호 기능의 중요성을 이해했습니다.  

- Verified domain registration by checking hosted zones and DNS records in Route 53.  
- 호스티드 존과 DNS 레코드를 확인하여 도메인 등록을 검증했습니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+250XP**
* 아이템: **"Domain Guardian Cloak" (개인정보 보호 +50%)** 🧥
* 업적 달성: **"Registrar of Truth"** 📜
