# What is a DNS?  
# DNS란 무엇인가?  

## Introduction to DNS  
## DNS 소개  

Before discussing Route 53, it is essential to understand what DNS is.  
Route 53를 논의하기 전에, DNS가 무엇인지 이해하는 것이 중요합니다.  
(Route 53 이해를 위해 DNS 기초 필요)  

This is a basic-level lecture designed to help you comprehend how DNS works.  
이 강의는 DNS가 어떻게 작동하는지 이해하도록 돕는 기초 수준 강의입니다.  
(DNS 작동 원리 학습 목적)  

You have been using DNS behind the scenes every day, although you may not know the exact details.  
여러분은 매일 DNS를 백그라운드에서 사용하고 있지만, 정확한 세부사항은 모를 수 있습니다.  
(일상 속 DNS 사용)  

---

## DNS Definition  
## DNS 정의  

DNS stands for Domain Name System.  
DNS는 Domain Name System의 약자입니다.  
(도메인 이름 시스템)  

Its primary function is to translate human-friendly hostnames into the target server IP addresses.  
주요 기능은 사람이 이해하기 쉬운 호스트 이름을 대상 서버의 IP 주소로 변환하는 것입니다.  
(호스트명 → IP 변환)  

For example, when you type www.google.com into your web browser, DNS ultimately returns an IP address.  
예를 들어, 브라우저에 www.google.com을 입력하면 DNS가 최종적으로 IP 주소를 반환합니다.  
(DNS의 실제 동작 예시)  

This IP address allows your browser to access Google's servers and retrieve data.  
이 IP 주소 덕분에 브라우저는 구글 서버에 접근하여 데이터를 가져올 수 있습니다.  
(IP를 통해 서버 접근)  

DNS is the backbone of the internet.  
DNS는 인터넷의 근간입니다.  
(인터넷 핵심 인프라)  

It enables the translation of URLs and hostnames into IP addresses, which computers use to communicate.  
컴퓨터가 통신할 수 있도록 URL과 호스트명을 IP 주소로 변환합니다.  
(URL → IP 변환 기능)  

---

## DNS Hierarchical Naming Structure  
## DNS 계층적 이름 구조  

DNS uses a hierarchical naming structure.  
DNS는 계층적 이름 구조를 사용합니다.  
(계층적 도메인 구조)  

For example, in www.google.com, the hierarchy is as follows:  
예를 들어 www.google.com의 계층 구조는 다음과 같습니다.  

- At the root is the dot (.).  
- 루트는 점(.)으로 표시됩니다.  
- Next is the top-level domain (TLD), such as .com.  
- 다음은 최상위 도메인(TLD), 예: .com  
- Then the second-level domain, like google.com.  
- 그 다음은 2차 도메인, 예: google.com  
- Finally, subdomains such as www.google.com or api.google.com.  
- 마지막으로 서브도메인, 예: www.google.com 또는 api.google.com  

All these components form the hierarchy of domain names.  
이 모든 요소가 도메인 이름의 계층 구조를 형성합니다.  
(계층적 구조 이해)  

---

## DNS Terminology  
## DNS 용어  

Let's define some key DNS terminology:  
몇 가지 핵심 DNS 용어를 정의합니다.  

- Domain Registrar: The service where you register your domain names. Examples include Amazon Route 53 and GoDaddy.  
- 도메인 등록기관: 도메인을 등록하는 서비스. 예: Amazon Route 53, GoDaddy  

- DNS Records: Different types of records that map hostnames to IP addresses or other data. Examples include A, AAAA, CNAME, NS records.  
- DNS 레코드: 호스트명과 IP 주소 또는 기타 데이터를 매핑하는 다양한 레코드. 예: A, AAAA, CNAME, NS  

- Zone File: A file containing all DNS records for a domain.  
- 존 파일: 특정 도메인의 모든 DNS 레코드를 포함한 파일  

- Name Servers: Servers that resolve DNS queries.  
- 네임 서버: DNS 질의를 해결하는 서버  

- Top-Level Domains (TLDs): Examples include .com, .us, .in, .gov, .org.  
- 최상위 도메인(TLD): 예: .com, .us, .in, .gov, .org  

- Second-Level Domain: For example, amazon.com or google.com.  
- 2차 도메인: 예: amazon.com, google.com  

Understanding these terms is crucial for managing DNS.  
이 용어들을 이해하는 것은 DNS 관리에 매우 중요합니다.  
(DNS 관리 핵심 용어)  

---

## Fully Qualified Domain Name (FQDN) and URL Structure  
## FQDN 및 URL 구조  

Consider the FQDN http://api.www.example.com.  
FQDN 예시: http://api.www.example.com  

- The last dot at the end represents the root of all domain names.  
- 마지막 점(.)은 모든 도메인의 루트를 나타냅니다.  

- .com is the top-level domain (TLD).  
- .com은 최상위 도메인(TLD)입니다.  

- example.com is the second-level domain.  
- example.com은 2차 도메인입니다.  

- www.example.com is a subdomain.  
- www.example.com은 서브도메인입니다.  

- api.www.example.com is the fully qualified domain name (FQDN).  
- api.www.example.com은 완전한 도메인 이름(FQDN)입니다.  

- HTTP is the protocol.  
- HTTP는 프로토콜입니다.  

Together, these components form the complete URL.  
이 모든 요소가 합쳐져 완전한 URL을 구성합니다.  
(URL 구조 이해)  

---

