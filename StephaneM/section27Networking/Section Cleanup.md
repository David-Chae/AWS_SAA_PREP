```markdown
# Section Cleanup  
# 섹션 정리  

🎮 게임보상: "AWS Cleanup Pro Badge" +500 XP  

---

## Section Cleanup  
## 섹션 정리  

In this section, we have completed many tasks.  
이번 섹션에서 여러 작업을 완료했습니다.  

However, it is important to address resources that may incur costs if left running.  
하지만 계속 실행 중인 리소스가 비용을 발생시킬 수 있으므로 반드시 처리해야 합니다.  

---

## Managing EC2 Instances  
## EC2 인스턴스 관리  

First, regarding the two instances we created, ensure that you either terminate or stop them.  
먼저, 우리가 생성한 두 개의 인스턴스는 종료하거나 중지해야 합니다.  

I will stop them because I might need to return to them for further demonstrations.  
저는 추가 실습을 위해 다시 사용할 수 있으므로 중지할 것입니다.  

However, I recommend that you terminate all instances to avoid charges.  
하지만 비용을 피하려면 모든 인스턴스를 종료하는 것이 좋습니다.  

---

## Managing VPC Resources  
## VPC 리소스 관리  

Other resources that can incur costs are related to your Virtual Private Cloud (VPC).  
비용이 발생할 수 있는 다른 리소스는 VPC와 관련이 있습니다.  

Let's review what has been created.  
생성된 리소스를 확인해봅시다.  

We cannot delete the VPC immediately.  
VPC는 바로 삭제할 수 없습니다.  

We need to delete the subnets and the first route table.  
먼저 서브넷과 기본 라우트 테이블을 삭제해야 합니다.  

There is also an internet gateway that must be detached and deleted.  
인터넷 게이트웨이도 분리하고 삭제해야 합니다.  

Similarly, the egress-only internet gateway needs to be detached and deleted.  
마찬가지로 Egress Only 인터넷 게이트웨이도 분리하고 삭제해야 합니다.  

---

## Managing Elastic IPs  
## Elastic IP 관리  

Elastic IPs are very important to manage.  
Elastic IP 관리도 매우 중요합니다.  

We created an Elastic IP attached to our NAT gateway.  
NAT 게이트웨이에 연결된 Elastic IP를 생성했습니다.  

Remember to remove the Elastic IP after deleting the NAT gateway to avoid charges.  
NAT 게이트웨이를 삭제한 후 Elastic IP도 제거하여 비용 발생을 방지하세요.  

---

## Deleting VPC Endpoints  
## VPC 엔드포인트 삭제  

We also created some VPC endpoints.  
몇 개의 VPC 엔드포인트도 생성했습니다.  

Remember to delete these endpoints because they incur hourly fees and can accumulate costs over time.  
이 엔드포인트들은 시간 단위 요금이 부과되므로 삭제하여 누적 비용을 방지하세요.  

No interface endpoints were created in the NAT gateway.  
NAT 게이트웨이에 인터페이스 엔드포인트는 생성되지 않았습니다.  

After deleting the NAT gateway and releasing the Elastic IP, you can also delete any peering connections you have established.  
NAT 게이트웨이와 Elastic IP를 삭제한 후에는 피어링 연결도 제거할 수 있습니다.  

---

## Cleaning Up Network ACLs  
## 네트워크 ACL 정리  

Before removing the VPC entirely, ensure that you remove any network ACLs if necessary.  
VPC를 완전히 삭제하기 전에 필요하다면 네트워크 ACL도 제거하세요.  

Although network ACLs do not incur costs, cleaning them up maintains a tidy environment.  
네트워크 ACL은 비용이 들지 않지만, 정리하면 깔끔한 환경을 유지할 수 있습니다.  

---

## Monitoring AWS Billing  
## AWS 요금 모니터링  

Please make sure to delete and clean up all resources to avoid unexpected charges at the end of the month.  
월말에 예상치 못한 요금이 발생하지 않도록 모든 리소스를 삭제하고 정리하세요.  

The best way to monitor your AWS expenses is to visit your billing dashboard and review your bill regularly.  
AWS 비용을 모니터링하는 가장 좋은 방법은 Billing Dashboard를 방문하여 정기적으로 요금을 확인하는 것입니다.  

For example, in my billing dashboard, I can see charges related to the Virtual Private Cloud.  
예를 들어, 제 Billing Dashboard에서는 VPC 관련 요금을 확인할 수 있습니다.  

To address these charges, navigate to the bills section and select the current month.  
요금을 확인하려면 Bills 섹션으로 이동하여 이번 달을 선택합니다.  

Here, I observe that Elastic Compute Cloud has incurred a charge of 1.25.  
여기서 Elastic Compute Cloud가 1.25 달러의 요금을 발생시킨 것을 확인했습니다.  

The NAT gateway has also cost me 1.25 so far.  
NAT 게이트웨이도 지금까지 1.25 달러의 비용이 발생했습니다.  

Additionally, Route 53 has cost me 0.70.  
추가로 Route 53은 0.70 달러의 비용이 발생했습니다.  

I had forgotten to delete the hosted zone, which costs 0.50 per month.  
호스티드 존을 삭제하지 않아 월 0.50 달러가 청구되었습니다.  

The VPC Reachability Analyzer has also incurred some charges.  
VPC Reachability Analyzer도 일부 비용이 발생했습니다.  

---

## Conclusion  
## 결론  

This concludes the lecture. I hope you found it helpful, and I look forward to seeing you in the next lecture.  
이번 강의를 마칩니다. 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Always terminate or stop instances to avoid unnecessary costs.  
- 불필요한 비용을 방지하려면 인스턴스를 항상 종료하거나 중지하세요.  

- Clean up VPC components such as subnets, route tables, internet gateways, and elastic IPs to prevent ongoing charges.  
- 서브넷, 라우트 테이블, 인터넷 게이트웨이, Elastic IP 등 VPC 구성 요소를 정리하여 지속적인 비용 발생을 막으세요.  

- Delete VPC endpoints and peering connections as they incur hourly fees.  
- VPC 엔드포인트와 피어링 연결은 시간 단위 요금이 부과되므로 삭제하세요.  

- Regularly review your AWS billing dashboard to monitor and manage expenses effectively.  
- AWS Billing Dashboard를 정기적으로 확인하여 비용을 효과적으로 관리하세요.  

- Neglecting to clean up resources can lead to unexpected charges at the end of the billing cycle.  
- 리소스를 정리하지 않으면 청구 주기 말에 예상치 못한 비용이 발생할 수 있습니다.  
```
