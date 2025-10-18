# Amazon RDS Hands On  
# Amazon RDS 실습  

---

## Creating an Amazon RDS Database Instance  
## Amazon RDS 데이터베이스 인스턴스 생성  

To begin, navigate to the Databases section on the left-hand side and click on Create database.  
먼저 왼쪽 메뉴에서 Databases 섹션으로 이동하여 'Create database'를 클릭합니다.  
(시작 단계)

---

## Selecting the Database Engine and Template  
## 데이터베이스 엔진 및 템플릿 선택  

On the database creation screen, select the database engine.  
데이터베이스 생성 화면에서 데이터베이스 엔진을 선택합니다.  
(기본 설정)

There are six engine types available, and two database creation methods: Standard Create and Easy Create.  
사용 가능한 엔진 유형은 6가지이며, 데이터베이스 생성 방식은 Standard Create와 Easy Create 두 가지가 있습니다.  
(옵션 설명)

To explore all options, choose Standard Create.  
모든 옵션을 확인하려면 Standard Create를 선택하세요.  
(권장 방법)

This method is more detailed but will show all necessary configurations for the exam.  
이 방법은 상세하지만, 시험에 필요한 모든 설정을 확인할 수 있습니다.  
(시험 대비)

Engine options include Aurora, MySQL, MariaDB, PostgreSQL, Oracle, and Microsoft SQL Server.  
엔진 옵션에는 Aurora, MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server가 있습니다.  
(엔진 종류)

For simplicity, select MySQL and use the provided version (e.g., MySQL 8.0.28).  
간단히 하기 위해 MySQL을 선택하고 제공된 버전을 사용합니다(예: MySQL 8.0.28).  
(예시)

The default selected version is sufficient.  
기본 선택된 버전으로 충분합니다.  
(권장)

Templates are available to match your use case: Free tier, Dev/Test, and Production.  
템플릿은 사용 사례에 따라 선택 가능: Free tier, Dev/Test, Production.  
(템플릿 설명)

Selecting the free tier pre-selects options suitable for free usage.  
Free tier를 선택하면 무료 사용에 적합한 옵션이 미리 선택됩니다.  
(무료 옵션)

For demonstration, select Production as a template but modify options to remain within the free tier.  
실습을 위해 Production을 선택하되, 무료 티어 범위 내 옵션으로 수정합니다.  
(실습 설정)

---

## Availability and Durability Options  
## 가용성과 내구성 옵션  

There are three options: Single DB instance, Multi-AZ, Multi-AZ DB Cluster.  
옵션은 세 가지: Single DB instance, Multi-AZ, Multi-AZ DB Cluster.  
(옵션 구분)

To stay within the free tier, select Single DB instance.  
무료 티어 범위 내에서는 Single DB instance를 선택합니다.  
(무료 티어 권장)

For a standby database, use a Multi-AZ option.  
스탠바이 DB는 Multi-AZ 옵션을 사용합니다.  
(재해 복구용)

Set the DB identifier to database-1.  
DB 식별자를 database-1로 설정합니다.  
(식별자 지정)

The master username is admin, and enter a password of your choice.  
마스터 사용자 이름은 admin으로, 비밀번호를 입력합니다.  
(사용자 설정)

---

## Instance Configuration  
## 인스턴스 구성  

The instance configuration determines the size of the underlying EC2 instance.  
인스턴스 구성은 기반 EC2 인스턴스의 크기를 결정합니다.  
(인스턴스 규모)

Options include Standard classes, Memory optimized classes, Burstable classes.  
옵션: Standard, Memory optimized, Burstable 클래스.  
(옵션 설명)

To remain within the free tier, select burstable classes and choose db.t3.micro.  
무료 티어 내에서는 Burstable 클래스 db.t3.micro를 선택합니다.  
(무료 티어 권장)

---

## Storage Configuration  
## 스토리지 구성  

For production, an io1 EBS volume is typical.  
프로덕션 환경에서는 io1 EBS 볼륨을 사용합니다.  
(일반적 설정)

For free tier, select a gp2 volume, which offers lower performance.  
무료 티어는 성능이 낮은 gp2 볼륨을 선택합니다.  
(무료 티어 권장)

Allocate 10 or 20 gigabytes of storage.  
스토리지를 10~20GB로 할당합니다.  
(스토리지 설정)

