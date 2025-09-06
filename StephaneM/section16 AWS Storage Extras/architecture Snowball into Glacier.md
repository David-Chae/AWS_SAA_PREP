# Architecture: Snowball into Glacier

## Overview
This lecture covers a scenario relevant for the exam, focusing on how to import data using Snowball into Amazon Glacier.  
**한국어 설명:** 이 강의에서는 Snowball을 사용해 데이터를 Amazon Glacier로 가져오는 방법에 대해 다루며, 시험과 관련된 시나리오를 설명합니다.

---

## Key Concept
Snowball cannot import data directly into Amazon Glacier. The solution is to use Amazon S3 as an intermediate storage service.  
**한국어 설명:** Snowball은 데이터를 Amazon Glacier로 직접 가져올 수 없습니다. 따라서 **중간 저장소 역할로 Amazon S3를 사용**해야 합니다.

---

## Process
1. First, you import data into Amazon S3 using Snowball.  
   **한국어:** 먼저 Snowball을 이용해 데이터를 Amazon S3로 가져옵니다.
2. Then, you create a lifecycle policy on the S3 bucket to transition these objects into Amazon Glacier automatically.  
   **한국어:** 이후 S3 버킷에 **라이프사이클 정책(Lifecycle Policy)**을 설정하여 데이터를 자동으로 Amazon Glacier로 이동시킵니다.

> In summary, Snowball imports data into Amazon S3, and thanks to the S3 lifecycle policy, the data is transitioned into Amazon Glacier. This is an important point to remember for the exam.  
> **한국어:** 요약하면, Snowball은 데이터를 S3로 가져오고, S3 라이프사이클 정책을 통해 해당 데이터를 Glacier로 전환합니다. 이 과정은 시험에서 중요한 포인트입니다.

---

## Key Takeaways
- Snowball cannot import data directly into Amazon Glacier.  
  **한국어:** Snowball은 데이터를 Glacier로 직접 가져올 수 없습니다.
- The solution is to import data into Amazon S3 first using Snowball.  
  **한국어:** 해결 방법은 먼저 Snowball을 사용해 데이터를 S3로 가져오는 것입니다.
- An S3 lifecycle policy is used to transition data from Amazon S3 to Amazon Glacier.  
  **한국어:** S3 라이프사이클 정책을 사용하여 S3에서 Glacier로 데이터를 전환합니다.
- This approach is essential knowledge for the exam.  
  **한국어:** 이 과정은 시험 준비를 위해 반드시 알아야 하는 지식입니다.
