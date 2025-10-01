# WhatIsTheTime.com: A Solutions Architect's Journey to Scalable and Highly Available Architecture  
# WhatIsTheTime.com: 확장성과 고가용성을 향한 솔루션 아키텍트의 여정  
→ 이 문서는 간단한 웹사이트를 예시로, 어떻게 아키텍처가 발전하는지 과정을 설명합니다.  

---

## Introduction to the WhatIsTheTime.com Application  
## WhatIsTheTime.com 애플리케이션 소개  
→ 단순한 서비스이지만 아키텍처 학습에 매우 유용한 사례입니다.  

Let's begin our first solution architecture discussion with the WhatIsTheTime.com website.  
첫 번째 솔루션 아키텍처 토론은 WhatIsTheTime.com 웹사이트로 시작하겠습니다.  
→ 학습 사례로 사용할 기본 애플리케이션입니다.  

This simple application allows users to know the current time.  
이 단순한 애플리케이션은 사용자가 현재 시간을 알 수 있게 합니다.  
→ 서비스 기능은 매우 간단합니다.  

Although it sounds basic, it serves as an excellent example to understand various architectural concepts and challenges faced by solutions architects.  
기능은 단순해 보이지만, 다양한 아키텍처 개념과 솔루션 아키텍트가 직면하는 문제를 이해하기에 훌륭한 예시가 됩니다.  
→ 단순한 예시를 통해 복잡한 원리를 학습합니다.  

Since the application is straightforward, we do not require a database.  
애플리케이션이 단순하기 때문에 데이터베이스는 필요하지 않습니다.  
→ 상태 저장이 필요 없는 애플리케이션 구조입니다.  

Each server instance inherently knows the current time.  
각 서버 인스턴스는 기본적으로 현재 시간을 알고 있습니다.  
→ 서버 자체가 데이터를 제공할 수 있어 DB 불필요.  

We will start small, accepting some downtime initially, but anticipate growing popularity as more users want to know the time worldwide.  
처음에는 소규모로 시작해 약간의 다운타임을 감수하지만, 전 세계적으로 더 많은 사용자가 시간을 확인하려 하면서 인기가 증가할 것으로 예상합니다.  
→ 향후 확장 가능성을 염두에 둔 설계입니다.  

This growth will require vertical and horizontal scaling to handle increased traffic and reduce downtime.  
이러한 성장은 트래픽 증가와 다운타임 감소를 위해 수직 및 수평 확장을 필요로 합니다.  
→ 확장 전략(Vertical & Horizontal Scaling)의 필요성을 제시합니다.  

---

## Initial Architecture: Single EC2 Instance with Elastic IP  
## 초기 아키텍처: Elastic IP가 있는 단일 EC2 인스턴스  
→ 기본 구조는 작은 단일 서버 기반입니다.  

As a solutions architect, the first approach is to deploy a T2 micro EC2 instance.  
솔루션 아키텍트로서 첫 번째 접근은 T2 micro EC2 인스턴스를 배포하는 것입니다.  
→ 최소 비용, 최소 구성을 사용합니다.  

When a user queries "What time is it?", the instance responds with the current time, such as "5:30 PM."  
사용자가 "지금 몇 시인가요?"라고 요청하면 인스턴스는 현재 시간(예: "오후 5:30")을 응답합니다.  
→ 단일 서버가 직접 요청을 처리합니다.  

To ensure the instance has a static IP address even after restarts, we attach an Elastic IP to it.  
인스턴스가 재시작 후에도 고정 IP 주소를 갖도록 Elastic IP를 연결합니다.  
→ 고정 IP는 사용자 접근성을 보장합니다.  

This proof of concept works well, and users can access the application successfully.  
이 개념 검증은 잘 작동하며, 사용자는 애플리케이션에 성공적으로 접근할 수 있습니다.  
→ 단순하고 기능하는 초기 모델 완성.  

---

## Vertical Scaling: Upgrading the EC2 Instance  
## 수직 확장: EC2 인스턴스 업그레이드  
→ 서버 크기를 키워 성능을 향상합니다.  

As the application gains popularity, more users access it simultaneously.  
애플리케이션이 인기를 얻으면서 동시에 접속하는 사용자가 늘어납니다.  
→ 트래픽 증가 상황.  

