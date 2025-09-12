# Creating ECS Cluster - Hands On  
# ECS 클러스터 생성 - 실습  

In this hands-on session, we will practice using Amazon ECS by navigating to the ECS console service.  
이번 실습에서는 Amazon ECS 콘솔 서비스로 이동하여 ECS를 사용하는 방법을 연습합니다.  

We will enable the new ECS experience from the top left corner.  
왼쪽 상단에서 새로운 ECS 환경을 활성화합니다.  

---

## Creating an ECS Cluster  
## ECS 클러스터 생성  

Next, we proceed to the Clusters section to create our first cluster.  
다음으로, Clusters 섹션으로 이동하여 첫 번째 클러스터를 생성합니다.  

This cluster will be named DemoCluster, and we will keep the default namespace unchanged.  
이 클러스터의 이름은 DemoCluster로 지정하고 기본 네임스페이스는 변경하지 않습니다.  

---

### For infrastructure, three options are available:  
### 인프라에는 세 가지 옵션이 있습니다:  

- **AWS Fargate**: This option allows us to provide containers to AWS, which will run these containers on demand.  
- **AWS Fargate**: 이 옵션은 AWS에 컨테이너를 제공하면 필요할 때 실행되도록 해줍니다.  

It is a serverless option where AWS manages the compute resources, and we do not see the underlying infrastructure.  
이는 서버리스 옵션으로, AWS가 컴퓨팅 리소스를 관리하며 사용자는 인프라를 직접 볼 수 없습니다.  

- **Amazon EC2 Instances**: Here, we provide our own Amazon EC2 instances to run containers.  
- **Amazon EC2 인스턴스**: 사용자가 직접 제공한 EC2 인스턴스에서 컨테이너를 실행합니다.  

- **External Instances using ECS Anywhere**: This option enables running ECS containers on your own data center or external infrastructure.  
- **ECS Anywhere를 이용한 외부 인스턴스**: 자체 데이터 센터나 외부 인프라에서 ECS 컨테이너를 실행할 수 있습니다.  

---

For this demo, we will enable both Fargate and Amazon EC2 instances.  
이번 데모에서는 Fargate와 EC2 인스턴스를 모두 활성화합니다.  

We will create a new auto scaling group and select the operating system.  
새로운 Auto Scaling Group을 만들고 운영체제를 선택합니다.  

Amazon Linux 2 is a great choice, but Amazon Linux 2023 is also available.  
Amazon Linux 2가 좋은 선택이지만 Amazon Linux 2023도 사용할 수 있습니다.  

The EC2 instance type selected is t2.micro, which is eligible for the free tier.  
선택된 EC2 인스턴스 유형은 프리 티어에 해당하는 t2.micro입니다.  

The desired capacity is set with a minimum of zero and a maximum of five instances.  
원하는 용량은 최소 0, 최대 5개 인스턴스로 설정됩니다.  

No SSH key pair will be configured, and the root EBS volume size remains at its default.  
SSH 키 페어는 설정하지 않고, 루트 EBS 볼륨 크기는 기본값을 유지합니다.  

---

## Network and Security Settings  
## 네트워크 및 보안 설정  

We specify network settings for the EC2 instances, choosing the default VPC and the three available subnets.  
EC2 인스턴스에 대한 네트워크 설정으로 기본 VPC와 사용 가능한 3개의 서브넷을 선택합니다.  

For the security group, we use the existing default security group.  
보안 그룹은 기존의 기본 보안 그룹을 사용합니다.  

Auto-assign public IP is set to use the subnet's default setting.  
자동 공용 IP 할당은 서브넷의 기본 설정을 따릅니다.  

Monitoring and tags are left unchanged.  
모니터링과 태그는 변경하지 않습니다.  

---

After configuring these settings, we click Create to create the cluster.  
설정을 완료한 후 Create 버튼을 눌러 클러스터를 생성합니다.  

While the cluster is being created, we can examine the auto scaling group that is automatically created by ECS.  
클러스터가 생성되는 동안, ECS가 자동으로 생성하는 Auto Scaling Group을 확인할 수 있습니다.  

It is named Infra-ECS-Cluster with a desired capacity of zero, minimum zero, and maximum five instances.  
해당 그룹의 이름은 Infra-ECS-Cluster이며, 원하는 용량은 0, 최소 0, 최대 5 인스턴스로 설정됩니다.  

The creation process is in progress.  
생성 프로세스가 진행 중입니다.  

