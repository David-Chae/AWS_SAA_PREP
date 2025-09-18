```markdown
# S3 Replication with Encryption  
# S3 암호화 복제  

🎮 게임보상: "S3 복제 마스터" 업적 달성 +500 XP  

---

## S3 Replication and Encrypted Objects  
## S3 복제와 암호화된 객체  

Let's discuss S3 Replication and its relation to encrypted objects.  
S3 복제와 암호화된 객체와의 관계에 대해 알아봅시다.  

If you enable S3 Replication from one bucket to another, any unencrypted objects and objects encrypted with SSE-S3 will be replicated by default.  
한 버킷에서 다른 버킷으로 S3 복제를 활성화하면, 암호화되지 않은 객체와 SSE-S3로 암호화된 객체는 기본적으로 복제됩니다.  

Objects encrypted with SSE-C, which uses a customer-provided key, can also be replicated.  
고객이 제공한 키를 사용하는 SSE-C로 암호화된 객체도 복제할 수 있습니다.  

For objects encrypted with SSE-KMS, replication is not enabled by default.  
SSE-KMS로 암호화된 객체는 기본적으로 복제가 활성화되지 않습니다.  

You need to enable the option to replicate these objects.  
이 객체를 복제하려면 해당 옵션을 활성화해야 합니다.  

You specify which KMS Key you want to use to encrypt the objects within the target buckets.  
대상 버킷에서 객체를 암호화할 KMS 키를 지정해야 합니다.  

Then, you adapt the KMS Key Policy for the target key.  
그 후, 대상 키에 맞게 KMS 키 정책을 조정합니다.  

An IAM Role is created that allows the S3 Replication service to first decrypt the data in the source bucket and then re-encrypt the data in the target bucket with the target KMS Key.  
S3 복제 서비스가 소스 버킷의 데이터를 먼저 복호화하고 대상 버킷에서 대상 KMS 키로 다시 암호화할 수 있도록 IAM 역할이 생성됩니다.  

Enabling this replication involves a lot of encryption and decryption operations.  
이 복제를 활성화하면 많은 암호화 및 복호화 작업이 수행됩니다.  

As a result, you may encounter KMS throttling errors, in which case you need to request service quota increases.  
그 결과 KMS 제한(스로틀링) 오류가 발생할 수 있으며, 이 경우 서비스 할당량 증가를 요청해야 합니다.  

---

## Should You Use Multi-Region Keys with S3 Replication?  
## S3 복제에 다중 리전 키를 사용해야 할까?  

The documentation states that you can use multi-region keys for S3 Replication.  
문서에서는 S3 복제에 다중 리전 키를 사용할 수 있다고 명시하고 있습니다.  

However, currently, these keys are treated as independent keys by the Amazon S3 service.  
그러나 현재 Amazon S3 서비스에서는 이러한 키를 독립된 키로 처리합니다.  

Therefore, the object is still decrypted and then encrypted using the same key, even though the key is a multi-region key.  
따라서, 키가 다중 리전 키라도 객체는 여전히 복호화된 후 동일한 키로 다시 암호화됩니다.  

This concludes the lecture on S3 Replication with encryption.  
이로써 S3 암호화 복제 강의를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Replication replicates unencrypted objects and those encrypted with SSE-S3 by default.  
  S3 복제는 기본적으로 암호화되지 않은 객체와 SSE-S3로 암호화된 객체를 복제합니다.  

- Objects encrypted with SSE-C can also be replicated.  
  SSE-C로 암호화된 객체도 복제할 수 있습니다.  

- Objects encrypted with SSE-KMS require enabling replication and specifying the target KMS Key.  
  SSE-KMS로 암호화된 객체는 복제를 활성화하고 대상 KMS 키를 지정해야 합니다.  

- An IAM Role must allow S3 Replication to decrypt source data and re-encrypt it in the target bucket.  
  IAM 역할은 S3 복제가 소스 데이터를 복호화하고 대상 버킷에서 다시 암호화할 수 있도록 허용해야 합니다.  

- KMS throttling errors may occur due to encryption and decryption operations, requiring service quota increases.  
  암호화 및 복호화 작업으로 인해 KMS 제한 오류가 발생할 수 있으며, 서비스 할당량 증가가 필요할 수 있습니다.  

- Multi-region keys are treated as independent keys in S3 Replication, so objects are decrypted and re-encrypted even with multi-region keys.  
  S3 복제에서는 다중 리전 키도 독립 키로 처리되므로, 객체는 다중 리전 키를 사용해도 복호화 후 다시 암호화됩니다.  

🎮 게임보상: "S3 복제 암호화 전문가" +600 XP 🔑  
```
