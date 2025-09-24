# EC2 Placement Groups - Hands On  
# EC2 배치 그룹 - 실습  
(직접 실습을 통해 EC2 배치 그룹을 생성하고 사용하는 방법을 학습)

---

## Introduction to EC2 Placement Groups  
## EC2 배치 그룹 소개  

In this session, we will practice working with EC2 placement groups.  
이번 세션에서는 EC2 배치 그룹을 다루는 실습을 진행합니다.  
➡️ 실제로 그룹을 생성하고 인스턴스를 배치하는 방법을 체험.

Placement groups allow you to influence the placement of instances to meet specific needs such as high network performance or fault tolerance.  
배치 그룹은 인스턴스의 배치를 제어하여 고성능 네트워크나 장애 허용성과 같은 특정 요구 사항을 충족할 수 있도록 해줍니다.  
➡️ 성능 최적화 또는 고가용성 전략 구현 가능.

---

## Navigating to Placement Groups  
## 배치 그룹으로 이동하기  

On the AWS Management Console, on the left-hand side, scroll down to find the Network & Security section.  
AWS 관리 콘솔 왼쪽 메뉴에서 아래로 스크롤하여 "네트워크 및 보안(Network & Security)" 섹션을 찾습니다.  
➡️ 배치 그룹 메뉴 접근 경로.

Under this section, select the Placement Groups option to begin creating placement groups.  
이 섹션에서 "Placement Groups" 옵션을 선택하여 배치 그룹 생성을 시작합니다.  
➡️ 실습의 시작 단계.

---

## Creating a Cluster Placement Group  
## 클러스터 배치 그룹 생성  

The first placement group we will create is named **my-high-performance-group**.  
첫 번째로 생성할 배치 그룹의 이름은 **my-high-performance-group**입니다.  
➡️ 이름 규칙 예시.

The placement strategy for this group is **cluster**.  
이 그룹의 배치 전략은 **클러스터(cluster)**입니다.  
➡️ 인스턴스를 한곳에 밀집 배치.

This strategy places instances very close to each other to maximize network capability and performance.  
이 전략은 인스턴스를 서로 가깝게 배치하여 네트워크 성능을 극대화합니다.  
➡️ 고성능 컴퓨팅(HPC)에 적합.

---

## Creating a Spread Placement Group  
## 스프레드 배치 그룹 생성  

Next, create a placement group named **my-critical-group**.  
다음으로 **my-critical-group**이라는 배치 그룹을 생성합니다.  
➡️ 중요 서비스용 그룹 예시.

The placement strategy here is **spread**.  
이 그룹의 배치 전략은 **스프레드(spread)**입니다.  
➡️ 인스턴스를 최대한 분산 배치.

This strategy distributes instances as much as possible to reduce correlated failures.  
이 전략은 인스턴스를 최대한 분산시켜 연관된 장애 발생 위험을 줄여줍니다.  
➡️ 고가용성 확보.

You can set the spread level to either rack (default) or host (which is only applicable for Outposts).  
스프레드 수준은 랙(rack, 기본값) 또는 호스트(host, Outposts 전용)로 설정할 수 있습니다.  
➡️ Outposts가 아니면 랙 수준만 사용 가능.

Since we are not using Outposts, we will use the default rack level.  
Outposts를 사용하지 않으므로 기본 랙 수준을 사용합니다.  
➡️ 일반 실습 환경 기준.

---

## Creating a Partition Placement Group  
## 파티션 배치 그룹 생성  

Finally, create a placement group named **my-distributed-group** using the **partition** placement strategy.  
마지막으로 **my-distributed-group**이라는 이름으로 **파티션(partition)** 전략을 사용하여 그룹을 생성합니다.  
➡️ 대규모 분산 애플리케이션용.

Here, you can specify the number of partitions, for example, 1, 2, or 7.  
여기서 파티션 개수를 1, 2, 또는 7 등으로 지정할 수 있습니다.  
➡️ 확장성과 격리 수준 조절.

In this example, we set it to **4 partitions** before creating the group.  
이 예제에서는 그룹을 생성하기 전에 **4개의 파티션**으로 설정합니다.  
➡️ 실습 설정값.

---

## Launching Instances in Placement Groups  
## 배치 그룹 내에서 인스턴스 실행하기  

After creating the placement groups, you can launch instances within them.  
배치 그룹을 생성한 후, 그 안에서 인스턴스를 실행할 수 있습니다.  
➡️ 그룹 사용 방법.

Click on **Launch Instances**, and when configuring the instance, scroll down to the **Advanced Details** section at the bottom.  
**Launch Instances**를 클릭하고, 인스턴스를 설정할 때 맨 아래 **Advanced Details** 섹션으로 스크롤합니다.  
➡️ 배치 그룹 설정 위치.

Here, you will find the option to specify the **Placement Group Name**.  
여기서 **Placement Group Name**을 지정할 수 있는 옵션이 있습니다.  
➡️ 배치 그룹 선택 가능.

You can select from **my-critical-group**, **my-distributed-group**, or **my-high-performance-group** based on your desired placement strategy.  
원하는 배치 전략에 따라 **my-critical-group**, **my-distributed-group**, 또는 **my-high-performance-group**을 선택할 수 있습니다.  
➡️ 적합한 전략 선택.

---

## Summary  
## 요약  

This brief lecture demonstrated how to create and use different types of EC2 placement groups to optimize instance placement for performance and fault tolerance.  
이번 강의에서는 성능과 장애 허용성을 최적화하기 위해 다양한 EC2 배치 그룹을 생성하고 사용하는 방법을 살펴보았습니다.  
➡️ 실습을 통한 이해.

You now know where to find these options and how to apply them when launching instances.  
이제 인스턴스를 실행할 때 배치 그룹 옵션을 어디에서 찾고 적용하는지 알게 되었습니다.  
➡️ 실무 활용 가능.

---

## Key Takeaways  
## 핵심 요약  

- Created three types of EC2 placement groups: cluster, spread, and partition.  
- 세 가지 EC2 배치 그룹(클러스터, 스프레드, 파티션)을 생성함.  

- Cluster placement groups keep instances close for maximum network performance.  
- 클러스터 그룹은 인스턴스를 가까이 배치해 네트워크 성능을 극대화함.  

- Spread placement groups distribute instances across racks to reduce correlated failures.  
- 스프레드 그룹은 인스턴스를 여러 랙에 분산시켜 연관 장애를 줄임.  

- Partition placement groups divide instances into partitions for fault isolation.  
- 파티션 그룹은 인스턴스를 여러 파티션에 분할하여 장애를 격리함.  
