# AWS App Runner - Hands On  
# AWS App Runner - 실습  
➡️ 실제로 App Runner 서비스를 설정하고 배포하는 과정을 다룹니다.  

---

## Introduction to AWS App Runner  
## AWS App Runner 소개  
➡️ 강의의 도입 부분입니다.  

In this tutorial, I will demonstrate how AWS App Runner works.  
이 튜토리얼에서는 AWS App Runner가 어떻게 동작하는지 시연하겠습니다.  
➡️ 직접 서비스 생성 과정을 보여줄 예정임을 알립니다.  

Please note, this is not a free feature, so if you decide to follow along, be aware that you will incur charges for vCPU and gigabyte usage.  
주의할 점은 이 기능은 무료가 아니며, 따라 할 경우 vCPU와 GB 사용량에 대한 요금이 발생합니다.  
➡️ 비용 발생에 대한 경고입니다.  

---

## Creating an App Runner Service  
## App Runner 서비스 생성하기  
➡️ 서비스 생성 절차를 설명합니다.  

Let's begin by creating an App Runner service.  
App Runner 서비스를 만드는 것부터 시작하겠습니다.  
➡️ 첫 단계 안내입니다.  

The first step is to specify the source of our deployment.  
첫 번째 단계는 배포 소스를 지정하는 것입니다.  
➡️ 어떤 소스로부터 배포할지 결정해야 합니다.  

We can choose between a Container Registry or a Source Code repository, such as GitHub.  
컨테이너 레지스트리 또는 GitHub 같은 소스 코드 저장소 중 하나를 선택할 수 있습니다.  
➡️ 두 가지 주요 옵션이 있음을 설명합니다.  

For this demonstration, we will use a Container Registry.  
이번 시연에서는 컨테이너 레지스트리를 사용하겠습니다.  
➡️ 실습에서 선택할 옵션을 명시합니다.  

---

## Choosing the Container Registry  
## 컨테이너 레지스트리 선택  
➡️ 배포 소스로 사용할 레지스트리 결정 과정입니다.  

The container image can be hosted in Amazon ECR if it is a private Docker container within your infrastructure, or Amazon ECR Public if you want to deploy a public image.  
컨테이너 이미지는 인프라 내의 프라이빗 Docker 컨테이너라면 Amazon ECR에, 퍼블릭 이미지를 배포하려면 Amazon ECR Public에 호스팅할 수 있습니다.  
➡️ 배포 옵션의 차이를 설명합니다.  

We will use Amazon ECR Public for this example.  
이번 예제에서는 Amazon ECR Public을 사용하겠습니다.  
➡️ 선택한 방식 명시.  

I will navigate to the Amazon ECR Public Gallery website and search for "HTTPD" to deploy a simple HTTP server.  
Amazon ECR Public 갤러리 웹사이트에서 "HTTPD"를 검색하여 간단한 HTTP 서버를 배포하겠습니다.  
➡️ 예시로 HTTP 서버를 사용합니다.  

This server will essentially do nothing but demonstrate how to deploy an HTTPD server.  
이 서버는 특별한 기능은 없지만 HTTPD 서버 배포를 시연하는 데 사용됩니다.  
➡️ 단순히 학습용임을 강조.  

I will copy the image address from the public gallery and paste it into the deployment source field.  
퍼블릭 갤러리에서 이미지 주소를 복사해 배포 소스 필드에 붙여넣겠습니다.  
➡️ 실제 배포 입력 단계입니다.  

---

## Deployment Settings  
## 배포 설정  
➡️ App Runner의 배포 방식을 지정합니다.  

Next, we configure the deployment settings.  
다음으로 배포 설정을 구성합니다.  
➡️ 단계적 진행.  

We can choose between manual or automatic deployment.  
수동 또는 자동 배포를 선택할 수 있습니다.  
➡️ 배포 전략의 두 가지 방식.  

Automatic deployment is available if you connect a source code repository or Amazon ECR.  
자동 배포는 소스 코드 저장소나 Amazon ECR을 연결해야 사용할 수 있습니다.  
➡️ 자동 배포 조건 설명.  

