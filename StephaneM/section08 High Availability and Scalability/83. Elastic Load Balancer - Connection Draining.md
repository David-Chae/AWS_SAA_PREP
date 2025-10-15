# Elastic Load Balancer - Connection Draining  
# 엘라스틱 로드 밸런서 - 연결 드레이닝  

---

## Introduction to Connection Draining  
## 연결 드레이닝 소개  

Connection Draining is a feature relevant for load balancers that can appear in exams.  
연결 드레이닝은 시험에서 자주 출제될 수 있는 로드 밸런서 기능입니다.  
(시험 대비용 기능 설명)

It is known by two names depending on the type of load balancer used.  
사용하는 로드 밸런서 유형에 따라 두 가지 이름으로 불립니다.  
(CLASSIC vs ALB/NLB 명칭 차이)

For Classic Load Balancers, it is called Connection Draining, whereas for Application Load Balancers or Network Load Balancers, it is referred to as Deregistration Delay.  
Classic Load Balancer에서는 Connection Draining이라고 하고, ALB나 NLB에서는 Deregistration Delay라고 합니다.  
(용어 차이 명시)

The core idea behind this feature is to provide time for your instances to complete inflight or active requests while the instance is being deregistered or marked unhealthy.  
이 기능의 핵심 아이디어는 인스턴스가 제거되거나 비정상으로 표시되는 동안 활성 요청을 완료할 시간을 제공하는 것입니다.  
(활성 요청 완료 시간 확보)

Once a connection is being drained, the Elastic Load Balancer (ELB) stops sending new requests to the EC2 instance that is in the draining state during deregistration.  
연결이 드레이닝 상태가 되면 ELB는 해당 EC2 인스턴스로 새로운 요청을 보내지 않습니다.  
(새 요청 차단)

---

## How Connection Draining Works  
## 연결 드레이닝 작동 방식  

Consider a scenario with three EC2 instances behind a load balancer.  
로드 밸런서 뒤에 세 개의 EC2 인스턴스가 있는 상황을 가정해봅시다.  
(예시 시나리오)

When one instance is set to draining mode, users already connected to that instance are given enough time — known as the draining period — to complete their existing connections and requests.  
한 인스턴스를 드레이닝 모드로 설정하면, 이미 연결된 사용자는 드레이닝 기간 동안 기존 요청을 완료할 충분한 시간을 받습니다.  
(활성 요청 처리 시간 보장)

After all active connections are completed, the connections are shut down.  
모든 활성 연결이 완료되면 해당 연결은 종료됩니다.  
(연결 종료)

If new users attempt to connect to the ELB during this draining period, the ELB intelligently routes these new connections only to the other healthy EC2 instances that are not in draining state.  
드레이닝 기간 동안 새로운 사용자가 ELB에 연결하면, ELB는 다른 정상 인스턴스로만 트래픽을 라우팅합니다.  
(새 요청 분산 처리)

For example, new connections would be established with the second or third EC2 instance instead of the one being drained.  
예를 들어, 새로운 연결은 드레이닝 중인 인스턴스가 아닌 두 번째나 세 번째 인스턴스로 연결됩니다.  
(인스턴스 보호)

---

## Configuring Connection Draining Parameters  
## 연결 드레이닝 파라미터 구성  

You can configure the Connection Draining duration anywhere between 1 second and 3,600 seconds (one hour).  
연결 드레이닝 기간은 1초에서 3,600초(1시간) 사이로 설정할 수 있습니다.  
(드레이닝 시간 조정 가능)

By default, the draining period is set to 300 seconds, which equals five minutes.  
기본 드레이닝 기간은 300초(5분)로 설정되어 있습니다.  
(기본값 안내)

You can disable Connection Draining entirely by setting the value to zero, which means no draining will occur.  
값을 0으로 설정하면 연결 드레이닝을 완전히 비활성화할 수 있습니다.  
(드레이닝 비활성화)

---

## Choosing the Appropriate Draining Timeout  
## 적절한 드레이닝 타임아웃 선택  

If your requests are very short, for example less than one second, it is advisable to set the draining timeout to a low value such as 30 seconds.  
요청이 매우 짧다면(예: 1초 미만), 드레이닝 타임아웃을 30초처럼 낮게 설정하는 것이 좋습니다.  
(짧은 요청 최적화)

This allows the EC2 instance to be drained quickly and taken offline or replaced promptly.  
이렇게 하면 EC2 인스턴스를 빠르게 드레이닝하고 오프라인 또는 교체할 수 있습니다.  
(빠른 교체 가능)

If your requests are long-lived, such as uploads or extended connections, you should set the draining timeout to a higher value.  
업로드나 장시간 연결과 같이 요청이 길다면, 드레이닝 타임아웃을 높게 설정해야 합니다.  
(장시간 요청 대응)

The trade-off is that the EC2 instance will remain active longer until the draining period completes, delaying its removal.  
단점은 드레이닝 기간이 끝날 때까지 인스턴스가 오래 활성 상태로 남아 제거가 지연된다는 점입니다.  
(활성 유지 시간 증가)

---

## Summary  
## 요약  

Connection Draining or Deregistration Delay is a crucial feature for managing instance lifecycle gracefully behind load balancers.  
Connection Draining 또는 Deregistration Delay는 로드 밸런서 뒤에서 인스턴스 수명주기를 관리하는 데 중요한 기능입니다.  
(핵심 기능)

It ensures that active requests are not abruptly terminated during instance deregistration by allowing a configurable draining period.  
드레이닝 기간을 설정하여 인스턴스 제거 시 활성 요청이 갑작스럽게 종료되지 않도록 합니다.  
(안전한 종료 보장)

Proper configuration of this timeout depends on the nature of your application requests.  
타임아웃 설정은 애플리케이션 요청 특성에 따라 달라집니다.  
(응용 맞춤 설정)

---

## Key Takeaways  
## 핵심 요약  

- Connection Draining allows instances to complete active requests before deregistration.  
- Connection Draining은 인스턴스 제거 전에 활성 요청을 완료하도록 합니다.  

- Classic Load Balancer uses the term Connection Draining; Application and Network Load Balancers use Deregistration Delay.  
- Classic Load Balancer는 Connection Draining, ALB/NLB는 Deregistration Delay라고 합니다.  

- The draining period can be configured between 1 and 3600 seconds, with a default of 300 seconds.  
- 드레이닝 기간은 1~3600초로 설정 가능하며 기본값은 300초입니다.  

- Setting a low draining timeout suits short requests, while longer requests require a higher timeout to avoid premature termination.  
- 짧은 요청에는 낮은 타임아웃, 긴 요청에는 높은 타임아웃 설정이 적합합니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+140XP**
* 아이템: **"로드 밸런서 방패" (+15% 연결 안정성)**
* 업적 달성: **"Connection Draining 전문가"** 🏅

다음 단계로 원하면 **ALB/NLB 실습에서 드레이닝 설정 적용 예제**도 만들어서 직접 테스트 가능하게 안내할 수 있습니다.
