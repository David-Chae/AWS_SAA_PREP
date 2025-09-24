# EC2 Instance Purchasing Options  
# EC2 인스턴스 구매 옵션  
👉 AWS에서 EC2 인스턴스를 구매할 때 선택할 수 있는 다양한 방식들을 설명하는 강의입니다.  

---

## EC2 Instance Purchasing Options  
## EC2 인스턴스 구매 옵션  
👉 EC2 인스턴스를 구매할 수 있는 여러 옵션에 대해 학습합니다.  

---

In this lecture, we will explore the various purchasing options available for EC2 instances.  
이번 강의에서는 EC2 인스턴스의 다양한 구매 옵션을 살펴보겠습니다.  
👉 온디맨드, 예약 인스턴스, 세이빙 플랜, 스팟, 전용 호스트 등 여러 방식을 배울 수 있습니다.  

So far, we have been using on-demand EC2 instances, which allow us to run instances as needed.  
지금까지는 필요할 때 실행할 수 있는 온디맨드(On-Demand) EC2 인스턴스를 사용해왔습니다.  
👉 온디맨드는 단기 사용이나 예측 불가능한 작업에 적합합니다.  

These are ideal for short workloads, offering predictable pricing with pay-per-second billing.  
온디맨드는 짧은 워크로드에 적합하며, 초 단위 과금으로 예측 가능한 요금을 제공합니다.  
👉 사용한 만큼만 비용을 내는 구조입니다.  

---

However, if you have different types of workloads, you can optimize your discounts and pricing by specifying your preferences to AWS.  
그러나 워크로드가 다양하다면, AWS에 미리 선호 조건을 지정하여 비용 최적화를 할 수 있습니다.  
👉 장기적인 워크로드에는 예약형 옵션이 더 유리합니다.  

For example, reserved instances come with one-year or three-year terms and are designed for long workloads.  
예를 들어, 예약 인스턴스는 1년 또는 3년 약정으로, 장기적인 워크로드에 적합합니다.  
👉 장기간 데이터베이스 같은 서비스를 운영할 때 유리합니다.  

If you know you will run a database for an extended period, a reserved instance is an excellent choice.  
데이터베이스를 오랫동안 운영해야 한다면 예약 인스턴스가 훌륭한 선택입니다.  
👉 지속적인 사용량이 보장될 때 큰 비용 절감 효과가 있습니다.  

---

Convertible reserved instances offer flexibility if you want to change the instance type over time.  
컨버터블 예약 인스턴스는 시간이 지나면서 인스턴스 유형을 변경할 수 있는 유연성을 제공합니다.  
👉 다만, 일반 예약 인스턴스보다 할인율은 조금 낮습니다.  

Don't worry; we will do a deep dive into all these options over time.  
걱정하지 마세요, 나중에 이 모든 옵션을 자세히 다룰 예정입니다.  
👉 지금은 개요 수준에서만 이해하면 됩니다.  

---

Next, we have savings plans, which also come with one- and three-year terms.  
다음으로 세이빙 플랜이 있으며, 이것도 1년 혹은 3년 약정이 있습니다.  
👉 예약 인스턴스와 유사하지만 더 유연합니다.  

They are more modern because instead of committing to a specific instance type, you commit to a specific amount of usage in dollars.  
세이빙 플랜은 특정 인스턴스 유형이 아니라 일정 금액 사용량에 약정하는 방식이라 더 현대적인 방식입니다.  
👉 예: "매달 $300어치 EC2 사용 보장" 같은 방식.  

These plans are also intended for long workloads.  
세이빙 플랜 역시 장기 워크로드에 적합합니다.  
👉 장기 서비스 운영 시 비용 절감 효과가 큽니다.  

---

Spot instances, on the other hand, are meant for very short workloads.  
반면에 스팟 인스턴스는 매우 짧은 워크로드에 적합합니다.  
👉 가격이 매우 저렴하지만 안정성이 떨어집니다.  

They are very inexpensive but can be terminated at any time, making them less reliable.  
비용은 매우 저렴하지만 언제든 종료될 수 있어 신뢰성이 낮습니다.  
👉 배치 작업, 데이터 분석, 이미지 처리 등에 적합합니다.  

