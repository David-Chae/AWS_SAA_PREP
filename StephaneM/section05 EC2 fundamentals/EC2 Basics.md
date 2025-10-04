# EC2 Basics  
# EC2 기초  
👉 EC2에 대한 기초 개념을 배우는 섹션입니다.  

---

In this section on EC2, we will create our first website on AWS.  
이번 EC2 섹션에서는 AWS에서 우리의 첫 번째 웹사이트를 만들어보겠습니다.  
➡️ 실습을 통해 EC2로 웹사이트를 배포하는 과정을 학습합니다.  

---

## What is Amazon EC2?  
## 아마존 EC2란 무엇인가?  

So what is Amazon EC2? EC2 is one of the most popular AWS offerings. It is used widely. It stands for Elastic Compute Cloud. This is the way to do infrastructure as a service on AWS.  
그렇다면 Amazon EC2란 무엇일까요? EC2는 AWS에서 가장 인기 있는 서비스 중 하나입니다. "Elastic Compute Cloud"의 약자이며, 광범위하게 사용됩니다. AWS에서 인프라를 서비스(IaaS) 형태로 제공하는 방식입니다.  
➡️ EC2는 클라우드에서 가상 서버를 임대해 사용하는 핵심 서비스입니다.  

---

## EC2 Components at a High Level  
## EC2의 주요 구성 요소  

EC2 is not just one service; it is composed of many parts at a high level. You can rent virtual machines on EC2 called EC2 instances. You can store data on virtual drives or EBS volumes. You can distribute load across machines using an Elastic Load Balancer. You can scale services using an Auto Scaling Group (ASG). We will see these components in depth during this course.  
EC2는 단일 서비스가 아니라 여러 부분으로 구성됩니다. 가상 머신(EC2 인스턴스)을 임대할 수 있고, EBS 볼륨에 데이터를 저장할 수 있습니다. Elastic Load Balancer로 트래픽을 분산할 수 있으며, Auto Scaling Group으로 서비스 규모를 확장할 수 있습니다. 이번 강의에서 이러한 구성 요소를 깊이 다뤄보겠습니다.  
➡️ EC2는 인스턴스, 스토리지, 로드 밸런서, 오토 스케일링 그룹으로 이루어진 종합적인 인프라 서비스입니다.  

---

## Why EC2 Matters  
## 왜 EC2가 중요한가?  

Knowing how to use EC2 in AWS is fundamental to understanding how the cloud works. The cloud is about renting compute resources whenever you need them on demand, and EC2 is exactly that.  
AWS에서 EC2를 다루는 것은 클라우드를 이해하는 데 필수적입니다. 클라우드의 핵심은 필요할 때마다 컴퓨팅 자원을 임대하는 것이며, EC2는 이를 가능하게 합니다.  
➡️ EC2를 이해하면 클라우드 개념의 기본을 이해할 수 있습니다.  

---

## Choosing Instance Options  
## 인스턴스 옵션 선택하기  

So EC2, what can we choose for our instances, our virtual servers that we rent from AWS? You must choose the operating system for your EC2 instances. There are three main options: Linux (the most popular), Windows, or even macOS.  
EC2 인스턴스를 만들 때는 운영체제를 선택해야 합니다. 일반적으로 Linux(가장 인기 있음), Windows, macOS 세 가지가 주요 옵션입니다.  
➡️ OS 선택은 인스턴스 사용 목적에 따라 달라집니다.  

---

## Compute, Memory and Storage  
## 컴퓨팅, 메모리, 스토리지 선택  

You must also decide how much compute power and how many cores you want on the virtual machine (how much CPU). Then choose how much random access memory (RAM) you want and how much storage space. For storage, you can attach storage through the network using EBS or EFS, or you can have hardware-attached storage using an EC2 instance store. We have a whole section on storage that will cover this in more detail.  
가상 머신에서 사용할 CPU 코어 수, RAM 크기, 스토리지 공간도 결정해야 합니다. 스토리지는 EBS나 EFS 같은 네트워크 연결 방식 또는 EC2 인스턴스 스토어 같은 물리적 연결 방식을 사용할 수 있습니다. 스토리지는 별도의 섹션에서 자세히 다룹니다.  
➡️ 인스턴스 성능은 CPU, RAM, 스토리지 방식에 따라 결정됩니다.  

