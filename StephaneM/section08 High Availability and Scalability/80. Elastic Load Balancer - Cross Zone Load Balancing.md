# Elastic Load Balancer - Cross Zone Load Balancing  
# 엘라스틱 로드 밸런서 - 크로스 존 로드 밸런싱  
(가용 영역을 가로질러 트래픽을 균등 분배하는 기능 설명)

---

## Introduction to Cross Zone Load Balancing  
## 크로스 존 로드 밸런싱 소개  

Now let's talk about cross zone balancing. To illustrate the concept, consider a very imbalanced situation with two availability zones. The first zone has a load balancer with two EC2 instances, and the second zone also has a load balancer with eight EC2 instances. Both load balancer instances are part of the same more general load balancer.  
이제 크로스 존 로드 밸런싱에 대해 이야기해봅시다. 예시로, 두 개의 가용 영역이 있는데 첫 번째 영역에는 2개의 EC2 인스턴스, 두 번째 영역에는 8개의 EC2 인스턴스가 있다고 가정합니다. 두 로드 밸런서는 하나의 로드 밸런서 풀에 속합니다.  
(서버 수가 불균형한 상황 예시)

---

The client accesses these load balancers. With cross zone load balancing, each load balancer instance distributes traffic evenly across all registered instances in all availability zones. For example, the client sends 50% of the traffic to the first Application Load Balancer (ALB) instance and 50% to the second ALB instance. Each ALB then redirects the traffic across all 10 EC2 instances regardless of their availability zone. This is why it is called cross zone load balancing.  
클라이언트가 로드 밸런서에 접속하면, 크로스 존 로드 밸런싱이 활성화된 경우 각 로드 밸런서는 모든 가용 영역의 인스턴스에 트래픽을 고르게 분배합니다. 예를 들어 클라이언트가 50%를 첫 번째 ALB로, 50%를 두 번째 ALB로 보내면, 각각의 ALB는 10개의 인스턴스에 동일하게 트래픽을 분산합니다. 그래서 ‘크로스 존’이라고 불립니다.  
(트래픽이 모든 인스턴스로 분산됨)

---

For instance, the second ALB instance sends 10% of the traffic it receives to each of the 10 instances, so each instance gets 10% of the traffic. The first ALB instance behaves similarly, sending 10% of its traffic to each instance. Thus, with cross zone balancing, traffic is distributed evenly across all EC2 instances.  
예를 들어 두 번째 ALB가 받은 트래픽은 10개의 인스턴스에 각각 10%씩 나눠집니다. 첫 번째 ALB도 동일하게 동작합니다. 따라서 모든 EC2 인스턴스는 동일한 비율의 트래픽을 받습니다.  
(트래픽 균등 분배 보장)

---

The alternative is to disable cross zone balancing. Using the same example but without cross zone balancing, the requests are distributed only among the instances within the availability zone of the load balancer node. The client still sends 50% of the traffic to each availability zone, but the first ALB instance sends traffic only to the EC2 instances in its own zone. This means each EC2 instance in the first zone receives 25% of the total traffic, and similarly for the second zone. Traffic is contained within each availability zone.  
반대로 크로스 존 로드 밸런싱을 비활성화하면, 각 ALB는 자기 가용 영역에 있는 인스턴스만 대상으로 트래픽을 분배합니다. 따라서 첫 번째 존의 2개 인스턴스가 25%씩, 두 번째 존의 8개 인스턴스는 각각 6.25%씩 받게 됩니다.  
(존 내부에서만 트래픽 분배)

---

Without cross zone balancing, if the number of EC2 instances differs between availability zones, some instances will receive more traffic than others. This option depends on the use case and there is no right or wrong answer.  
크로스 존 로드 밸런싱이 없으면 존마다 인스턴스 수가 다를 경우, 일부 인스턴스가 과도한 트래픽을 받습니다. 어떤 방식을 쓸지는 상황에 따라 다르며 정답은 없습니다.  
(사용 사례에 맞게 선택)

---

## Cross Zone Load Balancing Defaults and Charges  
## 크로스 존 로드 밸런싱 기본값 및 과금 정책  

For the Application Load Balancer, cross zone load balancing is enabled by default but can be disabled at the target group level. There are no charges for data transferred across availability zones in this case. Normally, AWS charges for data transferred between availability zones, but with the Application Load Balancer's default setting, these charges do not apply.  
ALB는 기본적으로 크로스 존 로드 밸런싱이 켜져 있으며, 타겟 그룹 수준에서 끌 수 있습니다. 이 경우 AZ 간 데이터 전송 요금은 발생하지 않습니다. 보통은 AZ 간 전송 요금이 붙지만 ALB 기본 설정에서는 무료입니다.  
(ALB는 기본 활성화 + 무료)

