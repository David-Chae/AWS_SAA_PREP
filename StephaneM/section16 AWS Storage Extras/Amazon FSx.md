이 내용은 AWS에서 제공하는 완전 관리형 파일 시스템 서비스인 **Amazon FSx**에 대한 설명입니다. 📂

핵심은 AWS가 **Windows, 고성능 컴퓨팅(HPC), 기존 온프레미스 시스템** 등 다양한 환경에서 요구하는 전문적인 파일 시스템을 설치와 관리 걱정 없이 제공한다는 것입니다.

---

## 💡 Amazon FSx란 무엇인가요?

**Amazon FSx**는 AWS에서 **외부의 고성능 파일 시스템**을 **완전 관리형 서비스**로 사용할 수 있게 해주는 서비스입니다.

* **비유:** 데이터베이스를 AWS에서 RDS(MySQL, PostgreSQL 등)로 쓰듯이, 파일 시스템을 FSx를 통해 전문적인 시스템으로 쓰는 것입니다.
* **지원 파일 시스템:** 현재 주로 **Lustre, Windows File Server, NetApp ONTAP, OpenZFS** 네 가지를 지원합니다.

---

## 1. 🖥️ Amazon FSx for Windows File Server

**Windows 환경에 익숙한 공유 드라이브**를 AWS에서 그대로 사용하는 서비스입니다.

* **프로토콜:** **SMB** 프로토콜을 사용하며, Windows의 표준 파일 시스템인 **NTFS**를 지원합니다.
* **보안 및 관리:**
    * **Microsoft Active Directory**와 통합되어 사용자 보안을 관리합니다.
    * **ACL(접근 제어 목록)** 및 **사용자 할당량**을 지원합니다.
    * Windows용으로 만들어졌지만, **Linux EC2 인스턴스**에서도 연결하여 사용할 수 있습니다.
* **고가용성 및 백업:** **Multi-AZ(다중 가용 영역)** 배포를 지원하여 높은 가용성을 제공하며, 매일 자동으로 **Amazon S3**에 백업됩니다.
* **저장 옵션:**
    * **SSD:** 데이터베이스나 미디어 처리 등 **매우 낮은 지연 시간**이 필요한 작업에 적합합니다.
    * **HDD:** 홈 디렉터리나 콘텐츠 관리 시스템(CMS) 등 **일반적인 용도**에 적합합니다.

---

## 2. 🔬 Amazon FSx for Lustre

**대규모 컴퓨팅**을 위해 설계된 **초고성능 분산 파일 시스템**입니다. 이름은 Linux와 Cluster에서 유래했습니다.

* **주요 용도:** **머신러닝(ML)**, **고성능 컴퓨팅(HPC)**, 비디오 처리, 금융 모델링 등 **엄청난 처리량과 속도**가 필요한 작업의 핵심 지표입니다.
* **성능:** 초당 수백 기가바이트의 처리량, 수백만 IOPS, 1밀리초 미만의 지연 시간 등 **극강의 성능**을 제공합니다.
* **S3 연동:** Amazon S3와 연동되어 S3를 파일 시스템처럼 읽거나, 계산 결과를 S3로 다시 쓰는 것이 매우 쉽습니다.

### 2-1. 배포 옵션 (저장 방식)

| 옵션 | 특징 | 적합한 용도 |
| :--- | :--- | :--- |
| **Scratch File System (스크래치)** | **임시 저장소** (데이터 복제 없음). 서버가 고장나면 **데이터가 사라집니다.** | 단기 데이터 처리, 비용 절감, 임시 분석용. (고성능 버스트 제공) |
| **Persistent File System (영구)** | **장기 저장소** (동일 AZ 내 데이터 복제). 서버가 고장나도 파일이 **투명하게 대체**됩니다. | 장기적인 처리, 민감한 데이터 보존용. |

---

## 3. 🌐 Amazon FSx for NetApp ONTAP

온프레미스에서 **NetApp ONTAP** 또는 **NAS(Network Attached Storage)** 시스템을 사용하던 고객이 AWS로 쉽게 마이그레이션할 수 있도록 만든 서비스입니다.

