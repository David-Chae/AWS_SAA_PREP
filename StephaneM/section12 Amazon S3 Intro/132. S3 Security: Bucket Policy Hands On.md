# S3 Security: Bucket Policy Hands On  
# S3 보안: 버킷 정책 실습  

---

## Configuring Public Access for S3 Bucket  
## S3 버킷의 공용 접근 설정  

Let's proceed to create a bucket policy that allows access to the coffee file via a public URL.  
공용 URL을 통해 coffee 파일에 접근할 수 있는 버킷 정책을 생성해보자.  
👉 설명: 실제 공용 접근 정책 작성 실습 시작.  

To begin, navigate to the Permissions tab of the bucket.  
먼저 버킷의 Permissions 탭으로 이동.  
👉 설명: 권한 설정 접근.  

The first step is to allow public access by modifying the bucket settings, as currently all access is blocked.  
첫 단계는 현재 모든 접근이 차단된 상태이므로, 버킷 설정을 수정해 공용 접근 허용.  
👉 설명: 접근 차단 해제 필요.  

Edit the public access settings and untick the block all public access option.  
공용 접근 설정 편집 후 "block all public access" 옵션 체크 해제.  
👉 설명: 공용 접근 활성화.  

This change enables public access to the bucket. However, this action should only be performed if you intend to set a public bucket policy, as it is a potentially dangerous operation.  
이 변경으로 버킷 공용 접근 가능. 단, 버킷 정책을 공용으로 설정할 의도일 때만 수행해야 하며, 위험할 수 있음.  
👉 설명: 신중히 수행 권장.  

Confirm the change by selecting Yes.  
변경 사항을 Yes 선택으로 확인.  
👉 설명: 설정 적용 완료.  

Keep in mind that making your company's real data public can lead to data leaks, which is highly undesirable.  
실제 회사 데이터를 공개하면 데이터 유출 가능성, 매우 위험.  
👉 설명: 보안 주의.  

After this, under the Permissions overview, you will see that objects can now be public.  
이후 Permissions 개요에서 오브젝트가 이제 공용 가능함 확인.  
👉 설명: 변경 결과 확인.  

This completes the first step.  
첫 번째 단계 완료.  
👉 설명: 준비 완료.  

---

## Creating the Bucket Policy  
## 버킷 정책 생성  

Next, scroll down to the Bucket policy section. Currently, there is no policy applied.  
다음으로 Bucket policy 섹션으로 이동. 현재 정책 없음.  
👉 설명: 정책 생성 준비.  

We want to create one to make the entire bucket public.  
전체 버킷을 공용으로 만들기 위해 정책 생성 필요.  
👉 설명: 목적 정의.  

You can review policy examples in the documentation, which provides various use cases and corresponding bucket policies.  
문서에서 다양한 정책 예제와 사용 사례 확인 가능.  
👉 설명: 참고 자료 활용.  

For our purpose, we will use the AWS Policy Generator.  
이번 실습에서는 AWS Policy Generator 사용.  
👉 설명: 정책 생성 도구 활용.  

Open the AWS Policy Generator and select S3 Bucket Policy as the policy type.  
AWS Policy Generator 열고 S3 Bucket Policy 선택.  
👉 설명: 정책 유형 설정.  

Set the effect to Allow.  
Effect를 Allow로 설정.  
👉 설명: 허용 액션 지정.  

For the principal, enter an asterisk (*) to allow anyone access.  
Principal에는 * 입력하여 누구나 접근 가능하게 설정.  
👉 설명: 모든 사용자 허용.  

The service is Amazon S3, and the action we want to permit is GetObject, which allows reading objects from the bucket.  
서비스는 Amazon S3, 허용 액션은 GetObject, 버킷 오브젝트 읽기 가능.  
👉 설명: 읽기 권한 설정.  

For the Amazon Resource Name (ARN), enter the bucket's ARN followed by a slash and an asterisk to represent all objects within the bucket.  
ARN에는 버킷 ARN 뒤에 /* 추가하여 모든 오브젝트 포함.  
👉 설명: 정책 적용 범위 지정.  

This is necessary because the GetObject action applies to objects inside the bucket, which are specified after the slash.  
GetObject는 슬래시 뒤 오브젝트에 적용되므로 필수.  
👉 설명: 경로 지정 이해.  

To find the bucket ARN, return to the S3 buckets list and copy the ARN displayed for your bucket.  
버킷 ARN 확인: S3 버킷 목록에서 ARN 복사.  
👉 설명: ARN 위치 확인.  

Paste it into the ARN field in the policy generator, then append /* to include all objects.  
ARN 필드에 붙여넣고 /* 추가.  
👉 설명: 전체 오브젝트 포함.  

Add this statement and generate the policy.  
정책 문장 추가 후 정책 생성.  
👉 설명: 정책 완성.  

The generated policy allows GetObject requests from anyone on any object within the bucket.  
생성된 정책은 누구나 모든 오브젝트에 GetObject 요청 가능.  
👉 설명: 정책 기능 확인.  

Copy the generated policy and paste it into the bucket policy editor in the AWS console.  
생성된 정책 복사 후 AWS 콘솔 버킷 정책 에디터에 붙여넣기.  
👉 설명: 콘솔 적용 준비.  

Remove any extra spaces if present, then save the changes.  
여분 공백 제거 후 저장.  
👉 설명: 정책 적용 완료.  

Once saved, the bucket policy is applied successfully.  
저장 후 정책 적용 완료.  
👉 설명: 적용 확인.  

---

## Verifying Public Access  
## 공용 접근 확인  

Navigate to the object, for example, coffee.jpg. Copy the object URL and open it in a browser.  
오브젝트로 이동, 예: coffee.jpg. URL 복사 후 브라우저에서 열기.  
👉 설명: 접근 테스트.  

You should now see the coffee image fully visible and accessible publicly, as well as any other objects in your Amazon S3 bucket.  
이제 coffee 이미지와 버킷의 다른 오브젝트가 공용으로 확인 가능.  
👉 설명: 정책 작동 확인.  

This concludes the lecture. We have covered bucket policies, the policy generator, and verified that the image is publicly accessible.  
강의 종료. 버킷 정책, 정책 생성기 사용법, 공용 접근 확인 완료.  
👉 설명: 실습 요약.  

---

## Key Takeaways  
## 핵심 요약  

- Configured S3 bucket to allow public access by modifying bucket settings.  
- 버킷 설정 수정으로 공용 접근 허용.  

- Created a bucket policy using AWS Policy Generator to permit public read access.  
- AWS Policy Generator로 공용 읽기 정책 생성.  

- Applied the policy to enable public access to all objects within the bucket.  
- 정책 적용으로 버킷 내 모든 오브젝트 공용 접근 가능.  

- Verified public accessibility by accessing the object URL directly.  
- 오브젝트 URL 직접 접근으로 공용 접근 확인.  

---

🎮 **게임보상:**

* **“S3 버킷 공용 접근 실습 완료!”**

  * 버킷 정책 생성 +25
  * 공용 접근 설정 및 확인 +25
  * Policy Generator 활용 +25
  * 실제 객체 접근 테스트 +25

총 **100 XP 획득!** 🎉
