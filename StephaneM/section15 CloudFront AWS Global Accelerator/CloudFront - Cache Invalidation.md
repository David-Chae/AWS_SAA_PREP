# CloudFront - Cache Invalidation  
# CloudFront - 캐시 무효화  

---

## Introduction to Cache Invalidation in CloudFront  
## CloudFront 캐시 무효화 소개  

CloudFront uses edge locations to cache content from a backend origin.  
CloudFront는 백엔드 오리진의 콘텐츠를 캐싱하기 위해 엣지 위치를 사용합니다.  
> 엣지 캐시는 사용자 근처에서 빠른 콘텐츠 제공을 위해 사용됩니다.  

When the backend origin is updated, CloudFront edge locations do not immediately know about these changes.  
백엔드 오리진이 업데이트되어도 CloudFront 엣지 위치는 즉시 이를 알지 못합니다.  
> 기본 캐시 동작으로 인해 업데이트가 지연될 수 있습니다.  

Instead, they serve the cached content until the cache's Time To Live (TTL) expires.  
대신 캐시된 콘텐츠를 TTL(Time To Live)이 만료될 때까지 제공합니다.  
> TTL 동안은 기존 캐시가 우선 사용됩니다.  

Only after the TTL expires will CloudFront fetch the refreshed content from the backend origin.  
TTL이 만료된 후에야 CloudFront는 백엔드 오리진에서 최신 콘텐츠를 가져옵니다.  
> 기본 동작에서는 TTL 만료 전까지 최신 내용 반영이 지연됩니다.  

---

This default behavior may be undesirable if you want new content to be served as soon as possible.  
최신 콘텐츠를 가능한 빨리 제공하고 싶다면 이 기본 동작은 바람직하지 않을 수 있습니다.  
> 콘텐츠 업데이트 지연 문제를 해결해야 합니다.  

To address this, CloudFront allows you to force a cache refresh, either for the entire cache or partially.  
이를 해결하기 위해 CloudFront는 전체 캐시 또는 일부만 강제로 새로 고칠 수 있는 기능을 제공합니다.  
> 캐시 강제 새로 고침 기능이 제공됩니다.  

This process eliminates the existing TTL in the cache and is known as a CloudFront invalidation.  
이 과정은 기존 TTL을 무시하며, 이를 CloudFront 캐시 무효화(Cache Invalidation)라고 합니다.  
> 무효화를 통해 즉시 콘텐츠 업데이트 가능.  

To perform an invalidation, you specify the file path(s) to invalidate.  
무효화를 수행하려면 무효화할 파일 경로를 지정합니다.  
> 특정 파일 또는 경로를 대상으로 캐시를 삭제할 수 있습니다.  

You can invalidate all files using a wildcard "*", or target specific paths such as /images/.  
와일드카드 "*"를 사용하여 모든 파일을 무효화하거나 /images/와 같은 특정 경로를 지정할 수 있습니다.  
> 전체 파일 또는 특정 폴더 단위로 무효화 가능.  

---

## How Cache Invalidation Works  
## 캐시 무효화 작동 방식  

Consider a CloudFront distribution with two edge locations.  
두 개의 엣지 위치가 있는 CloudFront 배포를 생각해봅시다.  
> 다중 엣지 위치에서 캐시가 어떻게 동작하는지 이해합니다.  

Each edge location maintains its own cache containing files like index.html and images fetched directly from the origin, such as an S3 bucket.  
각 엣지 위치는 S3 버킷과 같은 오리진에서 직접 가져온 index.html 및 이미지 파일을 포함한 자체 캐시를 유지합니다.  
> 각 엣지는 독립적으로 캐시를 관리합니다.  

Suppose the TTL for these files is set to one day, meaning the edge locations will re-fetch these files from the origin once every day.  
이 파일들의 TTL이 하루로 설정되어 있다고 가정하면, 엣지 위치는 하루에 한 번씩 오리진에서 파일을 다시 가져옵니다.  
> TTL에 따라 캐시 업데이트 주기가 결정됩니다.  

