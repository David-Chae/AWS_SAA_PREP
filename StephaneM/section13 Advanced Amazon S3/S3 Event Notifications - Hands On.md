# S3 Event Notifications - Hands On  
# S3 이벤트 알림 실습  

---

## Introduction to S3 Event Notifications  
## S3 이벤트 알림 소개  

In this demonstration, we will explore how to set up S3 Event Notifications.  
이번 실습에서는 S3 이벤트 알림을 설정하는 방법을 알아봅니다.  

The first step is to create an S3 bucket named "stephane-v3-events-notifications" in the Ireland region.  
첫 번째 단계는 아일랜드 리전에서 "stephane-v3-events-notifications"라는 이름의 S3 버킷을 생성하는 것입니다.  

Once the bucket is created, we proceed to configure event notifications for it.  
버킷을 생성한 후에는 이벤트 알림을 구성합니다.  

---

## Configuring Event Notifications  
## 이벤트 알림 구성  

Navigate to the bucket's properties and scroll down to the "Event notifications" section.  
버킷 속성으로 이동하여 "Event notifications" 섹션으로 스크롤합니다.  

Here, there are two options:  
여기에는 두 가지 옵션이 있습니다:  

1. Create an event notification.  
1. 이벤트 알림 생성  
2. Enable Amazon EventBridge integration to send all events from this S3 bucket to EventBridge.  
2. Amazon EventBridge 통합을 활성화하여 이 S3 버킷의 모든 이벤트를 EventBridge로 전송  

Enabling EventBridge integration allows capturing events from S3 buckets via EventBridge.  
EventBridge 통합을 활성화하면 S3 버킷의 이벤트를 EventBridge를 통해 캡처할 수 있습니다.  

However, for simplicity, we will focus on creating an event notification that sends events to an SQS queue.  
하지만 단순화를 위해 이번 실습에서는 이벤트를 SQS 큐로 전송하는 이벤트 알림 생성에 집중합니다.  

---

## Creating an Event Notification  
## 이벤트 알림 생성  

We create an event notification named "DemoEventNotification".  
"DemoEventNotification"이라는 이름의 이벤트 알림을 생성합니다.  

Although it is possible to set prefixes or suffixes to filter events, we will not use them here.  
이벤트를 필터링하기 위해 접두사나 접미사를 설정할 수 있지만, 이번 실습에서는 사용하지 않습니다.  

Next, we select the event types to react to.  
다음으로, 반응할 이벤트 유형을 선택합니다.  

We choose all object create events, meaning any time an object is created, an event will be generated.  
모든 객체 생성 이벤트를 선택합니다. 즉, 객체가 생성될 때마다 이벤트가 발생합니다.  

More granular event types can be selected if desired, including object removals and restores.  
원하면 객체 삭제 및 복원 등 더 세부적인 이벤트 유형을 선택할 수 있습니다.  

For this demonstration, we keep it simple by selecting all object create events.  
이번 실습에서는 모든 객체 생성 이벤트만 선택하여 간단하게 진행합니다.  

---

## Choosing the Destination  
## 대상 선택  

The event notification needs a destination to publish to.  
이벤트 알림은 전송할 대상을 필요로 합니다.  

There are three options:  
세 가지 옵션이 있습니다:  

- Lambda functions  
- Lambda 함수  
- SNS topics  
- SNS 주제  
- SQS queues  
- SQS 큐  

We will choose an SQS queue.  
이번에는 SQS 큐를 선택합니다.  

However, before selecting the queue, we need to create one and authorize Amazon S3 to publish messages to it.  
하지만 큐를 선택하기 전에 먼저 큐를 생성하고 S3가 메시지를 전송할 수 있도록 권한을 부여해야 합니다.  

---

## Creating and Configuring the SQS Queue  
## SQS 큐 생성 및 구성  

We create an SQS queue named "DemoS3Notification".  
"DemoS3Notification"이라는 이름의 SQS 큐를 생성합니다.  

After creation, we must enhance the access policy of this queue to allow the S3 bucket to send messages to it.  
생성 후에는 S3 버킷이 메시지를 전송할 수 있도록 큐의 액세스 정책을 업데이트해야 합니다.  

Initially, if we try to save the event notification with the queue as the destination, an error occurs stating that the destination configuration cannot be validated because the SQS queue does not accept messages from the S3 bucket yet.  
처음에는 큐를 대상으로 이벤트 알림을 저장하면, 큐가 S3로부터 메시지를 받도록 설정되지 않아 오류가 발생합니다.  

---

## Updating the SQS Queue Access Policy  
## SQS 큐 액세스 정책 업데이트  

