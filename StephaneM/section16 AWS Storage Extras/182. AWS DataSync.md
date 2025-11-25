# AWS DataSync - Overview

## Introduction to AWS DataSync
AWS DataSync는 AWS 자격증 시험에서 점점 더 자주 등장하는 서비스입니다. 기능 자체는 단순하지만 핵심 개념을 이해하는 것이 중요합니다.  
DataSync의 기본 목적은 **데이터 동기화**이며, 다양한 위치 간에 대량의 데이터를 전송할 수 있습니다.  

지원되는 위치:
- 온프레미스 환경
- 다른 클라우드 환경
- AWS 내 서비스 간 이동

온프레미스나 다른 클라우드 환경과 연결할 때는 **DataSync 에이전트**를 설치해야 합니다.  
AWS 서비스 간 이동은 에이전트 없이도 가능합니다.

**한국어 설명:**  
DataSync는 데이터를 AWS와 온프레미스, 다른 클라우드 간에 쉽게 이동하고 동기화할 수 있는 서비스입니다. 에이전트가 필요한 경우와 불필요한 경우가 있으며, AWS 내 이동은 에이전트 없이도 가능합니다.

---

## Supported Storage Services
DataSync는 다양한 AWS 스토리지 서비스와 동기화 가능합니다:  
- **Amazon S3** (Glacier 포함 모든 스토리지 클래스 지원)  
- **Amazon Elastic File System (EFS)**  
- **Amazon FSx**  

**한국어 설명:**  
DataSync는 S3, EFS, FSx 등 주요 AWS 스토리지 서비스와 연동되어 데이터를 안전하게 동기화합니다.

---

## Scheduling and Metadata Preservation
- DataSync는 **연속 복제**가 아닌 **스케줄 기반 동기화** 수행  
  - 시간 단위, 일 단위, 주 단위로 설정 가능  
- 파일 권한 및 메타데이터 보존  
  - NFS POSIX 권한, SMB 권한 지원  
  - 데이터 보안 및 컴플라이언스 유지

**한국어 설명:**  
DataSync는 예약된 시간에 따라 데이터를 동기화하며, 파일 권한과 메타데이터를 유지하여 보안과 규정을 준수합니다.

---

## Performance and Bandwidth Control
- 단일 DataSync 에이전트: 최대 10Gbps 처리 가능  
- 네트워크 포화 방지 위해 **대역폭 제한 설정 가능**

**한국어 설명:**  
에이전트 하나로 빠른 데이터 전송이 가능하며, 필요에 따라 대역폭을 제한해 네트워크 혼잡을 방지할 수 있습니다.

---

## Architecture Overview
온프레미스 파일을 SMB/NFS 프로토콜을 통해 AWS로 동기화하는 경우:  
1. 온프레미스 NFS/SMB 서버 준비  
2. **DataSync 에이전트 설치**  
3. DataSync 서비스와 암호화된 연결 설정  
4. 목적지 지정: Amazon S3, EFS, FSx  
5. 동기화 방식:  
   - 단방향 (온프레미스 → AWS)  
   - 양방향 (AWS ↔ 온프레미스)

**한국어 설명:**  
DataSync 에이전트가 온프레미스 서버와 AWS 사이의 안전한 데이터 전송을 관리하며, 단방향 또는 양방향 동기화가 가능합니다.

---

## Handling Limited Network Capacity
- 네트워크 용량 부족 시 **AWS Snowcone** 사용 가능  
- Snowcone에 DataSync 에이전트 사전 설치  
- 온프레미스에서 데이터 수집 후 물리적으로 AWS 지역으로 배송  
- AWS에서 스토리지에 동기화

**한국어 설명:**  
네트워크 대역폭이 제한된 경우 Snowcone 디바이스를 사용하면 오프라인으로 데이터를 안전하게 AWS로 전송할 수 있습니다.

---

## Synchronization Between AWS Storage Services
- AWS 내 스토리지 서비스 간 동기화 가능: S3, EFS, FSx  
- 데이터와 메타데이터, 파일 권한 모두 보존  
- 데이터 무결성과 보안 유지

**한국어 설명:**  
AWS 내 서비스 간에도 DataSync를 통해 안전하게 데이터를 이동하고, 파일 권한과 메타데이터를 유지할 수 있습니다.

---

## Summary
AWS DataSync는 다양한 위치와 스토리지 서비스 간 데이터를 동기화할 수 있는 **다목적 서비스**입니다.  
- 스케줄 기반 동기화  
- 메타데이터 및 권한 보존  
- NFS/SMB 연결 시 에이전트 필요  
- 강력한 데이터 마이그레이션 및 동기화 도구

