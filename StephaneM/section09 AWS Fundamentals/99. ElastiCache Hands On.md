# ElastiCache Hands On  
# 엘라스티캐시 실습  

---

## Introduction to ElastiCache  
## ElastiCache 소개  

Let's begin by practicing with ElastiCache.  
ElastiCache 실습을 시작해봅시다.  
(실습 안내)  

We will start by creating a Redis-type ElastiCache, although Memcached is also available as an option.  
Redis 유형의 ElastiCache를 생성하면서 시작할 것이며, Memcached도 옵션으로 사용할 수 있습니다.  
(캐시 유형 선택)  

---

## Choosing Cache Type  
## 캐시 유형 선택  

We have multiple options for ElastiCache:  
ElastiCache에는 여러 옵션이 있습니다.  
(옵션 안내)  

- A serverless offering that automatically scales to meet your application traffic with no servers to manage. This option is easier to manage but significantly more expensive.  
- 서버를 관리할 필요 없이 애플리케이션 트래픽에 맞춰 자동으로 확장되는 서버리스 옵션. 관리가 쉽지만 비용이 높습니다.  
(서버리스 옵션)  

- Designing your own cache, which is easier to understand and better for architectural learning on AWS.  
- 직접 캐시를 설계하는 방식으로, 이해하기 쉽고 AWS 아키텍처 학습에 유리합니다.  
(직접 설계 옵션)  

We will proceed with designing our own cache.  
이번 실습에서는 직접 캐시를 설계하는 방법으로 진행합니다.  
(실습 방식 선택)  

---

## Creating a Redis Cache Cluster  
## Redis 캐시 클러스터 생성  

When designing your own cache, you can:  
직접 캐시를 설계할 때 다음 옵션이 있습니다.  
(옵션 안내)  

- Restore from a backup.  
- 백업에서 복원.  
(백업 복원)  

- Use easy create with recommended best practice configurations such as production, development/test, or demo setups.  
- 프로덕션, 개발/테스트, 데모 환경과 같은 권장 설정으로 손쉽게 생성.  
(손쉬운 생성)  

- Configure everything manually, including cluster cache mode.  
- 클러스터 모드 포함 모든 설정을 수동으로 구성.  
(수동 구성)  

For this demonstration, we will configure all options manually to view all available settings.  
이번 데모에서는 모든 옵션을 수동으로 구성하여 사용 가능한 설정을 모두 확인합니다.  
(설정 확인)  

---

## Cluster Mode Configuration  
## 클러스터 모드 구성  

Cluster mode can be:  
클러스터 모드는 다음과 같습니다.  
(클러스터 모드 선택)  

- Disabled: This creates a single shard with one primary node and up to five read replicas.  
- 비활성화: 하나의 샤드, 기본 노드 하나, 최대 5개의 읽기 복제본 생성.  
(비활성화 모드)  

- Enabled: Allows multiple shards across multiple servers.  
- 활성화: 여러 서버에 걸쳐 다중 샤드 생성 가능.  
(활성화 모드)  

We will disable cluster mode for this example.  
이번 예제에서는 클러스터 모드를 비활성화합니다.  
(예제 설정)  

---

## Naming and Location  
## 클러스터 이름 및 위치  

The cluster will be named DemoCluster.  
클러스터 이름은 DemoCluster로 지정합니다.  
(클러스터 이름)  

The location will be on AWS Cloud, although ElastiCache can also run on-premises using AWS Outposts.  
위치는 AWS 클라우드이며, AWS Outposts를 사용하면 온프레미스에서도 실행 가능합니다.  
(배치 위치)  

---

## High Availability Settings  
## 고가용성 설정  

Multi-AZ can be enabled for high availability and failover support if the primary node fails.  
기본 노드 장애 시 고가용성과 장애 조치를 위해 Multi-AZ를 활성화할 수 있습니다.  
(Multi-AZ 옵션)  

For this demo, multi-AZ is disabled to avoid additional costs.  
이번 데모에서는 추가 비용을 피하기 위해 Multi-AZ를 비활성화합니다.  
(비활성화 선택)  

Auto failover is enabled to allow automatic failover if needed.  
자동 장애 조치는 필요 시 활성화되어 자동으로 장애 전환이 이루어집니다.  
(자동 장애 전환)  

---

## Cluster Settings  
## 클러스터 설정  

Engine version, ports, and parameter groups can be specified.  
엔진 버전, 포트, 파라미터 그룹을 지정할 수 있습니다.  
(기본 설정)  

For node type, we will use a micro instance type, choosing from t2.micro, t3.micro, or t4g.micro.  
노드 유형으로 t2.micro, t3.micro, t4g.micro 중 마이크로 인스턴스를 선택합니다.  
(노드 선택)  

t2 and t3 micro instances are included in the AWS free tier.  
t2 및 t3 마이크로 인스턴스는 AWS 무료 사용량에 포함됩니다.  
(무료 계층 안내)  

We will select t2.micro for this example.  
이번 예제에서는 t2.micro를 선택합니다.  
(예제 선택)  

---

## Replicas and Scaling  
## 복제본 및 스케일링  

Replicas help with scaling, especially when cluster mode is enabled.  
복제본은 스케일링에 도움을 주며, 특히 클러스터 모드 활성화 시 유용합니다.  
(복제본 활용)  

For cost purposes, we will set the number of replicas to zero.  
비용 절감을 위해 복제본 수를 0으로 설정합니다.  
(비용 관리)  

When multi-AZ is enabled, having replicas is recommended.  
Multi-AZ 활성화 시 복제본 사용이 권장됩니다.  
(복제본 권장)  

---

## Subnet Group Creation  
## 서브넷 그룹 생성  

