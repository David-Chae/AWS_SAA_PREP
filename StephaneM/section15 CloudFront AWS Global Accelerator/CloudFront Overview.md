# CloudFront Overview  
# CloudFront 개요  

---

## Now let us talk about CloudFront.  
## 이제 CloudFront에 대해 이야기해보겠습니다.  

---

## What is CloudFront (CDN)  
## CloudFront란 무엇인가 (CDN)  

CloudFront is a content delivery network, or CDN.  
CloudFront는 콘텐츠 전송 네트워크(CDN)입니다.  

---

So anytime you see "CDN" in the exam, think CloudFront.  
시험에서 "CDN"을 보면 CloudFront를 떠올리세요.  


CDN에 대해 알기 쉽게 설명해 드릴게요! 🌐

## CDN이란 무엇인가요?

**CDN**은 **Content Delivery Network (콘텐츠 전송 네트워크)**의 약자입니다. 이름 그대로, 사용자에게 **웹 콘텐츠(데이터)**를 **더 빠르고 효율적으로** 전송하기 위해 지리적으로 분산된 여러 대의 서버(네트워크)를 연결한 시스템입니다.

쉽게 말해, 전 세계에 흩어져 있는 **'창고'**를 만들어서 사용자가 가장 가까운 창고에서 물건(데이터)을 받아볼 수 있게 하는 개념입니다.

---

## 💡 CDN은 왜 필요한가요?

CDN이 없다면, 모든 사용자의 요청은 단 하나의 **원본 서버(Origin Server)**로 집중됩니다.

1.  **지연 시간 문제 (Latency):** 한국 사용자가 미국에 있는 원본 서버의 데이터를 요청하면, 데이터가 태평양을 건너와야 하므로 **시간이 오래 걸립니다.**
2.  **부하 문제 (Overload):** 많은 사용자가 동시에 원본 서버에 접속하면, 서버에 과부하가 걸려 **웹사이트가 느려지거나 다운될 수 있습니다.**

CDN은 이 두 가지 문제를 해결해 줍니다.

---

## 🏃‍♀️ CDN은 어떻게 작동하나요?

CDN이 데이터를 빠르고 안정적으로 전달하는 핵심 원리는 **캐싱(Caching)**과 **분산 배치(Distribution)**입니다.

### 1. 전 세계에 분산된 서버 (PoP)

CDN 제공 업체는 전 세계 주요 도시에 **Edge Server** 또는 **PoP (Point of Presence) 서버**라고 불리는 분산된 서버들을 설치합니다. 이것이 바로 '창고' 역할을 하는 서버들입니다.



### 2. 가장 가까운 서버로 연결 (라우팅)

사용자가 웹사이트에 접속하여 콘텐츠(이미지, 영상, 웹페이지 등)를 요청하면, 요청은 원본 서버로 바로 가지 않고 CDN 네트워크로 향합니다.

* CDN은 사용자의 위치를 파악하여 **지리적으로 가장 가까운 Edge 서버**로 요청을 자동으로 연결해 줍니다.
* 사용자는 **가까운 Edge 서버**에서 콘텐츠를 받아보므로, 데이터가 먼 거리를 이동할 필요가 없어 **속도가 훨씬 빨라집니다.**

### 3. 데이터 저장 (캐싱)

* **Edge 서버**는 원본 서버로부터 받은 데이터를 **임시로 저장(캐싱)**해 둡니다.
* 다음 사용자가 동일한 콘텐츠를 요청하면, Edge 서버는 원본 서버에 다시 요청하지 않고, **저장해 둔 데이터**를 즉시 전송합니다.

이 과정을 통해 원본 서버의 **부하가 크게 줄어들고**, 사용자에게는 **훨씬 빠른 응답 속도**를 제공할 수 있게 됩니다.

---

## 📝 CDN의 주요 장점 요약

