# SQS - Message Visibility Timeout  
# SQS - 메시지 가시성 타임아웃  

---

## Message Visibility Timeout in SQS  
## SQS의 메시지 가시성 타임아웃  

Let's discuss an important concept called the message visibility timeout.  
메시지 가시성 타임아웃이라는 중요한 개념을 살펴보겠습니다.  

When a message is polled by a consumer, it becomes invisible to other consumers.  
메시지가 소비자(consumer)에 의해 폴링되면 다른 소비자에게는 보이지 않게 됩니다.  

Consider a timeline moving from left to right. A consumer performs a ReceiveMessage request, and a message is returned from the queue. At this point, the visibility timeout begins.  
왼쪽에서 오른쪽으로 진행하는 타임라인을 생각해봅시다. 소비자가 `ReceiveMessage` 요청을 수행하면 큐에서 메시지가 반환됩니다. 이 시점부터 가시성 타임아웃이 시작됩니다.  

By default, the message visibility timeout is 30 seconds. This means that during these 30 seconds, the message must be processed.  
기본적으로 메시지 가시성 타임아웃은 30초입니다. 즉, 이 30초 동안 메시지가 처리되어야 합니다.  

If the same or other consumers make a message request API call during this timeout window, the message will not be returned. Effectively, during the visibility timeout, the message is invisible to other consumers.  
동일하거나 다른 소비자가 이 타임아웃 기간 동안 메시지 요청 API를 호출하더라도 메시지는 반환되지 않습니다. 즉, 가시성 타임아웃 동안 메시지는 다른 소비자에게 보이지 않게 됩니다.  

After the visibility timeout elapses, if the message has not been deleted, it is "put back" into the queue. Therefore, another consumer or the same consumer making a `ReceiveMessage` API call will receive the same message again.  
가시성 타임아웃이 끝난 후에도 메시지가 삭제되지 않았다면, 해당 메시지는 다시 큐에 "되돌아갑니다". 따라서 다른 소비자나 같은 소비자가 `ReceiveMessage` API를 호출하면 동일한 메시지를 다시 받게 됩니다.  

This is an important concept to understand: while a message is received, it becomes invisible during the visibility timeout period.  
이것은 중요한 개념입니다: 메시지가 수신되면 가시성 타임아웃 기간 동안 보이지 않게 된다는 것입니다.  

If a message is not processed within the visibility timeout window, it may be processed twice. This could happen either by two different consumers or twice by the same consumer.  
메시지가 가시성 타임아웃 기간 내에 처리되지 않으면 두 번 처리될 수 있습니다. 이는 서로 다른 두 소비자가 처리하거나, 같은 소비자가 두 번 처리할 수도 있습니다.  

If a consumer is actively processing a message but knows it needs more time beyond the visibility timeout, there is an API called `ChangeMessageVisibility`.  
소비자가 메시지를 처리 중인데 가시성 타임아웃을 초과하여 더 많은 시간이 필요하다면 `ChangeMessageVisibility`라는 API를 사용할 수 있습니다.  

The consumer should call the `ChangeMessageVisibility` API to inform SQS not to make the message visible yet, effectively extending the visibility timeout.  
소비자는 `ChangeMessageVisibility` API를 호출하여 SQS에 메시지를 아직 표시하지 말라고 알려야 하며, 이를 통해 가시성 타임아웃을 연장할 수 있습니다.  

---

## Setting the Message Visibility Timeout  
## 메시지 가시성 타임아웃 설정  

If you set the visibility timeout to a very high value, such as hours, and the consumer crashes, it will take hours before the message reappears in the queue.  
가시성 타임아웃을 몇 시간과 같은 매우 큰 값으로 설정하면, 소비자가 다운될 경우 메시지가 큐에 다시 나타나기까지 몇 시간이 걸리게 됩니다.  

Conversely, if you set it to a very low value, like a few seconds, and the consumer does not have enough time to process the message, the message will be read multiple times by different consumers, causing duplicate processing.  
반대로 몇 초와 같이 매우 작은 값으로 설정하면, 소비자가 메시지를 처리할 충분한 시간이 없으므로 여러 소비자가 메시지를 반복해서 읽게 되어 중복 처리가 발생할 수 있습니다.  

Therefore, the visibility timeout should be set to a reasonable value for your application. Consumers should be programmed to call the `ChangeMessageVisibility` API if they need more time to process a message.  
따라서 가시성 타임아웃은 애플리케이션에 적합한 합리적인 값으로 설정해야 합니다. 또한 소비자가 메시지를 처리하는 데 더 많은 시간이 필요하다면 `ChangeMessageVisibility` API를 호출하도록 설계해야 합니다.  

