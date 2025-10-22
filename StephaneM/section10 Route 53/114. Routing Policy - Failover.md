# Routing Policy - Failover  
# 라우팅 정책 - 페일오버  

In this lecture, we will discuss routing policies, specifically focusing on failover routing.  
이번 강의에서는 라우팅 정책 중 특히 페일오버 라우팅에 대해 다룹니다.  

The concept involves using Route 53 as the DNS service with two EC2 instances: one designated as the primary instance and the other as the secondary or disaster recovery instance.  
이 개념은 Route 53을 DNS 서비스로 사용하고, 두 개의 EC2 인스턴스를 구성합니다. 하나는 주(primary), 다른 하나는 보조(secondary) 또는 재해 복구용입니다.  

The primary record in Route 53 is associated with a health check, which is mandatory.  
Route 53의 주 레코드는 필수로 헬스체크와 연결됩니다.  

If the health check detects that the primary instance becomes unhealthy, Route 53 automatically fails over to the secondary EC2 instance and starts routing traffic to it instead.  
주 헬스체크가 비정상 상태를 감지하면 Route 53은 자동으로 보조 EC2 인스턴스로 트래픽을 전환(failover)합니다.  

The secondary EC2 instance can also be associated with a health check if desired.  
보조 EC2 인스턴스도 원하는 경우 헬스체크와 연결할 수 있습니다.  

However, there can only be one primary and one secondary record in this failover configuration.  
하지만 이 페일오버 구성에서는 주 레코드와 보조 레코드 각각 하나만 존재할 수 있습니다.  

When a client makes DNS requests, it will automatically receive the resource that is deemed healthy.  
클라이언트가 DNS 요청을 하면 자동으로 정상 상태의 리소스를 받습니다.  

If the primary instance is healthy, Route 53 responds with the primary record.  
주 인스턴스가 정상인 경우, Route 53은 주 레코드를 반환합니다.  

If the primary health check fails, the response switches to the secondary record, enabling seamless failover.  
주 헬스체크가 실패하면 응답이 보조 레코드로 전환되어 무중단 페일오버가 이루어집니다.  

---

## Hands-on: Creating a Failover Record  
## 실습: 페일오버 레코드 생성  

Let's practice creating a failover record using Route 53 health checks.  
Route 53 헬스체크를 사용하여 페일오버 레코드를 생성해봅시다.  

In the hosted zone, create a new record named failover.stephanetheteacher.com.  
호스티드 존에서 `failover.stephanetheteacher.com`이라는 새 레코드를 생성합니다.  

This will be an A record pointing to the EC2 instance in the EU-central-1 region, which is geographically closer.  
이 레코드는 지리적으로 가까운 EU-central-1 인스턴스를 가리키는 A 레코드입니다.  

Set the routing policy to failover and the TTL to a low value, such as 60 seconds, to allow quick DNS updates.  
라우팅 정책을 페일오버로 설정하고 TTL을 60초 등 낮게 설정하여 빠른 DNS 업데이트가 가능하게 합니다.  

The failover record type has two options: primary or secondary.  
페일오버 레코드 유형에는 주(primary)와 보조(secondary) 두 가지 옵션이 있습니다.  

This record will be the primary and must be associated with a health check named EU-central-1 with a record ID E.  
이 레코드는 주(primary)로 설정하며, 헬스체크 `EU-central-1`과 레코드 ID `E`에 연결해야 합니다.  

This setup means that this record is primary and linked to a health check, enabling failover to a secondary record if the health check fails.  
즉, 주 레코드가 헬스체크와 연결되어 헬스체크 실패 시 자동으로 보조 레코드로 페일오버됩니다.  

Next, add a secondary record with the same name failover.stephanetheteacher.com pointing to the EC2 instance in the US-east-1 region.  
다음으로 동일한 이름의 보조 레코드를 생성하고, US-east-1 인스턴스를 가리키도록 설정합니다.  

