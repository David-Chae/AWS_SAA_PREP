# Routing Policy - Geoproximity  
# 라우팅 정책 - 지리 근접(Geoproximity)  

## Introduction to Geoproximity Routing  
## 지리 근접 라우팅 소개  

Geoproximity Routing is a feature that allows you to route traffic to your resources based on the geographic location of your users and resources.  
지리 근접 라우팅은 사용자의 위치와 리소스 위치를 기반으로 트래픽을 리소스로 라우팅할 수 있는 기능입니다.  

Although it can be somewhat confusing, it becomes clearer with diagrams and examples.  
다소 혼란스러울 수 있지만, 다이어그램과 예제를 통해 더 명확하게 이해할 수 있습니다.  

With this policy, you can use a number called the bias to shift more traffic to resources based on specific locations.  
이 정책에서는 'bias'(편향)라는 값을 사용하여 특정 위치 기반으로 더 많은 트래픽을 리소스로 이동시킬 수 있습니다.  

Adjusting the bias value changes the size of the geographic area associated with a resource.  
bias 값을 조정하면 해당 리소스와 관련된 지리적 영역의 크기가 변경됩니다.  

To increase traffic to a specific resource, you expand the bias value by increasing it.  
특정 리소스로 트래픽을 늘리려면 bias 값을 증가시켜 영역을 확장합니다.  

Conversely, to decrease traffic, you shrink the bias by decreasing it to a negative number.  
반대로 트래픽을 줄이려면 bias 값을 감소시켜 음수로 설정하여 영역을 축소합니다.  

Resources can be AWS resources, in which case you specify the region they are in, and AWS automatically computes the correct routing.  
리소스가 AWS 리소스인 경우, 해당 리소스의 지역(region)을 지정하면 AWS가 자동으로 올바른 라우팅을 계산합니다.  

For non-AWS resources, such as on-premises data centers, you need to specify the latitude and longitude so AWS knows their location.  
AWS가 아닌 리소스(온프레미스 데이터 센터 등)의 경우, 위도와 경도를 지정해야 AWS가 위치를 인식할 수 있습니다.  

To leverage the bias feature, you need to use the advanced Route 53 Traffic Flow.  
bias 기능을 활용하려면 고급 Route 53 Traffic Flow를 사용해야 합니다.  

---

## Example of Geoproximity Routing  
## 지리 근접 라우팅 예시  

Consider two resources: one in the us-west-1 region and another in the us-east-1 region.  
두 리소스를 가정해보겠습니다: 하나는 us-west-1 지역, 다른 하나는 us-east-1 지역입니다.  

If the bias is set to zero in both regions, users across the United States will be routed based on proximity.  
두 지역 모두 bias를 0으로 설정하면, 미국 전역 사용자는 근접성을 기준으로 라우팅됩니다.  

There will be a dividing line splitting the US into two parts: users to the left of the line will be routed to us-west-1, and users to the right will be routed to us-east-1.  
미국을 두 부분으로 나누는 경계선이 생기며, 경계선 왼쪽 사용자는 us-west-1로, 오른쪽 사용자는 us-east-1로 라우팅됩니다.  

This setup routes users to the closest resource region based on their location when no bias is applied.  
bias가 적용되지 않은 경우, 사용자는 위치 기반으로 가장 가까운 리소스로 라우팅됩니다.  

---

## Effect of Bias on Routing  
## bias가 라우팅에 미치는 영향  

Now, suppose the bias is set to zero in us-west-1 but set to a positive value of 50 in us-east-1.  
이제 us-west-1의 bias는 0, us-east-1의 bias는 50으로 설정한다고 가정합니다.  

The bias causes the dividing line between the two resources to shift leftward, increasing the geographic area served by us-east-1.  
bias 값 때문에 두 리소스 사이의 경계선이 왼쪽으로 이동하며 us-east-1이 담당하는 영역이 넓어집니다.  

As a result, users to the left of the new dividing line will still go to us-west-1, but more users to the right will be routed to us-east-1 due to the higher bias.  
결과적으로, 새로운 경계선 왼쪽 사용자는 여전히 us-west-1로 가지만, 오른쪽 사용자는 더 많은 사용자가 높은 bias 때문에 us-east-1로 라우팅됩니다.  

This mechanism allows you to shift traffic to specific regions by adjusting the bias values accordingly.  
이 메커니즘을 통해 bias 값을 조정하여 특정 지역으로 트래픽을 이동시킬 수 있습니다.  

---

## Practical Use Case  
## 실전 활용 사례  

If you have resources distributed globally and want to direct more traffic to a particular region, you can increase the bias for that region.  
글로벌에 리소스가 분산되어 있고 특정 지역으로 더 많은 트래픽을 유도하고 싶다면, 해당 지역의 bias 값을 증가시키면 됩니다.  

This will attract more users and traffic to that resource.  
이렇게 하면 더 많은 사용자와 트래픽이 해당 리소스로 유입됩니다.  

In summary, Geoproximity Routing is especially helpful when you need to shift traffic from one region to another by increasing the bias value for the desired region.  
요약하면, 지리 근접 라우팅은 원하는 지역의 bias 값을 증가시켜 트래픽을 한 지역에서 다른 지역으로 이동시킬 때 특히 유용합니다.  

---

## Conclusion  
## 결론  

The diagrams and examples provided help clarify how Geoproximity Routing works and how bias values influence traffic distribution across geographic regions.  
제공된 다이어그램과 예제를 통해 지리 근접 라우팅 작동 방식과 bias 값이 지리적 영역별 트래픽 분포에 미치는 영향을 이해할 수 있습니다.  

Thank you for engaging with this lecture. I look forward to seeing you in the next session.  
이번 강의를 따라와 주셔서 감사합니다. 다음 세션에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 포인트  

- Geoproximity Routing allows routing traffic based on the geographic location of users and resources.  
  지리 근접 라우팅은 사용자와 리소스의 지리적 위치를 기준으로 트래픽을 라우팅할 수 있습니다.  

- The bias value controls the amount of traffic directed to a specific resource by expanding or shrinking its geographic influence.  
  bias 값은 특정 리소스로 유입되는 트래픽 양을 지리적 영향 범위를 확장하거나 축소함으로써 제어합니다.  

- AWS resources use region specifications, while non-AWS resources require latitude and longitude coordinates.  
  AWS 리소스는 지역(region) 지정으로 처리되며, 비-AWS 리소스는 위도/경도 좌표가 필요합니다.  

- Geoproximity Routing is useful for shifting traffic between regions by adjusting the bias values.  
  bias 값을 조정하여 지역 간 트래픽을 이동시키는 데 지리 근접 라우팅이 유용합니다.  

---

💡 **게임 보상:**

* 🌐 Geoproximity Routing 개념 학습 = +50 EXP
* ⚖️ Bias 값 이해 및 트래픽 이동 사례 = +70 EXP
* 🌎 글로벌 리소스 트래픽 조정 실습 = +80 EXP
  **총 보상: 200 EXP + Route 53 Geoproximity Specialist 뱃지 🏅**
