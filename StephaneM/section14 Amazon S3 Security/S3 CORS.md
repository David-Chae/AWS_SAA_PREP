# S3 CORS  
# S3 CORS  

---

## Introduction to CORS  
## CORS 소개  

CORS stands for Cross-Origin Resource Sharing. It is an important concept to understand, especially for exam purposes, as it often appears as a question. In this article, we will explore how CORS works in depth to facilitate easy understanding and answering of related questions.  
CORS는 Cross-Origin Resource Sharing(교차 출처 리소스 공유)을 의미합니다. 시험에서도 자주 출제되므로 이해가 중요한 개념입니다. 이 글에서는 CORS가 어떻게 작동하는지 깊이 있게 살펴보고 관련 문제를 쉽게 이해하고 답할 수 있도록 설명합니다.  

---

## Understanding Origin  
## 출처(Origin) 이해하기  

An origin is defined by a scheme (protocol), host (domain), and port. For example, consider the URL https://www.example.com. Here, the implied port is 443 for HTTPS, the protocol is HTTPS itself, and the domain is www.example.com.  
출처(origin)는 스킴(프로토콜), 호스트(도메인), 포트로 정의됩니다. 예를 들어, https://www.example.com URL을 보면 HTTPS의 기본 포트는 443이며, 프로토콜은 HTTPS, 도메인은 www.example.com입니다.  

---

## What is CORS?  
## CORS란 무엇인가?  

CORS is a web browser-based security mechanism that allows or denies requests to other origins while visiting the main origin. It controls cross-origin HTTP requests initiated from scripts running in the browser.  
CORS는 웹 브라우저 기반 보안 메커니즘으로, 사용자가 방문한 주 출처에서 다른 출처로의 요청을 허용하거나 거부합니다. 브라우저에서 실행되는 스크립트가 시작한 교차 출처 HTTP 요청을 제어합니다.  

---

## Same Origin Policy  
## 동일 출처 정책  

Two URLs share the same origin if they have the same scheme, host, and port. For example, these two URLs share the same origin. However, origins can differ, such as www.example.com and other.example.com.  
두 URL은 스킴, 호스트, 포트가 동일하면 동일 출처를 공유합니다. 예를 들어, 두 URL이 동일 출처를 공유할 수 있습니다. 그러나 www.example.com과 other.example.com처럼 출처가 다를 수 있습니다.  

---

## Cross-Origin Requests  
## 교차 출처 요청  

When a web browser visits one website and attempts to make a request to another website (a different origin), these requests will not be fulfilled unless the other origin explicitly allows the request using CORS headers. These headers are called Access-Control-Allow-Origin headers.  
웹 브라우저가 한 웹사이트를 방문하면서 다른 웹사이트(다른 출처)에 요청을 시도할 때, 다른 출처가 CORS 헤더를 통해 명시적으로 요청을 허용하지 않으면 요청이 수행되지 않습니다. 이러한 헤더를 Access-Control-Allow-Origin 헤더라고 합니다.  

---

## How CORS Works: Diagram Explanation  
## CORS 작동 방식: 다이어그램 설명  

Consider a web server at the origin https://www.example.com and a web browser. There is also a second web server at a cross-origin, for example, www.other.com.  
https://www.example.com 출처에 있는 웹 서버와 웹 브라우저를 고려해보겠습니다. 또한 www.other.com과 같은 교차 출처에 두 번째 웹 서버가 있습니다.  

The web browser makes an HTTPS request to the first origin web server. As part of the response, the HTML file retrieved instructs the browser to also get some images from the other web server.  
웹 브라우저가 첫 번째 출처의 웹 서버에 HTTPS 요청을 보냅니다. 응답의 일부로 가져온 HTML 파일이 브라우저에게 다른 웹 서버에서 일부 이미지를 가져오도록 지시합니다.  

Because of built-in browser security, the browser first performs a pre-flight OPTIONS request to the cross-origin server. It asks for the allowed HTTP methods and includes the origin of the request, which is https://www.example.com.  
브라우저 내장 보안 때문에 브라우저는 먼저 교차 출처 서버에 pre-flight OPTIONS 요청을 수행합니다. 허용되는 HTTP 메서드를 요청하고 요청의 출처인 https://www.example.com을 포함합니다.  

