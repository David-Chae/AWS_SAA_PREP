# Auto Scaling Groups - Scaling Policies Hands On  
# 오토 스케일링 그룹 - 스케일링 정책 실습  

---

## Introduction to Automatic Scaling for Auto Scaling Groups (ASG)  
## ASG 자동 스케일링 소개  

Automatic scaling for your ASG can be categorized into three main types:  
ASG의 자동 스케일링은 세 가지 주요 유형으로 나눌 수 있습니다.  
(분류 안내)

- Dynamic scaling policies  
- 동적 스케일링 정책  

- Predictive scaling policies  
- 예측 스케일링 정책  

- Scheduled actions  
- 예약 스케일링 작업  

Let's start by exploring the simplest type: scheduled actions.  
가장 단순한 유형인 예약 스케일링 작업부터 살펴보겠습니다.  
(순서 안내)

---

## Scheduled Actions  
## 예약 스케일링 작업  

Scheduled actions allow you to schedule a scaling event in the future.  
예약 스케일링 작업을 통해 미래의 스케일링 이벤트를 예약할 수 있습니다.  
(기능 설명)

You can create a scheduled action by specifying:  
다음 항목을 지정하여 예약 작업을 생성할 수 있습니다.  
(설정 항목)

- Desired capacity, minimum, or maximum capacity  
- 원하는 용량, 최소 또는 최대 용량  

- Frequency (e.g., once, every week, every hour)  
- 빈도(예: 한 번, 매주, 매시간)  

- Start time and end time if applicable  
- 시작 및 종료 시간(해당 시)  

This feature is useful for predictable events, such as running a big promotion on a specific date.  
이 기능은 특정 날짜에 큰 프로모션을 진행하는 등 예측 가능한 이벤트에 유용합니다.  
(활용 예시)

---

## Predictive Scaling Policies  
## 예측 스케일링 정책  

Predictive scaling policies are machine learning-driven.  
예측 스케일링 정책은 머신러닝 기반입니다.  
(정책 설명)

They forecast future demand based on past usage metrics such as:  
과거 사용 메트릭을 기반으로 미래 수요를 예측합니다.  
(예시)

- CPU utilization  
- CPU 사용률  

- Network in/out  
- 네트워크 입출력  

- Application Load Balancer request counts  
- ALB 요청 수  

- Custom metrics  
- 커스텀 메트릭  

You specify a target utilization, for example, 50% CPU utilization.  
목표 사용률을 지정합니다. 예: CPU 50%  
(목표 설정)

Based on historical data, a forecast is created, and your ASG scales accordingly.  
과거 데이터를 기반으로 예측이 생성되고 ASG가 이에 따라 스케일링됩니다.  
(작동 방식)

Note: Demonstrating predictive scaling requires enabling it for an extended period and having application usage data.  
참고: 예측 스케일링 시연은 장기간 활성화 및 애플리케이션 사용 데이터가 필요합니다.  
(제약 조건)

---

## Dynamic Scaling Policies  
## 동적 스케일링 정책  

Dynamic scaling policies include three options:  
동적 스케일링 정책에는 세 가지 옵션이 있습니다.  
(옵션 안내)

- Target tracking  
- 타깃 트래킹  

- Step scaling  
- 스텝 스케일링  

- Simple scaling  
- 심플 스케일링  

Let's examine each starting with simple scaling.  
각 정책을 살펴보되, 먼저 심플 스케일링부터 시작합니다.  
(순서 안내)

---

## Simple Scaling  
## 심플 스케일링  

In simple scaling, you specify:  
심플 스케일링에서는 다음을 지정합니다.  
(설정 항목)

- A name for the policy  
- 정책 이름  

- A CloudWatch alarm that triggers scaling  
- 스케일링을 트리거하는 CloudWatch 알람  

- The adjustment to capacity (e.g., add 2 instances)  
- 용량 조정(예: 인스턴스 2개 추가)  

- The minimum increment for capacity changes  
- 용량 변경 최소 단위  

This policy adds or removes instances when the alarm is triggered.  
알람이 트리거될 때 인스턴스를 추가하거나 제거합니다.  
(정책 동작)

---

## Step Scaling  
## 스텝 스케일링  

Step scaling allows multiple alarms with different thresholds.  
스텝 스케일링은 서로 다른 임계치를 가진 여러 알람을 허용합니다.  
(설명)

Based on the alarm value:  
알람 값에 따라:  
(조건 설명)

- If the alarm value is very high, add a larger number of capacity units (e.g., 10)  
- 알람 값이 매우 높으면 더 많은 용량 단위 추가(예: 10개)  

