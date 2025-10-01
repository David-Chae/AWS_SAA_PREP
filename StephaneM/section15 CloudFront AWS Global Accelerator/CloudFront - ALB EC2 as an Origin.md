# CloudFront - ALB/EC2 as an Origin  
# CloudFront - ALB/EC2를 오리진으로 연결  

---

## Connecting CloudFront to ALB or EC2 as an Origin  
## CloudFront를 ALB 또는 EC2 오리진으로 연결  

How can we connect CloudFront to an Application Load Balancer (ALB) or an EC2 instance as an origin?  
CloudFront를 Application Load Balancer(ALB) 또는 EC2 인스턴스를 오리진으로 연결하려면 어떻게 해야 할까요?  

---

There are two ways to achieve this, with the better and newer method being the use of VPC origins.  
방법은 두 가지가 있으며, 더 나은 최신 방법은 VPC 오리진을 사용하는 것입니다.  

---

VPC origins allow you to deliver content directly from applications hosted in your private subnets within your Virtual Private Cloud (VPC).  
VPC 오리진을 사용하면, Virtual Private Cloud(VPC) 내의 프라이빗 서브넷에 호스팅된 애플리케이션에서 직접 콘텐츠를 제공할 수 있습니다.  

---

This means everything can remain private without the need to expose any resources to the internet.  
즉, 리소스를 인터넷에 노출할 필요 없이 모든 것이 프라이빗하게 유지됩니다.  

---

With this setup, you can deliver traffic to private Application Load Balancers, Network Load Balancers, and EC2 instances.  
이 설정을 통해 프라이빗 Application Load Balancer, Network Load Balancer, EC2 인스턴스로 트래픽을 전달할 수 있습니다.  

---

## How VPC Origins Work  
## VPC 오리진 작동 방식  

We create a CloudFront distribution, which has multiple edge locations.  
여러 엣지 로케이션을 가진 CloudFront 배포를 생성합니다.  

---

Users access CloudFront through these edge locations.  
사용자는 이 엣지 로케이션을 통해 CloudFront에 접근합니다.  

---

From CloudFront, a VPC origin is created and connected to the backend resources, such as an ALB, NLB, or EC2 instance.  
CloudFront에서 VPC 오리진이 생성되고, ALB, NLB 또는 EC2 인스턴스 같은 백엔드 리소스와 연결됩니다.  

---

CloudFront then directs traffic through the VPC origin to your private subnets and applications.  
CloudFront는 트래픽을 VPC 오리진을 통해 프라이빗 서브넷과 애플리케이션으로 전달합니다.  

---

From a network perspective, this is one of the most secure ways to set up your architecture because your applications remain hosted privately and internally.  
네트워크 관점에서, 애플리케이션이 프라이빗하게 내부에 호스팅되므로 가장 안전하게 아키텍처를 구성하는 방법 중 하나입니다.  

---

You control what is exposed through CloudFront, which is very convenient.  
CloudFront를 통해 노출되는 것을 직접 제어할 수 있어 매우 편리합니다.  

---

## The Previous Method Using Public Networks  
## 이전 공용 네트워크 방식  

Before the VPC origin feature existed, the previous method involved using a public EC2 instance.  
VPC 오리진 기능이 생기기 전에는 공용 EC2 인스턴스를 사용하는 방식이었습니다.  

---

This required managing a list of CloudFront edge location public IPs and updating security groups accordingly.  
CloudFront 엣지 로케이션의 공용 IP 목록을 관리하고 보안 그룹을 업데이트해야 했습니다.  

---

You would retrieve the list of all CloudFront IPs and configure your EC2 instance's security group to allow inbound traffic only from these public IPs.  
모든 CloudFront IP 목록을 가져와서 EC2 인스턴스의 보안 그룹을 이 IP에서만 인바운드 트래픽을 허용하도록 구성했습니다.  

---

This setup made the EC2 instance public but restricted access to CloudFront edge locations.  
이 설정은 EC2 인스턴스를 공용으로 만들었지만 CloudFront 엣지 로케이션만 접근 가능하게 제한했습니다.  

---

The same approach applied if you had an Application Load Balancer.  
Application Load Balancer(ALB)를 사용할 경우에도 같은 방식이 적용되었습니다.  

---

The ALB would be public, but your EC2 instances could remain private, communicating through private networks secured by security groups.  
ALB는 공용이었지만, EC2 인스턴스는 보안 그룹으로 보호된 프라이빗 네트워크를 통해 프라이빗 상태를 유지했습니다.  

---

You had to ensure that your ALB's security group allowed inbound traffic from all CloudFront public IPs.  
ALB의 보안 그룹이 모든 CloudFront 공용 IP에서 들어오는 트래픽을 허용하도록 해야 했습니다.  

---

This process was more tedious because you needed to track and update these IPs regularly.  
이 과정은 IP를 정기적으로 추적하고 업데이트해야 해서 번거로웠습니다.  

---

Additionally, there was a risk that if someone modified the security group of your ALB or EC2 instance incorrectly, your instance could become publicly accessible to more than just your CloudFront distribution.  
또한, 누군가 ALB나 EC2 보안 그룹을 잘못 수정하면 CloudFront 배포 외에도 인스턴스가 공용으로 노출될 위험이 있었습니다.  

---

## Summary  
## 요약  

The old method required public exposure and manual IP management, whereas the new and better way is to use VPC origins.  
이전 방식은 공용 노출과 수동 IP 관리가 필요했지만, 새롭고 더 나은 방법은 VPC 오리진을 사용하는 것입니다.  

---

This approach enhances security by keeping backend resources private and simplifies configuration.  
이 방식은 백엔드 리소스를 프라이빗하게 유지하여 보안을 강화하고, 구성도 단순화합니다.  

---

This concludes the lecture on connecting CloudFront to ALB or EC2 as an origin using VPC origins.  
이로써 VPC 오리진을 사용해 CloudFront를 ALB 또는 EC2 오리진에 연결하는 강의를 마칩니다.  

---

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- CloudFront can connect to private application load balancers, network load balancers, and EC2 instances using VPC origins.  
- CloudFront는 VPC 오리진을 사용하여 프라이빗 ALB, NLB, EC2 인스턴스에 연결 가능  

- VPC origins allow delivering content directly from applications hosted in private subnets without exposing them to the internet.  
- VPC 오리진은 인터넷에 노출하지 않고 프라이빗 서브넷에서 직접 콘텐츠 제공 가능  

- The previous method involved using public EC2 instances or ALBs with security groups allowing CloudFront public IPs, which was more complex and less secure.  
- 이전 방식은 공용 EC2 또는 ALB와 CloudFront 공용 IP를 허용하는 보안 그룹을 사용하여 더 복잡하고 보안이 낮음  

- Using VPC origins is the more secure and modern approach for integrating CloudFront with backend resources.  
- VPC 오리진 사용은 CloudFront와 백엔드 리소스를 통합하는 더 안전하고 현대적인 접근 방식

🎮 **게임보상:**

* VPC 오리진 이해 +10 XP
* CloudFront + ALB/EC2 통합 보안 이해 +10 XP
* 이전 방식 대비 현대적 접근 비교 이해 +10 XP
  총 **30 XP 획득!** 🎉
