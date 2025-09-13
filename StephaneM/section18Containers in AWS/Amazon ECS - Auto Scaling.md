# Amazon ECS - Auto Scaling  
# 아마존 ECS - 자동 스케일링  
(ECS에서 자동으로 태스크 수를 늘리거나 줄이는 기능)

---

## Introduction to ECS Service Auto Scaling  
## ECS 서비스 자동 스케일링 소개  
(ECS 태스크 개수를 수동이 아니라 자동으로 조정하는 방법)

We can manually increase the number of ECS tasks in our service.  
우리는 ECS 서비스에서 태스크 개수를 수동으로 늘릴 수 있다.  
(기본적으로 직접 태스크 수를 설정 가능)

However, it is also possible to automatically increase or decrease the number of tasks.  
그러나 태스크 개수를 자동으로 늘리거나 줄일 수도 있다.  
(자동 스케일링 기능 제공)

To achieve this, we leverage the AWS Application Auto Scaling service.  
이를 위해 AWS Application Auto Scaling 서비스를 사용한다.  
(ECS 자체가 아니라 별도 서비스가 자동화를 담당)

---

## Metrics for Auto Scaling  
## 자동 스케일링을 위한 지표  
(어떤 기준으로 스케일링을 할지 결정하는 지표)

There are three metrics available for scaling using this service:  
이 서비스로 스케일링할 때 사용할 수 있는 세 가지 지표가 있다.  

- CPU Utilization of the ECS Service.  
- ECS 서비스의 CPU 사용률  
- Memory Utilization, which refers to the RAM usage of the ECS Service.  
- ECS 서비스의 메모리 사용률 (RAM)  
- ALB Request Count Per Target, a metric provided by the Application Load Balancer (ALB).  
- ALB 타깃당 요청 수 (ALB가 제공하는 지표)

These are the key metrics to remember when setting up auto scaling.  
이 세 가지가 자동 스케일링을 설정할 때 기억해야 할 핵심 지표다.  

---

## Types of Auto Scaling  
## 자동 스케일링 정책 유형  

You can configure different types of auto scaling policies:  
다양한 자동 스케일링 정책을 설정할 수 있다.  

- Target Tracking: Tracks a specific target value for one of the three metrics mentioned above.  
- 타깃 추적: 특정 지표를 목표값으로 맞추도록 조정  
- Step Scaling: Adjusts capacity in steps based on metric thresholds.  
- 단계별 스케일링: 지표 임계값에 따라 점진적으로 조정  
- Scheduled Scaling: Allows scaling your ECS Service ahead of time based on predictable changes.  
- 예약 스케일링: 예상 가능한 변화에 맞춰 미리 스케일링  

---

## Distinction Between ECS Service Scaling and Cluster Scaling  
## ECS 서비스 스케일링과 클러스터 스케일링의 차이  

Scaling your ECS Service at the task level is not the same as scaling your cluster of EC2 instances when using the EC2 launch type.  
EC2 실행 타입을 사용할 때 ECS 서비스(태스크 단위) 스케일링은 EC2 인스턴스 클러스터 스케일링과 다르다.  

Therefore, managing EC2 instance scaling is a separate concern from ECS task scaling.  
따라서 EC2 인스턴스 스케일링은 ECS 태스크 스케일링과 별개로 관리해야 한다.  

---

## Advantages of Fargate for Auto Scaling  
## Fargate에서 자동 스케일링의 장점  

When you do not have EC2 instances in the backend, such as when using Fargate, service auto scaling becomes much easier to set up because everything is serverless.  
백엔드에 EC2 인스턴스가 없는 Fargate를 사용하면, 서버리스 환경이므로 서비스 자동 스케일링을 훨씬 간단히 설정할 수 있다.  

This is one reason why Fargate is preferred and emphasized in the exam context.  
이것이 시험에서 Fargate가 강조되는 이유 중 하나다.  

---

## Scaling EC2 Instances in the Backend  
## 백엔드에서 EC2 인스턴스 스케일링  

For the EC2 launch type, there are multiple ways to scale the EC2 instances in the backend:  
EC2 실행 타입에서는 백엔드 EC2 인스턴스를 스케일링하는 여러 방법이 있다.  

