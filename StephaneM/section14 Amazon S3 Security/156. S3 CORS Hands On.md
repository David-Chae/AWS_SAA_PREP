# S3 CORS Hands On  
# S3 CORS 실습  

---

## Introduction to CORS Practice  
## CORS 실습 소개  

Let's practice using CORS. To begin, we must first modify the index.html file. Upon opening it, you will notice that a certain part has been commented out. This section is intended to demonstrate CORS functionality.  
CORS 사용을 실습해보겠습니다. 먼저 index.html 파일을 수정해야 합니다. 파일을 열면 특정 부분이 주석 처리되어 있는 것을 볼 수 있습니다. 이 부분은 CORS 기능을 시연하기 위한 것입니다.  

To enable CORS, go to line 13 in the index.html file and remove the initial comment characters before the <div> tag. Similarly, after the <script> tag, remove the closing comment markers -- and -->. This will activate the CORS demonstration.  
CORS를 활성화하려면 index.html 파일의 13번째 줄로 이동하여 <div> 태그 앞의 주석 문자를 제거합니다. 마찬가지로 <script> 태그 뒤의 종료 주석 --와 -->도 제거합니다. 이렇게 하면 CORS 시연이 활성화됩니다.  

Once enabled, the first webpage will display "Hello world, I love coffee" along with a coffee image. Additionally, a script will fetch an extra HTML page and display its content below. This extra HTML page contains the message: "This extra page has been successfully loaded."  
활성화되면 첫 번째 웹페이지에 "Hello world, I love coffee"와 커피 이미지가 표시됩니다. 추가로, 스크립트가 다른 HTML 페이지를 가져와 아래에 내용을 표시합니다. 이 추가 페이지에는 "This extra page has been successfully loaded."라는 메시지가 포함되어 있습니다.  

Next, we will upload two files to our S3 bucket: extra-page.html and index.html. After uploading, you can access the bucket's endpoint URL to verify the content. The page should show the coffee message and image, followed by the extra page message, confirming that the fetch request worked within the same origin since both files reside in the same bucket.  
다음으로 두 개의 파일(extra-page.html, index.html)을 S3 버킷에 업로드합니다. 업로드 후 버킷의 엔드포인트 URL에 접속하여 내용을 확인할 수 있습니다. 페이지에는 커피 메시지와 이미지가 표시되고, 이어서 추가 페이지 메시지가 나와야 합니다. 이는 두 파일이 동일 버킷에 있으므로 동일 출처 내에서 fetch 요청이 성공했음을 확인합니다.  

---

## Demonstrating CORS with a Different Origin  
## 다른 출처에서 CORS 시연  

To demonstrate CORS, we need to create another S3 bucket in a different region to simulate a different origin. Let's create a bucket named demo-other-origin-stephane in the Canada region. We will unblock all public access to make this bucket publicly accessible.  
CORS를 시연하기 위해 다른 출처를 시뮬레이션하려면 다른 리전에서 새 S3 버킷을 생성해야 합니다. Canada 리전에 demo-other-origin-stephane라는 버킷을 생성하고, 모든 공개 접근을 허용하여 누구나 접근할 수 있도록 합니다.  

After creating the bucket, enable static website hosting under the Properties tab. Set the index document to index.html even if it does not exist, as this is sufficient for hosting purposes.  
버킷 생성 후 Properties 탭에서 정적 웹사이트 호스팅을 활성화합니다. 인덱스 문서를 index.html로 설정합니다. 파일이 실제로 없어도 호스팅 목적에는 충분합니다.  

Next, configure the bucket policy to make the bucket public. Under the Permissions tab, edit the bucket policy by copying a previously used policy and updating the bucket ARN to match this new bucket. Save the changes to apply the public access policy.  
다음으로 버킷 정책을 구성하여 버킷을 공개합니다. Permissions 탭에서 이전에 사용한 정책을 복사하여 새로운 버킷 ARN에 맞게 수정하고 저장합니다. 이렇게 하면 공개 접근 정책이 적용됩니다.  

Upload the extra-page.html file to this new bucket. Once uploaded, verify that the file is publicly accessible by opening its Object URL. You should see the message "This extra page has been loaded," confirming public access.  
extra-page.html 파일을 새 버킷에 업로드합니다. 업로드 후 Object URL을 열어 공개 접근이 가능한지 확인합니다. "This extra page has been loaded" 메시지가 표시되면 공개 접근이 확인된 것입니다.  

Remove the extra-page.html file from the original bucket since it is now hosted in the new bucket. Modify the index.html file in the original bucket to fetch the extra-page.html from the new bucket's URL instead of the local one. This change will trigger a cross-origin resource sharing request.  
이제 새 버킷에 호스팅되므로 기존 버킷에서 extra-page.html 파일을 삭제합니다. 기존 버킷의 index.html 파일을 수정하여 extra-page.html을 새 버킷 URL에서 가져오도록 변경합니다. 이 변경으로 교차 출처 요청이 발생합니다.  

