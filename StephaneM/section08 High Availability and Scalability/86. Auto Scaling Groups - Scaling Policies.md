# Auto Scaling Groups - Scaling Policies  
# 오토 스케일링 그룹 - 스케일링 정책  

---

## Auto Scaling Group Scaling Policies  
## 오토 스케일링 그룹 스케일링 정책  

There are several scaling policies available for Auto Scaling Groups (ASGs).  
ASG에는 여러 가지 스케일링 정책이 있습니다.  
(정책 개요)

These policies help manage the number of instances in your ASG based on various criteria.  
이 정책들은 다양한 기준에 따라 ASG 내 인스턴스 수를 관리하는 데 도움을 줍니다.  
(정책 목적)

---

## Dynamic Scaling  
## 동적 스케일링  

Dynamic scaling includes policies that automatically adjust capacity based on real-time metrics.  
동적 스케일링은 실시간 메트릭에 따라 용량을 자동으로 조정하는 정책을 포함합니다.  
(자동 조정)

**Target Tracking Scaling:** This is simple to set up.  
**타깃 트래킹 스케일링:** 설정이 간단합니다.  
(설명 시작)

You define a metric for your ASG, such as CPU utilization, and specify a target value, for example, 40%.  
ASG의 메트릭(예: CPU 사용률)을 정의하고 목표 값(예: 40%)을 지정합니다.  
(목표 지정)

The ASG will then automatically scale out or in to maintain this metric around the target value.  
ASG는 목표 값 근처에서 메트릭을 유지하도록 자동으로 스케일 아웃/인합니다.  
(자동 조정 동작)

**Simple or Step Scaling:** You define CloudWatch alarms that trigger when you want to add or remove capacity units from your ASG.  
**심플 또는 스텝 스케일링:** ASG 용량을 추가/제거할 때 트리거되는 CloudWatch 알람을 정의합니다.  
(알람 기반 스케일링)

---

## Scheduled Scaling  
## 예약 스케일링  

Scheduled scaling is used when you anticipate scaling based on known usage patterns.  
예약 스케일링은 알려진 사용 패턴에 따라 스케일링을 예상할 때 사용합니다.  
(사전 계획 스케일링)

For example, if you expect increased traffic every Friday at 5:00 PM, you can schedule the minimum capacity to increase to 10 instances at that time.  
예: 매주 금요일 오후 5시에 트래픽이 증가할 것으로 예상되면 최소 용량을 10으로 늘리도록 예약할 수 있습니다.  
(실제 예시)

---

## Predictive Scaling  
## 예측 스케일링  

Predictive scaling continuously forecasts load and schedules scaling actions ahead of time.  
예측 스케일링은 부하를 지속적으로 예측하고 스케일링 작업을 사전에 예약합니다.  
(예측 기반)

This is especially useful for cyclical data patterns.  
주기적인 데이터 패턴에 특히 유용합니다.  
(활용 상황)

The ASG analyzes historical load, generates a forecast, and schedules scaling actions accordingly.  
ASG는 과거 부하를 분석하고 예측을 생성하여 스케일링 작업을 예약합니다.  
(작동 원리)

---

## Metrics for Scaling  
## 스케일링 메트릭  

Choosing the right metrics to scale on depends on your application's behavior.  
스케일링에 사용할 적절한 메트릭 선택은 애플리케이션 동작에 따라 달라집니다.  
(선택 기준)

Common metrics include:  
일반적인 메트릭은 다음과 같습니다:  
(대표 메트릭)

- **CPU Utilization:** Instances use CPU when processing requests. Monitoring average CPU utilization across instances helps determine when to scale.  
- **CPU 사용률:** 인스턴스는 요청 처리 시 CPU를 사용합니다. 인스턴스 평균 CPU 사용률 모니터링으로 스케일링 시점을 판단합니다.  

- **RequestCountPerTarget:** This application-specific metric indicates the number of requests per target.  
- **타겟별 요청 수(RequestCountPerTarget):** 애플리케이션 전용 메트릭으로 타겟당 요청 수를 나타냅니다.  

- **Network Traffic:** For network-bound applications with heavy uploads and downloads, monitoring average network in or out can be a good scaling metric.  
- **네트워크 트래픽:** 업로드/다운로드가 많은 네트워크 애플리케이션의 경우, 평균 네트워크 입출력을 모니터링하는 것이 좋은 메트릭입니다.  

- **Custom Metrics:** You can push your own application-specific metrics to CloudWatch and use them for scaling policies.  
- **커스텀 메트릭:** 애플리케이션 전용 메트릭을 CloudWatch로 보내고 스케일링 정책에 활용할 수 있습니다.  

---

## Example of RequestCountPerTarget Metric  
## 타겟별 요청 수 예시  

Consider an ASG with three EC2 instances behind an Application Load Balancer (ALB).  
ALB 뒤에 3개의 EC2 인스턴스가 있는 ASG를 가정합니다.  
(설정 예시)