If the cross-origin web server is configured to use Cross-Origin Resource Sharing, it responds with headers indicating it allows the origin example.com for specific methods such as GET, PUT, and DELETE.  
교차 출처 웹 서버가 CORS를 사용하도록 구성되어 있으면, 특정 메서드(GET, PUT, DELETE 등)에 대해 example.com 출처를 허용한다는 헤더를 응답으로 보냅니다.  

If the browser accepts these CORS headers, it proceeds to make the actual request to the other server to retrieve the files.  
브라우저가 이러한 CORS 헤더를 수락하면, 다른 서버에 실제 요청을 보내 파일을 가져옵니다.  

---

## Applying CORS to Amazon S3  
## Amazon S3에 CORS 적용  

When a client makes a cross-origin request to an Amazon S3 bucket, the bucket must have the correct CORS headers enabled to allow the request. This is a common exam question.  
클라이언트가 Amazon S3 버킷에 교차 출처 요청을 보낼 때, 버킷에 요청을 허용할 수 있는 올바른 CORS 헤더가 활성화되어 있어야 합니다. 이는 시험에서 자주 출제되는 질문입니다.  

One way to quickly enable this is to allow a specific origin or to allow all origins by using a wildcard.  
이를 빠르게 활성화하는 한 가지 방법은 특정 출처를 허용하거나 와일드카드를 사용해 모든 출처를 허용하는 것입니다.  

For example, consider a web browser accessing an S3 bucket configured as a static website. The bucket serves an index.html file. Within this file, there is an image that resides in another S3 bucket, also configured as a static website.  
예를 들어, 웹 브라우저가 정적 웹사이트로 구성된 S3 버킷에 접근한다고 가정합니다. 버킷은 index.html 파일을 제공합니다. 이 파일 내에는 다른 S3 버킷(정적 웹사이트로 구성됨)에 있는 이미지가 포함되어 있습니다.  

When the browser tries to load the image from the second bucket, it sends a request with the origin of the first bucket. If the second bucket is not configured with the correct CORS headers, it will refuse the request. If it allows the request, it sends the appropriate headers, and the browser successfully retrieves the image.  
브라우저가 두 번째 버킷에서 이미지를 로드하려고 시도할 때, 첫 번째 버킷의 출처(origin)를 포함하여 요청을 보냅니다. 두 번째 버킷이 올바른 CORS 헤더로 구성되지 않았다면 요청이 거부됩니다. 요청을 허용하면 적절한 헤더를 전송하여 브라우저가 이미지를 성공적으로 가져옵니다.  

---

## Summary  
## 요약  

CORS is a web browser security feature that enables or restricts the retrieval of assets such as images or files from one origin when the request originates from another origin. Proper configuration of CORS headers is essential for cross-origin resource sharing, especially in services like Amazon S3.  
CORS는 웹 브라우저 보안 기능으로, 요청이 다른 출처(origin)에서 시작될 때 이미지나 파일과 같은 자산의 가져오기를 허용하거나 제한합니다. Amazon S3와 같은 서비스에서는 CORS 헤더를 올바르게 구성하는 것이 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- CORS stands for Cross-Origin Resource Sharing, a browser security mechanism controlling requests between different origins.  
- CORS는 Cross-Origin Resource Sharing의 약자로, 서로 다른 출처 간 요청을 제어하는 브라우저 보안 메커니즘입니다.  

- The origin consists of the scheme, host, domain, and port; requests between different origins require explicit permission via CORS headers.  
- 출처(origin)는 스킴, 호스트, 도메인, 포트로 구성되며, 서로 다른 출처 간 요청은 CORS 헤더를 통해 명시적 허가가 필요합니다.  

- Browsers perform a pre-flight OPTIONS request to check if cross-origin requests are allowed by the server.  
- 브라우저는 교차 출처 요청이 서버에서 허용되는지 확인하기 위해 pre-flight OPTIONS 요청을 수행합니다.  

- In Amazon S3, enabling correct CORS headers on buckets allows cross-origin requests, such as loading images from a different S3 bucket.  
- Amazon S3에서는 버킷에 올바른 CORS 헤더를 활성화하면 다른 S3 버킷에서 이미지를 로드하는 등 교차 출처 요청이 허용됩니다.  

🎮 **게임보상:**

* CORS 개념 이해 +5 XP
* Same Origin Policy 이해 +5 XP
* 브라우저 Pre-flight 요청 이해 +5 XP
* Amazon S3에서 CORS 적용 이해 +5 XP
  총 **20 XP 획득!** 🎉