---

## Network and Security Settings  
## 네트워크 및 보안 설정  

Finally, you choose the type of network to attach to your EC2 instance: what network card performance you want, what kind of public IP you need, and how to handle firewall rules. Firewall rules are managed with security groups and related settings.  
마지막으로 EC2 인스턴스에 연결할 네트워크 유형을 선택해야 합니다. 네트워크 카드 성능, 공인 IP 여부, 방화벽 규칙 등을 설정합니다. 방화벽 규칙은 보안 그룹을 통해 관리됩니다.  
➡️ 네트워크와 보안 그룹 설정은 인스턴스 접근 제어의 핵심입니다.  

---

## Bootstrapping with EC2 User Data  
## EC2 User Data를 이용한 부트스트래핑  

There is also a bootstrap script to configure the instance at first launch called EC2 user data. We have many options when launching instances, and as you will see in the hands-on labs and at other certification levels, there are even more options to learn about.  
EC2에는 처음 실행 시 인스턴스를 자동으로 설정하는 부트스트랩 스크립트(User Data)가 있습니다. 인스턴스 실행 시 다양한 옵션이 있으며, 실습과 심화 과정에서 더 배울 수 있습니다.  
➡️ User Data는 인스턴스 초기 설정 자동화를 지원합니다.  

---

## What Bootstrapping Means  
## 부트스트래핑의 의미  

Bootstrapping means launching commands when the machine starts. The user data script runs only once at first start and then will not run again. The specific purpose of EC2 user data is to automate boot tasks, hence the name bootstrapping.  
부트스트래핑이란, 머신이 시작될 때 명령어를 실행하는 것을 말합니다. User Data 스크립트는 최초 실행 시 한 번만 동작하며 다시 실행되지 않습니다. EC2 User Data의 목적은 부팅 작업을 자동화하는 것입니다.  
➡️ 인스턴스 실행 시 자동 초기화 과정을 수행하는 것이 부트스트래핑입니다.  

---

## Common Tasks in User Data  
## User Data로 자동화하는 작업들  

Typical tasks you automate with user data include installing updates, installing software, and downloading common files from the internet. In fact, you can run any commands you need at boot time. Be aware: the more you add into your user data script, the more work your instance must perform at boot time.  
User Data에서 자동화할 수 있는 작업에는 업데이트 설치, 소프트웨어 설치, 인터넷에서 파일 다운로드 등이 있습니다. 사실상 부팅 시 필요한 어떤 명령어든 실행할 수 있습니다. 단, 스크립트가 많아질수록 인스턴스 부팅 시간이 길어집니다.  
➡️ User Data는 인스턴스 환경 세팅 자동화에 유용하지만, 부하를 고려해야 합니다.  

---

## Permissions and Final Notes  
## 권한 및 마무리  

The EC2 user data script runs as the root user, so any command in the script has sudo rights. This was a short introduction to EC2. Do not worry — it will get very practical very soon. I will see you in the next lecture.  
EC2 User Data 스크립트는 root 권한으로 실행되므로 모든 명령은 sudo 권한을 가집니다. 이번 강의에서는 EC2에 대한 간단한 소개를 했습니다. 곧 실습에서 구체적인 내용을 다룰 예정입니다.  
➡️ User Data 실행 시 root 권한으로 작업하므로 강력한 자동화가 가능합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon EC2 stands for Elastic Compute Cloud and provides infrastructure as a service on AWS.  
- Amazon EC2는 Elastic Compute Cloud의 약자로, AWS에서 인프라를 서비스 형태로 제공합니다.  

- EC2 includes instances, EBS volumes, load balancers, and auto scaling groups among other components.  
- EC2는 인스턴스, EBS 볼륨, 로드 밸런서, 오토 스케일링 그룹 등으로 구성됩니다.  

- When launching an instance you choose the operating system, CPU, memory, storage type, and network settings.  
- 인스턴스를 시작할 때 운영체제, CPU, 메모리, 스토리지 유형, 네트워크 설정을 선택합니다.  

- EC2 user data (bootstrapping) runs once at first launch as root to automate tasks such as updates and software installation.  
- EC2 User Data(부트스트래핑)는 인스턴스 최초 실행 시 root 권한으로 업데이트, 소프트웨어 설치 등의 작업을 자동화합니다.  
