# Amazon Elastic File System (EFS) Overview
# 아마존 엘라스틱 파일 시스템(EFS) 개요
> Amazon EFS의 기본 개념을 소개합니다.  
> 설명: EFS에 대한 전체 개요와 기능을 다루는 문서의 제목입니다.

## Introduction to Amazon EFS
## 아마존 EFS 소개
> Amazon Elastic File System (EFS) is a managed Network File System (NFS). Because it is a network file system, it can be mounted on many EC2 instances. These EC2 instances can also be located in different availability zones, which is the core strength of EFS.
> 아마존 엘라스틱 파일 시스템(EFS)은 관리형 네트워크 파일 시스템(NFS)입니다. 네트워크 파일 시스템이므로 여러 EC2 인스턴스에 마운트할 수 있습니다. 이 EC2 인스턴스들은 서로 다른 가용 영역에 위치할 수도 있으며, 이것이 EFS의 핵심 강점입니다.
> 설명: EFS의 기본 특성과 강점을 강조합니다.

> EFS is highly available and very scalable. However, it is more expensive, costing about three times as much as a GP2 EBS volume. The pricing model is pay-per-use, so you do not have to provision capacity in advance.
> EFS는 고가용성과 높은 확장성을 제공합니다. 그러나 비용이 더 비싸며, GP2 EBS 볼륨의 약 3배 정도입니다. 가격 모델은 사용량 기반(pay-per-use)이므로 사전에 용량을 프로비저닝할 필요가 없습니다.
> 설명: EFS의 장점과 단점, 비용 구조를 명확히 합니다.

## Architecture and Connectivity
## 아키텍처 및 연결
> You have your EFS file system surrounded by a security group. Multiple EC2 instances, for example in the US East-1A, US East-1B, or US East-1C availability zones, can connect simultaneously to the same network file system through EFS.
> EFS 파일 시스템은 보안 그룹(Security Group)으로 보호됩니다. 예를 들어 US East-1A, US East-1B, US East-1C 가용 영역에 있는 여러 EC2 인스턴스가 동시에 동일한 네트워크 파일 시스템에 연결할 수 있습니다.
> 설명: EFS의 네트워크 연결 구조와 보안 그룹 역할을 설명합니다.

## Use Cases and Compatibility
## 사용 사례 및 호환성
> EFS is suitable for content management, web serving, data sharing, and applications like WordPress. Internally, it uses the NFS protocol. To control access, you must configure a security group.
> EFS는 콘텐츠 관리, 웹 서버, 데이터 공유, WordPress와 같은 애플리케이션에 적합합니다. 내부적으로 NFS 프로토콜을 사용하며, 접근 제어를 위해 보안 그룹을 구성해야 합니다.
> 설명: EFS 활용 가능 분야와 내부 프로토콜, 보안 설정 요구 사항을 설명합니다.

> It is important to note that EFS is compatible only with Linux-based AMIs and not with Windows. Encryption at rest can be enabled using KMS. EFS uses the POSIX file system standard and provides a standard file API.
> EFS는 Linux 기반 AMI에서만 호환되며, Windows에서는 사용할 수 없습니다. 저장 데이터 암호화는 KMS를 통해 활성화할 수 있습니다. EFS는 POSIX 파일 시스템 표준을 사용하며, 표준 파일 API를 제공합니다.
> 설명: 호환 OS, 암호화 옵션, 표준 준수 여부를 명확히 합니다.

## Scalability and Performance
## 확장성 및 성능
> One of the advantages of EFS is that you do not need to plan capacity in advance. The file system scales automatically and you pay per gigabyte of data used.
> EFS의 장점 중 하나는 사전에 용량을 계획할 필요가 없다는 것입니다. 파일 시스템이 자동으로 확장되며 사용한 데이터 양에 따라 비용을 지불합니다.
> 설명: 자동 확장 기능과 비용 구조를 설명합니다.

> EFS supports thousands of concurrent NFS clients and throughput exceeding 10 gigabytes per second. It can grow to petabyte scale automatically.
> EFS는 수천 개의 동시 NFS 클라이언트를 지원하며 초당 10GB 이상의 처리량을 제공합니다. 페타바이트 규모까지 자동으로 확장될 수 있습니다.
> 설명: 동시 접속 지원 규모와 성능 한계를 강조합니다.

> You can set the performance mode at the time of EFS creation. The options include:
> EFS 생성 시 성능 모드를 설정할 수 있으며, 옵션은 다음과 같습니다:
> 설명: 성능 모드 설정 방법을 안내합니다.

- General Purpose (default): Suitable for latency-sensitive use cases such as web servers and content management systems.  
- 일반 용도(기본값): 웹 서버나 콘텐츠 관리 시스템처럼 지연에 민감한 경우에 적합합니다.  
> 설명: 기본 성능 모드 특징

- Max I/O: Provides higher throughput with higher latency, ideal for big data applications and media processing due to its high parallelism.  
- 최대 I/O: 높은 처리량과 상대적으로 높은 지연을 제공하며, 병렬성이 높은 빅데이터 및 미디어 처리에 적합합니다.  
> 설명: 고처리량, 병렬 처리용 성능 모드

## Throughput Modes
## 처리량 모드
> EFS offers different throughput modes:
> EFS는 다양한 처리량 모드를 제공합니다:
> 설명: 처리량 조정 옵션 안내

- Bursting: For example, with one terabyte of storage, you get 50 megabytes per second plus bursts up to 100 megabytes per second.  
- 버스팅(Bursting): 예를 들어 1TB 저장소에서는 초당 50MB 기본 처리량과 최대 100MB 버스트를 제공합니다.  
> 설명: 버스팅 모드 동작 방식 설명

