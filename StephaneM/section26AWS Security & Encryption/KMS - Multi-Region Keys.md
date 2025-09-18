```markdown
# KMS - Multi-Region Keys  
# KMS - 다중 리전 키  
🎮 게임보상: "KMS 다중 리전 마스터" 업적 달성 +500 XP  

---

## Introduction to KMS Multi-Region Keys  
## KMS 다중 리전 키 소개  

Let's discuss KMS Multi-Region keys. KMS allows you to have a Multi-Region key, meaning you have a primary key in one selected Region, for example, us-east-1.  
KMS 다중 리전 키에 대해 알아봅시다. KMS는 다중 리전 키를 지원하며, 예를 들어 us-east-1 같은 선택된 리전에 기본 키를 두는 것을 의미합니다.  

This key is then replicated to other Regions such as us-west-2, eu-west-1, and ap-southeast-2. The key material is replicated, so the same key exists in multiple Regions with the exact same key ID.  
이 키는 us-west-2, eu-west-1, ap-southeast-2 등 다른 리전으로 복제됩니다. 키 자료가 복제되므로 동일한 키 ID를 가진 동일한 키가 여러 리전에 존재합니다.  

You can observe that the key ID, including the suffix "mrk" and other identifiers, remains consistent across all Regions.  
"mrk" 접미사와 기타 식별자를 포함한 키 ID가 모든 리전에서 일관되게 유지됨을 확인할 수 있습니다.  

This is the fundamental principle behind KMS Multi-Region keys.  
이것이 KMS 다중 리전 키의 기본 원리입니다.  

---

## Use Cases for Multi-Region Keys  
## 다중 리전 키의 사용 사례  

What are the use cases for Multi-Region keys? They are a set of KMS keys usable in different AWS Regions interchangeably.  
다중 리전 키의 사용 사례는 무엇일까요? 이는 서로 다른 AWS 리전에서 상호 교환하여 사용할 수 있는 KMS 키 집합입니다.  

This means you can encrypt data in one Region and decrypt it in another.  
즉, 한 리전에서 데이터를 암호화하고 다른 리전에서 복호화할 수 있습니다.  

This capability is possible because the keys share the same key ID and key material.  
이 기능은 키가 동일한 키 ID와 키 자료를 공유하기 때문에 가능합니다.  

If automatic rotation is enabled for the primary key, the rotation is also replicated to the other Regions.  
기본 키에 자동 회전이 설정되어 있으면, 이 회전은 다른 리전에도 복제됩니다.  

The main advantage is that you can encrypt in one Region and decrypt in another without needing to re-encrypt your data when moving between Regions or making cross-Region API calls.  
주요 장점은 리전 간 이동이나 크로스 리전 API 호출 시 데이터를 다시 암호화할 필요 없이 한 리전에서 암호화하고 다른 리전에서 복호화할 수 있다는 점입니다.  

---

## Important Considerations  
## 중요한 고려 사항  

It is important to understand that KMS Multi-Region keys are not global keys.  
KMS 다중 리전 키는 글로벌 키가 아니라는 점을 이해하는 것이 중요합니다.  

You have a primary key and replicas, each managed independently with its own key policy.  
기본 키와 복제본이 있으며, 각각 독립적으로 자체 키 정책으로 관리됩니다.  

Therefore, it is generally not recommended to use Multi-Region keys except in very specific use cases because KMS prefers keys to be bound to a single Region.  
따라서, KMS는 키를 단일 리전에 바인딩하는 것을 선호하므로, 매우 특정한 경우를 제외하고 다중 리전 키 사용은 권장되지 않습니다.  

---

## Specific Use Cases for Multi-Region Keys  
## 다중 리전 키의 특정 사용 사례  

The primary use cases for Multi-Region keys include:  
다중 리전 키의 주요 사용 사례는 다음과 같습니다:  

- Global client-side encryption, allowing encryption in one Region and decryption in another.  
  글로벌 클라이언트 측 암호화: 한 리전에서 암호화하고 다른 리전에서 복호화 가능  

- Encryption for Global DynamoDB tables.  
  글로벌 DynamoDB 테이블 암호화  

- Encryption for Global Aurora databases.  
  글로벌 Aurora 데이터베이스 암호화  

Let's explore these use cases in detail.  
이제 이러한 사용 사례를 자세히 살펴봅시다.  

---

## Client-Side Encryption with DynamoDB Global Tables  
## DynamoDB 글로벌 테이블에서 클라이언트 측 암호화  

Consider an example with Regions us-east-1 and ap-southeast-2. The KMS service holds a Multi-Region key replicated to ap-southeast-2.  
예를 들어 us-east-1과 ap-southeast-2 리전을 생각해봅시다. KMS 서비스는 ap-southeast-2로 복제된 다중 리전 키를 보유합니다.  

A client application wants to insert data into a DynamoDB table. It encrypts specific attributes, such as a Social Security number, using the primary Multi-Region key.  
클라이언트 애플리케이션이 DynamoDB 테이블에 데이터를 삽입하려고 합니다. 이때 주민등록번호와 같은 민감 속성을 기본 다중 리전 키로 암호화합니다.  

Most fields in the DynamoDB table remain unencrypted, but sensitive attributes are encrypted client-side.  
DynamoDB 테이블의 대부분 필드는 암호화되지 않지만, 민감 속성은 클라이언트 측에서 암호화됩니다.  

This protects the data even from database administrators who have access to the table but not to the KMS key used for encryption.  
이렇게 하면 테이블에 접근할 수 있는 데이터베이스 관리자조차도 암호화 키 없이는 민감 데이터를 볼 수 없습니다.  

If the DynamoDB table is a Global Table, the data replicates to another Region, for example, ap-southeast-2.  
DynamoDB 테이블이 글로벌 테이블이면 데이터가 다른 리전(예: ap-southeast-2)으로 복제됩니다.  

Because the attribute was encrypted with a Multi-Region key, a client application in ap-southeast-2 can retrieve the encrypted attribute and perform a local API call to KMS to decrypt it using the replica Multi-Region key.  
속성이 다중 리전 키로 암호화되었기 때문에 ap-southeast-2의 클라이언트 애플리케이션은 암호화된 속성을 가져와 KMS에 로컬 API 호출을 통해 복제된 키로 복호화할 수 있습니다.  

This setup enables local decryption with lower latency.  
이 구성은 낮은 지연 시간으로 로컬 복호화를 가능하게 합니다.  

---

## Protecting Specific Attributes  
## 특정 속성 보호  

This client-side encryption technique allows protection of specific fields or attributes in your data.  
이 클라이언트 측 암호화 기술은 데이터의 특정 필드나 속성을 보호할 수 있습니다.  

Decryption is only possible when the client has access to the appropriate API key.  
복호화는 클라이언트가 적절한 API 키에 접근할 수 있을 때만 가능합니다.  

Thanks to Global Tables, both the data and the encryption keys are replicated together, ensuring seamless encryption and decryption across Regions.  
글로벌 테이블 덕분에 데이터와 암호화 키가 함께 복제되어, 리전 간 원활한 암호화 및 복호화가 가능합니다.  

---

## Client-Side Encryption with Global Aurora  
## 글로벌 Aurora에서 클라이언트 측 암호화  

Similarly, for Global Aurora databases, the AWS Encryption SDK can be used.  
마찬가지로 글로벌 Aurora 데이터베이스에서도 AWS Encryption SDK를 사용할 수 있습니다.  

Consider two Regions with a Multi-Region key replicated across them. A client application encrypts a sensitive column, such as an SSN, using the Multi-Region key before inserting data into an Amazon Aurora database table.  
두 개 리전에 다중 리전 키가 복제되어 있다고 가정합니다. 클라이언트 애플리케이션은 Amazon Aurora 데이터베이스 테이블에 데이터를 삽입하기 전에 주민등록번호 같은 민감 열을 다중 리전 키로 암호화합니다.  

All data in the row remains unencrypted except the sensitive column.  
행의 모든 데이터는 민감 열을 제외하고는 암호화되지 않습니다.  

Since the database is global, the data replicates to another Region, such as ap-southeast-2.  
데이터베이스가 글로벌이므로 데이터가 다른 리전(예: ap-southeast-2)으로 복제됩니다.  

Clients in that Region receive the encrypted data and can perform a local API call to KMS to decrypt the attribute using the replica Multi-Region key, achieving lower latency.  
해당 리전의 클라이언트는 암호화된 데이터를 받고, 복제된 다중 리전 키로 KMS 로컬 API 호출을 통해 속성을 복호화하여 낮은 지연 시간을 구현합니다.  

This approach also protects sensitive data from database administrators who do not have access to the KMS key.  
이 접근법은 KMS 키에 접근 권한이 없는 데이터베이스 관리자에게서도 민감 데이터를 보호합니다.  

---

## Conclusion  
## 결론  

In summary, KMS Multi-Region keys enable secure, low-latency encryption and decryption across multiple AWS Regions.  
요약하면, KMS 다중 리전 키는 여러 AWS 리전에서 안전하고 낮은 지연 시간의 암호화 및 복호화를 가능하게 합니다.  

They are particularly useful for client-side encryption scenarios in global applications using DynamoDB Global Tables and Global Aurora databases, providing protection even against privileged users like database administrators.  
특히 DynamoDB 글로벌 테이블과 글로벌 Aurora를 사용하는 글로벌 애플리케이션의 클라이언트 측 암호화 시나리오에서 유용하며, 데이터베이스 관리자 같은 권한 사용자로부터도 보호할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- KMS Multi-Region keys replicate key material and key ID across multiple AWS Regions, enabling encryption in one Region and decryption in another.  
  KMS 다중 리전 키는 키 자료와 키 ID를 여러 리전에 복제하여 한 리전에서 암호화하고 다른 리전에서 복호화할 수 있습니다.  

- Multi-Region keys are managed independently per Region with
```


separate key policies and are not global keys.
다중 리전 키는 각 리전별로 별도의 키 정책으로 독립 관리되며 글로벌 키가 아닙니다.

* Client-side encryption with Multi-Region keys allows selective attribute encryption in services like DynamoDB Global Tables and Global Aurora, protecting data even from database administrators.
  다중 리전 키를 사용한 클라이언트 측 암호화는 DynamoDB 글로벌 테이블과 글로벌 Aurora에서 특정 속성만 선택적으로 암호화할 수 있어 데이터베이스 관리자로부터도 보호합니다.

* Using Multi-Region keys reduces latency by enabling local API calls for decryption in replicated Regions.
  다중 리전 키 사용은 복제된 리전에서 로컬 API 호출로 복호화할 수 있어 지연 시간을 줄입니다.

🎮 게임보상: "KMS 다중 리전 키 마스터" +700 XP 🔑

```
