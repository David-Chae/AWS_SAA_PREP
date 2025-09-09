# SNS - Hands On  
# SNS - 실습  

---

## Introduction to SNS  
## SNS 소개  

In this session, we will practice using the Simple Notification Service (SNS).  
이번 세션에서는 Simple Notification Service(SNS)를 실습해보겠습니다.  

We will start by creating our first SNS topic.  
먼저 첫 번째 SNS 주제를 만들어보겠습니다.  

---

## Creating a Standard SNS Topic  
## 표준 SNS 주제 생성  

We will create a topic named MyFirstTopic.  
"MyFirstTopic"이라는 이름의 주제를 생성할 것입니다.  

There are two options for creating a topic:  
주제를 생성할 때 두 가지 옵션이 있습니다:  

- **Standard Topic**: Offers best-effort message ordering, at least once message delivery, and the highest throughput in terms of publishes per second. It supports subscriptions from SQS, Lambda, HTTPS, SMS, email, and mobile application endpoints.  
- **표준 주제(Standard Topic)**: 메시지 순서를 최선을 다해 보장하며, 최소 한 번 메시지 전달(at least once), 초당 최대 발행량을 제공합니다. SQS, Lambda, HTTPS, SMS, 이메일, 모바일 앱 엔드포인트 구독을 지원합니다.  

- **FIFO Topic**: Provides strictly preserved message ordering, exactly once message delivery, and high throughput up to 300 publishes per second. Only SQS queues can subscribe to FIFO SNS topics. The topic name must end with .fifo when creating a FIFO topic.  
- **FIFO 주제(FIFO Topic)**: 메시지 순서를 엄격히 보장하며, 정확히 한 번 메시지 전달(exactly once), 초당 최대 300 발행량을 제공합니다. SQS 큐만 FIFO SNS 주제를 구독할 수 있으며, 주제 이름은 `.fifo`로 끝나야 합니다.  

For this exercise, we will create a standard topic named MyFirstTopic.  
이번 실습에서는 "MyFirstTopic"이라는 표준 주제를 생성합니다.  

---

## Topic Configuration Options  
## 주제 구성 옵션  

We have the option to encrypt messages in our topic and set up an access policy.  
주제의 메시지를 암호화하거나 접근 정책을 설정할 수 있습니다.  

The access policy defines who and what can write to the SNS topic.  
접근 정책은 누가 무엇을 SNS 주제에 작성할 수 있는지 정의합니다.  

This is similar to an S3 bucket policy or an SQS access queue policy.  
이는 S3 버킷 정책이나 SQS 큐 접근 정책과 유사합니다.  

For example, an S3 bucket can be configured to write events into an SNS topic, which then can send data to SQS or other endpoints.  
예를 들어, S3 버킷을 구성하여 이벤트를 SNS 주제로 전송하면, SNS가 데이터를 SQS 또는 다른 엔드포인트로 전송할 수 있습니다.  

The access policy is necessary to allow such interactions.  
이러한 상호작용을 허용하려면 접근 정책이 필요합니다.  

For now, we will use the basic settings without encryption or custom access policies and proceed to create the topic.  
현재는 암호화나 커스텀 접근 정책 없이 기본 설정으로 주제를 생성합니다.  

---

## Topic Creation and Subscription Setup  
## 주제 생성 및 구독 설정  

After creating MyFirstTopic, we observe that it currently has zero subscriptions.  
"MyFirstTopic" 생성 후 현재 구독이 없는 것을 확인합니다.  

We will create our first subscription by choosing a protocol.  
첫 구독을 생성하려면 프로토콜을 선택합니다.  

Available protocols include Kinesis Data Firehose, SQS, Lambda, Email, Email-JSON, HTTP, HTTPS, and SMS.  
사용 가능한 프로토콜에는 Kinesis Data Firehose, SQS, Lambda, 이메일, Email-JSON, HTTP, HTTPS, SMS가 있습니다.  

For simplicity, we will use the Email protocol for this hands-on exercise.  
이번 실습에서는 간단히 이메일 프로토콜을 사용합니다.  

---

## Configuring Email Subscription  
## 이메일 구독 설정  

We need to specify an endpoint email address.  
엔드포인트 이메일 주소를 지정해야 합니다.  

For this demonstration, we will use stephanetheteachermailinator.com, a service that provides temporary public email inboxes.  
이번 실습에서는 임시 공개 이메일을 제공하는 stephanetheteachermailinator.com을 사용합니다.  

