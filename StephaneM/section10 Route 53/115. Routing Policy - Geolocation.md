# Routing Policy - Geolocation  
# 라우팅 정책 - 지리적 위치 기반  

Let's discuss the Routing Policy based on Geolocation, which differs significantly from Latency-based routing.  
지리적 위치 기반 라우팅 정책에 대해 논의해보겠습니다. 이 정책은 지연 시간 기반 라우팅과는 상당히 다릅니다.  

This policy routes users based on their actual physical location.  
이 정책은 사용자의 실제 물리적 위치를 기반으로 트래픽을 라우팅합니다.  

For example, you can specify routing rules based on a user's continent, country, or even more precise locations such as U.S. states.  
예를 들어, 사용자의 대륙, 국가, 또는 미국 주와 같은 더 세부적인 위치를 기반으로 라우팅 규칙을 지정할 수 있습니다.  

The most precise location match is selected first and then routed to the corresponding IP address.  
가장 정밀한 위치 일치 항목이 먼저 선택되며, 해당 IP 주소로 라우팅됩니다.  

It is important to create a default record to handle cases where there is no match for the user's location.  
사용자의 위치와 일치하지 않는 경우를 처리하기 위해 기본(default) 레코드를 생성하는 것이 중요합니다.  

Use cases for geolocation routing include website localization, restricting content distribution, load balancing, and more.  
지리적 위치 기반 라우팅의 사용 사례에는 웹사이트 현지화, 콘텐츠 배포 제한, 부하 분산 등이 있습니다.  

These types of records can also be associated with health checks.  
이러한 레코드들은 헬스체크와 연결할 수도 있습니다.  

Imagine a map of Europe with multiple countries.  
유럽 지도를 여러 나라로 나누어 상상해보세요.  

You can define a geolocation record for Germany so that German users are routed to an IP hosting the German version of your application.  
독일 사용자가 독일 버전 애플리케이션이 호스팅된 IP로 라우팅되도록 독일용 지리적 위치 레코드를 정의할 수 있습니다.  

Similarly, users from France can be routed to an IP hosting the French version.  
마찬가지로, 프랑스 사용자는 프랑스 버전 애플리케이션이 호스팅된 IP로 라우팅됩니다.  

For users from any other location, the default IP can serve, for example, the English version of the application.  
기타 지역 사용자는 기본 IP로 라우팅되어 예를 들어 영어 버전을 제공할 수 있습니다.  

---

## Creating Geolocation Records in the Console  
## 콘솔에서 지리적 위치 레코드 생성  

Let's practice creating geolocation records in the AWS console.  
AWS 콘솔에서 지리적 위치 레코드 생성 실습을 해보겠습니다.  

First, create a record with the routing policy set to geolocation.  
먼저, 라우팅 정책을 지리적 위치 기반으로 설정하여 레코드를 생성합니다.  

For example, set the record type to A and link it to the ap-southeast-1 region.  
예를 들어, 레코드 유형을 A로 설정하고 ap-southeast-1 지역과 연결합니다.  

Specify the location as Asia so that any user located in Asia is routed to this EC2 instance.  
위치를 아시아로 지정하면 아시아 사용자는 이 EC2 인스턴스로 라우팅됩니다.  

You may associate a health check if desired and provide a record ID.  
원하면 헬스체크를 연결하고 레코드 ID를 지정할 수 있습니다.  

Next, add another record for the us-east-1 region.  
다음으로 US-east-1 지역용 레코드를 추가합니다.  

Specify the location as the United States country.  
위치를 미국으로 지정합니다.  

Provide a record ID such as "US".  
레코드 ID를 "US"와 같이 지정합니다.  

This demonstrates that you can specify either a whole continent or a specific country for routing.  
이를 통해 전체 대륙 또는 특정 국가 단위로 라우팅을 지정할 수 있음을 보여줍니다.  

Finally, add a default record linked to the eu-central-1 region.  
마지막으로 eu-central-1 지역과 연결된 기본(default) 레코드를 추가합니다.  

Set the location to "default", which means any user not matching Asia or the United States will be routed here.  
위치를 "default"로 설정하면 아시아 또는 미국에 속하지 않는 사용자는 이곳으로 라우팅됩니다.  

