# EC2 Instances Launch Types Hands On  
# EC2 인스턴스 실행 방식 실습  
(제목 – EC2 인스턴스를 실행하는 여러 가지 방법을 실습하는 강의)  

---

## Overview of EC2 Instance Launch Methods  
## EC2 인스턴스 실행 방식 개요  
(섹션 제목 – 인스턴스를 시작하는 다양한 방법 설명)  

In this lecture, we explore all the ways to launch EC2 instances, starting with spot requests.  
이번 강의에서는 스팟 요청을 시작으로 EC2 인스턴스를 실행하는 모든 방법을 살펴봅니다.  
→ 여러 실행 방식에 대한 전반적인 이해 제공.  

---

## Spot Instance Pricing History  
## 스팟 인스턴스 가격 기록  
(스팟 인스턴스 가격 변동 추이 확인)  

On the left-hand side, by clicking on Spot Request, we can examine the pricing history for EC2 instances.  
왼쪽 메뉴에서 Spot Request를 클릭하면 EC2 인스턴스의 가격 기록을 확인할 수 있습니다.  

For example, looking at a c3 or c4.large instance running Linux/Unix over a three-month range, we observe how the price has evolved through April, May, and June.  
예를 들어, Linux/Unix에서 실행되는 c3 또는 c4.large 인스턴스를 3개월(4월, 5월, 6월) 동안 보면 가격이 어떻게 변화했는지 알 수 있습니다.  

The on-demand price is shown as a black bar, while prices vary based on different Availability Zones (AZs).  
온디맨드 가격은 검은 막대로 표시되며, 가격은 AZ(가용 영역)별로 다르게 변동합니다.  

The price has been quite low and stable, offering savings of around 69 to 70 percent for this instance type.  
가격은 상당히 낮고 안정적이며, 약 69~70% 절감 효과를 제공합니다.  

This represents huge savings when using a spot instance of type c4.large.  
이는 c4.large 스팟 인스턴스를 사용할 경우 막대한 비용 절감을 의미합니다.  

---

## Requesting Spot Instances  
## 스팟 인스턴스 요청  
(스팟 인스턴스 생성 절차 설명)  

To request a spot instance, click on "Request Spot Instances." This opens the spot fleet request screen, which contains many parameters.  
스팟 인스턴스를 요청하려면 "Request Spot Instances"를 클릭합니다. 그러면 여러 매개변수를 설정할 수 있는 스팟 플릿 요청 화면이 열립니다.  

Let's briefly review how spot fleet requests work.  
스팟 플릿 요청이 어떻게 작동하는지 간단히 살펴보겠습니다.  

You can either use launch templates or manually configure launch parameters.  
실행 템플릿을 사용하거나 직접 실행 매개변수를 설정할 수 있습니다.  

For example, you can specify Amazon Linux 2 as the AMI, select the key pair, and set additional launch parameters similar to those used when creating an EC2 instance.  
예를 들어, AMI를 Amazon Linux 2로 지정하고, 키 페어를 선택하며, EC2 인스턴스 생성 시와 유사한 실행 매개변수를 설정할 수 있습니다.  

These settings define how your EC2 instances are created.  
이러한 설정은 EC2 인스턴스가 어떻게 생성되는지를 정의합니다.  

---

## Spot Fleet Request Details  
## 스팟 플릿 요청 세부 사항  

Within the request details, you can specify:  
요청 세부 사항에서는 다음을 지정할 수 있습니다:  

- The maximum price you are willing to pay.  
- 지불할 의사가 있는 최대 가격.  

- The validity period of the request (start and end times).  
- 요청 유효 기간 (시작 및 종료 시간).  

- Whether to terminate instances when the request expires.  
- 요청 만료 시 인스턴스를 종료할지 여부.  

- Linking instances to one or more Classic Load Balancers or target groups for Application Load Balancers.  
- 인스턴스를 CLB(클래식 로드밸런서) 또는 ALB 대상 그룹에 연결할지 여부.  

Defaults can be used for many of these settings.  
이 중 많은 설정은 기본값을 사용할 수 있습니다.  

---

