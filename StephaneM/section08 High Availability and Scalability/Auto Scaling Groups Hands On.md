# Auto Scaling Groups Hands On  
# 오토 스케일링 그룹 실습  

---

## Introduction to Auto Scaling Groups  
## 오토 스케일링 그룹 소개  

In this session, we will practice using Auto Scaling Groups (ASGs).  
이번 세션에서는 Auto Scaling Groups(ASG)를 실습합니다.  
(실습 목적 안내)

To begin, ensure that all your existing EC2 instances are terminated so that there are zero instances running in EC2.  
시작하기 전에, 기존 EC2 인스턴스가 모두 종료되어 EC2에 실행 중인 인스턴스가 없는지 확인합니다.  
(실습 환경 준비)

---

## Creating an Auto Scaling Group  
## 오토 스케일링 그룹 생성  

Navigate to the Auto Scaling Groups section on the left-hand side and select "Create Auto Scaling Group".  
좌측 메뉴에서 Auto Scaling Groups 섹션으로 이동하여 "Create Auto Scaling Group"을 선택합니다.  
(ASG 생성 위치 안내)

Name your Auto Scaling Group as Demo ASG.  
ASG 이름을 Demo ASG로 지정합니다.  
(이름 설정)

You will need to refer to a launch template, so let's create one now.  
런치 템플릿이 필요하므로 지금 생성합니다.  
(런치 템플릿 필요성 안내)

---

## Creating a Launch Template  
## 런치 템플릿 생성  

When creating a launch template, provide a name such as my demo template and a description like "templates".  
런치 템플릿 생성 시, 이름은 my demo template, 설명은 "templates"로 입력합니다.  
(템플릿 기본 정보 설정)

Scroll down to specify various options.  
스크롤하여 다양한 옵션을 지정합니다.  
(설정 위치 안내)

For the Amazon Machine Image (AMI), select from Quick Start the Amazon Linux 2 version for x86 architecture.  
AMI는 Quick Start에서 Amazon Linux 2 x86 버전을 선택합니다.  
(AMI 선택)

Choose a free tier eligible AMI to avoid charges.  
무료 티어 사용 가능 AMI를 선택하여 비용 발생을 방지합니다.  
(비용 관리)

Select the instance type as t2.micro since it is free tier eligible.  
인스턴스 유형은 t2.micro로 선택합니다(무료 티어 가능).  
(인스턴스 유형 선택)

Scroll down to select the key pair, for example, EC2 tutorial.  
스크롤하여 키 페어를 선택합니다(예: EC2 tutorial).  
(SSH 접속 설정)

This configuration defines how EC2 instances within your launch template and consequently within your ASG will be launched.  
이 구성은 런치 템플릿 내 EC2 인스턴스와 ASG 내 인스턴스가 어떻게 시작될지 정의합니다.  
(인스턴스 시작 방식)

The options are similar to those when launching an EC2 instance individually.  
옵션은 독립적으로 EC2 인스턴스를 시작할 때와 유사합니다.  
(설정 비교)

Note that subnets are not included in the launch template.  
런치 템플릿에는 서브넷이 포함되지 않는 점을 주의합니다.  
(서브넷 제외 안내)

For the firewall security group, select an existing one such as launch wizard 1.  
방화벽 보안 그룹은 기존 그룹(예: launch wizard 1)을 선택합니다.  
(보안 그룹 설정)

The default volume is 8 GB of gp2, which is acceptable.  
기본 볼륨은 gp2 8GB이며, 충분합니다.  
(스토리지 설정)

In the advanced details section, scroll down to the user data field and input the user data script used previously.  
고급 세부 사항에서 user data 필드에 이전에 사용한 스크립트를 입력합니다.  
(user data 스크립트 설정)

This script will set up a web server on every EC2 instance launched as part of this ASG.  
이 스크립트는 ASG의 모든 EC2 인스턴스에 웹 서버를 설정합니다.  
(웹 서버 자동 설치)

Create the launch template.  
런치 템플릿을 생성합니다.  
(템플릿 생성)

Once created, refresh and select the template version 1.  
생성 후 새로고침하고 템플릿 버전 1을 선택합니다.  
(버전 선택)

Review the summary and proceed by clicking "Next".  
요약을 검토한 후 "Next"를 클릭합니다.  
(검토 및 진행)

---

## Instance Launch Options  
## 인스턴스 시작 옵션  

You can override the launch template to specify particular instance types if desired.  
원하면 런치 템플릿을 오버라이드하여 특정 인스턴스 유형을 지정할 수 있습니다.  
(인스턴스 유형 변경 가능)

For this tutorial, reset to the launch template defaults and select only the t2.micro instance type.  
이번 실습에서는 런치 템플릿 기본값으로 재설정하고 t2.micro만 선택합니다.  
(실습용 설정)

