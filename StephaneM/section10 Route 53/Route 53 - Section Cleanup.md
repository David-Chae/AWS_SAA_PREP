# Route 53 - Section Cleanup  
# Route 53 - 섹션 정리  

## Cleaning Up Route 53 Resources  
## Route 53 리소스 정리  

Let's proceed to clean up what we have done in Route 53 to avoid incurring unnecessary costs.  
불필요한 비용 발생을 피하기 위해 Route 53에서 수행한 작업을 정리해 보겠습니다.  

The domain name you have purchased remains in your account and will cost you $12 per year to renew, or more if you have bought a pricier domain name.  
구입한 도메인 이름은 계정에 남아 있으며, 연간 $12 또는 더 비싼 도메인의 경우 더 많은 비용이 갱신 비용으로 발생합니다.  

Regarding the domain name itself, specifically the hosted zone, if you are not using it, you can delete this hosted zone by first emptying all the records.  
도메인 자체, 특히 호스티드 존의 경우 사용하지 않는다면, 모든 레코드를 비운 후 호스티드 존을 삭제할 수 있습니다.  

Otherwise, it will cost you 50 cents per month to keep this hosted zone alive.  
그렇지 않으면, 호스티드 존을 유지하는 데 월 50센트가 발생합니다.  

Within the hosted zone, it does not matter if you have many records; you can just leave them as is.  
호스티드 존 내에 많은 레코드가 있어도 상관없으며, 그대로 두어도 됩니다.  

The other resources we need to delete are all our EC2 instances in our different regions, as well as our Application Load Balancer (ALB).  
삭제해야 하는 다른 리소스는 여러 리전에 있는 모든 EC2 인스턴스와 애플리케이션 로드 밸런서(ALB)입니다.  

We had EC2 instances in three different regions. I will delete them one by one.  
세 개 리전에 EC2 인스턴스가 있었으며, 하나씩 삭제하겠습니다.  

There was one instance in Frankfurt, and I believe the load balancer I created is also there. I will delete this load balancer as well.  
프랑크푸르트에는 하나의 인스턴스가 있었고, 생성한 로드 밸런서도 그곳에 있는 것으로 보입니다. 이 로드 밸런서도 삭제하겠습니다.  

We can also delete the associated target group with that load balancer.  
해당 로드 밸런서와 연관된 타겟 그룹도 삭제할 수 있습니다.  

We have to perform the same kind of cleanup in other regions.  
다른 리전에서도 동일한 정리를 수행해야 합니다.  

For me, this is the us-east-1 region, where I will terminate another EC2 instance.  
저의 경우 us-east-1 리전에서 또 다른 EC2 인스턴스를 종료하겠습니다.  

Finally, I will do the exact same thing in the ap-southeast-1 region.  
마지막으로 ap-southeast-1 리전에서도 동일한 작업을 수행하겠습니다.  

After this cleanup, you should not incur any costs from these lectures.  
이 정리를 마치면, 이번 강의와 관련된 추가 비용이 발생하지 않을 것입니다.  

I hope you liked this section, and I will see you in the next lecture.  
이 섹션이 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 포인트  

- Domain names purchased remain in your account and incur an annual renewal fee.  
  구입한 도메인은 계정에 남아 있으며 연간 갱신 비용이 발생합니다.  

- Hosted zones in Route 53 cost money monthly if not deleted; emptying records allows deletion.  
  삭제하지 않은 호스티드 존은 매월 비용이 발생하며, 레코드를 비워야 삭제할 수 있습니다.  

- EC2 instances and associated resources like load balancers must be terminated in all regions to avoid charges.  
  EC2 인스턴스와 로드 밸런서 등 연관 리소스는 모든 리전에서 종료해야 비용을 피할 수 있습니다.  

- Proper cleanup after using AWS resources prevents unexpected costs.  
  AWS 리소스를 사용한 후 적절한 정리를 통해 예상치 못한 비용 발생을 예방할 수 있습니다.  

---

💡 **게임 보상:**

* 🧹 Route 53 리소스 정리 이해 = +30 EXP
* 💰 비용 최적화와 삭제 방법 학습 = +40 EXP
* 🛠️ EC2 및 ALB 종료 및 다중 리전 정리 = +50 EXP
  **총 보상: 120 EXP + AWS Cleanup Master 뱃지 🏅**
