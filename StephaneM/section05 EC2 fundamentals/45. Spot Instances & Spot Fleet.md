# Spot Instances & Spot Fleet  
# 스팟 인스턴스 & 스팟 플릿  
(제목 – EC2 스팟 인스턴스와 플릿 개요)  

---

## Introduction to EC2 Spot Instances  
## EC2 스팟 인스턴스 소개  
(섹션 제목 – EC2 스팟 인스턴스에 대한 설명 시작)  

EC2 Spot Instances provide significant cost savings, offering discounts up to 90% compared to On-Demand instances.  
EC2 스팟 인스턴스는 온디맨드 인스턴스 대비 최대 90%까지 비용 절감을 제공합니다.  
→ 매우 저렴한 비용으로 인스턴스를 사용할 수 있는 옵션임.  

This is achieved by defining a maximum spot price that you are willing to pay for the instance.  
이는 인스턴스에 대해 지불할 최대 스팟 가격을 정의함으로써 가능합니다.  
→ 사용자가 지불 가능한 한도를 설정하는 방식.  

As long as the current spot price remains below this maximum, you retain the instance.  
현재 스팟 가격이 최대치 이하라면 인스턴스를 계속 유지할 수 있습니다.  
→ 가격이 낮게 유지될 때는 안정적으로 사용 가능.  

---

## Spot Price Behavior  
## 스팟 가격 동작 방식  
(스팟 가격 변동에 대한 설명)  

The hourly spot price fluctuates based on supply and demand, varying up and down.  
스팟 가격은 시간 단위로 수요와 공급에 따라 변동합니다.  
→ 가격은 고정되지 않고 실시간으로 달라짐.  

If the spot price rises above your defined maximum price, you have two options within a two-minute grace period:  
스팟 가격이 설정한 최대치보다 높아지면, 2분의 유예 시간 내에 두 가지 옵션을 선택할 수 있습니다:  
→ 갑작스런 종료 전에 준비 시간을 줌.  

- Stop your instance, preserving its state to restart later when prices drop.  
- 인스턴스를 정지하여 상태를 보존하고, 나중에 가격이 낮아지면 다시 시작하기.  
→ 중단은 하지만 데이터는 유지됨.  

- Terminate your instance if you do not need to preserve its state, starting fresh upon next launch.  
- 상태를 유지할 필요가 없다면 인스턴스를 종료하고, 이후 새로 시작하기.  
→ 필요 없는 경우 그냥 완전히 종료.  

These strategies depend on your workload requirements.  
이러한 전략은 워크로드 요구사항에 따라 다릅니다.  
→ 안정성이 필요한지, 비용만 중요한지에 따라 선택.  

---

## Spot Blocks  
## 스팟 블록  
(중단 없는 사용을 위한 예약 옵션)  

To avoid interruptions, you can use a spot block, which reserves a spot instance for a specified duration between one to six hours.  
중단을 피하려면 스팟 블록을 사용할 수 있으며, 이는 1~6시간 동안 스팟 인스턴스를 예약합니다.  
→ 단기 안정적인 워크로드에 적합.  

During this block, the instance is guaranteed not to be reclaimed, except in rare situations.  
이 기간 동안은 드물게 예외적인 경우를 제외하고 인스턴스가 회수되지 않습니다.  
→ 안정성을 제공.  

This provides more stability for workloads that require uninterrupted compute time.  
이는 중단 없는 계산이 필요한 워크로드에 더 많은 안정성을 제공합니다.  
→ 배치 처리 같은 작업에 적합.  

---

## Use Cases for Spot Instances  
## 스팟 인스턴스 사용 사례  
(어떤 상황에서 유용한지 설명)  

Spot Instances are ideal for batch jobs, data analysis, and workloads resilient to failures.  
스팟 인스턴스는 배치 작업, 데이터 분석, 장애에 강한 워크로드에 이상적입니다.  
→ 실패해도 괜찮은 작업에 잘 맞음.  

They are not recommended for critical jobs or databases due to the possibility of interruptions.  
중단 가능성이 있기 때문에 중요한 작업이나 데이터베이스에는 권장되지 않습니다.  
→ 안정성이 필수인 환경에는 부적합.  

---

## Spot Instance Pricing  
## 스팟 인스턴스 가격 책정  
(가격이 어떻게 결정되는지 설명)  

The spot price varies by availability zone and over time.  
스팟 가격은 가용 영역별로, 그리고 시간에 따라 달라집니다.  
→ 같은 리전이라도 AZ마다 다름.  

For example, the price for an m4.large instance in the us-east-1 region fluctuates across six availability zones.  
예를 들어, us-east-1 리전에서 m4.large 인스턴스 가격은 6개의 AZ마다 다르게 변동합니다.  
→ 특정 AZ 선택이 중요함.  

