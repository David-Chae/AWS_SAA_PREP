```md
# Athena Hands On
# Athena 실습
# → Amazon Athena를 활용한 실습 강의

## Using Athena to Query Data from Amazon S3
## Athena를 사용하여 Amazon S3 데이터 쿼리하기
## → 실습 목표 및 개요

In this lecture, we will use the Athena service to query data stored in Amazon S3 buckets.  
이번 강의에서는 Athena 서비스를 사용하여 Amazon S3 버킷에 저장된 데이터를 쿼리합니다.  
→ 실습 목표: Athena로 S3 데이터 조회.

We begin by launching the Athena query editor, which provides access to the user interface for running queries.  
먼저 Athena 쿼리 편집기를 실행하여 쿼리를 수행할 사용자 인터페이스에 접근합니다.  
→ 쿼리 편집기 사용법 이해.

## Setting Up Query Result Location
## 쿼리 결과 위치 설정
## → 결과 저장용 S3 버킷 설정

Before running our first query, it is necessary to set up a query result location in Amazon S3.  
첫 쿼리를 실행하기 전에 Amazon S3에 쿼리 결과 위치를 설정해야 합니다.  
→ Athena는 결과를 저장할 S3 버킷 필요.

This involves specifying an S3 bucket where Athena will store the results of queries.  
Athena가 쿼리 결과를 저장할 S3 버킷을 지정하는 과정입니다.  
→ 실습 단계 이해.

To do this, we edit the Athena settings and enter the name of an S3 bucket designated for query results.  
Athena 설정을 수정하여 쿼리 결과용 S3 버킷 이름을 입력합니다.  
→ 설정 경로 이해.

If such a bucket does not exist, we create one in the S3 console.  
해당 버킷이 없다면 S3 콘솔에서 새로 생성합니다.  
→ S3 버킷 생성 과정.

For example, we create a bucket named aws-athena-stephane in the EU Central 1 region.  
예를 들어, EU Central 1 리전에서 aws-athena-stephane라는 버킷을 생성합니다.  
→ 버킷 명명 규칙 및 리전 이해.

The bucket name must be unique globally.  
버킷 이름은 전 세계적으로 유일해야 합니다.  
→ S3 버킷 제약 사항 강조.

After creating the bucket, we copy its name and paste it into the Athena settings as the query result location.  
버킷 생성 후 이름을 복사하여 Athena 설정의 쿼리 결과 위치에 붙여넣습니다.  
→ 설정 완료 과정.

This ensures that Athena can browse and store query results in the specified bucket.  
이로써 Athena가 지정된 버킷에서 결과를 저장하고 조회할 수 있습니다.  
→ 결과 저장 보장.

Once saved, all query results will be stored there.  
설정 저장 후 모든 쿼리 결과는 해당 버킷에 저장됩니다.  
→ 최종 확인.

## Running Queries on S3 Access Logs
## S3 접근 로그 쿼리 실행
## → 실습 예제: S3 Access Logs

Next, we run queries on a specific S3 bucket containing access logs.  
다음으로 접근 로그가 저장된 특정 S3 버킷에서 쿼리를 실행합니다.  
→ 실습 대상 데이터 정의.

We have access logs stored in an S3 bucket, and we want to query all objects within this bucket.  
S3 버킷에 저장된 모든 접근 로그 객체를 쿼리합니다.  
→ 실습 목표.

First, we create a database in Athena to organize our data.  
먼저 Athena에서 데이터를 정리하기 위해 데이터베이스를 생성합니다.  
→ Athena 데이터 구조 이해.

Using SQL in the Athena query editor, we create a database named s3_access_logs_db.  
Athena 쿼리 편집기에서 SQL로 s3_access_logs_db라는 데이터베이스를 생성합니다.  
→ SQL 쿼리 실습.

Once created, this database appears alongside the default database in the Athena interface.  
생성 후 Athena 인터페이스에서 기본 데이터베이스와 함께 표시됩니다.  
→ UI 확인.

## Creating a Table for Access Logs
## 접근 로그용 테이블 생성
## → 테이블 생성 및 데이터 매핑

We then create a table within the database to represent the access logs.  
데이터베이스 내에서 접근 로그를 나타내는 테이블을 생성합니다.  
→ SQL 테이블 생성 이해.

The SQL query to create this table is sourced from the Amazon S3 and Athena documentation.  
테이블 생성 SQL은 S3와 Athena 문서에서 참조합니다.  
→ 공식 문서 활용.

The only modification needed is to update the location to point to our target S3 bucket and prefix if applicable.  
유일한 수정 사항은 S3 버킷 위치와 필요 시 프리픽스 업데이트입니다.  
→ 위치 지정 중요.

In our case, since all objects are at the top level of the bucket, no prefix is necessary.  
이번 실습에서는 모든 객체가 최상위에 있어 프리픽스는 필요 없습니다.  
→ 실습 데이터 구조 확인.

We ensure the location path ends with a trailing slash and run the query to create the table.  
경로가 슬래시로 끝나는지 확인하고 쿼리를 실행하여 테이블을 생성합니다.  
→ SQL 실행 절차.

After the table is created, it appears in the Athena interface along with all its fields.  
테이블 생성 후 모든 필드와 함께 Athena 인터페이스에 표시됩니다.  
→ UI 확인.

We can preview the table by querying the first 10 rows, which shows details such as bucket owner, bucket name, request date and time, IP address, requester, request ID, and more.  
첫 10개 행을 쿼리하여 테이블을 미리보기할 수 있으며, 버킷 소유자, 이름, 요청 시간, IP, 요청자, 요청 ID 등 세부 정보 확인 가능.  
→ 데이터 확인 방법 이해.

## Benefits of Using Athena
## Athena 사용 장점
## → 서버리스 SQL 활용 이점

Athena simplifies data analysis by allowing us to query data directly in Amazon S3 without the need to manually inspect individual files.  
Athena는 개별 파일을 확인하지 않고 S3 데이터를 직접 쿼리할 수 있어 데이터 분석을 단순화합니다.  
→ 서버리스 장점.

This serverless service enables us to use standard SQL to analyze large datasets efficiently.  
서버리스 서비스로 대규모 데이터셋도 SQL로 효율적으로 분석할 수 있습니다.  
→ 대규모 데이터 처리 시험 포인트.

## Performing Advanced Queries
## 고급 쿼리 수행
## → 집계 및 필터링

We can perform more advanced queries such as aggregations.  
집계와 같은 고급 쿼리를 수행할 수 있습니다.  
→ 데이터 분석 확장.

For example, we can count all requests grouped by HTTP status and request URI operation.  
예를 들어, HTTP 상태 코드와 요청 URI별로 요청 수를 집계할 수 있습니다.  
→ SQL 집계 예시.

Running such queries scans the relevant data and returns summarized results.  
쿼리 실행 시 관련 데이터를 스캔하고 요약 결과를 반환합니다.  
→ 효율적 분석 이해.

The query results show counts of various HTTP status codes, such as 404 errors and 200 successes.  
쿼리 결과는 404 오류, 200 성공 등 HTTP 상태 코드별 요청 수를 보여줍니다.  
→ 결과 해석.

This allows us to identify potential issues, such as unexpected not found errors, which may indicate problems that require investigation.  
예상치 못한 not found 오류와 같은 잠재적 문제를 식별할 수 있으며, 이는 조사 필요성을 의미합니다.  
→ 실무/시험 포인트.

We can also query for unauthorized access attempts by filtering for HTTP status code 403.  
HTTP 403 코드 필터링으로 무단 접근 시도를 쿼리할 수도 있습니다.  
→ 보안 분석 실습.

This helps us detect if there are any unauthorized access attempts to our bucket, enabling us to take appropriate security measures.  
버킷에 대한 무단 접근 시도를 감지하고 적절한 보안 조치를 취할 수 있습니다.  
→ 보안 대응 이해.

## Summary
## 요약
## → 실습 정리

In summary, we used the Athena service to query data stored in Amazon S3 easily and serverlessly.  
요약하면, Athena 서비스를 사용하여 S3 데이터를 쉽고 서버리스로 쿼리했습니다.  
→ 핵심 정리.

The process involved creating a database and table in Athena, setting up an S3 bucket for query results, and running SQL queries to analyze the data directly within Athena's query editor.  
이 과정에는 Athena에서 데이터베이스와 테이블 생성, 쿼리 결과용 S3 버킷 설정, Athena 쿼리 편집기 내 SQL 실행이 포함됩니다.  
→ 단계별 과정 요약.

Athena is one of the most convenient AWS services for querying large datasets without managing infrastructure.  
Athena는 인프라 관리 없이 대규모 데이터셋을 쿼리할 수 있는 가장 편리한 AWS 서비스 중 하나입니다.  
→ 장점 강조.

This concludes the lecture, and we look forward to exploring more in the next session.  
강의가 여기서 종료되며, 다음 세션에서 더 많은 내용을 다룰 예정입니다.  
→ 마무리.

## Key Takeaways
## 핵심 요약
## → 시험/실무 포인트

Set up an Amazon S3 bucket as the query result location for Athena.  
Athena 쿼리 결과를 저장할 S3 버킷을 설정합니다.  
→ 기본 필수 단계.

Created a database and table in Athena to query S3 access logs using SQL.  
Athena에서 SQL로 S3 접근 로그를 쿼리하기 위해 데이터베이스와 테이블을 생성했습니다.  
→ 실습 완료.

Used Athena's query editor to run SQL queries on S3 data without managing servers.  
서버 관리 없이 Athena 쿼리 편집기로 S3 데이터를 SQL로 쿼리했습니다.  
→ 서버리스 활용 이해.

Performed data analysis such as counting requests by HTTP status and identifying unauthorized access attempts.  
HTTP 상태별 요청 수 집계, 무단 접근 시도 탐지 등의 데이터 분석 수행.  
→ 실무 활용 예시.
```

🎮 **게임보상: Athena 실습 마스터! 🏆**
→ 서버리스 SQL 쿼리와 S3 데이터 분석 실무 능력 상승 완료!
