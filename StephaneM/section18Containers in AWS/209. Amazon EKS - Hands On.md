# Amazon EKS - Hands On  
# Amazon EKS - 실습  
(Amazon EKS 클러스터를 실제로 생성하고 구성하는 과정)

---

## In this hands-on session, we will explore Amazon EKS, the Kubernetes service from AWS.  
## 이번 실습에서는 AWS의 Kubernetes 서비스인 Amazon EKS를 살펴본다.  
(EKS 클러스터 생성과 설정 과정을 직접 확인)

Please note that this demonstration is outside the free tier and may incur costs.  
이 실습은 프리 티어에 포함되지 않아 비용이 발생할 수 있다는 점에 유의해야 한다.  

It is recommended to watch and understand the process rather than perform it yourself unless necessary.  
꼭 필요한 경우가 아니면 직접 따라 하기보다는 과정을 보고 이해하는 것을 권장한다.  

---

## Creating a New EKS Cluster  
## 새로운 EKS 클러스터 생성  

We will start by creating a new cluster on AWS.  
AWS에서 새로운 클러스터를 생성하는 것으로 시작한다.  

For this demonstration, the cluster will be named demo EKS.  
이번 실습에서 클러스터 이름은 **demo EKS**로 한다.  

We can select the Kubernetes version, and the default version will be used here.  
Kubernetes 버전을 선택할 수 있으며, 기본값을 사용한다.  

Next, a service role is required to manage the cluster resources.  
클러스터 리소스를 관리하기 위해 서비스 역할(Service Role)이 필요하다.  

---

## Creating the IAM Role for EKS Cluster  
## EKS 클러스터용 IAM 역할 생성  

Go to IAM Roles and click "Create Role".  
IAM 역할 콘솔로 가서 **Create Role**을 클릭한다.  

Select "AWS Service" and choose "EKS".  
"AWS Service"를 선택하고 "EKS"를 고른다.  

Select the EKS Cluster use case.  
EKS 클러스터 사용 사례를 선택한다.  

Proceed to permissions and attach the AmazonEKSClusterPolicy.  
권한 단계에서 **AmazonEKSClusterPolicy**를 연결한다.  

Name the role EKSClusterRole (ensure no leading spaces).  
역할 이름을 **EKSClusterRole**로 지정한다. (앞에 공백 없어야 함)  

Create the role and refresh the IAM roles list to confirm creation.  
역할을 생성하고 IAM 역할 목록을 새로고침해 생성 여부를 확인한다.  

---

## Cluster Configuration  
## 클러스터 설정  

Next, decide whether to encrypt secrets with AWS KMS.  
다음으로 AWS KMS를 사용해 시크릿을 암호화할지 여부를 결정한다.  

For this demonstration, encryption will not be enabled, but it is an option for enhanced security.  
이번 실습에서는 암호화를 사용하지 않지만, 보안 강화를 위해 선택 가능하다.  

Then, select the deployment location for the cluster.  
그다음 클러스터 배포 위치를 선택한다.  

Choose a VPC and subnets to ensure high availability.  
고가용성을 위해 VPC와 서브넷을 선택한다.  

Select the appropriate security groups, such as the default security group.  
기본 보안 그룹 같은 적절한 보안 그룹을 선택한다.  

Choose IPv4 for the cluster's network type.  
클러스터 네트워크 유형으로 IPv4를 선택한다.  

Set the cluster endpoint access to public to allow access from your computer.  
클러스터 엔드포인트 접근을 퍼블릭으로 설정해 로컬 컴퓨터에서 접근 가능하게 한다.  

For networking add-ons, select the default options for proxy and DNS.  
네트워크 애드온은 프록시와 DNS의 기본 옵션을 선택한다.  

---

## Review and Create Cluster  
## 검토 후 클러스터 생성  

Review the configured settings including security groups, networking, and public API access.  
보안 그룹, 네트워크, 퍼블릭 API 접근 등 설정을 검토한다.  

Once confirmed, create the cluster.  
확인되면 클러스터를 생성한다.  

This process will provision the cluster itself, after which compute capacity needs to be added by creating managed node groups or Fargate profiles.  
클러스터가 생성된 후에는 관리형 노드 그룹 또는 Fargate 프로필을 만들어 컴퓨팅 리소스를 추가해야 한다.  

---

## Managing Kubernetes Resources  
## Kubernetes 리소스 관리  

Within the cluster resources section, Kubernetes-specific resources are managed.  
클러스터 리소스 섹션에서는 Kubernetes 전용 리소스를 관리한다.  

This area is intended for users with Kubernetes expertise.  
이 부분은 Kubernetes에 익숙한 사용자를 대상으로 한다.  

---

## Creating IAM Role for Node Group  
## 노드 그룹용 IAM 역할 생성  

Navigate to the IAM console and create a new role.  
IAM 콘솔에서 새 역할을 생성한다.  

Select EC2 as the service that will use this role.  
이 역할을 사용할 서비스로 **EC2**를 선택한다.  

Attach the AmazonEKSWorkerNodePolicy to allow worker nodes to communicate with the cluster.  
**AmazonEKSWorkerNodePolicy**를 연결해 워커 노드가 클러스터와 통신할 수 있게 한다.  

