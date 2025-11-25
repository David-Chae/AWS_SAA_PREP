# SQS - Standard Queue Hands On  
# SQS - 스탠다드 큐 실습  

---

## Introduction to Amazon SQS  
## Amazon SQS 소개  

In this session, we will practice using Amazon Simple Queue Service (SQS). We begin by navigating to the SQS console to create a queue.  
이번 세션에서는 Amazon Simple Queue Service(SQS)를 실습해봅니다. 먼저 SQS 콘솔로 이동하여 큐를 생성하는 것부터 시작합니다.  

Amazon SQS provides two types of queues: the Standard queue and the FIFO queue. For this demonstration, we will use the Standard queue and name it "Demo Queue." We will explore FIFO queues in a later session.  
Amazon SQS는 두 가지 유형의 큐를 제공합니다: 스탠다드 큐와 FIFO 큐입니다. 이번 실습에서는 스탠다드 큐를 사용하여 "Demo Queue"라는 이름으로 생성합니다. FIFO 큐는 나중 세션에서 다룰 예정입니다.  

---

## Queue Configuration Options  
## 큐 구성 옵션  

We will review several configuration options, which will be covered in more detail in future lectures. These include:  
우리는 몇 가지 구성 옵션을 검토할 것이며, 이는 앞으로의 강의에서 더 자세히 다룰 예정입니다. 포함되는 항목은 다음과 같습니다:  

- Visibility timeout  
  - 가시성 타임아웃  
- Delivery delay  
  - 전달 지연  
- Wait time  
  - 대기 시간  
- Retention period (set to four days in this example)  
  - 보관 기간 (이 예제에서는 4일로 설정)  
- Maximum message size (set to 256 kilobytes, the maximum allowed in SQS)  
  - 최대 메시지 크기 (SQS에서 허용되는 최대값인 256KB로 설정)  

---

## Encryption Options  
## 암호화 옵션  

For encryption, there are several choices:  
암호화에는 몇 가지 선택지가 있습니다:  

- Encryption can be disabled entirely.  
  - 암호화를 완전히 비활성화할 수 있습니다.  
- By default, encryption is enabled using an Amazon SQS key, known as SSE-SQS encryption. This is similar to the SSE-S3 encryption used in Amazon S3.  
  - 기본적으로 SSE-SQS라고 불리는 Amazon SQS 키를 사용하여 암호화가 활성화됩니다. 이는 Amazon S3에서 사용되는 SSE-S3와 유사합니다.  
- Alternatively, you can use AWS Key Management Service (KMS) by selecting a customer master key (CMK). You may choose the default AWS CMK alias/AWS/SQS and define a data key reuse period, such as five minutes, to limit the number of API calls to KMS.  
  - 또는 AWS Key Management Service(KMS)를 사용하여 고객 마스터 키(CMK)를 선택할 수 있습니다. 기본 AWS CMK(alias/aws/sqs)를 선택하고 데이터 키 재사용 기간(예: 5분)을 정의하여 KMS API 호출 수를 줄일 수 있습니다.  

For this demonstration, we will keep the encryption set to the Amazon SQS key (SSE-SQS).  
이번 실습에서는 Amazon SQS 키(SSE-SQS)를 사용한 암호화를 유지하겠습니다.  

---

## Access Policy  
## 액세스 정책  

The access policy defines who can access the queue. Options include:  
액세스 정책은 누가 큐에 접근할 수 있는지를 정의합니다. 선택지는 다음과 같습니다:  

- Only the queue owner can send and receive messages.  
  - 큐 소유자만 메시지를 송수신할 수 있습니다.  
- Specifying a list of accounts, users, and roles who can send or receive messages.  
  - 메시지를 송수신할 수 있는 계정, 사용자, 역할 목록을 지정합니다.  

This configuration generates a JSON document similar to the Amazon S3 bucket policy, serving as a resource policy for SQS.  
이 구성은 Amazon S3 버킷 정책과 유사한 JSON 문서를 생성하며, SQS의 리소스 정책 역할을 합니다.  

---

## Redrive and Dead-Letter Queue  
## 재전송 정책 및 데드 레터 큐  

Redrive policies and dead-letter queues are advanced features that will be covered later. For now, we proceed without configuring these options.  
재전송 정책과 데드 레터 큐는 고급 기능으로, 나중에 다룰 예정입니다. 지금은 해당 옵션을 구성하지 않고 진행합니다.  

After configuring the queue, we create it successfully. We can now send and receive messages from this queue.  
큐 구성을 완료하면 성공적으로 생성됩니다. 이제 이 큐에서 메시지를 송수신할 수 있습니다.  

---

## Sending and Receiving Messages  
## 메시지 송수신  

In the SQS console, navigate to the top right-hand side and click on "Send and receive messages." This interface allows us to send messages to the queue and receive them at the bottom panel.  
SQS 콘솔에서 오른쪽 상단의 "메시지 송수신" 버튼을 클릭합니다. 이 인터페이스를 통해 큐에 메시지를 보내고 하단 패널에서 수신할 수 있습니다.  

