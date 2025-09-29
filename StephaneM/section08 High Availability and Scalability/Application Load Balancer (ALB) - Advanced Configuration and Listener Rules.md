# Application Load Balancer (ALB) - Advanced Configuration and Listener Rules  
# 애플리케이션 로드 밸런서 (ALB) - 고급 구성 및 리스너 규칙  
➡️ ALB의 고급 설정과 리스너 규칙을 다루는 주제임을 설명하는 제목입니다.  

---

## Advanced Concepts for Application Load Balancer  
## 애플리케이션 로드 밸런서의 고급 개념  
➡️ 기본 사용법을 넘어 네트워크 보안을 중심으로 심화된 개념을 설명하겠다는 의미입니다.  

Let's explore some advanced concepts related to our load balancer, focusing first on network security.  
먼저 네트워크 보안에 초점을 맞추어 로드 밸런서와 관련된 고급 개념을 살펴봅시다.  
➡️ 학습 목표: 보안 강화 방법을 이해.  

Currently, we access this load balancer through a security group assigned to it. Similarly, our EC2 instances have their own security groups.  
현재 이 로드 밸런서는 보안 그룹을 통해 접근합니다. 마찬가지로, EC2 인스턴스도 각자 보안 그룹을 가지고 있습니다.  
➡️ ALB와 EC2는 모두 개별 보안 그룹을 적용받음.  

At present, if I access the EC2 instance directly via its public IP, I can reach it, or I can access it through the load balancer.  
현재는 EC2 퍼블릭 IP로 직접 접속할 수도 있고, 로드 밸런서를 통해 접속할 수도 있습니다.  
➡️ 보안이 완전히 제한된 상태는 아님.  

However, it may be preferable to restrict access so that the EC2 instances can only be accessed through the load balancer. Let's see how to achieve this.  
그러나 EC2 인스턴스가 오직 로드 밸런서를 통해서만 접근되도록 제한하는 것이 더 바람직합니다. 어떻게 하는지 살펴봅시다.  
➡️ 목표: EC2 직접 접근 차단.  

---

## Restricting EC2 Access to Load Balancer Only  
## EC2 접근을 로드 밸런서 전용으로 제한하기  
➡️ 보안 강화를 위한 설정 단계 제목.  

Navigate to the EC2 instances section and select the security group associated with your instances, for example, launch-wizard-1. Then, edit the inbound rules.  
EC2 인스턴스 섹션으로 이동하여 인스턴스에 연결된 보안 그룹(예: launch-wizard-1)을 선택하고, 인바운드 규칙을 수정합니다.  
➡️ 시작 단계: EC2 보안 그룹 수정.  

Currently, the HTTP rule allows traffic from anywhere (0.0.0.0/0). We want to change this so that only traffic coming from the load balancer's security group is allowed.  
현재 HTTP 규칙은 모든 곳(0.0.0.0/0)에서 오는 트래픽을 허용합니다. 이를 로드 밸런서 보안 그룹에서 오는 트래픽만 허용하도록 변경합니다.  
➡️ 보안 그룹을 CIDR에서 SG 기반으로 전환.  

To do this, first delete the existing HTTP rule. Then add a new inbound rule for HTTP, but instead of specifying a CIDR block, select the security group option and choose the load balancer's security group.  
이를 위해 기존 HTTP 규칙을 삭제합니다. 그리고 새로운 HTTP 인바운드 규칙을 추가하되, CIDR 블록 대신 보안 그룹 옵션을 선택하고 로드 밸런서 보안 그룹을 지정합니다.  
➡️ 설정 변경 절차.  

After saving this change, if you try to access the EC2 instance directly via its public IP, the connection will time out because direct access is no longer allowed. However, accessing the instance through the load balancer still works because the load balancer's security group is permitted.  
변경 사항을 저장한 후 EC2 퍼블릭 IP로 직접 접근하면 타임아웃이 발생합니다. 하지만 로드 밸런서를 통해 접근하면 정상적으로 연결됩니다.  
➡️ 결과: EC2 직접 접근 차단 성공.  

This configuration tightens network security by ensuring that EC2 instances only accept inbound HTTP traffic from the load balancer.  
이 설정은 EC2 인스턴스가 로드 밸런서에서 오는 HTTP 트래픽만 허용하도록 보안성을 강화합니다.  
➡️ 핵심 요약.  

---

## Application Load Balancer Listener Rules  
## 애플리케이션 로드 밸런서 리스너 규칙  
➡️ ALB의 요청 처리 규칙을 설정하는 방법.  

Within the ALB settings, navigate to the listeners section and select your listener. You will see the default listener rule, which forwards all requests to your demo target group.  
ALB 설정에서 리스너 섹션으로 이동하여 리스너를 선택합니다. 기본 규칙이 보이며, 모든 요청을 데모 타겟 그룹으로 전달합니다.  
➡️ ALB 기본 리스너 설명.  

You can add additional rules to customize how requests are routed. For example, create a new rule named DemoRule.  
추가 규칙을 만들어 요청 경로를 맞춤화할 수 있습니다. 예를 들어, DemoRule이라는 새로운 규칙을 생성합니다.  
➡️ 맞춤형 라우팅 가능.  

---

## Adding Conditions to Listener Rules  
## 리스너 규칙에 조건 추가하기  
➡️ 요청 필터링 기준 설명.  

When adding a rule, you specify conditions to filter requests. These conditions can be based on:  
규칙을 추가할 때, 요청을 필터링할 조건을 지정할 수 있습니다. 조건은 다음과 같습니다:  

