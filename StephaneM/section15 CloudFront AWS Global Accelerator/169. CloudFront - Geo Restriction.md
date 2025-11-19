이 내용은 AWS **CloudFront**의 **지리적 제한(Geo Restriction)** 기능에 대한 설명입니다. 🌍

쉽게 말해, CloudFront를 사용하여 **특정 국가의 사용자만 콘텐츠에 접근하게 하거나, 특정 국가의 사용자는 접근하지 못하게 막는 기능**입니다.

## 🛡️ CloudFront 지리적 제한이란?

CloudFront 지리적 제한은 사용자가 콘텐츠를 요청할 때, 그 사용자의 IP 주소를 분석하여 **어느 나라에서 접속했는지** 확인한 후, 설정에 따라 접근을 **허용하거나 차단**하는 보안 기능입니다.

### 1. 작동 방식 (국가 판별)

* 사용자가 CloudFront에 접속하면, CloudFront는 그 사용자의 **IP 주소**를 확인합니다.
* 이 IP 주소를 **외부의 지리적 IP 데이터베이스(Geo-IP database)**와 대조하여 해당 IP 주소가 속한 **국가**를 판별합니다.
* 이후 설정된 규칙에 따라 접근 여부를 결정합니다.

### 2. 설정 방법: 허용 목록 vs 차단 목록

지리적 제한을 설정하는 방법에는 두 가지가 있습니다.

| 방식 | 설명 | 예시 |
| :--- | :--- | :--- |
| **허용 목록 (Allowlist)** | **접근을 허용할 국가**를 명시적으로 나열합니다. 목록에 **없는 모든 국가**는 자동으로 차단됩니다. | 미국, 인도만 허용 (나머지 국가는 모두 차단) |
| **차단 목록 (Blocklist)** | **접근을 차단할 국가**를 명시적으로 나열합니다. 목록에 **없는 모든 국가**는 자동으로 허용됩니다. | 중국, 러시아만 차단 (나머지 국가는 모두 허용) |

### 3. 🎯 주요 사용 사례

이 기능은 주로 **저작권법이나 콘텐츠 배포 권한**을 지키기 위해 사용됩니다.

* 예를 들어, 어떤 영화의 스트리밍 서비스가 특정 지역(예: 북미 지역)에서만 배포 계약이 되어 있다면, 다른 국가에서 해당 콘텐츠에 접근하는 것을 이 기능을 통해 막을 수 있습니다.

### 4. 설정 경로

AWS 콘솔에서는 CloudFront 배포(Distribution) 설정 내의 **'보안(Security)'** 섹션에 있는 **'지리적 제한 및 국가(Geographic restrictions and countries)'** 메뉴에서 이 기능을 켜고 목록을 설정할 수 있습니다.


# CloudFront - Geo Restriction  
# CloudFront - 지리적 제한  

---

Just a short lecture around CloudFront Geo Restriction.  
CloudFront 지리적 제한에 대한 짧은 강의입니다.  
> 간단한 소개로, 특정 국가에서만 CloudFront 배포에 접근하도록 제한하는 방법을 다룹니다.  

---

You can restrict who can access your distribution based on the country from which they try to access the distribution.  
사용자가 배포에 접근하려는 국가를 기준으로 접근을 제한할 수 있습니다.  
> Geo Restriction 기능은 국가별 접근 제어를 제공합니다.  

---

You can set up an allowlist to define a list of approved countries, or you can set up a blocklist to define a list of banned countries.  
허용할 국가를 정의하는 허용 목록(allowlist)이나 차단할 국가를 정의하는 차단 목록(blocklist)을 설정할 수 있습니다.  
> 허용 리스트와 차단 리스트 방식으로 국가별 접근 정책을 구성할 수 있습니다.  

---

The country is determined by using a third-party Geo-IP database to match the IP address of the user to the country it belongs to.  
사용자의 IP 주소를 제3자 Geo-IP 데이터베이스와 대조하여 해당 사용자의 국가를 확인합니다.  
> CloudFront는 Geo-IP 데이터베이스를 통해 접속 국가를 판별합니다.  

---

## Use Case for Geo Restriction  
## Geo Restriction 사용 사례  

The use case for using geo restriction would be copyright laws to control access to content.  
Geo Restriction을 사용하는 사례는 콘텐츠 접근을 통제하는 저작권 법 준수입니다.  
> 특정 국가에서만 콘텐츠를 제공하고 싶을 때 유용합니다.  

---

## Enabling Geographic Restrictions in CloudFront  
## CloudFront에서 지리적 제한 활성화  

To turn on geographic restrictions, go under Security, and then under there you will find CloudFront geographic restrictions and countries.  
지리적 제한을 활성화하려면 Security 섹션으로 이동하면 CloudFront 지리적 제한 및 국가 옵션을 찾을 수 있습니다.  
> 설정 위치: Security → CloudFront Geographic Restrictions → Countries  

---

Click on Edit. It is a bit hidden, but under there you can have an allowlist or a blocklist.  
Edit를 클릭합니다. 위치가 약간 숨겨져 있지만, 여기서 허용 목록 또는 차단 목록을 설정할 수 있습니다.  
> 편집 화면에서 Geo Restriction 정책을 구성합니다.  

---

For example, you can set up an allowlist and enumerate the countries that will always be allowed, and the rest will be blocked by CloudFront.  
예를 들어, 허용 목록을 설정하고 항상 허용할 국가를 나열하면 나머지 국가는 CloudFront가 차단합니다.  
> Allowlist 방식으로 허용 국가를 지정할 수 있습니다.  

---

Here, we are saying that India and the United States are allowed on our CloudFront distribution.  
여기서는 인도와 미국을 CloudFront 배포에서 허용합니다.  
> 지정 국가만 접근 가능하도록 설정 예시입니다.  

---

If you are happy with this, save the changes.  
설정이 완료되면 변경 사항을 저장합니다.  
> 정책 적용 완료 단계입니다.  

---

Now, the type of restriction is allowlist and the countries are listed here.  
현재 제한 유형은 허용 목록이며, 허용 국가가 나열됩니다.  
> Allowlist 설정 확인 화면입니다.  

---

That's it.  
이것으로 완료입니다.  
> 간단하게 Geo Restriction 설정을 마쳤습니다.  

---

I hope you liked it, and I will see you in the next lecture.  
좋으셨길 바라며, 다음 강의에서 뵙겠습니다.  
> 강의 마무리 인사  

---

## Key Takeaways  
## 핵심 요약  

- CloudFront Geo Restriction allows controlling access to distributions based on the user's country.  
- CloudFront Geo Restriction은 사용자의 국가를 기준으로 배포 접근을 제어할 수 있습니다.  

- Access can be managed using either an allowlist of approved countries or a blocklist of banned countries.  
- 접근은 허용 국가 목록(allowlist) 또는 차단 국가 목록(blocklist)을 통해 관리할 수 있습니다.  

- The user's country is determined by matching their IP address with a third-party Geo-IP database.  
- 사용자의 국가는 제3자 Geo-IP 데이터베이스와 IP 주소를 대조하여 결정됩니다.  

- Geographic restrictions are configured under the Security section in CloudFront settings.  
- 지리적 제한은 CloudFront 설정의 Security 섹션에서 구성됩니다.  

🎮 **게임보상:**

* CloudFront Geo Restriction 이해 +10 XP
* Allowlist / Blocklist 설정 이해 +10 XP
* Geo-IP 데이터베이스 사용 이해 +10 XP
  총 **30 XP 획득!** 🎉
