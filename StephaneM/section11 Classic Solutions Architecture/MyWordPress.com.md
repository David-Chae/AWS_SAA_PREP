# MyWordPress.com  
# MyWordPress.com  

---

## Introduction to MyWordPress.com  
## MyWordPress.com 소개  

In this lecture, we explore the creation of a fully scalable WordPress website named MyWordPress.com.  
이번 강의에서는 MyWordPress.com이라는 완전히 확장 가능한 워드프레스 웹사이트를 만드는 과정을 살펴봅니다.  
→ 워드프레스 사이트를 AWS 상에서 확장 가능한 구조로 설계하는 실습을 한다는 의미입니다.  

WordPress is a very popular platform for building websites.  
워드프레스는 웹사이트를 구축하는 데 매우 인기 있는 플랫폼입니다.  
→ 세계적으로 사용률이 높은 CMS(Content Management System)입니다.  

While hosted WordPress options exist, many users prefer to deploy WordPress on AWS for greater control and scalability.  
호스팅된 워드프레스 옵션이 있지만, 많은 사용자는 더 큰 제어권과 확장성을 위해 AWS에 워드프레스를 배포하는 것을 선호합니다.  
→ 직접 배포하면 커스터마이징과 성능 관리 측면에서 유리합니다.  

Our goal is to ensure that the website correctly displays picture uploads.  
우리의 목표는 웹사이트가 사진 업로드를 올바르게 표시하도록 보장하는 것입니다.  
→ 이미지 업로드 처리 및 표시가 안정적으로 되어야 함을 의미합니다.  

WordPress stores pictures on some drive, and all instances must have access to this data.  
워드프레스는 사진을 특정 드라이브에 저장하며, 모든 인스턴스가 이 데이터에 접근할 수 있어야 합니다.  
→ 인스턴스 간 데이터 공유가 필요하다는 점을 강조합니다.  

Additionally, user data and blog content should be stored in a MySQL database.  
또한, 사용자 데이터와 블로그 콘텐츠는 MySQL 데이터베이스에 저장해야 합니다.  
→ DB 계층은 반드시 별도로 구성해야 합니다.  

We aim to scale this setup globally.  
우리는 이 구성을 전 세계적으로 확장하는 것을 목표로 합니다.  
→ 글로벌 서비스로 확장할 수 있는 구조를 마련하는 것입니다.  

---

## Database Layer with RDS and Aurora  
## RDS와 Aurora를 활용한 데이터베이스 계층  

The first step is to create a database layer using RDS.  
첫 번째 단계는 RDS를 사용하여 데이터베이스 계층을 만드는 것입니다.  
→ 기본 DB 서비스로 RDS를 선택합니다.  

We are familiar with architectures involving RDS in the backend with Multi-AZ deployments.  
우리는 Multi-AZ 배포를 사용하는 백엔드 RDS 아키텍처에 익숙합니다.  
→ 고가용성을 위한 RDS 멀티 AZ 배포 구조입니다.  

To scale further, we can replace this layer with Aurora MySQL, which supports Multi-AZ, read replicas, and even global databases.  
더 확장하기 위해 이 계층을 Multi-AZ, 리드 리플리카, 글로벌 데이터베이스를 지원하는 Aurora MySQL로 교체할 수 있습니다.  
→ Aurora는 고성능, 글로벌 확장을 지원하는 DB 서비스입니다.  

Aurora reduces operational overhead and scales better.  
Aurora는 운영 부담을 줄이고 확장성이 더 뛰어납니다.  
→ 관리 효율성과 성능이 더 우수합니다.  

It also simplifies write operations.  
또한 쓰기 작업을 단순화합니다.  
→ 데이터 입력/갱신이 더 효율적입니다.  

While this is a choice for solutions architects, Aurora is preferred here due to its scalability and ease of use.  
이것은 솔루션 아키텍트의 선택 사항이지만, 여기서는 확장성과 사용 편의성 때문에 Aurora를 선호합니다.  
→ 시험 및 실제 환경에서 Aurora 사용이 더 적합합니다.  

---

## Storing Images with EBS in a Single Instance Setup  
## 단일 인스턴스 구성에서 EBS를 이용한 이미지 저장  

Consider a simple architecture with one EC2 instance and one EBS volume attached in a single availability zone (AZ).  
단일 가용 영역(AZ)에서 하나의 EC2 인스턴스와 하나의 EBS 볼륨이 연결된 단순한 아키텍처를 고려해봅시다.  
→ 가장 기본적인 구조입니다.  

When a user uploads an image, it is stored on the EBS volume attached to that instance.  
사용자가 이미지를 업로드하면 해당 인스턴스에 연결된 EBS 볼륨에 저장됩니다.  
→ 이미지 저장소가 인스턴스에 종속됩니다.  

Reading the image is straightforward since the image resides on the same EBS volume.  
이미지가 동일한 EBS 볼륨에 존재하기 때문에 읽기는 간단합니다.  
→ 단일 서버에서는 문제 없음.  

This setup works well for single-instance deployments.  
이 구성은 단일 인스턴스 배포에 적합합니다.  
→ 하지만 확장성에는 한계가 있습니다.  

---

## Challenges of EBS with Multiple Instances  
## 다중 인스턴스 환경에서의 EBS 문제  

Problems arise when scaling to multiple EC2 instances across different AZs.  
여러 AZ에서 다중 EC2 인스턴스로 확장할 때 문제가 발생합니다.  
→ 확장 시 데이터 공유의 어려움이 생깁니다.  

