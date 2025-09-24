# EC2 Placement Groups  
# EC2 배치 그룹  
(EC2 배치 그룹은 인스턴스의 배치를 제어하여 성능과 가용성을 최적화하는 기능임을 소개)

---

## Introduction to Placement Groups  
## 배치 그룹 소개  
(EC2 인스턴스를 AWS 인프라 내에서 어떻게 배치할지를 제어하는 고급 기능)

Placement groups are a more advanced feature used when you want control over how your EC2 instances are placed within the AWS infrastructure.  
배치 그룹은 EC2 인스턴스를 AWS 인프라 내에서 어떻게 배치할지를 제어할 수 있는 고급 기능입니다.  
➡️ AWS 하드웨어를 직접 다루지는 않지만, 인스턴스 배치 전략을 지정할 수 있음.

While you do not get direct interaction with AWS hardware, placement groups allow you to specify how your EC2 instances should be positioned relative to one another.  
AWS 하드웨어에 직접 접근할 수는 없지만, 인스턴스 간의 상대적 위치를 지정할 수 있습니다.  
➡️ 인스턴스 간의 물리적/논리적 위치를 AWS에 요청 가능.

When creating a placement group, you have three strategies available:  
배치 그룹을 만들 때 세 가지 전략을 사용할 수 있습니다:  
➡️ 클러스터(Cluster), 스프레드(Spread), 파티션(Partition).

- **Cluster**: Instances are grouped together in a low-latency hardware setup within a single availability zone.  
- **클러스터**: 인스턴스가 하나의 가용 영역(AZ) 내에서 저지연 하드웨어에 밀집 배치됨.  
➡️ 빠른 통신 속도와 높은 대역폭 제공.

- **Spread**: Instances are spread across different hardware.  
- **스프레드**: 인스턴스가 서로 다른 하드웨어에 분산 배치됨.  
➡️ 장애 발생 위험을 최소화.

- **Partition**: Instances are spread across multiple partitions, which are sets of racks within an availability zone.  
- **파티션**: 인스턴스가 가용 영역 내 여러 파티션(랙 단위)에 분산됨.  
➡️ 대규모 분산 애플리케이션에 적합.

---

## Cluster Placement Group  
## 클러스터 배치 그룹  

In a cluster placement group, all your EC2 instances are located within the same availability zone.  
클러스터 배치 그룹에서는 모든 인스턴스가 동일한 가용 영역 내에 배치됩니다.  
➡️ 빠른 성능 제공, 단일 AZ 의존.

This setup provides great networking capabilities, offering approximately 10 gigabits per second of bandwidth between instances with enhanced networking enabled.  
이 설정은 향상된 네트워킹이 활성화된 인스턴스 간에 약 10Gbps 대역폭을 제공합니다.  
➡️ 저지연, 고성능 네트워크 가능.

This results in low latency and high throughput, ideal for computationally intensive jobs.  
이는 저지연, 고처리를 제공하여 연산 집약적인 작업에 이상적입니다.  
➡️ HPC, 빅데이터 처리에 적합.

However, the drawback is that if the availability zone fails, all instances in the group fail simultaneously.  
하지만 단점은 가용 영역이 장애가 나면 그룹 내 모든 인스턴스가 동시에 실패한다는 것입니다.  
➡️ 단일 장애점(SPOF) 위험 존재.

Despite this risk, cluster placement groups are suitable for use cases such as big data jobs that require fast completion and applications needing extremely low latency and high throughput networking between instances.  
이러한 위험에도 불구하고, 빠른 처리가 필요한 빅데이터 작업이나 극저지연/고성능 네트워크가 필요한 애플리케이션에 적합합니다.  
➡️ 성능 우선 애플리케이션에 활용.

---

## Spread Placement Group  
## 스프레드 배치 그룹  

Spread placement groups aim to minimize failure risk by placing EC2 instances on different hardware.  
스프레드 배치 그룹은 인스턴스를 서로 다른 하드웨어에 배치하여 장애 위험을 최소화합니다.  
➡️ 고가용성을 목표.

For example, across three availability zones, six EC2 instances can be distributed so that each instance resides on separate hardware.  
예를 들어, 세 개의 가용 영역에 걸쳐 여섯 개의 인스턴스를 분산 배치할 수 있으며, 각 인스턴스는 독립된 하드웨어에 위치합니다.  
➡️ 동시 장애 위험이 크게 줄어듦.

