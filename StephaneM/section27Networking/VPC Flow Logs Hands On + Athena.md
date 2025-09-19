```markdown
# VPC Flow Logs Hands On + Athena  
# VPC 플로우 로그 실습 + Athena  

🎮 게임보상: "Flow Log Analyst Badge" +600 XP  

---

## Introduction to VPC Flow Logs  
## VPC 플로우 로그 소개  

In this session, we will practice creating and analyzing VPC flow logs.  
이번 세션에서는 VPC 플로우 로그를 생성하고 분석하는 실습을 진행합니다.  

We start by navigating to our demo VPC under the Flow Logs section to create a new flow log.  
먼저 Flow Logs 섹션에서 데모 VPC로 이동하여 새 플로우 로그를 생성합니다.  

---

## Creating a Flow Log  
## 플로우 로그 생성  

We name this flow log DemoS3FlowLog.  
이 플로우 로그의 이름을 DemoS3FlowLog로 지정합니다.  

We then select a filter type: accept, reject, or all traffic.  
그 다음 필터 유형을 선택합니다: 허용(accept), 거부(reject), 또는 모든 트래픽(all).  

If debugging why some traffic is not passing through, the reject filter is useful; otherwise, accept or all are good options.  
일부 트래픽이 통과하지 않는 이유를 디버깅할 때는 reject 필터가 유용하며, 그렇지 않으면 accept 또는 all을 선택합니다.  

Next, we set the maximum aggregation interval, which determines how long to wait before aggregating logs.  
다음으로 최대 집계 간격(maximum aggregation interval)을 설정합니다. 이는 로그를 집계하기 전 대기 시간을 결정합니다.  

A one-minute interval can be specified, but this results in more records being created and can be expensive when writing to S3 or CloudWatch Logs.  
1분 간격을 지정할 수 있지만, 기록이 많아져 S3 또는 CloudWatch Logs에 쓸 때 비용이 증가할 수 있습니다.  

For demonstration purposes, we use a one-minute interval to speed up the process, though a ten-minute interval is usually better for longer-term use.  
데모 목적상 1분 간격을 사용하여 과정을 빠르게 진행하지만, 장기적으로는 10분 간격이 더 적합합니다.  

---

## Destination Options  
## 대상 옵션  

We can send flow logs to CloudWatch Logs, an Amazon S3 bucket, or Kinesis Data Firehose (in the same or different account).  
플로우 로그는 CloudWatch Logs, Amazon S3 버킷, Kinesis Data Firehose(동일 또는 다른 계정)로 전송할 수 있습니다.  

For this demo, we will use Amazon S3.  
이번 데모에서는 Amazon S3를 사용합니다.  

---

## Creating an S3 Bucket for Flow Logs  
## 플로우 로그용 S3 버킷 생성  

We navigate to the S3 service and create a bucket named demo-stephane-vpc-flow-logs-v2 in the same region as our VPC.  
S3 서비스로 이동하여 데모 VPC와 동일한 리전에서 demo-stephane-vpc-flow-logs-v2 버킷을 생성합니다.  

After creating the bucket, we copy its ARN from the Properties tab and paste it into the flow log creation form.  
버킷 생성 후 Properties 탭에서 ARN을 복사하여 플로우 로그 생성 폼에 붙여넣습니다.  

A resource-based bucket policy is automatically created and attached to allow the VPC service to write data into our S3 bucket.  
리소스 기반 버킷 정책이 자동으로 생성되어 VPC 서비스가 S3 버킷에 데이터를 쓸 수 있도록 연결됩니다.  

---

## Flow Log Format and Creation  
## 플로우 로그 형식 및 생성  

The default AWS flow log format is used.  
기본 AWS 플로우 로그 형식을 사용합니다.  

We then click on Create Flow Log to finalize the first flow log.  
Create Flow Log 버튼을 클릭하여 첫 번째 플로우 로그를 완료합니다.  

---

## Creating a Second Flow Log to CloudWatch Logs  
## 두 번째 플로우 로그 생성(CloudWatch Logs)  

We create another flow log named DemoFlowLog CloudWatch Logs with all traffic filtered and a one-minute aggregation interval.  
모든 트래픽을 필터링하고 1분 집계 간격으로 DemoFlowLog CloudWatch Logs라는 두 번째 플로우 로그를 생성합니다.  

This time, the destination is CloudWatch Logs.  
이번에는 대상이 CloudWatch Logs입니다.  

We need to create a log group and an IAM role for permissions.  
권한을 위해 로그 그룹과 IAM 역할을 생성해야 합니다.  

---

## Setting Up IAM Role for Flow Logs  
## 플로우 로그용 IAM 역할 설정  

Clicking on Set Up Permissions, we create a role with a custom trust policy.  
Set Up Permissions을 클릭하여 사용자 지정 신뢰 정책으로 역할을 생성합니다.  

The principal service is set to vpc-flow-logs.amazonaws.com (in quotes).  
주체 서비스(principal service)를 "vpc-flow-logs.amazonaws.com"으로 설정합니다.  

This role allows VPC flow logs to assume it.  
이 역할은 VPC 플로우 로그가 역할을 사용할 수 있도록 허용합니다.  

We attach the CloudWatch Logs full access policy to this role and name it flowlogsrole.  
CloudWatch Logs 전체 접근 정책을 연결하고 역할 이름을 flowlogsrole로 지정합니다.  

After creation, we verify the role exists.  
생성 후 역할이 존재하는지 확인합니다.  

---

## Creating a CloudWatch Log Group  
## CloudWatch 로그 그룹 생성  

In the CloudWatch Logs console, under Log Groups, we create a log group named VPCFlowLogs with a retention period of one day.  
CloudWatch Logs 콘솔에서 Log Groups 아래 VPCFlowLogs라는 로그 그룹을 생성하고 보존 기간을 1일로 설정합니다.  

After creation, the log group appears in the list.  
생성 후 로그 그룹이 목록에 표시됩니다.  

---

## Finalizing the Second Flow Log  
## 두 번째 플로우 로그 완료  

We complete the creation of the second flow log, resulting in two flow logs: one sending data to Amazon S3 and the other to CloudWatch Logs.  
두 번째 플로우 로그를 완료하면, 하나는 Amazon S3로, 다른 하나는 CloudWatch Logs로 데이터를 보내는 두 개의 플로우 로그가 생성됩니다.  

---

## Viewing Flow Logs in Amazon S3  
## Amazon S3에서 플로우 로그 보기  

In the S3 bucket, refreshing the Objects list shows AWSLogs folders created automatically.  
S3 버킷에서 객체 목록을 새로고침하면 AWSLogs 폴더가 자동으로 생성됩니다.  

Navigating through the folders, we find VPC flow logs with timestamps and log files containing the flow log data.  
폴더를 탐색하면 타임스탬프와 플로우 로그 데이터를 포함한 로그 파일이 있는 VPC 플로우 로그를 찾을 수 있습니다.  

---

## Viewing Flow Logs in CloudWatch Logs  
## CloudWatch Logs에서 플로우 로그 보기  

Refreshing CloudWatch Logs shows two log streams corresponding to the Elastic Network Interfaces (ENIs) in the account.  
CloudWatch Logs를 새로고침하면 계정 내 ENI에 해당하는 두 개의 로그 스트림이 표시됩니다.  

We identify the ENI ID of our Bastion Host instance by checking its networking details.  
네트워킹 세부 정보를 확인하여 Bastion Host 인스턴스의 ENI ID를 식별합니다.  

Matching the ENI ID in CloudWatch Logs, we observe traffic logs showing attempts to access the EC2 instance.  
CloudWatch Logs에서 ENI ID를 매칭하면 EC2 인스턴스 접근 시도를 보여주는 트래픽 로그를 확인할 수 있습니다.  

Many connection attempts are rejected, indicating scanning or attack attempts from external IP addresses.  
많은 연결 시도가 거부되며, 외부 IP에서 스캔 또는 공격 시도가 있었음을 나타냅니다.  

---

## Traffic Analysis  
## 트래픽 분석  

The logs show rejected traffic from various IP addresses, which are likely attackers scanning for vulnerabilities.  
로그에는 다양한 IP에서 거부된 트래픽이 표시되며, 이는 취약점을 찾기 위한 공격일 가능성이 높습니다.  

If an IP address is particularly troublesome, it can be blocked at the security group or network ACL level to prevent unwanted traffic.  
특정 IP가 문제가 되면 SG 또는 NACL에서 차단하여 원치 않는 트래픽을 막을 수 있습니다.  

Accepted traffic can be observed when performing legitimate activities, such as connecting to Google from the instance.  
합법적 활동(예: 인스턴스에서 Google 접속) 시 허용된 트래픽을 확인할 수 있습니다.  

Similar data is available in the Amazon S3 logs.  
유사한 데이터는 Amazon S3 로그에서도 확인할 수 있습니다.  

---

## Use Cases for Flow Logs Destinations  
## 플로우 로그 대상 사용 사례  

Use CloudWatch Logs for real-time analysis and metric filters to detect attacks or unusual traffic patterns.  
실시간 분석과 공격/이상 트래픽 감지를 위해 CloudWatch Logs 사용  

Use Amazon S3 for large-scale batch analysis, such as querying logs with Athena.  
대규모 배치 분석(예: Athena로 로그 조회)을 위해 Amazon S3 사용  

---

## Querying VPC Flow Logs with Athena  
## Athena로 VPC 플로우 로그 조회  

We will now practice querying the flow log data stored in Amazon S3 using Athena.  
이제 Athena를 사용하여 S3에 저장된 플로우 로그 데이터를 조회하는 실습을 진행합니다.  

First, we set up a query result location in Amazon S3 by creating a new bucket named demo-athena-stephane-v2.  
먼저 S3에 쿼리 결과 위치를 설정하기 위해 demo-athena-stephane-v2라는 새 버킷을 생성합니다.  

We copy its ARN and configure Athena to use this bucket for query results.  
ARN을 복사하여 Athena가 쿼리 결과에 이 버킷을 사용하도록 구성합니다.  

---

## Creating
```


