# CloudFront with S3 - Hands On  
# S3와 함께하는 CloudFront - 실습  

---

## Creating an S3 Bucket for CloudFront  
## CloudFront용 S3 버킷 생성  

Let's begin by creating an S3 bucket to hold our files for the CloudFront distribution.  
CloudFront 배포용 파일을 담기 위해 S3 버킷을 생성하는 것으로 시작합니다.  

---

I will name this bucket demo-cloudfront-stephane-v4.  
이 버킷의 이름은 `demo-cloudfront-stephane-v4`로 지정합니다.  

---

We will leave all settings as default and click on Create Bucket.  
모든 설정은 기본값으로 두고, 'Create Bucket'을 클릭합니다.  

---

## Uploading Files to the S3 Bucket  
## S3 버킷에 파일 업로드  

After the bucket is created, I will upload three files: beach.jpg, coffee.jpg, and index.html.  
버킷이 생성된 후, `beach.jpg`, `coffee.jpg`, `index.html` 세 파일을 업로드합니다.  

---

Once uploaded, we can see all files listed in the bucket.  
업로드가 완료되면, 버킷 안에서 모든 파일이 나열된 것을 확인할 수 있습니다.  

---

## Accessing Files in S3  
## S3 파일 접근  

There are two ways to open the index.html file:  
`index.html` 파일을 열 수 있는 방법은 두 가지입니다.  

---

Using the Object URL: This results in an "Access Denied" error because the object is not public.  
객체 URL 사용: 객체가 공개되지 않았기 때문에 "Access Denied" 오류가 발생합니다.  

---

Using the Open option: This generates a pre-signed URL that allows temporary access to the object.  
Open 옵션 사용: 임시 접근을 허용하는 pre-signed URL이 생성됩니다.  

---

However, the image files are still not accessible because they are not public.  
하지만 이미지 파일들은 여전히 공개되지 않았기 때문에 접근할 수 없습니다.  

---

## Using CloudFront to Access Private S3 Files  
## 비공개 S3 파일 접근을 위한 CloudFront 사용  

To make these files accessible without making them public, we will use CloudFront.  
파일을 공개하지 않고 접근 가능하게 만들기 위해 CloudFront를 사용합니다.  

---

Let's open the CloudFront console and create a new distribution named DemoCloudFrontDistribution.  
CloudFront 콘솔을 열고 `DemoCloudFrontDistribution`이라는 새 배포를 생성합니다.  

---

## Configuring the CloudFront Distribution  
## CloudFront 배포 구성  

Distribution Type: Single website or app.  
배포 유형: 단일 웹사이트 또는 앱  

---

Domain: Use the default CloudFront domain name (no custom domain).  
도메인: 기본 CloudFront 도메인 사용 (커스텀 도메인 없음)  

---

Origin Type: Amazon S3.  
오리진 타입: Amazon S3  

---

Origin: Select the demo-cloudfront-stephane-v4 bucket.  
오리진: `demo-cloudfront-stephane-v4` 버킷 선택  

---

Origin Path: Leave empty since content is stored at the root of the bucket.  
오리진 경로: 버킷 루트에 콘텐츠가 저장되어 있으므로 비워둡니다.  

---

Settings: Enable private S3 bucket access to CloudFront. This allows CloudFront to access the bucket privately and automatically modifies the bucket policy.  
설정: CloudFront의 프라이빗 S3 버킷 접근 활성화. CloudFront가 버킷에 프라이빗하게 접근하며, 버킷 정책을 자동으로 수정합니다.  

---

We will use the recommended origin settings and proceed to the next step.  
추천 오리진 설정을 사용하고 다음 단계로 진행합니다.  

---

## Security Settings  
## 보안 설정  

For now, we will not enable additional security features to avoid extra costs.  
현재는 추가 보안 기능을 활성화하지 않아서 추가 비용을 방지합니다.  

---

After reviewing the configuration, we will create the distribution.  
설정을 검토한 후 배포를 생성합니다.  

---

## CloudFront Access to S3 Bucket  
## S3 버킷에 대한 CloudFront 접근  

