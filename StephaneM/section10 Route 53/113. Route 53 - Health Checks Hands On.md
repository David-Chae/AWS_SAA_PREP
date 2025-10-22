# Route 53 - Health Checks Hands On  
# Route 53 - 헬스체크 실습  
👉 EC2 인스턴스와 Route 53 헬스체크를 실제로 설정하고 테스트하는 방법을 학습합니다.  

---

## Creating Health Checks for EC2 Instances  
## EC2 인스턴스용 헬스체크 생성  
Let's proceed to create some health checks.  
이제 헬스체크를 생성해 보겠습니다.  

On the left-hand side, navigate to the health checks section.  
왼쪽 메뉴에서 헬스체크 섹션으로 이동합니다.  

We will create health checks for all our EC2 instances.  
모든 EC2 인스턴스에 대한 헬스체크를 생성할 것입니다.  

We will create three health checks.  
세 개의 헬스체크를 생성합니다.  

The first one will be from an instance in US East 1, targeting an endpoint.  
첫 번째는 US East 1 인스턴스를 대상으로 합니다.  

You can specify either an IP address or a domain name.  
IP 주소나 도메인 이름 중 하나를 지정할 수 있습니다.  

We will keep it as an IP address.  
여기서는 IP 주소를 사용합니다.  

My instance in US East 1 is right here, so we will paste that in.  
US East 1 인스턴스의 IP를 붙여넣습니다.  

We need to specify a port; we will keep it as 80 since this is the HTTP port.  
포트는 HTTP 포트인 80으로 설정합니다.  

For the path, we will keep it as slash (/), which is the root of our website.  
경로는 `/`로 설정, 웹사이트 루트 경로를 의미합니다.  

While this is the same as IP slash, if we had a real application, it is common to have a path such as /health that responds with the health status of the endpoint itself.  
실제 애플리케이션에서는 `/health` 같은 경로로 엔드포인트 상태를 반환하는 것이 일반적입니다.  

For now, we will remove the /health path and keep it as /.  
우선 `/`로 유지합니다.  

---

## Advanced Configuration Options  
## 고급 설정 옵션  
We can configure advanced options such as the health check frequency.  
헬스체크 빈도 등 고급 옵션을 설정할 수 있습니다.  

We have the choice between a standard check every thirty seconds or a fast check every ten seconds.  
30초마다 일반 체크, 10초마다 빠른 체크 중 선택 가능합니다.  

We will keep it as standard because the fast option is more expensive.  
비용이 더 높은 빠른 체크 대신 일반 체크로 유지합니다.  

We also specify how many consecutive failures are required before considering the endpoint unhealthy.  
연속 실패 횟수 임계값도 지정합니다.  

Additionally, we can enable string matching to look for a specific string in the first 5,120 bytes of the response.  
응답의 처음 5120바이트에서 특정 문자열 검색 옵션도 있습니다.  

We can choose to enable a latency graph to monitor latency over time, invert the health check status, disable the health check, or customize the regions of the health checkers.  
지연 그래프 표시, 상태 반전, 헬스체크 비활성화, 헬스체커 지역 커스터마이징 옵션도 설정 가능.  

We will keep all options as default, using the recommended regions.  
모든 옵션은 기본값으로 유지하며 권장 지역을 사용합니다.  

Finally, we can choose whether to be notified when the health check fails by creating an alarm.  
마지막으로 헬스체크 실패 시 알람 생성 여부 선택 가능.  

For now, we will not create an alarm.  
이번에는 알람을 생성하지 않습니다.  

We have now created our first health check.  
첫 번째 헬스체크가 생성되었습니다.  

---

Next, we will create our second health check for the AP Southeast 1 region.  
다음으로 AP Southeast 1 리전용 헬스체크를 생성합니다.  

We will specify the IP address for the instance in AP Southeast 1, not the hostname, then proceed to create the health check.  
호스트명이 아닌 AP Southeast 1 인스턴스의 IP 주소를 지정하고 헬스체크를 생성합니다.  

The last health check will be for the EU Central 1 region.  
마지막 헬스체크는 EU Central 1 리전용입니다.  

We will create this health check, name it EU Central 1, specify the IP address, and create the health check.  
헬스체크 생성, 이름 지정, IP 주소 지정 후 생성 완료.  

Our health checks are now created.  
헬스체크 생성 완료.  

---

## Testing Health Check Failure by Modifying Security Group  
## 보안 그룹 변경으로 헬스체크 실패 테스트  
To test a failing health check, I will go to one of my instances, for example, the one in Singapore (AP Southeast 1).  
헬스체크 실패를 테스트하기 위해 AP Southeast 1 인스턴스로 이동합니다.  

For its security group, I will block port 80 by removing the inbound HTTP rule.  
보안 그룹에서 인바운드 HTTP 규칙 삭제 → 포트 80 차단.  

