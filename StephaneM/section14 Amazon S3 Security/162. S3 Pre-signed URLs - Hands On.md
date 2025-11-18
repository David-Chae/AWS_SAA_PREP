# S3 Pre-signed URLs - Hands On  
# S3 사전 서명 URL 실습  

---

## Demonstrating S3 Pre-signed URLs  
## S3 사전 서명 URL 시연  

Let's demonstrate how to use S3 pre-signed URLs. I will select a bucket that I know is not public.  
S3 사전 서명 URL을 사용하는 방법을 시연해보겠습니다. 공개되지 않은 버킷을 선택합니다.  

---

For example, I click on my coffee.jpg image, but you can select any image you want.  
예를 들어, coffee.jpg 이미지를 클릭하지만, 원하는 다른 이미지를 선택할 수도 있습니다.  

---

We know this image is private because if I click on the object URL, I receive an "Access Denied" error.  
이 이미지가 개인용임을 아는 이유는 객체 URL을 클릭하면 "접근 거부" 오류가 나타나기 때문입니다.  

---

This public URL does not work since the bucket is not public.  
버킷이 공개되지 않았기 때문에 이 공개 URL은 작동하지 않습니다.  

---

However, if I click on "Open" here, it opens a new tab and the image displays correctly. Why is that?  
하지만 여기서 "열기(Open)"를 클릭하면 새 탭이 열리고 이미지가 정상적으로 표시됩니다. 왜 그럴까요?  

---

The beginning of the URL is the same as before, but appended to it is a pre-signed URL.  
URL의 시작 부분은 이전과 동일하지만, 여기에 사전 서명 URL이 추가되어 있습니다.  

---

This URL was pre-signed with my credentials, allowing me to access the image despite the bucket's privacy settings.  
이 URL은 제 자격 증명으로 사전 서명되었기 때문에, 버킷이 비공개 설정되어 있어도 이미지를 접근할 수 있습니다.  

---

## Generating Pre-signed URLs  
## 사전 서명 URL 생성  

How do we generate pre-signed URLs for others? There are two options:  
다른 사용자를 위해 사전 서명 URL을 생성하는 방법은 두 가지가 있습니다:  

---

- Use the AWS CLI.  
- AWS CLI를 사용합니다.  

- Generate them directly from the AWS Management Console.  
- AWS 관리 콘솔에서 직접 생성합니다.  

---

In the console, click on "Object Actions" and then select "Share a pre-signed URL."  
콘솔에서 "객체 작업(Object Actions)"을 클릭한 다음, "사전 서명 URL 공유(Share a pre-signed URL)"를 선택합니다.  

---

A message indicates that anyone with this URL can access the object until the URL expires, even if the bucket and object are private.  
메시지에는 이 URL을 가진 누구든지 버킷과 객체가 비공개여도 URL이 만료될 때까지 객체에 접근할 수 있다고 표시됩니다.  

---

You can specify how long the URL will be valid. For example, I will set it to be valid for the next five minutes.  
URL의 유효 기간을 지정할 수 있습니다. 예를 들어, 다음 5분 동안 유효하도록 설정할 수 있습니다.  

---

After clicking "Create pre-signed URL," the URL is generated and can be shared with anyone.  
"사전 서명 URL 생성(Create pre-signed URL)"을 클릭하면 URL이 생성되어 누구에게나 공유할 수 있습니다.  

---

Anyone with this URL can access the image until the expiration time, providing a secure and convenient way to share private files.  
이 URL을 가진 누구든지 만료 시간까지 이미지를 접근할 수 있으며, 개인 파일을 안전하고 편리하게 공유할 수 있습니다.  

---

This method is very handy for quickly sharing access to files in your S3 bucket while ensuring the URL expires for maximum security.  
이 방법은 S3 버킷 파일 접근을 빠르게 공유할 수 있고, URL이 만료되도록 설정하여 최대한 안전하게 공유할 수 있어 매우 유용합니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 pre-signed URLs allow temporary access to private objects in a bucket.  
- S3 사전 서명 URL은 버킷의 개인 객체에 임시 접근 권한을 제공합니다.  

- Pre-signed URLs can be generated via the AWS CLI or directly from the AWS Management Console.  
- 사전 서명 URL은 AWS CLI 또는 AWS 관리 콘솔에서 직접 생성할 수 있습니다.  

- These URLs include credentials embedded to grant access until they expire.  
- 이 URL에는 만료될 때까지 접근을 허용하는 자격 증명이 포함되어 있습니다.  

- Setting an expiration time ensures secure, time-limited sharing of private files.  
- 만료 시간을 설정하면 개인 파일을 안전하게 제한된 시간 동안 공유할 수 있습니다.  

🎮 **게임보상:**

* S3 사전 서명 URL 실습 이해 +10 XP
* AWS 콘솔/CLI 활용 실습 개념 +10 XP
* 안전한 파일 공유 원리 습득 +10 XP
  총 **30 XP 획득!** 🎉
