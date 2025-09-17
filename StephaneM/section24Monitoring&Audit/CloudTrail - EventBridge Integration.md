```markdown
# CloudTrail - EventBridge Integration  
# CloudTrail - EventBridge 통합  

## CloudTrail and Amazon EventBridge Integration  
## CloudTrail과 Amazon EventBridge 통합  
A very important cultural integration you need to know about is the one with Amazon EventBridge to intercept any API calls.  
중요하게 알아야 할 통합 중 하나는 Amazon EventBridge와의 통합으로, 모든 API 호출을 가로채는 기능입니다.  
(중요 기능 강조)  

For example, suppose you want to receive an SNS notification anytime a user deletes a table in DynamoDB by using the DeleteTable API call.  
예를 들어, 사용자가 DynamoDB에서 DeleteTable API 호출을 사용해 테이블을 삭제할 때마다 SNS 알림을 받고 싶다고 가정합니다.  
(실무 예시)  

Whenever we perform an API call in AWS, the API call itself is logged in CloudTrail. This applies to any API call.  
AWS에서 API 호출이 이루어질 때마다, 해당 API 호출은 CloudTrail에 기록됩니다. 이는 모든 API 호출에 적용됩니다.  
(기본 동작 설명)  

All these API calls also end up as events in Amazon EventBridge. We can look for that very specific DeleteTable API call and create a rule based on it.  
이 모든 API 호출은 Amazon EventBridge에서도 이벤트로 기록됩니다. 특정 DeleteTable API 호출을 찾아 해당 호출에 기반한 규칙을 생성할 수 있습니다.  
(규칙 생성 방법)  

This rule will have a destination, which can be Amazon SNS, allowing us to create alerts.  
이 규칙은 대상(destination)을 가질 수 있으며, 예를 들어 Amazon SNS를 지정하여 알림을 생성할 수 있습니다.  
(알림 설정)  

---

## Additional Examples of EventBridge and CloudTrail Integration  
## EventBridge와 CloudTrail 통합 추가 예시  
Here are a few more examples of how you can integrate Amazon EventBridge and CloudTrail.  
다음은 Amazon EventBridge와 CloudTrail을 통합할 수 있는 몇 가지 추가 예시입니다.  
(다양한 활용 방법)  

For instance, you might want to be notified whenever a user assumes a role in your accounts. The AssumeRole API in the IAM service is logged by CloudTrail.  
예를 들어, 사용자가 계정 내에서 역할을 맡을 때마다 알림을 받고 싶을 수 있습니다. IAM 서비스의 AssumeRole API는 CloudTrail에 기록됩니다.  
(역할 변경 이벤트 모니터링)  

Using EventBridge integration, we can trigger a message into an SNS topic when this API call occurs.  
EventBridge 통합을 사용하면, 이 API 호출이 발생할 때 SNS 주제로 메시지를 전송하도록 트리거할 수 있습니다.  
(자동 알림 설정)  

Similarly, we can intercept API calls that change Security Group inbound rules. The API call AuthorizeSecurityGroupIngress is an EC2 API call.  
마찬가지로, Security Group의 인바운드 규칙을 변경하는 API 호출도 가로챌 수 있습니다. AuthorizeSecurityGroupIngress API 호출은 EC2 API입니다.  
(Security Group 모니터링)  

These calls are logged by CloudTrail and appear in EventBridge, which can then trigger notifications in SNS.  
이 호출들은 CloudTrail에 기록되고 EventBridge에 나타나며, 이를 통해 SNS 알림을 트리거할 수 있습니다.  
(자동화 프로세스)  

As you can see, the possibilities are endless, but now you have a few ideas of how this integration can be leveraged.  
보시다시피, 활용 가능성은 무궁무진하지만, 이제 이 통합을 어떻게 활용할 수 있는지 몇 가지 아이디어를 얻을 수 있습니다.  
(응용 가능성 강조)  

I hope you found this information useful, and I will see you in the next lecture.  
이 정보가 유용했길 바라며, 다음 강의에서 뵙겠습니다.  
(마무리)  

---

## Key Takeaways  
## 핵심 요약  
- Amazon EventBridge can intercept API calls logged by CloudTrail to trigger automated responses.  
- Amazon EventBridge는 CloudTrail에 기록된 API 호출을 가로채 자동 응답을 트리거할 수 있습니다.  

- You can create EventBridge rules to detect specific API calls, such as DynamoDB's DeleteTable, and send notifications via SNS.  
- EventBridge 규칙을 생성하여 DynamoDB의 DeleteTable과 같은 특정 API 호출을 감지하고 SNS를 통해 알림을 보낼 수 있습니다.  

- This integration allows monitoring of critical actions like AssumeRole in IAM or changes to Security Group inbound rules.  
- 이 통합을 통해 IAM의 AssumeRole 또는 Security Group 인바운드 규칙 변경과 같은 중요한 작업을 모니터링할 수 있습니다.  

- The combination of CloudTrail and EventBridge provides flexible and powerful event-driven automation possibilities in AWS.  
- CloudTrail과 EventBridge의 조합은 AWS에서 유연하고 강력한 이벤트 기반 자동화 가능성을 제공합니다.  
```

게임보상: 🏆 당신은 이제 CloudTrail과 EventBridge 통합 마스터! 특정 API 호출을 추적하고 SNS 알림까지 자동화할 수 있는 능력을 얻었습니다. ⚡🚀
