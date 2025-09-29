# Elastic Load Balancer - SSL Certificates - Hands On  
# 엘라스틱 로드 밸런서 - SSL 인증서 실습  

---

## Enabling SSL Certificates on Load Balancers  
## 로드 밸런서에서 SSL 인증서 활성화  

Let's explore how to enable SSL certificates on both the Application Load Balancer (ALB) and the Network Load Balancer (NLB).  
Application Load Balancer(ALB)와 Network Load Balancer(NLB)에서 SSL 인증서를 활성화하는 방법을 살펴보겠습니다.  
(ALB/NLB SSL 활성화 실습 소개)

---

## Configuring SSL on Application Load Balancer (ALB)  
## Application Load Balancer(ALB)에서 SSL 구성  

To enable SSL on the ALB, add a listener with the following settings:  
ALB에서 SSL을 활성화하려면, 다음 설정으로 리스너를 추가합니다.  
(ALB 리스너 설정 시작)

- Protocol: HTTPS  
- 프로토콜: HTTPS  

- Port: 443 (default)  
- 포트: 443 (기본값)  

This listener will accept client connections on port 443 using HTTPS and forward traffic to a specific target group.  
이 리스너는 클라이언트 연결을 HTTPS 443 포트에서 수락하고 특정 타겟 그룹으로 트래픽을 전달합니다.  
(HTTPS 수신 + 트래픽 전달)

---

You can also configure secure listener settings such as the SSL security policy. This policy determines how the certificates are negotiated, including compatibility with older versions of SSL or TLS. If you do not have specific requirements, you can leave this setting as the default.  
SSL 보안 정책과 같은 보안 리스너 설정도 구성할 수 있습니다. 이 정책은 인증서 협상 방식과 구버전 SSL/TLS 호환성을 결정합니다. 특별한 요구사항이 없으면 기본값으로 둬도 됩니다.  
(SSL 정책 설정)

---

Next, specify the location of the SSL or TLS certificate. The certificate can be:  
다음으로 SSL/TLS 인증서 위치를 지정합니다. 인증서는 다음과 같이 구성할 수 있습니다.  
(인증서 위치 선택)

- Stored in AWS Certificate Manager (ACM)  
- AWS Certificate Manager(ACM)에 저장  

- Stored in IAM (not recommended as a domain method)  
- IAM에 저장 (도메인 방법으로는 권장하지 않음)  

- Imported manually by pasting the private key, certificate body, and certificate chain  
- 개인 키, 인증서 본문, 인증서 체인을 붙여 수동으로 가져오기  

Importing the certificate this way will add it directly into ACM.  
이 방식으로 가져오면 인증서가 직접 ACM에 추가됩니다.  
(ACM 직접 추가)

---

## Configuring SSL on Network Load Balancer (NLB)  
## Network Load Balancer(NLB)에서 SSL 구성  

The process for enabling SSL on the Network Load Balancer is similar:  
NLB에서 SSL을 활성화하는 과정도 유사합니다.  
(NLB SSL 설정)

- Add a listener with protocol set to TLS.  
- 프로토콜을 TLS로 설정한 리스너 추가  

- Forward traffic to the desired target group.  
- 원하는 타겟 그룹으로 트래픽 전달  

- Set the security policy according to your requirements.  
- 요구사항에 따라 보안 정책 설정  

- Choose the certificate source from ACM, IAM, or import it manually.  
- 인증서 소스를 ACM, IAM, 또는 수동 가져오기 중 선택  

- Optionally, configure application layer protocol negotiation (ALPN), which is an advanced TLS setting.  
- 선택적으로 ALPN(Application Layer Protocol Negotiation) 설정 가능 (고급 TLS 옵션)  

---

This concludes the overview of using SSL or TLS certificates on your load balancers. Implementing these settings ensures secure communication between clients and your applications.  
로드 밸런서에서 SSL/TLS 인증서를 사용하는 개요를 마칩니다. 이러한 설정을 적용하면 클라이언트와 애플리케이션 간 안전한 통신이 보장됩니다.  
(SSL/TLS 적용 완료)

---

## Key Takeaways  
## 핵심 요약  

- Enabled SSL certificates on both Application Load Balancer (ALB) and Network Load Balancer (NLB).  
- ALB와 NLB에서 SSL 인증서 활성화  

- Configured HTTPS listeners with default port 443 for ALB.  
- ALB에서 기본 포트 443으로 HTTPS 리스너 구성  

- Set SSL security policies to manage certificate negotiation and compatibility.  
- 인증서 협상과 호환성을 관리하기 위해 SSL 보안 정책 설정  

- Imported certificates directly into AWS Certificate Manager (ACM) or selected from IAM, with recommendation to use ACM.  
- 인증서를 ACM에 직접 가져오거나 IAM에서 선택 (권장: ACM 사용)  

- Configured TLS listeners and security policies on NLB with options for certificate sources and advanced application layer protocol negotiation.  
- NLB에서 TLS 리스너와 보안 정책 구성, 인증서 소스 선택 및 ALPN 고급 옵션 설정  

---

🎮 **게임 보상 지급**

* 경험치: **+160XP**
* 아이템: **"TLS 방패" (통신 암호화 강화 +20%)**
* 업적 달성: **"로드 밸런서 보안 마스터"** 🏆

원하면 다음 단계로 **ALB/NLB HTTPS 리스너 실습 스텝 바이 스텝 가이드**도 만들어서 바로 따라할 수 있게 해줄 수 있습니다.
