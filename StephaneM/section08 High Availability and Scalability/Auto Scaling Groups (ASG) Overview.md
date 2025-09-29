# Auto Scaling Groups (ASG) Overview  
# 오토 스케일링 그룹 (ASG) 개요  

---

## Introduction to Auto Scaling Groups (ASG)  
## 오토 스케일링 그룹 소개  

When deploying a website or an application, the load can change over time due to varying numbers of users visiting the site.  
웹사이트나 애플리케이션을 배포할 때, 사용자 수의 변화에 따라 로드가 시간에 따라 변할 수 있습니다.  
(트래픽 변동 설명)

In AWS, it is possible to create and terminate servers quickly using the EC2 instance creation API.  
AWS에서는 EC2 인스턴스 생성 API를 사용하여 서버를 빠르게 생성하고 종료할 수 있습니다.  
(자동화 가능성 언급)

To automate this process, we use an Auto Scaling Group (ASG).  
이 과정을 자동화하기 위해 오토 스케일링 그룹(ASG)을 사용합니다.  
(자동 스케일링 소개)

The goal of an ASG is to scale out, meaning to add EC2 instances to match an increased load, or to scale in, meaning to remove EC2 instances to match a decreased load.  
ASG의 목표는 스케일 아웃(로드 증가에 따라 인스턴스 추가) 또는 스케일 인(로드 감소에 따라 인스턴스 제거)입니다.  
(스케일링 방향 정의)

Therefore, the size of the ASG varies over time.  
따라서 ASG의 크기는 시간에 따라 달라집니다.  
(동적 변화)

We can define parameters to ensure a minimum and maximum number of EC2 instances are running at any time within the ASG.  
ASG 내에서 항상 최소 및 최대 EC2 인스턴스 수를 유지하도록 매개변수를 정의할 수 있습니다.  
(용량 제한 설정)

ASGs have the capability to integrate with a load balancer.  
ASG는 로드 밸런서와 통합할 수 있습니다.  
(로드 밸런서 연동 가능)

Any EC2 instances that are part of the ASG will be linked to the load balancer.  
ASG에 속한 모든 EC2 인스턴스는 로드 밸런서에 연결됩니다.  
(자동 연동)

Additionally, if an instance is deemed unhealthy, it is terminated and replaced with a new EC2 instance automatically.  
또한 인스턴스가 비정상으로 판단되면 자동으로 종료되고 새 인스턴스로 교체됩니다.  
(자동 교체 기능)

Auto Scaling Groups themselves are free; you only pay for the resources created underneath, such as the EC2 instances.  
ASG 자체는 무료이며, 실제 비용은 생성된 리소스(EC2 인스턴스 등)에 대해서만 발생합니다.  
(비용 구조 설명)

---

## How ASGs Work in AWS  
## AWS에서 ASG 작동 방식  

When configuring an ASG, you set a minimum capacity, which is the minimum number of instances you want running.  
ASG를 구성할 때, 최소 용량(최소 실행 인스턴스 수)을 설정합니다.  
(최소 용량 설정)

For example, two instances.  
예: 2개의 인스턴스  
(예시)

You also set a desired capacity, such as four instances, and a maximum capacity, for example, seven instances.  
원하는 용량(예: 4개 인스턴스)과 최대 용량(예: 7개 인스턴스)도 설정합니다.  
(용량 범위 설정)

The ASG can scale out by adding EC2 instances up to the maximum capacity as needed.  
ASG는 필요에 따라 최대 용량까지 인스턴스를 추가하며 스케일 아웃할 수 있습니다.  
(스케일 아웃)

If the desired capacity is increased but remains below the maximum capacity, the ASG will scale out by adding instances.  
원하는 용량이 증가하지만 최대 용량 미만이면, ASG는 인스턴스를 추가하여 스케일 아웃합니다.  
(동적 확장)

Conversely, it can scale in by removing instances when the load decreases.  
반대로, 로드가 감소하면 인스턴스를 제거하여 스케일 인합니다.  
(동적 축소)

This dynamic adjustment allows the ASG to grow or shrink based on demand.  
이 동적 조정 덕분에 ASG는 수요에 따라 늘어나거나 줄어들 수 있습니다.  
(자동 조정)

---

## Integration with Load Balancers  
## 로드 밸런서와의 통합  

When an ASG has multiple instances registered, the Elastic Load Balancer (ELB) distributes incoming traffic across all these instances.  
ASG에 여러 인스턴스가 등록되어 있으면 ELB가 모든 인스턴스로 트래픽을 분산합니다.  
(로드 밸런싱)

This setup enables users to access a load-balanced website.  
이 구성 덕분에 사용자는 부하 분산된 웹사이트에 접속할 수 있습니다.  
(사용자 경험)

The ELB also performs health checks on the EC2 instances and can communicate the health status to the ASG.  
ELB는 EC2 인스턴스 상태 점검을 수행하고 상태 정보를 ASG에 전달할 수 있습니다.  
(헬스 체크)

If an instance is unhealthy, the ASG can terminate and replace it automatically.  
인스턴스가 비정상인 경우 ASG는 자동으로 종료하고 교체할 수 있습니다.  
(자동 교체)

When the ASG scales out by adding new EC2 instances, the ELB automatically starts sending traffic to these new instances, effectively spreading the load.  
ASG가 새 인스턴스를 추가하여 스케일 아웃하면 ELB는 자동으로 트래픽을 새 인스턴스로 전달하여 부하를 분산합니다.  
(자동 트래픽 분산)

