```markdown
# CloudTrail vs CloudWatch vs Config  
# CloudTrail vs CloudWatch vs Config  

## Introduction to CloudWatch, CloudTrail, and Config  
## CloudWatch, CloudTrail, Config 소개  
One very popular exam question is to distinguish between CloudWatch, CloudTrail, and Config.  
시험에서 자주 나오는 질문 중 하나는 CloudWatch, CloudTrail, Config의 차이를 구분하는 것입니다.  
(시험 대비)  

Thanks to hands-on experience, you should know exactly what the differences are.  
실습 경험 덕분에 차이점을 정확히 이해할 수 있어야 합니다.  
(실습 중요)  

While it may seem obvious, it is beneficial to review examples to clarify their distinct purposes.  
명백해 보여도, 예제를 통해 각 서비스의 목적을 명확히 이해하는 것이 도움이 됩니다.  
(예제 학습)  

---

## CloudWatch Overview  
## CloudWatch 개요  
CloudWatch is designed for performance metrics such as CPU usage and network activity.  
CloudWatch는 CPU 사용률, 네트워크 활동 등 성능 지표를 모니터링하도록 설계되었습니다.  
(성능 모니터링)  

It allows you to create dashboards to visualize these metrics.  
대시보드를 만들어 지표를 시각화할 수 있습니다.  
(대시보드 생성)  

Additionally, CloudWatch supports events and alerts, and it provides log aggregation and analysis capabilities.  
또한 이벤트와 알림을 지원하며, 로그 집계 및 분석 기능을 제공합니다.  
(이벤트/로그 분석)  

---

## CloudTrail Overview  
## CloudTrail 개요  
CloudTrail records API calls made within your AWS account by all users and services.  
CloudTrail은 모든 사용자와 서비스가 AWS 계정에서 수행한 API 호출을 기록합니다.  
(API 감사)  

You can define specific trails for particular resources, such as EC2 instances, to obtain more focused information.  
특정 리소스(예: EC2 인스턴스)에 대해 특정 트레일을 정의하여 더 세밀한 정보를 얻을 수 있습니다.  
(세부 트레일 설정)  

CloudTrail operates as a global service.  
CloudTrail은 글로벌 서비스로 작동합니다.  
(글로벌 적용)  

---

## Config Overview  
## Config 개요  
Config records configuration changes and evaluates resource configurations against compliance rules.  
Config는 구성 변경을 기록하고, 리소스 구성을 규정 준수 규칙에 따라 평가합니다.  
(구성 기록 및 준수 평가)  

It provides a timeline of changes and compliance status through a user-friendly interface.  
사용자 친화적 인터페이스를 통해 변경 타임라인과 준수 상태를 제공합니다.  
(타임라인/준수 확인)  

---

## Applying These Services to an Elastic Load Balancer (ELB)  
## Elastic Load Balancer(ELB)에 서비스 적용  
Let's examine how each of these services can help you understand what is happening with your ELB.  
각 서비스가 ELB에서 발생하는 상황을 이해하는 데 어떻게 도움이 되는지 살펴봅시다.  
(ELB 적용 예제)  

---

### CloudWatch for ELB  
### ELB용 CloudWatch  
CloudWatch can monitor the number of incoming connections and visualize the percentage of error codes over time.  
CloudWatch는 들어오는 연결 수를 모니터링하고, 시간에 따른 오류 코드 비율을 시각화할 수 있습니다.  
(성능 모니터링)  

You can create dashboards to assess the load balancer's performance, including global dashboards if you have multiple load balancers supporting a global application.  
여러 LB를 사용하는 글로벌 애플리케이션이라면, 글로벌 대시보드를 포함하여 성능 평가용 대시보드를 생성할 수 있습니다.  
(대시보드 활용)  

---

### Config for ELB  
### ELB용 Config  
Config can track security group rules for the load balancer to ensure no unauthorized changes occur.  
Config는 로드 밸런서의 보안 그룹 규칙을 추적하여 무단 변경을 방지합니다.  
(보안 규칙 모니터링)  

It also monitors configuration changes to the load balancer itself, such as modifications to the SSL certificate.  
또한 SSL 인증서 변경 등 로드 밸런서 구성 변경도 모니터링합니다.  
(구성 변경 모니터링)  

Compliance rules can enforce requirements like always having an SSL certificate assigned and disallowing non-encrypted traffic.  
준수 규칙으로 항상 SSL 인증서 할당 및 비암호화 트래픽 차단을 강제할 수 있습니다.  
(규칙 강제 적용)  

---

### CloudTrail for ELB  
### ELB용 CloudTrail  
CloudTrail tracks who made any changes to the load balancer through API calls.  
CloudTrail은 API 호출을 통해 로드 밸런서에 변경을 가한 사용자를 추적합니다.  
(변경자 기록)  

For example, if someone changes security group rules or modifies or removes the SSL certificate, CloudTrail records the identity of the individual responsible.  
예: 누군가 보안 그룹 규칙을 변경하거나 SSL 인증서를 수정/삭제하면, CloudTrail이 책임자를 기록합니다.  
(책임 추적)  

---

## Summary  
## 요약  
These tools are complementary. Understanding how they are used with a load balancer provides a clear example of their distinct roles.  
이 도구들은 상호 보완적입니다. 로드 밸런서 적용 사례를 통해 각 도구의 역할 차이를 명확히 이해할 수 있습니다.  
(상호 보완 이해)  

This knowledge will help you confidently answer related exam questions.  
이 지식은 관련 시험 질문에 자신 있게 답하는 데 도움이 됩니다.  
(시험 대비)  

---

## Key Takeaways  
## 핵심 요약  
- CloudWatch monitors performance metrics, creates dashboards, and aggregates logs.  
- CloudWatch는 성능 지표를 모니터링하고, 대시보드를 생성하며, 로그를 집계합니다.  

- CloudTrail records API calls globally within an AWS account for auditing.  
- CloudTrail은 AWS 계정 내 API 호출을 글로벌 단위로 기록하여 감사를 지원합니다.  

- Config tracks configuration changes and evaluates compliance against rules.  
- Config는 구성 변경을 추적하고 규칙 준수를 평가합니다.  

- These services complement each other to provide comprehensive monitoring and auditing for AWS resources like Elastic Load Balancers.  
- 이 서비스들은 상호 보완적으로 작용하여 ELB와 같은 AWS 리소스에 대한 종합적인 모니터링과 감사를 제공합니다.  
```

게임보상: 🏆 Cloud 서비스 구분 마스터! 이제 CloudWatch, CloudTrail, Config의 역할과 ELB 적용 예제를 완벽히 이해했습니다. ⚡📊
