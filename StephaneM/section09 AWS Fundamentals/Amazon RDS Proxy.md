# Amazon RDS Proxy  
# 아마존 RDS 프록시  

---

## Introduction to Amazon RDS Proxy  
## 아마존 RDS 프록시 소개  

Amazon RDS Proxy is a fully managed database proxy for Amazon RDS that you can deploy within your Virtual Private Cloud (VPC).  
Amazon RDS 프록시는 Amazon RDS용 완전 관리형 데이터베이스 프록시로, VPC 내에서 배포할 수 있습니다.  
(VPC 내 배포 가능한 관리형 프록시)  

Instead of having each application connect directly to your RDS database instance, applications connect to the RDS Proxy, which pools and shares database connections.  
각 애플리케이션이 RDS DB 인스턴스에 직접 연결하는 대신, 애플리케이션은 RDS 프록시에 연결하며, 프록시는 연결을 풀링하고 공유합니다.  
(연결 효율 개선)  

This approach reduces the number of direct connections to your database instance.  
이 방법은 DB 인스턴스로의 직접 연결 수를 줄입니다.  
(연결 수 감소)  

Pooling connections through RDS Proxy improves database efficiency by reducing stress on resources such as CPU and RAM.  
RDS 프록시를 통한 연결 풀링은 CPU와 RAM 같은 리소스 부담을 줄여 DB 효율을 향상시킵니다.  
(리소스 최적화)  

It also minimizes the number of open connections and reduces timeouts to your database instance.  
또한 열린 연결 수를 최소화하고 DB 인스턴스의 타임아웃 발생을 줄입니다.  
(타임아웃 방지)  

---

## Features of RDS Proxy  
## RDS 프록시 기능  

**Fully Serverless and Auto Scaling:** RDS Proxy automatically scales without requiring capacity management.  
**완전 서버리스 및 자동 확장:** RDS 프록시는 용량 관리 없이 자동으로 확장됩니다.  
(자동 확장 기능)  

**High Availability:** It operates across multiple Availability Zones (AZs), ensuring resilience.  
**고가용성:** 여러 가용 영역(AZ)에서 운영되어 안정성을 보장합니다.  
(다중 AZ 지원)  

**Failover Handling:** In the event of a failover from the primary to the standby RDS instance, RDS Proxy reduces failover time by up to 66%.  
**장애 조치 처리:** 기본 RDS에서 스탠바이 RDS로 장애 조치 시, RDS 프록시는 장애 조치 시간을 최대 66% 단축합니다.  
(빠른 장애 조치)  

It manages failover internally, so applications connected to the proxy do not need to handle failover themselves.  
프록시가 내부적으로 장애 조치를 관리하므로, 프록시 연결 애플리케이션은 별도로 장애를 처리할 필요가 없습니다.  
(애플리케이션 부담 감소)  

---

## Supported Database Engines  
## 지원 데이터베이스 엔진  

RDS Proxy supports the following database engines:  
RDS 프록시는 다음 데이터베이스 엔진을 지원합니다.  

- MySQL  
- PostgreSQL  
- MariaDB  
- Microsoft SQL Server  
- Aurora for MySQL  
- Aurora for PostgreSQL  

Importantly, using RDS Proxy does not require any changes to your application code.  
중요하게도, RDS 프록시 사용 시 애플리케이션 코드를 변경할 필요가 없습니다.  
(코드 변경 불필요)  

Instead of connecting directly to your RDS or Aurora database instance, your application connects to the RDS Proxy endpoint.  
애플리케이션은 RDS 또는 Aurora 인스턴스에 직접 연결하는 대신 RDS 프록시 엔드포인트에 연결합니다.  
(연결 방식)  

---

## Security and Authentication  
## 보안 및 인증  

RDS Proxy enables enforcement of IAM authentication for your database connections.  
RDS 프록시는 데이터베이스 연결에 대한 IAM 인증 적용을 지원합니다.  
(IAM 인증 적용)  

This ensures that only authorized users can connect to your RDS database instance using IAM credentials.  
이를 통해 권한 있는 사용자만 IAM 자격 증명을 사용해 RDS에 연결할 수 있습니다.  
(접근 제어)  

These credentials are securely stored and managed in AWS Secrets Manager.  
자격 증명은 AWS Secrets Manager에서 안전하게 저장 및 관리됩니다.  
(자격 증명 관리)  

