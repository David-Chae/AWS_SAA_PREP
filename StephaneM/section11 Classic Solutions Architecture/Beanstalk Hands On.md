# Beanstalk Hands On  
# Beanstalk 실습  
👉 설명: 이번 섹션에서는 Elastic Beanstalk을 실제로 사용하여 애플리케이션을 배포하는 실습을 다룬다.  

---

## Introduction to Elastic Beanstalk  
## Elastic Beanstalk 소개  
👉 설명: Beanstalk 서비스 사용을 실습하며 첫 애플리케이션을 생성한다.  

In this session, we will practice using the Elastic Beanstalk service.  
이번 세션에서는 Elastic Beanstalk 서비스를 실습한다.  
👉 설명: 실무 환경에서 Beanstalk을 통한 배포 경험 획득.  

We will start by creating our first application in the Elastic Beanstalk console.  
먼저 Elastic Beanstalk 콘솔에서 첫 애플리케이션을 생성한다.  
👉 설명: 콘솔 기반 GUI 환경에서 작업을 시작.  

---

We have the option to choose either a Web server environment or a Worker environment.  
웹 서버 환경과 워커 환경 중 하나를 선택할 수 있다.  
👉 설명: 웹 요청 처리용인지, 백그라운드 작업용인지 선택.  

Since we want to run a website, we will select the Web server environment.  
웹사이트를 운영하기 때문에 웹 서버 환경을 선택한다.  
👉 설명: HTTP 요청 처리용 EC2 인스턴스 그룹 구성.  

If we wanted to process tasks off of a queue, we would choose a Worker environment, but for now, we will only use the Web server environment.  
큐에서 작업을 처리하려면 워커 환경을 선택하지만, 지금은 웹 서버 환경만 사용한다.  
👉 설명: 워커 환경은 SQS 기반 백그라운드 작업 처리에 적합.  

---

Let's create an application named MyApplication.  
"MyApplication"이라는 이름으로 애플리케이션을 생성하자.  
👉 설명: 실습용 기본 애플리케이션 이름 지정.  

Next, we scroll down to Environment information.  
다음으로 환경 정보를 확인하기 위해 아래로 스크롤한다.  
👉 설명: 환경 이름, 도메인 등 설정 가능.  

The environment name is pre-filled, but I will name it MyApplication-dev to represent my development environment.  
환경 이름이 기본 입력되어 있으나, 개발 환경임을 나타내기 위해 MyApplication-dev로 설정한다.  
👉 설명: 환경 구분을 위해 접두사/접미사 활용.  

A domain name will be automatically generated for this application, which is how we will access our web servers.  
도메인 이름이 자동 생성되며, 이를 통해 웹 서버에 접속할 수 있다.  
👉 설명: Beanstalk이 DNS 설정과 ELB 연결을 자동 처리.  

---

Now, we need to choose a platform. This platform is managed, and I will select Node.js.  
이제 플랫폼을 선택한다. 관리형 플랫폼이며 Node.js를 선택한다.  
👉 설명: 런타임 환경 선택.  

I will use the default options. You may see different options, but using the latest defaults should be fine.  
기본 옵션을 사용한다. 다른 옵션이 보일 수 있지만 최신 기본값을 사용하면 충분하다.  
👉 설명: 학습용 실습에서는 기본값 유지.  

Next, we need to choose some application code. I will use a sample application that matches the environment configuration.  
다음으로 애플리케이션 코드를 선택한다. 환경 구성에 맞는 샘플 애플리케이션을 사용한다.  
👉 설명: 코드 업로드 없이 샘플 앱으로 배포 실습.  

---

Beanstalk can be quite complex for configuration, so we have presets.  
Beanstalk 설정은 복잡할 수 있으므로 프리셋이 제공된다.  
👉 설명: 복잡한 설정을 단순화하기 위한 추천 값 제공.  

We can set recommended values for either a single instance, which is free tier eligible, high availability with a load balancer, or a custom configuration if you want to customize everything.  
프리셋으로 단일 인스턴스(프리티어 가능), 로드 밸런서 기반 고가용성, 맞춤 설정을 선택할 수 있다.  
👉 설명: 환경 목적에 따라 적절한 프리셋 선택.  

To keep things simple, we will select Single instance and click Next.  
단순하게 하기 위해 단일 인스턴스를 선택하고 Next를 클릭한다.  
👉 설명: 실습 목적상 가장 단순한 환경 사용.  

---

