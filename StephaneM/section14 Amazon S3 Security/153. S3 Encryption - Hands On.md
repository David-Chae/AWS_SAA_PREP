# S3 Encryption - Hands On  
# S3 암호화 실습  

---

## Practicing S3 Encryption  
## S3 암호화 실습하기  

Let's practice encryption by creating an S3 bucket named demo-encryption-stephane-v2. We will enable bucket versioning and set default encryption for the bucket.  
demo-encryption-stephane-v2라는 S3 버킷을 생성하여 암호화를 연습해봅시다. 버킷 버전 관리(versioning)를 활성화하고 기본 암호화를 설정합니다.  

After scrolling down in the bucket creation settings, we leave the default options on and enable bucket versioning. Under default encryption, there are three options available, but we must choose one as the default encryption for our bucket. We will start by selecting SSE-S3, and later explore SSE-KMS and DSSE-KMS.  
버킷 생성 설정에서 아래로 스크롤하여 기본 옵션은 그대로 두고 버킷 버전 관리를 활성화합니다. 기본 암호화에는 세 가지 옵션이 있으며, 버킷의 기본 암호화 방법으로 하나를 선택해야 합니다. 먼저 SSE-S3를 선택하고 이후 SSE-KMS와 DSSE-KMS를 살펴봅니다.  

We click on Create a bucket to finalize the creation. Now, the bucket has default encryption enabled.  
"Create a bucket"를 클릭하여 생성 작업을 완료합니다. 이제 버킷에는 기본 암호화가 활성화되었습니다.  

---

## Verifying Encryption by Uploading an Object  
## 객체 업로드로 암호화 확인하기  

To verify the encryption, we upload a file named coffee.jpg to the bucket. After uploading, we select the file and scroll down to the server-side encryption settings. The file is encrypted with server-side encryption using Amazon S3 managed keys, which is SSE-S3.  
암호화를 확인하기 위해 coffee.jpg 파일을 버킷에 업로드합니다. 업로드 후 파일을 선택하고 서버 측 암호화 설정을 확인합니다. 파일은 Amazon S3 관리 키(SSE-S3)를 사용하여 서버 측 암호화되었습니다.  

We can also edit the encryption mechanism for a file. Editing the server-side encryption creates a new version of the object with the updated settings. This is why bucket versioning was enabled — to allow multiple versions of the file with different encryption settings.  
파일의 암호화 방식을 수정할 수도 있습니다. 서버 측 암호화를 수정하면 업데이트된 설정으로 객체의 새 버전이 생성됩니다. 이 때문에 버킷 버전 관리가 활성화되었습니다 — 서로 다른 암호화 설정을 가진 파일 버전을 여러 개 허용하기 위해서입니다.  

---

## Changing Encryption to SSE-KMS  
## SSE-KMS로 암호화 변경하기  

Let's change the encryption for the object by overriding the bucket's default encryption settings for this specific file. We have the choice to use SSE-KMS or DSSE-KMS. DSSE-KMS involves two levels of encryption on KMS, providing stronger security, but we will focus on SSE-KMS for simplicity and cost-effectiveness.  
특정 파일에 대해 버킷의 기본 암호화 설정을 무시하고 객체의 암호화를 변경해봅시다. SSE-KMS 또는 DSSE-KMS를 선택할 수 있습니다. DSSE-KMS는 KMS 기반 두 단계 암호화를 제공하여 보안을 강화하지만, 여기서는 단순성과 비용 효율성을 위해 SSE-KMS에 집중합니다.  

When selecting SSE-KMS, we must specify a KMS key. We can either enter a KMS key ARN or choose from existing KMS keys. Typically, only the default AWS managed KMS key for S3 (AWS/S3) is available, which does not incur additional costs. Custom KMS keys can be created but may incur monthly charges.  
SSE-KMS를 선택할 때 KMS 키를 지정해야 합니다. KMS 키 ARN을 입력하거나 기존 KMS 키를 선택할 수 있습니다. 일반적으로 S3의 기본 AWS 관리 KMS 키(AWS/S3)만 사용 가능하며 추가 비용이 없습니다. 사용자 지정 KMS 키를 생성할 수도 있지만 월별 요금이 발생할 수 있습니다.  

We select the default AWS/S3 KMS key and save the changes. Now, under the Versions tab, we see two versions of the file. The current version is encrypted with SSE-KMS using the default AWS/S3 KMS key.  
기본 AWS/S3 KMS 키를 선택하고 변경 사항을 저장합니다. 이제 Versions 탭에서 파일의 두 버전을 확인할 수 있습니다. 현재 버전은 기본 AWS/S3 KMS 키를 사용하여 SSE-KMS로 암호화되었습니다.  

