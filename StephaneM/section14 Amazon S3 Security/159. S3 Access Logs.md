# S3 Access Logs  
# S3 접근 로그  

---

## Introduction to S3 Access Logs  
## S3 접근 로그 소개  

For audit purposes, you may want to log all access made to your S3 buckets. This means that any request made to your S3 bucket from any account, whether authorized or denied, will be logged as a file into another S3 bucket. This data can then be analyzed using data analysis tools such as Amazon Athena.  
감사(Audit) 목적으로 S3 버킷에 대한 모든 접근을 기록하고 싶을 수 있습니다. 이는 승인된 요청이든 거부된 요청이든 관계없이 모든 S3 버킷 요청이 다른 S3 버킷에 파일로 기록된다는 의미입니다. 이후 이 데이터를 Amazon Athena와 같은 데이터 분석 도구를 사용해 분석할 수 있습니다.  

---

## Logging Bucket Requirements  
## 로그 버킷 요구사항  

The target logging buckets must be in the same AWS region as the buckets being monitored.  
로그를 기록할 대상 버킷은 모니터링 대상 버킷과 동일한 AWS 리전에 있어야 합니다.  

---

## How S3 Access Logging Works  
## S3 접근 로그 작동 방식  

You make requests against your S3 buckets and enable access logging. All requests are then logged into the designated logging buckets.  
S3 버킷에 요청을 보내고 접근 로그를 활성화하면, 모든 요청이 지정된 로그 버킷에 기록됩니다.  

---

## Log Format  
## 로그 형식  

There is a specific format for these logs, which can be found at the official AWS URL for log formats.  
이 로그에는 특정 형식이 있으며, AWS 공식 로그 형식 URL에서 확인할 수 있습니다.  

---

## Important Warning  
## 중요 경고  

Never set your logging bucket to be the same as the bucket you are monitoring. Doing so will create a logging loop that is infinite, causing your bucket size to grow exponentially.  
로그 버킷을 모니터링하는 버킷과 동일하게 설정하지 마세요. 이렇게 하면 무한 로그 루프가 발생하여 버킷 크기가 기하급수적으로 증가합니다.  

This means that while you put an object, if the app bucket and the logging bucket are the same, there will be a logging loop. You will log that again and again, resulting in excessive costs.  
즉, 객체를 업로드할 때 앱 버킷과 로그 버킷이 동일하면 로그 루프가 발생하며, 같은 로그가 반복 기록되어 과도한 비용이 발생합니다.  

---

## Conclusion  
## 결론  

That concludes the overview of S3 access logs.  
이로써 S3 접근 로그 개요 설명을 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- S3 Access Logs record all requests made to your S3 buckets, including authorized and denied requests.  
- S3 접근 로그는 승인된 요청과 거부된 요청을 포함하여 모든 S3 버킷 요청을 기록합니다.  

- Access logs are stored as files in a separate S3 bucket within the same AWS region.  
- 접근 로그는 동일한 AWS 리전 내 별도의 S3 버킷에 파일로 저장됩니다.  

- The logs follow a specific format, which can be referenced via the official AWS documentation.  
- 로그는 특정 형식을 따르며, 공식 AWS 문서를 통해 참조할 수 있습니다.  

- Avoid setting the logging bucket to be the same as the monitored bucket to prevent infinite logging loops and excessive costs.  
- 무한 로그 루프와 과도한 비용을 방지하려면 로그 버킷을 모니터링 버킷과 동일하게 설정하지 마세요.  

🎮 **게임보상:**

* S3 접근 로그 개념 이해 +10 XP
* 로그 버킷 규칙과 주의사항 숙지 +5 XP
* 로그 활용 및 분석 개념 이해 +5 XP
  총 **20 XP 획득!** 🎉
