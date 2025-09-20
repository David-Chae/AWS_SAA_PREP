
```markdown
# CloudFormation - Hands On  
# CloudFormation 실습  
👉 이번 강의에서는 CloudFormation을 직접 다루며, 동작 원리를 이해할 수 있도록 개요와 실습 과정을 안내함.  

---

## Introduction  
## 소개  

**In this lecture, we will provide a quick introduction to CloudFormation and give an overview that allows you to understand how it works.**  
이번 강의에서는 CloudFormation을 간단히 소개하고, 동작 방식을 이해할 수 있도록 개요를 제공합니다.  
👉 이론과 실습을 통해 빠르게 개념 잡기.  

---

## Preparing to Create a CloudFormation Stack  
## CloudFormation 스택 생성 준비  

**First, ensure that you are in the US East (Northern Virginia) region, also known as US East 1.**  
먼저, 미국 동부(버지니아 북부) 리전(US East 1)에 있는지 확인하세요.  
👉 템플릿이 특정 리전에서만 동작함.  

**This is important because the template provided only works in this region. We will then proceed to create a stack.**  
제공된 템플릿은 이 리전에서만 동작하므로 중요합니다. 이제 스택 생성을 진행합니다.  
👉 리전 불일치 시 오류 발생 가능.  

🎖 보상 획득: "환경 설정 정확성 +50 EXP"  

---

## Selecting and Uploading a Template  
## 템플릿 선택 및 업로드  

**When creating a stack, you have multiple options for templates:**  
스택을 생성할 때 템플릿을 선택할 수 있는 여러 옵션이 있습니다:  
👉 다양한 시작 방법 제공.  

**Choose an existing template.**  
기존 템플릿 선택.  
**Use a sample template provided by AWS.**  
AWS에서 제공하는 샘플 템플릿 사용.  
**Build from Application Composer.**  
Application Composer에서 직접 빌드.  
👉 초보자는 샘플, 숙련자는 직접 작성 가능.  

**For this hands-on, we will choose an existing template by uploading a template file.**  
이번 실습에서는 템플릿 파일을 업로드하여 기존 템플릿을 사용합니다.  
👉 실습 진행 방식 확정.  

🎖 보상 획득: "템플릿 활용력 +60 EXP"  

---

## Template Example: 0-just-EC2.yaml  
## 템플릿 예시: 0-just-EC2.yaml  

**The template file named 0-just-EC2.yaml is a simple YAML file that defines a resource block to create an EC2 instance called MyInstance.**  
`0-just-EC2.yaml` 파일은 MyInstance라는 EC2 인스턴스를 생성하는 리소스 블록을 정의한 간단한 YAML 파일입니다.  
👉 최소 단위 예제.  

**The resource type is AWS::EC2::Instance.**  
리소스 타입은 `AWS::EC2::Instance` 입니다.  
👉 EC2 생성을 위한 표준 타입.  

**Key properties include:**  
핵심 속성은 다음과 같습니다:  
- **Availability Zone: us-east-1a** (따라서 반드시 US East 1 리전에 있어야 함).  
- **Image ID: 특정 AMI ID** (US East 1 리전에서만 유효).  
- **Instance Type: t2.micro.**  
👉 실습용 기본 구성.  

**This YAML file defines how to launch an EC2 instance through CloudFormation.**  
이 YAML 파일은 CloudFormation을 통해 EC2 인스턴스를 실행하는 방법을 정의합니다.  
👉 인프라 코드 시작점.  

🎖 보상 획득: "YAML 이해력 +70 EXP"  

---

## Uploading and Visualizing the Template  
## 템플릿 업로드 및 시각화  

**After selecting the template file, you can view it in Application Composer, which provides a visual understanding of your templates.**  
템플릿 파일을 선택한 후 Application Composer에서 시각적으로 확인할 수 있습니다.  
👉 시각화를 통한 직관적 이해.  

**The canvas shows the EC2 instance resource, and you can switch between YAML and JSON views.**  
캔버스에는 EC2 인스턴스 리소스가 표시되며 YAML/JSON 뷰 전환이 가능합니다.  
👉 다양한 포맷 학습 가능.  

**Application Composer is a helpful tool for visual feedback on your CloudFormation templates.**  
Application Composer는 CloudFormation 템플릿에 대한 시각적 피드백을 제공하는 유용한 도구입니다.  
👉 복잡한 아키텍처 파악에 도움.  

🎖 보상 획득: "시각화 스킬 +40 EXP"  

---

## Creating the Stack  
## 스택 생성  

**Next, provide a stack name, for example, demo-CloudFormation.**  
다음으로 스택 이름을 입력합니다. 예: `demo-CloudFormation`.  
👉 이름 규칙 중요.  

**Since the template does not define any parameters, no parameter input is required at this stage.**  
템플릿에 파라미터 정의가 없으므로 입력할 필요가 없습니다.  
👉 기본 실습이라 간단함.  

**You can add tags, such as CFDemo, to demonstrate tagging in CloudFormation.**  
CFDemo 같은 태그를 추가하여 태깅을 보여줄 수 있습니다.  
👉 태그 관리로 비용 추적 용이.  

**Leave permissions and other options as default, then review and create the stack.**  
권한과 다른 옵션은 기본값으로 두고 검토 후 스택을 생성합니다.  
👉 실습 효율 극대화.  

🎖 보상 획득: "스택 생성 능력 +80 EXP"  

---

## Stack Creation and Resource Verification  
## 스택 생성 및 리소스 확인  

**Once submitted, CloudFormation generates events quickly and creates the EC2 instance resource.**  
제출하면 CloudFormation이 빠르게 이벤트를 생성하고 EC2 인스턴스를 만듭니다.  
👉 자동화의 힘.  

**You can verify in the EC2 console that the instance named MyInstance is running, is of type t2.micro, and uses the specified AMI ID from the template.**  
EC2 콘솔에서 MyInstance가 실행 중인지, t2.micro 타입인지, 지정된 AMI ID를 사용하는지 확인할 수 있습니다.  
👉 검증 과정 필수.  

**Additionally, tags applied by CloudFormation include the stack name, logical ID, stack ID, and any user-specified tags such as CFDemo.**  
CloudFormation이 적용한 태그에는 스택 이름, 논리 ID, 스택 ID, 사용자 정의 태그 등이 포함됩니다.  
👉 태그로 추적 및 관리 가능.  

🎖 보상 획득: "리소스 검증력 +90 EXP"  

---

## Updating the Stack with a More Complete Template  
## 더 완전한 템플릿으로 스택 업데이트  

**To update the stack, choose to replace the existing template with a new file named 1-ec2-with-sg-eip.yaml.**  
스택을 업데이트하려면 기존 템플릿을 `1-ec2-with-sg-eip.yaml` 파일로 교체합니다.  
👉 점진적 확장 가능.  

**This template includes:**  
이 템플릿에는 다음이 포함됩니다:  
- 보안 그룹 설명을 위한 파라미터 섹션.  
- 두 개의 보안 그룹이 있는 EC2 인스턴스.  
- 인스턴스에 연결된 Elastic IP.  
- SSH(22번 포트) 및 HTTP(80번 포트) 규칙.  
👉 실제 서비스 운영에 가까운 설정.  

🎖 보상 획득: "고급 템플릿 활용 +100 EXP"  

---

## Applying the Update  
## 업데이트 적용  

**When applying the update, you will be prompted to enter the security group description parameter, for example, demo description.**  
업데이트 시 보안 그룹 설명 파라미터를 입력해야 합니다. 예: demo description.  
👉 사용자 입력으로 유연성 확보.  

**CloudFormation then generates a change set, previewing the changes:**  
CloudFormation은 변경 세트를 생성하여 변경 사항을 미리 보여줍니다:  
- Elastic IP 추가.  
- SSH 및 서버 보안 그룹 추가.  
- EC2 인스턴스 교체(구 인스턴스 삭제 후 새 인스턴스 생성).  
👉 변경 전 영향도 파악 가능.  

🎖 보상 획득: "변경 관리 능력 +120 EXP"  

---

## CloudFormation's Intelligent Resource Management  
## CloudFormation의 지능형 리소스 관리  

**CloudFormation manages resource creation and updates intelligently.**  
CloudFormation은 리소스 생성과 업데이트를 지능적으로 관리합니다.  
👉 사람 대신 순서 자동 처리.  

**It creates the new security groups first, then updates the EC2 instance by replacing it.**  
먼저 보안 그룹을 생성한 후, EC2 인스턴스를 교체합니다.  
👉 의존성 처리 자동화.  

**During this process, two EC2 instances may be visible temporarily: the old one and the new one being created.**  
이 과정에서 일시적으로 두 개의 EC2 인스턴스(기존/새로운)가 보일 수 있습니다.  
👉 업데이트 과정 이해 필요.  

**Once the update completes, the Elastic IP is created and attached to the new EC2 instance automatically.**  
업데이트가 완료되면 Elastic IP가 생성되어 새 EC2 인스턴스에 자동 연결됩니다.  
👉 자동화의 편리함.  

🎖 보상 획득: "지능형 자동화 이해력 +130 EXP"  

---

## Verifying Resources and Cleanup  
## 리소스 검증 및 정리  

**You can verify the Elastic IP is properly created, tagged, and attached to the EC2 instance by checking the networking details in the EC2 console.**  
EC2 콘솔 네트워킹에서 Elastic IP가 생성/태깅/연결되었는지 확인할 수 있습니다.  
👉 리소스 정상 작동 확인.  

**CloudFormation also handles cleanup by terminating the old EC2 instance after the update completes.**  
CloudFormation은 업데이트 후 기존 EC2 인스턴스를 자동으로 종료하여 정리합니다.  
👉 불필요한 리소스 제거.  

**The resources tab in CloudFormation shows all resources created through the stack.**  
CloudFormation의 리소스 탭에서 스택을 통해 생성된 모든 리소스를 확인할 수 있습니다.  
👉 전체 리소스 추적 가능.  

**Viewing the updated template in Application Composer provides a visual representation of the new architecture, including the EC2 instance, Elastic IP, and security groups.**  
Application Composer에서 업데이트된 템플릿을 확인하면 EC2 인스턴스, Elastic IP, 보안 그룹이 포함된 새로운 아키텍처를 시각적으로 볼 수 있습니다.  
👉 아키텍처 다이어그램 이해에 도움.  

🎖 보상 획득: "클린업 마스터리 +140 EXP"  

---

## Best Practices for Managing CloudFormation Stacks  
## CloudFormation 스택 관리 모범 사례  

**It is not recommended to manually delete or modify resources created by CloudFormation, such as EC2 instances or Elastic IPs.**  
CloudFormation이 만든 리소스(EC2, Elastic IP 등)는 수동으로 삭제/수정하지 않는 것이 좋습니다.  
👉 스택 무결성 유지 필수.  

**Instead, manage changes by updating the templates or deleting the entire stack through CloudFormation.**  
변경은 템플릿 업데이트 또는 스택 전체 삭제를 통해 관리해야 합니다.  
👉 올바른 변경 관리 방법.  

**This ensures resources are created and deleted in the correct order, maintaining stack integrity.**  
이렇게 해야 리소스가 올바른 순서로 생성/삭제되어 스택 무결성이 유지됩니다.  
👉 인프라 안정성 보장.  

🎖 보상 획득: "운영 모범 사례 +150 EXP"  

---

## Conclusion  
## 결론  

**CloudFormation is a powerful declarative service for managing infrastructure as code.**  
CloudFormation은 인프라를 코드로 관리할 수 있는 강력한 선언형 서비스입니다.  
👉 AWS 관리 핵심 도구.  

**By specifying what you want in templates, CloudFormation figures out how to create, update, and delete resources accordingly.**  
템플릿에 원하는 것을 정의하면 CloudFormation이 생성/업데이트/삭제를 알아서 처리합니다.  
👉 사람보다 효율적.  

**Learning to write and use CloudFormation templates is a valuable skill for AWS infrastructure management.**  
CloudFormation 템플릿 작성 및 활용 능력은 AWS 인프라 관리에 있어 귀중한 기술입니다.  
👉 클라우드 엔지니어의 필수 역량.  

🎖 보상 획득: "CloudFormation 숙련도 +200 EXP"  

---

# Key Takeaways  
# 핵심 요약  
👉 최종 보상 지급 🎁✨  

**CloudFormation allows you to define and manage AWS infrastructure as code using templates.**  
CloudFormation은 템플릿을 사용하여 AWS 인프라를 코드로 정의하고 관리합니다.  
🎖 보상: "인프라 자동화 능력 +100 EXP"  

**Templates are region-specific, and AMI IDs must correspond to the chosen AWS region.**  
템플릿은 리전별이며 AMI ID는 해당 리전에 맞아야 합니다.  
🎖 보상: "리전 관리력 +80 EXP"  

**Application Composer provides a visual interface to understand and edit CloudFormation templates.**  
Application Composer는 CloudFormation 템플릿을 이해하고 수정할 수 있는 시각적 인터페이스를 제공합니다.  
🎖 보상: "시각화 활용력 +90 EXP"  

**CloudFormation manages resource creation, updates, and deletion in the correct order, simplifying infrastructure management.**  
CloudFormation은 리소스를 올바른 순서로 생성/업데이트/삭제하여 인프라 관리를 단순화합니다.  
🎖 보상: "운영 단순화 +110 EXP"  

---

🔥 최종 게임 보상: `+1770 EXP`  
레벨 업까지 `230 EXP` 남았습니다. 🕹️  
```