- Host headers (e.g., *.example.com or myapp.example.com)  
- 호스트 헤더 (예: *.example.com 또는 myapp.example.com)  

- Path patterns (e.g., /error)  
- 경로 패턴 (예: /error)  

- HTTP request methods (GET, POST, etc.)  
- HTTP 요청 메서드 (GET, POST 등)  

- Source IP addresses  
- 소스 IP 주소  

- Query strings  
- 쿼리 문자열  

- HTTP headers  
- HTTP 헤더  

For this example, we will use a path condition with the value /error.  
이번 예시에서는 /error 경로 조건을 사용합니다.  
➡️ 실습 조건 지정.  

You can add multiple conditions if needed, but for now, one condition is sufficient.  
필요하다면 여러 조건을 추가할 수 있지만, 이번에는 하나만 사용합니다.  
➡️ 단순 조건 실습.  

---

## Defining Actions for Listener Rules  
## 리스너 규칙에 대한 동작 정의하기  
➡️ 조건 충족 시 수행할 작업 지정.  

After setting conditions, define the action to take when a request matches. Options include:  
조건을 설정한 후, 요청이 일치할 때 실행할 동작을 정의합니다. 가능한 동작은 다음과 같습니다:  

- Forwarding to specific target groups (useful if you have multiple target groups)  
- 특정 타겟 그룹으로 전달 (여러 타겟 그룹이 있는 경우 유용)  

- Redirecting to a specific URL with customizable protocol, host, path, and query  
- 지정된 URL로 리디렉션 (프로토콜, 호스트, 경로, 쿼리 설정 가능)  

- Returning a fixed response  
- 고정된 응답 반환  

For this example, we will return a fixed response with status code 404 and the message "Not found, custom error."  
이번 예시에서는 상태 코드 404와 메시지 "Not found, custom error."를 반환합니다.  
➡️ 에러 페이지 커스터마이징.  

---

## Rule Priority  
## 규칙 우선순위  
➡️ 여러 규칙 적용 시 우선순위 개념.  

Each listener rule has a priority number. The rule with the highest priority (lowest number) that matches a request is applied. You can have up to 100 rules, with priorities ranging from 1 to 50,000.  
각 리스너 규칙은 우선순위 번호를 가집니다. 숫자가 낮을수록 우선순위가 높으며, 최대 100개의 규칙(1~50,000 범위)을 설정할 수 있습니다.  
➡️ 우선순위 체계 설명.  

For this example, we assign a priority of 5 to the new rule.  
이번 예시에서는 새로운 규칙의 우선순위를 5로 설정합니다.  
➡️ 실습값 적용.  

After creating the rule, you will see both the default rule and the new DemoRule listed.  
규칙을 생성하면 기본 규칙과 새 DemoRule이 함께 표시됩니다.  
➡️ 설정 완료 확인.  

---

## Testing the Listener Rule  
## 리스너 규칙 테스트하기  
➡️ 규칙이 정상 동작하는지 검증.  

To test the new rule, access your load balancer's DNS name and append /error to the URL. This should trigger the rule and return the custom 404 response with the message "Not found, custom error."  
새 규칙을 테스트하려면 로드 밸런서의 DNS 이름 뒤에 /error를 붙여 접속합니다. 그러면 커스텀 404 응답이 반환됩니다.  
➡️ 테스트 결과 검증.  

This confirms that the path pattern condition and fixed response action are working as intended.  
이로써 경로 패턴 조건과 고정 응답 동작이 정상 작동함을 확인할 수 있습니다.  
➡️ 규칙 동작 검증 완료.  

---

## Conclusion  
## 결론  
➡️ 이번 세션의 요약.  

This session demonstrated how to enhance network security by restricting EC2 instance access to only the load balancer and how to configure ALB listener rules to route requests based on path conditions, including returning custom fixed responses.  
이번 세션에서는 EC2 인스턴스 접근을 로드 밸런서 전용으로 제한하여 네트워크 보안을 강화하는 방법과, ALB 리스너 규칙을 설정하여 경로 기반 요청 라우팅과 커스텀 응답을 구현하는 방법을 다루었습니다.  
➡️ 학습 성과 요약.  

---

## Key Takeaways  
## 핵심 요약  
➡️ 실습 핵심 포인트.  

- Configured EC2 instance security groups to only allow inbound HTTP traffic from the load balancer's security group, enhancing network security.  
- EC2 보안 그룹을 수정하여 로드 밸런서 보안 그룹에서 오는 HTTP 트래픽만 허용하도록 구성 → 네트워크 보안 강화.  

- Demonstrated how to modify Application Load Balancer (ALB) listener rules to route requests based on path conditions.  
- ALB 리스너 규칙을 수정하여 경로 기반으로 요청을 라우팅하는 방법 시연.  

- Created a custom rule to return a fixed 404 response for requests matching the /error path.  
- /error 경로에 대해 고정된 404 응답을 반환하는 커스텀 규칙 생성.  

- Explained the priority system for ALB listener rules, allowing multiple rules with defined precedence.  
- ALB 리스너 규칙의 우선순위 체계를 설명하여 여러 규칙을 정의된 순서대로 적용 가능함을 학습.  

---

제가 번역 + 설명을 라인별로 유지해서 정리했습니다. 🙂
이제 여기서 게임보상(예: ✅ 지식 포인트, 🔑 레벨업 포인트 등)을 어떻게 표시해드릴까요?
예를 들어 "이 부분을 이해하면 ✅ 보안 강화 포인트 +10 획득!" 같은 식으로 넣어드릴까요?
