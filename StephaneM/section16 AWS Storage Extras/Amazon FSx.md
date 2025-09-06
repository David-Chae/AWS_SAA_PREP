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