Next, we need to configure service access. This involves IAM roles that allow Beanstalk to perform necessary actions.  
다음으로 서비스 접근 권한을 구성한다. Beanstalk이 필요한 작업을 수행할 수 있도록 IAM 역할이 필요하다.  
👉 설명: Beanstalk이 AWS 리소스 생성/관리 가능하도록 권한 설정.  

We can create a new service role, which will create the elasticbeanstalk-service-role.  
새 서비스 역할을 생성할 수 있으며, elasticbeanstalk-service-role이 만들어진다.  
👉 설명: 기본 서비스 역할 생성.  

However, there may be a bug in the console where the EC2 instance profile is not pre-filled, so we need to create it manually.  
단, 콘솔 버그로 EC2 인스턴스 프로필이 자동 입력되지 않을 수 있으므로 수동 생성 필요.  
👉 설명: 실습 중 발생 가능한 콘솔 문제 대응.  

---

To create the EC2 instance profile, go to the IAM console, select Roles, and create a new role for the EC2 service.  
EC2 인스턴스 프로필을 생성하려면 IAM 콘솔에서 Roles 선택 후 EC2 서비스용 새 역할 생성.  
👉 설명: IAM에서 EC2 역할 생성 단계.  

For permissions, filter by 'beanstalk' and add the WebTier, WorkerTier, and MulticontainerDocker policies.  
권한은 'beanstalk'로 필터 후 WebTier, WorkerTier, MulticontainerDocker 정책 추가.  
👉 설명: Beanstalk 관련 정책 연결.  

Then name the role aws-elasticbeanstalk-ec2-role with hyphens. Create the role.  
역할 이름을 aws-elasticbeanstalk-ec2-role로 지정하고 역할 생성.  
👉 설명: 규칙에 맞는 네이밍 및 역할 생성 완료.  

After creating the role, return to the Beanstalk console and refresh.  
역할 생성 후 Beanstalk 콘솔로 돌아가 새로고침.  
👉 설명: 콘솔이 변경 사항을 반영하도록 함.  

The EC2 instance profile field should now be pre-filled with aws-elasticbeanstalk-ec2-role. Once this is set, you can proceed.  
EC2 인스턴스 프로필 필드가 aws-elasticbeanstalk-ec2-role로 자동 입력된다. 설정 완료 후 진행 가능.  
👉 설명: IAM 역할 연결 완료 확인.  

You may review networking, database, instance traffic, and scaling options, but these are optional. For now, click Skip to review to use the default single instance settings.  
네트워크, 데이터베이스, 트래픽, 스케일링 옵션을 검토할 수 있지만 선택 사항이다. 지금은 Skip 클릭하여 기본 단일 인스턴스 설정 사용.  
👉 설명: 실습에서는 기본값 유지.  

---

Ensure that under Service access, both the Service role and EC2 instance profile are selected.  
서비스 접근 권한에서 서비스 역할과 EC2 인스턴스 프로필이 모두 선택되어 있는지 확인.  
👉 설명: 권한 설정 완료 확인.  

When ready, click Submit to create the Beanstalk environment. The creation process will begin, and events will be displayed indicating progress.  
준비되면 Submit 클릭하여 Beanstalk 환경 생성. 진행 이벤트가 표시됨.  
👉 설명: 환경 생성 시작 및 상태 확인.  

---

The events come from the CloudFormation service.  
이 이벤트는 CloudFormation 서비스에서 발생.  
👉 설명: Beanstalk은 내부적으로 CloudFormation을 사용하여 리소스 생성.  

If you navigate to the CloudFormation console, you can see the Elastic Beanstalk stack being created.  
CloudFormation 콘솔에서 Beanstalk 스택 생성 과정을 볼 수 있다.  
👉 설명: 리소스 생성 과정 시각화 가능.  

Events show resources being created, such as Auto Scaling groups, Launch Configurations, Elastic IPs, and more.  
이벤트는 오토 스케일링 그룹, 런치 구성, Elastic IP 등 생성 중인 리소스를 표시.  
👉 설명: 내부 리소스 생성 과정 이해.  

Once creation is complete, the status changes to CREATE_COMPLETE.  
생성이 완료되면 상태가 CREATE_COMPLETE로 변경.  
👉 설명: 환경 생성 완료 표시.  

---

Returning to the Elastic Beanstalk console, the Events tab shows details such as Security Group creation, Elastic IP allocation, and EC2 instance launches.  
Elastic Beanstalk 콘솔로 돌아가면 Events 탭에서 보안 그룹 생성, Elastic IP 할당, EC2 인스턴스 실행 등의 세부 사항 표시.  
👉 설명: 환경 생성 로그 확인.  