---

## Network Accessibility  
## 네트워크 접근성  

RDS Proxy is never publicly accessible over the internet.  
RDS 프록시는 인터넷을 통해 공개적으로 접근할 수 없습니다.  
(보안 강화)  

It is only accessible from within your VPC, which enhances security by limiting exposure to internal network boundaries.  
VPC 내에서만 접근 가능하며, 내부 네트워크 경계로 제한되어 보안을 강화합니다.  
(VPC 제한 접근)  

---

## Use Case: AWS Lambda Functions  
## 사용 사례: AWS Lambda 함수  

AWS Lambda functions execute code in response to events and can scale rapidly, creating many instances that appear and disappear quickly.  
AWS Lambda 함수는 이벤트에 따라 코드를 실행하며, 빠르게 확장되어 많은 인스턴스가 빠르게 생성 및 삭제됩니다.  
(빠른 확장 환경)  

If each Lambda function opens a direct connection to your RDS database, this can lead to a large number of open connections, causing resource exhaustion and timeouts.  
각 Lambda 함수가 RDS에 직접 연결하면 연결 수가 급증하여 리소스 고갈과 타임아웃이 발생할 수 있습니다.  
(문제 상황)  

By using RDS Proxy, Lambda functions connect to the proxy, which pools these connections and reduces the number of direct connections to the database instance.  
RDS 프록시를 사용하면 Lambda 함수가 프록시에 연결되어 연결을 풀링하고 DB 인스턴스로의 직접 연결 수를 줄입니다.  
(해결 방법)  

This pooling solves the problem of connection overload caused by rapidly scaling Lambda functions.  
이 풀링은 빠르게 확장되는 Lambda 함수로 인한 연결 과부하 문제를 해결합니다.  
(문제 해결)  

---

## Summary  
## 요약  

RDS Proxy pools and minimizes connections to your RDS database instance.  
RDS 프록시는 RDS 인스턴스에 대한 연결을 풀링하고 최소화합니다.  
(핵심 기능)  

It reduces failover time by up to 66% by managing failover internally.  
내부적으로 장애 조치를 관리하여 장애 조치 시간을 최대 66% 단축합니다.  
(장애 조치 개선)  

Enforces IAM authentication with credentials stored securely in AWS Secrets Manager.  
IAM 인증을 적용하며 자격 증명을 AWS Secrets Manager에 안전하게 저장합니다.  
(보안 강화)  

Accessible only within your VPC, enhancing security.  
VPC 내에서만 접근 가능하여 보안을 강화합니다.  
(접근 제한)  

Particularly beneficial for managing connections from AWS Lambda functions that scale rapidly.  
특히 빠르게 확장되는 AWS Lambda 함수의 연결 관리를 위해 유용합니다.  
(Lambda 최적화)  

---

## Key Takeaways  
## 핵심 요약  

- Amazon RDS Proxy pools and shares database connections to improve efficiency and reduce resource stress.  
- Amazon RDS 프록시는 연결을 풀링하고 공유하여 효율성을 높이고 리소스 부담을 줄입니다.  

- It is fully serverless, auto-scaling, highly available across multiple Availability Zones, and reduces failover time by up to 66%.  
- 완전 서버리스, 자동 확장, 다중 AZ 고가용성을 제공하며, 장애 조치 시간을 최대 66% 단축합니다.  

- RDS Proxy supports multiple database engines without requiring application code changes and enforces IAM authentication with credentials stored securely in AWS Secrets Manager.  
- 애플리케이션 코드 변경 없이 여러 DB 엔진을 지원하며, IAM 인증을 적용하고 자격 증명을 안전하게 관리합니다.  

- It is accessible only within the VPC, enhancing security, and is especially beneficial for managing connections from rapidly scaling AWS Lambda functions.  
- VPC 내에서만 접근 가능하며 보안을 강화하고, 빠르게 확장되는 Lambda 함수 연결 관리에 특히 유용합니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+450XP**
* 아이템: **"RDS Proxy 카드"**
* 업적 달성: **"Connection Master"** 🔗

이 MD 자료는 **RDS Proxy의 개념, 기능, 지원 DB, 보안, 네트워크, Lambda 사용 사례**까지 핵심 내용을 포함하고 있어, 실제 환경 구성과 시험 대비에 모두 유용합니다.