Because we granted CloudFront access to the S3 origin, CloudFront can write and update the S3 bucket policies to restrict access to only the CloudFront distribution.  
CloudFront가 S3 오리진에 접근 권한을 가지므로, 버킷 정책을 작성 및 업데이트하여 CloudFront 배포에만 접근을 제한할 수 있습니다.  

---

Initially, the bucket policy is empty, but after creating the distribution, it is updated to allow CloudFront to access the bucket privately.  
처음에는 버킷 정책이 비어있지만, 배포 생성 후 CloudFront가 프라이빗하게 접근할 수 있도록 업데이트됩니다.  

---

## Observing the Updated Bucket Policy  
## 업데이트된 버킷 정책 확인  

The updated bucket policy permits the CloudFront service to get objects anywhere in the bucket, but only if the request originates from the specific CloudFront distribution we created.  
업데이트된 버킷 정책은 버킷 내 모든 객체 접근을 허용하지만, 우리가 생성한 특정 CloudFront 배포에서 요청될 경우에만 허용됩니다.  

---

## Accessing Content Through CloudFront  
## CloudFront를 통한 콘텐츠 접근  

Once the distribution status changes to Deployed, we can access our files using the CloudFront domain name.  
배포 상태가 'Deployed'로 변경되면, CloudFront 도메인을 통해 파일에 접근할 수 있습니다.  

---

For example:  
예시:  

---

Accessing coffee.jpg displays the coffee image.  
`coffee.jpg` 접근 시 커피 이미지 표시  

---

Accessing beach.jpg displays the beach image.  
`beach.jpg` 접근 시 해변 이미지 표시  

---

Accessing index.html displays the full HTML page.  
`index.html` 접근 시 전체 HTML 페이지 표시  

---

All content is served through CloudFront, while the S3 bucket objects remain private.  
모든 콘텐츠는 CloudFront를 통해 제공되며, S3 버킷 객체는 여전히 비공개 상태입니다.  

---

## Benefits of Using CloudFront  
## CloudFront 사용의 장점  

CloudFront caches the files, enabling instant loading and smooth performance globally.  
CloudFront는 파일을 캐싱하여 전 세계 어디서나 빠른 로딩과 원활한 성능을 제공합니다.  

---

Even if accessed from distant locations such as Asia, latency remains low due to CloudFront's distributed edge locations.  
아시아와 같이 먼 위치에서도 CloudFront의 분산 엣지 위치 덕분에 지연 시간은 낮게 유지됩니다.  

---

## Summary  
## 요약  

We have successfully created a CloudFront distribution connected to a private S3 bucket.  
프라이빗 S3 버킷에 연결된 CloudFront 배포를 성공적으로 생성했습니다.  

---

This setup allows secure, fast, and globally distributed access to our content without making the S3 objects public.  
이 설정은 S3 객체를 공개하지 않고도 콘텐츠에 안전하고 빠르며 전 세계적으로 접근할 수 있게 합니다.  

---

The bucket policy is automatically managed to restrict access exclusively to CloudFront.  
버킷 정책은 CloudFront에만 접근을 제한하도록 자동으로 관리됩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Created an S3 bucket to store files for CloudFront distribution.  
- CloudFront 배포용 파일을 저장하기 위해 S3 버킷 생성  

- Uploaded files to the S3 bucket and explored access methods.  
- 파일을 업로드하고 접근 방법을 확인  

- Configured a CloudFront distribution with private S3 bucket access using origin access control.  
- 오리진 액세스 컨트롤을 사용해 프라이빗 S3 접근이 가능한 CloudFront 배포 구성  

- Observed how CloudFront caches content to provide fast, globally distributed access without making S3 objects public.  
- S3 객체를 공개하지 않고도 CloudFront가 캐싱을 통해 빠르고 전 세계적으로 접근 가능하게 하는 방법 확인  

🎮 **게임보상:**

* CloudFront + S3 실습 구성 이해 +10 XP
* 배포, 오리진, 캐싱 및 보안 정책 이해 +10 XP
* 프라이빗 S3 접근과 글로벌 배포 적용 이해 +10 XP
  총 **30 XP 획득!** 🎉
