# Amazon ECS
# 아마존 ECS

## Introduction to Amazon ECS
## Amazon ECS 소개

Amazon ECS stands for Elastic Container Service.  
Amazon ECS는 Elastic Container Service(탄력적 컨테이너 서비스)의 약자입니다.  

When launching Docker containers on AWS, you are launching what is called an ECS Task on an ECS Cluster.  
AWS에서 Docker 컨테이너를 실행할 때, 이는 ECS 클러스터 내의 ECS 태스크(Task)를 실행하는 것입니다.  

An ECS Cluster is composed of multiple components depending on the launch type used.  
ECS 클러스터는 사용하는 실행 유형(런치 타입)에 따라 여러 구성 요소로 이루어집니다.  

---

## EC2 Launch Type
## EC2 실행 유형

With the EC2 Launch Type, the ECS Cluster is composed of EC2 instances.  
EC2 실행 유형에서는 ECS 클러스터가 EC2 인스턴스로 구성됩니다.  

In this case, you must provision and maintain the infrastructure yourself.  
이 경우, 인프라를 직접 프로비저닝하고 유지 관리해야 합니다.  

Each EC2 instance runs the ECS Agent, which registers the instance into the Amazon ECS service and the specified ECS Cluster.  
각 EC2 인스턴스는 ECS 에이전트를 실행하며, 이를 통해 인스턴스가 Amazon ECS 서비스 및 지정된 ECS 클러스터에 등록됩니다.  

Once this setup is in place, starting or stopping ECS tasks results in AWS managing the placement of Docker containers on the EC2 instances automatically.  
이 설정이 완료되면, ECS 태스크를 시작하거나 중지할 때 AWS가 자동으로 Docker 컨테이너를 EC2 인스턴스에 배치합니다.  

Docker containers are placed on Amazon EC2 instances that you provision in advance.  
Docker 컨테이너는 사용자가 미리 프로비저닝한 EC2 인스턴스에 배치됩니다.  

---

## Fargate Launch Type
## Fargate 실행 유형

The Fargate Launch Type also runs Docker containers on AWS, but you do not provision the infrastructure.  
Fargate 실행 유형 또한 AWS에서 Docker 컨테이너를 실행하지만, 인프라를 직접 프로비저닝할 필요가 없습니다.  

There are no EC2 instances to manage; it is serverless.  
EC2 인스턴스를 관리할 필요가 없으며, 서버리스 방식입니다.  

Although servers exist behind the scenes, you do not manage them.  
물론 내부적으로 서버가 존재하지만, 사용자가 이를 관리하지 않습니다.  

In this type, you create task definitions to define ECS tasks, and AWS runs these tasks based on the CPU and RAM requirements you specify.  
이 방식에서는 태스크 정의(Task Definition)를 작성하여 ECS 태스크를 정의하며, AWS가 지정된 CPU와 RAM 요구사항에 따라 태스크를 실행합니다.  

When running a new Docker container, it is launched without you knowing where it runs and without any EC2 instance being created in your account.  
새 Docker 컨테이너를 실행할 때, 어디서 실행되는지 알 필요도 없으며 계정 내에 EC2 인스턴스가 생성되지도 않습니다.  

To scale, you simply increase the number of tasks without managing EC2 instances.  
확장이 필요하다면 EC2 인스턴스를 관리하지 않고 단순히 태스크 개수만 늘리면 됩니다.  

Fargate is preferred for its serverless nature and ease of management compared to the EC2 Launch Type.  
Fargate는 서버리스 특성과 관리의 편의성 덕분에 EC2 실행 유형보다 선호됩니다.  

---

## IAM Roles for ECS Tasks
## ECS 태스크를 위한 IAM 역할

### EC2 Launch Type
### EC2 실행 유형

In the EC2 Launch Type, the EC2 instances running the ECS Agent use an EC2 Instance Profile.  
EC2 실행 유형에서는 ECS 에이전트를 실행하는 EC2 인스턴스가 EC2 인스턴스 프로파일을 사용합니다.  

This profile allows the ECS Agent to make API calls to the ECS service, CloudWatch Logs for sending container logs, ECR for pulling Docker images, and to reference sensitive data in Secrets Manager or the SSM Parameter Store.  
이 프로파일은 ECS 에이전트가 ECS 서비스에 API 호출을 하거나, CloudWatch Logs로 로그를 전송하거나, ECR에서 Docker 이미지를 가져오거나, Secrets Manager 또는 SSM 파라미터 스토어에서 민감한 데이터를 참조할 수 있도록 허용합니다.  

---

### ECS Task Roles
### ECS 태스크 역할

ECS tasks themselves receive ECS Task Roles, which are applicable to both EC2 Launch Type and Fargate.  
ECS 태스크는 자체적으로 ECS 태스크 역할(Task Role)을 받으며, 이는 EC2 실행 유형과 Fargate 모두에 적용됩니다.  

You can create specific roles per task.  
태스크마다 특정 역할을 따로 만들 수 있습니다.  

For example, Task A may have an ECS Task A Role allowing API calls against Amazon S3, while Task B may have a Task B Role allowing API calls against DynamoDB.  
예를 들어, 태스크 A는 Amazon S3에 API 호출을 허용하는 역할을, 태스크 B는 DynamoDB에 API 호출을 허용하는 역할을 가질 수 있습니다.  

