```markdown
# Application Migration Service (MGN)  
# 애플리케이션 마이그레이션 서비스 (MGN)  

🎮 게임보상: "Cloud Migration Apprentice" +500 XP  

---

## Introduction to Cloud Migration Use Cases  
## 클라우드 마이그레이션 사용 사례 소개  

There are two primary use cases when moving to the cloud.  
클라우드로 이전할 때 주요 사용 사례는 두 가지가 있습니다.  

First, you may want to start fresh and leverage the cloud directly.  
첫 번째는 새로 시작하여 클라우드를 직접 활용하고자 하는 경우입니다.  

In this scenario, migration is not necessary.  
이 경우에는 마이그레이션이 필요하지 않습니다.  

However, if you have on-premises servers and data centers and want to migrate to the cloud, you need to plan your migration carefully.  
하지만 온프레미스 서버와 데이터 센터가 있고 이를 클라우드로 이전하고자 한다면, 마이그레이션 계획을 신중히 세워야 합니다.  

---

## Planning Migration with AWS Application Discovery Service  
## AWS Application Discovery Service로 마이그레이션 계획  

To plan your migration, you can use the AWS Application Discovery Service.  
마이그레이션 계획을 세우기 위해 AWS Application Discovery Service를 사용할 수 있습니다.  

This service scans your servers and gathers important information such as server utilization data and dependency mapping.  
이 서비스는 서버를 스캔하고 서버 사용량 데이터 및 종속성 매핑과 같은 중요한 정보를 수집합니다.  

These insights are crucial to understand how to migrate and determine what to migrate first.  
이러한 정보는 마이그레이션 방법을 이해하고 무엇을 먼저 이전할지 결정하는 데 매우 중요합니다.  

---

## Types of Discovery Methods  
## 디스커버리 방법 유형  

There are two types of migration discovery you can perform:  
마이그레이션 디스커버리는 두 가지 방법으로 수행할 수 있습니다.  

### Agentless Discovery using a Connector  
### 커넥터를 사용하는 에이전트 없는 디스커버리  

This method provides information about your virtual machines, including configuration and performance history such as CPU, memory, and disk usage.  
이 방법은 CPU, 메모리, 디스크 사용량 등 구성과 성능 기록을 포함한 가상 머신 정보를 제공합니다.  

### Agent-based Discovery using an Application Discovery Agent  
### 애플리케이션 디스커버리 에이전트를 사용하는 에이전트 기반 디스커버리  

This approach offers more detailed updates and information from within your virtual machines, including system configuration, performance metrics, running processes, and detailed network connection data.  
이 방법은 가상 머신 내부에서 시스템 구성, 성능 지표, 실행 중인 프로세스, 상세한 네트워크 연결 데이터 등 더 자세한 정보를 제공합니다.  

This is particularly useful for dependency mapping.  
특히 종속성 매핑에 유용합니다.  

---

## Viewing Discovery Results in AWS Migration Hub  
## AWS Migration Hub에서 디스커버리 결과 보기  

All the data collected by the Application Discovery Service can be viewed within the AWS Migration Hub.  
Application Discovery Service가 수집한 모든 데이터는 AWS Migration Hub에서 확인할 수 있습니다.  

This service helps you map out what needs to be moved and how the components are interconnected.  
이 서비스는 무엇을 이전해야 하는지, 구성 요소가 어떻게 연결되어 있는지 매핑하는 데 도움을 줍니다.  

---

## Moving to AWS with Application Migration Service (MGN)  
## Application Migration Service (MGN)를 사용하여 AWS로 이전  

Once you have planned your migration, the simplest way to move from on-premises to AWS is by using the AWS Application Migration Service, also known as MGN.  
마이그레이션 계획이 완료되면, 온프레미스에서 AWS로 이전하는 가장 간단한 방법은 AWS Application Migration Service(MGN)를 사용하는 것입니다.  

This service was formerly called CloudEndure Migration but has since been replaced.  
이 서비스는 이전에 CloudEndure Migration이라고 불렸으나 지금은 MGN으로 대체되었습니다.  

MGN enables rehosting, commonly referred to as a lift-and-shift solution.  
MGN은 일반적으로 리프트 앤 시프트(lift-and-shift) 솔루션이라 불리는 리호스팅을 가능하게 합니다.  

It allows you to convert physical servers, virtual machines, or other cloud services to run natively on AWS.  
물리 서버, 가상 머신 또는 다른 클라우드 서비스를 AWS에서 네이티브로 실행할 수 있도록 변환합니다.  

---

## How AWS Application Migration Service Works  
## AWS Application Migration Service 작동 방식  

Suppose you have a corporate data center with operating systems, applications, and databases running on disks.  
기업 데이터 센터에 운영체제, 애플리케이션, 데이터베이스가 디스크에서 실행 중이라고 가정합니다.  

By running the Application Migration Service, you install a replication agent on your data center servers.  
Application Migration Service를 실행하면, 데이터 센터 서버에 복제 에이전트를 설치합니다.  

This agent performs continuous replication of your disks to AWS, storing the data on low-cost EC2 instances and EBS volumes.  
이 에이전트는 디스크를 AWS로 지속적으로 복제하며, 데이터를 저비용 EC2 인스턴스와 EBS 볼륨에 저장합니다.  

---

## Cutover Process  
## 컷오버 과정  

When you are ready to perform a cutover, you can transition from the staging environment to production.  
컷오버를 수행할 준비가 되면 스테이징 환경에서 프로덕션으로 전환할 수 있습니다.  

At this point, you can select a larger EC2 instance size and EBS volumes that match your required performance.  
이때 필요한 성능에 맞는 더 큰 EC2 인스턴스와 EBS 볼륨을 선택할 수 있습니다.  

The process involves replicating data continuously and then performing a cutover at the appropriate time, making it the simplest way to migrate.  
이 과정은 데이터를 지속적으로 복제한 뒤 적절한 시점에 컷오버를 수행하는 것으로, 가장 간단한 마이그레이션 방법입니다.  

---

## Benefits of AWS Application Migration Service  
## AWS Application Migration Service의 장점  

This service supports a wide range of platforms, operating systems, and databases.  
이 서비스는 다양한 플랫폼, 운영체제, 데이터베이스를 지원합니다.  

It offers minimal downtime during migration and reduces costs by automating the process, eliminating the need to hire complex engineering resources.  
마이그레이션 중 다운타임이 최소화되며, 프로세스를 자동화해 복잡한 엔지니어링 리소스를 고용할 필요 없이 비용을 절감할 수 있습니다.  

---

## Conclusion  
## 결론  

The AWS Application Migration Service provides an efficient and automated way to migrate your on-premises workloads to AWS with minimal downtime and reduced complexity.  
AWS Application Migration Service는 다운타임을 최소화하고 복잡성을 줄이면서 온프레미스 워크로드를 AWS로 효율적이고 자동화된 방식으로 이전할 수 있도록 합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Application Discovery Service helps plan cloud migrations by gathering server utilization and dependency data.  
- AWS Application Discovery Service는 서버 사용량과 종속성 데이터를 수집하여 클라우드 마이그레이션 계획에 도움을 줍니다.  

- Two discovery methods exist: Agentless Discovery using a Connector and Agent-based Discovery with an Application Discovery Agent.  
- 디스커버리 방법은 두 가지가 있습니다: 커넥터를 사용하는 에이전트 없는 디스커버리와 Application Discovery Agent를 사용하는 에이전트 기반 디스커버리.  

- AWS Migration Hub provides a centralized view of migration data collected.  
- AWS Migration Hub는 수집된 마이그레이션 데이터를 중앙에서 확인할 수 있습니다.  

- AWS Application Migration Service (MGN) enables lift-and-shift migration with continuous replication and minimal downtime.  
- AWS Application Migration Service(MGN)는 지속적 복제와 최소 다운타임으로 리프트 앤 시프트 마이그레이션을 가능하게 합니다.  
```