Athena Table for VPC Flow Logs

## VPC 플로우 로그 Athena 테이블 생성

We search for AWS VPC flow logs Athena tutorials and find a statement to create a table.
AWS VPC 플로우 로그 Athena 튜토리얼을 검색하여 테이블 생성 구문을 찾습니다.

We paste this statement into Athena's query editor.
Athena 쿼리 에디터에 해당 구문을 붙여넣습니다.

We specify the location of the flow log data in the S3 bucket, following the path structure: logs/account-id/vpc-flow-logs/region.
S3 버킷에서 플로우 로그 데이터 위치를 지정하며, 경로 구조는 logs/account-id/vpc-flow-logs/region입니다.

We copy the S3 URI from the bucket and paste it into the query.
버킷에서 S3 URI를 복사하여 쿼리에 붙여넣습니다.

Running the statement creates a partitioned table for the flow logs.
구문을 실행하면 플로우 로그용 파티션 테이블이 생성됩니다.

---

## Adding Partitions to Athena Table

## Athena 테이블에 파티션 추가

We run an ALTER TABLE statement to add partitions for specific dates, specifying year, month, and day.
ALTER TABLE 구문을 실행하여 특정 날짜의 파티션을 추가하고 연도, 월, 일을 지정합니다.

This process is manual but can be automated with AWS Glue.
이 과정은 수동이지만 AWS Glue로 자동화할 수 있습니다.

