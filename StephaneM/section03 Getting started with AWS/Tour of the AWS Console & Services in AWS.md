```markdown
# Tour of the AWS Console & Services in AWS  
# AWS 콘솔 및 서비스 둘러보기  
→ AWS 콘솔 홈 화면과 서비스 탐색 방법을 소개하는 강의입니다.  

Welcome to the AWS Console Home. This page offers a variety of functionalities to explore.  
AWS 콘솔 홈에 오신 것을 환영합니다. 이 페이지에서는 다양한 기능을 탐색할 수 있습니다.  
→ 콘솔 홈은 시작 지점으로, 여러 기능과 정보를 제공합니다.  

---

## Region Selector  
## 리전 선택기  
→ 콘솔 우측 상단에서 지역(Region)을 선택할 수 있습니다.  

At the top right corner of your screen, you will find the region selector. Currently, it is set to Northern Virginia, US East 1.  
화면 오른쪽 상단에 리전 선택기가 있으며, 현재는 미국 동부 1, 버지니아 북부로 설정되어 있습니다.  
→ AWS는 여러 지역을 지원하며, 기본값은 US East 1입니다.  

For this course, it is recommended to choose a region geographically close to you to minimize latency.  
이 강의에서는 지연 시간을 줄이기 위해 지리적으로 가까운 리전을 선택하는 것이 권장됩니다.  
→ 물리적으로 가까운 리전을 고르면 성능이 개선됩니다.  

For example, if you are in Europe, you might select EU West 1, which corresponds to Ireland.  
예를 들어 유럽에 있다면, 아일랜드에 해당하는 EU West 1을 선택할 수 있습니다.  
→ 유럽 사용자에게 적합한 예시.  

If you are in Africa near Cape Town, you can select that region.  
아프리카 케이프타운 근처에 있다면, 해당 리전을 선택할 수 있습니다.  
→ 아프리카 사용자에게 적합한 예시.  

Note that you do not have to be physically in the region to use it; choose the region that makes the most sense for your needs.  
실제로 해당 지역에 있지 않아도 리전을 사용할 수 있으며, 필요에 가장 적합한 리전을 선택하면 됩니다.  
→ 반드시 거주지와 동일할 필요는 없고, 목적에 맞는 리전을 고르면 됩니다.  

---

## Console Home Features  
## 콘솔 홈 기능  
→ 콘솔 홈은 최근 사용 서비스와 계정 정보를 제공합니다.  

Below the region selector, you will see a list of recently visited services. This list may be empty if you have not used any services yet.  
리전 선택기 아래에는 최근에 사용한 서비스 목록이 표시됩니다. 아직 서비스를 사용하지 않았다면 비어 있을 수 있습니다.  
→ 학습 초반에는 비어 있을 수 있지만, 점점 채워집니다.  

Additionally, the bottom of the page provides information about AWS health issues, cost and usage details for your account, tutorials to help you build solutions, and more.  
또한 페이지 하단에는 AWS 상태 문제, 계정 비용 및 사용량 정보, 솔루션 구축을 돕는 튜토리얼 등이 제공됩니다.  
→ 콘솔 홈은 단순 진입점이 아니라 다양한 리소스를 제공합니다.  

Note that the AWS Console Home page has evolved significantly over the past two years and may look different depending on when you access it.  
지난 2년 동안 AWS 콘솔 홈은 크게 발전했으며, 접속 시기에 따라 다르게 보일 수 있습니다.  
→ AWS는 UI와 기능을 자주 업데이트합니다.  

---

## Navigating AWS Services  
## AWS 서비스 탐색  
→ AWS 서비스는 메뉴 또는 검색으로 탐색할 수 있습니다.  

To explore AWS services, click on "Services" at the top left of the console.  
AWS 서비스를 탐색하려면 콘솔 왼쪽 상단의 "Services"를 클릭하세요.  
→ 모든 서비스는 이 메뉴에서 접근할 수 있습니다.  

You can browse services either alphabetically or by category.  
서비스는 알파벳 순서 또는 카테고리별로 탐색할 수 있습니다.  
→ 서비스가 많기 때문에 분류 탐색이 유용합니다.  

For example, under the "Compute" category, you will find all compute-related services.  
예를 들어, "Compute" 카테고리에는 모든 컴퓨팅 관련 서비스가 있습니다.  
→ 카테고리별 그룹화 예시.  

Over time, you will become familiar with these services and will not need to navigate this page frequently.  
시간이 지나면 서비스에 익숙해져 이 페이지를 자주 탐색하지 않아도 됩니다.  
→ 점차 서비스 이름을 직접 검색하게 됩니다.  

Another useful feature is the search bar, where you can type the name of a service, such as "Route 53," and receive matching results.  
또 다른 유용한 기능은 검색창으로, "Route 53" 같은 서비스 이름을 입력하면 관련 결과가 표시됩니다.  
→ 검색은 빠른 접근 방법입니다.  

This search also includes features, blogs, knowledge articles, and documentation related to your query, allowing you to jump directly to relevant content.  
이 검색은 기능, 블로그, 지식 글, 문서도 포함해 직접 관련 콘텐츠로 이동할 수 있습니다.  
→ 서비스뿐 아니라 학습 리소스도 함께 검색됩니다.  

---

## Global vs. Regional Services  
## 글로벌 서비스와 리전 서비스  
→ AWS 서비스는 전역(Global)과 지역(Region)으로 나뉩니다.  

Some AWS services are global, meaning they do not require region selection.  
일부 AWS 서비스는 글로벌로, 리전 선택이 필요하지 않습니다.  
→ 글로벌 서비스는 어디서든 동일합니다.  

For instance, when accessing the Route 53 console, you will notice "Global" displayed at the top right, indicating that the service's view is consistent regardless of your selected region.  
예를 들어, Route 53 콘솔에 접속하면 오른쪽 상단에 "Global"이 표시되며, 어떤 리전을 선택하든 동일한 화면을 제공합니다.  
→ Route 53은 글로벌 서비스의 대표적 사례입니다.  

However, most services, such as EC2, are region-specific.  
그러나 대부분의 서비스(예: EC2)는 리전별로 구분됩니다.  
→ EC2 같은 서비스는 리전마다 별도로 관리됩니다.  

For example, if you select the Ireland region, the EC2 console will display resources specific to that region.  
예를 들어 아일랜드 리전을 선택하면, EC2 콘솔은 해당 리전의 리소스를 표시합니다.  
→ 리전별 독립적 리소스 관리.  

If you switch to another region, such as Canada, the resources shown will differ accordingly.  
캐나다 리전으로 전환하면, 표시되는 리소스도 달라집니다.  
→ 리전을 바꾸면 새로운 환경으로 이동하는 것과 같습니다.  

It is important to remain within the same region throughout this course to maintain consistency.  
이 강의에서는 일관성을 유지하기 위해 동일한 리전 내에 머무는 것이 중요합니다.  
→ 실습 혼동을 줄이려면 같은 리전을 계속 사용하세요.  

---

## AWS Global Infrastructure  
## AWS 글로벌 인프라  
→ AWS는 전 세계 리전과 서비스 제공 현황을 공개합니다.  

You can find detailed information about AWS's global infrastructure by searching for "AWS global infrastructure" online.  
"AWS global infrastructure"를 온라인에서 검색하면 AWS의 글로벌 인프라에 대한 상세 정보를 찾을 수 있습니다.  
→ 공식 자료를 통해 최신 인프라 현황을 확인할 수 있습니다.  

This resource provides insights into service availability by region.  
이 자료는 리전별 서비스 가용성을 제공합니다.  
→ 각 리전에서 어떤 서비스가 가능한지 확인 가능합니다.  

For example, if a service discussed in the course is not available in your selected region, you can consult this information to determine which regions support that service.  
예를 들어 강의에서 다루는 서비스가 선택한 리전에 없다면, 이 자료를 통해 어떤 리전에서 지원하는지 확인할 수 있습니다.  
→ 특정 서비스 사용을 위해 리전을 전환해야 할 수 있습니다.  

This is particularly useful if you need to switch regions in the console to access specific services, as not all AWS services are available in every region.  
모든 AWS 서비스가 모든 리전에서 제공되는 것은 아니므로, 특정 서비스를 위해 리전을 전환해야 할 때 유용합니다.  
→ 서비스 가용성은 리전마다 다릅니다.  

---

## Summary  
## 요약  
→ 이번 강의에서 다룬 주요 학습 포인트 정리입니다.  

In this lecture, we covered how to navigate the AWS Console Home, select appropriate regions, browse and search for services, understand the distinction between global and regional services, and utilize the AWS Global Infrastructure information to verify service availability.  
이번 강의에서는 AWS 콘솔 홈 탐색, 적절한 리전 선택, 서비스 탐색 및 검색, 글로벌 서비스와 리전 서비스의 차이, 그리고 AWS 글로벌 인프라 정보를 활용해 서비스 가용성을 확인하는 방법을 다뤘습니다.  
→ 학습 포인트 종합 정리.  

---

## Key Takeaways  
## 핵심 요약  
→ 반드시 기억해야 할 부분입니다.  

- Selecting the AWS region closest to your geographic location reduces latency.  
- 지리적으로 가까운 AWS 리전을 선택하면 지연 시간이 줄어듭니다.  
→ 성능 최적화 포인트.  

- The AWS Console Home page provides quick access to recently used services, health status, cost information, and tutorials.  
- AWS 콘솔 홈은 최근 서비스, 상태, 비용 정보, 튜토리얼에 빠르게 접근할 수 있습니다.  
→ 콘솔 홈의 주요 기능.  

- AWS services can be browsed alphabetically, by category, or searched directly using the search bar.  
- AWS 서비스는 알파벳순, 카테고리별, 또는 검색창을 통해 탐색할 수 있습니다.  
→ 탐색 방법 요약.  

- Some AWS services, like Route 53, are global and do not require region selection, while others, like EC2, are region-specific.  
- Route 53 같은 서비스는 글로벌이지만, EC2 같은 서비스는 리전별로 구분됩니다.  
→ 서비스 특성에 따른 분류.  

- The AWS Global Infrastructure page helps verify service availability by region, which is important for hands-on exercises.  
- AWS 글로벌 인프라 페이지는 리전별 서비스 가용성을 확인할 수 있어 실습에 중요합니다.  
→ 실습 준비에 필요한 핵심 리소스.  
```

---

✅ 게임보상 : 경험치 +70 (AWS 콘솔 숙련도 +1)
👉 다음 강의로 넘어갈 준비 완료!
