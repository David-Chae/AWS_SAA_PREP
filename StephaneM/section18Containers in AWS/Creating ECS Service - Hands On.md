# Creating ECS Service - Hands On  
# ECS 서비스 생성 - 실습  

---

## Creating an ECS Task Definition  
## ECS 태스크 정의 생성  

To begin, we need to create an ECS service. However, before doing so, it is necessary to create a task definition.  
먼저 ECS 서비스를 만들기 위해 태스크 정의를 생성해야 합니다.  

I will create a new task definition from the task definition panel and assign it a name.  
태스크 정의 패널에서 새 태스크 정의를 만들고 이름을 지정합니다.  

I will call this task definition nginxdemos-hello.  
이 태스크 정의의 이름은 **nginxdemos-hello**로 합니다.  

This task definition uses the Docker image called nginxdemohello available on Docker Hub.  
이 태스크 정의는 Docker Hub에 있는 **nginxdemohello** 이미지를 사용합니다.  

This is the image we will use in our demonstration, which is why the task definition is named accordingly.  
이번 데모에서 사용할 이미지이므로 태스크 정의 이름을 그렇게 지었습니다.  

---

Next, we must choose the infrastructure requirements.  
다음으로 인프라 요구 사항을 선택해야 합니다.  

We have the option to launch on AWS Fargate or Amazon EC2 instances.  
AWS Fargate 또는 Amazon EC2 인스턴스에서 실행할 수 있습니다.  

Fargate is a serverless compute engine, so we will leave it enabled.  
Fargate는 서버리스 컴퓨팅 엔진이므로 그대로 활성화 상태로 둡니다.  

Enabling this option allows launching the task and service on Amazon EC2 instances, but for simplicity, we will use AWS Fargate and launch our containers in serverless compute mode.  
이 옵션을 켜면 EC2에서도 실행 가능하지만, 단순화를 위해 Fargate에서 서버리스 모드로 실행합니다.  

---

We then select the operating system and architecture. Linux is suitable for our needs.  
운영체제와 아키텍처를 선택합니다. Linux가 적합합니다.  

Next, we specify the task size for our Fargate container.  
그 다음 Fargate 컨테이너의 태스크 크기를 지정합니다.  

For example, we can select 0.5 or 1 vCPU, and the maximum allowed is 16 vCPUs.  
예를 들어 0.5 또는 1 vCPU를 선택할 수 있고, 최대 16 vCPU까지 가능합니다.  

We can also adjust the memory allocation; for instance, up to 120 gigabytes of memory can be assigned.  
메모리도 조정할 수 있으며, 최대 120GB까지 할당 가능합니다.  

All these resources are provided by Fargate in a serverless fashion.  
이 모든 리소스는 서버리스 방식으로 Fargate에서 제공합니다.  

To keep costs low and the setup simple, I will choose 0.5 vCPU and 1 gigabyte of memory.  
비용과 단순성을 위해 **0.5 vCPU, 1GB 메모리**를 선택합니다.  

---

## Task Roles  
## 태스크 역할  

The task role is an IAM role that can be assigned to the task if it needs to make API requests to AWS services.  
태스크 역할은 태스크가 AWS API 요청을 해야 할 때 부여할 수 있는 IAM 역할입니다.  

Since we do not require this functionality at the moment, we will not specify a task role.  
이번에는 필요하지 않으므로 지정하지 않습니다.  

However, this is crucial if your containers need to interact with AWS services.  
그러나 컨테이너가 AWS 서비스와 상호작용해야 한다면 반드시 필요합니다.  

For the task execution role, we will leave it as the default.  
태스크 실행 역할은 기본값으로 둡니다.  

If the ECS task execution role does not exist yet, it will be created automatically by the ECS service.  
ECS 태스크 실행 역할이 없다면 ECS가 자동으로 생성합니다.  

---

## Container Configuration  
## 컨테이너 설정  

We will name the container nginxdemos-hello.  
컨테이너 이름은 **nginxdemos-hello**로 지정합니다.  

The image URL will be nginxdemoshello/hello, which will automatically pull the image from Docker Hub.  
이미지 URL은 **nginxdemoshello/hello**이며, Docker Hub에서 자동으로 가져옵니다.  

This is a convenient and essential container for our demonstration.  
데모에 필수적인 컨테이너입니다.  

---

There are several options available, such as port mappings.  
여러 옵션이 있으며, 그 중 하나는 포트 매핑입니다.  

We want to map port 80 on the host to port 80 on the container, which is the default and suitable for our needs.  
호스트의 80번 포트를 컨테이너의 80번 포트에 매핑합니다(기본값).  