After running the statement, the partition is successfully added.
구문 실행 후 파티션이 성공적으로 추가됩니다.

---

## Querying Flow Logs in Athena

## Athena에서 플로우 로그 조회

We perform a SELECT query to find all rejected traffic entries.
모든 거부된 트래픽 항목을 찾기 위해 SELECT 쿼리를 수행합니다.

The query returns 46 results, showing fields such as day, date, interface ID, source address, action (reject), and protocol.
쿼리 결과 46개가 반환되며, day, date, interface ID, source address, action(reject), protocol 등의 필드를 보여줍니다.

Athena allows complex queries to analyze attack patterns, identify frequent attacking IP addresses, and determine where attacks are most prevalent.
Athena를 사용하면 공격 패턴 분석, 빈번한 공격 IP 식별, 공격이 가장 많이 발생한 위치 파악 등의 복잡한 쿼리를 수행할 수 있습니다.

---

## Conclusion

## 결론

In this demonstration, we have seen how to set up VPC flow logs, send them to CloudWatch Logs and Amazon S3, and use Athena to query the logs stored in S3 for analysis.
이번 실습에서는 VPC 플로우 로그를 설정하고 CloudWatch Logs 및 Amazon S3로 전송하며, Athena로 S3에 저장된 로그를 조회하는 방법을 확인했습니다.

Finally, to avoid ongoing costs, we delete the flow logs created during this session.
마지막으로 지속적인 비용을 피하기 위해 이번 세션에서 생성한 플로우 로그를 삭제합니다.

---

## Key Takeaways

## 핵심 요약

* Created VPC flow logs with options for filtering traffic and aggregation intervals.

* 트래픽 필터링 및 집계 간격 옵션으로 VPC 플로우 로그 생성

* Configured flow logs to send data to both Amazon S3 buckets and CloudWatch Logs.

* 플로우 로그를 Amazon S3 및 CloudWatch Logs로 전송하도록 구성

* Set up IAM roles and CloudWatch log groups for flow log permissions.

* 플로우 로그 권한을 위한 IAM 역할과 CloudWatch 로그 그룹 설정

* Used Athena to query VPC flow log data stored in S3 for analysis.

* S3에 저장된 VPC 플로우 로그 데이터를 Athena로 조회하여 분석

```
```
