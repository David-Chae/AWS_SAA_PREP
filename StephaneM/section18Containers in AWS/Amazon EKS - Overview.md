# Amazon EKS - Overview  
# 아마존 EKS - 개요  
(Amazon EKS: AWS에서 Kubernetes 클러스터를 관리할 수 있는 서비스)

---

## Introduction to Amazon EKS  
## Amazon EKS 소개  
(EKS의 기본 개념과 역할 설명)

Amazon EKS stands for Amazon Elastic Kubernetes Service.  
Amazon EKS는 Amazon Elastic Kubernetes Service의 약자이다.  
(AWS에서 Kubernetes 클러스터를 실행하고 관리하도록 설계된 서비스)

It is a service designed to launch and manage Kubernetes clusters on AWS.  
AWS에서 Kubernetes 클러스터를 시작하고 관리하기 위해 설계된 서비스이다.  
(EKS를 사용하면 AWS 내에서 Kubernetes 환경을 쉽게 구축 가능)

---

## What is Kubernetes?  
## Kubernetes란 무엇인가?  
(컨테이너 오케스트레이션의 핵심 개념 설명)

Kubernetes is an open-source system for automatic deployment, scaling, and management of containerized applications, typically Docker containers.  
Kubernetes는 컨테이너화된 애플리케이션(주로 Docker)을 자동으로 배포, 스케일링, 관리하는 오픈 소스 시스템이다.  
(ECS와 유사하지만 오픈 소스이며 다양한 클라우드 환경에서 사용 가능)

It serves as an alternative to Amazon ECS, which has a similar goal of running containers but uses a very different API.  
컨테이너 실행이라는 목표는 ECS와 비슷하지만, API 설계가 크게 다르기 때문에 ECS의 대안으로 볼 수 있다.  

Unlike ECS, which is not open-source, Kubernetes is open-source and is used by many cloud providers, providing a standardized approach to container orchestration.  
ECS와 달리 Kubernetes는 오픈 소스이며 여러 클라우드 제공자가 사용하여 컨테이너 오케스트레이션의 표준화된 접근 방식을 제공한다.  

---

## EKS Launch Modes  
## EKS 실행 모드  
(EKS에서 클러스터를 배포하는 두 가지 방식)

Amazon EKS supports two launch modes:  
Amazon EKS는 두 가지 실행 모드를 지원한다.  

- EC2 launch mode: Deploy worker nodes as EC2 instances.  
- EC2 실행 모드: 워커 노드를 EC2 인스턴스로 배포  

- Fargate mode: Deploy serverless containers within an EKS cluster.  
- Fargate 모드: 서버리스 컨테이너를 EKS 클러스터 내에서 실행  

---

## Use Cases for Amazon EKS  
## Amazon EKS 사용 사례  
(EKS를 사용하는 기업 환경)

Companies use Amazon EKS when they:  
기업이 Amazon EKS를 사용하는 경우는 다음과 같다.  

- Already use Kubernetes on-premises.  
- 이미 온프레미스에서 Kubernetes를 사용하는 경우  

- Use Kubernetes in another cloud environment.  
- 다른 클라우드 환경에서 Kubernetes를 사용하는 경우  

- Want to use the Kubernetes API while leveraging AWS to manage the Kubernetes cluster.  
- Kubernetes API를 사용하면서 AWS가 클러스터 관리를 담당하도록 하고 싶은 경우  

Kubernetes is cloud-agnostic and can be used across various clouds such as Azure and Google Cloud.  
Kubernetes는 클라우드에 종속되지 않으며, Azure, Google Cloud 등 다양한 클라우드에서 사용 가능하다.  

This makes migrating containers between clouds simpler when using Amazon EKS.  
EKS를 사용하면 클라우드 간 컨테이너 마이그레이션이 더 쉬워진다.  

---

## Amazon EKS Architecture  
## Amazon EKS 아키텍처  
(EKS 클러스터 구성과 구조)

An Amazon EKS cluster typically resides within a VPC that spans three Availability Zones, divided into public and private subnets.  
EKS 클러스터는 일반적으로 3개 가용 영역에 걸친 VPC 내에 존재하며, 퍼블릭 및 프라이빗 서브넷으로 나뉜다.  

Within this setup, EKS Worker Nodes are EC2 instances running EKS Pods.  
이 환경에서 EKS 워커 노드는 EKS Pod를 실행하는 EC2 인스턴스이다.  