Set the TTL to 60 seconds and the failover record type to secondary.  
TTL을 60초로 설정하고 페일오버 레코드 유형을 보조(secondary)로 지정합니다.  

Optionally, associate a health check with this record as well, for example, US-East-1 with record ID US.  
원하면 이 레코드에도 헬스체크를 연결할 수 있습니다. 예: `US-East-1`, 레코드 ID `US`.  

After creating the records, verify that both health checks associated with the records are healthy.  
레코드 생성 후 두 헬스체크가 모두 정상인지 확인합니다.  

---

## Testing Failover  
## 페일오버 테스트  

Currently, accessing failover.stephanetheteacher.com returns a response from the EU-central-1c instance, which is the primary.  
현재 `failover.stephanetheteacher.com` 접속 시 주 인스턴스(EU-central-1c)에서 응답이 반환됩니다.  

To test failover, simulate a failure in the primary instance by modifying its security group to block inbound HTTP traffic.  
페일오버를 테스트하려면 주 인스턴스의 보안 그룹에서 HTTP 인바운드 트래픽을 차단하여 실패를 시뮬레이션합니다.  

This makes the instance unreachable by the health checkers.  
이렇게 하면 헬스체커가 인스턴스에 접근할 수 없게 됩니다.  

Wait for the health check to detect the failure and become unhealthy.  
헬스체커가 실패를 감지하고 비정상 상태가 될 때까지 기다립니다.  

The monitoring tab shows when the health check status changed from healthy to unhealthy.  
모니터링 탭에서 헬스체크 상태가 정상 → 비정상으로 변경된 시점을 확인할 수 있습니다.  

Once the primary health check is unhealthy, refreshing the URL should now return a response from the US-east-1 instance, indicating that failover has occurred seamlessly behind the scenes.  
주 헬스체크가 비정상인 경우, URL 새로고침 시 US-east-1 인스턴스 응답이 반환되어 무중단 페일오버가 발생했음을 확인할 수 있습니다.  

To restore the primary instance, revert the security group changes by adding back the HTTP inbound rule.  
주 인스턴스를 복구하려면 보안 그룹에 HTTP 인바운드 규칙을 다시 추가합니다.  

The health check will then pass again, and Route 53 will fail back to the primary location automatically.  
헬스체크가 다시 정상으로 돌아오고, Route 53은 자동으로 주 인스턴스로 페일백(fail back)합니다.  

This concludes the lecture on failover routing policies using Route 53.  
이로써 Route 53을 활용한 페일오버 라우팅 정책 강의를 마칩니다.  

The failover mechanism ensures high availability by automatically routing traffic to a healthy resource without manual intervention.  
페일오버 메커니즘은 수동 개입 없이 정상 리소스로 자동 라우팅하여 고가용성을 보장합니다.  

---

## Key Takeaways  
## 핵심 포인트  

- Route 53 failover routing policy enables automatic DNS failover between primary and secondary EC2 instances based on health checks.  
  헬스체크 기반으로 주/보조 EC2 인스턴스 간 자동 DNS 페일오버 지원.  

- The primary record must be associated with a health check to enable failover.  
  페일오버를 위해 주 레코드는 반드시 헬스체크와 연결되어야 함.  

- Clients receive DNS responses from the healthy resource, ensuring high availability.  
  클라이언트는 정상 리소스에서 DNS 응답을 받아 고가용성 보장.  

- Failover can be tested by simulating failure in the primary instance and observing automatic routing to the secondary instance.  
  주 인스턴스 실패를 시뮬레이션하여 보조 인스턴스로 자동 라우팅되는지 확인 가능.  

---

💡 **게임 보상:**

* 🌐 페일오버 레코드 생성 실습 = +50 EXP
* 🔄 페일오버 테스트 = +50 EXP
* ✅ 헬스체크 연동 페일백 이해 = +100 EXP
  **총 보상: 200 EXP + Route 53 Failover Expert 뱃지 🏅**
