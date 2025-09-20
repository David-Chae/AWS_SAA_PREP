```markdown
# CloudFormation Intro  
# CloudFormation 소개  
👉 이 섹션에서는 AWS 인프라를 코드로 정의하고 관리하는 CloudFormation을 다룸.  

---

## Introduction to CloudFormation  
## CloudFormation 소개  

**Welcome to this section on Deploying and Managing Infrastructure at Scale.**  
대규모 인프라 배포 및 관리 섹션에 오신 것을 환영합니다.  
👉 대규모 클라우드 운영을 위한 핵심 도구 학습 시작.  

**In this section, we will explore different ways to deploy your workloads onto AWS.**  
이 섹션에서는 워크로드를 AWS에 배포하는 다양한 방법을 살펴봅니다.  
👉 여러 배포 방식 중 CloudFormation에 집중.  

**The first technology we will discuss is CloudFormation.**  
우리가 처음 다룰 기술은 CloudFormation입니다.  
👉 AWS 인프라 관리의 출발점.  

---

## What is CloudFormation?  
## CloudFormation이란 무엇인가?  

**CloudFormation is a crucial AWS technology because it provides a declarative way of outlining your AWS infrastructure for any resources, most of which are supported.**  
CloudFormation은 AWS 인프라를 선언형 방식으로 정의할 수 있는 핵심 기술이며, 대부분의 리소스를 지원합니다.  
👉 사람이 직접 순서를 고민할 필요 없음.  

**For example, in CloudFormation, you specify that you want a security group, two EC2 instances using that security group, an S3 bucket, and a load balancer in front of all these machines.**  
예를 들어, 보안 그룹, 그 보안 그룹을 사용하는 두 개의 EC2 인스턴스, S3 버킷, 그리고 그 앞의 로드 밸런서를 지정할 수 있습니다.  
👉 인프라 구성 요소를 템플릿으로 한 번에 정의 가능.  

**CloudFormation then automatically creates all these resources for you in the correct order with the exact configuration you specify.**  
CloudFormation은 지정된 순서와 설정대로 자동으로 모든 리소스를 생성합니다.  
👉 자동화된 인프라 배포의 강력함.  

---

## Benefits of Using CloudFormation  
## CloudFormation 사용 장점  

**Infrastructure as Code: All your infrastructure is defined as code. This means you will never create resources manually, which is excellent for control.**  
인프라를 코드로 관리: 모든 인프라가 코드로 정의되므로 수동으로 리소스를 생성할 필요가 없으며, 관리가 탁월해집니다.  
🎖 보상 획득: "코드 기반 관리력 +50 EXP"  

**Code Review: Any changes to your AWS cloud must be reviewed through code review, which is a great operational practice.**  
코드 리뷰: AWS 클라우드 변경 사항은 반드시 코드 리뷰를 통해 검토되어야 하며, 이는 뛰어난 운영 방식입니다.  
🎖 보상 획득: "운영 안정성 +40 EXP"  

**Cost Advantage: Each resource within a stack receives a tag similar to other resources in the stack, allowing easy cost estimation using CloudFormation templates.**  
비용 장점: 스택의 각 리소스는 태그를 받아 비용 추정이 용이합니다.  
🎖 보상 획득: "비용 최적화 +30 EXP"  

**Saving Strategy: You can automate deletion and recreation of resources at specific times to save costs. For example, deleting all resources at 5:00 PM and recreating them at 8:00 or 9:00 AM safely, ensuring no resources exist during off-hours.**  
절약 전략: 특정 시간에 리소스를 삭제하고 다시 생성하여 비용을 절감할 수 있습니다. 예: 오후 5시에 삭제 후 오전 8~9시에 재생성.  
🎖 보상 획득: "비용 절감 전략 +70 EXP"  

---

## Why CloudFormation is Powerful  
## CloudFormation의 강력한 이유  

**With CloudFormation, it is super easy to create and delete resources, which aligns with one of the biggest cloud principles.**  
CloudFormation으로 리소스를 쉽게 생성/삭제할 수 있으며, 이는 클라우드의 핵심 원칙과 부합합니다.  
👉 빠른 실험과 복구 가능.  

**Additionally, CloudFormation generates diagrams for your templates, which we will see shortly.**  
또한 CloudFormation은 템플릿에 대한 다이어그램을 생성합니다.  
👉 아키텍처 시각화 지원.  

**CloudFormation uses declarative programming, so you do not need to figure out the order of resource creation, such as whether to create a DynamoDB table or an EC2 instance first.**  
CloudFormation은 선언형 프로그래밍을 사용하므로, DynamoDB를 먼저 만들지 EC2를 먼저 만들지 고민할 필요가 없습니다.  
👉 순서 자동 처리.  

**The CloudFormation template is intelligent enough to determine the correct sequence.**  
CloudFormation 템플릿은 올바른 순서를 스스로 판단합니다.  
👉 자동 지능형 배포.  

---

## Leveraging Existing Templates and Resources  
## 기존 템플릿과 리소스 활용  

**With CloudFormation, you do not reinvent the wheel.**  
CloudFormation을 사용하면 바퀴를 다시 발명할 필요가 없습니다.  
👉 이미 검증된 템플릿 재활용 가능.  

**You can leverage existing templates available on the web and extensive documentation.**  
웹과 문서에서 제공되는 기존 템플릿을 활용할 수 있습니다.  
👉 빠른 시작 가능.  

**CloudFormation supports almost all AWS resources, meaning everything covered in this course is supported.**  
CloudFormation은 거의 모든 AWS 리소스를 지원하므로, 이 과정에서 다루는 모든 내용이 포함됩니다.  
👉 광범위한 지원.  

**In cases where a resource is not supported, you can use a custom resource.**  
지원되지 않는 리소스는 커스텀 리소스를 통해 구현할 수 있습니다.  
👉 확장성 보장.  

**CloudFormation is truly the foundation of infrastructure as code on AWS.**  
CloudFormation은 AWS에서 인프라를 코드로 관리하는 기반입니다.  
👉 핵심 기술임.  

---

## Visualizing CloudFormation Templates  
## CloudFormation 템플릿 시각화  

**You can visualize a CloudFormation template using the Infrastructure Composer service.**  
Infrastructure Composer 서비스를 사용하여 CloudFormation 템플릿을 시각화할 수 있습니다.  
👉 그림으로 아키텍처 확인.  

**For example, visualizing a WordPress CloudFormation stack shows all the resources of the template, such as the ALB Listener, database security group, SQL database, various security groups, launch configuration, application balancers, and more.**  
예를 들어 WordPress CloudFormation 스택을 시각화하면 ALB Listener, DB 보안 그룹, SQL DB, 여러 보안 그룹, 런치 구성, 애플리케이션 로드 밸런서 등이 보입니다.  
👉 실제 아키텍처 구조를 한눈에 파악.  

**Moreover, you can see the relationships between these components and how they are linked together, which is very helpful for understanding your architecture diagrams.**  
또한 컴포넌트 간 관계와 연결 방식을 확인할 수 있어 아키텍처 다이어그램 이해에 큰 도움이 됩니다.  
👉 시스템 구조 파악에 유리.  

---

## CloudFormation in Practice and Exam Perspective  
## 실습과 시험 관점에서의 CloudFormation  

**From an exam perspective, CloudFormation is used when infrastructure as code is required, especially when you need to repeat an architecture in different environments, regions, or AWS accounts.**  
시험 관점에서 CloudFormation은 인프라를 코드로 반복 정의할 때 사용됩니다. 특히 여러 환경, 리전, AWS 계정에서 같은 아키텍처를 반복할 때 필요합니다.  
👉 시험에 반드시 나오는 핵심 주제.  

**That concludes this lecture. In the next lecture, we will have a short practice session on CloudFormation.**  
이것으로 강의를 마칩니다. 다음 강의에서는 CloudFormation 실습을 진행합니다.  
👉 이론 → 실습 단계로 진행.  

---

# Key Takeaways  
# 핵심 요약  
👉 요약 및 보상 지급 🎁✨  

**CloudFormation provides a declarative way to define and deploy AWS infrastructure as code.**  
CloudFormation은 선언형 방식으로 AWS 인프라를 코드로 정의하고 배포합니다.  
🎖 보상 획득: "선언형 이해력 +60 EXP"  

**It automates resource creation in the correct order with specified configurations.**  
정확한 순서와 설정에 따라 리소스를 자동으로 생성합니다.  
🎖 보상 획득: "자동화 마스터리 +70 EXP"  

**Infrastructure as code enables code review, cost estimation, and automated resource management.**  
코드 기반 인프라는 코드 리뷰, 비용 추정, 자동화된 리소스 관리를 가능하게 합니다.  
🎖 보상 획득: "운영 효율성 +80 EXP"  

**CloudFormation supports almost all AWS resources and allows visualization of infrastructure relationships.**  
CloudFormation은 거의 모든 AWS 리소스를 지원하며, 인프라 관계를 시각화할 수 있습니다.  
🎖 보상 획득: "아키텍처 시각화 +90 EXP"  

---

🔥 최종 게임 보상: `+500 EXP`  
레벨 업까지 `500 EXP` 남았습니다. 🕹️  
```