This action will cause the health check for AP Southeast 1 to report an unhealthy status.  
이제 AP Southeast 1 헬스체크가 비정상 상태로 표시됩니다.  

I will navigate to the security group, select inbound rules, and delete the HTTP rule.  
보안 그룹 → 인바운드 규칙 → HTTP 삭제.  

This will block HTTP traffic to the instance.  
인스턴스로의 HTTP 트래픽 차단.  

After waiting a bit for the health checkers to perform their checks, we can observe the results.  
헬스체커가 체크 수행 후 결과 확인.  

We have three health checkers: one is unhealthy, which is expected because we blocked HTTP traffic via the security group.  
헬스체커 3개 중 1개 비정상 → 예상대로 HTTP 차단 때문.  

The other two are healthy since their security groups remain unchanged.  
나머지 2개는 정상, 보안 그룹 변경 없음.  

We can view details about the health checks, such as the last check time.  
헬스체크 세부 정보 확인 가능, 마지막 체크 시간 등.  

For the unhealthy health check, we can view the error status.  
비정상 헬스체크 → 오류 상태 확인 가능.  

Viewing the last failed check shows a connection timeout, likely due to requests being blocked by the firewall, which in this case is the security group.  
마지막 실패 확인 → 연결 시간 초과 → 보안 그룹 차단 확인.  

This confirms that the health checks are working as expected.  
헬스체크가 정상적으로 작동함을 확인.  

---

## Creating a Calculated Health Check  
## 계산 헬스체크 생성  
We can also create a calculated health check.  
계산 헬스체크도 생성 가능.  

This type of health check monitors the status of other health checks.  
여러 헬스체크 상태를 모니터링합니다.  

We specify which health checks to monitor and define the criteria for reporting healthy status, such as when one, two, or all monitored health checks are healthy.  
모니터링할 헬스체크 선택 → 정상 보고 기준 정의 (1개, 2개, 전체 헬스체크 정상 시).  

This allows for complex logical rules.  
복잡한 논리 규칙 적용 가능.  

We will create a calculated health check that reports healthy only when all monitored health checks are healthy.  
모든 모니터링 헬스체크가 정상일 때만 정상으로 보고되는 계산 헬스체크 생성.  

After configuring the calculated health check, we finalize its creation.  
계산 헬스체크 구성 후 생성 완료.  

---

## Monitoring CloudWatch Alarms with Health Checks  
## 헬스체크와 CloudWatch 알람 연동  
Another type of health check can monitor the state of a CloudWatch alarm.  
다른 유형 헬스체크: CloudWatch 알람 상태 모니터링 가능.  

To set this up, specify the region of the alarm and select the alarm to monitor.  
알람 리전 지정 후 모니터링할 알람 선택.  

This is useful for monitoring the health of private EC2 instances or other private resources by linking their health status into a Route 53 health check.  
사설 EC2 또는 사설 리소스 상태를 Route 53 헬스체크에 연결해 모니터링 가능.  

Currently, I cannot create this type of health check because I do not have an available alarm.  
현재 알람이 없어 생성 불가.  

My calculated health check is now reported as unhealthy because one of the monitored health checks is unhealthy.  
모니터링 헬스체크 중 1개 비정상 → 계산 헬스체크도 비정상 보고.  

This demonstrates the power of health checks in monitoring multiple endpoints collectively.  
여러 엔드포인트를 통합 모니터링하는 헬스체크 기능 확인.  

---

## Key Takeaways  
## 핵심 포인트  
- Created health checks for EC2 instances in multiple AWS regions using IP addresses and HTTP port 80.  
  여러 리전 EC2 인스턴스에 대한 IP 주소 + HTTP 80 포트 헬스체크 생성.  
- Configured health check settings including check intervals, failure thresholds, and string matching options.  
  체크 간격, 실패 임계값, 문자열 매칭 옵션 구성.  
- Demonstrated how security group rules affect health check status by blocking HTTP traffic.  
  보안 그룹 규칙이 헬스체크 상태에 미치는 영향 시연.  
- Created a calculated health check that monitors the status of multiple health checks collectively.  
  여러 헬스체크 상태를 통합 모니터링하는 계산 헬스체크 생성.  
- Explained the integration of CloudWatch alarms with Route 53 health checks for private resource monitoring.  
  사설 리소스 모니터링을 위한 CloudWatch 알람 + Route 53 헬스체크 통합 설명.  

---

💡 **게임 보상:**

* 🖥️ EC2 헬스체크 실습 = +50 EXP
* 🔐 보안 그룹 테스트 = +50 EXP
* 🧮 계산 헬스체크 생성 = +100 EXP
* 🌐 CloudWatch 연동 개념 학습 = +100 EXP
  **총 보상: 300 EXP + Route 53 Health Pro 뱃지 🏅**