Additional port mappings can be added if necessary.  
필요하면 추가 매핑을 할 수 있습니다.  

---

Resource allocation limits, environment variables (from a file or manually), and logging options are also available, but we will leave these as default since the current settings suffice.  
리소스 제한, 환경 변수, 로깅 옵션 등을 지정할 수 있지만, 기본값으로 둡니다.  

Regarding storage, Fargate provides ephemeral storage. The default is 21 gigabytes, which we will keep unchanged.  
스토리지는 Fargate에서 제공하며, 기본값은 21GB입니다. 그대로 둡니다.  

---

Let's create this task definition.  
이제 태스크 정의를 생성합니다.  

Since I have created it twice, it shows version two, but for you, it should be version one.  
제가 두 번 만들었기 때문에 버전 2로 보이지만, 여러분은 버전 1일 것입니다.  

---

## Launching the ECS Service  
## ECS 서비스 실행  

Next, we will launch this task definition as a service.  
이제 이 태스크 정의를 서비스로 실행합니다.  

Navigate to the clusters section, then select the demo cluster.  
Clusters 섹션으로 가서 DemoCluster를 선택합니다.  

Under services, click to create a new service.  
Services 메뉴에서 새 서비스를 생성합니다.  

---

Specify the service details by selecting the task definition family nginxdemoshello.  
서비스 세부 사항에서 **nginxdemoshello** 태스크 정의 패밀리를 선택합니다.  

Choose the latest revision available; for me, this is revision number two.  
가장 최신 리비전을 선택합니다. (여기서는 2번 리비전)  

You can keep or modify the service name as desired.  
서비스 이름은 유지하거나 변경할 수 있습니다.  

---

The service will be created within this cluster.  
서비스는 해당 클러스터 내에 생성됩니다.  

For compute configuration, we will use the capacity provider strategy with the default settings and select Fargate to launch our services and tasks.  
컴퓨트 구성은 기본값을 사용하고, 서비스와 태스크는 Fargate로 실행합니다.  

The platform version will remain as the latest.  
플랫폼 버전은 최신으로 둡니다.  

We will not modify deployment options or availability zone rebalancing, which helps distribute tasks evenly across availability zones.  
배포 옵션과 AZ 재조정은 수정하지 않습니다.  

---

For deployment configuration, which controls replicas, we will start with one task.  
배포 구성에서 복제본 개수를 지정할 수 있으며, 기본은 1입니다.  

If more tasks are desired, for example four, the service would run four containers of the nginxdemo application.  
원한다면 4개 태스크를 실행해 Nginx 컨테이너 4개를 띄울 수 있습니다.  

To keep costs minimal, we will keep it at one.  
비용 절감을 위해 1로 둡니다.  

---

For networking, we will use the existing subnets and create a new security group.  
네트워킹에서는 기존 서브넷을 사용하고, 새 보안 그룹을 만듭니다.  

The default name is acceptable.  
이름은 기본값을 사용합니다.  

We will allow HTTP traffic from anywhere to enable access to port 80 of our Nginx service.  
HTTP 트래픽을 허용해 누구나 80번 포트로 접근할 수 있도록 설정합니다.  

Public IP assignment will be enabled to allow external access.  
외부 접근을 위해 퍼블릭 IP 할당을 활성화합니다.  

---

For load balancing, we will enable it and create an application load balancer named DemoALBForECS.  
로드 밸런싱을 활성화하고 **DemoALBForECS**라는 ALB를 만듭니다.  

The listener will be on port 80.  
리스너는 80번 포트로 설정합니다.  

We will also create a new target group named nginxdemosTG on port 80.  
**nginxdemosTG**라는 새로운 Target Group을 80번 포트에 생성합니다.  

We will not configure VPC Lattice or service auto scaling at this time.  
VPC Lattice와 오토스케일링은 설정하지 않습니다.  

No volumes will be set up. Finally, create the service.  
볼륨도 설정하지 않고, 서비스를 생성합니다.  

---

The service has now been deployed successfully.  
서비스가 성공적으로 배포되었습니다.  

Clicking on the service shows one desired task, which is running with an active status.  
서비스를 클릭하면 원하는 태스크 1개가 실행 중임을 확인할 수 있습니다.  

The service is linked to a target group.  
서비스는 Target Group에 연결되어 있습니다.  

By clicking on the target group, we see it is associated with the application load balancer created for this service.  
Target Group을 클릭하면 ALB와 연결된 것을 확인할 수 있습니다.  

One IP address is registered as a target, corresponding to the container's private IP address.  
하나의 IP가 등록되어 있으며, 이는 컨테이너의 프라이빗 IP입니다.  