---

## Uploading Another File with Encryption Options  
## 다른 파일 업로드 시 암호화 옵션 선택하기  

We upload another file, for example, beach.jpg. Under the file's Properties, we find the server-side encryption settings. Here, we can specify an encryption key to either use the bucket's default encryption or override it with SSE-S3, SSE-KMS, or DSSE-KMS. This is one way to manage encryption on a per-object basis.  
beach.jpg와 같은 다른 파일을 업로드합니다. 파일의 Properties에서 서버 측 암호화 설정을 확인합니다. 여기서 버킷의 기본 암호화를 사용하거나 SSE-S3, SSE-KMS, DSSE-KMS로 개별 객체 암호화를 덮어쓸 수 있습니다. 이는 객체 단위로 암호화를 관리하는 방법입니다.  

---

## Reviewing Default Encryption Settings  
## 기본 암호화 설정 검토하기  

In the bucket properties, under Default encryption, we can edit and select SSE-S3, SSE-KMS, or DSSE-KMS as the default encryption method. When SSE-KMS is selected, an additional option called bucket key is available. This option reduces costs by minimizing API calls to AWS KMS and is enabled by default.  
버킷 속성에서 Default encryption 아래에서 SSE-S3, SSE-KMS, DSSE-KMS 중 하나를 기본 암호화 방법으로 선택할 수 있습니다. SSE-KMS를 선택하면 추가 옵션인 bucket key가 제공됩니다. 이 옵션은 AWS KMS API 호출을 최소화하여 비용을 절감하며 기본적으로 활성화되어 있습니다.  

If SSE-S3 is used as the default encryption, the bucket key setting does not apply. We have seen how to change the default encryption settings for the bucket.  
기본 암호화로 SSE-S3를 사용하는 경우 bucket key 설정은 적용되지 않습니다. 우리는 버킷의 기본 암호화 설정을 변경하는 방법을 확인했습니다.  

---

## Notes on SSE-C and Client-Side Encryption  
## SSE-C 및 클라이언트 측 암호화 관련 주의 사항  

You may notice that SSE-C (server-side encryption with customer-provided keys) is missing from the console options. This is because SSE-C can only be enabled via the AWS CLI, not through the AWS Management Console.  
콘솔 옵션에서 SSE-C(고객 제공 키를 사용한 서버 측 암호화)가 없는 것을 볼 수 있습니다. 이는 SSE-C가 AWS CLI를 통해서만 활성화 가능하고 AWS 관리 콘솔에서는 불가능하기 때문입니다.  

For client-side encryption, you must encrypt data before uploading it to AWS and decrypt it after downloading. AWS does not need to be informed that the data is client-side encrypted.  
클라이언트 측 암호화의 경우, 데이터를 업로드 전에 암호화하고 다운로드 후 복호화해야 합니다. AWS는 데이터가 클라이언트 측 암호화되었음을 알 필요가 없습니다.  

---

## Summary  
## 요약  

In the AWS console, the encryption options available for S3 buckets and objects are SSE-S3, SSE-KMS, and DSSE-KMS. SSE-C must be managed via CLI, and client-side encryption is handled entirely by the client application.  
AWS 콘솔에서 S3 버킷과 객체에 사용 가능한 암호화 옵션은 SSE-S3, SSE-KMS, DSSE-KMS입니다. SSE-C는 CLI를 통해 관리해야 하며, 클라이언트 측 암호화는 클라이언트 애플리케이션에서 완전히 처리됩니다.  

This concludes our overview of encryption options in AWS S3.  
이로써 AWS S3 암호화 옵션 개요를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created an S3 bucket with default encryption enabled.  
- 기본 암호화가 활성화된 S3 버킷을 생성했습니다.  

- Demonstrated how to upload files encrypted with SSE-S3 and SSE-KMS.  
- SSE-S3 및 SSE-KMS로 암호화된 파일 업로드 방법을 실습했습니다.  

- Explained the difference between SSE-S3, SSE-KMS, and DSSE-KMS encryption options.  
- SSE-S3, SSE-KMS, DSSE-KMS 암호화 옵션 간 차이를 설명했습니다.  

- Clarified that SSE-C encryption is only available via CLI, not the AWS console.  
- SSE-C 암호화는 AWS 콘솔에서 불가능하며 CLI에서만 가능함을 명확히 했습니다.  

🎮 **게임보상:**

* S3 버킷 생성 및 기본 암호화 실습 +5 XP
* SSE-S3, SSE-KMS 암호화 업로드 실습 +5 XP
* DSSE-KMS 이해 및 개념 학습 +5 XP
* SSE-C와 클라이언트 측 암호화 구분 +5 XP
  총 **20 XP 획득!** 🎉