You can enable storage autoscaling to automatically increase the EBS volume size as needed, setting a maximum (e.g., 1,000 gigabytes).  
스토리지 자동 확장을 활성화하면 필요에 따라 EBS 크기를 자동 증가시킬 수 있으며 최대값을 설정할 수 있습니다(예: 1,000GB).  
(자동 확장)

---

## Connectivity and Security  
## 연결 및 보안  

You can connect the RDS instance to an EC2 compute resource for automatic networking configuration.  
RDS를 EC2와 연결하면 자동 네트워킹 구성이 가능합니다.  
(초보자 편의)

For this demonstration, select Do not connect to an EC2 compute resource.  
실습에서는 EC2 연결을 하지 않습니다.  
(실습 목적)

This requires specifying a VPC and subnet group manually.  
수동으로 VPC와 서브넷 그룹을 지정해야 합니다.  
(수동 설정)

Enable public access to allow connections from your computer.  
컴퓨터에서 접속 가능하도록 공개 액세스를 활성화합니다.  
(접속 허용)

Create a new security group named demo-database-mysql.  
새 보안 그룹 demo-database-mysql을 생성합니다.  
(보안 그룹 설정)

The default MySQL port is 3306.  
MySQL 기본 포트는 3306입니다.  
(포트 확인)

For database authentication, three mechanisms are available: Username and password, IAM database authentication, Kerberos authentication.  
데이터베이스 인증 방식: 사용자 이름/비밀번호, IAM 인증, Kerberos 인증.  
(인증 옵션)

Leave authentication as password-based for this setup.  
이 실습에서는 비밀번호 기반 인증을 사용합니다.  
(설정)

---

## Additional Configuration  
## 추가 구성  

You can enable monitoring for 60-second granularity, but it can be disabled.  
60초 단위 모니터링을 활성화할 수 있으며, 비활성화 가능.  
(모니터링)

Specify an initial database name, such as mydb.  
초기 DB 이름을 mydb로 지정합니다.  
(DB 이름)

Enable or disable automated backups, with a retention period of 1 to 35 days (set to 7 days here).  
자동 백업 활성화/비활성화 가능, 보존 기간 1~35일(여기서는 7일).  
(백업 설정)

You may also specify a backup window and export logs to CloudWatch for long-term retention.  
백업 시간대 지정 및 로그를 CloudWatch로 내보내 장기 보존 가능.  
(추가 설정)

Set a maintenance window for minor version upgrades and enable deletion protection to prevent accidental deletion.  
마이너 버전 업그레이드 유지보수 시간대 설정, 삭제 보호 활성화.  
(보호 기능)

The estimated monthly cost may show as $17, but using db.t2.micro qualifies for the free tier.  
월 예상 비용 $17로 표시될 수 있지만, db.t2.micro 사용 시 무료 티어에 해당합니다.  
(비용 안내)

---

## Database Creation and SQL Client Setup  
## 데이터베이스 생성 및 SQL 클라이언트 설정  

After reviewing all options, create the database.  
모든 옵션을 확인 후 데이터베이스를 생성합니다.  
(생성)

While the database is being created, download Sqlelectron, a SQL client for connecting to the database.  
DB 생성 중, SQL 클라이언트 Sqlelectron을 다운로드합니다.  
(클라이언트 설치)

Download the appropriate version for your operating system and install it.  
OS에 맞는 버전을 다운로드하고 설치합니다.  
(설치 안내)

Once the database is available, note the endpoint and port (3306), and the associated security group.  
DB가 준비되면 엔드포인트, 포트(3306), 연결된 보안 그룹을 확인합니다.  
(접속 정보)

Check the inbound rules to ensure TCP port 3306 is open, ideally restricted to your IP address.  
인바운드 규칙에서 TCP 포트 3306이 열려 있는지 확인, 가능하면 내 IP로 제한.  
(보안 확인)

If connection issues occur, consider allowing access from Anywhere (IPv4).  
연결 문제가 발생하면 Anywhere(IPv4)로 접근 허용 고려.  
(문제 해결)

---

## Connecting to the Database with Sqlelectron  
## Sqlelectron으로 DB 접속  

Open Sqlelectron and add a new database connection:  
Sqlelectron을 열고 새 DB 연결 추가:  