A limitation of spread placement groups is that you can have only up to seven instances per availability zone per placement group.  
스프레드 배치 그룹의 제한은 가용 영역당 최대 7개의 인스턴스만 허용된다는 것입니다.  
➡️ 규모 제한 존재.

This makes it suitable for critical applications that require high availability and isolation of instance failures.  
이는 고가용성과 장애 격리가 중요한 애플리케이션에 적합합니다.  
➡️ 미션 크리티컬 시스템에 활용.

---

## Partition Placement Group  
## 파티션 배치 그룹  

Partition placement groups allow instances to be spread across multiple partitions within availability zones.  
파티션 배치 그룹은 인스턴스를 가용 영역 내 여러 파티션(랙 단위)에 분산시킵니다.  
➡️ 랙 단위 장애 격리 가능.

Each partition corresponds to a rack of hardware.  
각 파티션은 하나의 하드웨어 랙을 의미합니다.  
➡️ 물리적 격리 제공.

For example, you can have up to seven partitions per availability zone, each containing multiple EC2 instances.  
예를 들어, 가용 영역당 최대 7개의 파티션을 둘 수 있으며, 각 파티션에는 여러 인스턴스가 포함될 수 있습니다.  
➡️ 대규모 확장 가능.

This setup ensures that instances in different partitions do not share the same physical hardware rack, isolating them from rack-level failures.  
이 설정은 파티션 간 인스턴스가 동일한 하드웨어 랙을 공유하지 않도록 하여, 랙 단위 장애로부터 격리시킵니다.  
➡️ 장애 도메인 분리.

Partition placement groups can span multiple availability zones within the same region and support scaling to hundreds of EC2 instances.  
파티션 배치 그룹은 동일한 리전 내 여러 가용 영역에 걸쳐 구성될 수 있으며, 수백 개의 인스턴스로 확장 가능합니다.  
➡️ 대규모 분산 애플리케이션 적합.

Partition placement groups are ideal for partition-aware applications such as Hadoop Distributed File System (HDFS), HBase, Cassandra, and Apache Kafka, which distribute data and servers across partitions.  
파티션 배치 그룹은 HDFS, HBase, Cassandra, Kafka와 같은 파티션 인식 애플리케이션에 적합합니다.  
➡️ 분산 데이터 저장소/메시징 시스템에 사용.

You can determine which partition an EC2 instance belongs to by accessing this information through the instance metadata service.  
EC2 인스턴스가 속한 파티션은 인스턴스 메타데이터 서비스를 통해 확인할 수 있습니다.  
➡️ 관리 및 모니터링에 유용.

---

## Summary  
## 요약  

Placement groups provide strategic control over EC2 instance placement to optimize performance and availability:  
배치 그룹은 EC2 인스턴스 배치를 전략적으로 제어하여 성능과 가용성을 최적화합니다.  
➡️ 선택 전략에 따라 트레이드오프 존재.

- **Cluster**: High performance within a single AZ but higher risk.  
- **클러스터**: 단일 AZ 내 고성능, 단일 장애 위험 있음.  

- **Spread**: High availability by spreading instances across hardware, limited to seven per AZ.  
- **스프레드**: 인스턴스를 분산시켜 고가용성 확보, AZ당 최대 7개 제한.  

- **Partition**: Scalable, partition-aware distribution across racks and AZs for large applications.  
- **파티션**: 대규모 애플리케이션용, 파티션 단위 분산 및 확장 가능.  

---

## Key Takeaways  
## 핵심 요약  

- Placement groups allow control over EC2 instance placement within AWS infrastructure.  
- 배치 그룹은 AWS 인프라 내에서 EC2 인스턴스 배치를 제어할 수 있습니다.  

- Cluster placement groups provide low-latency, high-throughput networking within a single availability zone but carry higher risk.  
- 클러스터 배치 그룹은 저지연, 고성능 네트워크를 제공하지만 단일 AZ 장애 위험이 있습니다.  

- Spread placement groups distribute instances across different hardware to minimize simultaneous failures, limited to seven instances per AZ.  
- 스프레드 배치 그룹은 인스턴스를 다른 하드웨어에 분산하여 동시 장애를 줄이며, AZ당 7개 제한이 있습니다.  

- Partition placement groups spread instances across multiple partitions (racks) within AZs, supporting large-scale, partition-aware applications like Hadoop and Kafka.  
- 파티션 배치 그룹은 AZ 내 여러 파티션에 분산하여 Hadoop, Kafka 같은 대규모 분산 애플리케이션을 지원합니다.  