* **⚡️ 속도 향상:** 사용자에게 가장 가까운 서버에서 데이터를 전달하여 로딩 시간을 대폭 줄입니다.
* **🛡️ 안정성 향상:** 원본 서버의 부하를 분산시켜, 트래픽이 폭주해도 웹사이트가 다운되는 것을 방지합니다.
* **💸 비용 절감:** 원본 서버의 트래픽 처리량이 줄어들어 서버 운영 비용을 절감하는 효과도 있습니다.

결론적으로, CDN은 **넷플릭스, 유튜브** 같은 대용량 서비스부터 일반 **쇼핑몰**까지, 빠르고 안정적인 사용자 경험을 제공하기 위한 **필수 인프라**입니다.
---

It improves read performance by caching the content of your website at different edge locations.  
여러 엣지 위치에서 웹사이트 콘텐츠를 캐싱하여 읽기 성능을 향상시킵니다.  

---

Because your content is cached all around the world, your users around the world will have lower latency, and this will improve the user experience.  
콘텐츠가 전 세계에 캐시되기 때문에, 전 세계 사용자들이 더 낮은 지연 시간으로 접근할 수 있으며, 사용자 경험이 향상됩니다.  

---

## Global Presence and DDoS Protection  
## 글로벌 존재 및 DDoS 방어  

CloudFront is made of hundreds of points of presence globally, which includes edge locations and edge caches across the world.  
CloudFront는 전 세계 수백 개의 지점(엣지 위치 및 엣지 캐시)으로 구성됩니다.  

---

By having the content distributed globally, we gain protection against distributed denial-of-service (DDoS) attacks.  
콘텐츠를 전 세계에 분산하면 분산 서비스 거부(DDoS) 공격에 대한 방어를 제공합니다.  

---

A DDoS attack is a type of attack where many servers are targeted simultaneously.  
DDoS 공격은 여러 서버를 동시에 공격하는 유형의 공격입니다.  

---

CloudFront, by virtue of distributing your application worldwide, helps protect against these attacks, especially when combined with AWS Shield and the Web Application Firewall (WAF), which we will see in the security section.  
CloudFront는 애플리케이션을 전 세계에 분산함으로써 이러한 공격을 방어하며, AWS Shield 및 WAF와 결합하면 더욱 강력한 보호를 제공합니다.  

---

## Example: S3 Website in Australia and a User in America  
## 예제: 호주 S3 웹사이트와 미국 사용자  

If we created an S3 bucket and hosted a website on it in Australia, but we had a user in America, the user would request the content from an American edge location using CloudFront.  
호주에 S3 버킷을 만들고 웹사이트를 호스팅했지만 미국에 사용자가 있다면, CloudFront를 통해 미국 엣지 위치에서 콘텐츠를 요청하게 됩니다.  

---

CloudFront will fetch the content from Australia.  
CloudFront는 호주에서 콘텐츠를 가져옵니다.  

---

If another user in the US requests the same content, it will be served directly from the edge and will not go all the way to Australia to serve that content.  
미국의 다른 사용자가 동일한 콘텐츠를 요청하면, 엣지에서 바로 제공되며 호주까지 가지 않습니다.  

---

Similarly, if a user is in China, the client will talk to a Chinese point of presence, be redirected to the S3 bucket origin, and then the content will be cached at the edge.  
마찬가지로 중국 사용자는 중국 엣지 위치에서 요청하고, S3 버킷 원본으로 리디렉션된 후 콘텐츠가 엣지에 캐시됩니다.  

---

## Types of Origins  
## 오리진 타입  

CloudFront has several types of origins, which are basically the backends you want to connect CloudFront to:  
CloudFront는 여러 종류의 오리진을 지원하며, 기본적으로 CloudFront가 연결할 백엔드입니다.  

---

Amazon S3 buckets for distributing files and caching them at the edge. The connection between CloudFront and your S3 bucket is secured using an Origin Access Control (OAC).  
파일을 배포하고 엣지에서 캐싱하기 위한 Amazon S3 버킷. CloudFront와 S3 버킷 간 연결은 Origin Access Control(OAC)로 보호됩니다.  