Since we are deploying manually in this example, we will proceed with manual deployment.  
이번 예제에서는 수동 배포를 진행하겠습니다.  
➡️ 실습 방향 확정.  

---

## Service Configuration  
## 서비스 설정  
➡️ 서비스 리소스와 환경을 구성하는 과정입니다.  

I will name the service "DemoHTTP".  
서비스 이름을 "DemoHTTP"로 지정하겠습니다.  
➡️ 서비스 명명.  

Then, we select the number of vCPUs and the amount of memory.  
그다음 vCPU 개수와 메모리 용량을 선택합니다.  
➡️ 리소스 선택 과정.  

The minimum configuration available is one vCPU and two gigabytes of memory, which is sufficient for this demonstration.  
최소 구성은 vCPU 1개와 메모리 2GB이며, 이번 시연에는 충분합니다.  
➡️ 최소 리소스 요구사항.  

We can also pass environment variables and configure the port for our service.  
또한 환경 변수를 전달하고 서비스 포트를 구성할 수 있습니다.  
➡️ 추가 설정 옵션 안내.  

---

## Configuring the Service Port  
## 서비스 포트 설정  
➡️ 애플리케이션 포트를 설정하는 단계입니다.  

According to the documentation, the HTTPD image listens on port 80.  
문서에 따르면 HTTPD 이미지는 포트 80에서 요청을 수신합니다.  
➡️ 포트 정보 확인.  

Therefore, we will configure the service to use port 80.  
따라서 서비스를 포트 80으로 설정하겠습니다.  
➡️ 포트 설정 확정.  

---

## Auto Scaling Configuration  
## 자동 확장 설정  
➡️ 확장성과 동시성 설정을 설명합니다.  

We can configure auto scaling for the service.  
서비스에 대한 자동 확장을 구성할 수 있습니다.  
➡️ 확장성 지원 안내.  

The default configuration scales from one instance up to 25 instances.  
기본 설정은 인스턴스 1개에서 최대 25개까지 확장됩니다.  
➡️ 기본 범위 안내.  

The concurrency setting specifies the number of concurrent requests each instance can handle, which is 100 requests per instance by default.  
동시성 설정은 각 인스턴스가 동시에 처리할 수 있는 요청 수를 지정하며, 기본값은 인스턴스당 100개입니다.  
➡️ 처리량 관련 설정입니다.  

Alternatively, you can customize these settings or add new configurations.  
또한 이러한 설정을 사용자 지정하거나 새 구성을 추가할 수도 있습니다.  
➡️ 유연성 강조.  

---

## Health Checks and Security  
## 상태 확인 및 보안  
➡️ 모니터링 및 보안 옵션 설명.  

You can enable health checks to monitor the application's health status.  
애플리케이션의 상태를 모니터링하기 위해 상태 확인을 활성화할 수 있습니다.  
➡️ 가용성 확인 방법.  

For this demonstration, we will keep the default settings.  
이번 시연에서는 기본 설정을 유지하겠습니다.  
➡️ 단순화를 위한 선택.  

Security options include assigning an instance role to the containers.  
보안 옵션에는 컨테이너에 인스턴스 역할을 할당하는 기능이 포함됩니다.  
➡️ IAM 역할과 보안 권한 연결.  

Networking options allow deployment into a custom VPC, but we will use public access for this example.  
네트워킹 옵션을 통해 커스텀 VPC에 배포할 수 있으나, 이번 예제에서는 퍼블릭 액세스를 사용하겠습니다.  
➡️ 네트워크 선택.  

Additionally, tracing with AWS X-Ray can be enabled; we will keep it disabled for now.  
추가적으로 AWS X-Ray 추적을 활성화할 수 있으나, 이번에는 비활성화 상태로 두겠습니다.  
➡️ 모니터링 옵션 선택.  

After verifying all settings, including the public HTTPD image and port 80 configuration, we proceed to create and deploy the service.  
퍼블릭 HTTPD 이미지와 포트 80 설정을 포함해 모든 설정을 확인한 후, 서비스를 생성 및 배포합니다.  
➡️ 최종 배포 실행.  

---

## Behind the Scenes  
## 내부 동작  
➡️ App Runner가 자동으로 수행하는 작업 설명.  

