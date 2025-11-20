이 내용은 AWS의 **Storage Gateway** 서비스에 대한 설명입니다. ☁️↔️🏢

핵심은 **Storage Gateway**가 여러분의 회사 내부에 있는 시스템(온프레미스)과 AWS 클라우드 저장소(S3, Glacier 등)를 연결해주는 **"다리(Bridge)"** 역할을 한다는 것입니다. 이를 통해 **하이브리드 클라우드** 환경을 구축할 수 있습니다.

---

## 1. 🌉 하이브리드 클라우드와 Storage Gateway의 역할

### 하이브리드 클라우드란?
회사의 인프라 일부는 **회사 내부(온프레미스)**에 두고, 나머지 일부는 **AWS 클라우드**에 두는 방식입니다. 보안, 규제, 또는 마이그레이션 시간 등의 이유로 데이터를 모두 클라우드로 옮기지 못할 때 사용됩니다.

### Storage Gateway의 역할
Storage Gateway는 회사 내부에 **가상 머신(VM)** 형태로 설치되어, 회사 시스템의 데이터를 AWS 클라우드 저장소로 전송하고 동기화하는 역할을 합니다.

* **주요 사용 목적:**
    * 회사 내 데이터의 **클라우드 백업 및 재해 복구**
    * 클라우드를 회사 내 시스템의 **저장 공간 확장** 용도로 사용
    * 자주 쓰는 데이터는 회사 내에 두고(빠른 접근), 오래된 데이터는 클라우드로 옮겨 **비용 절감**

---

## 2. 🗄️ Storage Gateway의 세 가지 유형

Storage Gateway는 데이터를 처리하는 방식(블록, 파일, 테이프)에 따라 세 가지 종류로 나뉩니다.

### A. 📁 Amazon S3 파일 게이트웨이 (S3 File Gateway)

회사 내부 서버에서 **S3 버킷**을 일반적인 **공유 폴더(파일 서버)**처럼 사용할 수 있게 해줍니다.

* **작동 방식:** 회사 서버는 일반적인 파일 공유 프로토콜인 **NFS**나 **SMB**로 요청을 보냅니다. 파일 게이트웨이는 이 요청을 받아서 S3 버킷으로 데이터를 저장/요청합니다. 
* **특징:**
    * 데이터는 최종적으로 S3에 저장되지만, **자주 접근하는 파일**은 게이트웨이의 로컬 캐시에 저장되어 **빠르게 접근**할 수 있습니다.
    * SMB 사용 시 **Active Directory**와 통합되어 사용자 인증을 할 수 있습니다.

---

### B. 💾 볼륨 게이트웨이 (Volume Gateway)

회사 내부 서버에 **블록 저장소(디스크)**를 제공하고, 그 데이터를 AWS에 백업할 때 사용됩니다. **iSCSI** 프로토콜을 사용합니다.

* **모드 1: 캐시 볼륨 (Cached Volumes)**
    * **전체 데이터는 S3에** 저장됩니다.
    * 가장 **최근에 접근한 데이터만** 회사 내 게이트웨이에 캐시되어 낮은 지연 시간으로 접근할 수 있습니다. (클라우드 확장 용도)
* **모드 2: 저장된 볼륨 (Stored Volumes)**
    * **전체 데이터는 회사 내부**에 저장됩니다.
    * 정기적으로 **S3에 백업**됩니다. (온프레미스 백업 용도)
* **백업:** 게이트웨이를 통해 만들어진 볼륨은 **Amazon EBS 스냅샷** 형태로 S3에 백업되며, 필요할 때 복원할 수 있습니다.

---

### C. 📼 테이프 게이트웨이 (Tape Gateway)

**기존의 물리적 테이프 백업 시스템**을 클라우드로 대체하고자 할 때 사용됩니다.

* **작동 방식:** 회사 시스템에는 **가상 테이프 라이브러리(VTL)**로 보입니다. 기존 백업 소프트웨어는 이 VTL에 데이터를 백업하면, 게이트웨이는 이를 물리적 테이프 대신 **Amazon S3**에 가상 테이프 형태로 저장합니다.
* **장기 보관:** S3에 저장된 가상 테이프는 이후 **Glacier**나 **Glacier Deep Archive**로 전환되어 장기간 저렴하게 보관됩니다. (물리적 테이프 관리 필요성 제거)

---

## 📌 요약 및 설치

| 게이트웨이 종류 | 용도 | AWS 저장소 | 로컬 접속 프로토콜 |
| :--- | :--- | :--- | :--- |
| **S3 파일 게이트웨이** | S3를 파일 공유 폴더처럼 사용 | Amazon S3 | NFS, SMB |
| **볼륨 게이트웨이** | 온프레미스 블록 저장소 백업/확장 | Amazon S3 (EBS 스냅샷) | iSCSI |
| **테이프 게이트웨이** | 물리적 테이프 백업 시스템 대체 | Amazon S3, Glacier | iSCSI (VTL) |

Storage Gateway는 반드시 회사 내부 데이터 센터에 **가상 머신(VM) 형태로 설치**되어야 합니다. 그래야만 회사 시스템이 낮은 지연 시간으로 클라우드 저장소에 접근할 수 있습니다.

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
