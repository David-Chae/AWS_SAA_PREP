# S3 Performance  
# S3 성능  

---

## S3 Baseline Performance  
## S3 기본 성능  

Amazon S3 automatically scales to handle a very high number of requests with a low latency between 100 and 200 milliseconds to get the first byte from S3.  
Amazon S3는 자동으로 확장되어 매우 많은 요청을 처리하며, 첫 번째 바이트를 가져오는 데 100~200ms의 낮은 지연 시간을 제공합니다.  

This performance is quite fast by default.  
기본 성능만으로도 매우 빠릅니다.  

---

## Request Rates per Prefix  
## 접두사별 요청 속도  

In terms of request rates, each prefix in an S3 bucket supports:  
요청 속도 측면에서, S3 버킷의 각 접두사는 다음을 지원합니다:  

- 3,500 PUT, COPY, POST, or DELETE requests per second  
- 초당 3,500개의 PUT, COPY, POST, DELETE 요청  
- 5,500 GET or HEAD requests per second  
- 초당 5,500개의 GET 또는 HEAD 요청  

These limits apply per prefix, and there is no limit to the number of prefixes in a bucket.  
이 제한은 각 접두사별로 적용되며, 버킷 내 접두사 수에는 제한이 없습니다.  

---

## Understanding Prefixes  
## 접두사 이해  

Consider four objects named "file" located in different folders:  
다른 폴더에 위치한 "file"이라는 이름의 4개 객체를 고려합니다:  

- /folder1/sub1/file  
- /folder1/sub2/file  

The prefix is the part of the key between the bucket name and the file name.  
접두사는 버킷 이름과 파일 이름 사이의 키 부분입니다.  

For example, the prefix for /folder1/sub1/file is /folder1/sub1.  
예를 들어, /folder1/sub1/file의 접두사는 /folder1/sub1입니다.  

Each prefix independently supports the request rates mentioned above.  
각 접두사는 위에서 언급한 요청 속도를 독립적으로 지원합니다.  

Therefore, spreading requests evenly across multiple prefixes increases total throughput.  
따라서 여러 접두사에 요청을 고르게 분산하면 전체 처리량이 증가합니다.  

For example, with four different prefixes, you can achieve up to 22,000 GET or HEAD requests per second by distributing reads evenly across them.  
예를 들어, 네 개의 서로 다른 접두사에 요청을 균등하게 분산하면 초당 최대 22,000개의 GET 또는 HEAD 요청을 처리할 수 있습니다.  

---

## Optimizing S3 Performance  
## S3 성능 최적화  

### Multi-Part Upload  
### 멀티파트 업로드  

Multi-part upload is recommended for files larger than 100 megabytes and mandatory for files over 5 gigabytes.  
멀티파트 업로드는 100MB 이상의 파일에 권장되며, 5GB 이상 파일에는 필수입니다.  

It works by dividing a large file into smaller parts and uploading these parts in parallel to Amazon S3.  
큰 파일을 작은 파트로 나누고 이 파트를 병렬로 S3에 업로드하는 방식으로 작동합니다.  

Once all parts are uploaded, S3 assembles them back into the complete file.  
모든 파트가 업로드되면 S3가 다시 하나의 완전한 파일로 조립합니다.  

This parallelization speeds up transfers and maximizes bandwidth utilization.  
이 병렬 처리 덕분에 전송 속도가 빨라지고 대역폭 활용이 극대화됩니다.  

---

### S3 Transfer Acceleration  
### S3 전송 가속  

S3 Transfer Acceleration increases upload and download speeds by routing data through AWS edge locations.  
S3 전송 가속은 데이터를 AWS 엣지 로케이션을 통해 라우팅하여 업로드 및 다운로드 속도를 향상시킵니다.  

When uploading a file from the United States to an S3 bucket in Australia, the file is first sent quickly to a nearby edge location in the United States.  
미국에서 호주 S3 버킷으로 파일을 업로드할 때, 파일은 먼저 미국 내 가까운 엣지 로케이션으로 빠르게 전송됩니다.  

From there, the data is transferred over the fast, private AWS network to the S3 bucket in Australia.  
그 후, 데이터는 빠른 AWS 사설 네트워크를 통해 호주 S3 버킷으로 전송됩니다.  

