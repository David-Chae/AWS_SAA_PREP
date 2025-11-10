# S3 Default Encryption  
# S3 기본 암호화  

---

## S3 Default Encryption Overview  
## S3 기본 암호화 개요  

This lecture covers the topic of default encryption in Amazon S3 buckets and how it compares to bucket policies for enforcing encryption.  
이번 강의에서는 Amazon S3 버킷의 기본 암호화(default encryption)와 암호화 강제를 위한 버킷 정책(bucket policy)과의 비교를 다룹니다.  

By default, all S3 buckets have server-side encryption with Amazon S3-managed keys (SSE-S3) enabled. This default encryption is automatically applied to new objects uploaded to these buckets.  
기본적으로 모든 S3 버킷에는 Amazon S3 관리 키(SSE-S3)를 사용한 서버 측 암호화가 활성화되어 있습니다. 새로 업로드되는 객체에는 자동으로 이 기본 암호화가 적용됩니다.  

You can change the default encryption setting to use a different encryption method, such as server-side encryption with AWS Key Management Service keys (SSE-KMS).  
기본 암호화 설정은 AWS Key Management Service 키(SSE-KMS)를 사용한 서버 측 암호화와 같은 다른 암호화 방식으로 변경할 수 있습니다.  

---

## Enforcing Encryption with Bucket Policies  
## 버킷 정책을 통한 암호화 강제 적용  

In addition to default encryption, you can enforce encryption by using bucket policies. These policies can refuse any API call that attempts to put an S3 object without the correct encryption headers.  
기본 암호화 외에도 버킷 정책을 사용하여 암호화를 강제로 적용할 수 있습니다. 이러한 정책은 올바른 암호화 헤더 없이 S3 객체를 업로드하려는 API 호출을 거부할 수 있습니다.  

For example, a bucket policy can deny any PUT object request that does not include the encryption header specifying AWS KMS (SSE-KMS). Similarly, it can deny uploads that do not use customer-provided encryption keys (SSE-C).  
예를 들어, 버킷 정책은 AWS KMS(SSE-KMS)를 지정하는 암호화 헤더가 없는 PUT 객체 요청을 거부할 수 있습니다. 마찬가지로 고객 제공 키(SSE-C)를 사용하지 않은 업로드도 거부할 수 있습니다.  

Here is an example scenario:  
예제 시나리오는 다음과 같습니다:  

- If a PUT object request does not have the encryption header for AWS KMS, the request is denied.  
- PUT 객체 요청에 AWS KMS 암호화 헤더가 없으면 요청이 거부됩니다.  

- If an upload does not specify a customer-side encryption algorithm (SSE-C), the request is denied.  
- 업로드 시 고객 제공 암호화 알고리즘(SSE-C)을 지정하지 않으면 요청이 거부됩니다.  

This demonstrates how bucket policies can be used to enforce encryption requirements on your buckets.  
이 예제는 버킷 정책을 사용하여 버킷의 암호화 요구사항을 강제할 수 있음을 보여줍니다.  

It is important to note that bucket policies are always evaluated before the default encryption settings. This means bucket policies can preemptively enforce encryption standards regardless of the default encryption configuration.  
버킷 정책은 항상 기본 암호화 설정보다 먼저 평가된다는 점이 중요합니다. 이는 버킷 정책이 기본 암호화 설정과 상관없이 암호화 기준을 사전에 강제할 수 있음을 의미합니다.  

---

## Summary  
## 요약  

In summary, default encryption with SSE-S3 is enabled by default on all buckets, but you can change it to other encryption methods like SSE-KMS. Additionally, bucket policies provide a way to enforce encryption by denying requests that do not meet your encryption requirements.  
요약하면, 모든 버킷에는 기본적으로 SSE-S3 암호화가 활성화되어 있지만, 이를 SSE-KMS와 같은 다른 암호화 방식으로 변경할 수 있습니다. 또한 버킷 정책을 통해 암호화 요구사항을 충족하지 않는 요청을 거부하여 암호화를 강제할 수 있습니다.  

This concludes the lecture on S3 default encryption and bucket policies. Thank you for your attention, and I look forward to seeing you in the next lecture.  
이로써 S3 기본 암호화 및 버킷 정책 강의가 마무리되었습니다. 경청해주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- By default, all S3 buckets have SSE-S3 default encryption applied automatically to new objects.  
- 기본적으로 모든 S3 버킷에는 SSE-S3 기본 암호화가 새 객체에 자동으로 적용됩니다.  

- Default encryption can be changed to other types, such as SSE-KMS.  
- 기본 암호화는 SSE-KMS와 같은 다른 암호화 방식으로 변경할 수 있습니다.  

- Bucket policies can be used to enforce encryption by denying API calls that do not include the correct encryption headers.  
- 버킷 정책을 사용하면 올바른 암호화 헤더가 없는 API 호출을 거부하여 암호화를 강제할 수 있습니다.  

- Bucket policies are evaluated before default encryption settings, allowing preemptive enforcement of encryption standards.  
- 버킷 정책은 기본 암호화 설정보다 먼저 평가되므로 암호화 기준을 사전에 강제할 수 있습니다.  

🎮 **게임보상:**

* S3 기본 암호화 이해 및 설정 학습 +5 XP
* 버킷 정책을 통한 암호화 강제 적용 이해 +5 XP
* SSE-S3와 SSE-KMS 차이 이해 +5 XP
* 정책 우선 적용 순서 개념 이해 +5 XP
  총 **20 XP 획득!** 🎉
