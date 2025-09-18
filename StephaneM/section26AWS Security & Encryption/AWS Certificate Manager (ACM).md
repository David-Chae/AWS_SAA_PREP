```markdown
# AWS Certificate Manager (ACM)  
# AWS 인증서 관리자 (ACM)  

🎮 게임보상: "ACM 기초 학습 완료" +500 XP  

---

## Introduction to AWS Certificate Manager (ACM)  
## AWS 인증서 관리자(ACM) 소개  

AWS Certificate Manager, also known as ACM, allows you to easily provision, manage, and deploy TLS certificates on AWS.  
AWS Certificate Manager(ACM)는 AWS에서 TLS 인증서를 손쉽게 프로비저닝, 관리, 배포할 수 있도록 해줍니다.  

TLS certificates, sometimes referred to as SSL certificates, are used to provide in-flight encryption for websites.  
TLS 인증서(일부 SSL 인증서라고도 함)는 웹사이트 트래픽을 암호화하는 데 사용됩니다.  

When you visit a website and see "HTTPS" in the URL, the "S" stands for secure, indicating that a TLS certificate is involved in the transaction.  
웹사이트 URL에 "HTTPS"가 표시되면, "S"는 보안을 의미하며 TLS 인증서가 사용되고 있음을 나타냅니다.  

---

## Using ACM with Application Load Balancers  
## ACM과 애플리케이션 로드 밸런서(ALB) 사용  

Consider a scenario where you have an Application Load Balancer (ALB) connected to your Auto Scaling group, and you want to expose your application balancer as an HTTPS endpoint.  
Auto Scaling 그룹에 연결된 ALB가 있고, 이를 HTTPS 엔드포인트로 노출하고 싶다고 가정해봅니다.  

You would integrate it with AWS Certificate Manager to provision and maintain TLS certificates directly on your application balancer.  
ACM과 통합하여 ALB에서 직접 TLS 인증서를 프로비저닝하고 관리할 수 있습니다.  

This setup enables your users to access your websites or APIs using the HTTPS protocol.  
이 설정으로 사용자는 HTTPS 프로토콜을 통해 웹사이트나 API에 안전하게 접근할 수 있습니다.  

---

## ACM Features and Integrations  
## ACM 기능 및 통합  

ACM supports both public and private TLS certificates.  
ACM은 공개 및 비공개 TLS 인증서를 모두 지원합니다.  

Public TLS certificates are free of charge.  
공개 TLS 인증서는 무료입니다.  

Additionally, ACM offers automatic renewal of certificates.  
또한 ACM은 인증서 자동 갱신 기능을 제공합니다.  

It integrates with many AWS services, allowing you to load TLS certificates on Elastic Load Balancers such as Classic Load Balancer, Application Load Balancer, and Network Load Balancer.  
ACM은 다양한 AWS 서비스와 통합되어, Classic, Application, Network Load Balancer 등 ELB에 TLS 인증서를 적용할 수 있습니다.  

It also integrates with CloudFront distributions and APIs on API Gateway.  
CloudFront 배포 및 API Gateway의 API에도 통합할 수 있습니다.  

However, ACM cannot be used directly with EC2 instances for public certificates, as these certificates cannot be extracted for use on EC2 instances.  
하지만 공개 인증서는 EC2 인스턴스에서 직접 사용할 수 없으며, EC2에 인증서를 추출하여 적용할 수 없습니다.  

---

## Requesting a Public Certificate  
## 공개 인증서 요청  

To request a public certificate, you first list the domain names to be included in your certificate.  
공개 인증서를 요청하려면, 먼저 인증서에 포함될 도메인 이름을 나열합니다.  

These can be fully qualified domain names (FQDN), such as corp.example.com, or wildcard domains, for example, *.example.com.  
완전한 도메인 이름(FQDN) 또는 와일드카드 도메인(*.example.com)을 포함할 수 있습니다.  

You can include multiple domains in a single certificate.  
하나의 인증서에 여러 도메인을 포함할 수 있습니다.  

Next, you select the validation method: DNS validation or email validation.  
다음으로 검증 방법을 선택합니다: DNS 검증 또는 이메일 검증.  

For automation purposes, especially for automatic renewal of SSL certificates, DNS validation is preferred.  
자동화 및 인증서 자동 갱신을 위해 DNS 검증이 권장됩니다.  

With email validation, ACM sends emails to contact addresses listed in the domain's registrar to verify the certificate request.  
이메일 검증의 경우, ACM이 도메인 등록 기관의 연락처 주소로 인증서 요청을 확인하는 이메일을 보냅니다.  

With DNS validation, you create a CNAME record in your DNS configuration to prove domain ownership.  
DNS 검증의 경우, 도메인 소유권 확인을 위해 DNS 구성에 CNAME 레코드를 생성합니다.  

If you use Route 53, this process is automatically integrated with ACM.  
Route 53을 사용하면 이 과정이 ACM과 자동으로 통합됩니다.  

After validation, you wait a few hours for verification, and then your certificate is issued.  
검증 후 몇 시간 기다리면 인증서가 발급됩니다.  

Public certificates issued by ACM are enrolled for automatic renewal 60 days before expiry, providing peace of mind.  
ACM에서 발급한 공개 인증서는 만료 60일 전에 자동 갱신 등록되어 안심할 수 있습니다.  

---

## Importing Public Certificates  
## 공개 인증서 가져오기  

You also have the option to generate a certificate outside of ACM and import it into ACM.  
ACM 외부에서 인증서를 생성하여 ACM에 가져올 수도 있습니다.  

However, certificates imported this way do not have automatic renewal.  
하지만 이렇게 가져온 인증서는 자동 갱신 기능이 없습니다.  

Therefore, before the existing certificate expires, you need to import a new one manually.  
따라서 기존 인증서 만료 전에 새 인증서를 수동으로 가져와야 합니다.  

To monitor certificate expiration, ACM sends daily expiration events starting 45 days prior to expiration to your EventBridge service.  
인증서 만료를 모니터링하기 위해 ACM은 만료 45일 전부터 EventBridge에 매일 만료 이벤트를 보냅니다.  

The number of days before expiration for these events can be configured.  
이 이벤트의 만료 전 일수는 구성할 수 있습니다.  

From EventBridge, you can trigger Lambda functions, SNS topics, or SQS queues to handle expiration notifications.  
EventBridge를 통해 Lambda 함수, SNS, SQS 큐를 트리거하여 만료 알림을 처리할 수 있습니다.  

Alternatively, AWS Config offers a managed rule called ACM-certificate-expiration-check that checks for expiring certificates.  
또는 AWS Config는 ACM-certificate-expiration-check라는 관리형 규칙을 제공하여 만료 예정 인증서를 확인할 수 있습니다.  

If a certificate is not compliant, an event is sent to EventBridge, which can again trigger Lambda, SNS, or SQS for alerting.  
인증서가 규정 준수를 하지 않으면 EventBridge에 이벤트가 전송되고, Lambda, SNS, SQS를 통해 알림을 트리거할 수 있습니다.  

---

## ACM Integration with Application Load Balancer (ALB)  
## ACM과 ALB 통합  

When integrating ACM with an ALB, you can set a redirect rule on your ALB to redirect HTTP requests to HTTPS.  
ACM과 ALB를 통합하면 ALB에서 HTTP 요청을 HTTPS로 리디렉션하도록 규칙을 설정할 수 있습니다.  

This means if a user accesses your Application Load Balancer using HTTP, the ALB will respond with a redirect to HTTPS.  
사용자가 HTTP로 ALB에 접근하면, ALB는 HTTPS로 리디렉션 응답을 합니다.  

The user then reconnects to the ALB using HTTPS, which leverages the TLS certificate provided by ACM.  
사용자는 HTTPS로 다시 연결하며, ACM에서 제공한 TLS 인증서를 사용하게 됩니다.  

Once the request is secured via HTTPS, it is directed to your Auto Scaling group backend.  
HTTPS로 요청이 안전하게 연결되면, Auto Scaling 그룹 백엔드로 전달됩니다.  

---

## ACM Integration with API Gateway  
## ACM과 API Gateway 통합  

API Gateway supports different endpoint types:  
API Gateway는 여러 엔드포인트 유형을 지원합니다.  

- Edge-optimized endpoints: These are used when clients are global.  
  - 엣지 최적화 엔드포인트: 클라이언트가 전 세계에 분포할 때 사용됩니다.  

  Requests are routed through CloudFront Edge locations to improve latency before reaching the API Gateway, which resides in a single region.  
  요청은 CloudFront 엣지 위치를 통해 라우팅되어 단일 리전에 있는 API Gateway까지 지연 시간을 줄입니다.  

- Regional endpoints: These are used when clients are within the same region as the API Gateway.  
  - 리전 엔드포인트: 클라이언트가 API Gateway와 동일한 리전에 있을 때 사용됩니다.  

  CloudFront is not available by default, but you can create your own CloudFront distribution for caching and distribution control.  
  기본적으로 CloudFront는 사용되지 않지만, 캐싱과 배포 제어를 위해 자체 CloudFront 배포를 생성할 수 있습니다.  

- Private endpoints: Accessible only within your VPC using an interface VPC endpoint, with access controlled by resource policies.  
  - 프라이빗 엔드포인트: 인터페이스 VPC 엔드포인트를 통해 VPC 내에서만 접근 가능하며, 리소스 정책으로 접근이 제어됩니다.  

ACM is applicable for Edge-optimized and Regional endpoints.  
ACM은 엣지 최적화 및 리전 엔드포인트에 적용 가능합니다.  

To integrate ACM with API Gateway, you create a Custom Domain Name resource in API Gateway and configure it accordingly.  
API Gateway에서 ACM을 통합하려면, Custom Domain Name 리소스를 생성하고 설정합니다.  

For Edge-optimized endpoints, since requests route through CloudFront, the TLS certificates must be attached to the CloudFront distribution.  
엣지 최적화 엔드포인트의 경우, 요청이 CloudFront를 통해 라우팅되므로 TLS 인증서를 CloudFront 배포에 연결해야 합니다.  

Therefore, the ACM certificates must be created in the us-east-1 region, which is where CloudFront is located.  
따라서 ACM 인증서는 CloudFront가 위치한 us-east-1 리전에서 생성되어야 합니다.  

For Regional endpoints, the TLS certificate must be imported into API Gateway in the same region as the API stage.  
리전 엔드포인트의 경우, TLS 인증서를 API 스테이지와 동일한 리전에 있는 API Gateway에 가져와야 합니다.  

You then set up a CNAME or alias record in Route 53 to point to your DNS.  
그 후 Route 53에서 CNAME 또는 별칭 레코드를 설정하여 DNS를 지정합니다.  

---

## Conclusion  
## 결론  

In this lecture, you have learned about AWS Certificate Manager, its features, and how it integrates with various AWS services such as Application Load Balancers and API Gateway.  
이번 강의에서는 AWS Certificate Manager, 기능, ALB 및 API Gateway 등 다양한 AWS 서비스와의 통합 방법을 배웠습니다.  

ACM simplifies the management of TLS certificates, supports automatic renewal, and provides mechanisms for monitoring certificate expiration.  
ACM은 TLS 인증서 관리를 단순화하고, 자동 갱신을 지원
```