---

VPC origins: if you have an application hosted in private subnets in a VPC, CloudFront can connect privately to an Application Load Balancer, a Network Load Balancer, or an EC2 instance.  
VPC 오리진: VPC의 프라이빗 서브넷에 호스팅된 애플리케이션이 있는 경우, CloudFront는 ALB, NLB 또는 EC2 인스턴스에 프라이빗하게 연결할 수 있습니다.  

---

Custom origins: anything that uses HTTP can be used as a backend, for example a website hosted outside of AWS. For S3 static websites, ensure the S3 bucket is enabled as a static S3 website or any public HTTP backend you want, within or outside of AWS.  
커스텀 오리진: HTTP를 사용하는 모든 것이 백엔드가 될 수 있습니다. 예: AWS 외부에 호스팅된 웹사이트. S3 정적 웹사이트의 경우 S3 버킷을 정적 웹사이트로 활성화하거나 원하는 퍼블릭 HTTP 백엔드를 사용하세요.  

---

## How CloudFront Works (High Level)  
## CloudFront 작동 방식 (개요)  

At a high level, CloudFront uses edge locations around the world and connects to your origin, which could be an S3 bucket or an HTTP server.  
개요 수준에서 CloudFront는 전 세계 엣지 위치를 사용하며, S3 버킷이나 HTTP 서버 등 오리진에 연결합니다.  

---

When a client makes an HTTP request to an edge location, the edge location checks if the requested object is in its cache.  
클라이언트가 엣지 위치에 HTTP 요청을 보내면, 엣지 위치는 객체가 캐시에 있는지 확인합니다.  

---

If it does not have the object in the cache, it will request the object from the origin.  
캐시에 객체가 없으면, 오리진에서 객체를 요청합니다.  

---

Once it retrieves the results, the edge location caches the object locally so that if another client requests the same content from the same edge location, the edge location does not need to go back to the origin.  
결과를 가져오면, 엣지 위치가 객체를 로컬에 캐시하여 동일한 콘텐츠 요청 시 오리진까지 가지 않도록 합니다.  

---

## S3 as an Origin: Private Connections and Security  
## 오리진으로서 S3: 프라이빗 연결 및 보안  

If we have S3 as an origin, your S3 bucket is the origin in a specific region, and edge locations are distributed around the world, for example in Los Angeles.  
S3를 오리진으로 사용하면, S3 버킷이 특정 리전의 오리진이 되고, 엣지 위치는 전 세계에 분포합니다. 예: 로스앤젤레스.  

---

Users accessing the Los Angeles edge location will get content directly served through that edge location.  
로스앤젤레스 엣지 위치를 접근하는 사용자는 엣지 위치를 통해 직접 콘텐츠를 받습니다.  

---

The edge location will first fetch the content from the origin S3 bucket over the private AWS network.  
엣지 위치는 먼저 프라이빗 AWS 네트워크를 통해 오리진 S3 버킷에서 콘텐츠를 가져옵니다.  

---

The S3 bucket will be secured using an Origin Access Control and by modifying the S3 bucket policy.  
S3 버킷은 OAC와 버킷 정책 수정으로 보호됩니다.  

---

The same applies for other regions; for example, users in São Paulo will be served by a São Paulo edge location through a private connection to the S3 bucket.  
다른 리전도 마찬가지입니다. 예: 상파울루 사용자는 S3 버킷과의 프라이빗 연결을 통해 상파울루 엣지 위치에서 서비스를 받습니다.  

---

Using CloudFront and edge locations, the content of an S3 bucket in one region can be distributed globally through the edge locations or points of presence.  
CloudFront와 엣지 위치를 사용하면, 하나의 리전 S3 버킷 콘텐츠를 전 세계 엣지 위치를 통해 배포할 수 있습니다.  

---

