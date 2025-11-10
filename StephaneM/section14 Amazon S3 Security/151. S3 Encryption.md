# S3 Encryption  
# S3 암호화  

---

## Overview of Object Encryption in Amazon S3  
## Amazon S3 객체 암호화 개요  

You can encrypt objects in S3 buckets using one of the following four methods:  
S3 버킷의 객체는 다음 네 가지 방법 중 하나를 사용하여 암호화할 수 있습니다.  

- Server-side encryption (SSE), which has multiple flavors:  
- 서버 측 암호화(SSE), 여러 종류가 있음:  
  - SSE-S3: Server-side encryption with Amazon S3-managed keys.  
  - SSE-S3: Amazon S3 관리 키를 사용한 서버 측 암호화  
  - SSE-KMS: Server-side encryption with AWS Key Management Service (KMS) keys.  
  - SSE-KMS: AWS KMS 키를 사용한 서버 측 암호화  
  - SSE-C: Server-side encryption with customer-provided keys.  
  - SSE-C: 고객 제공 키를 사용한 서버 측 암호화  

- Client-side encryption, where you encrypt everything client-side before uploading to Amazon S3.  
- 클라이언트 측 암호화: S3에 업로드하기 전에 모든 데이터를 클라이언트 측에서 암호화  

It is important to understand which encryption method is suitable for each situation.  
각 상황에 적합한 암호화 방식을 이해하는 것이 중요합니다.  

---

## SSE-S3: Server-Side Encryption with S3-Managed Keys  
## SSE-S3: S3 관리 키를 사용한 서버 측 암호화  

With SSE-S3, the encryption uses a key that is handled, managed, and owned by AWS.  
SSE-S3에서는 암호화에 AWS가 관리하고 소유하는 키를 사용합니다.  

You never have access to this key.  
사용자는 이 키에 접근할 수 없습니다.  

The object is encrypted server-side by AWS using AES-256 encryption.  
객체는 AWS에서 AES-256 암호화를 사용하여 서버 측에서 암호화됩니다.  

To request Amazon S3 to encrypt the object using SSE-S3, you must set the header:  
SSE-S3로 객체를 암호화하려면 헤더를 설정해야 합니다.  

```

x-amz-server-side-encryption: AES256

```

SSE-S3 is enabled by default for new buckets and new objects.  
SSE-S3는 새 버킷과 새 객체에 기본적으로 활성화됩니다.  

When you upload a file with the correct header, it becomes an object under Amazon S3.  
정확한 헤더와 함께 파일을 업로드하면 해당 파일은 S3 객체가 됩니다.  

Amazon S3 pairs it with the S3-owned key and performs encryption by mixing the key and the object.  
S3는 객체를 S3 소유 키와 결합하여 암호화를 수행합니다.  

The encrypted object is then stored in your S3 bucket.  
암호화된 객체는 버킷에 저장됩니다.  

---

## SSE-KMS: Server-Side Encryption with AWS KMS Keys  
## SSE-KMS: AWS KMS 키를 사용한 서버 측 암호화  

With SSE-KMS, you manage your own keys using the AWS Key Management Service (KMS).  
SSE-KMS에서는 AWS KMS를 사용하여 직접 키를 관리합니다.  

The advantages of using KMS are:  
KMS 사용의 장점:  

- User control over the key: you can create keys yourself within KMS.  
- 키에 대한 사용자 제어: KMS에서 직접 키 생성 가능  
- Key usage is logged using AWS CloudTrail.  
- 키 사용 내역은 AWS CloudTrail에 기록  
- Anytime someone uses a key in KMS, it is logged in CloudTrail.  
- KMS 키가 사용될 때마다 CloudTrail에 기록됨  

To use SSE-KMS, you must set the header:  
SSE-KMS를 사용하려면 헤더를 설정해야 합니다.  

