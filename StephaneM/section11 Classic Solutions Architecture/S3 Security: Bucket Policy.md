# S3 Security: Bucket Policy  
# S3 보안: 버킷 정책  

---

## Introduction to Amazon S3 Security  
## Amazon S3 보안 소개  
Amazon S3 security can be approached from multiple perspectives.  
Amazon S3 보안은 여러 관점에서 접근 가능.  
👉 설명: S3 보안은 다양한 방법으로 관리 가능함.  

The first part is user-based security, where IAM policies authorize which API calls are allowed for a specific IAM user.  
첫 번째는 사용자 기반 보안으로, IAM 정책이 특정 IAM 사용자가 허용된 API 호출을 결정.  
👉 설명: IAM 사용자 권한 설정 기반 보안.  

---

## Resource-Based Security with S3 Bucket Policies  
## S3 버킷 정책을 통한 리소스 기반 보안  
In addition to user-based security, resource-based security is available.  
사용자 기반 보안 외에도 리소스 기반 보안 존재.  
👉 설명: 버킷 자체 정책으로 접근 제어 가능.  

This is a newer feature where S3 Bucket policies define bucket-wide rules that can be assigned directly from the S3 console.  
S3 버킷 정책은 콘솔에서 직접 할당 가능한 전체 버킷 규칙 정의 기능.  
👉 설명: 중앙에서 정책 적용 가능.  

These policies allow, for example, a specific user or a user from another AWS account (cross-account access) to access your S3 buckets.  
정책을 통해 특정 사용자나 다른 AWS 계정 사용자(교차 계정 접근)에게 버킷 접근 허용 가능.  
👉 설명: 교차 계정 접근 관리.  

This mechanism is also used to make S3 buckets public, which will be demonstrated shortly.  
이 메커니즘은 S3 버킷을 공개할 때도 사용됨.  
👉 설명: 공개 접근 설정 가능.  

---

## Object and Bucket Access Control Lists (ACLs)  
## 오브젝트 및 버킷 ACL  
Another layer of security involves Object Access Control Lists (ACLs), which provide finer-grained permissions and can be disabled if desired.  
오브젝트 ACL은 세밀한 권한 제공, 필요시 비활성화 가능.  
👉 설명: 객체 단위 권한 설정.  

Similarly, bucket-level ACLs exist but are less common and can also be disabled.  
버킷 ACL도 존재하지만 덜 사용되며 비활성화 가능.  
👉 설명: 버킷 단위 권한 설정.  

Currently, the most common method to secure an Amazon S3 bucket is through bucket policies.  
현재 가장 일반적인 S3 보안 방법은 버킷 정책 사용.  
👉 설명: 실무에서는 정책 중심 관리.  

---

## When Can an IAM Principal Access an S3 Object?  
## IAM 주체가 S3 오브젝트에 접근할 수 있는 조건  
An IAM principal can access an S3 object if the IAM permissions allow it, or if the resource policies allow it, provided there is no explicit deny on the action.  
IAM 권한 또는 리소스 정책이 허용되고, 명시적 거부가 없으면 IAM 주체가 S3 오브젝트 접근 가능.  
👉 설명: 권한 허용 조건.  

Under these conditions, the IAM principal can perform the specified API call on the S3 object.  
이 조건 하에서 IAM 주체는 해당 API 호출 수행 가능.  
👉 설명: 권한 부여 범위 이해.  

We will explore these use cases shortly.  
곧 실습으로 사례 학습 예정.  
👉 설명: 실습 기반 이해 강화.  

---

## Encryption as a Security Measure  
## 보안 측면에서의 암호화  
Another way to secure Amazon S3 is by encrypting objects using encryption keys, adding a layer of protection to the stored data.  
S3 오브젝트를 암호화하여 저장 데이터 보호.  
👉 설명: 암호화는 필수 보안 조치.  

---

## Structure of an S3 Bucket Policy  
## S3 버킷 정책 구조  
S3 bucket policies are JSON-based documents that are relatively easy to read.  
S3 버킷 정책은 JSON 기반 문서로 읽기 쉬움.  
👉 설명: 정책 구조 이해.  

The policy includes a resource block specifying the buckets and objects the policy applies to.  
정책에는 적용 대상 버킷과 오브젝트를 지정하는 리소스 블록 포함.  
👉 설명: 정책 범위 정의.  

For example, a resource might apply to every object within a bucket, indicated by a wildcard star (*).  
예: 리소스는 와일드카드(*)를 사용해 모든 오브젝트 적용 가능.  
👉 설명: 전체 객체 대상 지정 가능.  

The policy also specifies an effect, which can be either Allow or Deny, and defines which actions are allowed or denied.  
정책은 Allow 또는 Deny 효과 지정, 허용/거부 API 정의.  
👉 설명: 정책 결과 설정.  

For instance, the action GetObject can be allowed, enabling anyone specified by the principal to retrieve objects from the bucket.  
예: GetObject 허용 시 지정된 주체가 오브젝트 다운로드 가능.  
👉 설명: 개별 API 접근 허용 예시.  

In the example, the principal is set to a wildcard star (*), meaning anyone can perform the GetObject action on any object within the bucket.  
예제에서 주체를 (*)로 설정, 누구나 GetObject 가능.  
👉 설명: 공용 읽기 권한 설정.  

This effectively sets public read access on all objects inside the bucket.  
결과적으로 모든 오브젝트에 공용 읽기 권한 부여.  
👉 설명: 버킷 공개 설정.  

---