The T2 micro instance becomes insufficient to handle the load.  
T2 micro 인스턴스는 부하를 감당하기에 부족해집니다.  
→ 더 큰 서버 필요.  

To address this, we perform vertical scaling by replacing the T2 micro instance with a larger instance type, such as an M5 large.  
이를 해결하기 위해 T2 micro 인스턴스를 M5 large 같은 더 큰 인스턴스로 교체하는 수직 확장을 수행합니다.  
→ 인스턴스 타입 변경 전략.  

This involves stopping the instance, changing its type, and restarting it.  
이는 인스턴스를 중지하고, 타입을 변경한 후, 다시 시작하는 과정입니다.  
→ 과정 중 다운타임 발생.  

The Elastic IP remains the same, so users can still access the application.  
Elastic IP는 그대로 유지되므로 사용자는 여전히 애플리케이션에 접근할 수 있습니다.  
→ 사용자 입장에서는 주소가 바뀌지 않음.  

However, this process causes downtime during the upgrade, which affects user experience.  
하지만 이 과정에서 업그레이드 동안 다운타임이 발생해 사용자 경험에 영향을 줍니다.  
→ 확장의 한계점 명시.  

---

## Horizontal Scaling: Adding Multiple EC2 Instances  
## 수평 확장: 여러 EC2 인스턴스 추가  
→ 여러 서버를 병렬로 운영하여 성능을 높입니다.  

To handle increasing traffic and reduce downtime, we move to horizontal scaling by adding multiple M5 large EC2 instances.  
증가하는 트래픽과 다운타임을 줄이기 위해 여러 개의 M5 large EC2 인스턴스를 추가하는 수평 확장을 진행합니다.  
→ 부하 분산 기반 구조.  

Each instance has its own Elastic IP.  
각 인스턴스는 고유한 Elastic IP를 가집니다.  
→ 관리 복잡성 증가.  

However, this approach requires users to be aware of multiple IP addresses to access the application, which complicates management and user experience.  
하지만 이 방식은 사용자가 여러 개의 IP 주소를 알아야 애플리케이션에 접근할 수 있어 관리와 사용자 경험을 복잡하게 만듭니다.  
→ 실제 서비스에는 적합하지 않은 방식.  

---

## DNS Management with Route 53  
## Route 53을 활용한 DNS 관리  
→ IP 복잡성을 줄이고 사용자 접근성을 단순화합니다.  

To simplify IP management, we remove Elastic IPs and leverage Route 53 DNS service.  
IP 관리 단순화를 위해 Elastic IP를 제거하고 Route 53 DNS 서비스를 활용합니다.  
→ DNS를 통해 접속 경로를 단일화.  

We set up an A record with a TTL of one hour for the domain api.whatisthetime.com.  
api.whatisthetime.com 도메인에 대해 TTL이 1시간인 A 레코드를 설정합니다.  
→ 일정 시간마다 IP 업데이트 가능.  

The A record returns a list of IP addresses corresponding to the EC2 instances.  
A 레코드는 EC2 인스턴스에 해당하는 IP 주소 목록을 반환합니다.  
→ 다수 인스턴스를 한 도메인에 연결 가능.  

Users query Route 53 to get the current IP addresses, which can change over time but remain synchronized.  
사용자는 Route 53을 통해 최신 IP 주소를 얻으며, 이는 시간이 지남에 따라 변경되지만 동기화 상태를 유지합니다.  
→ 사용자는 단일 도메인만 알면 됨.  

This eliminates the need to manage Elastic IPs manually.  
이는 Elastic IP를 수동으로 관리할 필요를 없앱니다.  
→ 관리 효율성 증가.  

However, a challenge arises when instances are added or removed dynamically.  
하지만 인스턴스가 동적으로 추가되거나 제거될 때 문제가 발생합니다.  
→ Route 53의 한계 등장.  

Due to the one-hour TTL, users may continue to receive outdated IP addresses of terminated instances, causing connection failures and perceived downtime until the TTL expires.  
1시간 TTL 때문에 사용자들은 종료된 인스턴스의 오래된 IP를 받게 되어 연결 실패와 다운타임이 발생할 수 있습니다.  
→ DNS 기반 확장의 한계.  

