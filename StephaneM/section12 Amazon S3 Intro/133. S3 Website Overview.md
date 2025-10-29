# S3 Website Overview  
# S3 웹사이트 개요  

---

## Introduction to Amazon S3 Website Hosting  
## Amazon S3 웹사이트 호스팅 소개  

Amazon S3 can be used to create aesthetic websites by hosting static content.  
Amazon S3는 정적 콘텐츠를 호스팅하여 미적인 웹사이트를 만드는 데 사용할 수 있음.  
👉 설명: HTML, CSS, 이미지 등 정적 파일을 이용한 웹사이트 구축 가능.  

These websites are accessible on the internet through URLs that depend on the AWS region where the S3 bucket is created.  
이 웹사이트들은 S3 버킷이 생성된 AWS 리전에 따라 달라지는 URL을 통해 인터넷에서 접근 가능.  
👉 설명: URL 구조는 리전에 따라 결정됨.  

The URLs for these websites look very similar, with the only difference being that in one case there is a dash and in another case there is a dot.  
웹사이트 URL은 매우 유사하며, 차이점은 한 경우에는 대시(-)가 있고 다른 경우에는 점(.)이 있음.  
👉 설명: URL 형태 차이 이해.  

Although it is not necessary to remember this detail, it is useful to be aware of it.  
이 세부사항을 기억할 필요는 없지만, 알고 있으면 유용함.  
👉 설명: URL 규칙 이해.  

---

## Setting Up an S3 Bucket for Website Hosting  
## 웹사이트 호스팅을 위한 S3 버킷 설정  

To host a website, an extra S3 bucket is created which contains files such as HTML files and images.  
웹사이트를 호스팅하려면 HTML 파일과 이미지 등 파일을 담는 추가 S3 버킷 생성.  
👉 설명: 정적 콘텐츠 전용 버킷 필요.  

This bucket is then configured to be compatible with website hosting.  
이 버킷을 웹사이트 호스팅과 호환되도록 구성.  
👉 설명: 웹사이트용 설정 적용.  

Once configured, the website will have a corresponding URL through which users can access the contents of the S3 bucket.  
구성이 완료되면 사용자들이 버킷의 콘텐츠에 접근할 수 있는 URL 생성.  
👉 설명: 최종 접근 URL 확보.  

---

## Importance of Public Read Permissions  
## 공용 읽기 권한의 중요성  

However, the website will not work if public read permissions are not enabled on the S3 bucket.  
하지만 S3 버킷에 공용 읽기 권한이 없으면 웹사이트 작동 불가.  
👉 설명: 권한 없으면 403 오류 발생.  

This is why in the previous lecture, we learned about S3 bucket policies.  
이 때문에 이전 강의에서 S3 버킷 정책에 대해 배움.  
👉 설명: 정책을 통해 공용 접근 허용 필요.  

If you encounter a 403 Forbidden error after enabling your S3 bucket for reads, it means that your bucket is not public.  
S3 버킷 읽기 권한을 활성화했는데 403 Forbidden 오류가 발생하면, 버킷이 여전히 비공개임을 의미.  
👉 설명: 공용 접근 확인 필요.  

Therefore, you must attach an S3 bucket policy that allows public access.  
따라서 공용 접근을 허용하는 S3 버킷 정책을 적용해야 함.  
👉 설명: 정책을 통한 접근 제어.  

---

## Conclusion  
## 결론  

This concludes the short lecture on hosting static websites using Amazon S3.  
Amazon S3를 사용한 정적 웹사이트 호스팅에 대한 짧은 강의 종료.  
👉 설명: 요약 정리.  

Next, we will proceed to hands-on practice to apply these concepts.  
다음으로 실습을 진행하여 개념 적용 예정.  
👉 설명: 실습 준비.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 can host static websites accessible via the internet.  
- Amazon S3는 인터넷에서 접근 가능한 정적 웹사이트 호스팅 가능.  

- The website URL depends on the AWS region where the S3 bucket is created.  
- 웹사이트 URL은 S3 버킷이 생성된 AWS 리전에 따라 달라짐.  

- Public read permissions must be enabled on the S3 bucket for the website to be accessible.  
- 웹사이트 접근을 위해 버킷에 공용 읽기 권한 필수.  

- S3 bucket policies are essential to allow public access and avoid 403 forbidden errors.  
- 공용 접근 허용 및 403 오류 방지를 위해 S3 버킷 정책 필수.  

---

🎮 **게임보상:**

* **“S3 웹사이트 개요 학습 완료!”**

  * 정적 웹사이트 호스팅 이해 +25
  * 공용 읽기 권한 중요성 인지 +25
  * URL 구조와 정책 이해 +25
  * 실습 준비 완료 +25

총 **100 XP 획득!** 🎉