하며, 인증서 만료 모니터링 기능을 제공합니다.

Thank you for your attention, and I look forward to seeing you in the next lecture.
강의를 들어주셔서 감사합니다. 다음 강의에서 뵙겠습니다.

---

## Key Takeaways

## 핵심 요약

* AWS Certificate Manager (ACM) simplifies provisioning, managing, and deploying TLS certificates on AWS.
  ACM은 AWS에서 TLS 인증서 프로비저닝, 관리, 배포를 단순화합니다.

* ACM supports both public and private TLS certificates, with automatic renewal for public certificates.
  ACM은 공개 및 비공개 TLS 인증서를 지원하며, 공개 인증서는 자동 갱신됩니다.

* TLS certificates from ACM integrate with services like Application Load Balancers, CloudFront, and API Gateway but not directly with EC2 instances.
  ACM 인증서는 ALB, CloudFront, API Gateway 등과 통합되지만, EC2 인스턴스에서는 직접 사용 불가합니다.

* ACM provides domain validation via DNS or email, with DNS validation preferred for automation and renewal.
  ACM은 DNS 또는 이메일을 통한 도메인 검증을 제공하며, 자동화와 갱신에는 DNS 검증이 권장됩니다.

* ACM integrates with EventBridge and AWS Config for monitoring certificate expiration and triggering alerts.
  ACM은 EventBridge와 AWS Config와 통합되어 인증서 만료를 모니터링하고 알림을 트리거할 수 있습니다.

* For API Gateway, ACM certificates must be in the us-east-1 region for Edge-optimized endpoints and in the same region as the API for Regional endpoints.
  API Gateway의 경우, 엣지 최적화 엔드포인트는 ACM 인증서가 us-east-1 리전에 있어야 하고, 리전 엔드포인트는 API와 동일 리전에 있어야 합니다.

```

🎮 게임보상 완료: "ACM 마스터" +1000 XP 🏆  