By entering stephanetheteacher and accessing the inbox, we can receive emails sent to this address.  
stephanetheteacher를 입력하고 인박스를 확인하면, 해당 주소로 전송된 이메일을 받을 수 있습니다.  

This setup allows us to test SNS email notifications without using a personal email account.  
이를 통해 개인 이메일 계정을 사용하지 않고 SNS 이메일 알림을 테스트할 수 있습니다.  

---

## Subscription Filter Policy (Optional)  
## 구독 필터 정책(선택 사항)  

SNS allows setting up a subscription filter policy, which is optional.  
SNS는 선택 사항인 구독 필터 정책 설정을 허용합니다.  

This policy enables filtering messages sent to the subscription, which is useful when multiple subscribers only need subsets of the messages published to the SNS topic.  
이 정책은 구독으로 전송되는 메시지를 필터링할 수 있게 하며, 여러 구독자가 SNS 주제의 일부 메시지만 필요할 때 유용합니다.  

In this exercise, we will not configure a filter policy, so all messages sent to MyFirstTopic will be delivered to the subscription.  
이번 실습에서는 필터 정책을 구성하지 않으며, "MyFirstTopic"로 전송되는 모든 메시지가 구독으로 전달됩니다.  

---

## Confirming the Subscription  
## 구독 확인  

After creating the subscription, its status is "pending confirmation."  
구독 생성 후 상태는 "승인 대기(pending confirmation)"입니다.  

To confirm it, we check the Mailinator inbox for a confirmation email from SNS.  
승인하려면 Mailinator 인박스에서 SNS로부터 온 확인 이메일을 확인합니다.  

By clicking the confirmation link in the email, the subscription becomes confirmed.  
이메일 내 확인 링크를 클릭하면 구독이 승인됩니다.  

Once confirmed, the subscription status updates accordingly, indicating that SNS will send messages to the specified email endpoint.  
승인되면 구독 상태가 업데이트되어 SNS가 지정된 이메일로 메시지를 전송함을 나타냅니다.  

---

## Publishing a Test Message  
## 테스트 메시지 발행  

To verify that SNS is working correctly, we will publish a test message to MyFirstTopic.  
SNS가 올바르게 작동하는지 확인하기 위해 "MyFirstTopic"에 테스트 메시지를 발행합니다.  

We enter the message content "hello world," a common test phrase, and publish it.  
메시지 내용 "hello world"를 입력하고 발행합니다.  

After publishing, the message is sent to all confirmed subscriptions.  
발행 후 메시지는 승인된 모든 구독으로 전송됩니다.  

Checking the Mailinator inbox, we should see an AWS notification email from SNS containing the "hello world" message.  
Mailinator 인박스를 확인하면 SNS에서 전송된 "hello world" 메시지를 포함한 AWS 알림 이메일을 볼 수 있습니다.  

---

## Additional Notes on SNS  
## SNS 추가 참고 사항  

If we want to implement the SQS fanout pattern, we would choose SQS as the subscription protocol and set up multiple queues as receivers for the SNS topic.  
SQS 팬 아웃 패턴을 구현하려면 구독 프로토콜로 SQS를 선택하고, 여러 큐를 SNS 주제의 수신자로 설정합니다.  

This allows broadcasting messages to multiple queues simultaneously.  
이를 통해 메시지를 여러 큐에 동시에 브로드캐스트할 수 있습니다.  

When finished with the exercise, remember to delete the subscription and then delete the SNS topic by typing delete me to confirm the deletion.  
실습이 끝나면 구독을 삭제하고, SNS 주제를 삭제할 때 "delete me"를 입력하여 삭제를 확인합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created a standard SNS topic named MyFirstTopic with best-effort message ordering and at least once delivery.  
- MyFirstTopic이라는 이름의 표준 SNS 주제를 생성하고, 최선의 노력으로 메시지 순서를 보장하며 최소 한 번 전송을 수행했습니다.  

- Configured an email subscription using a temporary email service and confirmed the subscription.  
- 임시 이메일 서비스를 사용하여 이메일 구독을 구성하고 구독을 확인했습니다.  

- Published a test message "hello world" to verify SNS functionality.  
- SNS 기능을 확인하기 위해 테스트 메시지 "hello world"를 발행했습니다.  

- Explained the difference between standard and FIFO SNS topics and the SQS fanout pattern for multiple subscribers.  
- 표준 SNS 주제와 FIFO SNS 주제의 차이점, 그리고 여러 구독자를 위한 SQS 팬 아웃 패턴을 설명했습니다.  