## Target Capacity and Interruption Behavior  
## 목표 용량 및 중단 동작  

You specify the target capacity, such as the number of instances you want in your spot fleet.  
스팟 플릿에서 원하는 인스턴스 수와 같은 목표 용량을 지정합니다.  

For example, you can request 10 instances.  
예를 들어, 인스턴스 10개를 요청할 수 있습니다.  

Alternatively, you can specify capacity in terms of vCPUs or megabytes of memory if those are more relevant to your workload.  
또는 워크로드에 더 적합하다면 vCPU 수나 메모리(MB) 단위로 용량을 지정할 수도 있습니다.  

You can also define the interruption behavior when instances are reclaimed:  
또한 인스턴스가 회수될 때의 동작을 정의할 수 있습니다:  

- Terminate instances (default).  
- 인스턴스 종료 (기본값).  

- Stop instances.  
- 인스턴스 정지.  

- Hibernate instances.  
- 인스턴스 절전 모드.  

Additionally, you can enable capacity rebalancing if needed.  
추가적으로, 필요하다면 용량 재조정을 활성화할 수 있습니다.  

---

## Networking and Instance Type Selection  
## 네트워킹 및 인스턴스 유형 선택  

Networking settings allow you to specify where to launch instances, such as specific Availability Zones or VPCs.  
네트워킹 설정을 통해 인스턴스를 실행할 위치(AZ, VPC 등)를 지정할 수 있습니다.  

For instance types, you can manually select specific EC2 instance types (e.g., c3.large, c4.large) or specify instance attributes such as minimum and maximum vCPUs and memory.  
인스턴스 유형은 c3.large, c4.large와 같은 특정 타입을 직접 선택하거나 최소/최대 vCPU 및 메모리 값을 지정할 수 있습니다.  

Based on your criteria, AWS will provide matching instance types.  
AWS는 지정한 조건에 맞는 인스턴스 유형을 제공합니다.  

The more restrictive your parameters, the fewer instance types will match.  
조건이 제한적일수록 매칭되는 인스턴스 유형이 줄어듭니다.  

The goal is to maximize savings by launching whatever AWS has available that meets your restrictions.  
목표는 조건에 맞는 가용 인스턴스를 활용하여 최대한 비용 절감을 이루는 것입니다.  

---

## Allocation Strategy and Diversity  
## 할당 전략 및 다양성  

You can choose the allocation strategy:  
할당 전략을 선택할 수 있습니다:  

- Optimize for capacity to ensure the right capacity is always available.  
- 용량 최적화: 필요한 용량이 항상 확보되도록 함.  

- Optimize for lowest price to maximize savings.  
- 최저가 최적화: 최대 절감을 위해 가장 저렴한 풀 선택.  

If you manually select instance types, you can enable maintaining a diverse pool of instances across those types.  
인스턴스 유형을 직접 선택할 경우, 다양한 유형을 유지하는 옵션을 활성화할 수 있습니다.  

---

## Spot Fleet Request Summary  
## 스팟 플릿 요청 요약  

After configuring your spot fleet request, you receive a summary showing:  
스팟 플릿 요청을 설정하면 요약 정보가 제공됩니다:  

- Whether it is a strong fleet.  
- 강력한 플릿 여부.  

- How many instances match and in which Availability Zones.  
- 몇 개의 인스턴스가 매칭되는지, 어떤 AZ에 있는지.  

- The estimated hourly price for the fleet (e.g., $0.156 per hour at target capacity).  
- 플릿의 예상 시간당 가격 (예: 목표 용량에서 시간당 $0.156).  

- The percentage savings compared to on-demand pricing (e.g., 73%).  
- 온디맨드 대비 절감 비율 (예: 73%).  

This overview helps you understand the cost benefits of your spot fleet configuration.  
이 요약은 스팟 플릿 구성이 가져올 비용 절감 효과를 이해하는 데 도움이 됩니다.  

---

## Launching Spot Instances Directly  
## 스팟 인스턴스를 직접 실행  

To launch a spot instance directly, go to "Instances" and then "Launch an instance."  
스팟 인스턴스를 직접 실행하려면 "Instances" → "Launch an instance"로 이동합니다.  