## CloudFront vs S3 Cross-Region Replication  
## CloudFront vs S3 크로스리전 복제  

A common question is: what is the difference between CloudFront and S3 Cross-Region Replication?  
흔한 질문: CloudFront와 S3 크로스리전 복제의 차이점은 무엇인가요?  

---

CloudFront uses the global edge network (about 216 points of presence) and caches files in each edge location for a period of time (for example, maybe for a day).  
CloudFront는 전 세계 엣지 네트워크(약 216개 지점)를 사용하며, 각 엣지 위치에서 일정 시간 동안 파일을 캐시합니다.  

---

This approach is ideal for static content that must be available everywhere around the world with low latency.  
이 접근법은 전 세계 어디서나 낮은 지연 시간으로 접근해야 하는 정적 콘텐츠에 적합합니다.  

---

S3 Cross-Region Replication is configured per destination region. It replicates objects to target regions in near real time and does not involve caching.  
S3 크로스리전 복제는 대상 리전별로 구성되며, 객체를 거의 실시간으로 복제하지만 캐싱은 하지 않습니다.  

---

It is typically used for read-only replicas of data across regions and is useful for dynamic content that changes frequently and needs to be available at low
```


latency in a few regions.
주로 리전 간 읽기 전용 복제본에 사용되며, 자주 변경되는 동적 콘텐츠를 몇몇 리전에서 낮은 지연으로 제공할 때 유용합니다.

---

These two mechanisms serve different purposes: CloudFront is a CDN that caches content globally, whereas S3 Cross-Region Replication replicates an entire bucket into another region without caching.
두 메커니즘은 목적이 다릅니다: CloudFront는 전 세계에 콘텐츠를 캐싱하는 CDN이고, S3 크로스리전 복제는 버킷 전체를 캐싱 없이 다른 리전으로 복제합니다.

---

## Conclusion and Next Steps

## 결론 및 다음 단계

That explains CloudFront at a high level.
이로써 CloudFront를 개요 수준에서 설명했습니다.

---

In the next lecture, we will have a practical session and see how to set up a CloudFront distribution for an S3 bucket in the AWS Console.
다음 강의에서는 실습 세션을 통해 AWS 콘솔에서 S3 버킷용 CloudFront 배포를 설정하는 방법을 알아봅니다.

---

We will see you in the next lecture.
다음 강의에서 뵙겠습니다.

---

## Key Takeaways

## 핵심 요약

CloudFront is Amazon's CDN that caches content at global edge locations to reduce latency and improve user experience.
CloudFront는 전 세계 엣지 위치에서 콘텐츠를 캐시하여 지연 시간을 줄이고 사용자 경험을 향상시키는 아마존의 CDN입니다.

---

CloudFront provides DDoS protection and integrates with AWS Shield and AWS WAF for enhanced security.
CloudFront는 DDoS 방어를 제공하며, AWS Shield 및 WAF와 통합되어 보안을 강화합니다.

---

CloudFront supports multiple origin types: Amazon S3 (with Origin Access Control), VPC origins (ALB/NLB/EC2), and any custom HTTP origin.
CloudFront는 여러 오리진 타입을 지원합니다: Amazon S3(OAC 포함), VPC 오리진(ALB/NLB/EC2), 및 모든 커스텀 HTTP 오리진.

---

CloudFront caches content at edge locations globally, which differs from S3 Cross-Region Replication that replicates buckets to specific regions without caching.
CloudFront는 콘텐츠를 전 세계 엣지 위치에 캐시하지만, S3 크로스리전 복제는 캐싱 없이 특정 리전으로 버킷을 복제한다는 점에서 다릅니다.

🎮 **게임보상:**  
- CloudFront 개념 및 CDN 이해 +10 XP  
- 글로벌 엣지 캐싱과 DDoS 방어 이해 +10 XP  
- 오리진 유형과 S3/CloudFront 차이점 이해 +10 XP  
총 **30 XP 획득!** 🎉