---

## Introducing Load Balancer for Improved Availability  
## 가용성 향상을 위한 로드 밸런서 도입  
→ DNS 한계를 극복하고 유연한 확장 지원.  

(… 이하 동일한 방식으로 각 문장 번역 + 설명 유지 …)  

---

## Summary of Architectural Evolution  
## 아키텍처 발전 요약  
→ 설계가 단계적으로 어떻게 발전했는지 정리.  

- Started with a single EC2 instance with Elastic IP.  
- Elastic IP가 있는 단일 EC2 인스턴스로 시작.  
→ 가장 기본 구조.  

- Scaled vertically by upgrading instance type, causing downtime.  
- 인스턴스 타입 업그레이드를 통한 수직 확장, 다운타임 발생.  
→ 성능 ↑, 가용성 ↓  

- Scaled horizontally by adding multiple instances, managing multiple IPs.  
- 여러 인스턴스를 추가하는 수평 확장, 다수 IP 관리 필요.  
→ 복잡성 ↑  

- Improved DNS management using Route 53 A records and alias records.  
- Route 53 A 레코드 및 Alias 레코드로 DNS 관리 개선.  
→ 단순화 및 확장성 ↑  

- Introduced load balancer with health checks for traffic distribution.  
- 트래픽 분산을 위한 로드 밸런서와 헬스 체크 도입.  
→ 안정적 분산 처리 가능.  

- Automated scaling with auto-scaling groups.  
- 오토 스케일링 그룹을 통한 자동 확장.  
→ 관리 효율성 ↑  

- Enhanced availability with multi-AZ deployment.  
- 멀티 AZ 배포로 가용성 강화.  
→ 장애 복원력 확보.  

- Optimized costs using reserved and spot instances.  
- 예약 인스턴스와 스팟 인스턴스로 비용 최적화.  
→ 성능-비용 균형.  

좋습니다 👍 그러면 앞부분과 똑같은 방식( **한 줄 원문 → 한 줄 번역 → 설명** )을 끝까지 이어서 해드릴게요. 이어서 작성해드리겠습니다.