Upload the updated index.html file back to the original bucket, overwriting the existing file. Then, open the original bucket's website URL to load the updated page.  
수정된 index.html 파일을 기존 버킷에 다시 업로드하여 기존 파일을 덮어씁니다. 그런 다음 기존 버킷의 웹사이트 URL을 열어 업데이트된 페이지를 확인합니다.  

---

## Observing CORS Errors and Fixing Them  
## CORS 오류 관찰 및 수정  

Open the browser's developer tools (also known as Chrome Developer Tools) and refresh the page. Although no visible error appears on the page, the console log shows a warning indicating that the cross-origin request was blocked due to missing CORS headers, specifically the Access-Control-Allow header.  
브라우저 개발자 도구(Chrome Developer Tools)를 열고 페이지를 새로고침합니다. 페이지에는 오류가 표시되지 않지만, 콘솔 로그에 CORS 헤더(특히 Access-Control-Allow 헤더)가 없어서 교차 출처 요청이 차단되었다는 경고가 나타납니다.  

This error occurs because the new bucket is not yet configured to allow cross-origin requests from the original bucket. To fix this, navigate to the new bucket's Permissions tab and edit the CORS configuration, which is defined in JSON format.  
이 오류는 새 버킷이 아직 기존 버킷에서 오는 교차 출처 요청을 허용하도록 구성되지 않았기 때문입니다. 수정하려면 새 버킷의 Permissions 탭으로 이동하여 JSON 형식으로 정의된 CORS 구성을 편집합니다.  

Paste the appropriate CORS JSON configuration into the editor. In the AllowedOrigins field, specify the URL of the original bucket without a trailing slash. Save the changes to apply the CORS policy, allowing the new bucket to accept requests from the original bucket's origin.  
적절한 CORS JSON 구성을 편집기에 붙여넣습니다. AllowedOrigins 필드에 기존 버킷의 URL을 슬래시 없이 입력합니다. 변경 사항을 저장하면 새 버킷이 기존 버킷 출처에서 오는 요청을 허용하도록 CORS 정책이 적용됩니다.  

Refresh the original webpage again. This time, the extra page loads successfully without any errors. Inspecting the network tab in the developer tools reveals response headers such as Access-Control-Allow-Methods: GET and Access-Control-Allow-Origin set to the original bucket's URL, confirming that the CORS policy is correctly applied.  
기존 웹페이지를 다시 새로고침합니다. 이번에는 추가 페이지가 오류 없이 성공적으로 로드됩니다. 개발자 도구의 Network 탭을 확인하면 Access-Control-Allow-Methods: GET, Access-Control-Allow-Origin 등 응답 헤더가 기존 버킷 URL로 설정되어 있어 CORS 정책이 올바르게 적용되었음을 확인할 수 있습니다.  

---

## Conclusion  
## 결론  

While the CORS configuration details may seem advanced, understanding this process is essential for handling cross-origin requests. This demonstration provides practical insight into how CORS works, which can help in answering related questions at a conceptual level during exams or real-world scenarios.  
CORS 구성 세부 사항이 복잡해 보일 수 있지만, 교차 출처 요청을 처리하려면 이 과정을 이해하는 것이 중요합니다. 이 실습은 CORS 작동 방식을 실제로 경험하게 해주며, 시험이나 실무에서 개념적 수준의 질문을 이해하는 데 도움을 줍니다.  

---

## Key Takeaways  
## 핵심 요약  

- Demonstrated how to enable CORS by modifying the index.html file.  
- index.html 파일을 수정하여 CORS를 활성화하는 방법을 시연했습니다.  

- Showcased uploading files to S3 buckets and configuring them as static websites.  
- S3 버킷에 파일을 업로드하고 정적 웹사이트로 구성하는 과정을 보여주었습니다.  

- Explained the process of setting bucket policies and CORS configurations to allow cross-origin requests.  
- 교차 출처 요청을 허용하기 위한 버킷 정책과 CORS 구성 설정 과정을 설명했습니다.  

- Illustrated how to verify CORS functionality using browser developer tools and network inspection.  
- 브라우저 개발자 도구와 네트워크 검사 기능을 사용하여 CORS 기능을 확인하는 방법을 보여주었습니다.  

🎮 **게임보상:**

* index.html 수정으로 CORS 실습 +5 XP
* 다른 S3 버킷으로 교차 출처 요청 실습 +5 XP
* CORS 오류 관찰 및 수정 이해 +5 XP
* 브라우저 개발자 도구 활용 확인 +5 XP
  총 **20 XP 획득!** 🎉
