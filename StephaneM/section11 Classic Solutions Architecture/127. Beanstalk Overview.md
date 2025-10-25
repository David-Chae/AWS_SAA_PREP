# Beanstalk Overview  
# Beanstalk 개요  
👉 설명: 이 섹션에서는 AWS Elastic Beanstalk 서비스의 개념과 동작 방식을 소개한다.  

---

## Introduction to Elastic Beanstalk  
## Elastic Beanstalk 소개  
👉 설명: Elastic Beanstalk은 애플리케이션 배포를 단순화하는 AWS 관리형 서비스다.  

So far in this course, when deploying an application, we have used the same architecture.  
지금까지 이 강의에서는 애플리케이션을 배포할 때 동일한 아키텍처를 사용했다.  
👉 설명: 즉, 로드 밸런서, 오토 스케일링 그룹, EC2, 데이터베이스 등을 결합한 일반적인 구조다.  

This architecture includes a load balancer that receives all requests from users, an auto scaling group spanning multiple availability zones, with EC2 instances deployed in each zone.  
이 아키텍처는 사용자 요청을 받는 로드 밸런서, 여러 가용 영역에 걸친 오토 스케일링 그룹, 각 영역에 배포된 EC2 인스턴스로 구성된다.  
👉 설명: 확장성과 가용성을 높이기 위한 표준적인 AWS 배포 구조.  

In the backend, there may be data subnets hosting an RDS database for reads and writes, possibly with replicas.  
백엔드에는 읽기와 쓰기를 담당하는 RDS 데이터베이스가 데이터 서브넷에 호스팅될 수 있으며, 복제본도 포함될 수 있다.  
👉 설명: DB는 고가용성과 읽기 성능 향상을 위해 리드 리플리카를 둘 수 있다.  

For caching, ElastiCache is used.  
캐싱을 위해서는 ElastiCache를 사용한다.  
👉 설명: 성능 향상을 위해 메모리 기반 캐시를 적용.  

---

If there are many applications to deploy following this architecture, recreating it each time can be cumbersome.  
이 아키텍처로 여러 애플리케이션을 배포해야 한다면, 매번 재구성하는 것은 번거롭다.  
👉 설명: 반복적인 인프라 작업은 개발자 생산성을 떨어뜨린다.  

As developers, managing infrastructure and deploying code can be complicated.  
개발자 입장에서 인프라 관리와 코드 배포는 복잡하다.  
👉 설명: 코드 작성 이외의 작업 부담이 크다.  

We do not want to configure databases, load balancers, and other components repeatedly. Moreover, we want everything to scale automatically.  
데이터베이스, 로드 밸런서 등 구성 요소를 반복적으로 설정하기 싫고, 모든 것이 자동으로 확장되기를 원한다.  
👉 설명: 자동화와 관리형 서비스 필요성이 등장.  

---

Most web applications share this architecture with a load balancer and an auto scaling group.  
대부분의 웹 애플리케이션은 로드 밸런서와 오토 스케일링 그룹을 포함한 이 아키텍처를 공유한다.  
👉 설명: 표준 웹 아키텍처.  

As a developer, the primary concern is to have the code run without worrying about the underlying infrastructure.  
개발자에게 중요한 것은 인프라를 신경 쓰지 않고 코드가 실행되도록 하는 것이다.  
👉 설명: 핵심은 “코드 실행의 단순화.”  

Additionally, when developing in different programming languages or environments, having a single deployment method is desirable.  
또한 다양한 프로그래밍 언어나 환경에서 개발할 때 단일 배포 방식을 갖는 것이 바람직하다.  
👉 설명: 멀티 플랫폼 지원이 필요하다.  

This is where Elastic Beanstalk comes into play.  
여기서 Elastic Beanstalk이 등장한다.  
👉 설명: Beanstalk이 위 문제를 해결하는 서비스다.  

---

Elastic Beanstalk provides a developer-centric view for deploying applications on AWS.  
Elastic Beanstalk은 AWS에서 애플리케이션을 배포하기 위한 개발자 중심의 뷰를 제공한다.  
👉 설명: 관리형 서비스로서 코드 배포만 신경 쓰면 된다.  

It offers a single interface that reuses components such as EC2, auto scaling groups, load balancers, and RDS, but as a managed service that handles deployment for you.  
EC2, 오토 스케일링 그룹, 로드 밸런서, RDS 등을 재사용하면서, 배포를 대신 처리하는 단일 관리형 인터페이스를 제공한다.  
👉 설명: 기존 AWS 리소스를 통합적으로 관리.  

It manages capacity provisioning, load balancer configuration, scaling, application health monitoring, instance configuration, and more.  
용량 프로비저닝, 로드 밸런서 구성, 확장, 애플리케이션 상태 모니터링, 인스턴스 구성 등을 관리한다.  
👉 설명: 운영 작업을 자동화.  