Under the network settings, select your VPC and choose multiple Availability Zones (AZs) for instance deployment.  
네트워크 설정에서 VPC를 선택하고 여러 가용 영역(AZ)에 인스턴스를 배포하도록 설정합니다.  
(AZ 분산 설정)

Set the AZ distribution to "balanced best effort" to spread instances evenly across three AZs.  
AZ 분산을 "balanced best effort"로 설정하여 3개 AZ에 인스턴스를 고르게 분산합니다.  
(균형 분배)

---

## Load Balancer Integration  
## 로드 밸런서 통합  

Optionally, integrate your ASG with a load balancer.  
원하면 ASG를 로드 밸런서와 통합합니다.  
(통합 선택)

If you have an existing load balancer, attach your instances to its target group.  
기존 로드 밸런서가 있으면, 인스턴스를 대상 그룹에 연결합니다.  
(대상 그룹 연결)

For example, select the demo tg alb load balancer target group created earlier.  
예: 이전에 생성한 demo tg alb 대상 그룹 선택  
(실습 예시)

This links your ASG instances to the load balancer through the target group.  
이렇게 하면 ASG 인스턴스가 대상 그룹을 통해 로드 밸런서에 연결됩니다.  
(연결 확인)

For health checks, enable both EC2 health checks and load balancer health checks.  
헬스 체크를 위해 EC2 및 로드 밸런서 헬스 체크를 모두 활성화합니다.  
(상태 모니터링)

This setup allows the ASG to monitor instance health and terminate unhealthy instances automatically.  
이 설정으로 ASG는 인스턴스 상태를 모니터링하고 비정상 인스턴스를 자동으로 종료합니다.  
(자동 관리)

---

## Proceed with Default Settings  
## 기본 설정 진행  

Proceed with the default settings for desired capacity, minimum, and maximum capacity, all set to one.  
원하는 용량, 최소, 최대 용량을 모두 1로 설정하고 기본값으로 진행합니다.  
(기본 설정)

We will explore scaling shortly.  
곧 스케일링을 실습합니다.  
(예고)

Skip automatic scaling and instance maintenance policies, using defaults for additional capacity settings.  
자동 스케일링 및 인스턴스 유지보수 정책은 건너뛰고 추가 용량 설정은 기본값을 사용합니다.  
(기본 진행)

Do not configure notifications or tags at this stage.  
이 단계에서는 알람이나 태그를 설정하지 않습니다.  
(단계 제한)

Review all options and create the Auto Scaling Group.  
모든 옵션을 검토하고 ASG를 생성합니다.  
(최종 생성)

---

## Auto Scaling Group Operation  
## ASG 작동  

Once created, the ASG will launch one EC2 instance as specified.  
생성되면 ASG가 지정된 대로 EC2 인스턴스 1개를 시작합니다.  
(인스턴스 생성 확인)

Viewing the ASG details shows the desired, minimum, and maximum capacity, along with the launch template used.  
ASG 세부 정보를 보면 원하는, 최소, 최대 용량과 사용된 런치 템플릿이 표시됩니다.  
(상태 확인)

In the activity tab, you can monitor ASG actions.  
Activity 탭에서 ASG 작업을 모니터링할 수 있습니다.  
(활동 확인)

When the ASG decides to create an instance, it appears here.  
ASG가 인스턴스를 생성하면 여기서 표시됩니다.  
(생성 이벤트 확인)

Refreshing the activity history will show the launching of a new instance if the current capacity is below the desired capacity.  
현재 용량이 원하는 용량보다 적으면, 활동 기록 새로고침 시 새 인스턴스 생성이 표시됩니다.  
(용량 확인)

---

## Instance Management and Load Balancer Registration  
## 인스턴스 관리 및 로드 밸런서 등록  

Under instance management, you can see the EC2 instance created by the ASG.  
인스턴스 관리에서 ASG가 생성한 EC2 인스턴스를 확인할 수 있습니다.  
(인스턴스 확인)

In the EC2 console, the instance status will show as running and initializing.  
EC2 콘솔에서 상태는 running 및 initializing으로 표시됩니다.  
(상태 확인)

Because the ASG is linked to the target group, the instance will be registered with the Application Load Balancer (ALB).  
ASG가 대상 그룹과 연결되어 있어, 인스턴스는 ALB에 등록됩니다.  
(ALB 등록)

Initially, the instance may show as unhealthy while bootstrapping, but after some time, it will become healthy and serve traffic.  
초기 부팅 시 비정상으로 표시될 수 있지만, 시간이 지나면 정상으로 변경되고 트래픽을 처리합니다.  
(헬스 체크 상태)