- If the alarm value is moderately high, add fewer units (e.g., 1)  
- 알람 값이 중간 정도면 적은 단위 추가(예: 1개)  

This provides more granular control over scaling actions.  
이로써 스케일링 작업을 더 세밀하게 제어할 수 있습니다.  
(장점)

---

## Target Tracking Scaling Policy  
## 타깃 트래킹 스케일링 정책  

Target tracking automatically creates CloudWatch alarms for you.  
타깃 트래킹은 자동으로 CloudWatch 알람을 생성합니다.  
(자동화)

For example, you can create a policy to maintain average CPU utilization at a target value, such as 40%.  
예: 평균 CPU 사용률을 40% 목표 값으로 유지하도록 정책 생성 가능  
(예시)

When CPU utilization exceeds this target, the ASG adds capacity to bring it back to the target.  
CPU 사용률이 목표를 초과하면 ASG가 용량을 추가하여 목표로 맞춥니다.  
(동작 원리)

Let's create a target tracking policy named "target tracking policy" that tracks average CPU utilization with a target value of 40%.  
평균 CPU 사용률을 40%로 유지하는 "target tracking policy"를 생성해봅니다.  
(실습)

---

## Configuring Capacity Limits  
## 용량 제한 구성  

Set the desired capacity to 1, and set the maximum capacity to 3 (or 2) to allow scaling from 1 to 3 instances.  
원하는 용량을 1로, 최대 용량을 3(또는 2)로 설정하여 1~3 인스턴스 스케일링 가능  
(용량 범위 설정)

The goal is to maintain CPU utilization at 40% by scaling the number of instances accordingly.  
인스턴스 수를 조정하여 CPU 사용률을 40%로 유지하는 것이 목표입니다.  
(목적)

---

## Monitoring CPU Utilization  
## CPU 사용률 모니터링  

Currently, CPU utilization is near zero because the EC2 instance is idle.  
현재 EC2 인스턴스가 유휴 상태라 CPU 사용률이 거의 0입니다.  
(상태 설명)

To test scaling, we will stress the EC2 instance to increase CPU utilization to 100%.  
스케일링 테스트를 위해 EC2 인스턴스에 부하를 걸어 CPU 사용률을 100%로 올립니다.  
(실습 준비)

---

## Installing Stress Tool on EC2 Instance  
## EC2 인스턴스에 Stress 도구 설치  

Connect to the EC2 instance using EC2 Instance Connect.  
EC2 인스턴스 커넥트를 사용하여 연결합니다.  
(접속)

Run the following commands to install the stress tool on Amazon Linux 2:  
Amazon Linux 2에 Stress 도구를 설치하기 위해 다음 명령 실행:  
(설치)