This approach minimizes the use of the public internet and maximizes transfer speed.  
이 방법은 공용 인터넷 사용을 최소화하고 전송 속도를 최대화합니다.  

Transfer Acceleration is compatible with multi-part uploads and leverages over 200 edge locations worldwide.  
전송 가속은 멀티파트 업로드와 호환되며 전 세계 200개 이상의 엣지 로케이션을 활용합니다.  

---

### S3 Byte Range Fetches  
### S3 바이트 범위 가져오기  

To efficiently read large files, S3 supports byte range fetches, which allow clients to request specific byte ranges of a file.  
대용량 파일을 효율적으로 읽기 위해 S3는 바이트 범위 가져오기를 지원하며, 이를 통해 클라이언트는 파일의 특정 바이트 범위를 요청할 수 있습니다.  

This enables parallelized GET requests for different parts of a file, speeding up downloads.  
이를 통해 파일의 서로 다른 부분에 대해 병렬 GET 요청이 가능하며, 다운로드 속도가 빨라집니다.  

Additionally, if a failure occurs when fetching a specific byte range, only that smaller range needs to be retried, improving resilience.  
또한 특정 바이트 범위를 가져오는 중 오류가 발생하면 해당 작은 범위만 재시도하면 되므로 복원력이 향상됩니다.  

Use cases include:  
사용 사례는 다음과 같습니다:  

- Parallelizing downloads by requesting multiple byte ranges simultaneously.  
- 여러 바이트 범위를 동시에 요청하여 다운로드 병렬화  
- Retrieving only a partial amount of a file, such as the first 50 bytes containing header information.  
- 파일의 일부만 가져오기, 예: 헤더 정보를 포함한 처음 50바이트  

---

## Summary  
## 요약  

We have covered the baseline performance of Amazon S3, including request rate limits per prefix and low latency.  
각 접두사별 요청 속도 제한과 낮은 지연 시간을 포함한 Amazon S3의 기본 성능을 다뤘습니다.  

We discussed performance optimization techniques such as multi-part uploads, S3 Transfer Acceleration, and byte range fetches for efficient downloads.  
멀티파트 업로드, S3 전송 가속, 바이트 범위 가져오기와 같은 성능 최적화 기법을 논의했습니다.  

Understanding these concepts is essential for optimizing S3 usage and preparing for related exam topics.  
이 개념들을 이해하는 것은 S3 사용 최적화와 관련 시험 준비에 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Amazon S3 automatically scales to handle very high request rates with low latency.  
- Amazon S3는 매우 높은 요청 속도와 낮은 지연 시간으로 자동 확장됩니다.  

- Each prefix in an S3 bucket supports up to 3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second.  
- S3 버킷의 각 접두사는 초당 최대 3,500 PUT/COPY/POST/DELETE 및 5,500 GET/HEAD 요청을 지원합니다.  

- Multi-part upload is recommended for files over 100 MB and mandatory for files over 5 GB to speed up transfers by parallelizing uploads.  
- 멀티파트 업로드는 100MB 이상 파일에 권장되며, 5GB 이상 파일에는 필수로 병렬 업로드를 통해 전송 속도를 높입니다.  

- S3 Transfer Acceleration uses AWS edge locations to speed up uploads and downloads by minimizing public internet usage and maximizing private AWS network transfer.  
- S3 전송 가속은 AWS 엣지 로케이션을 사용하여 공용 인터넷 사용을 최소화하고 사설 AWS 네트워크 전송을 최대화하여 업로드 및 다운로드 속도를 향상시킵니다.  

- S3 Byte Range Fetches allow parallelized GET requests for specific byte ranges, improving download speed and resilience.  
- S3 바이트 범위 가져오기는 특정 바이트 범위에 대해 병렬 GET 요청을 허용하여 다운로드 속도와 복원력을 향상시킵니다.  

🎮 **게임보상:**

* **S3 Performance 학습 완료!**

  * 기본 성능 이해 +10
  * 멀티파트 업로드 & 전송 가속 +15
  * 바이트 범위 가져오기 이해 +10
    총 **35 XP 획득!** 🎉
