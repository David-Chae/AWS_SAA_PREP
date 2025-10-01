# CloudFront - Price Classes  
# CloudFront - 가격 클래스  

---

Let's explore some advanced options for CloudFront that can appear in the exam. We will focus on pricing and price classes.  
시험에 나올 수 있는 CloudFront의 고급 옵션을 살펴보겠습니다. 이번에는 요금과 가격 클래스에 집중합니다.  
> CloudFront의 비용 구조와 가격 클래스 설정이 시험에 자주 등장합니다.  

---

CloudFront edge locations are distributed worldwide. Because of this global distribution, the cost of data transfer out per edge location varies based on geographic region.  
CloudFront 엣지 위치는 전 세계에 분포되어 있습니다. 이러한 글로벌 분포 때문에, 엣지 위치별 데이터 전송 비용은 지역에 따라 다릅니다.  
> 지역별 전송 비용 차이를 이해하는 것이 중요합니다.  

---

Here is a table illustrating the pricing differences by continent or geographic region of the edge location.  
다음은 엣지 위치의 대륙 또는 지역별 가격 차이를 보여주는 표입니다.  
> 대륙별, 지역별 데이터 전송 요금 차이를 한눈에 확인할 수 있습니다.  

---

For example, in Mexico, the United States, and Canada, the first 10 terabytes of data transfer costs $0.085 per gigabyte.  
예를 들어, 멕시코, 미국, 캐나다에서 처음 10TB 데이터 전송 비용은 기가바이트당 $0.085입니다.  
> 북미 지역의 초기 전송 요금 예시입니다.  

---

In contrast, an edge location in India costs approximately twice as much at $0.17 per gigabyte of data transferred.  
반면, 인도의 엣지 위치는 기가바이트당 약 $0.17로 두 배 정도 비쌉니다.  
> 지역에 따라 요금이 크게 달라짐을 보여줍니다.  

---

Moreover, the more data transferred out of CloudFront, the lower the cost per gigabyte.  
게다가 CloudFront에서 더 많은 데이터를 전송할수록 기가바이트당 비용은 낮아집니다.  
> 대량 사용 시 할인 효과가 적용됩니다.  

---

For instance, if you transfer over five petabytes of data out of CloudFront in the United States, the cost drops to $0.02 per gigabyte.  
예를 들어, 미국에서 CloudFront를 통해 5페타바이트 이상 데이터를 전송하면 기가바이트당 $0.02로 비용이 떨어집니다.  
> 데이터 전송량이 많을수록 단가가 크게 낮아지는 구조입니다.  

---

From left to right in the pricing table, the cost increases based on region. This leads us to the concept of price classes in CloudFront.  
가격표에서 왼쪽에서 오른쪽으로 갈수록 지역별 비용이 증가합니다. 이것이 CloudFront 가격 클래스 개념으로 이어집니다.  
> 가격 클래스는 비용과 성능의 균형을 위해 엣지 위치를 선택하는 기능입니다.  

---

You have the option to reduce the number of edge locations used by your CloudFront distribution to lower costs.  
CloudFront 배포에서 사용되는 엣지 위치 수를 줄여 비용을 절감할 수 있는 옵션이 있습니다.  
> 가격 클래스 설정을 통해 비용 최적화가 가능합니다.  

---

There are three price classes available:  
세 가지 가격 클래스가 있습니다:  

- Price Class All: Includes all regions, providing the best performance but at a higher cost.  
- 가격 클래스 All: 모든 지역 포함, 최고 성능 제공하지만 비용이 높음  

- Price Class 200: Includes most regions but excludes the most expensive ones.  
- 가격 클래스 200: 대부분의 지역 포함, 가장 비싼 지역 제외  

- Price Class 100: Includes only the least expensive regions.  
- 가격 클래스 100: 가장 저렴한 지역만 포함  

---

This is summarized in the following table. To better visualize, consider the world map with many edge locations.  
다음 표에 요약되어 있습니다. 시각적으로 이해하려면 엣지 위치가 많은 세계 지도를 떠올리세요.  
> 가격 클래스가 전 세계 엣지 위치에 어떤 영향을 주는지 그림으로 이해하기 좋습니다.  

---

Price Class 100 covers North America and Europe. Price Class 200 adds some additional regions. Price Class All includes the entire world for edge locations.  
가격 클래스 100은 북미와 유럽을 포함합니다. 가격 클래스 200은 일부 추가 지역을 포함합니다. 가격 클래스 All은 전 세계 엣지 위치를 포함합니다.  
> 지역 범위와 비용, 성능 차이를 요약합니다.  

---

That concludes this lecture on CloudFront price classes. I hope you found it helpful, and I will see you in the next lecture.  
이것으로 CloudFront 가격 클래스 강의를 마칩니다. 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  
> 강의 마무리  

---

## Key Takeaways  
## 핵심 요약  

- CloudFront pricing varies by geographic region due to differing data transfer costs at edge locations.  
- CloudFront 요금은 엣지 위치의 데이터 전송 비용 차이 때문에 지역별로 다릅니다.  

- Data transfer costs decrease with higher volumes, benefiting large-scale usage.  
- 데이터 전송량이 많을수록 비용이 감소하여 대규모 사용에 유리합니다.  

- Price classes allow selection of edge locations to balance cost and performance.  
- 가격 클래스를 통해 비용과 성능의 균형을 맞추며 엣지 위치를 선택할 수 있습니다.  

- Price Class All includes all regions with best performance but higher cost; Price Class 200 excludes the most expensive regions; Price Class 100 includes only the least expensive regions.  
- 가격 클래스 All은 모든 지역 포함, 최고 성능 제공하지만 비용 높음; 가격 클래스 200은 가장 비싼 지역 제외; 가격 클래스 100은 가장 저렴한 지역만 포함  

🎮 **게임보상:**

* CloudFront 가격 클래스 이해 +10 XP
* 지역별 비용 차이 이해 +10 XP
* 데이터 전송량에 따른 단가 변화 이해 +10 XP
  총 **30 XP 획득!** 🎉
