# EBS Volume Types  
# EBS 볼륨 유형  

## Introduction to EBS Volume Types  
## EBS 볼륨 유형 소개  

Let's discuss EBS volumes and their different volume types.  
EBS 볼륨과 다양한 볼륨 유형에 대해 알아보겠습니다.  

Currently, there are six different types, which can be grouped into several categories.  
현재 EBS 볼륨은 6가지 유형이 있으며, 몇 가지 범주로 나눌 수 있습니다.  

- gp2 and gp3: General purpose SSD volumes that balance price and performance for a wide variety of workloads. These have been used throughout this course.  
- gp2 및 gp3: 다양한 워크로드에 대해 가격과 성능을 균형 있게 제공하는 범용 SSD 볼륨입니다. 이번 강의 내내 사용되었습니다.  

- io1 and io2 Block Express: Highest-performance SSD volumes designed for mission-critical, low-latency, and high-throughput workloads.  
- io1 및 io2 Block Express: 중요한 워크로드, 낮은 지연 시간, 높은 처리량을 요구하는 미션 크리티컬 환경용 최고 성능 SSD 볼륨입니다.  

- st1: Low-cost HDD volumes designed for frequently accessed, throughput-intensive workloads.  
- st1: 자주 액세스하며 높은 처리량을 요구하는 워크로드에 적합한 저가형 HDD 볼륨입니다.  

- sc1: Lowest-cost HDD volumes designed for less frequently accessed workloads.  
- sc1: 덜 자주 액세스되는 워크로드를 위한 최저가 HDD 볼륨입니다.  

## Defining an EBS Volume  
## EBS 볼륨 정의  

Several factors define an EBS volume, including size, throughput, and IOPS (Input/Output Operations Per Second).  
EBS 볼륨은 크기, 처리량, IOPS(초당 입출력 작업 수) 등 여러 요소로 정의됩니다.  

When uncertain, always consult the official documentation.  
불확실할 경우 공식 문서를 항상 참조하세요.  

For EC2 instances, only gp2, gp3, io1, and io2 volumes can be used as boot volumes, meaning they host the root operating system.  
EC2 인스턴스의 부트 볼륨으로는 gp2, gp3, io1, io2만 사용할 수 있으며, 루트 운영 체제를 호스팅합니다.  

## Deep Dive into gp2 and gp3 Volumes  
## gp2 및 gp3 볼륨 심층 분석  

The gp2 volume is cost-effective storage with low latency.  
gp2 볼륨은 저렴하고 낮은 지연 시간을 제공하는 스토리지입니다.  

It is suitable for system boot volumes, virtual desktops, and development and test environments.  
시스템 부트 볼륨, 가상 데스크톱, 개발 및 테스트 환경에 적합합니다.  

The size can vary between 1 gigabyte and 16 terabytes.  
볼륨 크기는 1GB에서 16TB까지 다양합니다.  

gp3 is the newer generation of volumes.  
gp3는 최신 세대 볼륨입니다.  

It provides a baseline of 3,000 IOPS and a throughput of 125 megabytes per second.  
기본 3,000 IOPS와 초당 125MB 처리량을 제공합니다.  

You can increase IOPS up to 16,000 and throughput up to 1,000 megabytes per second independently, meaning they are not linked.  
IOPS는 최대 16,000, 처리량은 최대 1,000MB/s까지 독립적으로 증가시킬 수 있으며 서로 연동되지 않습니다.  

In contrast, gp2 is the older version where the size of the volume and the IOPS are linked.  
반면 gp2는 볼륨 크기와 IOPS가 연동되는 이전 버전입니다.  

Small gp2 volumes can burst up to 3,000 IOPS.  
작은 gp2 볼륨은 최대 3,000 IOPS까지 버스트 가능합니다.  

Increasing the volume size increases IOPS at a rate of 3 IOPS per gigabyte, up to a maximum of 16,000 IOPS.  
볼륨 크기를 늘리면 IOPS가 GB당 3 IOPS씩 증가하며 최대 16,000 IOPS까지 가능합니다.  

For example, a 5,334-gigabyte gp2 volume will have 16,000 IOPS, which is the maximum.  
예를 들어, 5,334GB gp2 볼륨은 최대 16,000 IOPS를 가집니다.  

## Summary of gp2 and gp3  
## gp2 및 gp3 요약  

- Both are cost-effective storage options with low latency.  
- 둘 다 저렴하고 낮은 지연 시간을 제공하는 스토리지 옵션입니다.  

- gp3 allows independent scaling of IOPS and throughput.  
- gp3는 IOPS와 처리량을 독립적으로 조절할 수 있습니다.  

- gp2 links IOPS directly to volume size.  
- gp2는 IOPS가 볼륨 크기와 직접 연동됩니다.  

## Provisioned IOPS Volumes (io1 and io2)  
## 프로비저닝 IOPS 볼륨(io1 및 io2)  

Provisioned IOPS volumes are used for critical business applications that require sustained IOPS performance or applications needing more than 16,000 IOPS.  
프로비저닝 IOPS 볼륨은 지속적인 IOPS 성능이 필요한 중요 비즈니스 애플리케이션이나 16,000 IOPS 이상이 필요한 앱에 사용됩니다.  

