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