A subnet group defines which subnets ElastiCache can run in.  
서브넷 그룹은 ElastiCache가 실행될 서브넷을 정의합니다.  
(서브넷 정의)  

We will create our first subnet group.  
첫 번째 서브넷 그룹을 생성합니다.  
(실습)  

The VPC is selected, and subnets are auto-selected but can be specified manually.  
VPC 선택 후 서브넷은 자동 선택되지만 수동 지정 가능.  
(VPC 설정)  

AZ placements for replicas can be specified but are irrelevant here since multi-AZ is disabled.  
복제본의 AZ 배치는 지정 가능하지만 Multi-AZ 비활성화로 의미 없음.  
(AZ 배치)  

---

## Encryption and Access Control  
## 암호화 및 접근 제어  

Encryption at rest can be enabled by specifying a key.  
정적 데이터 암호화는 키를 지정하여 활성화할 수 있습니다.  
(정적 암호화)  

Encryption in transit secures data between clients and the server.  
전송 중 암호화는 클라이언트와 서버 간 데이터를 보호합니다.  
(전송 암호화)  

Enabling encryption in transit also enables access control features.  
전송 암호화 활성화 시 접근 제어 기능도 활성화됩니다.  
(접근 제어 연동)  

Redis AUTH allows specifying a password or AUTH token to connect to the Redis cluster.  
Redis AUTH는 클러스터 연결을 위한 비밀번호 또는 토큰을 지정할 수 있습니다.  
(Redis 인증)  

Alternatively, user group access control lists can be created from the ElastiCache console.  
또는 ElastiCache 콘솔에서 사용자 그룹 ACL을 생성할 수 있습니다.  
(ACL 설정)  

For this demo, encryption in transit is disabled.  
이번 데모에서는 전송 암호화를 비활성화합니다.  
(비활성화 선택)  

Security groups manage network-level access to the cluster.  
보안 그룹은 클러스터에 대한 네트워크 수준 접근을 관리합니다.  
(보안 그룹)  

---

## Backup, Maintenance, and Logging  
## 백업, 유지보수 및 로그  

Backup options can be enabled or disabled.  
백업 옵션 활성화/비활성화 가능.  
(백업)  

Maintenance windows allow scheduling minor version upgrades.  
유지보수 창을 통해 소규모 버전 업그레이드 일정 지정 가능.  
(유지보수)  

Logs such as slow logs or engine logs can be sent to CloudWatch logs.  
느린 로그나 엔진 로그를 CloudWatch 로그로 전송 가능.  
(로그 관리)  

Tags can be added for resource management.  
리소스 관리를 위해 태그 추가 가능.  
(태그 관리)  

These options are similar to those in Amazon RDS.  
이 옵션들은 Amazon RDS와 유사합니다.  
(RDS 비교)  

---

## Finalizing Cache Creation  
## 캐시 생성 완료  

After reviewing all settings, click create to provision the cache.  
모든 설정 확인 후 생성 버튼을 클릭하여 캐시를 프로비저닝합니다.  
(캐시 생성)  

Once created, you can view the cluster details, nodes, metrics, logs, and network security from the console.  
생성 후 콘솔에서 클러스터 상세, 노드, 지표, 로그, 네트워크 보안을 확인할 수 있습니다.  
(콘솔 확인)  

The interface resembles Amazon RDS but is tailored for Redis and Memcached.  
인터페이스는 RDS와 유사하지만 Redis 및 Memcached에 맞춰져 있습니다.  
(UI 안내)  

---

## Connecting to Redis Cache  
## Redis 캐시 연결  

Connecting to a Redis cache requires writing application code and is not straightforward to demonstrate here.  
Redis 캐시 연결은 애플리케이션 코드 작성이 필요하며, 여기서 바로 시연하기 어렵습니다.  
(연결 안내)  

The console provides primary endpoints for write operations and reader endpoints for read replicas.  
콘솔에서는 쓰기용 엔드포인트와 읽기 복제본용 엔드포인트를 제공합니다.  
(엔드포인트 안내)  

---

## Deleting the Cache Cluster  
## 캐시 클러스터 삭제  

To delete the Redis cluster, select the cluster, choose the delete action, and confirm by typing the cluster name.  
Redis 클러스터 삭제는 클러스터 선택 → 삭제 → 이름 입력으로 확인합니다.  
(삭제 방법)  

Backup before deletion is optional.  
삭제 전 백업은 선택 사항입니다.  
(백업 선택)  

This concludes the hands-on session.  
이로써 실습 세션이 종료됩니다.  
(실습 종료)  

---

## Key Takeaways  
## 핵심 요약  

- ElastiCache supports Redis and Memcached, with options for serverless or custom cache design.  
- ElastiCache는 Redis와 Memcached를 지원하며, 서버리스 또는 직접 설계 캐시 옵션을 제공합니다.  
- Cluster mode can be enabled for multiple shards or disabled for a single shard with replicas.  
- 클러스터 모드는 다중 샤드를 위해 활성화하거나, 단일 샤드와 복제본을 위해 비활성화할 수 있습니다.  
- Multi-AZ and auto failover enhance availability but may increase costs.  
- Multi-AZ 및 자동 장애 조치는 가용성을 향상시키지만 비용이 증가할 수 있습니다.  
- Encryption, access control, backups, and maintenance windows are configurable features.  
- 암호화, 접근 제어, 백업, 유지보수 창 등은 구성 가능한 기능입니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+500XP**
* 아이템: **"ElastiCache Hands-On Scroll"**
* 업적 달성: **"Cache Practitioner"** 🛠️

이 MD 파일은 **ElastiCache 실습 과정, 클러스터 생성, 설정, 연결, 삭제까지** 모든 단계를 포함하여 실제 학습과 시험 대비 자료로 활용 가능합니다.
