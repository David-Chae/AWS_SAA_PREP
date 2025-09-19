```markdown
# RDS & Aurora Migrations  
# RDS 및 Aurora 마이그레이션  

🎮 게임보상: "Aurora Migration Expert" +500 XP  

---

## Introduction to RDS and Aurora Migrations  
## RDS 및 Aurora 마이그레이션 소개  

This lecture covers methods to migrate databases to Aurora MySQL.  
이 강의에서는 데이터베이스를 Aurora MySQL로 마이그레이션하는 방법을 다룹니다.  

Although brief, this content is essential for exam preparation, possibly for one question.  
간단하지만, 시험 준비 시 중요한 내용이며 한 문제 정도 출제될 가능성이 있습니다.  

---

## Migration Options for RDS MySQL to Aurora MySQL  
## RDS MySQL → Aurora MySQL 마이그레이션 옵션  

If you have an RDS MySQL database and want to migrate it to Aurora MySQL, there are several options:  
RDS MySQL 데이터베이스를 Aurora MySQL로 마이그레이션하려면 몇 가지 옵션이 있습니다.  

- **Snapshot Restoration:** Take a database snapshot from the RDS MySQL database and restore this snapshot as a MySQL Aurora database.  
- **스냅샷 복원:** RDS MySQL 데이터베이스의 스냅샷을 생성한 뒤 Aurora MySQL로 복원합니다.  

  This method may involve some downtime because you need to stop operations on the original MySQL database before migrating to Aurora.  
  이 방법은 원본 MySQL 데이터베이스를 마이그레이션 전 중단해야 하므로 다운타임이 발생할 수 있습니다.  

- **Aurora Read Replica:** Create an Amazon Aurora Read Replica on top of your RDS MySQL instance.  
- **Aurora 읽기 전용 복제본:** RDS MySQL 인스턴스 위에 Aurora 읽기 전용 복제본을 생성합니다.  

  Once the replica lag reaches zero, meaning the Aurora replica has fully caught up with MySQL, you can promote it to its own database cluster.  
  복제 지연(replica lag)이 0이 되면 Aurora 복제본이 MySQL과 완전히 동기화된 것이며, 이를 독립적인 DB 클러스터로 승격할 수 있습니다.  

  This approach can take more time than the snapshot option and may incur additional costs due to network replication.  
  이 방법은 스냅샷 방식보다 시간이 더 걸리고, 네트워크 복제 때문에 추가 비용이 발생할 수 있습니다.  

- **External MySQL Database Migration Using Percona XtraBackup:**  
- **Percona XtraBackup을 이용한 외부 MySQL DB 마이그레이션:**  

  If you have a MySQL database external to RDS, you can back it up using the Percona XtraBackup utility.  
  RDS 외부의 MySQL 데이터베이스가 있다면, Percona XtraBackup 유틸리티를 사용해 백업할 수 있습니다.  

  This creates a backup file which you upload to Amazon S3.  
  이렇게 생성된 백업 파일을 Amazon S3에 업로드합니다.  

  Amazon Aurora supports directly importing this backup file into a new Aurora MySQL DB cluster.  
  Amazon Aurora는 이 백업 파일을 새 Aurora MySQL DB 클러스터로 직접 가져오는 것을 지원합니다.  

  Note that only the Percona XtraBackup utility is supported for this method.  
  이 방법은 Percona XtraBackup 유틸리티만 지원됩니다.  

- **MySQL Dump Utility:** You can run the MySQL Dump utility against a MySQL database and pipe the output into your existing Amazon Aurora database.  
- **MySQL Dump 유틸리티:** MySQL 데이터베이스에 대해 MySQL Dump를 실행하고 출력을 기존 Aurora DB로 전송할 수 있습니다.  

  This method is time-consuming and does not leverage Amazon S3.  
  이 방법은 시간이 오래 걸리며 Amazon S3를 활용하지 않습니다.  

- **Amazon Database Migration Service (DMS):** If both databases are operational, you can use Amazon DMS to perform continuous replication between the two databases.  
- **Amazon DMS:** 두 데이터베이스가 모두 운영 중이면 Amazon DMS를 사용하여 두 DB 간 지속적 복제를 수행할 수 있습니다.  

---

## Migration Options for PostgreSQL to Aurora PostgreSQL  
## PostgreSQL → Aurora PostgreSQL 마이그레이션 옵션  

The migration process for PostgreSQL databases is similar:  
PostgreSQL 데이터베이스의 마이그레이션 과정도 유사합니다.  

- You can restore database snapshots as Amazon Aurora PostgreSQL databases.  
- 데이터베이스 스냅샷을 Aurora PostgreSQL로 복원할 수 있습니다.  

- Alternatively, create an Amazon Aurora Read Replica of your PostgreSQL database.  
- 또는 PostgreSQL 데이터베이스의 Aurora 읽기 전용 복제본을 생성할 수 있습니다.  

  Once the replication lag is zero, promote it to its own database cluster.  
  복제 지연이 0이 되면 이를 독립적인 DB 클러스터로 승격합니다.  

- For external PostgreSQL databases, create a backup and upload it to Amazon S3.  
- 외부 PostgreSQL DB의 경우, 백업을 생성하고 Amazon S3에 업로드합니다.  

- Then, import the data using the AWS S3 Aurora extension, which creates a new database.  
- 이후 AWS S3 Aurora 확장을 사용하여 데이터를 가져오면 새 DB가 생성됩니다.  

- Finally, Amazon DMS can be used for continuous migration from PostgreSQL to Amazon Aurora.  
- 마지막으로, PostgreSQL → Aurora로의 지속적 마이그레이션에는 Amazon DMS를 사용할 수 있습니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on RDS and Aurora migrations.  
이로써 RDS 및 Aurora 마이그레이션 강의를 마칩니다.  

These methods provide flexible options depending on your database setup and downtime tolerance.  
이 방법들은 데이터베이스 환경과 허용 가능한 다운타임에 따라 유연한 옵션을 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- There are multiple methods to migrate RDS MySQL databases to Aurora MySQL, including snapshot restoration and creating Aurora Read Replicas.  
- RDS MySQL → Aurora MySQL 마이그레이션에는 스냅샷 복원과 Aurora 읽기 전용 복제본 생성 등 여러 방법이 있습니다.  

- Using Amazon Aurora Read Replicas allows for continuous replication with minimal downtime once replication lag reaches zero.  
- Aurora 읽기 전용 복제본을 사용하면 복제 지연이 0이 된 후 최소한의 다운타임으로 지속적 복제가 가능합니다.  

- External MySQL databases can be migrated using Percona XtraBackup utility backups imported via Amazon S3.  
- 외부 MySQL DB는 Percona XtraBackup으로 백업한 뒤 S3를 통해 Aurora로 가져올 수 있습니다.  

- Amazon DMS supports continuous replication for both MySQL and PostgreSQL migrations to Aurora.  
- Amazon DMS는 MySQL 및 PostgreSQL → Aurora 마이그레이션에서 지속적 복제를 지원합니다.  

- Similar migration options exist for PostgreSQL databases, including snapshot restoration, Aurora Read Replicas, S3 imports, and DMS.  
- PostgreSQL DB도 스냅샷 복원, Aurora 읽기 전용 복제본, S3 가져오기, DMS 등 유사한 마이그레이션 옵션이 존재합니다.  
```