Currently, the queue shows zero messages available. We enter "hello world!" in the message body and send the message. The message is sent successfully and is ready to be received, increasing the available messages count to one.  
현재 큐에는 메시지가 0개로 표시됩니다. 메시지 본문에 "hello world!"를 입력하고 전송하면 메시지가 성공적으로 발송되어 수신 준비 상태가 되며, 사용 가능한 메시지 수가 1로 증가합니다.  

Clicking "Pull for messages" retrieves the message. The message details include:  
"메시지 가져오기(Pull for messages)"를 클릭하면 메시지가 수신됩니다. 메시지 세부 정보에는 다음이 포함됩니다:  

- Message ID  
  - 메시지 ID  
- Metadata such as message hash, sender information  
  - 메시지 해시, 송신자 정보 등 메타데이터  
- Number of times the message has been received (currently one)  
  - 메시지가 수신된 횟수 (현재 1회)  
- Size in bytes  
  - 바이트 단위 크기  
- Message body content, which is "hello world!"  
  - 메시지 본문 내용: "hello world!"  

If message attributes were created, they would appear in the message attributes panel.  
메시지 속성이 생성되었다면, 메시지 속성 패널에 표시됩니다.  

This demonstrates the decoupling of producers and consumers: a producer sends information, and a consumer receives it independently.  
이는 생산자와 소비자가 분리되어 있다는 것을 보여줍니다: 생산자는 정보를 보내고 소비자는 독립적으로 수신합니다.  

The message has been received multiple times because it was not processed within the visibility timeout period. After 30 seconds, the message returned to the queue and was received again. The receive count increases accordingly.  
메시지가 가시성 타임아웃 기간 내에 처리되지 않았기 때문에 여러 번 수신되었습니다. 30초 후 메시지가 큐로 다시 돌아와 재수신되며, 수신 횟수가 증가합니다.  

To complete processing, select the message and delete it. Deleting the message signals to SQS that it has been successfully processed, reducing the available messages count to zero. Subsequent pulls will not retrieve the deleted message.  
처리를 완료하려면 메시지를 선택 후 삭제해야 합니다. 메시지를 삭제하면 SQS에 성공적으로 처리되었음을 알리고, 사용 가능한 메시지 수가 0으로 줄어듭니다. 이후 가져오기 작업에서는 삭제된 메시지가 나타나지 않습니다.  

---

## Working with Multiple Messages  
## 다중 메시지 처리  

You can send multiple messages, such as "hello world," "hello world 2," and "hello world 3." Refreshing the window shows the number of available messages increasing accordingly. Pulling messages retrieves all available messages, which can then be deleted after processing to signal completion.  
"hello world," "hello world 2," "hello world 3"과 같은 여러 메시지를 보낼 수 있습니다. 창을 새로고침하면 사용 가능한 메시지 수가 증가하며, 가져오기 작업을 통해 모든 메시지를 수신한 뒤 처리 후 삭제하여 완료를 알릴 수 있습니다.  

---

## Queue Management Options  
## 큐 관리 옵션  

Within the queue settings, you can:  
큐 설정 내에서 할 수 있는 작업은 다음과 같습니다:  

- Edit queue configurations  
  - 큐 구성 수정  
- Purge the queue, which deletes all messages (useful during development but not recommended in production)  
  - 큐 비우기: 모든 메시지를 삭제 (개발 환경에서는 유용하지만 운영 환경에서는 권장되지 않음)  
- Monitor queue metrics such as the number of messages and the approximate age of the oldest message, which can inform auto-scaling decisions  
  - 메시지 수 및 가장 오래된 메시지의 대략적인 연령과 같은 큐 지표 모니터링 (자동 확장 결정에 유용)  
- Manage access policies and encryption settings  
  - 액세스 정책 및 암호화 설정 관리  
- Configure dead-letter queues and redrive policies (covered in later sessions)  
  - 데드 레터 큐 및 재전송 정책 구성 (추후 세션에서 다룸)  

---

## Conclusion  
## 결론  

This concludes our hands-on session with Amazon SQS standard queues. Thank you for your attention, and we will continue exploring more features in upcoming lectures.  
이것으로 Amazon SQS 스탠다드 큐 실습 세션을 마칩니다. 경청해 주셔서 감사합니다. 앞으로 더 많은 기능을 다루는 강의가 이어질 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon SQS offers two types of queues: Standard and FIFO.  
  - Amazon SQS는 스탠다드 큐와 FIFO 큐 두 가지를 제공합니다.  
- Standard queues support features like visibility timeout, delivery delay, and server-side encryption using SSE-SQS or KMS.  
  - 스탠다드 큐는 가시성 타임아웃, 전달 지연, SSE-SQS 또는 KMS를 통한 서버 측 암호화를 지원합니다.  
- Messages can be sent, received, and deleted through the SQS console, demonstrating decoupled producer-consumer architecture.  
  - 메시지는 SQS 콘솔에서 송수신 및 삭제할 수 있으며, 생산자-소비자 분리 아키텍처를 보여줍니다.  
- Queue management includes editing configurations, purging messages, monitoring metrics, and setting access policies.  
  - 큐 관리는 구성 편집, 메시지 삭제, 지표 모니터링, 액세스 정책 설정 등을 포함합니다. 