```markdown
## Introducing Load Balancer for Improved Availability  
## 가용성 향상을 위한 로드 밸런서 도입  
→ DNS 기반 방식의 한계를 보완하기 위해 로드 밸런서를 도입합니다.  

To address the limitations of DNS-based IP management, we introduce a load balancer (ELB).  
DNS 기반 IP 관리의 한계를 해결하기 위해 로드 밸런서(ELB)를 도입합니다.  
→ ELB는 동적 IP와 인스턴스 상태 관리 문제를 해결해줍니다.  

We deploy private EC2 instances within the same availability zone and place the ELB as the public-facing endpoint.  
동일 가용 영역(AZ) 내에 프라이빗 EC2 인스턴스를 배포하고, ELB를 외부 접근 지점으로 설정합니다.  
→ 사용자는 ELB를 통해서만 접근합니다.  

The ELB performs health checks to ensure traffic is only routed to healthy instances.  
ELB는 헬스 체크를 수행하여 정상 인스턴스로만 트래픽을 라우팅합니다.  
→ 자동으로 불량 인스턴스를 배제합니다.  

Security groups restrict traffic so that EC2 instances only accept requests from the ELB.  
보안 그룹은 EC2 인스턴스가 ELB로부터의 요청만 수락하도록 제한합니다.  
→ 직접 접근을 막아 보안을 강화합니다.  

Since the ELB's IP address changes dynamically, we cannot use an A record.  
ELB의 IP 주소는 동적으로 변경되므로 A 레코드를 사용할 수 없습니다.  
→ 고정 IP 기반 접근이 불가능합니다.  

Instead, we use a Route 53 alias record pointing to the ELB.  
대신 Route 53 Alias 레코드를 ELB에 연결하여 사용합니다.  
→ Route 53이 동적 IP를 자동 처리합니다.  

Users query the alias record to reach the load balancer, which distributes traffic evenly across the EC2 instances.  
사용자는 Alias 레코드를 통해 로드 밸런서에 접속하며, 로드 밸런서는 트래픽을 EC2 인스턴스에 고르게 분산합니다.  
→ 안정적이고 자동화된 트래픽 분산 구조입니다.  

This setup allows adding or removing instances without downtime, thanks to health checks and dynamic routing.  
이 설정 덕분에 헬스 체크와 동적 라우팅으로 인스턴스를 추가하거나 제거해도 다운타임이 발생하지 않습니다.  
→ 확장성과 무중단 운영이 가능합니다.  

---

## Auto-Scaling Group for Dynamic Instance Management  
## 동적 인스턴스 관리를 위한 오토 스케일링 그룹  
→ 인스턴스를 자동으로 증감 관리하여 효율을 극대화합니다.  

Manually managing EC2 instances remains challenging.  
EC2 인스턴스를 수동으로 관리하는 것은 여전히 어렵습니다.  
→ 규모가 커지면 사람이 직접 관리하기 힘듭니다.  

To automate scaling, we deploy an auto-scaling group managing private EC2 instances across availability zones.  
확장을 자동화하기 위해 여러 가용 영역(AZ)에 걸쳐 프라이빗 EC2 인스턴스를 관리하는 오토 스케일링 그룹을 배포합니다.  
→ 자동화로 관리 부담을 줄입니다.  

The auto-scaling group adjusts the number of instances based on demand, scaling out during peak times and scaling in during low usage periods.  
오토 스케일링 그룹은 수요에 따라 인스턴스 수를 조정하며, 피크 시간에는 확장하고 사용량이 적을 때는 축소합니다.  
→ 자원 활용을 최적화합니다.  

This ensures optimal resource utilization and cost efficiency.  
이를 통해 자원 활용을 최적화하고 비용 효율성을 보장합니다.  
→ 성능과 비용의 균형을 유지합니다.  

---

## Multi-AZ Deployment for High Availability  
## 고가용성을 위한 멀티 AZ 배포  
→ 장애 대응을 위한 고급 아키텍처 기법입니다.  

To improve resilience, we deploy the application across multiple availability zones (AZs).  
복원력을 높이기 위해 애플리케이션을 여러 가용 영역(AZ)에 걸쳐 배포합니다.  
→ 장애 시 다른 AZ가 서비스 지속.  

The ELB spans three AZs, and the auto-scaling group launches instances in each AZ, for example, two instances in AZ1, two in AZ2, and one in AZ3.  
ELB는 3개의 AZ에 걸쳐 있으며, 오토 스케일링 그룹은 각 AZ에 인스턴스를 배포합니다. 예를 들어 AZ1에는 2개, AZ2에는 2개, AZ3에는 1개를 배포합니다.  
→ 트래픽이 여러 AZ로 분산됩니다.  

If one AZ fails, the remaining AZs continue serving traffic, ensuring high availability and fault tolerance.  
한 AZ가 실패하더라도 나머지 AZ가 트래픽을 계속 처리하여 고가용성과 장애 허용성을 보장합니다.  
→ 단일 장애 지점을 제거합니다.  

---

## Cost Optimization with Reserved and Spot Instances  
## 예약 인스턴스와 스팟 인스턴스를 통한 비용 최적화  
→ 성능과 비용의 균형을 잡는 전략입니다.  

Knowing that a minimum number of instances must always run, we reserve capacity for these baseline instances to reduce costs.  
최소한 항상 실행되어야 하는 인스턴스 수를 알고 있으므로, 해당 기준 인스턴스에 대해 예약 용량을 확보해 비용을 절감합니다.  
→ 예약 인스턴스는 장기 비용 절감 효과.  

Additional instances launched during scaling can be on-demand or spot instances, which are cheaper but may be terminated unexpectedly.  
확장 시 추가되는 인스턴스는 온디맨드나 스팟 인스턴스로 실행할 수 있는데, 이는 더 저렴하지만 예기치 않게 종료될 수 있습니다.  
→ 가변적 부하에 적합.  

This strategy balances cost savings with availability requirements.  
이 전략은 비용 절감과 가용성 요구 사항의 균형을 맞춥니다.  
→ 안정성과 절약을 동시에 달성.  

---

## Summary of Architectural Evolution  
## 아키텍처 발전 요약  
→ 아키텍처가 점진적으로 발전한 과정을 정리합니다.  

Started with a single EC2 instance with Elastic IP.  
Elastic IP가 있는 단일 EC2 인스턴스로 시작했습니다.  
→ 초기 구조.  

Scaled vertically by upgrading instance type, causing downtime.  
인스턴스 타입 업그레이드를 통한 수직 확장으로 다운타임이 발생했습니다.  
→ 성능 ↑, 가용성 ↓  

Scaled horizontally by adding multiple instances, managing multiple IPs.  
여러 인스턴스를 추가하는 수평 확장을 통해 다수 IP를 관리했습니다.  
→ 확장성 ↑, 관리 복잡성 ↑  

Improved DNS management using Route 53 A records and alias records.  
Route 53 A 레코드와 Alias 레코드를 통해 DNS 관리를 개선했습니다.  
→ 접근 단순화.  

Introduced load balancer with health checks for traffic distribution.  
헬스 체크가 포함된 로드 밸런서를 도입해 트래픽을 분산했습니다.  
→ 안정성 ↑  

Automated scaling with auto-scaling groups.  
오토 스케일링 그룹으로 자동 확장을 구현했습니다.  
→ 관리 효율 ↑  

Enhanced availability with multi-AZ deployment.  
멀티 AZ 배포로 가용성을 강화했습니다.  
→ 장애 허용성 ↑  

Optimized costs using reserved and spot instances.  
예약 및 스팟 인스턴스를 사용해 비용을 최적화했습니다.  
→ 비용 효율성 ↑  

This journey illustrates the solutions architect's role in understanding requirements and designing scalable, available, and cost-effective architectures.  
이 여정은 요구사항을 이해하고 확장 가능하며, 고가용성, 비용 효율적인 아키텍처를 설계하는 솔루션 아키텍트의 역할을 보여줍니다.  
→ 실무적으로 매우 중요한 역량.  

---

## Key Takeaways  
## 핵심 요약  
→ 이 사례에서 배운 핵심 교훈입니다.  

Started with a simple EC2 instance with an Elastic IP to serve time queries.  
시간 질의 처리를 위해 Elastic IP가 있는 단순한 EC2 인스턴스로 시작했습니다.  
→ 기본 출발점.  

Scaled vertically by upgrading instance type, causing downtime during upgrade.  
인스턴스 타입 업그레이드를 통한 수직 확장 과정에서 다운타임이 발생했습니다.  
→ 단점 확인.  

Scaled horizontally by adding multiple EC2 instances, managing multiple Elastic IPs.  
여러 EC2 인스턴스를 추가하고 다수 Elastic IP를 관리하는 수평 확장을 수행했습니다.  
→ 관리 복잡성 증가.  

Improved DNS management using Route 53 A records and later Alias records with a load balancer.  
Route 53 A 레코드와 이후 Alias 레코드 및 로드 밸런서를 활용해 DNS 관리를 개선했습니다.  
→ 단일 진입점 확보.  

Introduced a load balancer with health checks to distribute traffic and avoid downtime.  
헬스 체크를 수행하는 로드 밸런서를 도입하여 트래픽을 분산하고 다운타임을 방지했습니다.  
→ 안정성 강화.  

Implemented auto-scaling groups for dynamic scaling based on demand.  
수요 기반 동적 확장을 위해 오토 스케일링 그룹을 구현했습니다.  
→ 효율적 자원 사용.  

Enhanced availability by deploying multi-AZ architecture to withstand zone failures.  
멀티 AZ 아키텍처를 배포하여 가용성을 강화하고 AZ 장애를 견뎌냈습니다.  
→ 고도화된 안정성.  

Optimized costs by reserving capacity for minimum instances and using on-demand or spot instances for scaling.  
최소 인스턴스는 예약으로 확보하고, 확장에는 온디맨드 및 스팟 인스턴스를 사용해 비용을 최적화했습니다.  
→ 비용-성능 균형.  

---

🎮 **게임보상 획득!** 🎁  
- 아키텍처 전략 이해력 +150  
- 확장성/가용성 지식 +120  
- 비용 최적화 능력 +100  
- “AWS 솔루션 아키텍트 Lv.2 달성!” 🏆  


