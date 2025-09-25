# AMI Overview  
# AMI 개요  
👉 이번 강의에서는 EC2 인스턴스를 구동하는 핵심인 AMI에 대해 다룹니다.  

---

## Introduction to AMIs  
## AMI 소개  

Now let's talk about what powers our EC2 instances, which is an AMI.  
이제 EC2 인스턴스를 구동하는 핵심 요소인 AMI에 대해 이야기해보겠습니다.  

AMI stands for Amazon Machine Image, and it represents a customization of an EC2 instance.  
AMI는 Amazon Machine Image의 약자로, EC2 인스턴스의 맞춤화된 이미지를 의미합니다.  

You can use AMIs created by AWS or customize your own.  
AWS에서 제공하는 AMI를 사용하거나 직접 커스터마이즈한 AMI를 만들 수 있습니다.  

What is in an AMI? It includes your own software configuration, the operating system setup, and any monitoring tools you want to install.  
AMI에는 소프트웨어 구성, 운영체제 설정, 설치하고 싶은 모니터링 도구 등이 포함됩니다.  

If you create your own AMI, you will benefit from faster boot time and configuration time because all the software you want to install on your EC2 instance is prepackaged through the AMI.  
직접 AMI를 만들면, EC2 인스턴스 부팅과 구성 시간이 빨라집니다. 왜냐하면 필요한 소프트웨어가 이미 AMI 안에 패키징되어 있기 때문입니다.  

You need to build your own AMIs, which can be created for a specific region.  
자신만의 AMI를 만들 수 있으며, 특정 리전에서 생성 가능합니다.  

Then, they can be copied across regions if you want to leverage the AWS global infrastructure.  
그 후, AWS 글로벌 인프라를 활용하고 싶다면 다른 리전으로 복사할 수 있습니다.  

We can launch EC2 instances from different kinds of AMIs.  
다양한 종류의 AMI로부터 EC2 인스턴스를 실행할 수 있습니다.  

So far in this course, we have been using public AMIs provided by AWS.  
지금까지는 AWS가 제공하는 퍼블릭 AM이를 사용했습니다.  

For example, the Amazon Linux 2 AMI is a very popular AMI provided by AWS themselves.  
예를 들어 Amazon Linux 2 AMI는 AWS가 제공하는 매우 인기 있는 AMI입니다.  

However, you can create your own AMI, which means you have to make and maintain them yourself.  
하지만 직접 AMI를 만들 수도 있으며, 이 경우 직접 생성하고 관리해야 합니다.  

There are tools to automate this, but it is a task you must perform as a cloud user.  
자동화 도구가 있긴 하지만, 클라우드 사용자로서 직접 수행해야 하는 작업입니다.  

Finally, you can launch an EC2 instance from an AWS Marketplace AMI.  
마지막으로, AWS Marketplace AMI를 통해 EC2 인스턴스를 실행할 수도 있습니다.  

This is an AMI made by someone else and potentially sold by them.  
이 AMI는 다른 사람이 만들고 판매할 수도 있는 AMI입니다.  

It is common for vendors on AWS to create their own AMIs or software with nice configurations and sell them through the marketplace.  
AWS 벤더들은 자신만의 AMI나 소프트웨어를 만들어 좋은 설정으로 판매하는 것이 일반적입니다.  

Even you, as a user, could create a business selling AMIs on the AWS Marketplace.  
사용자도 AWS Marketplace에서 AMI를 판매하는 사업을 할 수 있습니다.  

This is something some businesses do.  
실제로 일부 기업들이 이런 비즈니스를 운영합니다.  

---

## AMI Creation Process  
## AMI 생성 과정  

How does the AMI process work from an EC2 instance?  
EC2 인스턴스로부터 AMI를 생성하는 과정은 어떻게 될까요?  

First, we start an EC2 instance and customize it.  
먼저 EC2 인스턴스를 시작하고 원하는 설정으로 커스터마이즈합니다.  

Then, we stop the instance to ensure data integrity is correct.  
그 후 데이터 무결성을 위해 인스턴스를 중지합니다.  

Next, we build an AMI from the instance.  
다음으로 인스턴스에서 AMI를 생성합니다.  

This process also creates EBS snapshots behind the scenes.  
이 과정에서 EBS 스냅샷도 자동으로 생성됩니다.  

Finally, we can launch instances from other AMIs.  
마지막으로 다른 AMI로부터 인스턴스를 실행할 수 있습니다.  

For example, we can launch an instance in US-EAST-1A, customize it, and create an AMI from it.  
예를 들어, US-EAST-1A에서 인스턴스를 시작하고 커스터마이즈 후, 여기서 AMI를 생성할 수 있습니다.  

This will be our custom AMI.  
이것이 우리가 만든 커스텀 AMI입니다.  

Then, in US-EAST-1B, we can launch an instance from that AMI, effectively creating a copy of our EC2 instance in a different availability zone.  
그 후, US-EAST-1B에서 해당 AMI로 인스턴스를 실행하면, 다른 AZ에서 EC2 인스턴스 복사본이 생성됩니다.  

I hope you are excited, and I will see you in the next lecture.  
흥미롭게 느끼셨길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- An AMI (Amazon Machine Image) customizes EC2 instances with preconfigured software and operating systems.  
- AMI는 사전 설정된 소프트웨어와 운영체제를 포함해 EC2 인스턴스를 맞춤화합니다.  

- Creating your own AMI results in faster boot and configuration times for EC2 instances.  
- 자체 AMI를 만들면 EC2 부팅과 구성 시간이 빨라집니다.  

- AMIs can be region-specific but can be copied across AWS regions to leverage global infrastructure.  
- AMI는 리전별 생성이 가능하지만, 글로벌 인프라 활용을 위해 다른 리전으로 복사할 수 있습니다.  

- AWS Marketplace offers AMIs created and sold by third parties, enabling users to save time or even sell their own AMIs.  
- AWS Marketplace에서는 제3자가 만든 AMI를 제공하며, 사용자는 시간을 절약하거나 자신의 AMI를 판매할 수도 있습니다.  
