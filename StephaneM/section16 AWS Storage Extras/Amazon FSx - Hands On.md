# Amazon FSx - Hands On

## Introduction to Amazon FSx
Amazon FSx is the service to get managed file systems on AWS. You can create a file system by choosing between multiple options.  
**한국어 설명:** Amazon FSx는 AWS에서 관리형 파일 시스템을 생성할 수 있는 서비스입니다. 여러 옵션 중에서 파일 시스템을 선택하여 생성할 수 있습니다. 시험 목적상, 4가지 주요 FSx 파일 시스템 유형을 알아두어야 합니다. 추가 옵션이 생기더라도 시험에 나오지 않으면 여기서 다루지 않습니다.

---

## FSx for Lustre
FSx for Lustre provides a Lustre file system for your workload. You can enter the file system details such as deployment and storage type, which affects performance. You can also choose throughput and the placement within your VPC, along with any level of encryption. There are Persistent and Scratch file system options for Lustre.  
**한국어 설명:** FSx for Lustre는 HPC나 대규모 워크로드를 위한 Lustre 파일 시스템을 제공합니다. 배포 방식, 스토리지 타입, 처리량, VPC 내 위치, 암호화 옵션 등을 설정할 수 있습니다. Lustre에는 Persistent(지속형)와 Scratch(임시) 파일 시스템 옵션이 있습니다.

---

## FSx for Windows File Server
This option provides a Windows File Server on AWS, accessible using the Server Message Block (SMB) protocol.  
**한국어 설명:** FSx for Windows File Server는 AWS에서 Windows 파일 서버를 제공하며 SMB 프로토콜로 접근할 수 있습니다.

### Key Features
- Multi-AZ or Single-AZ deployment (Single-AZ suitable for dev environments)  
  **한국어:** Multi-AZ 또는 Single-AZ 배포 가능(개발 환경은 Single-AZ 적합)
- Storage types: SSD or HDD  
  **한국어:** SSD 또는 HDD 선택 가능
- Throughput depends on storage capacity (예: 10,000 GB 지정 시 처리량 옵션 달라짐)  
  **한국어:** 저장 용량에 따라 처리량 달라짐
- Can be deployed in a specific VPC  
  **한국어:** 특정 VPC 내 배포 가능
- Windows authentication with Active Directory integration (hosted AD on AWS or self-managed)  
  **한국어:** AD 통합 인증 가능(AWS 호스팅 AD 또는 자체 관리 AD)
- Encryption, auditing, access management, backup, maintenance options  
  **한국어:** 암호화, 감사, 접근 관리, 백업, 유지보수 옵션 지원

---

## FSx for NetApp ONTAP
This option allows you to get the popular NetApp ONTAP file system on AWS.  
**한국어 설명:** FSx for NetApp ONTAP은 AWS에서 인기 있는 NetApp ONTAP 파일 시스템을 제공합니다. Linux, Windows, macOS와 호환되며 성능이 우수합니다.

### Key Features
- Multi-AZ or Single-AZ deployment  
  **한국어:** Multi-AZ 또는 Single-AZ 배포 가능
- Storage type and capacity specification  
  **한국어:** 스토리지 타입과 용량 설정 가능
- Storage efficiency: deduplication, compression, compaction  
  **한국어:** 저장 효율화 기능: 중복 제거, 압축, 컴팩션
- Quick create or Standard create (Standard create provides more options)  
  **한국어:** Quick create 또는 Standard create 선택 가능(표준 생성 시 옵션 더 많음)

---

## FSx for OpenZFS
This option provides a ZFS file system on AWS, compatible with Linux, Windows, and macOS.  
**한국어 설명:** FSx for OpenZFS는 AWS에서 ZFS 파일 시스템을 제공하며 Linux, Windows, macOS와 호환됩니다. 시험에서는 4가지 FSx 옵션 간 차이를 이해하는 것이 중요합니다.

---

## Conclusion
Understanding the high-level differences between FSx for Lustre, Windows File Server, NetApp ONTAP, and OpenZFS is essential for exam preparation.  
**한국어 설명:** Lustre, Windows File Server, NetApp ONTAP, OpenZFS의 주요 차이를 이해하는 것이 시험 준비에 필수적입니다.

---

## Key Takeaways
- Amazon FSx provides managed file systems on AWS with multiple options.  
  **한국어:** FSx는 AWS에서 관리형 파일 시스템을 다양한 옵션으로 제공합니다.
- The four main FSx file systems to know are Lustre, Windows File Server, NetApp ONTAP, and OpenZFS.  
  **한국어:** 시험에서 알아야 할 주요 4가지 FSx 파일 시스템은 Lustre, Windows File Server, NetApp ONTAP, OpenZFS입니다.
- Each FSx option supports different protocols, storage types, and deployment configurations.  
  **한국어:** 각 FSx 옵션은 서로 다른 프로토콜, 스토리지 유형, 배포 구성을 지원합니다.
- Understanding the high-level differences between these file systems is essential for exam preparation.  
  **한국어:** 이들 파일 시스템 간 주요 차이를 이해하는 것이 시험 준비에 필수적입니다.

