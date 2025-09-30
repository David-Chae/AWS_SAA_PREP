# Routing Policy - Weighted  
# 라우팅 정책 - 가중(Weighted)  
👉 Route 53에서 가중 라우팅 정책을 이해하고 실습합니다.  

---

## Introduction to Weighted Routing Policy  
## 가중 라우팅 정책 소개  
👉 트래픽을 특정 리소스에 비율에 따라 분배 가능.  

The weighted routing policy enables controlling the percentage of requests directed to specific resources by assigning weights to them.  
가중 라우팅 정책은 리소스별 요청 비율을 제어할 수 있도록 가중치를 지정합니다.  
👉 각 리소스에 트래픽을 몇 % 보낼지 결정할 수 있습니다.  

Simply put, using Amazon Route 53, you can assign different weights to multiple EC2 instances to distribute traffic accordingly.  
쉽게 말해, 여러 EC2 인스턴스에 서로 다른 가중치를 지정하여 트래픽을 분배할 수 있습니다.  

For example, consider three EC2 instances assigned weights of 70, 20, and 10 respectively.  
예: 세 개의 EC2 인스턴스에 각각 70, 20, 10 가중치를 할당.  

In this example, these weights sum to 100, but in real scenarios, they do not need to sum to 100.  
이 예시는 합이 100이지만 실제로 합이 100일 필요는 없습니다.  

The weight indicates the proportion of DNS responses that Route 53 will direct to each instance.  
가중치는 Route 53이 각 인스턴스로 보내는 DNS 응답의 비율을 나타냅니다.  

Thus, 70% of DNS responses will redirect to the first EC2 instance, 20% to the second, and 10% to the third.  
따라서 70%는 첫 번째 인스턴스로, 20%는 두 번째, 10%는 세 번째로 전송됩니다.  

To implement this, each DNS record is assigned a relative weight.  
이를 구현하려면 각 DNS 레코드에 상대 가중치를 지정합니다.  

The traffic percentage sent to each record is calculated as the weight of that record divided by the sum of all weights of all records.  
트래픽 비율은 "해당 레코드 가중치 ÷ 전체 레코드 가중치 합"으로 계산됩니다.  

This effectively represents the percentage of total traffic each record receives.  
즉, 각 레코드가 받는 총 트래픽의 비율을 의미합니다.  

It is important to note that weights do not need to sum to 100; they simply indicate the relative amount of traffic to send to each instance compared to the others.  
가중치 합이 100일 필요는 없으며, 다른 인스턴스 대비 상대 트래픽 비율을 나타냅니다.  

For weighted routing to function correctly, all DNS records must have the same name and type.  
가중 라우팅이 정상 작동하려면 모든 레코드가 같은 이름과 타입이어야 합니다.  

Additionally, these records can be associated with health checks, although that topic will be covered separately.  
또한 헬스체크와 연결 가능하며, 이는 별도 강의에서 다룹니다.  

---

## Use Cases for Weighted Routing Policy  
## 가중 라우팅 정책 활용 사례  
👉 트래픽 분산과 테스트에 유용.  

Weighted routing is useful for several scenarios, including:  
가중 라우팅이 유용한 경우:  

- Load balancing traffic across different regions.  
- 여러 리전 간 트래픽 부하 분산.  
- Testing new application versions by sending a small portion of traffic to the new version.  
- 새 버전 테스트를 위해 일부 트래픽만 새 버전으로 전송.  
- Gradually shifting traffic away from or towards specific resources by adjusting weights.  
- 가중치 조정을 통해 특정 리소스로의 트래픽 점진적 이동.  

If a resource's weight is set to zero, no traffic will be sent to it.  
리소스 가중치를 0으로 설정하면 트래픽이 전달되지 않습니다.  

If all resource records have a weight of zero, Route 53 returns all records with equal weight.  
모든 레코드 가중치가 0이면, Route 53은 모든 레코드를 동일 가중치로 반환합니다.  

---

## Demonstration in AWS Console  
## AWS 콘솔 실습  
👉 가중 레코드 생성 및 테스트.  

Let's create weighted DNS records in the AWS Route 53 console.  
AWS 콘솔에서 가중 DNS 레코드를 생성해봅니다.  

We will create three A records with the same name but different values and weights.  
같은 이름, 다른 값과 가중치를 가진 A 레코드 3개 생성.  

