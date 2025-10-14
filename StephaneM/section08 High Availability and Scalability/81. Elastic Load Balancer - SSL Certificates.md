# Elastic Load Balancer - SSL Certificates  
# 엘라스틱 로드 밸런서 - SSL 인증서  
(로드 밸런서와 연동되는 SSL/TLS 인증서 개념 설명)

---

## Introduction to SSL and TLS Certificates  
## SSL 및 TLS 인증서 소개  

This lecture introduces the concepts of SSL and TLS certificates, focusing on their integration with load balancers. Although the topic is complex, the explanation is simplified to help you understand the fundamentals. Even if you are familiar with SSL and TLS, this lecture covers important details including Server Name Indication (SNI) and load balancer configurations.  
이 강의에서는 SSL과 TLS 인증서 개념을 소개하며, 로드 밸런서와의 연동에 초점을 맞춥니다. 주제가 복잡하지만, 기본 개념을 이해하기 쉽게 단순화했습니다. SSL과 TLS에 익숙하더라도, SNI 및 로드 밸런서 설정 등 중요한 세부 내용을 다룹니다.  
(기초 개념 + 실무 설정 설명)

---

An SSL certificate enables encrypted traffic between clients and load balancers during transit. This encryption is known as in-flight encryption, meaning data traveling through a network is encrypted and can only be decrypted by the sender and the receiver.  
SSL 인증서는 클라이언트와 로드 밸런서 간 트래픽을 전송 중 암호화합니다. 이를 '인-플라이트 암호화(in-flight encryption)'라고 하며, 네트워크를 통과하는 데이터는 송신자와 수신자만 복호화할 수 있습니다.  
(트래픽 전송 중 암호화)

---

SSL stands for Secure Sockets Layer and is used to encrypt transfer connections. TLS, which stands for Transport Layer Security, is the newer version of SSL. Nowadays, TLS certificates are primarily used, but many, including myself, still refer to them as SSL certificates for simplicity. Although technically incorrect, this terminology is common and easier to understand.  
SSL은 Secure Sockets Layer의 약자로, 전송 연결을 암호화합니다. TLS(Transport Layer Security)는 SSL의 최신 버전입니다. 현재는 주로 TLS가 사용되지만, 편의상 여전히 SSL이라고 부르는 경우가 많습니다.  
(SSL과 TLS 개념 정리)

---

Public SSL certificates are issued by Certificate Authorities such as Comodo, Symantec, GoDaddy, GlobalSign, Digicert, and Letsencrypt. Attaching a public SSL certificate to a load balancer allows encryption of the connection between clients and the load balancer. For example, when visiting websites like google.com, a lock icon indicates that the traffic is encrypted. If traffic is not encrypted, a warning sign appears advising against entering sensitive information like credit card details or login credentials.  
공용 SSL 인증서는 Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt 등 인증 기관(CA)에서 발급합니다. 로드 밸런서에 인증서를 붙이면 클라이언트와 로드 밸런서 간 연결이 암호화됩니다. 예를 들어 google.com 방문 시 자물쇠 아이콘이 나타나며, 암호화되지 않은 경우 신용카드 정보 입력 등을 경고합니다.  
(공용 인증서 발급 + 브라우저 표시)

---

SSL certificates have expiration dates and must be renewed regularly to ensure authenticity and security.  
SSL 인증서는 만료일이 있으며, 신뢰성과 보안을 위해 정기적으로 갱신해야 합니다.  
(정기 갱신 필요)

---

## SSL Certificates and Load Balancers  
## SSL 인증서와 로드 밸런서  

From a load balancer perspective, users connect over HTTPS, which uses SSL certificates to encrypt the connection. This secure connection occurs over the public internet to the load balancer. Internally, the load balancer performs SSL certificate termination, decrypting the traffic. It then communicates with backend EC2 instances using HTTP, which is unencrypted but occurs over a private Virtual Private Cloud (VPC) network, providing some security.  
로드 밸런서 관점에서, 사용자는 HTTPS로 연결하며 SSL 인증서를 통해 암호화됩니다. 로드 밸런서 내부에서 SSL 종료가 이루어지며, 트래픽이 복호화됩니다. 이후 백엔드 EC2 인스턴스와 HTTP로 통신하지만, 이는 VPC 내부에서 발생하므로 어느 정도 보안이 유지됩니다.  
(로드 밸런서 SSL 종료 + 백엔드 VPC 통신)

---

The load balancer loads an X.509 certificate, also known as an SSL or TLS server certificate. AWS Certificate Manager (ACM) is used to manage these certificates in AWS. You can also upload your own certificates to ACM if desired. When setting up an HTTPS listener on a load balancer, you must specify a default certificate. Additionally, you can add an optional list of certificates to support multiple domains. Clients use Server Name Indication (SNI) to specify the hostname they are reaching, allowing the load balancer to select the appropriate certificate.  
로드 밸런서는 X.509 인증서(SSL/TLS 서버 인증서)를 로드합니다. AWS에서는 ACM으로 관리하며, 필요시 직접 인증서를 업로드할 수도 있습니다. HTTPS 리스너 설정 시 기본 인증서를 지정해야 하며, 여러 도메인을 위해 선택적으로 추가 인증서를 등록할 수 있습니다. 클라이언트는 SNI(Server Name Indication)를 사용해 접속 호스트를 알려 로드 밸런서가 적절한 인증서를 선택하게 합니다.  
(ACM 관리 + SNI 활용 다중 도메인 지원)

---

