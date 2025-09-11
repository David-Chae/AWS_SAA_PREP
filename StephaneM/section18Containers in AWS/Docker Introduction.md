# Docker Introduction  
# 도커 소개  

## Introduction to Docker and Containers  
## 도커와 컨테이너 소개  

Docker is a software development platform designed to deploy applications using container technology.  
도커는 컨테이너 기술을 사용하여 애플리케이션을 배포하기 위해 설계된 소프트웨어 개발 플랫폼입니다.  

Containers package applications in a standardized way, allowing them to run consistently on any operating system without compatibility issues.  
컨테이너는 애플리케이션을 표준화된 방식으로 패키징하여, 어떤 운영 체제에서도 호환성 문제 없이 일관되게 실행할 수 있도록 합니다.  

This predictability simplifies maintenance and deployment, supporting any programming language, operating system, or technology.  
이러한 예측 가능성은 유지보수와 배포를 단순화하며, 모든 프로그래밍 언어, 운영체제, 기술을 지원합니다.  

---

## Use Cases for Docker  
## 도커의 사용 사례  

- Microservice architectures  
- 마이크로서비스 아키텍처  

- Migrating applications from on-premises to the cloud  
- 온프레미스에서 클라우드로 애플리케이션 이전  

- Running any containerized applications  
- 컨테이너화된 애플리케이션 실행  

---

## Docker Architecture on an Operating System  
## 운영체제에서의 도커 아키텍처  

Docker runs on a server, such as an EC2 instance or any other server type, where a Docker agent operates.  
도커는 EC2 인스턴스나 다른 서버 유형에서 실행되며, 이 서버에서 도커 에이전트가 동작합니다.  

Multiple Docker containers can be started on this server.  
이 서버에서는 여러 도커 컨테이너를 시작할 수 있습니다.  

For example, one container might run a Java application, while another runs a Node.js application.  
예를 들어, 하나의 컨테이너는 Java 애플리케이션을, 또 다른 컨테이너는 Node.js 애플리케이션을 실행할 수 있습니다.  

Multiple instances of the same application can run simultaneously in separate containers.  
같은 애플리케이션의 여러 인스턴스를 별도의 컨테이너에서 동시에 실행할 수도 있습니다.  

Docker containers can also run databases like MySQL, demonstrating Docker's versatility.  
도커 컨테이너는 MySQL과 같은 데이터베이스도 실행할 수 있어, 도커의 다재다능함을 보여줍니다.  

---

## Docker Images and Repositories  
## 도커 이미지와 저장소  

Docker images are stored in Docker repositories.  
도커 이미지는 도커 저장소에 저장됩니다.  

Common options include:  
일반적인 옵션은 다음과 같습니다:  

- **Docker Hub**: A public repository hosting base images for various technologies and operating systems such as Ubuntu and MySQL.  
- **Docker Hub**: Ubuntu, MySQL 등 다양한 기술과 운영체제의 베이스 이미지를 호스팅하는 공개 저장소  

- **Amazon Elastic Container Registry (ECR)**: A private repository for storing private images, with a public repository option called Amazon ECR Public Gallery.  
- **Amazon Elastic Container Registry (ECR)**: 프라이빗 이미지를 저장하는 개인용 저장소이며, Amazon ECR Public Gallery라는 공개 저장소 옵션도 제공  

---

## Docker vs. Virtual Machines  
## 도커 vs 가상 머신  

Docker is a form of virtualization technology but differs from traditional virtual machines (VMs).  
도커는 가상화 기술의 한 형태이지만, 전통적인 가상 머신(VM)과는 다릅니다.  

In a VM architecture, the infrastructure runs a host operating system, then a hypervisor, followed by guest operating systems and applications.  
VM 아키텍처에서는 인프라가 호스트 운영체제를 실행하고, 그 위에 하이퍼바이저와 게스트 운영체제 및 애플리케이션이 실행됩니다.  

For example, EC2 instances are virtual machines running on a hypervisor, providing isolated environments with separate resources.  
예를 들어, EC2 인스턴스는 하이퍼바이저 위에서 실행되는 가상 머신으로, 분리된 환경과 독립적인 리소스를 제공합니다.  

In contrast, Docker containers share the host operating system and run on top of the Docker Daemon.  
반대로, 도커 컨테이너는 호스트 운영체제를 공유하며 도커 데몬 위에서 실행됩니다.  

This allows many lightweight containers to coexist on a single server, sharing networking and some data.  
이로 인해 여러 가벼운 컨테이너가 하나의 서버에서 공존하며 네트워크와 일부 데이터를 공유할 수 있습니다.  

While Docker containers are less isolated and thus less secure than VMs, they enable higher density and efficiency.  
도커 컨테이너는 VM보다 격리성이 낮아 보안성이 떨어질 수 있지만, 더 높은 밀도와 효율성을 제공합니다.  

---

## Getting Started with Docker  
## 도커 시작하기  

To create a Docker container, you first write a Dockerfile that defines the container's configuration.  
도커 컨테이너를 만들려면 먼저 컨테이너 구성을 정의하는 Dockerfile을 작성해야 합니다.  

This includes specifying a base Docker image and adding necessary files.  
이는 기본 도커 이미지를 지정하고 필요한 파일을 추가하는 과정을 포함합니다.  

Building the Dockerfile produces a Docker image, which can be pushed to a Docker repository such as Docker Hub or Amazon ECR.  
Dockerfile을 빌드하면 도커 이미지가 생성되며, 이를 Docker Hub 또는 Amazon ECR 같은 도커 저장소에 업로드할 수 있습니다.  

Later, you can pull these images from the repository and run them as Docker containers, which execute your application code.  
이후 저장소에서 이미지를 가져와 도커 컨테이너로 실행하여 애플리케이션 코드를 실행할 수 있습니다.  

---

## Docker Container Management on AWS  
## AWS에서의 도커 컨테이너 관리  

Amazon Web Services offers several container management solutions:  
AWS는 여러 컨테이너 관리 솔루션을 제공합니다:  

- **Amazon ECS (Elastic Container Service)**: AWS의 기본 도커 컨테이너 관리 플랫폼  
- **Amazon EKS (Elastic Kubernetes Service)**: 컨테이너 오케스트레이션을 위한 관리형 Kubernetes 서비스  
- **AWS Fargate**: ECS와 EKS 모두에서 작동하는 서버리스 컨테이너 플랫폼으로, 서버를 관리하지 않고 컨테이너 실행 가능  
- **Amazon ECR**: 컨테이너 이미지를 안전하게 저장하는 서비스  

These services provide a comprehensive ecosystem for deploying and managing containerized applications on AWS.  
이러한 서비스들은 AWS에서 컨테이너화된 애플리케이션을 배포하고 관리할 수 있는 포괄적인 생태계를 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Docker is a container technology that packages applications to run consistently across any operating system.  
- 도커는 애플리케이션을 패키징하여 어떤 운영체제에서도 일관되게 실행할 수 있게 하는 컨테이너 기술입니다.  

- Docker containers share the host OS resources, making them lightweight compared to virtual machines.  
- 도커 컨테이너는 호스트 OS 리소스를 공유하여 가상 머신보다 가볍습니다.  

- Docker images are stored in repositories such as Docker Hub and Amazon ECR.  
- 도커 이미지는 Docker Hub 및 Amazon ECR 같은 저장소에 저장됩니다.  

- AWS provides multiple container management services including Amazon ECS, EKS, Fargate, and ECR.  
- AWS는 Amazon ECS, EKS, Fargate, ECR 등 다양한 컨테이너 관리 서비스를 제공합니다.  