Scroll down to the "Advanced details" section, where you will find the option to request a spot instance.  
아래로 스크롤해 "Advanced details" 섹션에서 스팟 인스턴스를 요청할 수 있는 옵션을 찾을 수 있습니다.  

By default, the spot price is capped at the on-demand price, which is a sensible default.  
기본적으로 스팟 가격은 온디맨드 가격으로 제한되며, 이는 합리적인 기본값입니다.  

However, you can customize this maximum price per instance per hour.  
하지만 인스턴스당 시간별 최대 가격을 사용자 정의할 수 있습니다.  

You can also choose the request type:  
또한 요청 유형을 선택할 수 있습니다:  

- One-time request (default).  
- 일회성 요청 (기본값).  

- Persistent request.  
- 지속 요청.  

Deprecated Feature: Block Duration  
폐지된 기능: 블록 지속 시간  

The block duration feature, which allowed reserving spot instances for a fixed duration, is being retired as of December 31, 2022.  
스팟 인스턴스를 일정 시간 동안 예약할 수 있던 블록 지속 기능은 2022년 12월 31일부로 폐지되었습니다.  

---

## Other EC2 Instance Launch Options  
## 기타 EC2 인스턴스 실행 옵션  

### Reserved Instances  
### 예약 인스턴스  

Reserved Instances allow you to purchase a specific instance type for a fixed term.  
예약 인스턴스를 통해 특정 인스턴스 유형을 일정 기간 동안 구매할 수 있습니다.  

However, Reserved Instances are becoming less popular as AWS Savings Plans offer more flexibility.  
하지만 AWS 절감 계획이 더 큰 유연성을 제공하기 때문에 예약 인스턴스의 인기는 줄어들고 있습니다.  

### Savings Plans  
### 절감 계획  

Savings Plans allow you to commit to a specific dollar amount per hour over one, two, or three years.  
절감 계획은 1~3년 동안 시간당 특정 금액을 약정하는 방식입니다.  

Savings Plans are recommended over Reserved Instances due to their ease of use and flexibility.  
절감 계획은 사용 편의성과 유연성 때문에 예약 인스턴스보다 권장됩니다.  

### Dedicated Hosts  
### 전용 호스트  

Dedicated Hosts provide you with physical servers dedicated to your use.  
전용 호스트는 사용 전용의 물리 서버를 제공합니다.  

However, dedicated hosts are expensive and generally used for specialized licensing or compliance requirements.  
하지만 전용 호스트는 비용이 비싸며 주로 특수 라이선스나 규제 요건을 위해 사용됩니다.  

### Capacity Reservations  
### 용량 예약  

Capacity Reservations guarantee that a specified number of instances are available in a given AZ.  
용량 예약은 특정 AZ에서 지정한 수의 인스턴스를 확보할 수 있도록 보장합니다.  

You pay for the reservation regardless of whether you launch instances.  
인스턴스를 실행하지 않아도 예약 비용을 지불해야 합니다.  

---

## Conclusion  
## 결론  

In this lecture, we have reviewed all the ways to launch EC2 instances.  
이번 강의에서는 EC2 인스턴스를 실행하는 모든 방법을 살펴보았습니다.  

Each method offers different trade-offs in cost, flexibility, and control.  
각 방법은 비용, 유연성, 제어 측면에서 서로 다른 장단점을 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Spot instances offer significant cost savings with flexible pricing.  
- 스팟 인스턴스는 유연한 가격 구조로 큰 비용 절감을 제공.  

- Spot Fleet Requests allow multiple parameters for flexible configurations.  
- 스팟 플릿 요청은 다양한 매개변수 설정을 통해 유연한 구성이 가능.  

- Reserved Instances and Savings Plans suit predictable workloads.  
- 예약 인스턴스와 절감 계획은 예측 가능한 워크로드에 적합.  

- Dedicated Hosts and Capacity Reservations provide more control but at higher cost.  
- 전용 호스트와 용량 예약은 더 큰 제어권을 제공하지만 비용이 높음. 