```

x-amz-server-side-encryption: aws:kms

````

When you upload the object with this header, you specify the KMS key to use.  
이 헤더로 객체를 업로드하면 사용할 KMS 키를 지정합니다.  

The object appears in Amazon S3, and the KMS key from AWS KMS is used for encryption.  
객체가 S3에 나타나며 AWS KMS 키로 암호화됩니다.  

To read the file, you need access to both the object and the underlying KMS key used for encryption, providing another level of security.  
파일을 읽으려면 객체와 암호화에 사용된 KMS 키 모두에 접근해야 하므로 추가 보안이 제공됩니다.  

SSE-KMS has some limitations.  
SSE-KMS에는 몇 가지 제한이 있습니다.  

When you upload or download files from Amazon S3, you need to leverage a KMS key, which has its own APIs such as GenerateDataKey and Decrypt.  
S3에서 파일 업로드/다운로드 시 KMS 키를 사용해야 하며, GenerateDataKey와 Decrypt 등의 자체 API가 필요합니다.  

Each API call counts towards the KMS quotas of API calls per second, which ranges between 5,000 and 30,000 requests per second depending on the region.  
각 API 호출은 지역에 따라 초당 5,000~30,000 요청 범위의 KMS API 할당량에 포함됩니다.  

These quotas can be increased using the Service Quotas Console.  
Service Quotas 콘솔을 사용해 할당량을 늘릴 수 있습니다.  

If you have a high throughput S3 bucket with everything encrypted using KMS keys, you may encounter a throttling use case.  
모든 객체를 KMS 키로 암호화한 높은 처리량 S3 버킷에서는 스로틀링이 발생할 수 있습니다.  

---

## SSE-C: Server-Side Encryption with Customer-Provided Keys  
## SSE-C: 고객 제공 키를 사용한 서버 측 암호화  

With SSE-C, the keys are managed outside of AWS, but it is still server-side encryption because you send the key to AWS.  
SSE-C는 키를 AWS 외부에서 관리하지만, 키를 AWS로 보내므로 여전히 서버 측 암호화입니다.  

Amazon S3 never stores the encryption key you provide; after use, the key is discarded.  
S3는 제공된 키를 저장하지 않으며, 사용 후 키는 폐기됩니다.  

Because you transmit a key into Amazon S3, you must use HTTPS and pass the key as part of HTTP headers for every request.  
키를 S3로 전송하므로 HTTPS를 사용하고 HTTP 헤더에 키를 포함해야 합니다.  

When uploading a file, you provide the key, which you manage outside of AWS.  
파일 업로드 시, AWS 외부에서 관리하는 키를 제공합니다.  

Amazon S3 uses the client-provided key and the object to perform encryption, and the encrypted file is stored in the S3 bucket.  
S3는 클라이언트 제공 키와 객체를 사용해 암호화하며, 암호화된 파일을 버킷에 저장합니다.  

To read the file, you must again provide the same key used for encryption.  
파일을 읽으려면 동일한 키를 다시 제공해야 합니다.  

---

## Client-Side Encryption  
## 클라이언트 측 암호화  

With client-side encryption, clients must encrypt data themselves before sending it to Amazon S3.  
클라이언트 측 암호화에서는 S3에 보내기 전에 데이터를 직접 암호화해야 합니다.  

You can use a client library, such as the Client-Side Encryption Library, to help with this process.  
Client-Side Encryption Library 같은 클라이언트 라이브러리를 사용하여 암호화 가능  

Decryption of the data also happens on the client, outside of Amazon S3.  
데이터 복호화 또한 클라이언트 측에서 수행되며 S3에서는 처리되지 않습니다.  

Clients fully manage the keys and the encryption cycle.  
클라이언트가 키와 암호화 주기를 완전히 관리합니다.  

---

## Encryption in Transit  
## 전송 중 암호화  

Encryption in transit, also called SSL or TLS, ensures secure transmission of data.  
전송 중 암호화(SSL 또는 TLS라고도 함)는 데이터 안전 전송을 보장합니다.  

Amazon S3 buckets have two endpoints:  
S3 버킷에는 두 가지 엔드포인트가 있습니다.  

- HTTP endpoint: not encrypted  
- HTTP 엔드포인트: 암호화되지 않음  
- HTTPS endpoint: encrypted in flight  
- HTTPS 엔드포인트: 전송 중 암호화  

When you see a lock icon in your browser, it usually means the connection is encrypted in flight, meaning the connection between you and the target server is secure and fully encrypted.  
브라우저에서 자물쇠 아이콘은 전송 중 암호화를 의미하며, 사용자와 서버 간 연결이 안전하게 암호화됨  

When using Amazon S3, it is recommended to use HTTPS for secure transmission of data.  
S3 사용 시, 안전한 데이터 전송을 위해 HTTPS 사용 권장  

If you use the SSE-C mechanism, you must use the HTTPS protocol.  
SSE-C를 사용할 경우 HTTPS 프로토콜 필수  

Most clients use the HTTPS endpoint by default.  
대부분의 클라이언트는 기본적으로 HTTPS 엔드포인트 사용  

---

## Enforcing Encryption in Transit with Bucket Policy  
## 버킷 정책으로 전송 중 암호화 강제 적용  

To force encryption in transit, you can use a bucket policy.  
전송 중 암호화를 강제 적용하려면 버킷 정책 사용 가능  

Attach a policy to your S3 bucket with a statement that denies any GetObject operation if the condition aws:SecureTransport is false.  
aws:SecureTransport 조건이 false일 경우 GetObject 작업을 거부하는 정책을 버킷에 적용  

SecureTransport is true when using HTTPS and false when not using an encrypted connection.  
SecureTransport는 HTTPS 사용 시 true, 암호화되지 않은 연결 시 false  

Any user trying to use HTTP on your bucket will be blocked, while users using HTTPS will be allowed.  
HTTP를 사용하는 사용자는 차단되고 HTTPS 사용자는 허용됨  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect
````


": "Deny",
"Principal": "*",
"Action": "s3:GetObject",
"Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*",
"Condition": {
"Bool": {"aws:SecureTransport": "false"}
}
}
]
}

```