Each instance has its own EBS volume.  
각 인스턴스는 자체 EBS 볼륨을 가집니다.  
→ 인스턴스 간 저장소 공유가 불가능합니다.  

If an image is uploaded to one instance's EBS volume, it is not accessible from another instance's EBS volume.  
이미지가 특정 인스턴스의 EBS 볼륨에 업로드되면 다른 인스턴스의 EBS 볼륨에서는 접근할 수 없습니다.  
→ 데이터 불일치와 접근 문제 발생.  

This lack of shared storage leads to inconsistencies and access issues, which is problematic for scalable applications.  
이러한 공유 저장소의 부족은 불일치와 접근 문제를 초래하며, 확장 가능한 애플리케이션에 문제가 됩니다.  
→ 따라서 단순 EBS 기반 아키텍처는 확장에 부적합합니다.  

---

## Using EFS for Shared Storage Across Instances  
## 인스턴스 간 공유 스토리지를 위한 EFS 사용  

To solve this, we use Amazon Elastic File System (EFS), a Network File System (NFS) that creates Elastic Network Interfaces (ENIs) in each AZ.  
이를 해결하기 위해, 우리는 각 AZ에 ENI를 생성하는 네트워크 파일 시스템(NFS)인 Amazon Elastic File System(EFS)을 사용합니다.  
→ EFS는 다중 인스턴스 간 공유 스토리지를 제공합니다.  

These ENIs allow all EC2 instances to access the same shared storage.  
이러한 ENI는 모든 EC2 인스턴스가 동일한 공유 스토리지에 접근할 수 있게 합니다.  
→ 인스턴스 간 데이터 일관성을 보장합니다.  

When an image is uploaded, it is stored in EFS.  
이미지가 업로드되면 EFS에 저장됩니다.  
→ 중앙 집중식 저장 방식입니다.  

Any instance can read the image from EFS via its ENI, ensuring consistent access regardless of the instance or AZ.  
어떤 인스턴스든 ENI를 통해 EFS에서 이미지를 읽을 수 있어, 인스턴스나 AZ에 상관없이 일관된 접근을 보장합니다.  
→ 확장성과 안정성이 확보됩니다.  

This architecture enables scalable website storage across multiple EC2 instances and availability zones, allowing all instances to access the same files seamlessly.  
이 아키텍처는 여러 EC2 인스턴스와 가용 영역에 걸쳐 확장 가능한 웹사이트 저장을 가능하게 하며, 모든 인스턴스가 동일한 파일에 원활하게 접근할 수 있도록 합니다.  
→ 고가용성, 고확장성 아키텍처 완성.  

---

## Summary and Cost Considerations  
## 요약 및 비용 고려사항  

To summarize, Aurora MySQL provides a scalable, multi-AZ database solution with read replicas and global database options.  
요약하면, Aurora MySQL은 리드 리플리카와 글로벌 데이터베이스 옵션을 지원하는 확장 가능한 Multi-AZ 데이터베이스 솔루션을 제공합니다.  
→ DB 확장성과 글로벌 서비스에 적합.  

For file storage, EBS volumes are suitable for single-instance applications but do not scale well across multiple instances or AZs.  
파일 저장의 경우, EBS 볼륨은 단일 인스턴스 애플리케이션에는 적합하지만 다중 인스턴스나 AZ 확장에는 적합하지 않습니다.  
→ 기본은 EBS, 확장은 불가.  

EFS offers a distributed file system accessible by multiple instances across AZs, supporting scalable applications.  
EFS는 여러 AZ에 걸쳐 다중 인스턴스에서 접근 가능한 분산 파일 시스템을 제공하여 확장 가능한 애플리케이션을 지원합니다.  
→ EFS는 확장 환경에서 핵심 스토리지 역할을 합니다.  

However, EFS is more expensive than EBS, so architects must weigh the trade-offs between cost and scalability when designing their solutions.  
그러나 EFS는 EBS보다 비용이 더 많이 들기 때문에, 아키텍트는 설계 시 비용과 확장성 간의 균형을 고려해야 합니다.  
→ 비용-성능 최적화를 항상 고려해야 함.  

This concludes the lecture on building a scalable WordPress website architecture.  
이것으로 확장 가능한 워드프레스 웹사이트 아키텍처 구축 강의를 마치겠습니다.  

Thank you for your attention, and see you in the next lecture.  
경청해주셔서 감사합니다. 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- WordPress websites require scalable storage solutions for images and user data.  
- 워드프레스 웹사이트는 이미지 및 사용자 데이터를 위한 확장 가능한 저장소 솔루션이 필요합니다.  

- Aurora MySQL offers better scalability and multi-AZ support compared to traditional RDS.  
- Aurora MySQL은 기존 RDS보다 뛰어난 확장성과 Multi-AZ 지원을 제공합니다.  

- EBS volumes work well for single-instance setups but are problematic when scaling across multiple instances or availability zones.  
- EBS 볼륨은 단일 인스턴스 구성에서는 잘 작동하지만, 다중 인스턴스 또는 AZ 확장 시 문제가 발생합니다.  

- EFS provides a shared network file system accessible by multiple EC2 instances across AZs, enabling scalable and consistent file storage.  
- EFS는 여러 AZ의 EC2 인스턴스에서 접근 가능한 공유 네트워크 파일 시스템을 제공하여 확장 가능하고 일관된 파일 저장을 지원합니다.  

- Cost considerations between EBS and EFS must be balanced against architectural needs and scalability requirements.  
- EBS와 EFS 간의 비용 고려는 아키텍처 요구사항과 확장성 필요성에 맞추어 균형을 맞춰야 합니다.  

