# EBS Overview  
# EBS 개요  
👉 EBS(Elastic Block Store)의 기본 개념과 특징을 설명하는 섹션입니다.  

---

## Introduction to EBS Volumes  
## EBS 볼륨 소개  
👉 EC2 인스턴스에서 사용할 수 있는 다양한 스토리지 옵션 중 EBS를 다루는 부분입니다.  

In this section, we will explore the different storage options available for EC2 instances, focusing primarily on EBS volumes.  
이 섹션에서는 EC2 인스턴스에서 사용할 수 있는 다양한 스토리지 옵션을 탐구하며, 주로 EBS 볼륨에 집중합니다.  
👉 EBS는 EC2에서 가장 기본적이고 중요한 스토리지 서비스이므로 중점적으로 다루고 있습니다.  

EBS stands for Elastic Block Store. It is a network drive that cannot be attached to your instances while they are running.  
EBS는 Elastic Block Store의 약자입니다. 네트워크 드라이브이며, 실행 중인 인스턴스에 물리적으로 직접 연결되지 않습니다.  
👉 물리 디스크가 아니라 네트워크를 통해 연결되는 스토리지라는 점이 핵심입니다.  

Interestingly, we have been using EBS volumes without even realizing it.  
흥미롭게도, 우리는 인지하지 못한 채 이미 EBS 볼륨을 사용하고 있었습니다.  
👉 EC2 인스턴스를 실행할 때 기본적으로 루트 디스크는 EBS를 사용합니다.  

---

## Persistence of EBS  
## EBS의 데이터 지속성  
👉 EBS는 인스턴스의 종료와 무관하게 데이터를 보존할 수 있습니다.  

EBS volumes allow us to persist data even after the instance is terminated.  
EBS 볼륨은 인스턴스가 종료된 후에도 데이터를 지속할 수 있게 합니다.  
👉 데이터를 잃지 않고 재사용할 수 있다는 장점이 있습니다.  

This means we can recreate an instance and mount the same EBS volume from before, retrieving our data.  
즉, 인스턴스를 새로 만들어도 이전에 사용한 EBS 볼륨을 다시 연결하여 데이터를 복원할 수 있습니다.  
👉 서버를 재시작하거나 새로 구성할 때 유용합니다.  

This feature is very helpful for data persistence.  
이 기능은 데이터 영속성 확보에 매우 유용합니다.  

---

## Availability Zone Binding  
## 가용 영역(AZ) 종속성  
👉 EBS 볼륨은 특정 가용 영역에 묶여 있습니다.  

At the Certified Cloud Practitioner level, EBS volumes can only be mounted to one instance at a time.  
클라우드 실무자(CLF-C02) 수준에서는, 하나의 EBS 볼륨은 동시에 하나의 인스턴스에만 연결될 수 있습니다.  

Additionally, when you create an EBS volume, it is bound to a specific availability zone.  
또한, EBS 볼륨을 생성하면 특정 가용 영역(AZ)에 묶이게 됩니다.  

For example, an EBS volume created in us-east-1a cannot be attached to an instance in us-east-1b.  
예를 들어, us-east-1a에서 생성된 EBS 볼륨은 us-east-1b 인스턴스에 연결할 수 없습니다.  

We will illustrate this with a diagram shortly.  
이 부분은 곧 다이어그램으로 설명될 예정입니다.  

---

## EBS as Network USB  
## 네트워크 USB 같은 EBS  
👉 EBS는 일종의 "네트워크 USB"로 비유할 수 있습니다.  

You can think of EBS volumes as network USB sticks.  
EBS 볼륨은 네트워크 USB 스틱이라고 생각할 수 있습니다.  

It is like a USB stick that you can take from one computer and attach to another,  
마치 USB를 한 컴퓨터에서 빼서 다른 컴퓨터에 꽂는 것과 같습니다.  

but instead of physically moving it, it is attached through the network.  
하지만 물리적으로 이동하지 않고 네트워크를 통해 연결됩니다.  

---

## Performance and Provisioning  
## 성능과 용량 설정  
👉 EBS는 미리 용량과 성능(IOPS)을 프로비저닝해야 합니다.  

EBS volumes require you to provision capacity in advance.  
EBS 볼륨은 사전에 용량을 프로비저닝해야 합니다.  

You must specify how many gigabytes you want and the IOPS.  
몇 GB를 쓸지와 IOPS(초당 입출력 연산 수)를 지정해야 합니다.  

This defines how you want your EBS volume to perform.  
이 설정이 EBS 볼륨의 성능을 정의합니다.  

You will be billed for the provisioned capacity,  
프로비저닝된 용량에 대해 과금되며,  

and you can increase the capacity over time to improve performance or size.  
시간이 지남에 따라 성능이나 용량을 늘릴 수도 있습니다.  

---

## Delete on Termination Attribute  
## 종료 시 삭제 속성  
👉 EBS의 중요한 속성 중 하나는 "delete on termination"입니다.  

When creating EBS volumes through EC2 instances, there is an attribute called "delete on termination."  
EC2 인스턴스를 통해 EBS 볼륨을 만들 때, "delete on termination"이라는 속성이 있습니다.  

This attribute controls the behavior of the EBS volume when the EC2 instance is terminated.  
이 속성은 EC2 인스턴스 종료 시 EBS 볼륨이 어떻게 처리될지 제어합니다.  

By default, the root EBS volume has "delete on termination" enabled,  
기본적으로 루트 EBS 볼륨은 종료 시 삭제가 활성화되어 있으며,  

meaning it is deleted alongside the instance termination.  
즉, 인스턴스 종료 시 함께 삭제됩니다.  

Other attached EBS volumes have this attribute disabled by default,  
추가 연결된 EBS 볼륨은 기본적으로 종료 시 삭제되지 않으며,  

so they are not deleted when the instance is terminated.  
따라서 인스턴스 종료 시에도 삭제되지 않습니다.  

---

## Key Takeaways  
## 핵심 요약  
👉 시험 대비 및 실무 핵심 포인트  

- EBS volumes are network-attached storage devices that persist data independently of EC2 instance lifecycles.  
- EBS 볼륨은 EC2 인스턴스 수명 주기와 독립적으로 데이터를 보존하는 네트워크 연결 스토리지 장치입니다.  

- Each EBS volume is bound to a specific availability zone and can only be attached to one instance at a time.  
- 각 EBS 볼륨은 특정 가용 영역에 묶이며, 동시에 하나의 인스턴스에만 연결 가능합니다.  

- EBS volumes must be provisioned with capacity and IOPS in advance.  
- EBS는 용량과 IOPS를 사전에 지정해야 합니다.  

- The "delete on termination" attribute controls whether EBS volumes are deleted when their associated EC2 instance is terminated.  
- "종료 시 삭제(delete on termination)" 속성은 인스턴스 종료 시 EBS 볼륨이 삭제될지 여부를 결정합니다.  