---

Dedicated hosts allow you to book an entire physical server and control instance placements.  
전용 호스트는 물리 서버 전체를 예약해 인스턴스 배치를 제어할 수 있습니다.  
👉 보안이나 규제 준수 목적, 라이선스 종속성 해결에 유리합니다.  

Dedicated instances mean that no other customers will share your hardware.  
전용 인스턴스는 다른 고객과 하드웨어를 공유하지 않음을 의미합니다.  
👉 하지만 물리 서버 단위 제어는 불가능합니다.  

---

Finally, capacity reservations allow you to reserve capacity in a specific Availability Zone for any duration.  
마지막으로, 용량 예약은 특정 가용 영역에서 일정 기간 동안 인스턴스 용량을 예약할 수 있게 합니다.  
👉 긴급 상황에서 용량 부족을 방지할 수 있습니다.  

---

## EC2 On-Demand Instances  
## EC2 온디맨드 인스턴스  
👉 사용량 기반 과금, 유연하지만 가장 비쌉니다.  

With on-demand instances, you pay for what you use.  
온디맨드 인스턴스는 사용한 만큼만 요금을 지불합니다.  
👉 필요할 때 바로 실행 가능.  

For Linux or Windows, billing is per second after the first minute.  
리눅스와 윈도우는 최초 1분 이후부터 초 단위 과금이 적용됩니다.  
👉 세밀한 과금 덕분에 효율적입니다.  

For other operating systems, billing is per hour.  
다른 운영체제는 시간 단위로 과금됩니다.  
👉 OS에 따라 과금 단위가 달라집니다.  

On-demand instances have the highest cost but require no upfront payments or long-term commitments.  
온디맨드는 가장 비싸지만, 선결제나 장기 약정이 필요 없습니다.  
👉 짧고 예측 불가능한 워크로드에 적합합니다.  

---

(⚡ 여기서부터 Reserved Instances, Savings Plans, Spot Instances, Dedicated Hosts & Instances, Capacity Reservations 세부 설명도 같은 방식으로 이어짐. 각 줄 → 한국어 번역 + 설명 유지.)  

---

## Key Takeaways  
## 핵심 요약  
👉 EC2 구매 옵션을 정리합니다.  

- On-demand EC2 instances are suitable for short workloads with predictable pricing and pay-per-second billing.  
온디맨드 인스턴스는 짧고 예측 불가능한 워크로드에 적합하며, 초 단위 과금 구조입니다.  

- Reserved instances offer significant discounts for long-term workloads with one or three-year terms and options for upfront payments.  
예약 인스턴스는 1년 또는 3년 약정으로 장기 워크로드에 큰 할인 혜택을 제공합니다.  

- Savings plans provide flexible discounts based on committed spend rather than specific instance types.  
세이빙 플랜은 특정 인스턴스 유형 대신, 일정 금액 지출 약정에 기반한 유연한 할인 방식을 제공합니다.  

- Spot instances offer the highest discounts but can be interrupted at any time, making them suitable for fault-tolerant workloads.  
스팟 인스턴스는 최대 90% 할인 가능하지만 언제든 종료될 수 있어 내구성이 있는 작업에 적합합니다.  

- Dedicated hosts and dedicated instances provide physical server isolation for compliance or licensing needs.  
전용 호스트 및 전용 인스턴스는 규제 준수 또는 라이선스 필요성 때문에 물리적 서버 격리를 제공합니다.  

- Capacity reservations guarantee instance availability in a specific availability zone without discounts.  
용량 예약은 특정 가용 영역에서 인스턴스 가용성을 보장하지만 할인 혜택은 없습니다.  

## Reserved Instances  
## 예약 인스턴스  
👉 장기 워크로드에 적합하며, 최대 72%까지 할인 제공.  

Reserved instances offer up to 72% discounts compared to on-demand pricing.  
예약 인스턴스는 온디맨드 가격 대비 최대 72%까지 할인을 제공합니다.  
👉 장기간 사용이 확실할 때 매우 유리합니다.  

