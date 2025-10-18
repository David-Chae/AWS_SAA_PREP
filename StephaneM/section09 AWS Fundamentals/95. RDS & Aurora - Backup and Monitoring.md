# RDS & Aurora - Backup and Monitoring  
# RDS 및 Aurora - 백업과 모니터링  

---

## RDS Backup Overview  
## RDS 백업 개요  

RDS offers automated backups, meaning the service automatically performs a daily full backup of the database during your designated backup window.  
RDS는 자동 백업을 제공하며, 지정된 백업 창 동안 매일 전체 데이터베이스 백업을 자동으로 수행합니다.  
(자동 백업 기능 설명)  

Additionally, transaction logs are backed up every five minutes.  
또한 트랜잭션 로그는 5분마다 백업됩니다.  
(트랜잭션 로그 백업 설명)  

This setup ensures that the earliest backup available is only five minutes old, allowing restoration to any point in time up to five minutes ago.  
이 구성으로 인해 가장 이른 백업도 5분 전까지만 존재하며, 최대 5분 전 시점까지 복원이 가능합니다.  
(포인트 인 타임 복원 가능성)

The automated backup retention period can be set between one and thirty-five days.  
자동 백업 보존 기간은 1일에서 35일 사이로 설정할 수 있습니다.  
(보존 기간 설정 안내)  

To disable automated backups, you would set the retention period to zero.  
자동 백업을 비활성화하려면 보존 기간을 0으로 설정합니다.  
(자동 백업 해제 방법)

---

## Manual DB Snapshots  
## 수동 DB 스냅샷  

Manual database snapshots are backups triggered manually by the user.  
수동 DB 스냅샷은 사용자가 직접 트리거하는 백업입니다.  
(수동 백업 정의)  

Unlike automated backups, these snapshots can be retained indefinitely, allowing you to keep them as long as you want.  
자동 백업과 달리, 수동 스냅샷은 무기한 보관 가능하며 원하는 만큼 유지할 수 있습니다.  
(장기 보관 가능)

---

## Cost-saving Backup Strategy  
## 비용 절감 백업 전략  

A useful trick is to use manual snapshots to save costs.  
비용 절감을 위해 수동 스냅샷을 활용하는 방법이 있습니다.  
(전략 제안)  

For example, if you have an RDS database that you only use for two hours per month, instead of stopping the database—which still incurs storage costs—you can take a snapshot after use and delete the original database.  
예를 들어, 월 2시간만 사용하는 RDS DB가 있다면, DB를 중지하면 저장 비용이 발생하므로 사용 후 스냅샷을 만들고 원본 DB를 삭제할 수 있습니다.  
(비용 절약 사례)  

The snapshot costs significantly less than the storage for an active RDS database.  
스냅샷 비용은 활성 RDS DB 저장소보다 훨씬 저렴합니다.  
(비용 비교)

When you need to use the database again, you restore the snapshot.  
다시 DB가 필요할 때 스냅샷을 복원하면 됩니다.  
(복원 방법)

---

## Aurora Backups  
## Aurora 백업  

Aurora backups are similar to RDS backups.  
Aurora 백업은 RDS 백업과 유사합니다.  
(유사성 설명)  

Automated backups have a retention period from one to thirty-five days but cannot be disabled, unlike in RDS.  
자동 백업은 1~35일 동안 보존되지만 RDS와 달리 비활성화할 수 없습니다.  
(자동 백업 제한)

Aurora also supports point-in-time recovery within this timeframe.  
Aurora는 이 기간 내 포인트 인 타임 복원도 지원합니다.  
(복원 기능)

Manual DB snapshots in Aurora are also manually triggered by the user and can be retained indefinitely.  
Aurora의 수동 DB 스냅샷도 사용자가 직접 트리거하며, 무기한 보관할 수 있습니다.  
(수동 스냅샷 설명)

---

## Restore Options  
## 복원 옵션  

You can restore an RDS or Aurora backup or snapshot into a new database instance.  
RDS 또는 Aurora의 백업/스냅샷을 새 DB 인스턴스로 복원할 수 있습니다.  
(복원 기본 원리)

Restoring either an automated backup or a manual snapshot creates a new database.  
자동 백업이든 수동 스냅샷이든 복원하면 새로운 DB가 생성됩니다.  
(복원 결과)

Additionally, you can restore a MySQL RDS database from Amazon S3.  
추가로, Amazon S3에서 MySQL RDS DB를 복원할 수 있습니다.  
(S3 복원 옵션)

Amazon S3 is an object storage service in AWS.  
Amazon S3는 AWS의 객체 스토리지 서비스입니다.  
(서비스 설명)

The process involves creating a backup of your on-premises database, uploading it to Amazon S3, and then restoring the backup file onto a new RDS instance running MySQL.  
이 과정은 온프레미스 DB 백업 생성 → S3 업로드 → 새로운 MySQL RDS 인스턴스에 복원 순으로 진행됩니다.  
(복원 절차)