As an administrator, you update files in the S3 bucket, such as adding or changing images and modifying the index.html file.  
관리자는 S3 버킷에서 이미지 추가/수정, index.html 수정과 같은 업데이트를 수행합니다.  
> 업데이트된 콘텐츠를 사용자에게 바로 제공하고 싶습니다.  

You want these updates to be reflected immediately to your users through CloudFront.  
이 업데이트를 CloudFront를 통해 사용자에게 즉시 반영하고 싶습니다.  
> 캐시 무효화가 필요한 상황입니다.  

---

To achieve this, you invalidate specific paths:  
이를 위해 특정 경로를 무효화합니다:  

- `/index.html` to invalidate the specific file.  
- `/index.html`: 특정 파일 무효화  

- `/images/` to invalidate all images in the cache at the edge locations.  
- `/images/`: 엣지 위치 캐시에 있는 모든 이미지 무효화  

CloudFront then instructs the edge locations to remove these files from their caches.  
CloudFront는 엣지 위치에 이 파일들을 캐시에서 제거하도록 지시합니다.  
> TTL 만료를 기다리지 않고 즉시 캐시 삭제.  

These files are simply removed, bypassing the TTL expiration.  
이 파일들은 TTL 만료를 무시하고 단순히 제거됩니다.  
> 캐시 무효화의 핵심 기능입니다.  

On the next user request for index.html or any image, the edge location will detect that the file is no longer in its cache.  
다음에 사용자가 index.html 또는 이미지를 요청하면, 엣지 위치는 해당 파일이 더 이상 캐시에 없음을 감지합니다.  
> 새로운 요청 시 최신 콘텐츠를 가져오도록 트리거됩니다.  

It will then forward the request to the origin to fetch the updated and newer content.  
그 후 오리진에 요청을 전달하여 업데이트된 최신 콘텐츠를 가져옵니다.  
> 사용자는 TTL 만료를 기다리지 않고 최신 콘텐츠를 받습니다.  

This process ensures that users receive the most recent content without waiting for the original TTL to expire, demonstrating the value of cache invalidations in CloudFront.  
이 과정은 사용자가 TTL 만료를 기다리지 않고 최신 콘텐츠를 받도록 보장하며, 캐시 무효화의 가치를 보여줍니다.  
> 캐시 무효화는 콘텐츠 신속 제공에 핵심적입니다.  

---

## Conclusion  
## 결론  

Cache invalidation is a powerful feature in CloudFront that allows immediate propagation of content updates by removing cached files from edge locations before their TTL expires.  
캐시 무효화는 CloudFront의 강력한 기능으로, TTL 만료 전 엣지 캐시를 제거하여 콘텐츠 업데이트를 즉시 반영할 수 있습니다.  
> 최신 콘텐츠 제공을 보장하는 필수 기능입니다.  

This ensures that users always receive the latest content promptly.  
이를 통해 사용자는 항상 최신 콘텐츠를 즉시 받을 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- CloudFront caches content at edge locations with a set TTL, delaying updates from the origin.  
- CloudFront는 엣지 위치에서 TTL을 가진 캐시를 유지하며, 오리진의 업데이트가 지연될 수 있습니다.  

- Cache invalidation forces CloudFront to remove cached files before TTL expiry, enabling immediate content updates.  
- 캐시 무효화는 TTL 만료 전에 캐시된 파일을 제거하여 즉시 콘텐츠 업데이트를 가능하게 합니다.  

- Invalidation can target specific files or entire paths using wildcards.  
- 무효화는 특정 파일이나 와일드카드를 사용하여 전체 경로를 대상으로 할 수 있습니다.  

- After invalidation, edge locations fetch updated content from the origin upon the next user request.  
- 무효화 후, 엣지 위치는 다음 사용자 요청 시 오리진에서 최신 콘텐츠를 가져옵니다.  

🎮 **게임보상:**

* CloudFront 캐시 무효화 이해 +10 XP
* TTL과 무효화 차이 이해 +10 XP
* 특정 파일/경로 무효화 개념 이해 +10 XP
  총 **30 XP 획득!** 🎉