- Name: RDSDemo  
- 이름: RDSDemo  

- Type: MySQL  
- 유형: MySQL  

- Server address: Use the RDS endpoint  
- 서버 주소: RDS 엔드포인트 사용  

- Port: 3306  
- 포트: 3306  

- User: admin  
- 사용자: admin  

- Password: (your password)  
- 비밀번호: (설정한 비밀번호)  

- Initial database: mydb  
- 초기 DB: mydb  

Test the connection. If successful, save and connect.  
연결 테스트 후 성공하면 저장하고 연결.  
(연결 확인)

If not, verify public access and security group settings.  
실패 시 공개 액세스 및 보안 그룹 설정 확인.  
(문제 해결)

---

## Creating a Table and Inserting Data  
## 테이블 생성 및 데이터 삽입  

Once connected, you can execute SQL statements.  
연결 후 SQL 문을 실행할 수 있습니다.  
(기본 사용법)

For example, to create
```


a table:
예: 테이블 생성

```sql
CREATE TABLE mytable (
  name VARCHAR(20),
  first_name VARCHAR(20)
);
```

To insert data into the table:
테이블에 데이터 삽입

```sql
INSERT INTO mytable VALUES ('maarek', 'Stephane');
```

Selecting rows from the table will show the inserted data.
테이블에서 SELECT를 실행하면 삽입한 데이터 확인 가능.
(기본 SQL 실습)

---

## RDS Management Features

## RDS 관리 기능

The RDS database is fully managed.
RDS DB는 완전 관리형입니다.
(관리 편의)

You can create read replicas to increase read capacity, and choose whether to make them Multi-AZ for recovery purposes.
리드 리플리카 생성 가능, 필요 시 Multi-AZ로 구성 가능.
(확장/복구)

Monitoring features display metrics such as CPU utilization and connection counts, which are useful for scaling decisions.
모니터링 기능에서 CPU 사용량, 연결 수 등의 지표 확인 가능.
(확장 판단)

You can also create snapshots for backup and restore purposes, including point-in-time recovery and cross-region migration.
스냅샷 생성 가능, 시점 복구 및 지역 간 이전 가능.
(백업/복원)

RDS provides options to manage instance types, read replicas, and Multi-AZ deployments, all from a managed service perspective.
인스턴스 유형, 리드 리플리카, 멀티 AZ 배포 등 관리형 서비스에서 모두 관리 가능.
(관리 편의)

---

## Deleting the Database

## 데이터베이스 삭제

To delete the database, first remove termination protection by modifying the database settings.
DB 삭제 시 먼저 종료 보호 해제 필요.
(삭제 준비)

Scroll to the delete protection setting, disable it, and apply changes.
삭제 보호 설정에서 비활성화 후 변경 적용.
(설정 적용)

Once protection is removed, delete the database, optionally skipping the final snapshot.
보호 해제 후 DB 삭제, 최종 스냅샷 생략 가능.
(삭제)

Confirm deletion, acknowledging that all data will be lost.
삭제 확인, 모든 데이터 손실 동의.
(주의)

---

## Key Takeaways

## 핵심 요약

* Demonstrated step-by-step creation of an Amazon RDS MySQL database instance within the free tier.

* 무료 티어 내에서 Amazon RDS MySQL DB 인스턴스를 단계별로 생성 실습.

* Covered configuration options including engine selection, storage, connectivity, and security groups.

* 엔진 선택, 스토리지, 연결, 보안 그룹 등 구성 옵션 확인.

* Showed how to connect to the RDS instance using Sqlelectron and perform basic SQL operations.

* Sqlelectron으로 RDS 연결 및 기본 SQL 작업 실습.

* Explained monitoring, backup, snapshot, and deletion protection features for RDS management.

* RDS 관리 기능: 모니터링, 백업, 스냅샷, 삭제 보호 설명.

---

🎮 **게임 보상 지급**  
- 경험치: **+300XP**  
- 아이템: **"RDS SQL 클라이언트" (+10% 작업 효율)**  
- 업적 달성: **"RDS 실습 마스터"** 🏆  

이 자료를 통해 **RDS 생성, 연결, SQL 사용, 관리 기능** 실습 경험을 습득할 수 있습니다.