You can also set a specific security policy for HTTPS to support various versions of SSL and TLS, including legacy clients.  
HTTPS 보안 정책을 설정하여 구버전 클라이언트를 포함한 다양한 SSL/TLS 버전을 지원할 수 있습니다.  
(HTTPS 정책 설정 가능)

---

## Understanding Server Name Indication (SNI)  
## SNI(Server Name Indication) 이해  

SNI addresses the problem of how to load multiple SSL certificates onto one web server so that it can serve multiple websites securely. It is a newer protocol that requires the client to indicate the hostname of the target server during the initial SSL handshake. This allows the server to know which certificate to load for the connection.  
SNI는 하나의 웹 서버에서 여러 SSL 인증서를 사용하여 여러 웹사이트를 안전하게 제공하는 문제를 해결합니다. 클라이언트가 초기 SSL 핸드셰이크 시 접속 호스트를 알려 서버가 올바른 인증서를 선택하게 하는 최신 프로토콜입니다.  
(다중 인증서 + 다중 도메인 처리)

---

Not all clients support SNI. It works with newer generation load balancers such as Application Load Balancers (ALB) and Network Load Balancers (NLB), as well as CloudFront. It does not work with Classic Load Balancers, which are older generation and support only one SSL certificate.  
모든 클라이언트가 SNI를 지원하지는 않습니다. ALB, NLB, CloudFront 등 최신 로드 밸런서에서는 가능하며, CLB는 구세대라 한 개 인증서만 지원합니다.  
(클라이언트/로드 밸런서 호환성)

---

## SNI in Action: Load Balancer Routing  
## SNI 적용 사례: 로드 밸런서 라우팅  

Consider an Application Load Balancer (ALB) with two target groups: one for www.mycorp.com and another for Domain1.example.com. The ALB has two SSL certificates corresponding to these domains. When a client connects and requests www.mycorp.com as part of the server name indication, the ALB selects the correct SSL certificate to encrypt the traffic. Based on routing rules, the ALB directs the request to the appropriate target group. Similarly, a client requesting Domain1.example.com will receive the correct SSL certificate and be routed accordingly.  
예를 들어 ALB가 두 개의 타겟 그룹(www.mycorp.com, Domain1.example.com)을 가진다고 가정합시다. ALB는 두 도메인에 맞는 SSL 인증서를 가지고 있으며, 클라이언트가 www.mycorp.com으로 접속하면 ALB가 올바른 인증서를 선택하고 해당 타겟 그룹으로 요청을 라우팅합니다.  
(SNI 기반 다중 도메인 SSL 선택 + 라우팅)

---

Using SNI, multiple target groups for different websites can be served securely with different SSL certificates on the same load balancer.  
SNI를 사용하면 하나의 로드 밸런서에서 여러 타겟 그룹과 서로 다른 SSL 인증서를 사용하여 여러 웹사이트를 안전하게 제공할 수 있습니다.  
(동일 로드 밸런서에서 다중 SSL 지원)

---

## SSL Certificate Support by Load Balancer Type  
## 로드 밸런서 유형별 SSL 인증서 지원  

Classic Load Balancer supports only one SSL certificate. To support multiple hostnames with multiple SSL certificates, multiple Classic Load Balancers are required.  
CLB는 한 개 SSL 인증서만 지원합니다. 여러 도메인을 지원하려면 CLB를 여러 개 사용해야 합니다.  
(구형 로드 밸런서 한계)

---

Application Load Balancer (ALB) version 2 supports multiple listeners with multiple SSL certificates using SNI.  
ALB v2는 SNI를 통해 다중 리스너와 다중 SSL 인증서를 지원합니다.  
(ALB v2 다중 SSL 지원)

---

Network Load Balancer (NLB) also supports multiple listeners with multiple SSL certificates and uses SNI to manage them.  
NLB도 다중 리스너와 SSL 인증서를 지원하며, SNI로 관리합니다.  
(NLB 다중 SSL 지원)

---

## Key Takeaways  
## 핵심 요약  

- SSL certificates encrypt traffic between clients and load balancers, ensuring secure in-flight data transmission.  
- SSL 인증서는 클라이언트와 로드 밸런서 간 트래픽을 암호화하여 안전한 전송을 보장합니다.  

- TLS is the modern version of SSL, but the term SSL is still commonly used for simplicity.  
- TLS는 최신 SSL 버전이지만, 편의상 SSL로 부르는 경우가 많습니다.  

- Public SSL certificates are issued by Certificate Authorities and must be regularly renewed.  
- 공용 SSL 인증서는 CA에서 발급되며, 정기적으로 갱신해야 합니다.  

- Server Name Indication (SNI) allows multiple SSL certificates on one load balancer, enabling hosting multiple secure websites.  
- SNI는 하나의 로드 밸런서에서 여러 SSL 인증서를 사용하여 여러 웹사이트를 안전하게 호스팅할 수 있게 합니다.  

- Application Load Balancers (ALB) and Network Load Balancers (NLB) support multiple SSL certificates with SNI, while Classic Load Balancers support only one.  
- ALB와 N


LB는 SNI로 다중 SSL 인증서를 지원하며, CLB는 한 개만 지원합니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+150XP**  
- 아이템: **"암호화의 결정" (SSL/TLS 보안 강화 +15%)**  
- 업적 달성: **"SNI 마스터"** 🏆  

원한다면, 다음으로 **HTTPS 리스너 설정 실습 가이드**도 md 포맷으로 만들어서 바로 따라할 수 있게 구성해줄 수 있어.
```