The first record is named weighted.stephanetheteacher.com, with an IP address from the ap-southeast-1 region.  
첫 번째 레코드: `weighted.stephanetheteacher.com`, IP는 `ap-southeast-1`.  

We assign it a weight of 10 and set the TTL to 3 seconds for demonstration purposes.  
가중치 10, TTL 3초로 설정(실습용).  

The second record has the same name, with an IP address from the us-east-1 region.  
두 번째 레코드: 같은 이름, IP는 `us-east-1`.  

We assign it a weight of 70 and also set the TTL to 3 seconds.  
가중치 70, TTL 3초.  

The third record, again with the same name, has an IP address from the eu-central-1 region.  
세 번째 레코드: 같은 이름, IP는 `eu-central-1`.  

We assign it a weight of 20 and set the TTL to 3 seconds.  
가중치 20, TTL 3초.  

Each record also has a unique record ID to identify it within the weighted record set.  
각 레코드에는 고유 ID가 있어 가중 레코드 세트에서 식별 가능.  

After creating these records, the table shows three records, each with one value and weights of 10, 70, and 20 respectively.  
생성 후 테이블에 3개의 레코드가 표시, 각각 가중치 10, 70, 20.  

This differs from a simple record with multiple values; here, each record is distinct with its own weight.  
단순 레코드와 달리, 각 레코드는 고유 가중치를 가집니다.  

---

## Testing Weighted Routing  
## 가중 라우팅 테스트  
👉 브라우저와 dig로 트래픽 분배 확인.  

When accessing weighted.stephanetheteacher.com in a browser, the response is typically from the us-east-1 region, which has the highest weight of 70.  
브라우저 접속 시 대부분 `us-east-1`(가중치 70)에서 응답.  

Refreshing the page every three seconds may occasionally return responses from other regions, reflecting the weighted distribution.  
3초마다 새로고침 시 가끔 다른 리전에서 응답, 가중치 분포 반영.  

Using the dig command to query the DNS record confirms this behavior.  
dig 명령으로 확인 시 동일한 동작 관찰 가능.  

For example, multiple queries show responses mostly from the us-east-1 IP address, but occasionally from the eu-central-1 IP address, which has a weight of 20.  
예: 대부분 `us-east-1` IP 응답, 가끔 `eu-central-1` IP(가중치 20) 응답.  

This demonstrates that weighted routing directs most queries to the resource with the highest weight, while still distributing some traffic to other resources based on their weights.  
즉, 가중치 기반으로 대부분의 트래픽은 높은 가중치 리소스로 가고, 일부는 다른 리소스로 분산됨.  

---

## Conclusion  
## 결론  
Weighted routing policies provide a powerful way to control traffic distribution among multiple resources.  
가중 라우팅 정책은 여러 리소스 간 트래픽 분배 제어에 강력한 수단.  

By assigning weights, you can balance load, test new versions, or gradually shift traffic as needed.  
가중치로 부하 균형, 새 버전 테스트, 트래픽 점진적 이동 가능.  

This lecture demonstrated how to configure weighted routing in AWS Route 53 and verified its behavior through browser and command-line testing.  
이번 강의에서는 AWS Route 53에서 가중 라우팅 설정 및 브라우저/CLI 테스트로 검증.  

---

## Key Takeaways  
## 핵심 포인트  
Weighted routing policy allows directing a percentage of DNS requests to specific resources based on assigned weights.  
가중 라우팅 정책은 지정 가중치에 따라 DNS 요청 일부를 특정 리소스로 전달.  

Weights do not need to sum to 100; they represent relative proportions of traffic distribution.  
가중치 합 100 필요 없음, 상대 비율로 트래픽 분배.  

DNS records must share the same name and type to use weighted routing, and can be associated with health checks.  
같은 이름/타입 레코드에서만 가능하며, 헬스체크 연결 가능.  

Weighted routing is useful for load balancing across regions and testing new application versions by controlling traffic distribution.  
리전 간 부하 분산과 새 버전 테스트에 유용.  

---

💡 **게임 보상:**

* ⚖️ 가중 라우팅 설정 이해 = +50 EXP
* 🌍 브라우저/CLI 테스트 = +50 EXP
* 📊 트래픽 분배 확인 = +100 EXP
  **총 보상: 200 EXP + Weighted Routing 마스터 뱃지 🏅**
