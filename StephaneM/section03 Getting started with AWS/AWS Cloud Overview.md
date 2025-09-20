```md
# AWS Cloud Overview - Regions & AZ  
# AWS 클라우드 개요 - 리전 & 가용 영역  
(이 문서는 AWS의 역사, 인프라 구조, 리전/가용 영역 개념을 설명합니다.)

---

## History of AWS Cloud  
## AWS 클라우드의 역사  
(AWS의 시작과 주요 서비스의 발전 과정을 설명합니다.)

AWS was launched internally at Amazon.com in 2002 because they realized that IT departments could be externalized.  
AWS는 2002년 아마존닷컴 내부에서 시작되었는데, IT 부서를 외부화할 수 있다는 사실을 깨달았기 때문입니다.  
→ 아마존은 내부 IT 인프라를 다른 기업에도 제공할 수 있다고 생각했습니다.  

Their Amazon infrastructure was one of their core strengths, and they thought, "Maybe we can do IT for someone else, for other people."  
아마존의 인프라는 핵심 강점 중 하나였고, “우리가 다른 사람을 위해 IT를 해줄 수 있지 않을까?”라고 생각했습니다.  
→ 인프라를 서비스 형태로 외부에 제공할 가능성을 탐색한 것입니다.  

They launched their first offering publicly, which was SQS, in 2004.  
2004년에 첫 번째 공개 서비스인 SQS(Simple Queue Service)를 출시했습니다.  
→ 메시지 큐 서비스가 AWS의 첫 번째 외부 서비스였습니다.  

In 2006, they expanded their offering and relaunched with the availability of SQS, S3, and EC2.  
2006년에는 SQS, S3, EC2를 포함한 서비스들을 확장하여 다시 출시했습니다.  
→ 본격적으로 클라우드 서비스 사업이 시작된 시점입니다.  

Don't worry, we will see all these services in this course.  
걱정하지 마세요, 이 모든 서비스는 이 과정에서 배우게 됩니다.  
→ 학습 과정에서 각 서비스의 기능을 배웁니다.  

Then they expanded and said, "We don't have to be just in America. We could be in Europe."  
그 후 그들은 “우리는 미국에만 머물 필요가 없다. 유럽에도 갈 수 있다”라고 하며 확장했습니다.  
→ 글로벌 진출의 시작이었습니다.  

Fast forward to today, many applications that used to run, or are still running on AWS include Dropbox, Netflix, Airbnb, and even NASA.  
오늘날에는 드롭박스, 넷플릭스, 에어비앤비, 심지어 NASA까지도 AWS 위에서 운영됩니다.  
→ 현재 AWS는 전 세계 주요 기업과 기관이 사용하는 핵심 플랫폼입니다.  

---

## AWS Today  
## 현재의 AWS  
(시장 점유율과 규모를 설명합니다.)

If you look at the Magic Quadrant from Gartner, you can see that AWS is a leader, and it has been the case for many years.  
가트너의 매직 쿼드런트를 보면 AWS가 오랫동안 리더로 자리하고 있음을 알 수 있습니다.  
→ AWS는 클라우드 시장에서 지속적으로 1위를 유지하고 있습니다.  

AWS now has 90 billion in revenue as of 2023, and it accounts for about 31% of the market in Q1 2024, with Microsoft being second with 25%.  
AWS는 2023년 기준 매출이 900억 달러에 달하며, 2024년 1분기에는 시장 점유율 31%로 1위, 마이크로소프트는 25%로 2위입니다.  
→ AWS는 압도적인 시장 지배력을 가지고 있습니다.  

AWS has been a pioneer and leader of the market for 13 consecutive years and has over 1 million active users.  
AWS는 13년 연속 시장의 선구자이자 리더로 자리하며, 100만 명 이상의 활성 사용자를 보유하고 있습니다.  
→ 시장에서 신뢰성과 규모가 입증된 서비스입니다.  

Learning AWS really sets you up for success in the cloud world.  
AWS를 배우는 것은 클라우드 세계에서 성공하기 위한 발판이 됩니다.  
→ AWS 학습은 IT 전문가에게 필수적인 역량이 됩니다.  

---

## What Can You Build on AWS?  
## AWS에서 무엇을 만들 수 있는가?  
(AWS 활용 사례를 설명합니다.)

Pretty much everything. AWS enables you to build sophisticated and scalable applications applicable to a diverse set of industries.  
거의 모든 것을 만들 수 있습니다. AWS는 다양한 산업에서 정교하고 확장 가능한 애플리케이션을 구축할 수 있게 합니다.  
→ AWS는 범용성과 확장성을 제공합니다.  

Every company has a use case for the cloud. Netflix, McDonald's, 21st Century Fox, and Activision are all using the cloud.  
모든 기업은 클라우드 활용 사례를 가지고 있습니다. 넷플릭스, 맥도날드, 21세기 폭스, 액티비전도 클라우드를 사용합니다.  
→ 산업과 분야를 막론하고 활용 가능합니다.  

Use cases include transferring your enterprise IT, using the cloud as backup and storage, performing big data analytics, hosting websites, creating backends for mobile and social applications, or running entire gaming servers on the cloud.  
활용 사례로는 기업 IT 이전, 클라우드를 백업 및 저장소로 활용, 빅데이터 분석, 웹사이트 호스팅, 모바일/소셜 앱 백엔드 구축, 전체 게임 서버 운영 등이 있습니다.  
→ 다양한 IT 인프라 활용이 가능합니다.  

The applications are endless.  
적용 사례는 끝이 없습니다.  
→ 클라우드의 잠재력은 무궁무진합니다.  

---

## AWS Global Infrastructure  
## AWS 글로벌 인프라  
(글로벌 인프라 구조를 설명합니다.)

AWS is global, consisting of AWS regions, availability zones, data centers, edge locations, and points of presence.  
AWS는 리전, 가용 영역, 데이터 센터, 엣지 로케이션, 접속 지점으로 구성된 글로벌 서비스입니다.  
→ AWS는 전 세계적으로 분산된 인프라를 운영합니다.  

These components can be represented on a global map.  
이 구성 요소들은 세계 지도에 표시될 수 있습니다.  
→ 인프라의 전 세계적 배치를 시각적으로 확인할 수 있습니다.  

On the AWS website, you can see that AWS has multiple regions around the world, marked in orange.  
AWS 웹사이트에서 오렌지색으로 표시된 여러 글로벌 리전을 볼 수 있습니다.  
→ 리전은 전 세계에 분산되어 있습니다.  

Examples include Paris, Spain, Ohio, Sao Paulo, Cape Town, Mumbai, and many others.  
예로 파리, 스페인, 오하이오, 상파울루, 케이프타운, 뭄바이 등이 있습니다.  
→ 다양한 대륙과 도시에서 서비스됩니다.  

AWS truly is a global service.  
AWS는 진정한 글로벌 서비스입니다.  
→ 어디서든 접근 가능한 클라우드 플랫폼입니다.  

Each region is connected through a private AWS network.  
각 리전은 AWS 전용 네트워크로 연결됩니다.  
→ 안정적이고 빠른 통신이 보장됩니다.  

Within each region, such as Cape Town, there are blue dots representing availability zones, which will be described in the next section.  
각 리전(예: 케이프타운)에는 가용 영역을 나타내는 파란 점이 있으며, 이는 다음 섹션에서 설명됩니다.  
→ 리전 내부 구성 단위인 가용 영역이 있습니다.  

The key takeaway is that AWS is truly global, and you can leverage the infrastructure of a cloud provider to make your application global.  
핵심은 AWS가 진정한 글로벌 서비스이며, 이를 활용해 애플리케이션을 글로벌하게 배포할 수 있다는 점입니다.  
→ 글로벌 비즈니스를 손쉽게 구축할 수 있습니다. 


## AWS Regions  
AWS Regions  
AWS 리전  

Regions are located all around the world, as seen on the map.  
리전은 지도에서 볼 수 있듯이 전 세계에 위치해 있습니다.  
→ AWS의 서비스 제공 거점은 특정 도시/지역 단위로 구분됩니다.  

Each region has a name, such as US-east-1 or EU-West-3, which maps to a code used in the AWS console.  
각 리전은 US-east-1 또는 EU-West-3와 같은 이름을 가지며, 이는 AWS 콘솔에서 사용하는 코드에 대응합니다.  
→ 리전은 고유 코드로 식별되며, 콘솔/CLI/API에서 이 코드로 구분합니다.  

A region is essentially a cluster of data centers located near each other, for example, in Ohio, Singapore, Sydney, or Tokyo.  
리전은 본질적으로 서로 가까이 모여 있는 데이터 센터들의 집합으로, 예를 들어 오하이오, 싱가포르, 시드니, 도쿄 등에 위치합니다.  
→ 리전은 여러 데이터 센터 묶음을 의미합니다.  

Most AWS services are scoped to a specific region.  
대부분의 AWS 서비스는 특정 리전에 종속됩니다.  
→ 예를 들어 EC2 인스턴스를 US-east-1에 생성하면, ap-southeast-2(시드니)와는 독립적인 리소스로 취급됩니다.  

This means that if you use a service in one region and try to use it in another, it will be treated as a new instance of the service.  
즉, 한 리전에서 사용하던 서비스를 다른 리전에서 사용하려 하면, 완전히 새로운 서비스 인스턴스로 간주됩니다.  
→ 리전 간 자원은 공유되지 않습니다.  

---

## Choosing an AWS Region  
Choosing an AWS Region  
AWS 리전 선택하기  

When launching a new application, deciding where to deploy it depends on several factors:  
새 애플리케이션을 배포할 때, 어디에 배포할지는 몇 가지 요인에 따라 결정됩니다.  
→ 리전 선택은 단순히 위치 문제가 아니라, 기술적·법적 요구 조건과도 연결됩니다.  

**Compliance:** Some governments require data to remain local to the country. For example, data in France may have to stay in France, so you should launch your application in the French region.  
**컴플라이언스:** 일부 정부는 데이터가 자국 내에만 저장되도록 요구합니다. 예를 들어 프랑스의 경우 데이터는 프랑스 리전에 저장해야 합니다.  
→ 데이터 거버넌스, 법적 규제가 중요한 요소입니다.  

**Latency:** Deploying your application close to your users reduces latency. For instance, if most users are in America, deploying in America is preferable to deploying in Australia.  
**지연 시간:** 애플리케이션을 사용자 가까이에 배포하면 지연 시간이 줄어듭니다. 예를 들어 대부분의 사용자가 미국에 있으면 미국 리전에 배포하는 것이 호주 리전에 배포하는 것보다 좋습니다.  
→ 사용자 경험에 직결되는 요소입니다.  

**Service Availability:** Not all regions have all services. You need to ensure the region you choose supports the services your application requires.  
**서비스 가용성:** 모든 리전이 모든 서비스를 제공하지는 않습니다. 따라서 필요한 서비스가 선택한 리전에 있는지 확인해야 합니다.  
→ 최신 기능은 보통 미국 리전부터 제공됩니다.  

**Pricing:** Pricing varies between regions. Consult the services pricing pages to understand cost differences, which may impact your deployment decision.  
**가격:** 가격은 리전에 따라 다릅니다. 서비스 가격 페이지를 참고하여 비용 차이를 이해해야 하며, 이는 배포 결정에 영향을 줄 수 있습니다.  
→ 동일한 서비스라도 지역별 환율·운영비에 따라 가격이 다릅니다.  

---
```