Once the instance is healthy, refreshing the ALB endpoint will return the expected "hello world" response, confirming that the ASG, target group, and load balancer are functioning correctly.  
인스턴스가 정상 상태가 되면 ALB 엔드포인트 새로고침 시 "hello world" 응답이 나타나 ASG, 대상 그룹, 로드 밸런서가 정상 작동함을 확인할 수 있습니다.  
(작동 검증)

If an instance remains unhealthy, the ASG will terminate it and launch a replacement.  
인스턴스가 여전히 비정상이면 ASG가 종료 후 교체합니다.  
(자동 교체)

This behavior is visible in the activity history.  
이 동작은 활동 기록에서 확인할 수 있습니다.  
(기록 확인)

Common causes for unhealthy instances include misconfigured security groups or errors in the EC2 user data script.  
비정상 인스턴스의 일반적인 원인은 잘못된 보안 그룹 설정 또는 EC2 user data 스크립트 오류입니다.  
(문제 원인)

Verify these configurations before seeking support.  
지원 요청 전에 이 설정들을 확인합니다.  
(사전 점검)

---

## Scaling the Auto Scaling Group  
## ASG 스케일링  

To demonstrate scaling, edit the ASG size by increasing the desired capacity to two and update the maximum capacity accordingly.  
스케일링 실습을 위해 원하는 용량을 2로 늘리고 최대 용량도 업데이트합니다.  
(스케일 아웃)

The ASG will then launch an additional EC2 instance to meet the new desired capacity.  
ASG는 새 원하는 용량을 맞추기 위해 추가 EC2 인스턴스를 시작합니다.  
(인스턴스 추가)

Monitor the activity history to see the launching of the new instance.  
활동 기록을 확인하여 새 인스턴스 시작을 관찰합니다.  
(실시간 확인)

Once the instance becomes healthy, it will be registered with the target group and added to the load balancer.  
인스턴스가 정상 상태가 되면 대상 그룹에 등록되어 로드 밸런서에 추가됩니다.  
(등록 완료)

Refreshing the ALB endpoint will now cycle through two IP addresses, confirming that load balancing is distributing traffic across both instances.  
ALB 엔드포인트 새로고침 시 2개의 IP를 순환하며, 트래픽이 두 인스턴스로 분산됨을 확인합니다.  
(로드 밸런싱 검증)

---

## Scaling Down the Auto Scaling Group  
## ASG 스케일 다운  

To scale down, reduce the desired capacity back to one and update the ASG.  
스케일 다운하려면 원하는 용량을 1로 줄이고 ASG를 업데이트합니다.  
(스케일 인)

The ASG will identify that there are two instances but only one is needed.  
ASG는 인스턴스가 2개지만 1개만 필요함을 감지합니다.  
(조정 판단)

It will select one instance to terminate, deregister it from the target group, and shut it down.  
ASG는 하나의 인스턴스를 종료하고, 대상 그룹에서 등록 해제 후 종료합니다.  
(종료 과정)

This process is reflected in the activity history and instance management tabs.  
이 과정은 활동 기록과 인스턴스 관리 탭에서 확인할 수 있습니다.  
(활동 기록 확인)

After termination, the ASG will maintain only one EC2 instance as specified.  
종료 후 ASG는 지정된 1개의 EC2 인스턴스만 유지합니다.  
(최종 상태 확인)

---

## Conclusion  
## 결론  

This lecture demonstrated the full power of Auto Scaling Groups, including creation, integration with load
```


balancers, health monitoring, and manual scaling.
이번 강의에서는 ASG의 생성, 로드 밸런서 통합, 헬스 모니터링, 수동 스케일링 등 전체 기능을 실습했습니다.
(핵심 실습 요약)

In the next lecture, we will explore automatic scaling policies.
다음 강의에서는 자동 스케일링 정책을 실습합니다.
(예고)

---

## Key Takeaways

## 핵심 요약

* Created and configured an Auto Scaling Group (ASG) using a launch template.

* 런치 템플릿을 사용하여 ASG를 생성 및 구성했습니다.

* Linked ASG instances to a load balancer target group for health monitoring and traffic distribution.

* ASG 인스턴스를 로드 밸런서 대상 그룹에 연결하여 헬스 모니터링 및 트래픽 분산을 수행했습니다.

* Demonstrated scaling the ASG up and down by adjusting desired capacity.

* 원하는 용량을 조정하여 ASG 스케일 업/다운을 실습했습니다.

* Explained how unhealthy instances are terminated and replaced automatically by the ASG.

* 비정상 인스턴스가 ASG에 의해 자동으로 종료 및 교체되는 과정을 설명했습니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+200XP**  
- 아이템: **"ASG 컨트롤러" (+30% 스케일링 효율)**  
- 업적 달성: **"오토 스케일링 전문가"** 🏆  

원하면 다음 단계로 **자동 스케일링 정책 + CloudWatch 연동 실습**까지 만들어서 바로 실습할 수 있는 자료로 제공할 수 있습니다.