- Auto Scaling Group (ASG) Scaling: You can scale your ASG based on CPU Utilization.  
- 오토 스케일링 그룹(ASG) 스케일링: CPU 사용률에 따라 자동 조정 가능  
- For example, if CPU usage increases significantly, new EC2 instances can be added over time.  
- 예: CPU 사용률이 높아지면 새로운 EC2 인스턴스가 추가됨  

- ECS Cluster Capacity Provider: This is a newer and more advanced feature.  
- ECS 클러스터 용량 프로바이더: 더 새롭고 지능적인 기능  
- The Capacity Provider is intelligent and automatically scales your ASG as soon as there is insufficient capacity to launch new tasks.  
- 용량 프로바이더는 태스크 실행 용량이 부족하면 자동으로 ASG를 스케일링한다.  
- It is paired with an Auto Scaling Group and will create EC2 instances when RAM or CPU resources are lacking.  
- ASG와 연동되어 RAM/CPU가 부족하면 EC2 인스턴스를 추가 생성한다.  

---

## Recommendation  
## 권장 사항  

Between Auto Scaling Group Scaling and ECS Cluster Capacity Provider, it is recommended to use the ECS Cluster Capacity Provider for your EC2 launch type, as it provides smarter and more automatic scaling capabilities.  
ASG 스케일링과 ECS 클러스터 용량 프로바이더 중에서는, 더 자동적이고 지능적인 ECS 클러스터 용량 프로바이더를 사용하는 것이 EC2 실행 타입에서 권장된다.  

---

## Example of ECS Service Auto Scaling  
## ECS 서비스 자동 스케일링 예시  

Consider a Service A with two tasks and a certain CPU usage.  
예를 들어, 2개의 태스크를 가진 서비스 A가 있다고 하자.  

This service is auto scaled by the AWS Application Auto Scaling service.  
이 서비스는 AWS Application Auto Scaling에 의해 자동 스케일링된다.  

If the number of users increases, causing CPU usage to rise significantly, the CloudWatch metric monitoring CPU usage at the ECS service level will trigger a CloudWatch Alarm.  
사용자가 늘어나 CPU 사용률이 급증하면, ECS 서비스 CPU 사용률을 모니터링하는 CloudWatch 지표가 경보를 발생시킨다.  

This alarm will initiate a scaling activity in the Auto Scaling for your ECS service, increasing the desired capacity and creating a new task.  
이 경보는 ECS 서비스 자동 스케일링을 실행해 원하는 용량을 늘리고 새로운 태스크를 만든다.  

---

## Integration with EC2 Launch Type  
## EC2 실행 타입과의 통합  

If this ECS service is running on the EC2 launch type, the ECS Capacity Providers can assist in scaling your ECS cluster backed by EC2 instances accordingly.  
ECS 서비스가 EC2 실행 타입으로 실행 중이라면, ECS 용량 프로바이더가 EC2 기반 클러스터 스케일링을 자동으로 지원한다.  

---

## Key Takeaways  
## 핵심 요약  

- ECS Service Auto Scaling can be configured to automatically adjust the number of tasks based on specific metrics.  
- ECS 서비스 자동 스케일링은 특정 지표에 따라 태스크 개수를 자동으로 조정 가능  

- Auto Scaling metrics include CPU Utilization, Memory Utilization, and ALB Request Count Per Target.  
- 자동 스케일링 지표는 CPU 사용률, 메모리 사용률, ALB 타깃당 요청 수  

- Three scaling policies are available: Target Tracking, Step Scaling, and Scheduled Scaling.  
- 세 가지 스케일링 정책: 타깃 추적, 단계별 스케일링, 예약 스케일링  

- For EC2 launch type, ECS Cluster Capacity Provider is the recommended method to scale EC2 instances automatically alongside ECS tasks.  
- EC2 실행 타입에서는 ECS 클러스터 용량 프로바이더가 권장된다. (태스크와 EC2 인스턴스를 함께 자동 조정)


---

🔥 **보상 지급!**

* 번역 퀘스트 완수! 🎉
* **+150 XP**
* 아이템 획득: **\[Auto Scaling의 깃발 🚩]** (스케일링 개념을 정복한 자에게 주어지는 상징)