That concludes the discussion on encryption in Amazon S3.  
이로써 Amazon S3 암호화에 대한 설명을 마칩니다.  

---

## Key Takeaways  
## 주요 포인트  

- Amazon S3 supports four main encryption methods: SSE-S3, SSE-KMS, SSE-C, and client-side encryption.  
- S3는 SSE-S3, SSE-KMS, SSE-C, 클라이언트 측 암호화 4가지 방법을 지원  

- SSE-S3 uses AWS-managed keys and is enabled by default for new buckets and objects.  
- SSE-S3는 AWS 관리 키를 사용하며 새 버킷과 객체에 기본 활성화  

- SSE-KMS allows user control over keys using AWS Key Management Service, with additional security and API quotas.  
- SSE-KMS는 KMS를 통해 키를 사용자 관리 가능, 추가 보안 및 API 할당량 제공  

- SSE-C requires customer-provided keys, which are never stored by AWS and must be transmitted over HTTPS.  
- SSE-C는 고객 제공 키 필요, AWS에 저장되지 않으며 HTTPS로 전송  

- Client-side encryption requires clients to encrypt and decrypt data themselves, fully managing the keys.  
- 클라이언트 측 암호화는 클라이언트가 데이터 암복호화 및 키를 전부 관리  

- Encryption in transit is achieved using HTTPS, and bucket policies can enforce secure transport.  
- 전송 중 암호화는 HTTPS 사용으로 구현되며, 버킷 정책으로 강제 적용 가능  


🎮 **게임보상:**

* **S3 Encryption 학습 완료!**

  * SSE-S3/SSE-KMS/SSE-C 이해 +15
  * 클라이언트 측 암호화 및 전송 암호화 이해 +10
  * 버킷 정책 적용 이해 +10
    총 **35 XP 획득!** 🎉