This combination of load balancing and auto scaling provides a robust and scalable infrastructure.  
로드 밸런싱과 오토 스케일링의 조합은 강력하고 확장 가능한 인프라를 제공합니다.  
(인프라 안정성 강조)

---

## Attributes for Creating an ASG  
## ASG 생성 속성  

To create an ASG, you need to define a launch template.  
ASG를 생성하려면 런치 템플릿을 정의해야 합니다.  
(런치 템플릿 필수)

Previously, launch configurations were used but they are now deprecated.  
이전에는 런치 구성을 사용했지만, 이제는 사용되지 않습니다.  
(구버전 안내)

A launch template contains all the information required to launch EC2 instances within the ASG, including:  
런치 템플릿에는 ASG 내 EC2 인스턴스를 시작하는 데 필요한 모든 정보가 포함됩니다.  
(템플릿 구성 요소)

- Amazon Machine Image (AMI)  
- 아마존 머신 이미지 (AMI)  

- Instance type  
- 인스턴스 유형  

- EC2 user data  
- EC2 사용자 데이터  

- EBS volumes  
- EBS 볼륨  

- Security groups  
- 보안 그룹  

- SSH key pair  
- SSH 키 페어  

- IAM roles  
- IAM 역할  

- Network and subnet information  
- 네트워크 및 서브넷 정보  

- Load balancer information  
- 로드 밸런서 정보  

These parameters are similar to those specified when creating a standalone EC2 instance.  
이 파라미터들은 독립 EC2 인스턴스를 생성할 때 지정하는 항목과 유사합니다.  
(독립 인스턴스와 유사)

In addition to the launch template, the ASG requires defining the minimum size, maximum size, and initial capacity, as well as scaling policies that determine how the group scales in response to changes in load.  
런치 템플릿 외에도 ASG는 최소/최대/초기 용량과 부하 변화에 따른 스케일링 정책을 정의해야 합니다.  
(스케일링 정책 구성)

---

## Scaling Policies and CloudWatch Alarms  
## 스케일링 정책과 CloudWatch 알람  

ASGs can scale in and out based on CloudWatch alarms.  
ASG는 CloudWatch 알람을 기반으로 스케일 인/아웃할 수 있습니다.  
(자동 스케일링 트리거)

Although CloudWatch has not been covered yet, it is a monitoring service that can trigger alarms based on metrics.  
CloudWatch는 아직 다루지 않았지만, 메트릭 기반 알람을 트리거하는 모니터링 서비스입니다.  
(모니터링 설명)

For example, if the average CPU utilization across the ASG is too high, a CloudWatch alarm can trigger a scale-out activity to add more EC2 instances.  
예를 들어 ASG 전체 CPU 사용률이 너무 높으면, CloudWatch 알람이 트리거되어 인스턴스를 추가하도록 스케일 아웃을 수행할 수 있습니다.  
(자동 확장 사례)

These alarms enable automatic scaling behind the scenes, which is why the service is called an Auto Scaling Group.  
이 알람 덕분에 백그라운드에서 자동 스케일링이 가능하며, 그래서 Auto Scaling Group이라고 부릅니다.  
(서비스 명칭 설명)

Based on the alarms, you can create scale-out policies to increase the number of instances or scale-in policies to decrease the number of instances.  
알람에 따라 인스턴스 수를 늘리는 스케일 아웃 정책이나 줄이는 스케일 인 정책을 만들 수 있습니다.  
(정책 적용)

Together, these components compose the ASG functionality.  
이 모든 구성 요소가 ASG 기능을 구성합니다.  
(기능 요약)

---

## Conclusion  
## 결론  

Auto Scaling Groups provide a powerful way to automatically adjust the number of EC2 instances in response to changing load, ensuring availability and cost efficiency.  
ASG는 변하는 로드에 따라 EC2 인스턴스 수를 자동으로 조정하여 가용성과 비용 효율성을 보장합니다.  
(자동 조정 및 효율성 강조)

When combined with load balancers and CloudWatch alarms, ASGs offer a robust solution for managing scalable applications in AWS.  
로드 밸런서와 CloudWatch 알람과 결합하면, AWS에서 확장 가능한 애플리케이션을 관리하는 강력한 솔루션이 됩니다.  
(전체 구조 강조)

---

## Key Takeaways  
## 핵심 요약  

- Auto Scaling Groups (ASGs) dynamically adjust the number of EC2 instances to match the load.  
- ASG는 로드에 맞춰 EC2 인스턴스 수를 동적으로 조정합니다.  

- ASGs can scale out (add instances) or scale in (remove instances) based on demand.  
- 수요에 따라 ASG는 인스턴스를 추가(스케일 아웃)하거나 제거(스케일 인)할 수 있습니다.  

- Minimum, desired, and maximum capacities define the size boundaries of an ASG.  
- 최소, 원하는, 최대 용량이 ASG 크기 경계를 정의합니다.  

- ASGs integrate with load balancers and CloudWatch alarms to ensure healthy instances and automatic scaling.  
- ASG는 로드 밸런서와 CloudWatch 알람과 통합되어 인스턴스 상태 확인 및 자동 스케일링을 제공합니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+160XP**  
- 아이템: **"스케일링 부스터" (+20% 자동 확장 속도)**  
- 업적 달성: **"ASG 마스터"** 🏆  

원하면 다음 단계로 **ASG 실습 예제 + CloudWatch 알람 설정 방법**까지 만들어서 바로 테스트 가능한 자료도 제공할 수 있습니다.