* **프로토콜 호환성:** **NFS, SMB, iSCSI** 등 다양한 프로토콜을 모두 지원하여 Linux, Windows, macOS 등 광범위한 운영체제와 호환됩니다.
* **주요 기능:**
    * **자동 스케일링:** 필요에 따라 저장 공간이 자동으로 늘거나 줄어듭니다.
    * **데이터 중복 제거(De-duplication):** 중복된 파일을 제거하여 저장 공간을 절약합니다.
    * **스냅샷/복제:** 데이터 복제와 백업 기능이 내장되어 있습니다.
    * **순간 복제(Instantaneous Cloning):** 파일 시스템을 **순식간에 복제**하여 테스트 환경 등을 빠르게 만들 수 있습니다.

---

## 4. 🗃️ Amazon FSx for OpenZFS

기존에 **OpenZFS** 파일 시스템을 사용하던 고객을 위해 제공되는 완전 관리형 서비스입니다.

* **프로토콜:** **NFS** 프로토콜만 지원합니다.
* **성능:** 0.5밀리초 미만의 지연 시간으로 최대 100만 IOPS까지 확장되는 **고성능**을 제공합니다.
* **주요 기능:**
    * **스냅샷 및 압축:** 지원됩니다.
    * **순간 복제(Instantaneous Cloning):** 새로운 워크로드를 테스트하기 위한 빠른 복제가 가능합니다.
    * **참고:** NetApp ONTAP과 달리 **데이터 중복 제거는 지원하지 않습니다.**

---

## 📌 요약: 언제 어떤 FSx를 사용해야 할까요?

| 파일 시스템 | 핵심 프로토콜 | 주요 용도 및 특징 |
| :--- | :--- | :--- |
| **Windows File Server** | **SMB** | Windows 공유 폴더, Active Directory 통합, Multi-AZ 지원. |
| **Lustre** | 분산 파일 시스템 | **머신러닝/HPC** 등 초고성능 컴퓨팅 및 대규모 데이터 처리. |
| **NetApp ONTAP** | NFS, **SMB, iSCSI** | 기존 **NetApp/NAS** 워크로드 마이그레이션, **데이터 중복 제거** 지원. |
| **OpenZFS** | **NFS** | 기존 **OpenZFS** 마이그레이션, 고성능, 순간 복제 지원. |

# Amazon FSx

## Introduction to Amazon FSx
Amazon FSx allows you to launch third-party high-performance file systems on AWS as a fully managed service.  
**한국어 설명:** Amazon FSx는 AWS에서 제3자 고성능 파일 시스템을 완전 관리형 서비스로 실행할 수 있도록 해줍니다. RDS가 데이터베이스를 제공하는 것과 유사하게, FSx는 파일 시스템을 제공하며, 예시로는 Lustre, Windows File Server, NetApp ONTAP, OpenZFS가 있습니다.

---

## Amazon FSx for Windows File Server
Amazon FSx for Windows File Server is a fully managed Windows File Server share drive.  
**한국어 설명:** FSx for Windows File Server는 완전 관리형 Windows 파일 서버 공유 드라이브로, SMB 프로토콜과 NTFS를 지원합니다. Active Directory와 통합되어 사용자 보안을 제공하며, ACL과 사용자 쿼터도 지원합니다. Linux EC2 인스턴스에서도 마운트 가능합니다.

### Key Features
- Integration with on-premises Windows File Server using DFS.  
  **한국어:** 기존 온프레미스 Windows File Server와 DFS를 통해 통합 가능.
- Performance: Tens of GB/s, millions of IOPS, hundreds of PB storage.  
  **한국어:** 성능: 수십 GB/s, 수백만 IOPS, 수백 PB 데이터 저장 가능.
- Storage options: SSD (low-latency workloads), HDD (general workloads).  
  **한국어:** SSD(저지연 워크로드), HDD(일반 워크로드) 선택 가능.
- Multi-AZ deployment and daily backups to S3.  
  **한국어:** 고가용성을 위한 Multi-AZ 배포, S3로 일일 백업 지원.

---

## Amazon FSx for Lustre
Amazon FSx for Lustre provides a distributed file system designed for large-scale computing.  
**한국어 설명:** FSx for Lustre는 대규모 컴퓨팅을 위해 설계된 분산 파일 시스템으로, ML, HPC, 비디오 처리, 금융 모델링 등에 사용됩니다.

### Storage and Integration
- SSDs for low-latency, IOPS-intensive workloads; HDDs for throughput-intensive workloads.  
  **한국어:** SSD: 저지연, IOPS 중심; HDD: 대용량 순차 처리 중심.
- Integrates with S3 for reading/writing data.  
  **한국어:** S3와 통합되어 FSx를 파일 시스템처럼 사용 가능.
