# S3 Website Hands On  
# S3 웹사이트 실습  

---

## Enabling Static Website Hosting on S3 Bucket  
## S3 버킷에서 정적 웹사이트 호스팅 활성화  

First, we will enable our bucket to function as a website.  
먼저, 버킷이 웹사이트로 작동하도록 활성화할 예정.  
👉 설명: 정적 웹사이트를 위해 버킷 설정 시작.  

Before that, I am going to upload one more file, specifically my beach.jpg file, into our bucket.  
그 전에 beach.jpg 파일을 버킷에 업로드할 예정.  
👉 설명: 웹사이트에 사용할 이미지 추가.  

The upload is complete, so now we have two files in our bucket.  
업로드가 완료되어 현재 버킷에는 두 개의 파일이 있음.  
👉 설명: 현재 버킷 상태 확인.  

Next, navigate to the Properties tab and scroll down all the way to find the Static website hosting section.  
다음으로 Properties 탭으로 이동 후 정적 웹사이트 호스팅 섹션까지 스크롤.  
👉 설명: 웹사이트 호스팅 옵션 위치 확인.  

Click on Edit, and here we will enable static website hosting.  
Edit를 클릭하여 정적 웹사이트 호스팅 활성화.  
👉 설명: 웹사이트 호스팅 기능 켜기.  

We want to host a static website and need to specify an index document.  
정적 웹사이트를 호스팅하려면 인덱스 문서 지정 필요.  
👉 설명: 홈페이지 역할 파일 지정 필요.  

I will specify index.html as the index document.  
index 문서로 index.html 파일 지정.  
👉 설명: 기본 홈페이지 파일 설정.  

This file will serve as the default or homepage of the website.  
이 파일이 웹사이트의 기본 페이지 또는 홈페이지 역할 수행.  
👉 설명: 웹사이트 시작 페이지 정의.  

There is a warning indicating that to enable this as a website endpoint, all your content must be publicly readable.  
웹사이트 엔드포인트로 활성화하려면 모든 콘텐츠가 공개적으로 읽을 수 있어야 한다는 경고 표시.  
👉 설명: 공개 읽기 권한 필수.  

We have already configured this in the previous lecture, so that requirement is met.  
이전 강의에서 이미 설정했으므로 요구사항 충족.  
👉 설명: 공용 권한 확인 완료.  

After setting this, click Save.  
설정 후 Save 클릭.  
👉 설명: 설정 저장.  

After saving, go back to the Objects tab.  
저장 후 Objects 탭으로 돌아가기.  
👉 설명: 파일 업로드 확인.  

One thing missing here is the index.html file.  
여기에서 누락된 파일은 index.html.  
👉 설명: 홈페이지 파일 업로드 필요.  

Let's upload this file now by clicking Add files, selecting index.html, and then clicking Upload.  
Add files 클릭 후 index.html 선택, Upload 클릭하여 업로드.  
👉 설명: 홈페이지 파일 업로드 수행.  

Once uploaded, close the upload dialog.  
업로드가 완료되면 업로드 다이얼로그 닫기.  
👉 설명: 업로드 완료 후 인터페이스 종료.  

Now, return to the Properties tab and scroll down to the Static website hosting section.  
이제 Properties 탭으로 돌아가 정적 웹사이트 호스팅 섹션으로 스크롤.  
👉 설명: 웹사이트 엔드포인트 URL 확인 준비.  

You will see the Bucket website endpoint URL displayed.  
버킷 웹사이트 엔드포인트 URL이 표시됨.  
👉 설명: 웹사이트 접속 URL 확인.  

Copy this URL and paste it into your browser.  
이 URL을 복사하여 브라우저에 붙여넣기.  
👉 설명: 실제 웹사이트 접근 확인.  

The website loads, displaying the text "I love coffee. Hello world!" along with the coffee.jpg image.  
웹사이트가 로드되어 "I love coffee. Hello world!" 텍스트와 coffee.jpg 이미지 표시.  
👉 설명: 홈페이지와 이미지 정상 표시 확인.  

This confirms that the index.html file is working correctly.  
index.html 파일이 정상적으로 작동함을 확인.  
👉 설명: 홈페이지 기능 검증 완료.  

If you right-click on the image and open it in a new tab, you will see the public URL of the coffee.jpg file.  
이미지를 우클릭 후 새 탭에서 열면 coffee.jpg 파일의 공개 URL 확인 가능.  
👉 설명: 이미지 공개 접근 확인.  

This confirms that the image is publicly accessible.  
이미지가 공개적으로 접근 가능함을 확인.  
👉 설명: 공개 권한 정상 확인.  

Additionally, if you want to change the coffee image to the beach image, you can navigate to beach.jpg in the bucket and view it.  
추가로 coffee 이미지를 beach 이미지로 변경하려면 bucket 내 beach.jpg 파일로 이동하여 확인 가능.  
👉 설명: 다른 이미지 접근 테스트 가능.  

This confirms that the beach image is also accessible.  
beach 이미지도 접근 가능함을 확인.  
👉 설명: 여러 파일 공개 접근 검증.  

In summary, our S3 bucket is enabled for static website hosting, and thanks to the bucket policy being public, all these files are accessible.  
요약하면, S3 버킷이 정적 웹사이트 호스팅 활성화 상태이며, 버킷 정책이 공개 설정되어 있어 모든 파일 접근 가능.  
👉 설명: 전체 웹사이트 구성 및 접근 정상 확인.  

Everything is working as expected.  
모든 것이 예상대로 작동함.  
👉 설명: 실습 성공.  

I hope you found this lecture helpful. See you in the next lecture.  
이번 강의가 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  
👉 설명: 강의 마무리.  

---

## Key Takeaways  
## 핵심 요약  

- Enabled static website hosting on an S3 bucket by configuring the index document.  
- 인덱스 문서를 설정하여 S3 버킷에서 정적 웹사이트 호스팅 활성화.  

- Uploaded necessary files including HTML and image files to the S3 bucket.  
- HTML 및 이미지 파일 등 필요한 파일을 S3 버킷에 업로드.  

- Ensured the bucket policy allowed public read access for website content.  
- 버킷 정책이 웹사이트 콘텐츠에 대해 공개 읽기 권한을 허용하도록 확인.  

- Verified the website endpoint URL to confirm the static website is live and accessible.  
- 웹사이트 엔드포인트 URL을 확인하여 정적 웹사이트가 정상적으로 작동하는지 검증.  

---

🎮 **게임보상:**

* **“S3 웹사이트 실습 완료!”**

  * 정적 웹사이트 호스팅 설정 +25
  * HTML과 이미지 업로드 +25
  * 공개 접근 권한 검증 +25
  * 웹사이트 엔드포인트 확인 +25

총 **100 XP 획득!** 🎉