Pods are the Kubernetes equivalent of ECS tasks.  
Pod는 ECS 태스크에 해당하는 Kubernetes 개념이다.  

These nodes can be managed by an Auto Scaling group.  
이 노드들은 오토스케일링 그룹으로 관리할 수 있다.  

To expose services running on EKS, you can configure private or public load balancers, similar to ECS, to route traffic appropriately.  
EKS에서 실행되는 서비스를 외부에 노출하려면, ECS처럼 퍼블릭 또는 프라이빗 로드 밸런서를 구성해 트래픽을 라우팅할 수 있다.  

---

## Node Types in Amazon EKS  
## Amazon EKS 노드 유형  
(EKS에서 지원하는 워커 노드 유형)

Amazon EKS supports three main node types:  
EKS는 세 가지 주요 노드 유형을 지원한다.  

- Managed Node Groups: AWS creates and manages EC2 instances for you as part of an Auto Scaling group. Supports both On-Demand and Spot Instances.  
- 관리형 노드 그룹: AWS가 오토스케일링 그룹의 일부로 EC2 인스턴스를 생성하고 관리. 온디맨드와 스팟 인스턴스 지원  

- Self-Managed Nodes: You create and manage your own nodes, registering them with the EKS cluster. You can use the Amazon EKS Optimized AMI or build your own. Supports On-Demand and Spot Instances.  
- 자체 관리 노드: 사용자가 직접 노드를 생성하고 EKS 클러스터에 등록. EKS 최적화 AMI 사용 가능, 온디맨드 및 스팟 지원  

- Fargate Mode: Serverless mode where no nodes are visible or managed; you simply run containers on EKS without maintenance overhead.  
- Fargate 모드: 서버리스 모드로, 노드가 보이지 않고 관리할 필요 없음. 단순히 컨테이너 실행 가능  

---

## Storage Integration with Amazon EKS  
## Amazon EKS 스토리지 통합  
(EKS 클러스터에 데이터 볼륨 연결)

You can attach data volumes to your Amazon EKS cluster by specifying a StorageClass manifest.  
StorageClass 매니페스트를 지정하여 EKS 클러스터에 데이터 볼륨을 연결할 수 있다.  

This leverages the Container Storage Interface (CSI) compliant driver.  
이는 CSI(Container Storage Interface) 호환 드라이버를 사용한다.  

Supported storage options include:  
지원되는 스토리지 옵션은 다음과 같다.  

- Amazon Elastic Block Store (EBS)  
- Amazon Elastic Block Store (EBS)  

- Amazon Elastic File System (EFS) — the only storage class supported with Fargate  
- Amazon Elastic File System (EFS) — Fargate에서 지원되는 유일한 스토리지 클래스  

- Amazon FSx for Lustre  
- Amazon FSx for Lustre  

- Amazon FSx for NetApp ONTAP  
- Amazon FSx for NetApp ONTAP  

This concludes the overview of Amazon EKS.  
이로써 Amazon EKS 개요를 마친다.  

It provides a flexible, standardized, and managed Kubernetes service on AWS, supporting various deployment and storage options.  
AWS에서 유연하고 표준화된 관리형 Kubernetes 서비스를 제공하며, 다양한 배포 및 스토리지 옵션을 지원한다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon EKS is a managed Kubernetes service on AWS that supports both EC2 and Fargate launch modes.  
- Amazon EKS는 AWS에서 관리되는 Kubernetes 서비스로, EC2 및 Fargate 실행 모드를 지원  

- Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.  
- Kubernetes는 컨테이너화된 애플리케이션 배포, 스케일링, 관리를 자동화하는 오픈 소스 시스템  

- EKS supports managed node groups, self-managed nodes, and serverless Fargate mode for running containers.  
- EKS는 관리형 노드 그룹, 자체 관리 노드, 서버리스 Fargate 모드를 지원  

- Storage integration in EKS uses the Container Storage Interface (CSI) with support for Amazon EBS, EFS, FSx for Lustre, and FSx for NetApp ONTAP.  
- EKS의 스토리지 통합은 CSI를 사용하며, Amazon EBS, EFS, FSx for Lustre, FSx for NetApp ONTAP을 지원


---

🎮 **보상 지급!**

* EKS 노트 퀘스트 완료! 🏗️
* **+160 XP**
* 아이템 획득: **\[K8s Compass 🧭]** (Kubernetes 구조를 이해한 자에게 주어지는 아이템)
