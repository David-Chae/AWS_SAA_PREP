# SQS - Long Polling  
# SQS - 롱 폴링  

## Introduction to Long Polling in Amazon SQS  
## Amazon SQS에서 롱 폴링 소개  

Let's discuss long polling in Amazon Simple Queue Service (SQS).  
Amazon 단순 큐 서비스(SQS)의 롱 폴링에 대해 이야기해봅시다.  

The concept involves your consumer, which requests messages from the queue, waiting for messages to arrive if none are immediately available.  
이 개념은 메시지를 요청하는 소비자가 큐에 즉시 메시지가 없을 경우, 메시지가 도착할 때까지 기다리는 것을 포함합니다.  

Your consumer polls the queue, but it can wait for a message to arrive.  
소비자는 큐를 폴링하지만, 메시지가 도착할 때까지 기다릴 수 있습니다.  

When a message arrives, it is sent immediately to the consumer.  
메시지가 도착하면 즉시 소비자에게 전달됩니다.  

---

## Benefits of Long Polling  
## 롱 폴링의 장점  

With long polling, your consumer reduces the number of API calls because these calls are long-lived.  
롱 폴링을 사용하면, 소비자가 API 호출 횟수를 줄일 수 있는데, 이는 호출이 오래 지속되기 때문입니다.  

For example, the consumer may ask the SQS queue for messages and wait up to 10 seconds if none are currently available.  
예를 들어, 소비자가 SQS 큐에 메시지를 요청하고, 현재 메시지가 없으면 최대 10초까지 기다릴 수 있습니다.  

While making fewer API calls, long polling also reduces the latency of your application.  
API 호출 수를 줄이는 동시에, 롱 폴링은 애플리케이션의 지연 시간도 줄여줍니다.  

This is because as soon as a message is received by SQS, it is sent to the consumer, minimizing lag.  
이는 메시지가 SQS에 도착하는 즉시 소비자에게 전달되기 때문에 지연이 최소화되기 때문입니다.  

---

## Configuring Long Polling  
## 롱 폴링 설정하기  

Long polling can be set anywhere between one second to 20 seconds.  
롱 폴링은 1초에서 20초 사이로 설정할 수 있습니다.  

The longer the wait time, the more efficient the process becomes, resulting in fewer API calls to SQS.  
대기 시간이 길수록 프로세스가 더 효율적이 되어, SQS에 대한 API 호출 수가 줄어듭니다.  

A wait time of 20 seconds is often preferable.  
대기 시간을 20초로 설정하는 것이 종종 더 바람직합니다.  

Overall, you should prefer long polling over short polling.  
전반적으로, 짧은 폴링보다 롱 폴링을 사용하는 것이 좋습니다.  

You can enable long polling either at the queue level or at the API level by using the WaitTimeSeconds parameter.  
롱 폴링은 큐 수준 또는 API 수준에서 **WaitTimeSeconds** 매개변수를 사용하여 활성화할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

Long polling in Amazon SQS allows consumers to wait for messages to arrive if none are currently available.  
Amazon SQS의 롱 폴링은 현재 메시지가 없을 경우, 메시지가 도착할 때까지 소비자가 기다릴 수 있도록 합니다.  

This approach reduces the number of API calls by allowing the consumer to wait up to 20 seconds for messages.  
이 접근 방식은 소비자가 메시지를 최대 20초 동안 기다리게 하여 API 호출 횟수를 줄여줍니다.  

Long polling decreases application latency by delivering messages to consumers as soon as they arrive.  
롱 폴링은 메시지가 도착하는 즉시 소비자에게 전달하므로 애플리케이션의 지연 시간을 줄입니다.  

It is recommended to prefer long polling over short polling and configure it either at the queue or API level using the WaitTimeSeconds parameter.  
짧은 폴링보다 롱 폴링을 사용하는 것이 권장되며, 큐 또는 API 수준에서 **WaitTimeSeconds** 매개변수를 사용해 설정할 수 있습니다.  