Understanding this concept is important from an exam perspective because scenarios involving message visibility timeout are common.  
이 개념을 이해하는 것은 시험 관점에서도 중요합니다. 메시지 가시성 타임아웃과 관련된 시나리오는 자주 등장하기 때문입니다.  

---

## Demonstration in the Console  
## 콘솔에서의 시연  

Let's see how this works in practice by opening two windows: one for sending messages and one for receiving messages.  
실제 동작 방식을 보기 위해 두 개의 창을 엽니다: 하나는 메시지 전송용이고 다른 하나는 메시지 수신용입니다.  

In the first window, we send a "hello world" message into the queue. The queue has a default visibility timeout of 30 seconds.  
첫 번째 창에서 "hello world" 메시지를 큐에 전송합니다. 큐의 기본 가시성 타임아웃은 30초입니다.  

We have two consumers: the first and the second window. Polling messages from the first window returns the message.  
두 명의 소비자가 있습니다: 첫 번째 창과 두 번째 창입니다. 첫 번째 창에서 메시지를 폴링하면 메시지가 반환됩니다.  

Polling messages from the second window does not return the message because it is still within the visibility timeout window.  
두 번째 창에서 메시지를 폴링하면, 여전히 가시성 타임아웃 기간 내이므로 메시지가 반환되지 않습니다.  

If we stop polling and do not delete the message, after the visibility timeout expires, the message becomes visible again and is received by the second consumer.  
폴링을 멈추고 메시지를 삭제하지 않으면, 가시성 타임아웃이 만료된 후 메시지가 다시 보이게 되어 두 번째 소비자가 이를 받게 됩니다.  

If we delete the message after processing, it is fully processed. Note that the message was received twice, as indicated by the receive count of two.  
처리 후 메시지를 삭제하면 완전히 처리된 것입니다. 메시지 수신 횟수가 2로 표시된 것처럼, 메시지는 두 번 수신된 것을 알 수 있습니다.  

This demonstration shows how the visibility timeout works in practice.  
이 시연은 가시성 타임아웃이 실제로 어떻게 작동하는지 보여줍니다.  

---

## Changing the Visibility Timeout Setting  
## 가시성 타임아웃 설정 변경  

You can change the default visibility timeout by editing the queue settings. The value can be set between zero seconds (not recommended) and up to 12 hours.  
큐 설정을 편집하여 기본 가시성 타임아웃을 변경할 수 있습니다. 값은 0초(비추천)부터 최대 12시간까지 설정할 수 있습니다.  

While 30 seconds is a reasonable default, remember that if a consumer needs more time, it should call the `ChangeMessageVisibility` API to extend the visibility timeout for that message.  
30초는 합리적인 기본값이지만, 소비자가 더 많은 시간이 필요하다면 `ChangeMessageVisibility` API를 호출하여 해당 메시지의 가시성 타임아웃을 연장해야 합니다.  

This prevents other consumers from seeing the message and allows the first consumer enough time to process it accordingly.  
이렇게 하면 다른 소비자가 메시지를 보는 것을 방지하고, 첫 번째 소비자가 충분한 시간을 갖고 메시지를 처리할 수 있습니다.  

That concludes this lecture on message visibility timeout. Thank you for your attention.  
이것으로 메시지 가시성 타임아웃 강의를 마치겠습니다. 경청해 주셔서 감사합니다.  

---

## Key Takeaways  
## 핵심 요약  

- The message visibility timeout makes a message invisible to other consumers for a default period of 30 seconds after being received.  
  - 메시지 가시성 타임아웃은 메시지가 수신된 후 기본적으로 30초 동안 다른 소비자에게 보이지 않게 합니다.  
- If a message is not deleted within the visibility timeout, it becomes visible again and may be processed multiple times.  
  - 메시지가 가시성 타임아웃 내에 삭제되지 않으면 다시 보이게 되어 여러 번 처리될 수 있습니다.  
- The `ChangeMessageVisibility` API allows extending the visibility timeout if more processing time is needed.  
  - `ChangeMessageVisibility` API를 사용하면 메시지 처리에 더 많은 시간이 필요할 때 가시성 타임아웃을 연장할 수 있습니다.  
- Setting the visibility timeout too high or too low can cause delays or duplicate processing, so it should be set reasonably based on application needs.  
  - 가시성 타임아웃을 너무 크게 또는 너무 작게 설정하면 지연이나 중복 처리가 발생할 수 있으므로, 애플리케이션 필요에 따라 합리적으로 설정해야 합니다.  