## Uses of S3 Bucket Policies  
## S3 버킷 정책 활용  
S3 bucket policies can be used to grant public access to a bucket, enforce encryption on objects at upload, or grant access to another AWS account.  
버킷 정책으로 공용 접근 허용, 업로드 시 암호화 강제, 다른 AWS 계정 접근 허용 가능.  
👉 설명: 실무 활용 사례.  

Let's examine these scenarios.  
이제 시나리오 살펴보기.  
👉 설명: 실습 준비.  

---

## Public Access Bucket Policy Example  
## 공용 접근 버킷 정책 예제  
Consider a website visitor on the worldwide web who wants to access files within your S3 bucket.  
웹사이트 방문자가 S3 버킷 파일 접근을 원한다고 가정.  
👉 설명: 실제 접근 상황 예시.  

By attaching a bucket policy that allows public access, as shown previously, any object within the bucket becomes accessible.  
공용 접근 허용 정책 적용 시 모든 오브젝트 접근 가능.  
👉 설명: 정책 적용 효과.  

This will be demonstrated in the hands-on section.  
실습에서 직접 시연 예정.  
👉 설명: 실습 기반 이해 강화.  

---

## IAM User Access  
## IAM 사용자 접근  
If you have an IAM user within your AWS account who needs to access Amazon S3, you can assign IAM permissions to that user through a policy.  
AWS 계정 내 IAM 사용자가 S3 접근 필요 시, 정책을 통해 권한 부여 가능.  
👉 설명: 사용자 기반 접근 관리.  

When the policy allows access to the S3 buckets, the user can access those buckets accordingly.  
정책 허용 시 사용자가 버킷 접근 가능.  
👉 설명: 권한 반영 확인.  

---

## EC2 Instance Access via IAM Roles  
## IAM 역할을 통한 EC2 접근  
For EC2 instances requiring access to S3 buckets, IAM users are not appropriate.  
S3 접근이 필요한 EC2는 IAM 사용자 사용 불가.  
👉 설명: 인스턴스 권한 관리 차이.  

Instead, you create an IAM role for the EC2 instance with the correct permissions.  
대신 EC2 전용 IAM 역할 생성, 권한 부여.  
👉 설명: 역할 기반 접근 제어.  

The EC2 instance will then be able to access the Amazon S3 buckets using this role.  
EC2 인스턴스가 역할을 통해 S3 접근 가능.  
👉 설명: 역할 기반 인증 적용.  

---

## Cross-Account Access  
## 교차 계정 접근  
To allow cross-account access, where an IAM user from another AWS account needs access to your S3 buckets, you must use a bucket policy.  
다른 AWS 계정 IAM 사용자에게 접근 허용 시 버킷 정책 필요.  
👉 설명: 교차 계정 설정 방법.  

This policy grants access to the specific IAM user in the other account, enabling them to make API calls to your S3 buckets.  
정책을 통해 해당 IAM 사용자에게 API 호출 권한 부여.  
👉 설명: 세부 권한 설정.  

---

## Block Public Access Settings  
## 공용 접근 차단 설정  
AWS provides bucket settings called Block Public Access, which are enabled by default when creating buckets.  
AWS는 Block Public Access 설정 제공, 버킷 생성 시 기본 활성화.  
👉 설명: 기본 보안 강화 기능.  

These settings serve as an extra security layer to prevent accidental data leaks.  
이 설정은 의도치 않은 데이터 유출 방지 추가 보안층 역할.  
👉 설명: 안전 장치 역할.  

Even if a bucket policy makes a bucket public, these settings will prevent the bucket from being publicly accessible.  
버킷 정책이 공용 접근 허용해도 설정이 활성화되면 공개 불가.  
👉 설명: 정책보다 우선 적용.  

If you want to ensure that your bucket is never public, keep these settings enabled.  
버킷을 절대 공개하지 않으려면 설정 유지.  
👉 설명: 안전한 관리 권장.  

They provide protection against misconfigured bucket policies.  
잘못된 정책 설정으로부터 보호.  
👉 설명: 보안 예방 조치.  

Additionally, you can apply these settings at the account level if none of your buckets should ever be public.  
계정 단위 적용 가능, 모든 버킷 공용 금지 시 유용.  
👉 설명: 계정 전체 보호.  

---

## Conclusion  
## 결론  
This concludes the overview of Amazon S3 security.  
S3 보안 개요 마침.  
👉 설명: 이론 학습 완료.  

Next, we will proceed to the hands-on section to practice these concepts.  
다음은 실습 섹션에서 개념 적용 예정.  
👉 설명: 실습 기반 이해 강화.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 security includes user-based IAM policies, resource-based bucket policies, and object ACLs.  
- S3 보안은 사용자 기반 IAM 정책, 리소스 기반 버킷 정책, 오브젝트 ACL 포함.  

- S3 Bucket policies are JSON documents that define permissions on buckets and objects, allowing actions like GetObject.  
- 버킷 정책은 JSON 문서, 버킷/오브젝트 권한 정의, GetObject 등 액션 허용.  

- Bucket policies can grant public access, cross-account access, or enforce encryption.  
- 버킷 정책으로 공용 접근, 교차 계정 접근, 업로드 시 암호화 적용 가능.  

- AWS provides Block Public Access settings to prevent accidental public exposure of buckets, adding an extra security layer.  
- AWS는 Block Public Access 제공, 버킷 공용 노출 방지, 추가 보안층 제공.  

---

🎮 **게임보상:**

* **“S3 보안 전문가 칭호 획득!”**

  * 사용자/리소스 기반 보안 이해 +25
  * 버킷 정책 작성 및 분석 +25


* ACL과 공개 접근 차단 이해 +25
* 교차 계정 및 EC2 역할 접근 관리 +25

총 **100 XP 획득!** 🎉