For example, database workloads sensitive to storage performance and consistency benefit from these volumes.  
예를 들어, 스토리지 성능과 일관성에 민감한 데이터베이스 워크로드에 유용합니다.  

The io1 volume type ranges between 4 and 16 terabytes.  
io1 볼륨 크기는 4~16TB입니다.  

The maximum provisioned IOPS (PIOPS) is approximately 64,000 for Nitro-based EC2 instances and 32,000 for other instance types.  
최대 프로비저닝 IOPS(PIOPS)는 Nitro 기반 EC2 인스턴스에서 약 64,000, 다른 인스턴스 유형에서는 32,000입니다.  

The provisioned IOPS can be increased independently from the storage size.  
프로비저닝 IOPS는 스토리지 크기와 독립적으로 증가시킬 수 있습니다.  

The io2 Block Express volume supports up to 64 terabytes of data, offers sub-millisecond latency, and provides up to 256,000 maximum IOPS with an IOPS to gigabyte ratio of 1,000:1.  
io2 Block Express 볼륨은 최대 64TB, 서브 밀리초 지연 시간, 최대 256,000 IOPS(GB당 1,000:1)를 제공합니다.  

This is a very high-performance I/O volume type.  
이는 매우 높은 성능의 I/O 볼륨 유형입니다.  

Additionally, provisioned IOPS volumes support the EBS multi-attach feature, which will be discussed in upcoming lectures.  
또한 프로비저닝 IOPS 볼륨은 EBS 멀티 어태치 기능을 지원하며, 다음 강의에서 다룰 예정입니다.  

## Overview of st1 and sc1 Volumes  
## st1 및 sc1 볼륨 개요  

st1 and sc1 volumes cannot be used as boot volumes.  
st1과 sc1 볼륨은 부트 볼륨으로 사용할 수 없습니다.  

They can be sized up to 16 terabytes and come in two types:  
볼륨 크기는 최대 16TB이며, 두 가지 유형이 있습니다.  

- st1 (Throughput Optimized HDD): Suitable for big data, data warehousing, and log processing workloads.  
- st1(Throughput Optimized HDD): 빅데이터, 데이터 웨어하우스, 로그 처리 워크로드에 적합합니다.  

It offers a maximum throughput of 500 megabytes per second and a maximum of 500 IOPS.  
최대 처리량 500MB/s, 최대 IOPS 500을 제공합니다.  

- sc1 (Cold HDD): Designed for archive data that is infrequently accessed.  
- sc1(Cold HDD): 드물게 접근하는 아카이브 데이터용으로 설계되었습니다.  

It provides the lowest possible cost with a maximum throughput of 250 megabytes per second and a maximum of 250 IOPS.  
최저 비용으로 최대 처리량 250MB/s, 최대 IOPS 250을 제공합니다.  

## Exam Preparation Notes  
## 시험 준비 참고사항  

You do not need to memorize all the detailed specifications for the exam.  
시험에서는 모든 세부 사양을 암기할 필요는 없습니다.  

Instead, understand the high-level differences:  
대신, 주요 차이점을 이해하세요.  

- General purpose SSD (gp2, gp3) versus provisioned IOPS SSD (io1, io2) for database workloads.  
- 범용 SSD(gp2, gp3)와 프로비저닝 IOPS SSD(io1, io2)의 데이터베이스 워크로드용 차이.  

- st1 and sc1 for high throughput and lowest cost HDD options.  
- st1과 sc1은 높은 처리량 및 최저 비용 HDD 옵션입니다.  

Also, to achieve over 32,000 IOPS, you need EC2 Nitro instances with io1 or io2 volumes.  
또한 32,000 IOPS 이상을 달성하려면 io1 또는 io2 볼륨이 있는 EC2 Nitro 인스턴스가 필요합니다.  

For a summary of all volume types and their characteristics, refer to the official AWS documentation or the provided link in the course materials.  
모든 볼륨 유형과 특성 요약은 AWS 공식 문서나 강의 자료의 링크를 참조하세요.  

## Key Takeaways  
## 핵심 요약  

- EBS volumes come in six types: gp2, gp3, io1, io2 Block Express, st1, and sc1.  
- EBS 볼륨은 gp2, gp3, io1, io2 Block Express, st1, sc1 등 6가지 유형이 있습니다.  

- gp2 and gp3 are general purpose SSDs balancing price and performance; gp3 allows independent scaling of IOPS and throughput.  
- gp2와 gp3는 가격과 성능을 균형 있게 제공하는 범용 SSD이며, gp3는 IOPS와 처리량을 독립적으로 조절할 수 있습니다.

* io1 and io2 are high-performance provisioned IOPS SSDs for mission-critical workloads, with io2 Block Express offering up to 256,000 IOPS.

* io1과 io2는 미션 크리티컬 워크로드용 고성능 프로비저닝 IOPS SSD이며, io2 Block Express는 최대 256,000 IOPS를 제공합니다.

* st1 and sc1 are HDD volumes optimized for throughput and cost, respectively, and cannot be used as boot volumes.

* st1과 sc1은 각각 처리량과 비용에 최적화된 HDD 볼륨이며, 부트 볼륨으로 사용할 수 없습니다.
