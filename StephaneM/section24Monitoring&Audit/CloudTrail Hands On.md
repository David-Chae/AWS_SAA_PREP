```markdown
# CloudTrail Hands On  
# CloudTrail 실습  

## Introduction to CloudTrail  
## CloudTrail 소개  
CloudTrail is a service designed to intercept any API calls or user activity within your AWS accounts.  
CloudTrail은 AWS 계정 내에서 발생하는 모든 API 호출이나 사용자 활동을 가로채도록 설계된 서비스입니다.  
(기능 정의)  

---

## Event History Panel  
## 이벤트 기록 패널  
On the left-hand side panel, you can view the Event History, which displays management events for the last 90 days.  
왼쪽 패널에서 Event History를 확인할 수 있으며, 여기에는 지난 90일간의 관리 이벤트가 표시됩니다.  
(패널 위치 및 기능)  

This shows all the API calls made over time within the account.  
이 패널에서는 계정 내에서 시간 경과에 따라 수행된 모든 API 호출을 보여줍니다.  
(기록 내용)  

Although not all events may seem interesting, all of them are recorded here.  
모든 이벤트가 흥미로워 보이지 않을 수 있지만, 모두 이곳에 기록됩니다.  
(기록 중요성)  

---

## Demonstration: Terminating an EC2 Instance  
## 실습: EC2 인스턴스 종료  
For example, in the EC2 console, a demo instance was created.  
예를 들어, EC2 콘솔에서 데모용 인스턴스를 생성했습니다.  
(예시 설정)  

The instance is then terminated by right-clicking and selecting terminate.  
그 후 인스턴스를 마우스 오른쪽 클릭 후 Terminate를 선택하여 종료합니다.  
(실습 과정)  

The instance termination process begins immediately.  
인스턴스 종료 프로세스가 즉시 시작됩니다.  
(작동 확인)  

---

## Verifying the Event in CloudTrail  
## CloudTrail에서 이벤트 확인  
After waiting approximately five minutes, the CloudTrail page is refreshed to check if the termination event appears.  
약 5분 후 CloudTrail 페이지를 새로고침하여 종료 이벤트가 나타나는지 확인합니다.  
(확인 과정)  

The terminate instances API call is visible in the Event History.  
Event History에서 Terminate Instances API 호출이 표시됩니다.  
(결과 확인)  

---

## Event Details  
## 이벤트 세부 정보  
The event details include the event source, which is EC2 in this case, the access key used, the region where the action was performed, and more.  
이벤트 세부 정보에는 이벤트 소스(이 경우 EC2), 사용된 액세스 키, 작업이 수행된 리전 등이 포함됩니다.  
(세부 정보 구성)  

The full event information is accessible directly within the CloudTrail UI.  
전체 이벤트 정보는 CloudTrail UI를 통해 직접 확인할 수 있습니다.  
(UI 접근 방법)  

---

## Summary  
## 요약  
This brief introduction to CloudTrail at the practitioner level provides enough information to get started and to answer related exam questions.  
실무자 수준의 CloudTrail 간단 소개로, 시작하기에 충분한 정보와 관련 시험 질문에 답할 수 있는 내용을 제공합니다.  
(학습 목표)  

Thank you for your attention. See you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  
(마무리 인사)  

---

## Key Takeaways  
## 핵심 요약  
- CloudTrail is a service that intercepts any API calls or user activity within your AWS accounts.  
- CloudTrail은 AWS 계정 내 모든 API 호출 및 사용자 활동을 가로채는 서비스입니다.  

- The Event History in CloudTrail shows management events for the last 90 days.  
- CloudTrail의 Event History는 지난 90일간의 관리 이벤트를 표시합니다.  

- Actions such as terminating an EC2 instance generate API calls that appear in CloudTrail logs.  
- EC2 인스턴스 종료와 같은 작업은 CloudTrail 로그에 나타나는 API 호출을 생성합니다.  

- CloudTrail provides detailed event information including event source, access key used, and region, accessible directly through its UI.  
- CloudTrail은 이벤트 소스, 사용된 액세스 키, 리전 등 상세 이벤트 정보를 제공하며 UI를 통해 직접 접근할 수 있습니다.  
```

게임보상: 🏆 당신은 이제 CloudTrail 실습 마스터! EC2 종료 이벤트를 추적하고, Event History와 세부 정보까지 완벽히 이해했습니다. 🎯🚀