- Provisioned: Allows setting throughput independently of storage size, such as one gigabyte per second for one terabyte of storage.  
- 프로비저닝(Provisioned): 저장 용량과 독립적으로 처리량을 설정할 수 있으며, 예를 들어 1TB 저장소에 초당 1GB 처리량을 지정할 수 있습니다.  
> 설명: 고정 처리량 설정 가능 모드

- Elastic: Automatically scales throughput up and down based on workload, supporting up to three gigabytes per second for reads and one gigabyte per second for writes. This mode is ideal for unpredictable workloads.  
- 탄력적(Elastic): 워크로드에 따라 처리량을 자동으로 확장 및 축소하며, 읽기 최대 3GB/s, 쓰기 최대 1GB/s를 지원합니다. 예측 불가능한 워크로드에 적합합니다.  
> 설명: 워크로드 기반 자동 처리량 조정 모드

## Storage Classes and Lifecycle Management
## 스토리지 클래스 및 라이프사이클 관리
> EFS provides storage tiers with lifecycle management features to move files between tiers based on access patterns:
> EFS는 파일 접근 패턴에 따라 파일을 스토리지 계층 간 자동 이동시키는 라이프사이클 관리 기능이 있는 스토리지 계층을 제공합니다:
> 설명: 접근 빈도 기반 계층화 기능 안내

- Standard Tier: For frequently accessed files.  
- 표준(Standard) 계층: 자주 접근하는 파일용  
> 설명: 기본 계층 사용 목적

- EFS-Infrequent Access (EFS-IA): For infrequently accessed files, offering lower storage costs but with retrieval costs.  
- EFS-IA(저빈도 접근): 자주 접근하지 않는 파일용으로, 저장 비용은 낮지만 조회 비용이 발생합니다.  
> 설명: 비용 절감용 저빈도 계층

- Archive Storage Tier: For rarely accessed data, such as files accessed only a few times a year, providing significant storage cost savings.  
- 아카이브(Archive) 계층: 연간 몇 회만 접근하는 파일과 같이 거의 접근하지 않는 데이터용으로, 저장 비용을 크게 절감할 수 있습니다.  
> 설명: 거의 사용하지 않는 데이터 비용 최적화

> Lifecycle policies can be configured to automatically move files to appropriate tiers after a specified number of days. For example, files not accessed for 60 days can be moved from the standard tier to EFS-IA.
> 라이프사이클 정책을 설정하여 지정한 일수 이후 파일을 자동으로 적절한 계층으로 이동시킬 수 있습니다. 예를 들어 60일간 접근하지 않은 파일은 표준 계층에서 EFS-IA로 이동시킬 수 있습니다.
> 설명: 자동 계층 이동 정책 예시

## Availability and Durability
## 가용성과 내구성
> The standard storage class is suitable for multi-availability zone setups, providing resilience to disasters for production workloads.
> 표준 스토리지 클래스는 다중 가용 영역 구성에 적합하며, 프로덕션 워크로드의 재해 복원력을 제공합니다.
> 설명: 표준 계층 활용 시 고가용성 강조

> For development or cost-sensitive scenarios, the One Zone storage class offers storage within a single availability zone with backup compatibility and support for the IA storage tier.
> 개발 환경이나 비용 민감 시나리오에서는 One Zone 스토리지 클래스가 단일 가용 영역 내 저장소를 제공하며, 백업 호환성과 IA 계층 지원을 제공합니다.
> 설명: 비용 최적화용 단일 영역 스토리지

> Using the appropriate EFS storage classes can yield up to 90% cost savings.
> 적절한 EFS 스토리지 계층 사용 시 최대 90%까지 비용 절감이 가능합니다.
> 설명: 계층별 비용 최적화 효과 강조

## Conclusion
## 결론
> Amazon EFS is a versatile, scalable, and highly available network file system designed for Linux-based environments. Its flexible performance and storage options make it suitable for a wide range of workloads, from web serving to big data applications, with cost optimization through lifecycle management and storage tiers.
> Amazon EFS는 Linux 기반 환경용으로 설계된 다목적, 확장 가능, 고가용성 네트워크 파일 시스템입니다. 유연한 성능 및 스토리지 옵션을 통해 웹 서버부터 빅데이터 애플리케이션까지 다양한 워크로드에 적합하며, 라이프사이클 관리 및 스토리지 계층을 통한 비용 최적화가 가능합니다.
> 설명: EFS의 전반적 장점과 적용 범위를 요약합니다.

## Key Takeaways
## 핵심 요약
> Amazon EFS is a managed NFS network file system that can be mounted on multiple EC2 instances across different availability zones.
> Amazon EFS는 관리형 NFS 네트워크 파일 시스템으로, 서로 다른 가용 영역에 있는 여러 EC2 인스턴스에 마운트할 수 있습니다.
> 설명: 핵심 특징 요약 1

> EFS offers high availability, scalability, and pay-per-use pricing without the need to provision capacity in advance.
> EFS는 고가용성, 확장성, 사용량 기반 요금제를 제공하며, 사전 용량 프로비저닝이 필요 없습니다.
> 설명: 핵심 특징 요약 2

> It supports Linux-based AMIs only, provides encryption at rest via KMS, and uses POSIX standard file APIs.
> Linux 기반 AMI만 지원하며, KMS를 통한 저장 데이터 암호화 제공, POSIX 표준 파일 API 사용  
> 설명: OS 호환성, 암호화, 표준 API 요약

> Various performance modes, throughput modes, and storage classes allow customization for different workloads and cost optimization.
> 다양한 성능 모드, 처리량 모드, 스토리지 클래스는 워크로드에 맞춘 맞춤화와 비용 최적화를 가능하게 합니다.
> 설명: 성능/처리량/스토리지 선택 옵션 요약