Also attach the AmazonEC2ContainerRegistryReadOnly policy to allow nodes to pull container images.  
**AmazonEC2ContainerRegistryReadOnly** 정책을 연결해 노드가 컨테이너 이미지를 가져올 수 있게 한다.  

Name the role AmazonEKSNodeRole (ensure no leading spaces).  
역할 이름을 **AmazonEKSNodeRole**로 지정한다. (앞에 공백 없어야 함)  

Create the role and refresh the IAM roles list to confirm creation.  
역할을 생성하고 IAM 목록을 새로고침해 생성 여부를 확인한다.  

---

## Configuring the Node Group  
## 노드 그룹 구성  

When creating the node group:  
노드 그룹을 생성할 때는 다음을 설정한다.  

- Optionally specify a launch template for EC2 instances; this demonstration will leave it unticked.  
- 필요하다면 EC2 인스턴스 런치 템플릿 지정 가능 (실습에서는 생략)  

- Choose the node group type, such as Amazon Linux 2.  
- 노드 그룹 유형(Amazon Linux 2 등) 선택  

- Select instance types, for example, T3 medium or T3 micro.  
- 인스턴스 유형(T3 medium, T3 micro 등) 선택  

- Define disk size and node scaling configuration, including the desired number of nodes.  
- 디스크 크기 및 노드 수(스케일링 설정 포함) 정의  

- Configure node group update settings to specify how many nodes can be updated simultaneously.  
- 동시에 업데이트할 수 있는 노드 수 설정  

- Select subnets for node access.  
- 노드 접근을 위한 서브넷 선택  

After configuration, create the managed node group.  
구성이 완료되면 관리형 노드 그룹을 생성한다.  

This process deploys EC2 instances managed by AWS for the EKS cluster.  
이 과정에서 AWS가 관리하는 EC2 인스턴스가 EKS 클러스터에 배포된다.  

---

## Alternative Compute Option: Fargate Profiles  
## 대체 컴퓨팅 옵션: Fargate 프로필  

Aside from managed node groups, compute capacity can be provisioned using Fargate profiles.  
관리형 노드 그룹 외에도 Fargate 프로필을 사용해 컴퓨팅 리소스를 제공할 수 있다.  

Fargate allows running containers without managing EC2 instances.  
Fargate를 사용하면 EC2 인스턴스를 직접 관리하지 않고도 컨테이너 실행 가능하다.  

To add a Fargate profile, navigate to the compute section and add a target profile.  
Fargate 프로필을 추가하려면 컴퓨트 섹션에서 타깃 프로필을 추가한다.  

This demonstration will not create a Fargate profile but highlights the option available.  
이번 실습에서는 Fargate 프로필을 생성하지 않지만, 사용할 수 있는 옵션임을 강조한다.  

---

## Add-ons for Amazon EKS  
## Amazon EKS 애드온  

Amazon EKS supports add-ons to extend cluster functionality.  
EKS는 클러스터 기능을 확장하기 위해 애드온을 지원한다.  

For example, the Amazon EBS CSI driver can be installed to enable the use of EBS volumes with the cluster.  
예를 들어, Amazon EBS CSI 드라이버를 설치해 클러스터에서 EBS 볼륨을 사용할 수 있다.  

Other add-ons include drivers for EFS and FSx.  
다른 애드온으로는 EFS 및 FSx 드라이버가 있다.  

These add-ons enhance storage capabilities within the Kubernetes environment.  
이 애드온들은 Kubernetes 환경의 스토리지 기능을 확장한다.  

---

## Conclusion and Cleanup  
## 결론 및 정리  

Kubernetes requires specialized knowledge and is complex, often necessitating dedicated courses.  
Kubernetes는 전문 지식이 필요하고 복잡해 별도의 학습 과정이 필요하다.  

This demonstration covered the basic steps to create and configure an Amazon EKS cluster and its compute resources.  
이번 실습에서는 Amazon EKS 클러스터와 컴퓨팅 리소스를 생성하고 구성하는 기본 단계를 다뤘다.  

To conclude, the created cluster will be deleted.  
마지막으로 생성된 클러스터를 삭제한다.  

Before deletion, node groups must be removed; this step is omitted from the video for brevity.  
삭제 전에 노드 그룹을 제거해야 하지만, 실습 영상에서는 생략되었다.  

This concludes the lecture on Amazon EKS hands-on demonstration.  
이것으로 Amazon EKS 실습 강의를 마친다.  

---

## Key Takeaways  
## 핵심 요약  

- Demonstrated how to create an Amazon EKS cluster and configure its settings.  
- Amazon EKS 클러스터를 생성하고 설정하는 방법을 실습  

- Explained the process of creating IAM roles for EKS cluster and node groups.  
- EKS 클러스터 및 노드 그룹용 IAM 역할 생성 과정 설명  

- Showcased options for adding managed node groups and Fargate profiles for compute capacity.  
- 관리형 노드 그룹 및 Fargate 프로필 추가 옵션 시연  

- Highlighted the availability of add-ons such as the Amazon EBS CSI driver for storage integration.  
- Amazon EBS CSI 드라이버 같은 스토리지 통합 애드온 사용 가능성 강조  
```

---

🎮 **보상 지급!**

* EKS Hands-On 퀘스트 완료! 🔧
* **+200 XP**
* 아이템 획득: **\[Cluster Builder Hammer 🔨]** (EKS 클러스터를 직접 세울 수 있는 힘을 상징하는 아이템)