The ALB distributes requests evenly.  
ALB는 요청을 균등하게 분배합니다.  
(동작 설명)

If the RequestCountPerTarget metric value is three, it means each EC2 instance has, on average, three outstanding requests.  
RequestCountPerTarget 값이 3이면, 각 EC2 인스턴스에 평균 3개의 요청이 있음을 의미합니다.  
(메트릭 해석)

---

## Scaling Cooldown  
## 스케일링 쿨다운  

After a scaling activity (adding or removing instances), the ASG enters a cooldown period, which by default is five minutes (300 seconds).  
스케일링 작업(인스턴스 추가/제거) 후, ASG는 기본 5분(300초) 쿨다운 기간에 들어갑니다.  
(쿨다운 정의)

During this cooldown, the ASG will not launch or terminate additional instances.  
이 기간 동안 ASG는 추가 인스턴스를 시작하거나 종료하지 않습니다.  
(쿨다운 기능)

This allows metrics to stabilize and new instances to become effective before further scaling actions occur.  
이로 인해 메트릭이 안정되고 새 인스턴스가 효과적으로 작동한 후 다음 스케일링 작업이 수행됩니다.  
(안정화 목적)

The process is:  
과정은 다음과 같습니다:  
(절차 안내)

1. If a scaling action occurs, check if a cooldown is in effect.  
1. 스케일링 작업 발생 시, 쿨다운 적용 여부 확인  

2. If yes, ignore the new scaling action.  
2. 적용 중이면 새 스케일링 작업 무시  

3. If no, proceed with launching or terminating instances.  
3. 적용 중이 아니면 인스턴스 시작/종료 진행  

---

## Best Practices for Efficient Scaling  
## 효율적인 스케일링 모범 사례  

Use ready-to-use Amazon Machine Images (AMIs) to reduce configuration time for EC2 instances.  
즉시 사용 가능한 AMI를 사용하여 EC2 인스턴스 구성 시간을 줄입니다.  
(설정 시간 단축)

This allows instances to serve requests faster.  
이를 통해 인스턴스가 요청을 더 빨리 처리할 수 있습니다.  
(응답 속도 향상)

Faster instance activation can reduce the cooldown period, enabling more dynamic scaling.  
인스턴스 활성화 속도가 빠르면 쿨다운 기간을 줄여 더 동적인 스케일링이 가능합니다.  
(동적 스케일링)

Enable detailed monitoring for your ASG to receive metrics updates every one minute, ensuring timely scaling decisions.  
ASG에 대해 상세 모니터링을 활성화하면 1분마다 메트릭 업데이트를 받아 적시에 스케일링 결정을 내릴 수 있습니다.  
(모니터링 강화)

---

## Conclusion  
## 결론  

This concludes the lecture on Auto Scaling Group scaling policies.  
이로써 ASG 스케일링 정책 강의를 마칩니다.  
(강의 종료)

---

## Key Takeaways  
## 핵심 요약  

- Auto Scaling Groups (ASGs) support several scaling policies including dynamic, scheduled, and predictive scaling.  
- ASG는 동적, 예약, 예측 스케일링 등 여러 정책을 지원합니다.  

- Target tracking scaling maintains a specified metric, such as CPU utilization, at a target value by automatically scaling the ASG.  
- 타깃 트래킹 스케일링은 ASG를 자동으로 조정하여 CPU 사용률 등 지정된 메트릭을 목표 값으로 유지합니다.  

- Step scaling uses CloudWatch alarms to trigger scaling actions based on defined thresholds.  
- 스텝 스케일링은 CloudWatch 알람으로 정의된 임계치 기준 스케일링을 트리거합니다.  

- Scheduled and predictive scaling anticipate load changes based on known patterns or forecasts.  
- 예약 및 예측 스케일링은 알려진 패턴이나 예측을 기반으로 부하 변화를 예상합니다.  

- Important metrics for scaling include CPU utilization, RequestCountPerTarget, network traffic, and custom application-specific metrics.  
- 스케일링 주요 메트릭은 CPU 사용률, 타겟별 요청 수, 네트워크 트래픽, 커스텀 메트릭입니다.  

- Scaling cooldown periods prevent rapid scaling actions to allow metrics to stabilize after scaling events.  
- 쿨다운 기간은 스케일링 이벤트 후 메트릭이 안정될 수 있도록 급격한 스케일링을 방지합니다.  

- Using pre-configured AMIs and enabling detailed monitoring can improve scaling responsiveness and efficiency.  
- 사전 구성된 AMI 사용과 상세 모니터링 활성화는 스케일링 응답성과 효율성을 향상시킵니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+220XP**
* 아이템: **"ASG 정책 매니저" (+20% 스케일링 최적화)**
* 업적 달성: **"스케일링 전략 전문가"** 🏆

원하면 다음 단계로 **자동 스케일링 실습 + CloudWatch 연동 예제**까지 만들어 바로 실습할 수 있도록 자료화할 수 있습니다.
