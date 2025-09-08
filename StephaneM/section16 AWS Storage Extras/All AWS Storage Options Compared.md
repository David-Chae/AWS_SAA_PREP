
# All AWS Storage Options Compared

## Overview of AWS Storage Options
AWS provides numerous storage options, each designed for different use cases.  
This lecture summarizes these options and highlights their differences.

---

## Amazon S3 and Glacier
- **Amazon S3**: Object storage with a specific API, integrates well with other AWS services.  
- **S3 Glacier**: For archiving objects at low cost.

---

## EBS Volumes
- Block storage attached to a **single EC2 instance** at a time.  
- Supports multitasking for IO1 and IO2.  
- Volume types: **GP3, IO2, etc.**, each designed for different performance needs.

---

## EC2 Instance Storage
- High-performance **physical storage directly attached** to EC2 instances.  
- Provides **very high IOPS**.  
- Not networked, storage is ephemeral and tied to the instance lifecycle.

---

## Amazon EFS
- Fully managed **NFS (Network File System)** for Linux instances.  
- **POSIX-compliant** filesystem.  
- Can be mounted across multiple availability zones.

---

## FSx File Systems
- **FSx for Windows File Server**: Managed Windows Server file system.  
- **FSx for Lustre**: High-performance computing file system for Linux.  
- **FSx for NetApp ONTAP**: Broad OS compatibility with enterprise NFS/CIFS.  
- **FSx for OpenZFS**: Managed ZFS file system.

---

## Storage Gateway
Bridge between **on-premises storage** and AWS.  
- **File Gateway**: Synchronize files between on-premises and Amazon S3 or FSx.  
- **Volume Gateway**: Block storage volumes on-premises backed up in the cloud.  
- **Tape Gateway**: Virtual tape backup solution.

---

## AWS Transfer Family
- Enables **FTP, FTPS, or SFTP** access to Amazon S3 or Amazon EFS.  
- Provides familiar transfer protocols on top of AWS storage.

---

## DataSync
- Automates **scheduled data synchronization**:  
  - On-premises ↔ AWS  
  - AWS ↔ AWS (between storage services)  
- Supports preserving metadata and permissions.

---

## Snow Family Devices
- For **large-scale data transfer when network bandwidth is insufficient**.  
- Options: **Snowcone, Snowball, Snowmobile**.  
- **Snowcone** includes a built-in DataSync agent.

---

## Databases
- While databases store data, they serve **specialized workloads** (indexing, querying).  
- A separate section is dedicated to database selection.

---

## Conclusion
Understanding the differences between AWS storage options is essential for selecting the right solution for your architecture and for AWS Solutions Architect exam preparation.

---

## Key Takeaways
- **Amazon S3** → Object storage, with Glacier for archiving.  
- **EBS Volumes** → Block storage, single EC2 instance, multiple performance classes.  
- **EC2 Instance Storage** → Local physical storage with very high IOPS.  
- **Amazon EFS** → POSIX-compliant NFS for Linux across AZs.  
- **FSx** → Specialized managed file systems (Windows, Lustre, NetApp ONTAP, OpenZFS).  
- **Storage Gateway** → Bridges on-premises storage with AWS (File, Volume, Tape).  
- **AWS Transfer Family** → FTP/FTPS/SFTP access to S3/EFS.  
- **DataSync** → Scheduled synchronization between on-premises and AWS or between AWS services.  
- **Snow Family** → Physical devices for massive data transfers to AWS.  



---

## 한국어 설명

이 문서는 AWS에서 제공하는 **모든 주요 스토리지 옵션을 비교**한 개요입니다.
각 서비스는 특정한 **사용 목적**에 맞게 설계되어 있으며, 시험 대비나 아키텍처 설계 시 올바른 선택을 하기 위해 차이점을 이해하는 것이 중요합니다.

* **Amazon S3 & Glacier** → 객체 스토리지, 장기 보관은 Glacier 사용
* **EBS** → EC2 전용 블록 스토리지, 성능별 볼륨 타입 제공
* **EC2 Instance Store** → 인스턴스에 물리적으로 연결된 초고속 스토리지, 일시적
* **EFS** → Linux 전용 네트워크 파일 시스템, 여러 AZ에서 공유 가능
* **FSx** → 특수 목적 파일 시스템 (Windows, HPC Lustre, NetApp, ZFS)
* **Storage Gateway** → 온프레미스 ↔ AWS 스토리지 연동 (파일, 볼륨, 테이프)
* **AWS Transfer Family** → FTP/FTPS/SFTP 기반 데이터 전송
* **DataSync** → 정기적/예약된 데이터 동기화 서비스
* **Snow Family** → 네트워크로 불가능한 대규모 데이터 물리적 이동 장치
