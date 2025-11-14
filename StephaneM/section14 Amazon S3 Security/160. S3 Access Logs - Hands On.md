# S3 Access Logs - Hands On  
# S3 접근 로그 실습  

---

## Introduction to S3 Access Logs  
## S3 접근 로그 소개  

In this session, we will practice enabling and using S3 access logs. The first step is to create an S3 bucket dedicated to storing access logs. This bucket will serve as our logging bucket.  
이번 세션에서는 S3 접근 로그를 활성화하고 사용하는 실습을 진행합니다. 첫 번째 단계는 접근 로그를 저장할 전용 S3 버킷을 생성하는 것입니다. 이 버킷이 로그 버킷 역할을 합니다.  

---

Next, open the AWS Management Console in another tab and select one of your existing buckets where you want to enable logging. Navigate to the Properties tab and scroll down to find Server Access Logging.  
다음으로, 다른 탭에서 AWS 관리 콘솔을 열고 로그를 활성화할 기존 버킷 중 하나를 선택합니다. Properties 탭으로 이동한 후 아래로 스크롤하여 Server Access Logging 항목을 찾습니다.  

---

Click Edit to enable server access logging. You will need to specify a destination bucket where the logs will be stored. For this example, select the previously created logging bucket named stefan-access-log-v3 as the destination.  
Edit를 클릭하여 서버 접근 로그를 활성화합니다. 로그가 저장될 대상 버킷을 지정해야 합니다. 이번 예제에서는 이전에 생성한 stefan-access-log-v3 버킷을 대상 버킷으로 선택합니다.  

---

Configure the destination region, which in this case is EU West 1. Optionally, you can specify a prefix for the log object keys, such as /logs, but for this demonstration, we will leave it blank.  
대상 리전을 설정합니다. 이번 경우에는 EU West 1입니다. 선택적으로 로그 객체 키에 대한 접두사(/logs 등)를 지정할 수 있지만, 이번 실습에서는 비워둡니다.  

---

The log object key format can be set to the default option, which is sufficient for our use case. After configuring these settings, click Save changes to enable server access logging.  
로그 객체 키 형식은 기본 옵션으로 설정할 수 있으며, 이번 실습에서는 충분합니다. 설정 후 Save changes를 클릭하여 서버 접근 로그를 활성화합니다.  

---

With server access logging enabled, any activity on the source bucket will be recorded and stored in the logging bucket. To generate activity, navigate to the source bucket's Objects tab and upload a file, for example, a JPEG image. This action will create access log entries.  
서버 접근 로그가 활성화되면, 소스 버킷에서 발생하는 모든 활동이 기록되어 로그 버킷에 저장됩니다. 활동을 생성하려면 소스 버킷의 Objects 탭으로 이동하여 파일(예: JPEG 이미지)을 업로드합니다. 이 작업으로 접근 로그 항목이 생성됩니다.  

---

Note that access logs may take some time to appear in the logging bucket. While waiting, it is important to verify the permissions. When enabling server access logging, the bucket policy of the logging bucket is automatically updated to allow Amazon S3's logging service to write objects into it.  
접근 로그가 로그 버킷에 표시되기까지 시간이 걸릴 수 있습니다. 기다리는 동안 권한을 확인하는 것이 중요합니다. 서버 접근 로그를 활성화하면 로그 버킷의 버킷 정책이 자동으로 업데이트되어 Amazon S3 로깅 서비스가 객체를 작성할 수 있도록 허용됩니다.  

---

After some time, refresh the logging bucket to see the generated log files. These objects contain detailed records of the access events. Opening a log file reveals information such as the API call made, the success status, the identity of the requester, the bucket accessed, the timestamp, and other relevant details.  
잠시 후 로그 버킷을 새로고침하여 생성된 로그 파일을 확인합니다. 이러한 객체에는 접근 이벤트의 상세 기록이 포함되어 있습니다. 로그 파일을 열면 API 호출, 성공 여부, 요청자 신원, 접근한 버킷, 타임스탬프 등 관련 세부 정보를 확인할 수 있습니다.  

---

## Conclusion  
## 결론  

This concludes our hands-on session on S3 access logs. We have learned how to enable server access logging, configure the logging bucket, generate access activity, and interpret the log files. These logs are valuable for auditing and monitoring access to your S3 buckets.  
이로써 S3 접근 로그 실습 세션을 마칩니다. 서버 접근 로그 활성화, 로그 버킷 구성, 접근 활동 생성, 로그 파일 해석 방법을 배웠습니다. 이러한 로그는 S3 버킷 접근 감사 및 모니터링에 유용합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Enabled server access logging on an S3 bucket by specifying a destination logging bucket.  
- 대상 로그 버킷을 지정하여 S3 버킷의 서버 접근 로그를 활성화했습니다.  

- Configured logging bucket policies to allow Amazon S3 to write access logs.  
- Amazon S3가 접근 로그를 작성할 수 있도록 로그 버킷 정책을 구성했습니다.  

- Demonstrated generating activity in the source bucket to produce access logs.  
- 소스 버킷에서 활동을 생성하여 접근 로그가 기록되는 과정을 시연했습니다.  

- Access logs provide detailed information about API calls, access times, and request outcomes.  
- 접근 로그는 API 호출, 접근 시간, 요청 결과 등 상세 정보를 제공합니다.  

🎮 **게임보상:**

* S3 접근 로그 실습 경험 +15 XP
* 로그 생성 및 버킷 정책 적용 이해 +10 XP
* 로그 분석 및 이벤트 추적 개념 습득 +5 XP
  총 **30 XP 획득!** 🎉