Switching to the EC2 console, you can see the running instance, which is a t3.micro with a public IP address.  
EC2 콘솔로 전환하면 실행 중인 t3.micro 인스턴스와 공인 IP 확인 가능.  
👉 설명: 배포된 인스턴스 확인.  

The Elastic IP is allocated to this instance. The Auto Scaling group manages this single EC2 instance, consistent with the single instance preset.  
Elastic IP가 이 인스턴스에 할당됨. 오토 스케일링 그룹이 단일 EC2 인스턴스를 관리하며, 단일 인스턴스 프리셋과 일치.  
👉 설명: 단일 인스턴스 배포 확인.  

---

When the environment is successfully launched, the health status will be OK.  
환경이 성공적으로 시작되면 Health 상태가 OK로 표시.  
👉 설명: 배포 성공 확인 지표.  

You will receive a domain name to access your application. Opening this domain in a browser shows the sample application running on the EC2 instance, confirming successful deployment.  
애플리케이션 접근용 도메인 제공. 브라우저에서 도메인을 열면 EC2에서 샘플 애플리케이션 실행 확인 가능.  
👉 설명: 최종 배포 확인.  

---

Beanstalk simplifies infrastructure creation by generating all necessary resources from the sample code.  
Beanstalk은 샘플 코드로 필요한 모든 리소스를 자동 생성하여 인프라 구성을 단순화.  
👉 설명: 코드 배포 중심으로 인프라 추상화.  

This includes the web server and supporting infrastructure, enabling quick application deployment.  
웹 서버 및 지원 인프라 포함, 빠른 애플리케이션 배포 가능.  
👉 설명: 실습 목표 달성.  

---

Beanstalk provides options to upload new application versions, which are automatically deployed to EC2 instances.  
Beanstalk은 새 애플리케이션 버전을 업로드할 수 있으며, EC2에 자동 배포됨.  
👉 설명: 버전 관리 및 배포 자동화.  

The Health tab shows health checks for all instances. Logs can be viewed for troubleshooting, and Monitoring provides metrics for the application. Additional features include Alarms, update management, and configuration settings for environments.  
Health 탭은 모든 인스턴스 상태 확인. 로그 확인 가능, 모니터링은 애플리케이션 지표 제공. 추가 기능: 알람, 업데이트 관리, 환경 설정.  
👉 설명: 운영 및 모니터링 기능 제공.  

---

You can create multiple environments within the same application, such as MyApplication-dev and MyApplication-prod, allowing separation of development and production environments.  
하나의 애플리케이션 내 여러 환경 생성 가능(예: MyApplication-dev, MyApplication-prod), 개발/운영 환경 분리.  
👉 설명: 멀티 환경 관리 가능.  

---

In summary, Elastic Beanstalk centers around deploying code within managed environments.  
요약하면, Elastic Beanstalk은 관리형 환경에서 코드 배포 중심.  
👉 설명: 개발자가 코드에만 집중할 수 있음.  

It abstracts infrastructure management by creating resources automatically.  
리소스 자동 생성으로 인프라 관리를 추상화.  
👉 설명: 운영 부담 감소.  

CloudFormation, on the other hand, allows arbitrary infrastructure deployment using templates.  
반면 CloudFormation은 템플릿 기반 자유로운 인프라 배포 가능.  
👉 설명: Beanstalk과 CloudFormation 차이점 이해.  

If you are taking further Beanstalk courses, keep your application. Otherwise, you can delete it to clean up resources.  
추가 Beanstalk 강의를 수강한다면 애플리케이션 유지, 그렇지 않으면 리소스 정리를 위해 삭제 가능.  
👉 설명: 실습 후 리소스 관리 팁.  

---

## Key Takeaways

## 핵심 요약

* Created and configured an Elastic Beanstalk application with a web server environment.

* 웹 서버 환경으로 Elastic Beanstalk 애플리케이션 생성 및 구성 완료.

* Manually set up IAM roles and EC2 instance profiles for Beanstalk service access.

* Beanstalk 서비스 접근용 IAM 역할 및 EC2 인스턴스 프로필 수동 설정.

* Observed underlying AWS resources created by Beanstalk via CloudFormation.

* CloudFormation을 통해 Beanstalk이 생성한 AWS 리소스 확인.

* Explored Beanstalk environment management including deployment, monitoring, and configuration options.

* 배포, 모니터링, 환경 설정 등 Beanstalk 환경 관리 실습.

---

🎮 게임보상: **“Beanstalk 실습 마스터 칭호 획득!”** (IAM 설정 + 배포 경험치 +50, CloudFormation 이해 +30)  

