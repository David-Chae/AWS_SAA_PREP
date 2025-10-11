# EFS vs EBS
# EFS와 EBS 비교
> Differences Between EBS Volumes and EFS File Systems
> EBS 볼륨과 EFS 파일 시스템의 차이점
> 설명: EBS와 EFS의 기본적인 차이를 이해하기 위한 섹션입니다.

## EBS Overview
## EBS 개요
> EBS volumes are attached to one EC2 instance at a time, except in the specific case of using the multi-attach feature available for the io1 and io2 volume types. However, this feature is intended for very specific use cases.
> EBS 볼륨은 한 번에 하나의 EC2 인스턴스에만 연결됩니다. 단, io1 및 io2 볼륨 타입에서 제공되는 Multi-Attach 기능을 사용할 경우 예외입니다. 그러나 이 기능은 매우 특정한 사용 사례에 적합합니다.
> 설명: EBS는 기본적으로 단일 인스턴스 전용이며, Multi-Attach 기능은 제한적 용도임을 강조

> EBS volumes are locked at the Availability Zone (AZ) level. For example, if we have one EC2 instance in AZ 1 with an attached EBS volume, that volume cannot be attached to an EC2 instance in AZ 2.
> EBS 볼륨은 가용 영역(AZ) 단위로 잠깁니다. 예를 들어 AZ1의 EC2 인스턴스에 연결된 EBS 볼륨은 AZ2의 인스턴스에 연결할 수 없습니다.
> 설명: EBS는 AZ 이동 불가, AZ 의존성 강조

> For the gp2 volume type, the IO performance increases as the disk size increases. In contrast, for the gp3 and io1 volume types, you can increase the IO performance independently from the disk size.
> gp2 볼륨의 경우, 디스크 크기가 커지면 IO 성능도 증가합니다. 반면 gp3 및 io1 볼륨은 디스크 크기와 관계없이 IO 성능을 독립적으로 조절할 수 있습니다.
> 설명: 볼륨 타입별 IO 성능 특징

> To migrate an EBS volume across Availability Zones, you need to take a snapshot of the volume. This snapshot is stored in EBS snapshots, and then you can restore the snapshot into another AZ. This is the process to move an EBS volume from one AZ to another.
> EBS 볼륨을 다른 AZ로 이동하려면 볼륨 스냅샷을 생성해야 합니다. 스냅샷은 EBS 스냅샷으로 저장되며, 이를 다른 AZ에서 복원할 수 있습니다. 이 과정을 통해 EBS를 AZ 간 이동시킵니다.
> 설명: AZ 간 EBS 이동 시 스냅샷 활용 절차

> EBS volume backups consume IO resources. Therefore, it is advisable not to run backups while your application is handling a high volume of traffic, as this may impact performance.
> EBS 볼륨 백업은 IO 리소스를 사용합니다. 따라서 트래픽이 많은 애플리케이션 실행 중에는 백업을 수행하지 않는 것이 좋습니다. 성능에 영향을 줄 수 있기 때문입니다.
> 설명: 백업 시 성능 영향 주의

> By default, the root EBS volumes of your EC2 instances are terminated when the EC2 instance is terminated. However, you can disable this behavior if you want the volume to persist after instance termination.
> 기본적으로 EC2 인스턴스 종료 시 루트 EBS 볼륨도 함께 삭제됩니다. 하지만 종료 후에도 볼륨을 유지하려면 이 동작을 비활성화할 수 있습니다.
> 설명: 루트 볼륨 영속성 설정 가능

## EFS Overview
## EFS 개요
> EFS is a network file system designed to be attached to hundreds of instances across multiple Availability Zones. This is a key distinction from EBS volumes.
> EFS는 여러 가용 영역의 수백 개 인스턴스에 연결 가능하도록 설계된 네트워크 파일 시스템입니다. 이는 EBS와의 중요한 차이점입니다.
> 설명: EFS는 네트워크 FS로 다수 인스턴스 공유 가능

> With one EFS file system, you can have different mount targets in different AZs. Multiple instances can share the same file system simultaneously.
> 하나의 EFS 파일 시스템으로 여러 AZ에 마운트 타깃을 만들 수 있습니다. 여러 인스턴스가 동시에 같은 파일 시스템을 공유할 수 있습니다.
> 설명: 다중 AZ 공유 가능, EFS의 핵심 장점

> EFS is particularly helpful for applications like WordPress running on Linux instances because it supports the POSIX file system standard.
> EFS는 POSIX 파일 시스템 표준을 지원하므로, Linux 인스턴스에서 WordPress 같은 애플리케이션에 특히 유용합니다.
> 설명: Linux 워크로드 친화적

> EFS generally has a higher price point than EBS. However, you can leverage storage tiers within EFS to achieve cost savings.
> EFS는 일반적으로 EBS보다 비용이 높습니다. 하지만 EFS 내 스토리지 계층(Storage Tier)을 활용하면 비용 절감이 가능합니다.
> 설명: 비용 최적화 방법 안내

## Instance Store
## 인스턴스 스토어
> The instance store is physically attached to the EC2 instance. Therefore, if you lose your EC2 instance, you will also lose the storage associated with the instance store.
> 인스턴스 스토어는 EC2 인스턴스에 물리적으로 연결됩니다. 따라서 EC2 인스턴스를 잃으면, 인스턴스 스토어에 연결된 데이터도 함께 사라집니다.
> 설명: 인스턴스 종료 시 데이터 손실 주의

## Conclusion
## 결론
> This concludes the comparison between EFS and EBS. I hope this explanation was helpful.
> 이것으로 EFS와 EBS 비교를 마칩니다. 이 설명이 도움이 되었길 바랍니다.
> 설명: 비교 요약 마무리

## Key Takeaways
## 핵심 요약
- EBS volumes are attached to a single EC2 instance at a time and are locked to a specific Availability Zone (AZ).  
- EBS 볼륨은 한 번에 하나의 EC2 인스턴스에 연결되며, 특정 AZ에 잠깁니다.  
> 설명: EBS 단일 인스턴스 연결, AZ 종속

- EBS IO performance varies by volume type, with gp3 and io1 allowing independent IO scaling.  
- EBS IO 성능은 볼륨 타입에 따라 다르며, gp3와 io1은 IO를 독립적으로 조정할 수 있습니다.  
> 설명: 볼륨별 IO 확장 가능 여부

- Migrating EBS volumes across AZs requires creating and restoring snapshots.  
- EBS 볼륨을 AZ 간 이동하려면 스냅샷 생성 및 복원이 필요합니다.  
> 설명: AZ 이동 절차 요약

- EFS is a network file system designed to be shared across multiple instances and AZs, supporting POSIX and suitable for Linux workloads.  
- EFS는 다수 인스턴스와 AZ에서 공유 가능하도록 설계된 네트워크 파일 시스템으로, POSIX를 지원하며 Linux 워크로드에 적합합니다.  
> 설명: EFS 장점 요약

- EFS generally has a higher cost but offers storage tiers for cost optimization.  
- EFS는 비용이 높지만 스토리지 계층을 통해 비용 최적화가 가능합니다.  
> 설명: 비용 관리 방법 요약

- Instance store volumes are physically attached to EC2 instances and data is lost if the instance is terminated.  
- 인스턴스 스토어 볼륨은 EC2 인스턴스에 물리적으로 연결되며, 인스턴스 종료 시 데이터가 손실됩니다.  
> 설명: 인스턴스 스토어 특징 요약
