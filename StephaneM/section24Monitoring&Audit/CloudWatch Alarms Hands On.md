````markdown
# CloudWatch Alarms Hands On  
# CloudWatch 알람 실습  
(제목: 실습을 통해 CloudWatch 알람 설정 및 테스트 방법 학습)  

---

## Introduction to CloudWatch Alarms  
## CloudWatch 알람 소개  
In this session, we will create a CloudWatch alarm.  
이번 세션에서는 CloudWatch 알람을 생성해보겠습니다.  
(실습 목표 소개)  

First, we will quickly create an EC2 instance and then set up an alarm based on the CPU utilization metric.  
먼저 EC2 인스턴스를 빠르게 생성한 후, CPU 사용률 메트릭을 기반으로 알람을 설정합니다.  
(실습 순서 안내)  

We will launch a t2.micro EC2 instance.  
t2.micro EC2 인스턴스를 실행합니다.  
(인스턴스 유형 명시)  

I will proceed quickly to preview and launch the instance, confirming that I have the necessary key pair.  
키 페어가 준비되었는지 확인한 후, 인스턴스를 미리보기 및 실행을 빠르게 진행합니다.  
(실습 시점 설정)  

We do not need to keep the instance running for long; the goal is to create an alarm that will terminate the instance if the CPU utilization reaches 100%.  
인스턴스를 오래 유지할 필요는 없습니다. 목표는 CPU 사용률이 100%에 도달하면 인스턴스를 종료하는 알람을 만드는 것입니다.  
(알람 실습 목적)  

---

## Selecting the Metric for the Alarm  
## 알람용 메트릭 선택  
To create the alarm, we need to select a metric.  
알람을 생성하려면 메트릭을 선택해야 합니다.  
(메트릭 선택 중요)  

We will locate our EC2 instance by its instance ID and search for it in the metrics dashboard.  
인스턴스 ID로 EC2 인스턴스를 찾아 메트릭 대시보드에서 검색합니다.  
(실습 단계)  

It may take a few minutes for the metrics to populate after launching the instance.  
인스턴스를 실행한 후, 메트릭이 표시되기까지 몇 분 걸릴 수 있습니다.  
(실습 팁)  

After approximately five minutes, the metrics appear in the CloudWatch dashboard.  
약 5분 후, 메트릭이 CloudWatch 대시보드에 나타납니다.  
(대기 후 확인)  

Refreshing the page allows us to select the metric.  
페이지를 새로 고치면 메트릭을 선택할 수 있습니다.  
(실습 동작)  

We will choose the CPU utilization metric for our instance.  
인스턴스의 CPU 사용률 메트릭을 선택합니다.  
(모니터링 대상 메트릭 지정)  

---

## Configuring the Alarm Conditions  
## 알람 조건 구성  
We select the CPU utilization metric and choose how to compute it, such as average, sum, or maximum.  
CPU 사용률 메트릭을 선택하고 평균, 합계, 최대값 등 계산 방식을 선택합니다.  
(계산 방식 설정)  

The evaluation period is set to five minutes, which aligns with the metric's update frequency when detailed monitoring is not enabled.  
평가 기간은 5분으로 설정하며, 상세 모니터링이 비활성화된 경우 메트릭 업데이트 주기에 맞춥니다.  
(평가 기간 설정)  

Next, we set the alarm threshold.  
다음으로 알람 임계값을 설정합니다.  
(임계값 설정 단계)  

We choose a static threshold and specify that the alarm triggers if the CPU utilization is greater than 95% for three consecutive evaluation periods, which totals 15 minutes.  
정적 임계값을 선택하고, CPU 사용률이 95%를 초과하면 3번 연속 평가 기간 동안 알람이 트리거되도록 설정합니다(총 15분).  
(연속 사용률 기준 알람)  

This indicates a sustained high CPU usage that may signal an issue with the instance.  
이는 인스턴스에 문제가 있을 수 있는 지속적인 높은 CPU 사용률을 의미합니다.  
(실무 의미 설명)  

---

## Defining Alarm Actions  
## 알람 동작 정의  
When the alarm state is triggered, we can configure various actions.  
알람 상태가 트리거되면 다양한 동작을 구성할 수 있습니다.  
(알람 행동 설정)  

Options include sending notifications, triggering Auto Scaling actions, EC2 actions, or Systems Manager actions.  
옵션에는 알림 전송, 오토스케일링 동작, EC2 동작, Systems Manager 동작 등이 있습니다.  
(동작 종류)  

In this case, we choose an EC2 action to terminate the instance automatically if the alarm is in the alarm state.  
이번 실습에서는 알람 상태일 때 EC2 인스턴스를 자동으로 종료하는 EC2 동작을 선택합니다.  
(실습 목표 동작)  