---

The load balancer is active. Copying its DNS name and opening it in a browser displays the Nginx welcome page, confirming that everything is functioning correctly.  
로드 밸런서는 활성 상태이며, DNS를 브라우저에 입력하면 Nginx 환영 페이지가 정상 표시됩니다.  

---

Within the service, we can view the tasks.  
서비스 내에서 태스크를 확인할 수 있습니다.  

Currently, one container is running.  
현재 컨테이너 1개가 실행 중입니다.  

Clicking on the task reveals its configuration, revision, launch location, private IP, and container details.  
태스크를 클릭하면 설정, 리비전, 실행 위치, 프라이빗 IP, 컨테이너 세부정보를 확인할 수 있습니다.  

Logs for the Nginx container are also accessible.  
Nginx 로그도 볼 수 있습니다.  

---

The service events indicate that one task has started, registered in the target group, completed deployment, and reached a steady state.  
서비스 이벤트에서 태스크가 시작되고, TG에 등록되고, 배포가 완료되어 안정 상태에 도달했음을 확인할 수 있습니다.  

Navigating to /test on the URL changes the URI accordingly, demonstrating that Nginx is working as expected.  
URL 뒤에 `/test`를 붙이면 URI가 바뀌고, 정상 작동을 확인할 수 있습니다.  

---

## Scaling the ECS Service  
## ECS 서비스 확장  

Since we are using ECS, scaling is straightforward.  
ECS에서는 확장이 간단합니다.  

We currently have one task running, but we can increase this number.  
현재 1개의 태스크가 실행 중이지만, 더 늘릴 수 있습니다.  

Let's update the service to have a desired count of three tasks, for example one per availability zone.  
서비스를 업데이트해 원하는 개수를 3으로 변경합니다.  

Other settings such as task definition and compute configuration remain unchanged.  
태스크 정의나 컴퓨트 구성은 그대로 둡니다.  

After updating, ECS will provision two additional tasks on Fargate.  
업데이트 후 ECS가 2개의 태스크를 추가로 생성합니다.  

Behind the scenes, AWS automatically provisions the necessary resources to launch these tasks.  
백엔드에서 AWS가 자동으로 필요한 리소스를 프로비저닝합니다.  

Refreshing the tasks page shows the new tasks transitioning from pending to activating and then running states.  
태스크 페이지 새로고침 시 Pending → Activating → Running 상태로 변하는 것을 확인할 수 있습니다.  

The load balancer distributes traffic across all running containers, as evidenced by the changing IP addresses upon refresh.  
로드 밸런서는 실행 중인 컨테이너로 트래픽을 분산하며, 새로고침 시 IP가 바뀌는 것을 볼 수 있습니다.  

---

To scale down and save costs, update the service to have zero desired tasks.  
비용 절감을 위해 서비스의 원하는 태스크 수를 0으로 변경합니다.  

The service remains but no containers run.  
서비스는 유지되지만 컨테이너는 실행되지 않습니다.  

Additionally, ensure the desired capacity of the auto scaling group is set to zero to avoid running EC2 instances unnecessarily.  
EC2 인스턴스가 실행되지 않도록 ASG의 원하는 용량도 0으로 설정해야 합니다.  

Verify that no tasks are running and review service events to understand ECS actions during the update.  
태스크가 실행되지 않음을 확인하고, 서비스 이벤트에서 업데이트 과정의 ECS 동작을 확인합니다.  

---

## This concludes the demonstration  
## 데모 종료  

This concludes the demonstration of creating an ECS cluster, deploying an ECS service on Fargate, and scaling the service.  
ECS 클러스터 생성, ECS 서비스 배포, 서비스 확장 데모가 완료되었습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created an ECS task definition using the nginxdemos-hello Docker image.  
- **nginxdemos-hello** Docker 이미지를 사용해 ECS 태스크 정의를 생성함.  

- Configured the task to run on AWS Fargate with specified CPU and memory resources.  
- 지정된 CPU/메모리 리소스를 갖춘 태스크를 AWS Fargate에서 실행하도록 설정함.  

- Launched an ECS service with load balancing and public IP enabled.  
- 로드 밸런싱 및 퍼블릭 IP를 활성화하여 ECS 서비스를 실행함.  

- Demonstrated scaling the ECS service by increasing and decreasing the desired number of tasks.  
- ECS 서비스의 태스크 개수를 늘리고 줄이는 스케일링을 시연함.  


✨ **+150 XP 획득**
🏅 칭호: *“서비스의 지휘자”* 획득!
🎁 보너스 아이템: `[ECS Service의 황금 톱니바퀴 ⚙️]`
