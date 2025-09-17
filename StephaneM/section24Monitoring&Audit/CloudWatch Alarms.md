```markdown
# CloudWatch Alarms  
# CloudWatch 알람  
(제목: CloudWatch에서 알람 설정과 활용 방법)  

---

## Introduction to CloudWatch Alarms  
## CloudWatch 알람 소개  
CloudWatch Alarms are used to trigger notifications based on any metric.  
CloudWatch 알람은 어떤 메트릭이든 기준을 만족하면 알림을 트리거하는 데 사용됩니다.  
(메트릭 기반 알림 시스템 설명)  

You can define complex alarms with various options such as sampling, percentage, maximum, and more.  
샘플링, 퍼센트, 최대값 등 다양한 옵션을 사용하여 복잡한 알람을 정의할 수 있습니다.  
(세밀한 조건으로 알람 설정 가능)  

---

## Alarm States  
## 알람 상태  
An alarm has three states:  
알람에는 세 가지 상태가 있습니다:  

- OK: The alarm is not triggered.  
- OK: 알람이 트리거되지 않은 상태입니다.  

- INSUFFICIENT_DATA: There is not enough data for the alarm to determine a state.  
- INSUFFICIENT_DATA: 알람이 상태를 판단할 충분한 데이터가 없는 상태입니다.  

- ALARM: The threshold has been breached, and a notification will be sent.  
- ALARM: 임계값을 초과하여 알람이 트리거되고, 알림이 전송되는 상태입니다.  

---

## Alarm Evaluation Period  
## 알람 평가 기간  
The period defines how long the alarm evaluates the metric.  
평가 기간은 알람이 메트릭을 평가하는 시간을 정의합니다.  
(짧게도, 길게도 설정 가능)  

This period can be very short or very long and applies to high-resolution custom metrics as well.  
이 기간은 매우 짧거나 길 수 있으며, 고해상도 커스텀 메트릭에도 적용됩니다.  
(예: 10초, 30초, 60초 단위)  

---

## Alarm Targets  
## 알람 대상  
Alarms have three main targets:  
알람의 주요 대상은 세 가지입니다:  

- EC2 Instance Actions: Such as stopping, terminating, rebooting, or recovering an instance.  
- EC2 인스턴스 동작: 인스턴스 중지, 종료, 재부팅, 복구 등  

- Auto-Scaling Actions: For example, scaling out or scaling in.  
- 오토스케일링 동작: 예를 들어, 스케일 아웃 또는 스케일 인  

- Notifications: Sending alerts to the SNS service, which can trigger Lambda functions to perform various tasks based on the alarm breach.  
- 알림: SNS 서비스로 알림을 보내고, 이를 통해 Lambda 함수를 트리거하여 알람 상황에 맞는 작업 수행  

---

## Composite Alarms  
## 합성 알람  
CloudWatch Alarms monitor single metrics, but Composite Alarms allow monitoring the states of multiple alarms.  
CloudWatch 알람은 단일 메트릭을 모니터링하지만, 합성 알람은 여러 알람의 상태를 동시에 모니터링할 수 있습니다.  
(복합 조건 모니터링 가능)  

Each underlying alarm can rely on a different metric.  
각 기본 알람은 서로 다른 메트릭에 의존할 수 있습니다.  
(다양한 메트릭 통합 가능)  

Composite Alarms combine these alarms using logical operators such as AND or OR, providing flexibility in defining conditions.  
합성 알람은 AND 또는 OR와 같은 논리 연산자로 알람을 결합하여 조건 정의의 유연성을 제공합니다.  
(알람 조건 세분화 가능)  

Composite Alarms help reduce alarm noise by creating complex conditions.  
합성 알람은 복잡한 조건 설정을 통해 불필요한 알람을 줄이는 데 도움이 됩니다.  
(알람 노이즈 감소)  

For example, you might only want to be alerted when the CPU is high and the network is low, ignoring other combinations.  
예를 들어, CPU가 높고 네트워크가 낮을 때만 알림을 받고, 다른 조합은 무시할 수 있습니다.  
(실무 적용 예시)  

---

## Example of Composite Alarm  
## 합성 알람 예시  
Consider an EC2 instance with two underlying alarms:  
두 개의 기본 알람이 있는 EC2 인스턴스를 고려해 봅시다:  

- Alarm A monitors the CPU usage.  
- Alarm A는 CPU 사용량을 모니터링합니다.  

- Alarm B monitors the IOPS.  
- Alarm B는 IOPS를 모니터링합니다.  

The Composite Alarm is defined as the logical junction of Alarm A and Alarm B.  
합성 알람은 Alarm A와 Alarm B의 논리적 결합으로 정의됩니다.  

If both Alarm A and Alarm B are in the ALARM state, the Composite Alarm will also be in the ALARM state and can trigger an SNS notification.  
Alarm A와 Alarm B가 모두 ALARM 상태이면, 합성 알람도 ALARM 상태가 되고 SNS 알림을 트리거할 수 있습니다.  
(실시간 통합 알림 가능)  

---

## EC2 Instance Recovery  
## EC2 인스턴스 복구  
There are several status checks for EC2 instances:  
EC2 인스턴스에는 여러 상태 검사가 있습니다:  

- Instance Status Check: Checks the EC2 virtual machine.  
- 인스턴스 상태 검사: EC2 VM 확인  

- System Status Check: Checks the underlying hardware layer.  
- 시스템 상태 검사: 하드웨어 레이어 확인  

- Attached EBS Status Check: Checks the health of any attached EBS volumes.  
- 연결된 EBS 상태 검사: 연결된 EBS 볼륨 상태 확인  

You can define CloudWatch Alarms on these checks to monitor a specific EC2 instance.  
이러한 검사에 대해 CloudWatch 알람을 정의하여 특정 EC2 인스턴스를 모니터링할 수 있습니다.  
(자동화된 인스턴스 모니터링)  

If an alarm is breached, you can initiate an EC2 instance recovery.  
알람이 발동되면 EC2 인스턴스 복구를 시작할 수 있습니다.  
(문제 발생 시 자동 복구 가능)  

This process moves your instance from one host to another while retaining the same private IP, public IP, elastic IP, metadata, and placement group.  
이 과정에서 인스턴스는 동일한 프라이빗 IP, 퍼블릭 IP, 엘라스틱 IP, 메타데이터, 배치 그룹을 유지하며 다른 호스트로 이동합니다.  
(네트워크/설정 그대로 유지)  

Additionally, you can send alerts to an SNS topic to be notified when recovery occurs.  
복구가 진행되면 SNS 주제로 알림을 보내 확인할 수 있습니다.  
(자동 알림 기능 제공)  

---

## Additional Features of CloudWatch Alarms  
## CloudWatch 알람 추가 기능  
You can create alarms based on CloudWatch Logs metric filters.  
CloudWatch 로그 메트릭 필터를 기반으로 알람을 생성할 수 있습니다.  
(로그 기반 알람 트리거 가능)  

For example, if a specific word such as "error" appears too many times, an alarm can trigger and send a message to Amazon SNS.  
예를 들어 "error"라는 단어가 너무 많이 나타나면, 알람이 트리거되고 Amazon SNS로 메시지를 보낼 수 있습니다.  
(로그 내용에 따른 알람 가능)  

To test alarms and notifications, you can use the CLI command set-alarm-state.  
알람과 알림을 테스트하려면 CLI 명령어 **set-alarm-state**를 사용할 수 있습니다.  
(수동으로 알람 테스트 가능)  

This allows you to trigger an alarm manually, even if the threshold has not been reached, to verify that the alarm triggers the correct actions in your infrastructure.  
임계값에 도달하지 않아도 수동으로 알람을 트리거하여, 알람이 인프라에서 올바른 작업을 수행하는지 확인할 수 있습니다.  
(테스트 및 검증 기능)  

---

## Conclusion  
## 결론  
This concludes the discussion on CloudWatch Alarms.  
이로써 CloudWatch 알람에 대한 설명을 마칩니다.  
(강의 종료)  

These alarms provide powerful monitoring and automation capabilities for your AWS infrastructure.  
이 알람은 AWS 인프라에 강력한 모니터링과 자동화 기능을 제공합니다.  
(실무 활용 강조)  

---

## Key Takeaways  
## 핵심 요약  

- CloudWatch Alarms monitor metrics and trigger notifications based on defined thresholds.  
- CloudWatch 알람은 메트릭을 모니터링하고 정의된 임계값을 기준으로 알림을 트리거합니다.  

- Alarms have three states: OK, INSUFFICIENT_DATA, and ALARM.  
- 알람에는 세 가지 상태가 있습니다: OK, INSUFFICIENT_DATA, ALARM  

- Composite Alarms combine multiple alarms using logical conditions to reduce noise.  
- 합성 알람은 여러 알람을 논리 조건으로 결합하여 불필요한 알람을 줄입니다.  

- EC2 instance recovery can be automated through alarms monitoring status checks.  
- 상태 검사를 모니터링하는 알람을 통해 EC2 인스턴스 복구를 자동화할 수 있습니다.  
```

🎮 **게임 보상**: 이번 CloudWatch 알람 강의 완주로 **+150 EXP**와 **“알람 마스터” 배지 🔔** 획득!
