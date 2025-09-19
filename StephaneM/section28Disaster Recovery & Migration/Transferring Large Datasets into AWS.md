```markdown
# Transferring Large Datasets into AWS  
# AWS로 대용량 데이터 전송  

🎮 게임보상: "Data Transfer Novice" +500 XP  

---

## Overview of Data Transfer Methods into AWS  
## AWS로 데이터 전송 방법 개요  

This lecture provides a quick summary of the various methods available to transfer large amounts of data into AWS.  
이번 강의에서는 AWS로 대용량 데이터를 전송할 때 사용할 수 있는 다양한 방법을 간략히 요약합니다.  

It also discusses which method is most appropriate based on specific constraints.  
또한 특정 제약 조건에 따라 어떤 방법이 가장 적합한지도 다룹니다.  

---

## Scenario: Transferring 200 Terabytes with a 100 Mbps Connection  
## 시나리오: 100 Mbps 연결로 200TB 데이터 전송  

Consider the task of transferring 200 terabytes of data into the cloud using a 100 megabits per second internet connection.  
100Mbps 인터넷 연결을 사용하여 200TB 데이터를 클라우드로 전송하는 작업을 가정해 봅시다.  

---

## Option 1: Using Public Internet or Site-to-Site VPN  
## 옵션 1: 퍼블릭 인터넷 또는 사이트 간 VPN 사용  

One option is to use the public internet directly or establish a Site-to-Site VPN, which also utilizes the public internet.  
하나의 옵션은 퍼블릭 인터넷을 직접 사용하거나 사이트 간 VPN을 구축하는 것으로, VPN도 기본적으로 퍼블릭 인터넷을 사용합니다.  

The advantage of this approach is that it is immediate to set up and leverages the existing connection right away.  
이 방법의 장점은 즉시 설정할 수 있고 기존 연결을 바로 활용할 수 있다는 점입니다.  

---

### Time Calculation for Data Transfer Over Internet  
### 인터넷을 통한 데이터 전송 시간 계산  

To estimate the transfer time:  
전송 시간을 계산하려면:  

- Convert 200 terabytes to gigabytes and then to megabytes.  
  200TB를 기가바이트로, 다시 메가바이트로 변환합니다.  

- Convert megabytes to megabits by multiplying by eight.  
  메가바이트를 8배하여 메가비트로 변환합니다.  

- Divide by the connection speed of 100 megabits per second.  
  연결 속도인 100Mbps로 나눕니다.  

This results in approximately 16 million seconds, which is equivalent to 185 days.  
이 계산 결과 약 1,600만 초, 즉 185일이 걸립니다.  

Therefore, transferring 200 terabytes over a 100 Mbps internet connection would take almost half a year, which may be impractical depending on the use case.  
따라서 100Mbps 인터넷으로 200TB를 전송하면 거의 6개월이 걸리며, 경우에 따라 비현실적일 수 있습니다.  

---

## Option 2: AWS Direct Connect with 1 Gbps Line  
## 옵션 2: 1Gbps 회선 AWS Direct Connect 사용  

Using AWS Direct Connect with a provisioned one gigabit per second line is another option.  
1Gbps 회선으로 AWS Direct Connect를 사용하는 것이 또 다른 옵션입니다.  

However, establishing this connection requires a one-time setup that can take about a month if Direct Connect has not been used before.  
단, Direct Connect를 처음 사용하는 경우, 연결 설정에는 약 한 달의 시간이 필요할 수 있습니다.  

### Transfer Time with Direct Connect  
### Direct Connect를 통한 전송 시간  

Once the connection is established, the transfer speed is approximately ten times faster than the 100 Mbps internet connection.  
연결이 설정되면 전송 속도는 100Mbps 인터넷 연결보다 약 10배 빠릅니다.  

This reduces the transfer time to about 18.5 days, which is significantly quicker but still relatively long.  
이로 인해 전송 시간은 약 18.5일로 줄어들지만, 여전히 다소 긴 시간입니다.  

---

## Option 3: AWS Snowball  
## 옵션 3: AWS Snowball  

AWS Snowball is a physical data transport solution.  
AWS Snowball은 물리적 데이터 전송 솔루션입니다.  

Ordering Snowballs and completing the entire process—from delivery, loading data, shipping back to AWS, and data transfer—takes about one week end-to-end.  
Snowball을 주문하고 전체 과정을 완료하는 데(배송, 데이터 적재, AWS로 반환, 데이터 전송) 약 1주일이 소요됩니다.  

---

### Combining Snowball with Database Migration Service (DMS)  
### Snowball과 Database Migration Service(DMS) 결합  

If transferring a database, Snowball can be combined with AWS Database Migration Service (DMS) to transfer the remaining data after the initial bulk transfer.  
데이터베이스를 전송할 경우, 초기 대량 전송 후 남은 데이터를 AWS DMS와 결합하여 전송할 수 있습니다.  

---

## Ongoing Data Replication Options  
## 지속적인 데이터 복제 옵션  

For ongoing data replication rather than one-off transfers, options include:  
일회성 전송이 아닌 지속적인 데이터 복제를 위해 사용할 수 있는 옵션은 다음과 같습니다.  

- Site-to-Site VPN, suitable for transferring smaller amounts of data continuously.  
  소량 데이터를 지속적으로 전송할 때 적합한 사이트 간 VPN.  

- AWS Direct Connect.  
  AWS Direct Connect.  

- AWS Database Migration Service (DMS).  
  AWS Database Migration Service(DMS).  

- AWS DataSync.  
  AWS DataSync.  

These methods allow continuous or periodic data transfer over more reasonable internet lines.  
이 방법들은 합리적인 인터넷 회선을 통해 지속적 또는 주기적인 데이터 전송을 가능하게 합니다.  

---

## Summary of Use Cases  
## 사용 사례 요약  

Snowball is best suited for one-off large data transfers, significantly speeding up the initial data migration into AWS.  
Snowball은 일회성 대용량 데이터 전송에 가장 적합하며, 초기 AWS 데이터 마이그레이션을 크게 가속화합니다.  

Site-to-Site VPN and Direct Connect are more appropriate for ongoing replication with smaller data volumes.  
사이트 간 VPN과 Direct Connect는 소규모 데이터의 지속적 복제에 더 적합합니다.  

This lecture aims to help you understand which data transfer method is most appropriate based on your specific use case and constraints.  
이번 강의는 특정 사용 사례와 제약 조건에 따라 가장 적합한 데이터 전송 방법을 이해하도록 돕는 것을 목표로 합니다.  

---

## Exam Relevance  
## 시험 관련성  

In exams, you may be asked to determine the easiest, fastest, or most reliable way to transfer data into AWS depending on whether the dataset is small or large.  
시험에서는 데이터셋의 크기에 따라 AWS로 데이터를 전송하는 가장 쉽고, 빠르며, 신뢰할 수 있는 방법을 판단하라는 문제가 나올 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Transferring large datasets over a 100 Mbps internet connection can take several months.  
- 100Mbps 인터넷 연결로 대용량 데이터를 전송하면 수개월이 걸릴 수 있습니다.  

- AWS Direct Connect offers faster transfer speeds but requires a longer setup time.  
- AWS Direct Connect는 전송 속도를 높여주지만 설정 시간이 더 오래 걸립니다.  

- AWS Snowball is effective for one-time large data transfers, significantly reducing transfer time.  
- AWS Snowball은 일회성 대용량 전송에 효과적이며 전송 시간을 크게 단축시킵니다.  

- Ongoing data replication can be managed using Site-to-Site VPN, Direct Connect, DMS, or DataSync depending on data size and transfer frequency.  
- 지속적인 데이터 복제는 데이터 크기와 전송 빈도에 따라 Site-to-Site VPN, Direct Connect, DMS, DataSync를 사용해 관리할 수 있습니다.  
```