- Accessible via VPN or Direct Connect from on-premises.  
  **한국어:** 온프레미스에서 VPN 또는 Direct Connect를 통해 접근 가능.

### Deployment Options
- **Scratch File System:** Temporary storage, high burst performance, data lost if server fails.  
  **한국어:** 임시 저장소, 높은 일시 성능, 서버 실패 시 데이터 손실.
- **Persistent File System:** Long-term storage, data replicated within AZ, transparent recovery.  
  **한국어:** 장기 저장용, 데이터 AZ 내 복제, 서버 실패 시 자동 복구.

---

## Amazon FSx for NetApp ONTAP
Amazon FSx for NetApp ONTAP is a managed NetApp ONTAP file system on AWS.  
**한국어 설명:** FSx for NetApp ONTAP는 AWS에서 관리되는 NetApp ONTAP 파일 시스템으로, NFS, SMB, iSCSI 프로토콜을 지원하며 온프레미스 NAS/ONTAP 마이그레이션에 적합합니다.

### Features
- Broad OS compatibility: Linux, Windows, macOS; integrates with VMware Cloud, WorkSpaces, AppStream, EC2, ECS, EKS.  
  **한국어:** 다양한 OS 호환, AWS 서비스 및 VMware Cloud와 통합 가능.
- Auto-scaling, replication, snapshots, compression, data deduplication.  
  **한국어:** 자동 확장, 복제, 스냅샷, 압축, 데이터 중복 제거 지원.
- Point-in-time instantaneous cloning for testing or staging.  
  **한국어:** 시점 복제(Instant Cloning)로 테스트 환경 생성 가능.

---

## Amazon FSx for OpenZFS
Amazon FSx for OpenZFS is a managed OpenZFS file system on AWS, NFS protocol only.  
**한국어 설명:** FSx for OpenZFS는 AWS에서 관리되는 OpenZFS 파일 시스템으로, NFS 프로토콜 전용이며 ZFS 워크로드 마이그레이션에 적합합니다.

### Features
- High performance: up to 1M IOPS, <0.5 ms latency.  
  **한국어:** 높은 성능: 최대 100만 IOPS, 0.5ms 미만 지연.
- Supports snapshots, compression; no deduplication.  
  **한국어:** 스냅샷 및 압축 지원, 중복 제거는 미지원.
- Point-in-time instantaneous cloning for testing new workloads.  
  **한국어:** 새로운 워크로드 테스트용 시점 복제 지원.

---

## Conclusion
This overview of Amazon FSx and its supported file systems equips you to choose the right file system for your workload requirements.  
**한국어 설명:** Amazon FSx와 지원 파일 시스템의 특징을 이해하면 워크로드 요구사항에 맞는 적합한 파일 시스템을 선택할 수 있습니다. 각 파일 시스템의 프로토콜, 성능, 기능, 사용 사례를 이해하는 것이 중요합니다.

---

## Key Takeaways
- Amazon FSx provides fully managed third-party high-performance file systems on AWS.  
  **한국어:** FSx는 AWS에서 완전 관리형 고성능 제3자 파일 시스템을 제공합니다.
- FSx supports multiple file systems: Windows File Server, Lustre, NetApp ONTAP, OpenZFS.  
  **한국어:** FSx는 Windows File Server, Lustre, NetApp ONTAP, OpenZFS를 지원합니다.
- FSx for Windows File Server supports SMB, Active Directory, and Linux mounting.  
  **한국어:** Windows File Server는 SMB, AD 통합, Linux 마운트 지원.
- FSx for Lustre is HPC-focused with scratch and persistent file system options.  
  **한국어:** Lustre는 HPC 중심, 임시 및 지속형 파일 시스템 선택 가능.
- FSx for NetApp ONTAP offers broad protocol support, auto-scaling, replication, deduplication.  
  **한국어:** ONTAP는 광범위한 프로토콜 지원, 자동 확장, 복제, 중복 제거 지원.
- FSx for OpenZFS supports NFS, high IOPS with low latency, snapshots, compression, cloning.  
  **한국어:** OpenZFS는 NFS, 고IOPS 저지연, 스냅샷, 압축, 시점 복제 지원.

> AI may make mistakes. Verify for accuracy.  
> **한국어:** AI가 오류를 만들 수 있으므로, 시험 준비 시 반드시 정확성을 확인하세요.