## How DNS Works  
## DNS 작동 원리  

Suppose you have a web server with a public IP address, for example, 9.10.11.12, such as an EC2 instance.  
예를 들어, 공인 IP 9.10.11.12를 가진 웹 서버(EC2 인스턴스)가 있다고 가정합니다.  

You want to access this server using the domain name example.com.  
example.com 도메인을 통해 이 서버에 접근하고 싶습니다.  

You register this domain name with a DNS server.  
이 도메인을 DNS 서버에 등록합니다.  

When your web browser wants to access example.com, it asks its local DNS server, "Do you know what example.com is?"  
브라우저가 example.com에 접근하려고 하면, 로컬 DNS 서버에 "example.com을 아는가?"라고 질의합니다.  

The local DNS server is usually assigned and managed by your company or internet service provider dynamically.  
로컬 DNS 서버는 일반적으로 회사나 ISP에서 동적으로 할당하고 관리합니다.  

If the local DNS server has never seen this query before, it will ask the root DNS server managed by the ICANN organization, "Do you know what example.com is?"  
로컬 DNS 서버가 해당 질의를 처음 접하면, ICANN이 관리하는 루트 DNS 서버에 질의합니다.  

The root DNS server replies, "I do not have the answer, but I know about .com."  
루트 DNS 서버는 "답은 없지만 .com에 대해서는 알고 있다"고 응답합니다.  

It returns the name server (NS) record for .com with its IP address, for example, 1234.  
루트 서버는 .com의 네임서버(NS) 레코드와 IP(예: 1234)를 반환합니다.  

This response tells the local DNS server that the .com domain name server can provide more specific information.  
이 응답은 로컬 DNS 서버에게 .com 도메인 서버가 더 구체적인 정보를 제공할 수 있음을 알려줍니다.  

The local DNS server then queries the .com domain server at IP 1234, asking for example.com.  
그 다음 로컬 DNS 서버는 IP 1234의 .com 도메인 서버에 example.com 정보를 요청합니다.  

This .com domain server, managed by IANA, replies that it knows about example.com but does not have the exact answer.  
IANA가 관리하는 .com 서버는 example.com 정보를 알고 있지만 정확한 IP는 없다고 응답합니다.  

It provides the IP address of the name server responsible for example.com, for example, 5.6.7.8.  
그 대신 example.com을 담당하는 네임 서버의 IP(예: 5.6.7.8)를 제공합니다.  

Next, the local DNS server queries the second-level domain DNS server at 5.6.7.8, which is managed by your domain registrar, such as Amazon Route 53.  
그 후 로컬 DNS 서버는 5.6.7.8의 2차 도메인 DNS 서버(예: Amazon Route 53)에게 질의합니다.  

It asks, "Do you know about example.com?"  
질문: "example.com을 아는가?"  

This DNS server has an entry for example.com and replies, "Yes, I know example.com. It is an A record with the IP address 9.10.11.12."  
DNS 서버는 example.com 레코드가 있어 "알고 있다. IP는 9.10.11.12(A 레코드)"라고 응답합니다.  

The local DNS server now has the answer by recursively querying DNS servers and finding the most specific one.  
로컬 DNS 서버는 재귀 질의를 통해 가장 구체적인 DNS 서버에서 답을 얻습니다.  

It caches this answer so that if someone asks again for example.com, it can respond immediately.  
이 답을 캐시하여 다음에 example.com 요청 시 즉시 응답할 수 있습니다.  

Finally, it sends the IP address back to your browser, which can then access the web server.  
마지막으로 브라우저에 IP를 전달하여 웹 서버에 접근합니다.  

---

## Summary  
## 요약  

You have been using DNS behind the scenes your entire life, such as when accessing www.google.com or any other
```


website.
[www.google.com](http://www.google.com) 등 웹사이트 접근 시 DNS를 계속 사용해 왔습니다.

Now, you understand how DNS queries work through recursive resolution from root servers to authoritative name servers.
이제 루트 서버에서 권한 있는 네임 서버까지 재귀적으로 DNS 질의가 어떻게 작동하는지 이해합니다.

This background knowledge prepares you to manage your own DNS server using Route 53 in the upcoming lectures.
이 지식을 바탕으로 다음 강의에서 Route 53으로 DNS 서버를 관리할 준비가 됩니다.

---

## Key Takeaways

## 핵심 정리

* DNS translates human-friendly hostnames into IP addresses, enabling web browsers to access servers.

* DNS는 사람이 읽을 수 있는 호스트명을 IP 주소로 변환하여 브라우저가 서버에 접근하도록 합니다.

* DNS has a hierarchical naming structure including top-level domains, second-level domains, and subdomains.

* DNS는 TLD, 2차 도메인, 서브도메인을 포함하는 계층적 구조를 가집니다.

* DNS resolution involves recursive queries starting from the root DNS server down to authoritative name servers.

* DNS 해석은 루트 서버에서 권한 있는 네임 서버까지 재귀적 질의를 통해 이루어집니다.

* Local DNS servers cache responses to improve query efficiency and reduce latency.

* 로컬 DNS 서버는 응답을 캐시하여 질의 효율을 높이고 지연 시간을 줄입니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+250XP**  
- 아이템: **"DNS Hierarchy Map"**  
- 업적 달성: **"Master of DNS Basics"** 🛡️  

이 MD 파일은 DNS 기초부터 계층 구조, 재귀적 해석까지 단계별로 이해할 수 있도록 구성했습니다.