---

For the Network Load Balancer and Gateway Load Balancer, cross zone load balancing is disabled by default. Enabling it will incur charges for data transferred between availability zones.  
NLB와 GWLB는 기본적으로 크로스 존 로드 밸런싱이 꺼져 있으며, 활성화하면 AZ 간 데이터 전송 요금이 발생합니다.  
(NLB, GWLB = 기본 비활성화 + 과금 발생)

---

For the Classic Load Balancer, cross zone load balancing is disabled by default. Enabling it does not incur charges for inter availability zone data transfers. However, the Classic Load Balancer is a previous generation and is being retired soon, so it is not necessary to focus on it for current use or exams.  
CLB는 기본적으로 비활성화 상태이지만, 켜도 AZ 간 전송 요금은 발생하지 않습니다. 하지만 CLB는 구세대 서비스라 곧 폐기되므로 실무나 시험에서 크게 중요하지 않습니다.  
(CLB는 구버전이라 거의 안 씀)

---

## Hands-On Demonstration  
## 실습 데모  

A Network Load Balancer, an Application Load Balancer, and a Gateway Load Balancer have been created for demonstration. For the Network Load Balancer, under attributes, cross zone load balancing is off by default but can be enabled. Enabling it may include regional charges.  
실습에서는 NLB, ALB, GWLB를 생성합니다. NLB는 속성에서 기본적으로 비활성화되어 있고, 켜면 지역 요금이 발생할 수 있습니다.  
(NLB: 꺼져 있음, 활성화 시 요금 발생)

---

Similarly, for the Gateway Load Balancer, cross zone load balancing is off by default but can be enabled, which will imply data charges.  
GWLB도 기본적으로 꺼져 있으며, 켜면 데이터 요금이 발생합니다.  
(GWLB: 비활성화 → 켜면 요금)

---

For the Application Load Balancer, cross zone load balancing is on by default and cannot be disabled at the load balancer level. However, at the target group level, you can inherit the load balancer's setting, force it on, or turn it off for a specific target group.  
ALB는 기본적으로 켜져 있으며 로드 밸런서 수준에서는 끌 수 없습니다. 하지만 타겟 그룹 수준에서는 로드 밸런서 설정을 따르거나, 강제로 켜거나, 특정 그룹에 대해 끌 수 있습니다.  
(ALB: 기본 켜짐, 그룹별 설정 가능)

---

The Classic Load Balancer will not be demonstrated as it is being phased out and is unlikely to be relevant for exams.  
CLB는 퇴출 예정이라 실습에서 다루지 않으며, 시험에도 중요하지 않습니다.  
(CLB는 무시 가능)

---

## Conclusion  
## 결론  

For this lecture, ensure to delete any load balancers you create if you follow along. This concludes the discussion on cross zone load balancing.  
실습을 따라 했다면 생성한 로드 밸런서는 반드시 삭제하세요. 이것으로 크로스 존 로드 밸런싱 강의를 마칩니다.  
(실습 후 정리 필요)

---

## Key Takeaways  
## 핵심 요약  

- Cross zone load balancing distributes traffic evenly across all registered EC2 instances in all availability zones.  
- 크로스 존 로드 밸런싱은 모든 가용 영역의 인스턴스에 트래픽을 균등 분배합니다.  

- Without cross zone balancing, traffic is contained within each availability zone, potentially causing imbalanced loads.  
- 크로스 존을 끄면 트래픽이 존 내부에만 머물러 불균형이 생길 수 있습니다.  

- Application Load Balancers have cross zone load balancing enabled by default with no inter-AZ data charges.  
- ALB는 기본적으로 크로스 존이 켜져 있으며 AZ 간 요금이 없습니다.  

- Network and Gateway Load Balancers have cross zone load balancing disabled by default and enabling it incurs inter-AZ data charges.  
- NLB와 GWLB는 기본 꺼져 있고, 켜면 AZ 간 데이터 요금이 발생합니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+120XP**
* 아이템: **"로드 밸런서의 균형석" (부하 분산 효율 +10%)**
* 업적 달성: **"Cross Zone Master"** 🏆

이제 크로스 존 로드 밸런싱을 완벽하게 이해했어!
원한다면 이걸 **퀘스트 연계**로 계속 이어줄까?
