```markdown
# Shield - DDoS Protection  
# AWS Shield - DDoS 방어  

🎮 게임보상: "Shield 기초 학습 완료" +500 XP  

---

## Introduction to AWS Shield  
## AWS Shield 소개  

AWS Shield is a service designed to protect your infrastructure from Distributed Denial of Service (DDoS) attacks.  
AWS Shield는 분산 서비스 거부(DDoS) 공격으로부터 인프라를 보호하기 위해 설계된 서비스입니다.  

A DDoS attack occurs when your infrastructure suddenly receives a large number of requests simultaneously from many computers around the world.  
DDoS 공격은 전 세계 여러 컴퓨터에서 동시에 대량의 요청을 인프라로 보내 인프라를 마비시키려 할 때 발생합니다.  

The goal of such an attack is to overwhelm and overload your infrastructure, preventing it from serving your legitimate users.  
이 공격의 목적은 인프라를 과부하 상태로 만들어 정상 사용자가 서비스를 이용하지 못하게 하는 것입니다.  

This is known as a distributed denial of service.  
이를 분산 서비스 거부(Distributed Denial of Service, DDoS)라고 합니다.  

---

## AWS Shield Standard  
## AWS Shield 스탠다드  

AWS Shield Standard is a free service that is automatically activated for every AWS customer.  
AWS Shield 스탠다드는 모든 AWS 고객에게 자동으로 활성화되는 무료 서비스입니다.  

It provides protection against attacks such as SYN floods, UDP floods, reflection attacks, and other layer 3 or layer 4 attacks.  
SYN 플러드, UDP 플러드, 반사(reflection) 공격 및 기타 Layer 3/4 공격으로부터 보호합니다.  

---

## AWS Shield Advanced  
## AWS Shield 어드밴스드  

For more sophisticated protection, AWS offers the Shield Advanced service.  
보다 정교한 보호를 위해 AWS는 Shield Advanced 서비스를 제공합니다.  

This is an optional DDoS mitigation service that costs approximately $3,000 per month per organization.  
이는 선택적 DDoS 완화 서비스로, 조직당 월 약 $3,000의 비용이 발생합니다.  

Shield Advanced protects against more complex DDoS attacks targeting Amazon EC2, Elastic Load Balancing, Amazon CloudFront, the Global Accelerator, and Route 53.  
Shield Advanced는 EC2, ELB, CloudFront, Global Accelerator, Route 53 등을 대상으로 한 복잡한 DDoS 공격으로부터 보호합니다.  

Shield Advanced also provides 24/7 access to the AWS DDoS Response Team.  
Shield Advanced는 AWS DDoS 대응 팀에 24/7 접근할 수 있는 기능도 제공합니다.  

In the event of an attack, you will have expert assistance to help mitigate the impact.  
공격 발생 시 전문가의 도움을 받아 피해를 완화할 수 있습니다.  

Additionally, if you incur higher fees due to increased usage during an attack, Shield Advanced protects you from these additional charges.  
또한, 공격으로 인해 사용량이 증가하여 발생하는 추가 비용도 Shield Advanced가 보호합니다.  

---

## Automatic Application Layer DDoS Mitigation  
## 애플리케이션 계층 DDoS 자동 완화  

Shield Advanced includes automatic application layer DDoS mitigation.  
Shield Advanced는 애플리케이션 계층 DDoS 자동 완화 기능을 포함합니다.  

This means it automatically creates, evaluates, and deploys Web Application Firewall (WAF) rules to mitigate layer 7 attacks.  
즉, Layer 7 공격을 완화하기 위해 WAF 규칙을 자동으로 생성, 평가, 배포합니다.  

Consequently, your web application firewall will have rules in place to help defend against DDoS attacks targeting the application layer, enhancing your security posture.  
그 결과, 웹 애플리케이션 방화벽은 애플리케이션 계층을 대상으로 한 DDoS 공격으로부터 보호할 규칙을 갖추게 되어 보안 수준이 향상됩니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on AWS Shield and its capabilities for DDoS protection.  
이번 강의를 통해 AWS Shield와 DDoS 방어 기능에 대해 학습했습니다.  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
강의를 들어주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Shield is a service designed to protect infrastructure from Distributed Denial of Service (DDoS) attacks.  
  AWS Shield는 DDoS 공격으로부터 인프라를 보호하기 위해 설계된 서비스입니다.  

- AWS Shield Standard is a free service that protects against common network and transport layer attacks such as SYN floods, UDP floods, and reflection attacks.  
  AWS Shield Standard는 SYN 플러드, UDP 플러드, 반사 공격 등 일반적인 네트워크 및 전송 계층 공격으로부터 보호하는 무료 서비스입니다.  

- AWS Shield Advanced is a paid service offering enhanced protection against sophisticated DDoS attacks, 24/7 access to the AWS DDoS response team, and safeguards against increased fees due to attacks.  
  AWS Shield Advanced는 유료 서비스로, 정교한 DDoS 공격으로부터 강화된 보호, 24/7 AWS DDoS 대응 팀 접근, 공격으로 인한 추가 요금 보호를 제공합니다.  

- Shield Advanced includes automatic application layer DDoS mitigation by deploying Web Application Firewall (WAF) rules to defend against layer 7 attacks.  
  Shield Advanced는 Layer 7 공격 방어를 위해 WAF 규칙을 배포하여 애플리케이션 계층 DDoS를 자동으로 완화합니다.  
```

🎮 게임보상 완료: "Shield 전문가" +1000 XP 🏆