The only responsibility for developers is the application code itself.  
개발자의 유일한 책임은 애플리케이션 코드뿐이다.  
👉 설명: 코드 중심 개발이 가능해진다.  

---

## Components of Elastic Beanstalk  
## Elastic Beanstalk 구성 요소  
👉 설명: Beanstalk을 구성하는 주요 단위들.  

- **Application**: A collection of Beanstalk components including environments, versions, and configurations.  
- **애플리케이션**: 환경, 버전, 설정을 포함한 Beanstalk 구성 요소의 집합.  

- **Application Version**: An iteration of your application code, such as version one, two, three, etc.  
- **애플리케이션 버전**: 애플리케이션 코드의 반복 버전(예: v1, v2, v3 등).  

- **Environment**: A collection of resources running a specific application version. Only one application version runs in an environment at a time, but you can update the environment to a new version.  
- **환경**: 특정 애플리케이션 버전을 실행하는 리소스 모음. 동시에 하나의 버전만 실행되며, 새로운 버전으로 업데이트할 수 있다.  

- **Tiers**: Beanstalk supports two tiers: the web server environment tier and the worker environment tier.  
- **계층**: Beanstalk은 웹 서버 환경 계층과 워커 환경 계층 두 가지를 지원한다.  

- **Multiple Environments**: You can create multiple environments such as development, testing, and production.  
- **다중 환경**: 개발, 테스트, 운영 등 여러 환경을 만들 수 있다.  

---

## Supported Programming Languages  
## 지원 프로그래밍 언어  
👉 설명: Beanstalk이 지원하는 언어 및 플랫폼.  

Go, Java SE, Java with Tomcat, .NET Core on Linux, .NET on Windows Server, Node.js, PHP, Python, Ruby, Packer Builder, Single Docker Container, Multi Docker Container, Pre-configured Docker  
Go, Java SE, Tomcat 기반 Java, 리눅스 .NET Core, Windows Server .NET, Node.js, PHP, Python, Ruby, Packer Builder, 단일 도커, 다중 도커, 사전 구성된 도커  
👉 설명: 사실상 대부분의 인기 있는 언어를 지원한다.  

---

## Environment Tiers: Web Server and Worker  
## 환경 계층: 웹 서버와 워커  
👉 설명: 두 가지 배포 환경.  

- **Web Server Environment**: Traditional architecture with a load balancer sending traffic to multiple EC2 web servers. Handles HTTP requests.  
- **웹 서버 환경**: 로드 밸런서가 여러 EC2 웹 서버로 트래픽을 분산하는 전통적 구조. HTTP 요청 처리에 사용.  

- **Worker Environment**: Uses SQS queue. EC2 workers pull and process messages. Scales with message volume.  
- **워커 환경**: SQS 큐를 사용해 EC2 워커가 메시지를 가져와 처리. 메시지 양에 따라 확장.  

👉 설명: 웹과 백그라운드 작업을 분리하여 효율적 확장 가능.  

---

## Deployment Modes  
## 배포 모드  
👉 설명: 배포 방식은 두 가지.  

- **Single Instance**: For development, runs on one EC2 with Elastic IP, optional RDS. Not highly available.  
- **단일 인스턴스**: 개발용. 하나의 EC2와 Elastic IP, 선택적으로 RDS. 고가용성 아님.  

- **High Availability**: For production. Load balancer + multiple AZ EC2s via ASG + Multi-AZ RDS.  
- **고가용성**: 운영용. 로드 밸런서, 다중 AZ EC2, 오토 스케일링 그룹, 멀티-AZ RDS 포함.  

---

## Key Takeaways  
## 핵심 정리  

- Elastic Beanstalk simplifies deploying web apps by managing infrastructure like EC2, ELB, ASG.  
- Elastic Beanstalk은 EC2, ELB, ASG 같은 인프라를 관리하며 웹 앱 배포를 단순화한다.  

- It provides a developer-centric interface supporting multiple languages and versions.  
- 개발자 중심 인터페이스를 제공하며 다수 언어와 버전을 지원한다.  

- Supports two tiers: web servers for HTTP, workers for background tasks via SQS.  
- 두 가지 계층 지원: HTTP를 위한 웹 서버, SQS 기반 백그라운드 작업을 위한 워커.  

- Deployment modes: single instance for dev, high availability for production.  
- 배포 모드: 개발용 단일 인스턴스, 운영용 고가용성.  

---

👉 게임보상 🎁: **“Elastic Beanstalk 마스터 칭호 획득!”** (AWS 인프라 관리 자동화 + 멀티 언어 배포 경험치 +50)