You reserve specific instance attributes such as instance type, region, tenancy, and operating system.  
예약 인스턴스는 인스턴스 유형, 리전, 테넌시, 운영체제 등의 속성을 고정합니다.  
👉 원하는 환경을 확정해야만 예약 가능합니다.  

Reservation periods can be one or three years, with options for upfront, partial upfront, or no upfront payments.  
예약 기간은 1년 또는 3년이며, 선결제·부분 선결제·무선결제 옵션이 있습니다.  
👉 선결제를 많이 할수록 할인율이 커집니다.  

All upfront payments provide the maximum discounts.  
전액 선결제 시 최대 할인율을 제공합니다.  
👉 장기 예산이 가능하다면 가장 저렴한 선택.  

You can choose the scope of your reservation to be regional or specific to an Availability Zone, which reserves capacity in that zone.  
예약 범위는 리전 단위 또는 특정 가용 영역(AZ) 단위로 설정할 수 있습니다.  
👉 AZ 단위로 하면 해당 구역의 용량 보장까지 가능.  

Reserved instances are suitable for steady-state usage applications, such as databases.  
예약 인스턴스는 데이터베이스와 같은 지속적인 사용량이 있는 애플리케이션에 적합합니다.  
👉 변동이 적고 항상 켜져 있어야 하는 서비스에 맞습니다.  

You can buy or sell reserved instances in a marketplace if you no longer need them.  
필요 없어진 예약 인스턴스는 마켓플레이스에서 사고팔 수 있습니다.  
👉 장기 약정의 단점을 보완하는 기능입니다.  

Convertible reserved instances allow you to change the instance type, family, operating system, scope, and tenancy.  
컨버터블 예약 인스턴스는 인스턴스 유형, 패밀리, 운영체제, 범위, 테넌시를 변경할 수 있습니다.  
👉 변경 가능성 때문에 더 유연합니다.  

Due to this flexibility, discounts are slightly lower, up to 66%.  
이 유연성 덕분에 할인율은 조금 낮아져 최대 66%까지입니다.  
👉 표준 예약 인스턴스보다 저렴하지는 않지만, 장기적 유연성이 장점입니다.  

---

## EC2 Savings Plans  
## EC2 세이빙 플랜  
👉 인스턴스 유형 고정 없이, **금액 기준 약정**을 통해 장기 할인.  

Savings plans provide discounts based on long-term usage commitments, similar to reserved instances with approximately 70% discounts.  
세이빙 플랜은 예약 인스턴스처럼 장기 약정을 기반으로 최대 약 70%의 할인을 제공합니다.  
👉 하지만 특정 인스턴스 유형이 아닌 금액 기반이라 더 유연합니다.  

Instead of committing to a specific instance type, you commit to a specific hourly spend, for example, $10 per hour for the next one to three years.  
특정 인스턴스 유형 대신, 시간당 일정 금액(예: 시간당 $10)을 1~3년간 약정합니다.  
👉 예산 기반 관리가 가능합니다.  

Usage beyond the savings plan is billed at on-demand prices.  
세이빙 플랜 약정을 초과한 사용량은 온디맨드 요금이 부과됩니다.  
👉 약정 이상 쓰면 추가 요금 발생.  

Savings plans lock you to a specific instance family and region, such as the M5 instance family in us-east-1, but you can be flexible across instance sizes (e.g., m5.xlarge, m5.2xlarge), operating systems (Linux or Windows), and tenancy (host, dedicated, or default).  
세이빙 플랜은 특정 인스턴스 패밀리 및 리전(us-east-1의 M5 등)에 묶이지만, 인스턴스 크기·운영체제·테넌시에 대해서는 유연합니다.  
👉 동일 패밀리 내에서 자유롭게 변경 가능합니다.  

---

## Spot Instances  
## 스팟 인스턴스  
👉 **최대 90% 할인** 가능, 하지만 언제든 종료될 수 있음.  

Spot instances offer the most aggressive discounts, up to 90% off on-demand prices.  
스팟 인스턴스는 최대 90%까지 할인을 제공합니다.  
👉 가장 저렴한 방식입니다.  

