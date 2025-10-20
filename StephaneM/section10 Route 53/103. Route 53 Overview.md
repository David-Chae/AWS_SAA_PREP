# Route 53 Overview  
# Route 53 개요  

## Introduction to Amazon Route 53  
## 아마존 Route 53 소개  

Now that we understand what DNS is, let's explore Amazon Route 53. This service is highly available, scalable, fully managed, and authoritative DNS.  
이제 DNS가 무엇인지 이해했으니, Amazon Route 53을 살펴봅시다. 이 서비스는 고가용성, 확장성, 완전 관리형, 권한 있는 DNS 서비스입니다.  

Being authoritative means that customers can update DNS records, giving them full control over their DNS configurations.  
권한 있다는 것은 사용자가 DNS 레코드를 직접 업데이트할 수 있으며, DNS 구성을 완전히 제어할 수 있다는 뜻입니다.  

The concept is that clients want to access your EC2 instance, for example, example.com. Currently, your EC2 instance only has a public IP address. To facilitate access, you write DNS records into Amazon Route 53 within a hosted zone. When a client queries example.com, Route 53 responds with the corresponding IP address, such as 54.22.33.44, allowing the client to connect directly to the EC2 instance.  
예를 들어, 클라이언트가 EC2 인스턴스(example.com)에 접근하려고 할 때, EC2는 현재 퍼블릭 IP만 가지고 있습니다. 접근을 쉽게 하기 위해 Route 53의 호스티드 존에 DNS 레코드를 작성합니다. 클라이언트가 example.com을 질의하면 Route 53은 54.22.33.44와 같은 IP 주소를 반환하여 클라이언트가 EC2에 직접 연결할 수 있게 합니다.  

Route 53 also functions as a domain registrar, enabling you to register your own domain names like example.com. This will be demonstrated in the hands-on section to help you get started with the service.  
Route 53은 도메인 등록기관 역할도 하여 example.com 같은 도메인을 직접 등록할 수 있습니다. 이는 실습 섹션에서 다루며 서비스를 시작하는 데 도움이 됩니다.  

Additionally, Route 53 allows you to monitor the health of your resources. This feature will be covered in a dedicated section. Notably, Route 53 is the only AWS service that provides a 100% availability SLA.  
또한 Route 53은 리소스의 상태 모니터링도 지원합니다. 이 기능은 별도 섹션에서 설명됩니다. 특히 Route 53은 100% 가용성을 보장하는 SLA를 제공하는 유일한 AWS 서비스입니다.  

The name "Route 53" refers to port 53, the traditional port used by DNS services.  
"Route 53"이라는 이름은 DNS 서비스가 사용하는 전통적인 포트 53을 의미합니다.  

---

## DNS Records in Route 53  
## Route 53의 DNS 레코드  

Within Route 53, you define DNS records that specify how to route traffic to a domain. Each record contains several pieces of information:  
Route 53에서는 트래픽을 도메인으로 라우팅하는 방법을 정의하는 DNS 레코드를 설정합니다. 각 레코드에는 여러 정보가 포함됩니다:  

- The domain or subdomain name, such as example.com.  
- 도메인 또는 서브도메인 이름 (예: example.com).  

- The record type, for example, A or AAAA.  
- 레코드 유형 (예: A 또는 AAAA).  

- The value of the record, such as an IP address like 12.34.56.78.  
- 레코드 값 (예: IP 주소 12.34.56.78).  

- The routing policy, which determines how Route 53 responds to queries.  
- 라우팅 정책 (Route 53이 질의에 응답하는 방식).  

- The TTL (Time To Live), which specifies how long the record is cached by DNS resolvers.  
- TTL(Time To Live) 값 (레코드가 DNS 리졸버에 캐시되는 시간).  

Route 53 supports many DNS record types. The essential ones to know are A, AAAA, CNAME, and NS records. These will be explored in the hands-on section. There are also advanced record types, but they are not required knowledge for the exam.  
Route 53은 다양한 레코드 유형을 지원합니다. 중요한 것은 A, AAAA, CNAME, NS 레코드이며, 실습에서 다룰 예정입니다. 고급 레코드도 있지만 시험 대비 필수는 아닙니다.  

---

### A Record  
The A record maps a hostname to an IPv4 address. For example, example.com can be directed to 1.2.3.4.  
A 레코드는 호스트명을 IPv4 주소와 매핑합니다. 예: example.com → 1.2.3.4  

### AAAA Record  
Similar to the A record, the AAAA record maps a hostname to an IPv6 address.  
AAAA 레코드는 A 레코드와 유사하지만 IPv6 주소에 매핑됩니다.  

### CNAME Record  
A CNAME record maps a hostname to another hostname. The target hostname can be an A or AAAA record. However, you cannot create CNAME records for the top nodes of a DNS namespace, also known as the Zone Apex. For example, you cannot create a CNAME for example.com, but you can create one for www.example.com. This will be discussed further in a future lecture.  
CNAME 레코드는 호스트명을 다른 호스트명으로 매핑합니다. 대상 호스트명은 A 또는 AAAA 레코드일 수 있습니다. 하지만 최상위 노드(Zone Apex)에는 CNAME을 만들 수 없습니다. 예: example.com은 불가, www.example.com은 가능. 이는 추후 강의에서 다룹니다.  

