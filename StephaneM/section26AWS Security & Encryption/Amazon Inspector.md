```markdown
# Amazon Inspector  
# 아마존 인스펙터  

🎮 게임보상: "Security Auditor" +500 XP  

---

## Introduction to Amazon Inspector  
## 아마존 인스펙터 소개  

Amazon Inspector is a service that enables you to run automated security assessments on several resources.  
Amazon Inspector는 여러 리소스에 대해 자동화된 보안 평가를 수행할 수 있는 서비스입니다.  

---

## Security Assessment on EC2 Instances  
## EC2 인스턴스에 대한 보안 평가  

Amazon Inspector leverages the Systems Manager agent installed on your EC2 instances to assess their security continuously.  
Amazon Inspector는 EC2 인스턴스에 설치된 Systems Manager 에이전트를 활용하여 지속적으로 보안을 평가합니다.  

It analyzes the instances for unintended network accessibility and examines the running operating system for known vulnerabilities.  
인스턴스가 의도치 않게 외부에 노출되어 있는지 분석하고, 실행 중인 운영체제에서 알려진 취약점을 검사합니다.  

---

## Security Assessment on Container Images  
## 컨테이너 이미지에 대한 보안 평가  

Amazon Inspector also evaluates container images, such as Docker images, that are pushed to Amazon Elastic Container Registry (ECR).  
Amazon Inspector는 Amazon Elastic Container Registry(ECR)에 푸시된 Docker 이미지와 같은 컨테이너 이미지도 평가합니다.  

As these container images are pushed, Amazon Inspector analyzes them against known vulnerabilities.  
컨테이너 이미지가 푸시될 때, Amazon Inspector는 알려진 취약점에 대해 이미지를 분석합니다.  

---

## Security Assessment on Lambda Functions  
## Lambda 함수에 대한 보안 평가  

Lambda functions are assessed by Amazon Inspector upon deployment.  
Lambda 함수는 배포 시 Amazon Inspector에 의해 평가됩니다.  

The service analyzes the function code and its package dependencies for software vulnerabilities during this process.  
이 과정에서 함수 코드와 패키지 종속성에 대한 소프트웨어 취약점을 분석합니다.  

---

## Reporting and Integration  
## 보고 및 통합  

Once Amazon Inspector completes its assessments, it reports findings to AWS Security Hub.  
Amazon Inspector가 평가를 완료하면 결과를 AWS Security Hub로 보고합니다.  

Additionally, it sends findings and related events to Amazon EventBridge.  
추가로, 탐지 결과와 관련 이벤트를 Amazon EventBridge로 전송합니다.  

This integration provides a centralized view of vulnerabilities across your infrastructure and enables automation based on these findings.  
이 통합은 인프라 전체의 취약점을 중앙에서 볼 수 있게 하며, 결과를 기반으로 자동화된 대응이 가능하게 합니다.  

---

## What Does Amazon Inspector Evaluate?  
## Amazon Inspector가 평가하는 항목  

Amazon Inspector focuses on the following resources:  
Amazon Inspector는 다음 리소스에 초점을 맞춥니다:  

- Running EC2 instances  
- 실행 중인 EC2 인스턴스  

- Container images stored in Amazon ECR  
- Amazon ECR에 저장된 컨테이너 이미지  

- Lambda functions  
- Lambda 함수  

It performs continuous scanning of the infrastructure as needed.  
필요에 따라 인프라를 지속적으로 스캔합니다.  

---

## Vulnerability Database and Network Reachability  
## 취약점 데이터베이스와 네트워크 접근성  

The service references a database of vulnerabilities, specifically the Common Vulnerabilities and Exposures (CVE) database, to identify package vulnerabilities across EC2, ECR, and Lambda.  
이 서비스는 취약점 데이터베이스, 특히 CVE(Common Vulnerabilities and Exposures) 데이터베이스를 참조하여 EC2, ECR, Lambda의 패키지 취약점을 식별합니다.  

It also assesses network reachability on Amazon EC2 instances.  
또한 Amazon EC2 인스턴스의 네트워크 접근성도 평가합니다.  

---

## Continuous Updates and Risk Scoring  
## 지속적 업데이트 및 위험 점수  

Whenever the CVE database is updated, Amazon Inspector automatically reruns assessments to ensure your infrastructure is tested against the latest vulnerabilities.  
CVE 데이터베이스가 업데이트될 때마다 Amazon Inspector는 자동으로 평가를 다시 실행하여 최신 취약점에 대해 인프라가 테스트되도록 합니다.  

Each run associates a risk score with identified vulnerabilities to assist in prioritization.  
각 평가 실행 시 식별된 취약점에 위험 점수가 부여되어 우선순위 결정을 지원합니다.  

---

## Conclusion  
## 결론  

Amazon Inspector is a comprehensive security assessment tool that continuously evaluates your EC2 instances, container images, and Lambda functions for vulnerabilities, integrates with AWS Security Hub and EventBridge for centralized management and automation, and helps prioritize risks through scoring.  
Amazon Inspector는 EC2 인스턴스, 컨테이너 이미지, Lambda 함수를 지속적으로 평가하는 종합 보안 평가 도구이며, AWS Security Hub 및 EventBridge와 통합되어 중앙 관리와 자동화를 제공하고, 위험 점수를 통해 취약점 우선순위 결정을 돕습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon Inspector provides automated security assessments for EC2 instances, container images in Amazon ECR, and Lambda functions.  
- Amazon Inspector는 EC2 인스턴스, Amazon ECR의 컨테이너 이미지, Lambda 함수에 대한 자동화된 보안 평가를 제공합니다.  

- It continuously analyzes EC2 instances using the Systems Manager agent for unintended network accessibility and known operating system vulnerabilities.  
- Systems Manager 에이전트를 사용하여 EC2 인스턴스를 지속적으로 분석하며, 의도치 않은 네트워크 접근성과 알려진 운영체제 취약점을 확인합니다.  

- Container images pushed to Amazon ECR are scanned for known vulnerabilities during the push process.  
- Amazon ECR에 푸시된 컨테이너 이미지는 푸시 과정에서 알려진 취약점에 대해 스캔됩니다.  

- Lambda functions are assessed for software vulnerabilities in the function code and package dependencies upon deployment.  
- Lambda 함수는 배포 시 함수 코드와 패키지 종속성의 소프트웨어 취약점에 대해 평가됩니다.  

- Findings from Amazon Inspector can be sent to AWS Security Hub and Amazon EventBridge for centralized visibility and automation.  
- Amazon Inspector의 탐지 결과는 AWS Security Hub 및 Amazon EventBridge로 전송되어 중앙에서 가시화하고 자동화할 수 있습니다.  

- Amazon Inspector evaluates vulnerabilities based on a continuously updated CVE database and performs rescans when updates occur, assigning risk scores to prioritize vulnerabilities.  
- Amazon Inspector는 지속적으로 업데이트되는 CVE 데이터베이스를 기반으로 취약점을 평가하며, 업데이트 시 재평가를 수행하고 위험 점수를 부여하여 취약점 우선순위를 지정합니다.  
```

🎮 게임보상 완료: "Vulnerability Hunter" +1000 XP 🏆