Provide a record ID such as "Default EU".  
레코드 ID를 "Default EU"로 지정합니다.  

After creating these records, they will be successfully set up.  
이 레코드들을 생성하면 성공적으로 설정됩니다.  

---

## Testing Geolocation Routing  
## 지리적 위치 라우팅 테스트  

To test the setup, access the URL from your current location.  
설정을 테스트하려면 현재 위치에서 URL에 접속합니다.  

If you are not in the U.S. or Asia, you should be routed to the default eu-central-1 region.  
미국이나 아시아에 있지 않다면 기본 eu-central-1 지역으로 라우팅됩니다.  

This confirms that the default record is working properly.  
기본 레코드가 정상 작동함을 확인할 수 있습니다.  

Change your geographic location using a VPN.  
VPN을 사용하여 지리적 위치를 변경합니다.  

For example, connect to India in Asia.  
예를 들어, 아시아의 인도로 연결합니다.  

Refresh the page, and you should receive a response from the ap-southeast-1 instance.  
페이지를 새로고침하면 ap-southeast-1 인스턴스에서 응답이 반환됩니다.  

If you experience a timeout, it is often due to security group settings blocking HTTP traffic.  
타임아웃이 발생하면 보안 그룹 설정이 HTTP 트래픽을 차단했기 때문일 수 있습니다.  

Check the security group inbound rules in the relevant region (e.g., Singapore for ap-southeast-1).  
관련 지역의 보안 그룹 인바운드 규칙을 확인합니다(예: ap-southeast-1은 싱가포르).  

If the HTTP rule was removed, add it back to allow traffic.  
HTTP 규칙이 제거되었으면 다시 추가하여 트래픽을 허용합니다.  

After updating the security group, refresh the page again to confirm you receive the expected response from the Asia region.  
보안 그룹을 업데이트한 후 페이지를 새로고침하여 아시아 지역에서 예상 응답이 오는지 확인합니다.  

Similarly, connect to a location in the United States and refresh the page.  
마찬가지로, 미국 위치로 연결한 후 페이지를 새로고침합니다.  

You should receive a response from the us-east-1 region.  
us-east-1 지역에서 응답을 받게 됩니다.  

If you connect to a nearby country not specified in the geolocation records, such as Mexico, you will be routed to the default eu-central-1 region.  
지리적 위치 레코드에 지정되지 않은 인근 국가(예: 멕시코)로 연결하면 기본 eu-central-1 지역으로 라우팅됩니다.  

This confirms that the geolocation routing policy is working perfectly, directing users based on their physical location with a fallback default route.  
이를 통해 지리적 위치 라우팅 정책이 정상 작동하며, 물리적 위치 기반 라우팅과 기본 경로(fallback)가 모두 작동함을 확인할 수 있습니다.  

Thank you for following this lecture.  
이번 강의를 따라와 주셔서 감사합니다.  

I hope you found it informative, and I look forward to seeing you in the next lecture.  
유익한 시간이었길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 포인트  

- Routing policies based on geolocation direct users to specific IPs depending on their physical location.  
  지리적 위치 기반 라우팅 정책은 사용자의 물리적 위치에 따라 특정 IP로 라우팅합니다.  

- A default record is essential to handle users from locations not explicitly specified.  
  명시되지 않은 위치 사용자를 처리하려면 기본 레코드가 필수입니다.  

- Geolocation routing is useful for website localization, content restriction, and load balancing.  
  지리적 위치 라우팅은 웹사이트 현지화, 콘텐츠 제한, 부하 분산에 유용합니다.  

- Health checks and security group settings are critical to ensure proper routing and accessibility.  
  올바른 라우팅과 접근성을 위해 헬스체크와 보안 그룹 설정이 중요합니다.  

---

💡 **게임 보상:**

* 🌏 아시아/미국/기본 레코드 생성 = +60 EXP
* 🔄 지리적 위치 라우팅 테스트 = +60 EXP
* ✅ VPN을 통한 위치별 라우팅 검증 = +80 EXP
  **총 보상: 200 EXP + Route 53 Geolocation Expert 뱃지 🏅**
