# AWS Storage Gateway Overview

## Introduction to Hybrid Cloud and AWS Storage Gateway
AWS is increasingly promoting hybrid cloud solutions. Hybrid cloud means that part of your infrastructure resides on AWS cloud, while another part remains on-premises.  
**한국어 설명:** AWS는 하이브리드 클라우드 솔루션을 적극적으로 지원합니다. 하이브리드 클라우드는 인프라 일부는 AWS 클라우드에 있고, 나머지는 온프레미스에 존재하는 환경을 의미합니다. 이유는 클라우드 마이그레이션 기간, 보안·규제 요건, 특정 워크로드만 클라우드의 탄력성을 활용하려는 전략 등 다양합니다.

AWS offers several storage services, including Amazon S3 and Amazon EFS. To expose Amazon S3 data on-premises, AWS provides the Storage Gateway service.  
**한국어 설명:** AWS는 Amazon S3(객체 스토리지)와 Amazon EFS(NFS 파일 시스템) 등 다양한 스토리지 서비스를 제공합니다. 온프레미스에서 S3 데이터를 사용하려면 Storage Gateway를 통해 AWS와 로컬 인프라를 연결할 수 있습니다.

---

## AWS Cloud Storage Options
- **Block Storage:** Amazon EBS, EC2 instance store  
- **File Systems:** Amazon EFS, Amazon FSx  
- **Object Storage:** Amazon S3, Amazon Glacier  

**한국어 설명:** AWS는 블록, 파일, 객체 스토리지 등 다양한 클라우드 네이티브 스토리지를 제공합니다. Storage Gateway는 온프레미스 데이터를 AWS 스토리지와 연결하여 통합 환경을 제공합니다.

---

## Overview of AWS Storage Gateway
AWS Storage Gateway serves as a bridge between your on-premises data and cloud data.  
**한국어 설명:** Storage Gateway는 온프레미스 데이터와 클라우드 데이터를 연결하는 다리 역할을 합니다. 주요 용도는 다음과 같습니다:

- 온프레미스 데이터를 클라우드로 백업하여 재해 복구
- 백업 및 복원
- 온프레미스에서 클라우드로 데이터 이전 또는 스토리지 확장
- 데이터 계층 관리: 최신 데이터는 온프레미스, 오래된 데이터는 클라우드
- 로컬 캐시를 활용한 저지연 파일 접근

Storage Gateway에는 **S3 File Gateway, Volume Gateway, Tape Gateway** 세 가지 유형이 있습니다.

---

## Amazon S3 File Gateway
The S3 File Gateway allows you to connect an Amazon S3 bucket to an on-premises application server using NFS or SMB.  
**한국어 설명:** S3 File Gateway는 온프레미스 서버에서 NFS 또는 SMB를 통해 S3 버킷에 접근할 수 있도록 해줍니다. 서버 입장에서는 일반 파일 공유처럼 보이지만, 실제 데이터는 S3에 저장됩니다.

- **Supported S3 storage classes:** Standard, Standard-IA, One Zone-IA, Intelligent-Tiering (Glacier 제외)  
- **Lifecycle policies:** S3 객체를 Glacier로 이동 가능  
- **Local caching:** 최근에 접근한 파일만 캐시  
- **SMB + Active Directory integration:** 사용자 인증 가능  

---

## Volume Gateway
Volume Gateway provides block storage using the iSCSI protocol backed by Amazon S3.  
**한국어 설명:** Volume Gateway는 iSCSI 프로토콜을 통해 블록 스토리지를 제공하며, Amazon S3와 EBS 스냅샷으로 백업됩니다.

### Modes
- **Cached Volumes:** 최근 데이터는 로컬에서 빠르게 접근, 전체 데이터는 S3 저장  
- **Stored Volumes:** 전체 데이터를 온프레미스에 저장, S3로 주기적 백업

---

## Tape Gateway
Tape Gateway supports tape backup virtualization and stores data in S3/Glacier.  
**한국어 설명:** Tape Gateway는 테이프 백업 환경을 가상화하여 클라우드로 백업합니다. S3에 저장 후 Glacier 또는 Glacier Deep Archive로 장기 보관이 가능합니다.

---

## Deployment and Summary
Storage Gateway runs as a virtual machine within your corporate data center, enabling low-latency access and seamless integration with on-premises systems.  
**한국어 설명:** Storage Gateway는 기업 데이터 센터 내 VM으로 배포되어 로컬 캐시와 저지연 접근을 제공합니다.

### Summary of Storage Gateway Types and Use Cases

| Gateway Type      | Protocols Supported | Storage Backend             | Use Case                                                   |
|------------------|------------------|----------------------------|-----------------------------------------------------------|
| S3 File Gateway  | NFS, SMB          | Amazon S3                  | File share access to S3 buckets with local caching       |
| Volume Gateway   | iSCSI             | Amazon S3 (EBS snapshots)  | Block storage volumes with backup and restore capabilities |
| Tape Gateway     | iSCSI (VTL)       | Amazon S3, Glacier         | Virtual tape library for tape backup systems             |

**한국어 설명:** 각 게이트웨이 유형은 특정 용도에 맞춰 설계되어 있으며, 온프레미스와 AWS 클라우드를 연결하는 하이브리드 스토리지 아키텍처를 구현합니다.

---

## Key Takeaways
- AWS Storage Gateway bridges on-premises infrastructure with AWS cloud storage.  
  **한국어:** Storage Gateway는 온프레미스 인프라와 AWS 클라우드를 연결합니다.
- Three types: S3 File Gateway, Volume Gateway, Tape Gateway  
  **한국어:** 세 가지 유형: S3 File Gateway, Volume Gateway, Tape Gateway
- S3 File Gateway exposes S3 buckets as NFS/SMB with local caching  
  **한국어:** S3 File Gateway는 NFS/SMB 파일 공유 형태로 S3 접근 제공, 자주 쓰는 데이터 캐싱
- Volume Gateway provides block storage via iSCSI with cached/stored volumes backed by S3/EBS snapshots  
  **한국어:** Volume Gateway는 iSCSI 블록 스토리지 제공, 캐시/스토어 모드 지원, S3/EBS 스냅샷으로 백업
- Tape Gateway virtualizes tape infrastructure, storing backups in S3/Glacier  
  **한국어:** Tape Gateway는 테이프 백업을 가상화하고 S3/Glacier에 장기 저장
- Storage Gateway runs as a VM in the data center for low-latency access  
  **한국어:** Storage Gateway는 데이터 센터 내 VM으로 운영되어 저지연 접근과 통합 지원
