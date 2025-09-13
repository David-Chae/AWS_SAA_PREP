# Amazon ECR  
# 아마존 ECR  
(Amazon ECR: AWS에서 Docker 이미지를 저장하고 관리하는 서비스)

---

## Introduction to Amazon ECR  
## Amazon ECR 소개  
(ECR의 기본 개념과 역할 설명)

Amazon ECR stands for Elastic Container Registry, and it is used to store and manage Docker images on AWS.  
Amazon ECR은 Elastic Container Registry의 약자로, AWS에서 Docker 이미지를 저장하고 관리하는 데 사용된다.  
(ECR은 Docker Hub와 유사하지만 AWS 내부에서 관리되는 레지스트리)

So far, we have been using online repositories such as Docker Hub, but we can also store our own images on Amazon ECR.  
지금까지 Docker Hub 같은 온라인 레포지토리를 사용했지만, Amazon ECR에 직접 이미지를 저장할 수도 있다.  
(자체 이미지를 AWS 환경에 안전하게 관리 가능)

---

## Repository Options  
## 레포지토리 옵션  
(ECR에서 이미지 저장 방식 선택)

With Amazon ECR, you have two options:  
Amazon ECR에는 두 가지 옵션이 있다.  

- you can store images privately, just for your account or your own accounts,  
- 개인 계정 전용으로 프라이빗하게 이미지를 저장할 수 있고,  

- or you can use a public repository and publish to the Amazon ECR public gallery.  
- 또는 퍼블릭 레포지토리를 사용해 Amazon ECR 퍼블릭 갤러리에 이미지를 공개할 수도 있다.  

---

## Integration with Amazon ECS  
## Amazon ECS와의 통합  
(ECR과 ECS의 연동 방식)

ECR is fully integrated with Amazon ECS, which is great.  
ECR은 Amazon ECS와 완전히 통합되어 있어 편리하다.  
(ECS 태스크가 쉽게 이미지를 가져올 수 있음)

Your images are behind the scenes stored by Amazon S3.  
이미지는 내부적으로 Amazon S3에 저장된다.  
(실제 저장 위치는 S3)

Your ECR repository may contain different Docker images, and then your ECS cluster, for example, an EC2 instance on your ECS cluster, may want to pull these images.  
ECR 레포지토리는 여러 Docker 이미지를 포함할 수 있으며, ECS 클러스터 내 EC2 인스턴스 등이 이 이미지를 가져와 실행할 수 있다.  
(ECS와 ECR이 협력하는 구조)

---

## Access Control and IAM Roles  
## 접근 제어와 IAM 역할  
(ECR 이미지 접근 권한 관리)

To pull images, we assign an IAM role to our EC2 instance.  
이미지를 가져오려면 EC2 인스턴스에 IAM 역할을 할당한다.  
(EC2가 ECR에 접근 가능하도록 권한 부여)

This IAM role will allow the instance to pull Docker images.  
이 IAM 역할이 인스턴스가 Docker 이미지를 가져오도록 허용한다.  

All access to ECR is protected by IAM.  
ECR 접근은 모두 IAM으로 보호된다.  
(권한이 없으면 접근 불가)

If you encounter a permission error on ECR, review your policies.  
ECR에서 권한 오류가 발생하면 정책을 검토해야 한다.  
(정책 설정 오류가 흔한 문제)

Your containers will be started on your EC2 instance after they are pulled by the instance.  
이미지를 가져오면, 해당 EC2 인스턴스에서 컨테이너가 실행된다.  
(ECS가 ECR에서 이미지 가져와 컨테이너 실행)

This is how ECS and ECR work together.  
이것이 ECS와 ECR의 협동 방식이다.  
(이미지 관리와 컨테이너 실행 연결)

---

## Additional Features of Amazon ECR  
## Amazon ECR의 추가 기능  
(ECR이 단순 레포지토리 이상의 기능 제공)

Amazon ECR is great because, on top of being a repository, it supports image vulnerability scanning, versioning, image tags, and image lifecycle management.  
ECR은 단순 레포지토리뿐 아니라 이미지 취약점 스캔, 버전 관리, 태그 관리, 라이프사이클 관리 기능을 제공한다.  
(보안과 관리 기능까지 지원)

Overall, anytime you see storing Docker images, think ECR, and that should be it for you at the exam.  
결론적으로 Docker 이미지를 저장할 때는 ECR을 생각하면 되고, 시험에서도 중요한 개념이다.  
(시험 대비 핵심 포인트)

---

## Key Takeaways  
## 핵심 요약  

- Amazon ECR stands for Elastic Container Registry and is used to store and manage Docker images on AWS.  
- Amazon ECR은 Elastic Container Registry의 약자로, AWS에서 Docker 이미지를 저장하고 관리하는 서비스  

- ECR supports both private repositories for individual accounts and public repositories accessible via the Amazon ECR public gallery.  
- ECR은 개인 계정용 프라이빗 레포지토리와 퍼블릭 갤러리를 통한 공개 레포지토리를 지원  

- ECR integrates fully with Amazon ECS, with images stored behind the scenes in Amazon S3.  
- ECR은 Amazon ECS와 완전히 통합되며, 이미지는 내부적으로 S3에 저장  

- Access to ECR is secured by IAM roles, which must be correctly configured to allow EC2 instances to pull Docker images.  
- ECR 접근은 IAM 역할로 보호되며, EC2가 이미지를 가져올 수 있도록 올바르게 설정해야 함  

- Amazon ECR offers features such as image vulnerability scanning, versioning, image tags, and lifecycle management.  
- ECR은 이미지 취약점 스캔, 버전 관리, 태그, 라이프사이클 관리 등의 기능 제공

---

🎮 **보상 지급!**

* ECR 노트 퀘스트 완료! 🏆
* **+140 XP**
* 아이템 획득: **\[ECR Key 🔑]** (컨테이너 이미지 관리 마스터에게 주어지는 상징)