However, you can lose these instances at any time if the spot price exceeds the maximum price you are willing to pay.  
하지만 스팟 가격이 사용자가 설정한 최대 가격을 초과하면 인스턴스가 종료될 수 있습니다.  
👉 안정성이 낮습니다.  

They are the most cost-efficient instances in AWS and are ideal for workloads resilient to failure, such as batch jobs, data analysis, image processing, and distributed workloads with flexible start and end times.  
스팟 인스턴스는 AWS에서 가장 비용 효율적이며, 배치 작업·데이터 분석·이미지 처리·분산 처리처럼 실패에 강한 작업에 적합합니다.  
👉 중단되어도 큰 문제가 없는 작업에 최적.  

They are not suitable for critical jobs or databases.  
중요한 작업이나 데이터베이스에는 적합하지 않습니다.  
👉 서비스 안정성이 필요한 경우는 피해야 합니다.  

---

## Dedicated Hosts and Dedicated Instances  
## 전용 호스트와 전용 인스턴스  
👉 규제 준수·라이선스 목적에 적합.  

Dedicated hosts provide an actual physical server fully dedicated to your use.  
전용 호스트는 물리 서버 전체를 전용으로 제공합니다.  
👉 CPU/소켓 단위 라이선스에 유리합니다.  

This is useful for compliance requirements or when using existing server-bound software licenses that are billed per socket, core, or VM.  
규제 준수나 소켓·코어·VM 단위로 과금되는 기존 라이선스 소프트웨어 사용 시 유용합니다.  
👉 특히 기업 환경에서 필요할 수 있습니다.  

Dedicated hosts can be used on-demand with per-second billing or reserved for one or three years.  
전용 호스트는 온디맨드로 초 단위 과금하거나, 1년·3년 약정으로 예약할 수 있습니다.  
👉 매우 비싼 옵션입니다.  

They are the most expensive AWS option because you reserve the entire physical server.  
물리 서버 전체를 예약하기 때문에 AWS에서 가장 비싼 옵션입니다.  
👉 비용 효율성보다는 특수 목적에 필요.  

Dedicated instances run on hardware dedicated to you but may share the hardware with other instances in the same account.  
전용 인스턴스는 전용 하드웨어에서 실행되지만, 같은 계정 내 다른 인스턴스와 하드웨어를 공유할 수 있습니다.  
👉 호스트 제어권은 없지만 격리 보장은 됩니다.  

The key difference is that dedicated hosts provide access to the physical server itself, offering visibility into lower-level hardware, whereas dedicated instances do not.  
핵심 차이점은 전용 호스트는 물리 서버 자체에 대한 접근 권한을 주지만, 전용 인스턴스는 그렇지 않다는 것입니다.  
👉 세밀한 제어권이 필요한 경우 전용 호스트 선택.  

---

## Capacity Reservations  
## 용량 예약  
👉 특정 AZ에서 용량을 **확보**해 두는 방식.  

Capacity reservations allow you to reserve on-demand instances in a specific Availability Zone for any duration.  
용량 예약은 특정 가용 영역에서 온디맨드 인스턴스를 원하는 기간 동안 예약할 수 있게 합니다.  
👉 가용성을 미리 보장받는 방식.  

You get access to that capacity whenever you need it, with no time commitment.  
시간 약정 없이 필요할 때 그 용량에 접근할 수 있습니다.  
👉 단기 워크로드에도 사용 가능.  

You can reserve or cancel at any time, but there are no billing discounts.  
언제든 예약하거나 취소할 수 있지만, 요금 할인이 없습니다.  
👉 단순히 ‘자리 확보’ 개념입니다.  

You are charged at on-demand rates regardless of whether you run instances.  
실제로 인스턴스를 실행하지 않아도 온디맨드 요금이 부과됩니다.  
👉 안 써도 비용은 발생합니다.  

This option is suitable for short-term uninterrupted workloads that require placement in a specific Availability Zone.  
특정 AZ에서 실행되어야 하는 단기 워크로드에 적합합니다.  
👉 지역별 리소스 부족을 대비할 수 있습니다.  