### NS Record  
NS records specify the name servers of the hosted zone. These are the DNS names or IP addresses of servers that respond to DNS queries for your hosted zone, controlling how traffic is routed to a domain.  
NS 레코드는 호스티드 존의 네임 서버를 지정합니다. 이는 해당 존의 DNS 질의에 응답하는 서버의 DNS 이름 또는 IP 주소로, 트래픽 라우팅을 제어합니다.  

---

## Hosted Zones  
## 호스티드 존  

Hosted zones are containers for records that define how to route traffic to a domain and its subdomains. There are two types of hosted zones:  
호스티드 존은 도메인 및 서브도메인의 트래픽 라우팅 방법을 정의하는 레코드들을 담는 컨테이너입니다. 두 가지 유형이 있습니다:  

- Public hosted zones  
- 퍼블릭 호스티드 존  

- Private hosted zones  
- 프라이빗 호스티드 존  

When you purchase a public domain name, such as mypublicdomain.com, you create a public hosted zone. Public hosted zones answer queries from the internet, for example, resolving application1.mypublicdomainname.com to its IP address.  
퍼블릭 도메인(mypublicdomain.com)을 구매하면 퍼블릭 호스티드 존이 생성됩니다. 퍼블릭 존은 인터넷에서 오는 질의에 응답합니다. 예: application1.mypublicdomainname.com → IP 주소.  

Private hosted zones are for domain names that are not publicly available. They are accessible only within your own Virtual Private Cloud (VPC). For example, application1.company.internal is a private domain name accessible only within the corporate network. Behind the scenes, this is managed by private DNS records.  
프라이빗 호스티드 존은 공개되지 않은 도메인에 사용됩니다. 오직 VPC 내부에서만 접근 가능합니다. 예: application1.company.internal → 회사 내부 네트워크 전용. 이는 프라이빗 DNS 레코드로 관리됩니다.  

For any hosted zone you create in AWS, you pay $0.50 per month. Domain registration costs start at $12 per year. Therefore, Route 53 is not a free service.  
AWS에서 생성한 호스티드 존은 개당 월 $0.50이 부과됩니다. 도메인 등록 비용은 연 $12부터 시작합니다. 따라서 Route 53은 무료 서비스가 아닙니다.  

---

## Public vs Private Hosted Zones  
## 퍼블릭 vs 프라이빗 호스티드 존  

Public hosted zones answer queries from public clients on the internet. For example, when your web browser requests example.com, it receives the corresponding IP address.  
퍼블릭 존은 인터넷의 공개 클라이언트 질의에 응답합니다. 예: 브라우저가 example.com 요청 → 해당 IP 반환.  

Private hosted zones answer queries only from within your VPC. They allow you to identify private resources with private domain names. For instance, you might have:  
프라이빗 존은 VPC 내부에서만 질의에 응답합니다. 이를 통해 프라이빗 리소스를 프라이빗 도메인 이름으로 식별할 수 있습니다. 예:  

- webapp.example.internal for one EC2 instance  
- webapp.example.internal → 특정 EC2 인스턴스  

- api.example.internal for another EC2 instance  
- api.example.internal → 다른 EC2 인스턴스  

- database.example.internal for a database  
- database.example.internal → 데이터베이스  

If the first EC2 instance requests api.example.internal, the private hosted zone responds with the private IP, such as 10.0.0.10, allowing direct connection.  
첫 번째 EC2가 api.example.internal을 요청하면 프라이빗 존은 10.0.0.10 같은 내부 IP로 응답하여 직접 연결할 수 있습니다.  

Public and private hosted zones operate similarly, but public hosted zones allow queries from the internet, while private hosted zones restrict queries to private resources within your VPC.  
퍼블릭/프라이빗 존은 유사하게 작동하지만, 퍼블릭은 인터넷 질의를 허용하고, 프라이빗은 VPC 내부 리소스로 제한됩니다.  

---

## Key Takeaways  
## 핵심 정리  

- Amazon Route 53 is a highly available, scalable, fully managed, and authoritative DNS service.  
- Route 53은 고가용성, 확장성, 완전 관리형, 권한 있는 DNS 서비스입니다.  

- Route 53 supports various DNS record types including A, AAAA, CNAME, and NS, each serving specific routing purposes.  
- A, AAAA, CNAME, NS 등 다양한 DNS 레코드를 지원하며 각각 고유한 라우팅 목적을 가집니다.  

- Hosted zones in Route 53 can be public or private, controlling DNS resolution accessibility.  
- 호스티드 존은 퍼블릭/프라이빗으로 나뉘며 DNS 해석 접근성을 제어합니다.  

- Using Route 53 incurs costs: $0.50 per hosted zone per month and domain registration fees starting at $12 per year.  
- Route 53 사용에는 비용이 발생합니다: 호스티드 존 월 $0.50, 도메인 등록 연 $12부터.  

---

🎮 **게임 보상 지급**

* 경험치: **+300XP**
* 아이템: **"Route 53 Authority Badge"** 🏅
* 업적 달성: **"DNS Architect"** 🏰

---

제가 만든 이 md 파일은 Route 53의 기초부터 레코드 유형, 퍼블릭/프라이빗 존 차이, 비용 구조까지 정리해 두었어요.
👉 혹시 이걸 **시험 대비 요약 버전**으로도 따로 만들어드릴까요?
