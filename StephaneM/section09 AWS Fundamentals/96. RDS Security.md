# RDS Security  
# RDS 보안  

---

## Introduction to RDS and Aurora Security  
## RDS 및 Aurora 보안 개요  

This lecture provides a quick overview of security features available for RDS and Aurora databases.  
이번 강의에서는 RDS와 Aurora 데이터베이스에서 사용할 수 있는 보안 기능을 간단히 소개합니다.  
(보안 개요 안내)  

---

## Data Encryption at Rest  
## 저장 시 데이터 암호화  

You can encrypt data at rest on your RDS and Aurora databases.  
RDS와 Aurora 데이터베이스에서 저장된 데이터를 암호화할 수 있습니다.  
(데이터 보안 기본)  

This means that the data stored on the volumes is encrypted.  
즉, 볼륨에 저장된 데이터가 암호화된다는 뜻입니다.  
(암호화 범위 설명)  

Both the master database and any replicas are encrypted using AWS Key Management Service (KMS).  
마스터 DB와 모든 복제본은 AWS KMS를 사용하여 암호화됩니다.  
(KMS 활용)  

This encryption setting is defined at the time of the database's initial launch.  
이 암호화 설정은 데이터베이스 초기 생성 시 정의됩니다.  
(설정 시점 안내)  

If the master database is not encrypted at launch, then any read replicas cannot be encrypted either.  
마스터 DB가 생성 시 암호화되지 않으면, 읽기 전용 복제본도 암호화할 수 없습니다.  
(제약 조건 안내)  

To encrypt an existing unencrypted database, you must take a snapshot of that unencrypted database and then restore the snapshot as an encrypted database.  
기존 암호화되지 않은 DB를 암호화하려면, 먼저 스냅샷을 만든 후 해당 스냅샷을 암호화된 DB로 복원해야 합니다.  
(암호화 후 처리 방법)  

This process involves a snapshot and restore operation.  
이 과정은 스냅샷 생성과 복원 작업을 포함합니다.  
(작업 설명)  

---

## In-Flight Encryption  
## 전송 중 데이터 암호화  

In-flight encryption protects data transmitted between your clients and the database.  
전송 중 데이터 암호화는 클라이언트와 데이터베이스 간 전송되는 데이터를 보호합니다.  
(데이터 전송 보안)  

Each RDS and Aurora database supports in-flight encryption by default.  
모든 RDS 및 Aurora DB는 기본적으로 전송 중 데이터 암호화를 지원합니다.  
(기본 설정 안내)  

Clients must use the TLS root certificates provided by AWS, which are available on the AWS website, to establish secure connections.  
클라이언트는 AWS 웹사이트에서 제공하는 TLS 루트 인증서를 사용하여 안전한 연결을 설정해야 합니다.  
(TLS 인증서 사용)  

---

## Database Authentication  
## 데이터베이스 인증  

For authentication, RDS and Aurora support the traditional username and password method.  
인증 방법으로 RDS와 Aurora는 전통적인 사용자 이름/비밀번호 방식을 지원합니다.  
(기본 인증 방식)  

Additionally, because these services are part of AWS, you can use IAM roles to connect to your database.  
또한, AWS 서비스의 일부이므로 IAM 역할을 사용하여 데이터베이스에 연결할 수 있습니다.  
(IAM 역할 활용)  

For example, EC2 instances with assigned IAM roles can authenticate directly to the database using those roles instead of a username and password.  
예를 들어, IAM 역할이 할당된 EC2 인스턴스는 사용자 이름/비밀번호 대신 해당 역할을 사용해 DB에 직접 인증할 수 있습니다.  
(실무 예시)  

This approach helps manage security centrally within AWS and IAM.  
이 방식은 AWS와 IAM에서 중앙 집중식 보안 관리를 가능하게 합니다.  
(중앙 관리 장점)  

---

## Network Access Control  
## 네트워크 접근 제어  

You can control network access to your database using security groups.  
보안 그룹을 사용하여 데이터베이스 네트워크 접근을 제어할 수 있습니다.  
(보안 그룹 활용)  

Security groups allow you to permit or block specific ports, IP addresses, or other security groups, thereby managing inbound and outbound traffic effectively.  
보안 그룹은 특정 포트, IP 주소, 다른 보안 그룹을 허용하거나 차단할 수 있어, 인바운드/아웃바운드 트래픽을 효과적으로 관리할 수 있습니다.  
(트래픽 관리 설명)  

---

## Access and Audit Logs  
## 접근 및 감사 로그  

RDS and Aurora do not provide SSH access since they are managed services, except when using the RDS Custom service from AWS.  
RDS와 Aurora는 관리형 서비스이므로 SSH 접근이 제공되지 않으며, AWS RDS Custom 서비스를 사용하는 경우를 제외합니다.  
(SSH 접근 제한)  

To monitor database activity, you can enable Audit Logs to track queries and other operations over time.  
DB 활동을 모니터링하려면 감사 로그(Audit Logs)를 활성화하여 쿼리 및 기타 작업을 추적할 수 있습니다.  
(감사 로그 활용)  

These logs are retained temporarily by default.  
이 로그들은 기본적으로 일시적으로 보관됩니다.  
(기본 보관 기간)  

For long-term retention, you should send audit logs to AWS CloudWatch Logs, a dedicated service for log storage and analysis.  
장기 보관을 위해 감사 로그를 AWS CloudWatch Logs로 전송해야 합니다.  
(장기 보관 방법)

---

## Summary  
## 요약  

This concludes the brief overview of security options available for RDS and Aurora databases.  
이로써 RDS와 Aurora 데이터베이스에서 제공되는 보안 옵션에 대한 간단한 개요를 마칩니다.  
(강의 마무리)

---

## Key Takeaways  
## 핵심 요약  

- RDS and Aurora support data encryption at rest using KMS, defined at database launch.  
- RDS와 Aurora는 데이터베이스 생성 시 정의된 KMS를 사용한 저장 데이터 암호화를 지원합니다.  

- In-flight encryption is enabled by default, requiring clients to use AWS TLS root certificates.  
- 전송 중 데이터 암호화는 기본 활성화되어 있으며, 클라이언트는 AWS TLS 루트 인증서를 사용해야 합니다.  

- Database authentication can be done via username/password or IAM roles for enhanced security.  
- 데이터베이스 인증은 사용자 이름/비밀번호 또는 IAM 역할을 통해 수행할 수 있어 보안을 강화합니다.  

- Network access is controlled through security groups, and audit logs can be sent to CloudWatch Logs for long-term retention.  
- 네트워크 접근은 보안 그룹으로 제어하며, 감사 로그는 장기 보관을 위해 CloudWatch Logs로 전송할 수 있습니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+400XP**
* 아이템: **"RDS Security 토큰"**
* 업적 달성: **"Guardian of Databases"** 🛡️

이 MD 자료는 **RDS와 Aurora의 저장/전송 암호화, 인증, 네트워크 제어, 감사 로그**까지 보안 관련 핵심 내용을 포함하고 있습니다.
