# 3rd Party Domains & Route 53  
# 서드파티 도메인 & Route 53  

## Distinction Between Domain Registrar and DNS Service  
## 도메인 등록기관과 DNS 서비스의 구분  

It is important to distinguish between a domain registrar and a DNS service.  
도메인 등록기관과 DNS 서비스는 구분하는 것이 중요합니다.  

You can purchase your domain name from any domain registrar you prefer, and you will pay annual charges for it.  
원하는 도메인 등록기관에서 도메인을 구매할 수 있으며, 매년 비용을 지불하게 됩니다.  

In this course, we have used the Amazon Registrar through the Route 53 console, but you can use any domain name registrar such as GoDaddy or Google Domains.  
이 강의에서는 Route 53 콘솔을 통해 Amazon 등록기관을 사용했지만, GoDaddy나 Google Domains 같은 다른 도메인 등록기관도 사용할 수 있습니다.  

Usually, when you register a domain with a registrar, they also provide a DNS service to manage your DNS records.  
일반적으로 도메인을 등록하면, 등록기관에서 DNS 레코드를 관리할 수 있는 DNS 서비스도 제공합니다.  

For example, when we registered a domain name with Amazon, we had a Route 53 hosted zone to manage our DNS records.  
예를 들어 Amazon에서 도메인을 등록하면, Route 53 호스티드 존을 통해 DNS 레코드를 관리하게 됩니다.  

---

## Using Different Providers for Domain Registration and DNS Management  
## 도메인 등록과 DNS 관리에 다른 제공자 사용  

It is possible to choose not to use AWS Route 53 as your DNS service even if you registered your domain with Amazon Registrar.  
Amazon 등록기관에서 도메인을 등록했더라도 AWS Route 53을 DNS 서비스로 사용하지 않을 수 있습니다.  

Conversely, you can register your domain with GoDaddy and use Amazon Route 53 to manage your DNS records.  
반대로, GoDaddy에서 도메인을 등록하고 Amazon Route 53을 사용하여 DNS 레코드를 관리할 수도 있습니다.  

This is a perfectly acceptable combination.  
이 조합은 완전히 허용되는 방법입니다.  

---

## How to Configure Route 53 with a Third-Party Registrar  
## 서드파티 등록기관과 Route 53 연동 방법  

For example, if you register your domain on GoDaddy, you will have an option to specify custom name servers.  
예를 들어 GoDaddy에서 도메인을 등록하면, 커스텀 네임서버를 지정할 수 있는 옵션이 있습니다.  

To do this, first go to Amazon Route 53 and create a public hosted zone for your domain.  
이를 위해 먼저 Amazon Route 53에 접속하여 도메인용 퍼블릭 호스티드 존을 생성합니다.  

In the hosted zone details, you will find four name servers listed on the right-hand side.  
호스티드 존 세부 정보에서 오른쪽에 4개의 네임서버가 나열되어 있습니다.  

You need to update the name servers on the GoDaddy website to these Route 53 name servers.  
GoDaddy 웹사이트에서 네임서버를 이 Route 53 네임서버로 업데이트해야 합니다.  

This way, when GoDaddy receives a DNS query asking which name server to use, it will point to the Amazon Route 53 name servers.  
이렇게 하면 GoDaddy가 DNS 쿼리를 받을 때 어떤 네임서버를 사용할지 묻는 경우, Amazon Route 53 네임서버를 가리키게 됩니다.  

Consequently, you can manage all your DNS records from the Route 53 console.  
따라서 모든 DNS 레코드를 Route 53 콘솔에서 관리할 수 있습니다.  

---

## Summary  
## 요약  

To summarize, if you buy your domain from a third-party registrar, you can still use Route 53 as your DNS service provider.  
정리하면, 서드파티 등록기관에서 도메인을 구매해도 Route 53을 DNS 서비스로 사용할 수 있습니다.  

You need to create a public hosted zone in Route 53 and then update the NS (name server) records on the registrar's website to point to the Route 53 name servers.  
Route 53에서 퍼블릭 호스티드 존을 생성한 후, 등록기관 웹사이트에서 NS 레코드를 Route 53 네임서버로 업데이트하면 됩니다.  

It is important to understand that a domain registrar is different from a DNS service, even though most domain registrars usually provide some DNS features.  
대부분의 등록기관이 DNS 기능을 제공하지만, 도메인 등록기관과 DNS 서비스는 별개라는 점을 이해하는 것이 중요합니다.  

---

## Key Takeaways  
## 핵심 포인트  

- A domain registrar is where you purchase your domain name, and it is distinct from a DNS service provider.  
  도메인 등록기관은 도메인을 구매하는 곳이며, DNS 서비스 제공자와 별개입니다.  

- You can register your domain with any registrar, such as GoDaddy or Google Domains, and still use Amazon Route 53 to manage your DNS records.  
  GoDaddy나 Google Domains와 같은 어떤 등록기관에서도 도메인을 등록하고, Amazon Route 53으로 DNS 레코드를 관리할 수 있습니다.  

- To use Route 53 with a third-party registrar, create a public hosted zone in Route 53 and update the name server (NS) records on your registrar's website to point to Route 53's name servers.  
  서드파티 등록기관과 Route 53을 사용하려면, Route 53에서 퍼블릭 호스티드 존을 생성하고 등록기관 웹사이트에서 NS 레코드를 Route 53 네임서버로 업데이트해야 합니다.  

- Although most domain registrars provide DNS services, you have the flexibility to separate domain registration and DNS management across different providers.  
  대부분의 등록기관이 DNS 서비스를 제공하지만, 도메인 등록과 DNS 관리를 서로 다른 제공자에서 분리하여 사용할 수 있는 유연성이 있습니다.  

---

💡 **게임 보상:**

* 🌐 도메인 등록기관과 DNS 서비스의 차이 이해 = +40 EXP
* 🔗 서드파티 등록기관과 Route 53 연동 방법 학습 = +60 EXP
* 🛠️ 퍼블릭 호스티드 존과 NS 레코드 설정 실습 이해 = +50 EXP
  **총 보상: 150 EXP + Domain Master 뱃지 🏅**
