```markdown
# Direct Connect and Site-to-Site VPN Backup Architecture  
# Direct Connect 및 Site-to-Site VPN 백업 아키텍처  

🎮 게임보상: "Backup Architect Badge" +500 XP  

---

## Direct Connect and Site-to-Site VPN Architecture  
## Direct Connect 및 Site-to-Site VPN 아키텍처  

This lecture covers an architecture that may appear in the exam.  
이 강의에서는 시험에 나올 수 있는 아키텍처를 다룹니다.  

The setup involves connecting your corporate data center to your Virtual Private Cloud (VPC) using Direct Connect.  
이 설정은 Direct Connect를 사용하여 기업 데이터 센터를 Virtual Private Cloud(VPC)에 연결하는 것을 포함합니다.  

Direct Connect serves as your primary connection.  
Direct Connect는 기본(primary) 연결 역할을 합니다.  

It is an expensive solution but provides a dedicated link between your data center and VPC.  
비용은 높지만 데이터 센터와 VPC 간 전용 링크를 제공합니다.  

However, there may be occasions when your Direct Connect connection experiences issues.  
하지만 Direct Connect 연결에 문제가 발생할 수 있는 경우가 있습니다.  

In such cases, you do not want to lose internet connectivity to your VPC.  
이러한 경우, VPC와의 인터넷 연결을 잃고 싶지 않습니다.  

One option is to use Direct Connect as a secondary connection as well, but this approach is quite expensive.  
한 가지 방법은 Direct Connect를 보조 연결(secondary)로 사용하는 것이지만, 이 방법은 비용이 상당히 높습니다.  

Alternatively, you can set up a site-to-site VPN connection as a backup.  
대안으로, 사이트 간 VPN(site-to-site VPN) 연결을 백업으로 설정할 수 있습니다.  

This backup connection is configured to activate if the primary Direct Connect connection fails.  
이 백업 연결은 기본 Direct Connect 연결이 실패할 경우 활성화되도록 구성됩니다.  

When the backup activates, your connection to the VPC is maintained through the public internet using the site-to-site VPN.  
백업이 활성화되면 사이트 간 VPN을 사용하여 공용 인터넷을 통해 VPC와의 연결이 유지됩니다.  

This setup can be more reliable because the public internet may always be accessible, providing a fallback path to your VPC.  
이 설정은 공용 인터넷이 항상 접근 가능할 수 있어, VPC로의 대체 경로(fallback)를 제공하므로 더 신뢰할 수 있습니다.  

This architecture is important to understand as it can appear in the exam.  
이 아키텍처는 시험에 출제될 수 있으므로 이해하는 것이 중요합니다.  

It ensures continuous connectivity to your VPC by combining Direct Connect with a site-to-site VPN backup.  
Direct Connect와 사이트 간 VPN 백업을 결합하여 VPC에 대한 지속적인 연결을 보장합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Direct Connect provides a primary, dedicated connection between a corporate data center and a VPC.  
- Direct Connect는 기업 데이터 센터와 VPC 간 기본 전용 연결을 제공합니다.  

- Due to its expense, Direct Connect may sometimes fail, necessitating a backup connection.  
- 비용 때문에 Direct Connect는 때때로 실패할 수 있으며, 백업 연결이 필요합니다.  

- A site-to-site VPN can be configured as a backup to Direct Connect, activating if the primary connection fails.  
- 사이트 간 VPN은 Direct Connect의 백업으로 구성할 수 있으며, 기본 연결이 실패할 경우 활성화됩니다.  

- The site-to-site VPN uses the public internet, which may offer more reliable accessibility as a fallback.  
- 사이트 간 VPN은 공용 인터넷을 사용하며, 대체 경로로서 더 안정적인 접근성을 제공할 수 있습니다.  
```