The Task Role is defined in the task definition of your ECS service.  
태스크 역할은 ECS 서비스의 태스크 정의에서 정의됩니다.  

It is important to distinguish between the EC2 Instance Profile Role used by ECS Agents and the ECS Task Role used by ECS tasks.  
ECS 에이전트가 사용하는 EC2 인스턴스 프로파일 역할과 ECS 태스크가 사용하는 태스크 역할을 구분하는 것이 중요합니다.  

---

## Load Balancer Integrations
## 로드 밸런서 통합

Whether using the EC2 Launch Type or Fargate, you can run multiple ECS tasks within an ECS Cluster and expose these tasks as HTTP or HTTPS endpoints.  
EC2 실행 유형이든 Fargate든, 하나의 ECS 클러스터 내에서 여러 ECS 태스크를 실행하고 이를 HTTP/HTTPS 엔드포인트로 노출할 수 있습니다.  

An Application Load Balancer (ALB) can be placed in front of the ECS tasks, routing user traffic to the tasks directly.  
Application Load Balancer(ALB)를 ECS 태스크 앞에 두어 사용자 트래픽을 태스크로 직접 라우팅할 수 있습니다.  

The ALB supports most use cases and is a good choice.  
ALB는 대부분의 사용 사례를 지원하며 좋은 선택입니다.  

A Network Load Balancer (NLB) is recommended only for very high throughput or high performance use cases, or when used with AWS PrivateLink.  
Network Load Balancer(NLB)는 매우 높은 처리량이나 성능이 필요한 경우, 또는 AWS PrivateLink와 함께 사용할 때 권장됩니다.  

The older Classic Load Balancer can be used but is not recommended because it lacks advanced features and cannot be linked to Fargate.  
구형 Classic Load Balancer도 사용할 수 있으나, 고급 기능이 부족하고 Fargate와 연동되지 않기 때문에 권장되지 않습니다.  

The Application Load Balancer works with both EC2 and Fargate launch types.  
Application Load Balancer는 EC2와 Fargate 실행 유형 모두와 호환됩니다.  

---

## Data Persistence on Amazon ECS
## Amazon ECS에서의 데이터 지속성

To achieve data persistence on Amazon ECS, you need data volumes.  
Amazon ECS에서 데이터 지속성을 확보하려면 데이터 볼륨이 필요합니다.  

One notable option is Amazon Elastic File System (EFS).  
대표적인 옵션은 Amazon Elastic File System(EFS)입니다.  

Both EC2 instances and Fargate launch types can mount an Amazon EFS file system onto ECS tasks.  
EC2 인스턴스와 Fargate 실행 유형 모두 ECS 태스크에 Amazon EFS 파일 시스템을 마운트할 수 있습니다.  

EFS is a network file system compatible with both launch types.  
EFS는 두 실행 유형 모두와 호환되는 네트워크 파일 시스템입니다.  

Mounting an EFS file system allows tasks running in any Availability Zone linked to the file system to share the same data and communicate via the file system if needed.  
EFS 파일 시스템을 마운트하면 연결된 가용 영역 내 태스크가 동일한 데이터를 공유하고 필요시 파일 시스템을 통해 통신할 수 있습니다.  

The optimal combination is to use Fargate to launch ECS tasks in a serverless fashion and Amazon EFS for persistent file system storage.  
최적의 조합은 Fargate를 사용해 ECS 태스크를 서버리스 방식으로 실행하고, Amazon EFS를 사용해 지속적인 파일 시스템 스토리지를 제공하는 것입니다.  

EFS is also serverless, pay-as-you-go, and requires no server management.  
EFS 또한 서버리스이며 사용한 만큼만 과금되며, 서버 관리가 필요 없습니다.  

---

## Key Takeaways
## 핵심 요약

Amazon ECS offers two launch types: EC2 Launch Type requiring self-managed infrastructure, and Fargate Launch Type which is serverless.  
Amazon ECS는 두 가지 실행 유형을 제공합니다: 인프라를 직접 관리해야 하는 EC2 실행 유형, 그리고 서버리스인 Fargate 실행 유형입니다.  

ECS tasks run Docker containers on ECS clusters, with EC2 instances running the ECS Agent in the EC2 Launch Type.  
ECS 태스크는 ECS 클러스터에서 Docker 컨테이너를 실행하며, EC2 실행 유형에서는 EC2 인스턴스가 ECS 에이전트를 실행합니다.  

IAM roles differentiate between EC2 Instance Profile Roles for ECS Agents and ECS Task Roles for individual tasks.  
IAM 역할은 ECS 에이전트용 EC2 인스턴스 프로파일 역할과 개별 태스크용 ECS 태스크 역할로 구분됩니다.  

Load balancers like Application Load Balancer integrate with ECS tasks for HTTP/HTTPS endpoints; Network Load Balancer is for high throughput scenarios.  
Application Load Balancer 같은 로드 밸런서는 ECS 태스크와 통합되어 HTTP/HTTPS 엔드포인트를 제공하며, Network Load Balancer는 고처리량 시나리오에 적합합니다.  

Amazon EFS provides persistent, shared, multi-AZ storage compatible with both EC2 and Fargate launch types.  
Amazon EFS는 EC2와 Fargate 실행 유형 모두에서 사용 가능한 지속적이고 공유되는 다중 가용 영역 스토리지를 제공합니다.  