This setup is useful when the application experiences a failure causing CPU utilization to remain at or above 95% for an extended period, and the only resolution is to terminate the instance.  
애플리케이션 장애로 CPU 사용률이 장시간 95% 이상 유지될 경우, 인스턴스를 종료하는 것이 유일한 해결책일 때 유용합니다.  
(실무 적용 설명)  

We name the alarm "Terminate EC2 on High CPU" and proceed to verify the configuration.  
알람 이름을 "Terminate EC2 on High CPU"로 지정하고 설정을 검토합니다.  
(알람 이름 지정 및 검토)  

The alarm initially shows insufficient data because it requires 15 minutes of data to evaluate the condition.  
알람은 초기에는 충분한 데이터가 없음을 표시하며, 조건 평가를 위해 15분 데이터가 필요합니다.  
(초기 상태 안내)  

The alarm will not trigger unless the CPU utilization reaches the threshold for the specified duration.  
CPU 사용률이 지정된 기간 동안 임계값에 도달하지 않으면 알람이 트리거되지 않습니다.  
(알람 트리거 조건)  

---

## Testing the Alarm  
## 알람 테스트  
To test the alarm without waiting for 15 minutes of high CPU usage, we can manually set the alarm state using the AWS CLI.  
15분 동안 CPU 사용률이 높아질 때까지 기다리지 않고, AWS CLI를 사용하여 알람 상태를 수동으로 설정할 수 있습니다.  
(실습 팁: 수동 테스트)  

The command used is set-alarm-state, which requires the alarm name, the state value, and a reason for the state change.  
사용되는 명령어는 set-alarm-state로, 알람 이름, 상태 값, 상태 변경 이유가 필요합니다.  
(CLI 명령어 설명)  

The command syntax is as follows:  
명령어 구문은 다음과 같습니다:  
```bash
aws cloudwatch set-alarm-state --alarm-name <alarm-name> --state-value ALARM --state-reason "testing"
````

Executing this command sets the alarm state to ALARM, simulating the condition where the CPU utilization exceeds the threshold.
이 명령을 실행하면 알람 상태가 ALARM으로 설정되어, CPU 사용률이 임계값을 초과한 조건을 시뮬레이션합니다.
(알람 시뮬레이션)

---

## Observing Alarm Effects

## 알람 효과 관찰

After setting the alarm state to ALARM, the CloudWatch console reflects the alarm status as "In Alarm."
알람 상태를 ALARM으로 설정하면, CloudWatch 콘솔에서 상태가 "In Alarm"으로 표시됩니다.
(알람 상태 확인)

The configured action triggers, terminating the EC2 instance automatically.
설정된 동작이 실행되어 EC2 인스턴스가 자동으로 종료됩니다.
(동작 결과)

The alarm history shows the transition from OK to In Alarm and confirms that the termination action was successfully executed.
알람 기록에는 OK에서 In Alarm으로의 전환이 표시되며, 종료 동작이 성공적으로 실행되었음을 확인할 수 있습니다.
(알람 이력 확인)

Refreshing the EC2 instances page shows that the instance is shutting down and being terminated due to the triggered alarm and the configured action.
EC2 인스턴스 페이지를 새로고침하면, 알람과 설정된 동작으로 인해 인스턴스가 종료 중임을 확인할 수 있습니다.
(실습 최종 확인)

---

## Conclusion

## 결론

This demonstration showed how to create a CloudWatch alarm based on CPU utilization for an EC2 instance, configure it to terminate the instance upon sustained high CPU usage, and test the alarm using the AWS CLI to simulate alarm conditions.
이번 실습에서는 EC2 인스턴스의 CPU 사용률을 기준으로 CloudWatch 알람을 생성하고, 지속적인 높은 CPU 사용 시 인스턴스를 종료하도록 설정하며, AWS CLI로 알람을 시뮬레이션하는 방법을 보여주었습니다.
(실습 요약)

I hope this explanation was clear and helpful.
설명이 명확하고 도움이 되었기를 바랍니다.
(강의 종료 멘트)

---

## Key Takeaways

## 핵심 요약

* Created an EC2 instance to monitor CPU utilization with CloudWatch Alarms.

* CloudWatch 알람으로 CPU 사용률을 모니터링할 EC2 인스턴스를 생성했습니다.

* Configured a CloudWatch alarm to trigger when CPU usage exceeds 95% for 15 minutes.

* CPU 사용률이 15분 동안 95%를 초과하면 알람이 트리거되도록 설정했습니다.

* Set up the alarm action to automatically terminate the EC2 instance upon alarm state.

* 알람 상태에서 EC2 인스턴스를 자동으로 종료하도록 알람 동작을 설정했습니다.

* Demonstrated using AWS CLI to manually set the alarm state for testing purposes.

* 테스트 목적으로 AWS CLI를 사용해 알람 상태를 수동으로 설정하는 방법을 시연했습니다.

```
🎮 **게임 보상**: 실습 완료! **+200 EXP**와 **“CloudWatch 알람 실습 마스터” 배지 🖥️** 획득!  
```