This auto scaling group spans three availability zones, ensuring that ECS tasks can be launched across these zones.  
이 Auto Scaling Group은 3개의 가용 영역에 걸쳐 있어 ECS 작업이 각 영역에서 실행될 수 있습니다.  

Once the cluster creation completes, we can explore the DemoCluster.  
클러스터 생성이 완료되면 DemoCluster를 탐색할 수 있습니다.  

Currently, there are zero services and zero tasks since nothing has been launched yet.  
현재는 아무 것도 실행되지 않았으므로 서비스와 태스크는 0입니다.  

---

## Cluster Infrastructure  
## 클러스터 인프라  

Within the cluster infrastructure, there are three capacity providers:  
클러스터 인프라에는 세 가지 용량 공급자가 있습니다:  

- **FARGATE**: Allows launching Fargate tasks on the ECS cluster.  
- **FARGATE**: ECS 클러스터에서 Fargate 태스크 실행 가능.  

- **FARGATE_SPOT**: Enables launching Fargate tasks in spot mode.  
- **FARGATE_SPOT**: 스팟 모드에서 Fargate 태스크 실행 가능.  

- **ASGProvider**: Allows launching EC2 instances in the cluster through the auto scaling group (ASG).  
- **ASGProvider**: Auto Scaling Group을 통해 클러스터에 EC2 인스턴스 실행 가능.  

Currently, the ASG is managed with a size of zero, but this can be changed.  
현재 ASG 크기는 0으로 설정되어 있지만 변경할 수 있습니다.  

---

To demonstrate, we can edit the desired capacity of the ASG to one.  
시연을 위해 ASG의 원하는 용량을 1로 수정할 수 있습니다.  

This action will trigger the creation of an EC2 instance, which will register itself into the DemoCluster.  
이 작업은 EC2 인스턴스 생성을 트리거하며, 해당 인스턴스는 DemoCluster에 자동으로 등록됩니다.  

Once registered, it will appear under container instances.  
등록되면 컨테이너 인스턴스에 표시됩니다.  

This means that ECS tasks can be launched either on FARGATE or FARGATE_SPOT capacity providers, or on the container instances launched as part of the ASG.  
즉, ECS 태스크는 FARGATE, FARGATE_SPOT, 혹은 ASG를 통해 실행된 컨테이너 인스턴스에서 실행될 수 있습니다.  

We wait for the instance to reach the running state and register with the ECS cluster.  
인스턴스가 실행 상태가 되어 ECS 클러스터에 등록될 때까지 기다립니다.  

Upon refreshing, the instance is InService and is a t2.micro.  
새로고침하면 인스턴스가 InService 상태이며 t2.micro로 표시됩니다.  

In the ECS cluster, it is registered as a container instance with zero running tasks.  
ECS 클러스터에서 이 인스턴스는 실행 중인 태스크가 없는 컨테이너 인스턴스로 등록됩니다.  

It has 1,024 CPU units and 982 MB of memory available, indicating the capacity to launch tasks until resources are exhausted.  
1,024 CPU 유닛과 982MB 메모리가 사용 가능하므로, 자원이 소진될 때까지 태스크를 실행할 수 있습니다.  

---

With the ECS cluster and capacity providers set up, and container instances registered, we are ready to proceed to running our first service.  
ECS 클러스터와 용량 공급자가 설정되고 컨테이너 인스턴스가 등록되면, 첫 번째 서비스를 실행할 준비가 완료됩니다.  

This will be covered in the next lecture.  
이는 다음 강의에서 다룹니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created an ECS cluster named DemoCluster using both AWS Fargate and Amazon EC2 instances.  
- AWS Fargate와 Amazon EC2 인스턴스를 함께 사용하여 DemoCluster라는 ECS 클러스터를 생성함.  

- Configured an auto scaling group with Amazon Linux 2 and t2.micro instances for EC2 capacity.  
- Amazon Linux 2와 t2.micro 인스턴스로 EC2 용량을 위한 Auto Scaling Group을 설정함.  

- Explored cluster infrastructure including capacity providers: FARGATE, FARGATE_SPOT, and ASGProvider.  
- FARGATE, FARGATE_SPOT, ASGProvider를 포함한 클러스터 인프라를 탐색함.  

- Registered EC2 instances as container instances in the ECS cluster, ready to launch tasks.  
- EC2 인스턴스를 ECS 클러스터의 컨테이너 인스턴스로 등록하여 태스크 실행 준비 완료.  