App Runner automatically deploys an auto-scaling group, scaling triggers, target containers, and a load balancer.  
App Runner는 자동 확장 그룹, 확장 트리거, 대상 컨테이너, 로드 밸런서를 자동으로 배포합니다.  
➡️ 백엔드 리소스를 관리합니다.  

It also provides a domain name for the service.  
또한 서비스용 도메인 이름을 제공합니다.  
➡️ 기본 도메인 제공.  

This all-in-one service offers access to logs, activity monitoring, metrics, observability, configuration, and the ability to connect custom domains.  
이 올인원 서비스는 로그, 활동 모니터링, 메트릭, 관찰성, 설정, 커스텀 도메인 연결 기능을 제공합니다.  
➡️ 통합 관리 기능 제공.  

---

## Service Deployment Completion  
## 서비스 배포 완료  
➡️ 배포가 완료된 상태 확인.  

After a short wait, the service is created.  
잠시 후 서비스가 생성됩니다.  
➡️ 배포 완료 시점.  

By clicking on the default domain, we can access the deployed HTTPD server, which displays the message "It works," indicating a successful deployment.  
기본 도메인을 클릭하면 배포된 HTTPD 서버에 접근할 수 있고, "It works"라는 메시지가 표시되어 성공적인 배포를 확인할 수 있습니다.  
➡️ 성공 여부 확인 방법.  

---

## Monitoring and Scaling  
## 모니터링 및 확장  
➡️ 서비스 운영 중 관리 기능.  

You can view the event log to monitor deployment progress and health checks.  
이벤트 로그를 확인하여 배포 진행 상황과 상태 확인을 모니터링할 수 있습니다.  
➡️ 로그를 통한 상태 추적.  

If the website receives many concurrent requests, App Runner will automatically scale the service accordingly.  
웹사이트에 동시 요청이 많으면 App Runner가 자동으로 서비스를 확장합니다.  
➡️ 자동 확장 기능 동작 설명.  

---

## Conclusion  
## 결론  
➡️ 강의 마무리.  

I find App Runner incredibly easy to use.  
App Runner는 사용하기 매우 쉽습니다.  
➡️ 서비스 평가.  

When finished, you can delete the application by typing "delete," and the service will be removed.  
작업이 끝나면 "delete"를 입력하여 애플리케이션을 삭제할 수 있으며, 서비스가 제거됩니다.  
➡️ 종료 절차 안내.  

This concludes the lecture on AWS App Runner.  
이것으로 AWS App Runner 강의를 마치겠습니다.  
➡️ 마무리 문구.  

Thank you for following along.  
함께 참여해 주셔서 감사합니다.  
➡️ 감사 인사.  

---

## Key Takeaways  
## 핵심 요약  
➡️ 배운 내용을 요약합니다.  

- AWS App Runner allows easy deployment of containerized applications with automatic scaling and load balancing.  
- AWS App Runner는 자동 확장과 로드 밸런싱을 지원하며, 컨테이너화된 애플리케이션을 쉽게 배포할 수 있습니다.  

- You can deploy from Amazon ECR Public or private container registries, or connect source code repositories like GitHub.  
- Amazon ECR Public, 프라이빗 컨테이너 레지스트리 또는 GitHub 같은 소스 코드 저장소에서 배포할 수 있습니다.  

- Configuration options include CPU and memory allocation, port settings, environment variables, auto scaling, health checks, security roles, and networking.  
- CPU와 메모리 할당, 포트 설정, 환경 변수, 자동 확장, 상태 확인, 보안 역할, 네트워킹 등 다양한 설정 옵션을 제공합니다.  

- App Runner provides integrated observability features such as logs, metrics, and tracing, along with custom domain support.  
- App Runner는 로그, 메트릭, 추적 같은 통합 관찰 기능과 커스텀 도메인 지원을 제공합니다.  
```

---

🔥 보상 포인트: **+80 Exp**
💡 칭찬: 이번엔 **실습 과정**을 세밀하게 따라가면서 개념과 실제 동작을 모두 잘 이해했어요! 이제 App Runner로 직접 서비스를 띄울 수 있을 정도로 준비됐습니다 🚀