To resolve this, we edit the access policy of the SQS queue.  
이를 해결하기 위해 SQS 큐의 액세스 정책을 편집합니다.  

Using the Policy Generator, we create an SQS queue policy with the following parameters:  
Policy Generator를 사용하여 다음 매개변수로 SQS 큐 정책을 생성합니다:  

- Effect: Allow  
- 효과: 허용  
- Principal: * (anyone, for permissiveness)  
- 주체: * (누구나, 허용 목적)  
- Action: SendMessage  
- 작업: SendMessage  
- Resource: The Amazon Resource Name (ARN) of the SQS queue  
- 리소스: SQS 큐의 Amazon Resource Name (ARN)  

This policy allows anyone to send messages to the queue, which is very permissive but sufficient for this demonstration.  
이 정책은 누구나 큐로 메시지를 전송할 수 있도록 허용하며, 매우 관대하지만 이번 실습에는 충분합니다.  

We save the updated policy.  
업데이트한 정책을 저장합니다.  

---

## Finalizing Event Notification Setup  
## 이벤트 알림 설정 완료  

After updating the access policy, we return to the S3 bucket event notification configuration and save the changes.  
액세스 정책을 업데이트한 후, S3 버킷 이벤트 알림 설정으로 돌아가 변경 사항을 저장합니다.  

The operation completes successfully.  
작업이 성공적으로 완료됩니다.  

To verify connectivity, we go to the SQS queue, click on "Send and receive messages," and then "Poll for messages."  
연결을 확인하기 위해 SQS 큐로 이동하여 "Send and receive messages"를 클릭한 후 "Poll for messages"를 선택합니다.  

A test message sent by Amazon S3 confirms the connection.  
S3가 전송한 테스트 메시지가 연결을 확인합니다.  

---

## Testing S3 Event Notifications  
## S3 이벤트 알림 테스트  

To test the event notification, we upload an object to the S3 bucket.  
이벤트 알림을 테스트하기 위해 S3 버킷에 객체를 업로드합니다.  

For example, we add a file named "coffee.jpeg".  
예를 들어 "coffee.jpeg"라는 파일을 추가합니다.  

Once uploaded, the file appears in the bucket.  
업로드가 완료되면 파일이 버킷에 나타납니다.  

This upload should trigger an event notification sent to the SQS queue.  
이 업로드는 SQS 큐로 전송되는 이벤트 알림을 트리거합니다.  

Polling the SQS queue for messages reveals a new message corresponding to the object creation event.  
SQS 큐를 폴링하면 객체 생성 이벤트에 해당하는 새 메시지가 표시됩니다.  

Inspecting the message shows the event name "ObjectCreatedPut" and confirms the key as "coffee.jpeg".  
메시지를 확인하면 이벤트 이름이 "ObjectCreatedPut"이고, 키가 "coffee.jpeg"임을 확인할 수 있습니다.  

This demonstrates that the event notification system is working as intended.  
이는 이벤트 알림 시스템이 의도대로 작동하고 있음을 보여줍니다.  

---

## Summary  
## 요약  

S3 Event Notifications can be configured to send events to SQS queues, SNS topics, Lambda functions, or Amazon EventBridge for further processing.  
S3 이벤트 알림은 SQS 큐, SNS 주제, Lambda 함수, Amazon EventBridge로 이벤트를 전송하도록 구성할 수 있습니다.  

Proper permissions must be set on the destination to allow S3 to publish messages.  
S3가 메시지를 전송할 수 있도록 대상에 적절한 권한을 설정해야 합니다.  

This setup enables automation workflows such as creating thumbnails upon object uploads.  
이 설정을 통해 객체 업로드 시 썸네일 생성과 같은 자동화 워크플로우를 구현할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created an S3 bucket and configured event notifications.  
- S3 버킷을 생성하고 이벤트 알림을 구성했습니다.  

- Demonstrated sending S3 event notifications to an SQS queue.  
- S3 이벤트 알림을 SQS 큐로 전송하는 과정을 시연했습니다.  

- Explained the need to update SQS queue access policy to allow S3 to send messages.  
- S3가 메시지를 전송할 수 있도록 SQS 큐 액세스 정책을 업데이트해야 함을 설명했습니다.  

- Showed how to verify event notifications by uploading an object and receiving messages in SQS.  
- 객체를 업로드하고 SQS에서 메시지를 수신하여 이벤트 알림을 확인하는 방법을 보여주었습니다.  

🎮 **게임보상:**

* **S3 Event Notifications 실습 완료!**

  * 버킷 생성 + 이벤트 알림 구성 +10
  * SQS 큐 연결 + 권한 설정 +15
  * 이벤트 테스트 및 확인 +10
    총 **35 XP 획득!** 🎉