**한국어 설명:**  
DataSync는 온프레미스, 다른 클라우드, AWS 간 데이터 동기화를 쉽게 수행할 수 있는 서비스로, 메타데이터와 권한도 유지하며 안전한 전송이 가능합니다.

---

## Key Takeaways
- DataSync는 온프레미스, 다른 클라우드, AWS 간 대용량 데이터 전송 및 동기화 서비스  
- NFS, SMB, HDFS 등 프로토콜 지원, 연결 시 에이전트 필요  
- Amazon S3(Glacier 포함), EFS, FSx로 동기화 가능, 파일 권한과 메타데이터 보존  
- 동기화 작업은 예약 기반(시간/일/주 단위), 대역폭 제한 설정 가능

**한국어 요약:**  
DataSync는 다양한 위치와 AWS 스토리지 간 안전하게 데이터를 이동하고 동기화하는 완전 관리형 서비스이며, 예약 동기화와 대역폭 제어 기능을 제공합니다.

AWS DataSync - Overview
Introduction to AWS DataSync
AWS DataSync is a service that is increasingly appearing in AWS certification exams. It is a straightforward service, but it is essential to understand its core functionality. Essentially, DataSync is designed to synchronize data, enabling the transfer of large amounts of data to and from various locations.

These locations can include on-premises environments or other cloud locations into AWS. To connect to your server, DataSync supports protocols such as NFS, SMB, HDFS, and others. When connecting to on-premises or other cloud environments, an agent must be installed to facilitate this connection.

DataSync also supports migrations between AWS services themselves, which does not require an agent. This means you can move data from one AWS storage service to another seamlessly.

Supported Storage Services
DataSync can synchronize data to various AWS storage services, including:

Amazon S3, supporting all storage classes including Glacier.
Amazon Elastic File System (EFS).
Amazon FSx.
It fully supports all these services for data synchronization.

Scheduling and Metadata Preservation
Replication tasks in DataSync are not continuous; instead, they are scheduled. You can configure DataSync to run hourly, daily, or weekly, which means there is a lag between synchronizations. However, the service ensures that data is synchronized according to the schedule.

Additionally, DataSync preserves file permissions and metadata, maintaining security and compliance. It supports NFS POSIX file system permissions and SMB permissions, which is crucial for preserving metadata when moving files between locations.

Performance and Bandwidth Control
A single DataSync agent is quite powerful and can handle up to 10 gigabits of data per second. If you want to avoid saturating your network, you can configure bandwidth limits to control the data transfer rate.

Architecture Overview
Consider the use case of synchronizing your on-premises files using SMB or NFS protocols into AWS. Your on-premises environment contains an NFS or SMB server. To enable synchronization, you install the AWS DataSync agent on-premises and configure it to connect to your NFS or SMB server.

The DataSync agent establishes an encrypted connection to the DataSync service in AWS. From there, you can specify the destination, which could be any storage class in Amazon S3, Amazon EFS, or Amazon FSx.

Synchronization can be one-way, from on-premises to AWS, or it can be bi-directional, synchronizing data from AWS back to on-premises. This flexibility is why the service is named DataSync.

Handling Limited Network Capacity
In scenarios where network capacity is insufficient to use DataSync directly, AWS Snowcone devices can be utilized. The Snowcone device comes with the DataSync agent pre-installed. You can run Snowcone on-premises to pull your data using the DataSync agent. Then, the device is physically shipped back to your AWS region, where the data is synchronized to AWS storage resources.

Synchronization Between AWS Storage Services
DataSync can also synchronize data between different AWS storage services, such as between Amazon S3, Amazon EFS, and Amazon FSx. This process preserves both the data and the metadata, including file permissions, which is important for maintaining data integrity and security.

Summary
To summarize, AWS DataSync is a versatile service that can synchronize data between various locations and storage services. It operates on scheduled tasks rather than continuous replication, preserves metadata and file permissions, and requires agents when connecting to NFS or SMB servers. It is a powerful tool for data migration and synchronization in AWS environments.

Key Takeaways
AWS DataSync is a service designed to synchronize and move large amounts of data between on-premises, other cloud locations, and AWS.
DataSync supports protocols like NFS, SMB, and HDFS, requiring an on-premises or cloud agent for these connections.
It can synchronize data to Amazon S3 (including Glacier), Amazon EFS, and Amazon FSx, preserving file permissions and metadata.
DataSync tasks are scheduled (hourly, daily, weekly), not continuous, and bandwidth limits can be configured to manage network usage.