If you set a user-defined maximum price, you will lose your spot instance when the current spot price exceeds this maximum.  
사용자 정의 최대 가격을 설정하면, 현재 가격이 이를 초과할 경우 스팟 인스턴스를 잃게 됩니다.  
→ 가격이 오르면 인스턴스 종료됨.  

When the price falls below your maximum, you regain the instance.  
가격이 다시 낮아지면 인스턴스를 다시 확보할 수 있습니다.  
→ 가격이 내리면 자동으로 복구 가능.  

---

## Spot Requests and Termination  
## 스팟 요청과 종료  
(요청 및 중단 처리 방식 설명)  

A spot request defines the number of instances, maximum price, launch specifications such as AMI, and the request validity period.  
스팟 요청은 인스턴스 개수, 최대 가격, AMI와 같은 실행 사양, 요청 유효 기간을 정의합니다.  
→ 요청 시 여러 조건을 설정 가능.  

There are two types of spot requests:  
스팟 요청에는 두 가지 유형이 있습니다:  

- One-time requests: Instances launch once and the request is removed after fulfillment.  
- 일회성 요청: 인스턴스가 한 번 실행되면 요청이 완료되고 삭제됩니다.  

- Persistent requests: The request remains active, and if instances are interrupted, the request attempts to relaunch them.  
- 지속 요청: 요청이 계속 활성 상태이며, 인스턴스가 중단되면 다시 실행하려 시도합니다.  

To cancel a spot request, it must be in an open, active, or disabled state.  
스팟 요청을 취소하려면 열림, 활성, 또는 비활성 상태여야 합니다.  

Canceling a spot request does not terminate existing instances; you must terminate those separately.  
스팟 요청을 취소해도 실행 중인 인스턴스는 종료되지 않으며, 별도로 종료해야 합니다.  

---

## Spot Fleets  
## 스팟 플릿  
(여러 인스턴스를 묶어서 관리하는 기능 설명)  

Spot Fleets allow you to define a group of spot instances and optionally On-Demand instances to meet a target capacity within price constraints.  
스팟 플릿은 스팟 인스턴스와 온디맨드 인스턴스를 묶어 목표 용량을 충족하도록 정의할 수 있습니다.  

They can launch instances from multiple launch pools, which may include different instance types, operating systems, and availability zones.  
여러 실행 풀에서 인스턴스를 실행할 수 있으며, 여기에는 다양한 인스턴스 타입, 운영체제, AZ가 포함될 수 있습니다.  

---

## Spot Fleet Allocation Strategies  
## 스팟 플릿 할당 전략  
(인스턴스를 배치하는 방식 설명)  

- Lowest Price: Launch instances from the pool with the lowest price.  
- 최저가: 가장 낮은 가격의 풀에서 인스턴스를 실행.  

- Diversified: Distribute instances across all defined pools.  
- 다각화: 정의된 모든 풀에 인스턴스를 분산 배치.  

- Capacity Optimized: Choose pools with optimal capacity.  
- 용량 최적화: 인스턴스 수에 적합한 풀 선택.  

- Price Capacity Optimized: Select pool with the highest capacity, then lowest price.  
- 가격·용량 최적화: 가장 큰 용량을 가진 풀을 선택하고, 그 안에서 가장 낮은 가격을 선택.  

---

## Summary  
## 요약  
(전체 핵심 정리)  

Spot Fleets provide a powerful way to optimize costs by allowing multiple instance types and availability zones.  
스팟 플릿은 다양한 인스턴스 타입과 AZ를 활용하여 비용을 최적화할 수 있는 강력한 방법을 제공합니다.  

This differs from simple spot instance requests where you specify a single instance type and availability zone.  
이는 단일 인스턴스 타입과 AZ만 지정하는 단순 스팟 요청과는 다릅니다.  

Understanding these concepts is crucial for efficient AWS cost management and is often tested in certification exams.  
이 개념을 이해하는 것은 효율적인 AWS 비용 관리에 필수적이며, 자격증 시험에도 자주 출제됩니다.  

---

## Key Takeaways  
## 핵심 요약  
(가장 중요한 포인트만 추린 정리)  

- EC2 Spot Instances offer up to 90% cost savings compared to On-Demand.  
- EC2 스팟 인스턴스는 온디맨드 대비 최대 90%까지 비용 절감 가능.  

- When spot price exceeds the max price, instances can be stopped or terminated within 2 minutes.  
- 스팟 가격이 최대치를 초과하면 인스턴스는 2분 내에 정지 또는 종료 가능.  

- Spot blocks provide interruption-free spot instances for 1~6 hours.  
- 스팟 블록은 1~6시간 동안 중단 없는 인스턴스를 보장.  

- Spot Fleets allow combining multiple pools with strategies like lowest price or capacity optimized.  
- 스팟 플릿은 다양한 풀을 결합해 최저가, 용량 최적화 등의 전략으로 운영 가능.  