For restoring to a MySQL Aurora cluster, you must use a backup created with Percona XtraBackup software.  
Aurora MySQL 클러스터로 복원하려면 Percona XtraBackup으로 생성한 백업을 사용해야 합니다.  
(복원 조건)

This backup file is uploaded to Amazon S3 and then restored onto a new Aurora cluster running MySQL.  
백업 파일을 S3에 업로드 후 새로운 Aurora MySQL 클러스터로 복원합니다.  
(복원 과정)

The key difference is that restoring into RDS MySQL requires only a database backup, whereas restoring into Aurora MySQL requires a Percona XtraBackup backup.  
주요 차이점: RDS MySQL은 일반 DB 백업만 필요하지만, Aurora MySQL은 Percona XtraBackup 백업이 필요합니다.  
(핵심 차이)

---

## Aurora Database Cloning  
## Aurora DB 클로닝  

Aurora supports database cloning, which allows you to create a new Aurora database cluster from an existing one.  
Aurora는 DB 클로닝을 지원하며, 기존 Aurora 클러스터에서 새 클러스터를 생성할 수 있습니다.  
(클로닝 기능 소개)

For example, if you have a production Aurora database and want to run tests in a staging environment, you can clone the production database to create a staging database quickly.  
예: 운영 Aurora DB가 있고 스테이징 환경에서 테스트를 하려면, 운영 DB를 클론해 빠르게 스테이징 DB를 만들 수 있습니다.  
(실용 사례)

Cloning is faster than snapshot and restore because it uses a copy-on-write protocol.  
클로닝은 복사-쓰기(copy-on-write) 프로토콜을 사용하므로 스냅샷 후 복원보다 빠릅니다.  
(속도 이유)

Initially, the cloned database uses the same data volume as the original cluster, which is efficient and fast since no data copying occurs.  
초기 클론 DB는 원본 클러스터와 동일한 데이터 볼륨을 사용하며, 데이터 복사가 없으므로 효율적이고 빠릅니다.  
(작동 원리)

As updates are made to either the production or staging database, new storage is allocated, and data is copied and separated.  
운영 또는 스테이징 DB에 업데이트가 발생하면, 새로운 스토리지가 할당되고 데이터가 복사 및 분리됩니다.  
(데이터 분리 과정)

This approach provides the benefits of speed and cost-effectiveness, allowing you to have a staging database from a production database without impacting the production environment or going through snapshot and restore processes.  
이 방법은 속도와 비용 효율성을 제공하며, 스냅샷/복원 없이 운영 환경에 영향 없이 스테이징 DB를 생성할 수 있습니다.  
(효과 설명)

---

## Summary  
## 요약  

We have covered the options for backup and restore in RDS and Aurora, as well as the cloning feature in Aurora.  
이번 강의에서는 RDS 및 Aurora의 백업/복원 옵션과 Aurora 클로닝 기능을 다뤘습니다.  
(내용 정리)

These tools provide flexible and efficient ways to manage database backups, restorations, and testing environments.  
이 도구들은 DB 백업, 복원, 테스트 환경 관리를 유연하고 효율적으로 수행할 수 있도록 합니다.  
(실무적 가치)

---

## Key Takeaways  
## 핵심 요약  

- RDS provides automated backups with daily full backups and transaction log backups every five minutes, allowing point-in-time recovery within the retention period.  
- RDS는 매일 전체 백업과 5분 단위 트랜잭션 로그 백업을 제공하여 보존 기간 내 포인트 인 타임 복원을 지원합니다.  

- Manual DB snapshots in RDS can be retained indefinitely, unlike automated backups which expire.  
- RDS의 수동 DB 스냅샷은 자동 백업과 달리 무기한 보관할 수 있습니다.  

- Aurora backups are similar to RDS but automated backups cannot be disabled.  
- Aurora 백업은 RDS와 유사하지만 자동 백업은 비활성화할 수 없습니다.  

- Restoring backups or snapshots creates a new database instance; MySQL RDS databases can also be restored from Amazon S3 backups.  
- 백업/스냅샷 복원 시 새로운 DB 인스턴스가 생성되며, MySQL RDS는 S3 백업에서 복원할 수도 있습니다.  

- Aurora supports database cloning using copy-on-write, enabling fast and cost-effective creation of staging environments without impacting production.  
- Aurora는 copy-on-write 방식의 DB 클로닝을 지원하여 운영 환경에 영향을 주지 않고 스테이징 환경을 빠르고 비용 효율적으로 생성할 수 있습니다.  

---

🎮 **게임 보상 지급**

* 경험치: **+450XP**
* 아이템: **"Aurora Backup & Cloning 토큰"**
* 업적 달성: **"Master of Backup & Restore"** 🏆

이 MD 자료는 **RDS와 Aurora의 백업/복원, 수동 스냅샷, Aurora 클로닝**까지 실무와 시험 대비 핵심 내용을 포함하고 있습니다.
