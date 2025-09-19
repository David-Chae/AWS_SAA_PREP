```markdown
# VPC Traffic Mirroring  
# VPC 트래픽 미러링  

🎮 게임보상: "Mirror Guardian Badge" +500 XP  

---

## Introduction to VPC Traffic Mirroring  
## VPC 트래픽 미러링 소개  

VPC Traffic Mirroring is a powerful security feature designed to capture and inspect network traffic within a Virtual Private Cloud (VPC) without disrupting normal operations.  
VPC 트래픽 미러링은 VPC 내 네트워크 트래픽을 캡처하고 분석할 수 있도록 설계된 강력한 보안 기능으로, 정상 운영을 방해하지 않습니다.  

The main idea is to route network traffic to security appliances that we manage, enabling detailed analysis while maintaining the integrity and performance of the original traffic flow.  
핵심 아이디어는 네트워크 트래픽을 우리가 관리하는 보안 장치로 라우팅하여, 원래 트래픽의 무결성과 성능을 유지하면서 상세 분석을 가능하게 하는 것입니다.  

---

## Configuring Traffic Mirroring  
## 트래픽 미러링 구성  

To set up traffic mirroring, we define the source Elastic Network Interfaces (ENIs) from which we want to capture traffic.  
트래픽 미러링을 설정하려면, 트래픽을 캡처할 소스 ENI(Elastic Network Interface)를 정의합니다.  

Then, we specify the targets where this mirrored traffic should be sent, such as our own ENIs or a Network Load Balancer.  
그런 다음, 미러링된 트래픽을 보낼 대상, 예를 들어 자체 ENI나 네트워크 로드 밸런서를 지정합니다.  

---

## Example Scenario  
## 예제 시나리오  

Consider an EC2 instance with an attached ENI that handles inbound and outbound internet traffic.  
인바운드 및 아웃바운드 인터넷 트래픽을 처리하는 ENI가 연결된 EC2 인스턴스를 가정해봅니다.  

We want to analyze this traffic without interrupting the instance's normal function.  
인스턴스의 정상 기능을 방해하지 않고 트래픽을 분석하고 싶습니다.  

To achieve this, we set up a Network Load Balancer with an auto scaling group of EC2 instances running security software behind it.  
이를 위해, 보안 소프트웨어가 실행되는 EC2 인스턴스의 오토스케일링 그룹 뒤에 네트워크 로드 밸런서를 설정합니다.  

All traffic from the source ENI is mirrored to this load balancer for inspection.  
소스 ENI의 모든 트래픽은 검사 목적을 위해 이 로드 밸런서로 미러링됩니다.  

---

## Traffic Mirroring Operation  
## 트래픽 미러링 작동 방식  

With VPC Traffic Mirroring enabled, all traffic sent to the source ENI is duplicated and sent to the Network Load Balancer.  
VPC 트래픽 미러링이 활성화되면, 소스 ENI로 전송되는 모든 트래픽이 복제되어 네트워크 로드 밸런서로 전송됩니다.  

The original EC2 instance continues to operate normally, unaware of the mirroring process.  
원래 EC2 인스턴스는 미러링 과정을 인식하지 못한 채 정상적으로 작동합니다.  

Optionally, filters can be applied to capture only specific traffic, reducing the volume of mirrored data and focusing on relevant information.  
선택적으로, 특정 트래픽만 캡처하도록 필터를 적용할 수 있어 미러링 데이터 양을 줄이고 관련 정보에 집중할 수 있습니다.  

---

## Supporting Multiple Sources  
## 다중 소스 지원  

Traffic mirroring can be configured for multiple source ENIs.  
트래픽 미러링은 여러 소스 ENI에 대해 구성할 수 있습니다.  

For example, a second EC2 instance with its own ENI can also have its traffic mirrored to the same Network Load Balancer for centralized analysis.  
예를 들어, 자체 ENI를 가진 두 번째 EC2 인스턴스의 트래픽도 동일한 네트워크 로드 밸런서로 미러링하여 중앙 집중 분석이 가능합니다.  

---

## Requirements and Use Cases  
## 요구 사항 및 사용 사례  

The source and target must be in the same VPC or in different VPCs connected via VPC Peering.  
소스와 대상은 동일한 VPC에 있거나 VPC Peering으로 연결된 다른 VPC에 있어야 합니다.  

Common use cases include content inspection, threat monitoring, and network troubleshooting.  
일반적인 사용 사례로는 콘텐츠 검사, 위협 모니터링, 네트워크 문제 해결이 있습니다.  

---

## Conclusion  
## 결론  

While it is challenging to demonstrate VPC Traffic Mirroring in a live demo, the conceptual diagram and explanation provide a clear understanding of how this feature enhances network security and monitoring capabilities.  
VPC 트래픽 미러링을 실시간 데모로 보여주는 것은 어렵지만, 개념적 다이어그램과 설명을 통해 이 기능이 네트워크 보안 및 모니터링 기능을 어떻게 향상시키는지 명확히 이해할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- VPC Traffic Mirroring allows capturing and inspecting network traffic in a non-intrusive manner.  
- VPC 트래픽 미러링은 네트워크 트래픽을 비침습적으로 캡처하고 분석할 수 있게 합니다.  

- Traffic from source ENIs can be mirrored to targets such as ENIs or Network Load Balancers.  
- 소스 ENI의 트래픽은 ENI나 네트워크 로드 밸런서와 같은 대상으로 미러링할 수 있습니다.  

- This feature supports multiple sources and can work across VPCs with VPC Peering enabled.  
- 이 기능은 다중 소스를 지원하며, VPC Peering이 활성화된 VPC 간에서도 작동할 수 있습니다.  

- Use cases include content inspection, threat monitoring, and network troubleshooting.  
- 사용 사례로는 콘텐츠 검사, 위협 모니터링, 네트워크 문제 해결이 있습니다.  
```
