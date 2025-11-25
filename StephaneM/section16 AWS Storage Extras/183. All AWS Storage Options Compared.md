AWS의 스토리지 종류를 **“어떤 상황에서 무엇을 쓰면 되는지” 기준으로 아주 쉽게** 설명해줄게.
AWS 스토리지는 많아 보이지만, 사실 **역할별로 정리하면 금방 이해된다.**

---

# 🚀 AWS 스토리지 한눈에 보기 (초간단 요약)

AWS 저장소는 크게 4종류로 나뉜다:

1. **파일 저장(File)**
2. **블록 저장(Block)**
3. **오브젝트 저장(Object)**
4. **물리 장비/연결 서비스**

이제 각각을 쉽게 설명해볼게.

---

# 🟦 1. Amazon S3 & Glacier (오브젝트 스토리지)

### ✔ S3 = “이메일 첨부파일 박스”

파일을 넣어두면 이름/경로 없이 **객체(Object)** 형태로 저장됨.

* 이미지, 로그, 백업 등 대부분의 정적 파일 저장
* 거의 모든 AWS 서비스와 잘 연동됨
* 무한대 확장 가능

### ✔ Glacier = “아카이브 금고”

S3보다 훨씬 싸지만 바로 꺼내 쓸 수 없음

* 자주 안 쓰는 데이터 보관용 (백업, 기록 보관)

---

# 🟥 2. EBS (EC2 전용 블록 스토리지)

### ✔ EBS = “노트북 SSD 같은 저장장치”

* EC2 인스턴스에 **딱 한 대** 연결
* 운영체제, DB, 애플리케이션 저장
* 종류:

  * **gp3**: 일반 SSD
  * **io1/io2**: 고성능 IOPS SSD

**특징**:

* EC2 중지해도 데이터 유지
* 네트워크를 통해 EC2에 연결되는 형태

---

# 🟨 3. EC2 Instance Store (물리적으로 달린 NVMe)

### ✔ Instance Store = “EC2 본체 안에 들어있는 로컬 SSD”

* 엄청 빠르지만, **EC2 종료하면 데이터 날아감**
* DB 캐시, 임시 파일, 빅데이터 임시 처리 용도

**장점**: 최고의 속도
**단점**: 휘발성

---

# 🟩 4. Amazon EFS (Linux용 네트워크 파일 공유)

### ✔ EFS = “여러 서버가 같이 쓰는 네트워크 드라이브”

* NFS 기반 (Linux 전용)
* 여러 EC2가 동시에 마운트 가능
* 멀티 AZ 가능
* POSIX 권한 지원

용도:

* 웹 서버 공유 폴더
* 애플리케이션 간 공유 파일 시스템

---

# 🟪 5. FSx 제품군 (특수 목적 파일 시스템)

FSx는 **특정 OS나 특수 워크로드에 맞춘 고급 파일시스템**이다.

### ✔ FSx for Windows

* Windows Server SMB 파일 공유
* AD(Active Directory) 연동 필요
* 사내 Windows 파일 서버 대체

### ✔ FSx for Lustre

* 슈퍼컴퓨터·HPC·AI·ML용 고성능 Linux 파일시스템
* S3와 연동 가능

### ✔ FSx for NetApp ONTAP

* NetApp 저장장치 기능을 그대로 AWS에서 사용
* 스냅샷, 복제 등 엔터프라이즈 기능 지원

### ✔ FSx for OpenZFS

* ZFS를 관리형으로 제공
* 스냅샷, 압축 등 고급 기능 제공

---

# 🧩 6. Storage Gateway (온프레미스 ↔ AWS 연결)

온프레미스와 AWS 저장소를 **자연스럽게 연결**하는 서비스.

### 종류 3가지:

#### ✔ File Gateway

* 사내에서 저장하면 자동으로 S3와 동기화

#### ✔ Volume Gateway

* 사내 서버가 사용하던 디스크(LUN)를 AWS 백업으로 제공

#### ✔ Tape Gateway

* 테이프 백업 시스템을 S3/Glacier로 대체

---

# 🔁 7. AWS Transfer Family (FTP/SFTP 서버 대체)

### ✔ Transfer Family = “SFTP/FTP 서버를 AWS로 옮기는 서비스”

* SFTP/FTP/FTPS 서버를 AWS에서 제공
* 데이터를 S3 또는 EFS에 저장
* 기존 FTP 기반 시스템과 연결할 때 유용

---

# 🔄 8. DataSync (자동화된 데이터 이동 서비스)

### ✔ DataSync = “대량 파일을 정해진 시간마다 자동 복사하는 로봇”

* 온프레미스 ↔ AWS
* AWS ↔ AWS
* 스케줄 기반 동기화
* 권한/메타데이터 유지
* 매우 빠르고 개입 필요 없음

---

# 📦 9. Snow Family (물리 장비로 데이터 이송)

인터넷이 느려서 데이터 전송이 어려운 경우 사용.

### ✔ Snowcone

* 가장 작은 장비, DataSync 에이전트 내장

### ✔ Snowball

* Petabyte 단위 전송 가능

### ✔ Snowmobile

* 데이터센터 전체 옮길 때 쓰는 트레일러(트럭)

물리 장비에 데이터를 담아 AWS로 “배송”하는 방식.

---

# 🗄 10. 데이터베이스(별도 범주)

DB도 저장공간이지만,
**검색/쿼리/트랜잭션** 등을 위해 설계된 다른 영역이므로
스토리지와 분리해서 따로 다룬다.

---

# 🌟 전체 그림 한 줄 요약

| 서비스                 | 쉽게 말하면             | 용도                  |
| ------------------- | ------------------ | ------------------- |
| **S3**              | 만능 파일 보관함          | 정적파일, 백업            |
| **Glacier**         | 초저렴 장기 보관 금고       | 기록 보관               |
| **EBS**             | EC2 전용 SSD         | OS/DB용 디스크          |
| **Instance Store**  | EC2 안에 달린 초고속 디스크  | 캐시/임시 데이터           |
| **EFS**             | Linux 공용 네트워크 드라이브 | 여러 서버에서 공유          |
| **FSx(W/L/O/Z)**    | 특수 목적 고급 파일시스템     | Windows, HPC, ZFS 등 |
| **Storage Gateway** | 사내 ↔ AWS 연결 다리     | 파일/볼륨/테이프 연동        |
| **Transfer Family** | AWS 기반 FTP/SFTP 서버 | 기존 FTP 시스템 연동       |
| **DataSync**        | 대량 파일 자동 복사 로봇     | 온프레 ↔ AWS 동기화       |
| **Snow Family**     | 물리 장비로 AWS에 보내기    | 대규모 오프라인 이송         |

---

원하면 **각 서비스 비교 그림**, **시험 대비 암기 팁**, **“어떤 상황에서 무엇을 써야 하나” 흐름도**, **10문제 시험 스타일 문제**도 만들어줄게!



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
