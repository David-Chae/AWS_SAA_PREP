# Routing Policy - Multi Value  
# 라우팅 정책 - 멀티 값  

## Multi-Value Routing Policy  
## 멀티 값 라우팅 정책  

Let's discuss the last routing policy, which is Multi-Value.  
마지막 라우팅 정책인 멀티 값 라우팅에 대해 살펴보겠습니다.  

This policy is used when you want to route traffic to multiple resources.  
이 정책은 트래픽을 여러 리소스로 라우팅하고 싶을 때 사용됩니다.  

Route 53 will therefore return multiple values or resources.  
따라서 Route 53은 여러 값이나 리소스를 반환합니다.  

You can associate these resources with Health Checks.  
이 리소스들은 헬스 체크와 연동할 수 있습니다.  

Therefore, only the resources that are associated with a healthy Health Check will be returned via the Multi-Value policy.  
따라서 멀티 값 정책을 통해 반환되는 리소스는 헬스 체크가 정상인 리소스만 반환됩니다.  

Up to eight healthy records are returned for each Multi-Value query.  
각 멀티 값 쿼리마다 최대 8개의 정상 레코드가 반환됩니다.  

Although it looks like an Elastic Load Balancer (ELB), Multi-Value routing is not a substitute for having an ELB.  
비록 ELB처럼 보이지만, 멀티 값 라우팅은 ELB를 대체하지는 않습니다.  

The idea is that it provides client-side load balancing.  
멀티 값 라우팅의 핵심은 클라이언트 측 로드 밸런싱을 제공한다는 것입니다.  

---

## Example Setup  
## 예시 설정  

We will set up multiple A Records for our example.com domain and associate them with Health Checks.  
example.com 도메인에 대해 여러 A 레코드를 설정하고 헬스 체크와 연동해 보겠습니다.  

When a Multi-Value query is performed by clients, they will receive up to eight records back.  
클라이언트가 멀티 값 쿼리를 수행하면 최대 8개의 레코드를 받을 수 있습니다.  

The clients will then choose one of them.  
클라이언트는 그 중 하나를 선택하게 됩니다.  

By combining this with Health Checks, we ensure that one of the up to eight records returned is healthy, allowing clients to have very safe queries.  
헬스 체크와 결합하면 반환된 8개의 레코드 중 적어도 하나가 정상임을 보장하여 안전한 쿼리를 가능하게 합니다.  

This differs from simple routing with multiple values because simple routing does not allow Health Checks.  
단순 멀티 값 라우팅과 다른 점은 단순 라우팅은 헬스 체크를 지원하지 않는다는 것입니다.  

Therefore, it is possible that one of the resources returned in a simple routing query will be unhealthy.  
따라서 단순 라우팅에서 반환된 리소스 중 하나가 비정상일 가능성이 있습니다.  

This is why Multi-Value routing is more powerful as a type of record.  
이 때문에 멀티 값 라우팅은 더 강력한 레코드 유형으로 볼 수 있습니다.  

---

## Creating Multi-Value Records in the UI  
## UI에서 멀티 값 레코드 생성  

Let's practice creating Multi-Value records.  
멀티 값 레코드를 생성하는 실습을 해보겠습니다.  

First, create a record named multi pointing to the us-east-1 region.  
먼저, 이름을 `multi`로 지정하고 us-east-1 리전을 가리키는 레코드를 생성합니다.  

Set the Routing policy to Multi-Value, associate it with the us-east-1 Health Check, set the Record ID to US, and the TTL to 60 seconds.  
라우팅 정책을 멀티 값으로 설정하고, us-east-1 헬스 체크와 연동하며, 레코드 ID를 `US`로, TTL은 60초로 설정합니다.  

Next, add another record named multi routing to the ap-southeast-1 region.  
다음으로, 이름을 `multi`로 하고 ap-southeast-1 리전을 가리키는 레코드를 추가합니다.  

Set the Routing policy to Multi-Value, associate it with the ap-southeast-1 Health Check, set the Record ID to Asia, and the TTL to 60 seconds.  
라우팅 정책을 멀티 값으로 설정하고, ap-southeast-1 헬스 체크와 연동하며, 레코드 ID를 `Asia`로, TTL을 60초로 설정합니다.  

Finally, add a third record named multi pointing to the eu-central-1 region.  
마지막으로, 이름을 `multi`로 하고 eu-central-1 리전을 가리키는 세 번째 레코드를 추가합니다.  

Set the Routing policy to Multi-Value, associate it with the eu-central-1 Health Check, set the Record ID to EU, and the TTL to 60 seconds.  
라우팅 정책을 멀티 값으로 설정하고, eu-central-1 헬스 체크와 연동하며, 레코드 ID를 `EU`로, TTL을 60초로 설정합니다.  

After creating these records, they will be successfully added to the hosted zone.  
이 레코드들을 생성하면 호스티드 존에 성공적으로 추가됩니다.  

---

## Testing Multi-Value Records  
## 멀티 값 레코드 테스트  

To test the records, use CloudShell.  
레코드를 테스트하려면 CloudShell을 사용합니다.  

Perform a dig command on the multi-value record.  
멀티 값 레코드에 대해 dig 명령을 수행합니다.  

You should receive three answers corresponding to the three healthy IP addresses because all three Health Checks are currently healthy.  
현재 세 헬스 체크가 모두 정상이라면, 세 개의 정상 IP 주소가 반환됩니다.  

If you make one of the Health Checks unhealthy, for example, by inverting the health status of the eu-central-1 Health Check, the dig command will return only two values instead of three.  
헬스 체크 중 하나를 비정상으로 만들면, 예를 들어 eu-central-1 헬스 체크 상태를 반전시키면 dig 명령은 두 개의 값만 반환합니다.  

This demonstrates that the Multi-Value routing policy correctly returns only healthy records.  
이는 멀티 값 라우팅 정책이 정상 레코드만 반환함을 보여줍니다.  

To revert, edit the Health Check again and untick the invert health check status to restore it to healthy.  
복구하려면 헬스 체크를 다시 편집하고 반전 상태를 해제하여 정상으로 복원합니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on Multi-Value routing policy.  
이로써 멀티 값 라우팅 정책 강의를 마칩니다.  

I hope you found it informative, and I will see you in the next lecture.  
유익했길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 포인트  

- Multi-Value routing policy allows routing traffic to multiple resources simultaneously.  
  멀티 값 라우팅 정책은 트래픽을 동시에 여러 리소스로 라우팅할 수 있습니다.  

- Only healthy resources associated with Health Checks are returned, up to eight records per query.  
  헬스 체크와 연동된 정상 리소스만 반환되며, 쿼리당 최대 8개의 레코드가 반환됩니다.  

- Multi-Value routing provides client-side load balancing but is not a substitute for an ELB.  
  멀티 값 라우팅은 클라이언트 측 로드 밸런싱을 제공하지만 ELB를 대체하지는 않습니다.  

- Health Checks ensure that only healthy records are returned, unlike simple routing which does not support Health Checks.  
  헬스 체크를 통해 정상 레코드만 반환되며, 단순 라우팅과 달리 헬스 체크를 지원하지 않습니다.  

---

💡 **게임 보상:**

* 🌐 멀티 값 라우팅 개념 학습 = +40 EXP
* ⚡ 헬스 체크와 연동된 안전한 레코드 반환 이해 = +60 EXP
* 🖥️ CloudShell dig 테스트 실습 = +50 EXP
  **총 보상: 150 EXP + Multi-Value Routing Master 뱃지 🏅**