```bash
sudo yum install -y epel-release
sudo yum install -y stress
````

---

## Running Stress to Maximize CPU Usage

## CPU 사용률 최대화를 위한 Stress 실행

Run the following command to stress 4 CPU cores, driving CPU utilization to 100%:
다음 명령으로 4개의 CPU 코어에 부하를 걸어 CPU 사용률 100% 달성:
(실행)

```bash
stress -c 4
```

---

## Observing Scaling Activity

## 스케일링 활동 관찰

As CPU utilization spikes, the ASG monitoring should detect this and trigger scaling actions.
CPU 사용률 급증 시 ASG 모니터링이 이를 감지하고 스케일링을 트리거합니다.
(관찰)

The ASG will increase the number of instances from 1 to 2 based on the target tracking policy.
ASG는 타깃 트래킹 정책에 따라 인스턴스 수를 1에서 2로 증가시킵니다.
(동작 확인)

---

## Viewing Scaling Activity

## 스케일링 활동 확인

In the ASG Activity History, you will see an alarm triggered by the target tracking policy, causing capacity to increase from one to two instances.
ASG 활동 내역에서 타깃 트래킹 정책에 의해 알람이 트리거되고 인스턴스 수가 1→2로 증가하는 것을 확인할 수 있습니다.
(관찰 방법)

Instance Management will show two EC2 instances running due to scaling.
인스턴스 관리에서 스케일링으로 인해 실행 중인 2개의 EC2 인스턴스를 볼 수 있습니다.
(결과 확인)

---

## Monitoring CPU Utilization at EC2 Level

## EC2 수준에서 CPU 사용률 모니터링

EC2 monitoring will show CPU utilization reaching very high values, triggering scaling.
EC2 모니터링에서 CPU 사용률이 높게 올라가 스케일링을 트리거하는 것을 볼 수 있습니다.
(모니터링 확인)

This confirms that the target tracking policy is functioning as expected.
타깃 트래킹 정책이 정상 작동함을 확인합니다.
(검증)

---

## CloudWatch Alarms for Target Tracking

## 타깃 트래킹을 위한 CloudWatch 알람

In the CloudWatch service, under Alarms, two alarms are created by the target tracking policy:
CloudWatch 서비스의 알람 섹션에 타깃 트래킹 정책으로 두 개 알람이 생성됩니다.
(설정 확인)

* AlarmHigh: triggers scale out when CPU utilization exceeds 40% for 3 data points within 3 minutes

* AlarmHigh: CPU 사용률이 3분 동안 3 데이터 포인트에서 40% 초과 시 스케일 아웃

* AlarmLow: triggers scale in when CPU utilization is below 28% for 15 data points

* AlarmLow: CPU 사용률이 15 데이터 포인트 동안 28% 이하일 때 스케일 인

These alarms control scaling actions automatically.
이 알람들이 스케일링 작업을 자동으로 제어합니다


.
(자동화 확인)

---

## Stopping Stress and Triggering Scale In

## Stress 종료 및 스케일 인 트리거

To reduce CPU utilization and trigger scale in:
CPU 사용률을 낮추고 스케일 인을 트리거하려면:
(목적)

* Stop the stress command or reboot the EC2 instances
* Stress 명령 종료 또는 EC2 인스턴스 재부팅

This will cause CPU utilization to drop, triggering scale in actions after the defined thresholds are met.
CPU 사용률이 낮아져 정의된 임계치 충족 시 스케일 인 작업이 트리거됩니다.
(결과)

---

## Rebooting EC2 Instances

## EC2 인스턴스 재부팅

Reboot the instances to stop the stress workload and reduce CPU usage:
Stress 작업을 종료하고 CPU 사용률을 낮추기 위해 인스턴스를 재부팅:
(실행)

```bash
sudo reboot
```

---

## Observing Scale In Actions

## 스케일 인 동작 관찰

After CPU utilization drops below the threshold, the ASG will scale in by terminating instances.
CPU 사용률이 임계치 아래로 떨어지면 ASG가 인스턴스를 종료하며 스케일 인합니다.
(관찰)

Activity History will show capacity decreasing from 3 to 2, then to 1 instance.
활동 내역에서 용량이 3→2→1로 감소하는 것을 확인할 수 있습니다.
(결과)

Instance Management will reflect terminated instances accordingly.
인스턴스 관리에서도 종료된 인스턴스가 반영됩니다.
(결과)

---

## Visualizing CPU Utilization and Alarms

## CPU 사용률 및 알람 시각화

The CPU utilization graph shows spikes and drops corresponding to scaling events.
CPU 사용률 그래프에서 스케일링 이벤트에 따른 급등과 급락을 확인할 수 있습니다.
(그래프 확인)

When CPU utilization falls below the lower threshold, the alarm state triggers scale in actions.
CPU 사용률이 하한선 아래로 내려가면 알람 상태가 스케일 인 작업을 트리거합니다.
(동작 확인)

This demonstrates the effectiveness of target tracking policies in maintaining desired performance levels.
이는 목표 성능 수준을 유지하는 타깃 트래킹 정책의 효과를 보여줍니다.
(결론)

---

## Cleanup

## 정리

When finished, remember to delete the scaling policy to clean up resources.
작업 완료 후, 리소스 정리를 위해 스케일링 정책을 삭제합니다.
(정리)

---

## Key Takeaways

## 핵심 요약

* Scheduled actions allow you to plan scaling events based on predictable future events.

* 예약 작업은 예측 가능한 미래 이벤트에 따라 스케일링을 계획할 수 있습니다.

* Predictive scaling policies use machine learning to forecast demand and adjust capacity accordingly.

* 예측 스케일링 정책은 머신러닝으로 수요를 예측하고 용량을 조정합니다.

* Dynamic scaling policies include simple scaling, step scaling, and target tracking, each with different mechanisms for adjusting capacity.

* 동적 스케일링 정책은 심플, 스텝, 타깃 트래킹으로 구성되며 각각 용량 조정 메커니즘이 다릅니다.

* Target tracking policies automatically adjust capacity to maintain a specified metric, such as CPU utilization, using CloudWatch alarms.

* 타깃 트래킹 정책은 CloudWatch 알람을 사용하여 CPU 사용률과 같은 지정된 메트릭을 유지하도록 용량을 자동 조정합니다.

---

🎮 **게임 보상 지급**  
- 경험치: **+250XP**  
- 아이템: **"ASG 스케일링 마스터" (+25% 스케일링 효율)**  
- 업적 달성: **"자동 스케일링 실습 완료"** 🏆  

다음 단계로 **예측 스케일링 실습 + ML 기반 수요 예측** 자료도 만들어 실습 가능하게 정리할 수 있습니다.
