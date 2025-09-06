# AWS Transfer Family

## Introduction to AWS Transfer Family
AWS Transfer Family를 살펴보겠습니다. 주요 목적은 Amazon S3나 EFS에 데이터를 넣거나 가져올 때 직접 S3 API나 EFS 네트워크 파일 시스템을 사용하지 않고, **FTP 프로토콜**을 통해 데이터를 전송하는 것입니다.  

이럴 경우 AWS Transfer Family 서비스를 사용합니다. 지원되는 프로토콜은 다음과 같습니다:  
- **FTP (File Transfer Protocol)**  
- **FTPS (File Transfer Protocol over SSL, 암호화 지원)**  
- **SFTP (Secure File Transfer Protocol, 암호화 지원)**  

**한국어 설명:**  
Transfer Family는 S3나 EFS와 직접 통신하지 않고도 FTP 계열 프로토콜로 파일 전송을 가능하게 합니다. FTP는 암호화되지 않으며, FTPS와 SFTP는 전송 중 암호화를 제공합니다.

---

## Features of AWS Transfer Family
- FTP 프로토콜을 통해 Amazon S3나 EFS에 데이터 업로드 가능  
- 완전 관리형 인프라로 확장성, 신뢰성, 고가용성을 제공  
- AWS가 모든 관리 작업 수행  
- 요금: 프로비저닝된 엔드포인트 시간 단위 + 전송한 데이터 기가바이트 단위 요금

**한국어 설명:**  
Transfer Family는 완전 관리형 서비스로 사용자는 확장성이나 가용성을 걱정하지 않고 데이터 전송만 집중하면 됩니다. 요금은 엔드포인트 사용 시간과 전송 데이터량 기준으로 부과됩니다.

---

## User Authentication and Integration
- AWS Transfer Family 내에서 사용자 인증 정보 관리 가능  
- 기존 인증 시스템과 통합 가능: Microsoft Active Directory, LDAP, Okta, Amazon Cognito, 또는 커스텀 소스  

**한국어 설명:**  
사용자 인증을 서비스 내부에서 처리하거나 기존 온프레미스/클라우드 인증 시스템과 연결할 수 있어 기업 환경에 유연하게 적용 가능합니다.

---

## Use Cases
- S3 또는 EFS에 FTP 인터페이스 제공  
- 파일 공유, 공공 데이터셋 배포  
- CRM, ERP 등 애플리케이션 지원

**한국어 설명:**  
Transfer Family는 FTP 기반 파일 업로드/다운로드가 필요한 시스템과 애플리케이션에서 유용합니다.

---

## Architecture Overview
- 사용자 접근: FTP, FTPS, SFTP 엔드포인트  
- 선택 사항: Amazon Route 53을 사용하여 맞춤 호스트네임 제공  
- 서비스는 IAM 역할을 사용해 S3 또는 EFS에서 파일 읽기/쓰기 수행  
- 최소 설정으로 바로 사용 가능

**한국어 설명:**  
사용자는 FTP 계열 엔드포인트를 통해 S3/EFS에 접근하고, 서비스는 백그라운드에서 IAM 역할을 이용해 파일 권한을 처리합니다.

---

## Security and Authentication
- Active Directory, LDAP 등 외부 인증 시스템과 연동하여 사용자 인증 가능  

**한국어 설명:**  
외부 인증 시스템을 통해 사용자 접근을 안전하게 관리할 수 있습니다.

---

## Conclusion
AWS Transfer Family의 주요 개념과 사용 사례를 살펴보았습니다. 다음 강의에서는 더 심화된 예제를 다룰 예정입니다.

**한국어 설명:**  
Transfer Family를 통해 FTP 계열 프로토콜로 안전하고 관리되는 데이터 전송을 수행할 수 있습니다.

---

## Key Takeaways
- S3나 EFS와 직접 통신하지 않고 FTP 프로토콜을 사용해 데이터 전송 가능  
- 지원 프로토콜: FTP, FTPS, SFTP (FTPS, SFTP는 암호화 제공)  
- 완전 관리형 서비스, 확장성, 고가용성 제공  
- 요금: 엔드포인트 시간 단위 + 데이터 전송량  
- 사용자 인증: 서비스 내 관리 또는 외부 시스템 통합 가능 (AD, LDAP, Okta, Cognito 등)

**한국어 요약:**  
AWS Transfer Family는 FTP/FTPS/SFTP를 통해 S3와 EFS에 안전하게 데이터를 전송할 수 있는 완전 관리형 서비스이며, 사용자 인증과 통합도 유연하게 지원합니다.
