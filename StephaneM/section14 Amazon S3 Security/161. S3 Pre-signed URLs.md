# S3 Pre-signed URLs  
# S3 사전 서명 URL  

---

## Introduction to Amazon S3 Pre-signed URLs  
## Amazon S3 사전 서명 URL 소개  

Amazon S3 pre-signed URLs are URLs that you can generate using the S3 console, the CLI, or the SDK. These URLs have an expiration time after which they become invalid.  
Amazon S3 사전 서명 URL은 S3 콘솔, CLI, 또는 SDK를 사용하여 생성할 수 있는 URL입니다. 이 URL에는 만료 시간이 지정되어 있으며, 만료 후에는 사용할 수 없습니다.  

---

When using the console, the maximum expiration time is up to 12 hours. If you use the CLI, you can set the expiration time up to 168 hours.  
콘솔을 사용할 경우 최대 만료 시간은 12시간까지입니다. CLI를 사용하면 최대 168시간까지 만료 시간을 설정할 수 있습니다.  

---

## How Pre-signed URLs Work  
## 사전 서명 URL 작동 방식  

When you generate a pre-signed URL, the user who receives that URL inherits the permissions of the user who generated it. This applies for both GET and PUT operations.  
사전 서명 URL을 생성하면, 해당 URL을 받은 사용자는 URL을 생성한 사용자의 권한을 상속받습니다. 이는 GET과 PUT 작업 모두에 적용됩니다.  

---

## Use Case for Pre-signed URLs  
## 사전 서명 URL 사용 사례  

Suppose you have an S3 bucket that is private, and you want to give someone outside of AWS access to a single file. You do not want to make that file public or compromise your security in any way.  
만약 개인용 S3 버킷이 있고, AWS 외부의 사용자에게 단일 파일에 접근 권한을 주고 싶다고 가정해봅니다. 파일을 공개하거나 보안을 위태롭게 하고 싶지는 않습니다.  

---

As the bucket owner or authorized user, you generate a pre-signed URL for that specific file. The S3 bucket then provides you with a URL that is pre-signed, meaning it carries your credentials in terms of authorization to access that file.  
버킷 소유자 또는 권한이 있는 사용자는 해당 파일에 대한 사전 서명 URL을 생성합니다. 그러면 S3 버킷은 사전 서명된 URL을 제공하며, 이 URL에는 해당 파일 접근 권한을 갖는 생성자의 자격 증명이 포함됩니다.  

---

You then send this URL to the target user to whom you want to grant access to the file for a limited amount of time.  
그런 다음 이 URL을 제한된 시간 동안 파일에 접근하도록 허용하고 싶은 대상 사용자에게 전송합니다.  

---

The user will use the URL to access the file on the S3 bucket. They will be able to download the file, for example, during the validity period of the URL.  
사용자는 해당 URL을 사용하여 S3 버킷의 파일에 접근합니다. 예를 들어, URL의 유효 기간 동안 파일을 다운로드할 수 있습니다.  

---

## Common Use Cases  
## 일반적인 사용 사례  

Pre-signed URLs are a very common solution for temporary access to a specific file, either for download or upload.  
사전 서명 URL은 특정 파일에 대한 임시 접근을 제공하는 매우 일반적인 솔루션입니다. 다운로드 또는 업로드 모두 가능합니다.  

---

- Allow only logged-in users to download a premium video stored in your S3 bucket.  
- S3 버킷에 저장된 프리미엄 비디오를 로그인한 사용자만 다운로드할 수 있도록 허용합니다.  

- Dynamically generate URLs to allow an ever-changing list of users to download files.  
- 동적으로 URL을 생성하여 계속 변경되는 사용자 목록이 파일을 다운로드할 수 있도록 합니다.  

- Temporarily allow a user to upload a file to a precise location in your private S3 bucket.  
- 특정 사용자가 개인 S3 버킷의 정확한 위치에 파일을 일시적으로 업로드할 수 있도록 허용합니다.  

---

## Conclusion  
## 결론  

That concludes this lecture on Amazon S3 pre-signed URLs. In the next lecture, we will have some hands-on examples.  
이로써 Amazon S3 사전 서명 URL에 대한 강의를 마칩니다. 다음 강의에서는 실습 예제를 진행할 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 pre-signed URLs allow temporary access to private S3 bucket files.  
- Amazon S3 사전 서명 URL은 개인 S3 버킷 파일에 임시 접근 권한을 제공합니다.  

- Pre-signed URLs can be generated via the S3 console, CLI, or SDK, with expiration times up to 168 hours.  
- 사전 서명 URL은 S3 콘솔, CLI, 또는 SDK를 통해 생성 가능하며, 만료 시간은 최대 168시간까지 설정할 수 있습니다.  

- The user accessing the file via the pre-signed URL inherits the permissions of the URL generator.  
- 사전 서명 URL을 통해 파일에 접근하는 사용자는 URL 생성자의 권한을 상속받습니다.  

- Common use cases include granting temporary download or upload access without making files public.  
- 일반적인 사용 사례는 파일을 공개하지 않고 임시 다운로드 또는 업로드 권한을 부여하는 것입니다.  

🎮 **게임보상:**

* 사전 서명 URL 개념 이해 +10 XP
* 임시 접근 권한 관리 개념 습득 +10 XP
* S3 보안 실무 활용 이해 +10 XP
  총 **30 XP 획득!** 🎉
