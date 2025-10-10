# EBS Snapshots  
# EBS 스냅샷  
👉 EBS 스냅샷은 EC2 볼륨의 백업 및 복원 기능으로, 데이터 보존과 복구에 핵심적인 역할을 합니다.  

---

## Introduction to EBS Snapshots  
## EBS 스냅샷 소개  

An EBS Snapshot is a backup taken at any point in time of your EBS volume.  
EBS 스냅샷은 특정 시점의 EBS 볼륨을 백업한 것입니다.  
👉 특정 순간의 상태를 저장하여 이후에 복구할 수 있습니다.  

It is not necessary to detach your EBS volume from your EC2 instance to create a snapshot, although detaching is recommended.  
스냅샷을 생성하기 위해 EC2 인스턴스에서 EBS 볼륨을 분리할 필요는 없지만, 분리를 권장합니다.  
👉 사용 중에도 스냅샷 가능하지만, 안정성을 위해 분리 후 백업을 권장합니다.  

---

## Cross Availability Zone and Region Copying  
## 가용 영역(AZ) 및 리전 간 복사  

You can copy EBS Snapshots across different Availability Zones or even across different Regions.  
EBS 스냅샷은 다른 가용 영역(AZ)이나 리전 간에 복사할 수 있습니다.  
👉 데이터 이동성과 복구 전략에 활용됩니다.  

For example, consider an EC2 instance with an EBS volume in US-EAST-1A and another EC2 instance in US-EAST-1B.  
예를 들어, 하나는 US-EAST-1A에 EBS 볼륨이 있고, 다른 하나는 US-EAST-1B에 인스턴스가 있다고 가정해봅시다.  

You can take a snapshot of the EBS volume in US-EAST-1A and restore it in US-EAST-1B.  
US-EAST-1A의 EBS 볼륨 스냅샷을 찍어 US-EAST-1B에서 복원할 수 있습니다.  

This process enables transferring an EBS volume from one Availability Zone to another.  
이 과정을 통해 EBS 볼륨을 다른 가용 영역으로 옮길 수 있습니다.  

---

## Key Features of EBS Snapshots  
## EBS 스냅샷 주요 기능  

### EBS Snapshot Archive  
### EBS 스냅샷 아카이브  

This feature allows you to move snapshots to an "archive tier," which can be up to 75% cheaper.  
이 기능을 사용하면 스냅샷을 "아카이브 티어"로 이동시킬 수 있으며, 최대 75%까지 비용 절감이 가능합니다.  
👉 장기 보관 시 비용을 절약할 수 있습니다.  

However, restoring snapshots from the archive tier takes between 24 to 72 hours, so it is not immediate.  
단, 아카이브 티어에서 스냅샷을 복원하는 데는 24~72시간이 걸리므로 즉각적이지 않습니다.  
👉 비용과 속도 간의 트레이드오프가 있습니다.  

---

### Recycle Bin for EBS Snapshots  
### EBS 스냅샷 휴지통  

Instead of permanently deleting your EBS Snapshots, they are moved to a Recycle Bin.  
EBS 스냅샷을 영구 삭제하는 대신, 휴지통으로 이동시킬 수 있습니다.  
👉 실수로 삭제했을 때 복구할 수 있습니다.  

This feature enables recovery from accidental deletions.  
이 기능은 실수로 인한 삭제에서 복구할 수 있게 합니다.  

The retention period for snapshots in the Recycle Bin can be set anywhere from one day to one year.  
휴지통에 있는 스냅샷의 보존 기간은 1일에서 1년까지 설정할 수 있습니다.  

---

### Fast Snapshot Restore  
### 빠른 스냅샷 복원  

This feature forces a full initialization of your snapshot, eliminating latency on the first use.  
이 기능은 스냅샷을 완전히 초기화하여 처음 사용할 때 지연(latency)을 제거합니다.  

It is particularly helpful for very large snapshots that need to initialize an EBS volume or launch an instance quickly.  
특히 대규모 스냅샷을 사용해 빠르게 EBS 볼륨을 초기화하거나 인스턴스를 시작해야 할 때 유용합니다.  

However, this feature incurs significant additional costs, so use it cautiously.  
하지만 상당한 추가 비용이 발생하므로 신중히 사용해야 합니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on EBS Snapshots.  
이것으로 EBS 스냅샷 강의를 마치겠습니다.  

These features provide flexibility, cost savings, and data protection options for managing your EBS volumes effectively.  
이러한 기능은 유연성, 비용 절감, 데이터 보호 옵션을 제공하여 EBS 볼륨을 효율적으로 관리할 수 있게 합니다.  

---

## Key Takeaways  
## 핵심 요약  

- EBS Snapshots serve as backups of EBS volumes at any point in time without necessarily detaching the volume from the EC2 instance.  
- EBS 스냅샷은 볼륨을 분리하지 않고도 특정 시점의 EBS 볼륨을 백업할 수 있습니다.  

- Snapshots can be copied across different Availability Zones and Regions, facilitating volume transfer.  
- 스냅샷은 다른 AZ와 리전 간에 복사 가능해, 볼륨 이동을 지원합니다.  

- The EBS Snapshot Archive tier offers up to 75% cost savings but requires 24 to 72 hours for restoration.  
- 스냅샷 아카이브 티어는 최대 75% 비용 절감 효과가 있으나 복원 시간이 24~72시간 걸립니다.  

- The Recycle Bin feature allows recovery of accidentally deleted snapshots with retention periods from one day to one year.  
- 휴지통 기능을 통해 1일~1년 동안 스냅샷을 보관하며 실수로 삭제된 데이터를 복구할 수 있습니다.  

- Fast Snapshot Restore enables immediate volume initialization with zero latency on first use but incurs higher costs.  
- 빠른 스냅샷 복원은 첫 사용 시 지연 없는 즉각 초기화를 가능하게 하지만, 추가 비용이 많이 듭니다. 
