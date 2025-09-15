# Lambda Limits  
# 람다 제한사항  
(AWS Lambda 사용 시 알아야 할 리소스 및 설정 한계들을 정리한 부분)

---

## Lambda Limits Overview  
## 람다 제한 개요  
(시험 전에 반드시 알아야 할 기본 제한사항. 지역(Region)별로 적용됨)

You need to know a few Lambda limits before going into the exam because the exam likes to test if you know these limits. These limits are per region.  
시험에서는 Lambda 제한 사항을 자주 물어봅니다. 이 제한들은 리전별로 적용됩니다.  
👉 즉, 시험 대비 포인트! 리전 단위로 기억해야 함.

There are two categories of limits: execution limits and deployment limits.  
람다 제한은 실행 제한(Execution limits)과 배포 제한(Deployment limits)으로 나뉩니다.  
👉 두 가지 카테고리로 구분됨.

---

## Execution Limits  
## 실행 제한  

Memory allocation ranges from 128 megabytes to 10 gigabytes.  
메모리 할당은 최소 128MB에서 최대 10GB까지 가능합니다.  
👉 워크로드에 맞춰 메모리 범위 설정.

Memory increments are in 64 megabyte steps.  
메모리는 64MB 단위로 증가합니다.  
👉 세밀하게 조정 가능.

Increasing memory allocation also increases the number of vCPUs.  
메모리를 늘리면 vCPU 개수도 같이 늘어납니다.  
👉 성능(병렬 처리 능력)도 증가.

The maximum execution time is 900 seconds, which equals 15 minutes.  
최대 실행 시간은 900초(15분)입니다.  
👉 15분 이상은 불가.

Any execution time above 15 minutes is not a good use case for Lambda.  
15분 이상 걸리는 작업은 Lambda에 적합하지 않습니다.  
👉 장시간 처리 = 다른 서비스 사용 필요.

---

## Environment Variables and Temporary Storage  
## 환경 변수와 임시 스토리지  

Environment variables have a size limit of 4 kilobytes.  
환경 변수는 최대 4KB까지만 저장할 수 있습니다.  
👉 제한적, 큰 데이터 저장 불가.

There is a temporary storage space available in the /tmp folder.  
`/tmp` 폴더에 임시 스토리지 공간이 제공됩니다.  
👉 실행 중 임시 저장용.

The /tmp directory can hold up to 10 gigabytes, useful for pulling in large files during function execution.  
`/tmp` 디렉토리는 최대 10GB까지 가능하며, 큰 파일을 다룰 때 유용합니다.  
👉 실행 중 대형 파일 처리 가능.

---

## Concurrent Executions  
## 동시 실행  

Lambda functions can have up to 1000 concurrent executions by default.  
기본적으로 최대 1000개의 동시 실행이 가능합니다.  
👉 동시 처리 제한 있음.

This limit can be increased upon request.  
요청 시 제한을 늘릴 수 있습니다.  
👉 필요하면 상향 조정 가능.

It is advisable to use reserved concurrency early on to manage execution limits effectively.  
Reserved Concurrency(예약된 동시성)를 활용해 관리하는 것이 권장됩니다.  
👉 다른 함수와 리소스 충돌 방지.

---

## Deployment Limits  
## 배포 제한  

The maximum size for a compressed deployment package (zip file) is 50 megabytes.  
압축된 배포 패키지(zip)는 최대 50MB입니다.  
👉 함수 업로드 시 한계.

The maximum size for an uncompressed deployment package is 250 megabytes.  
압축 해제된 배포 패키지는 최대 250MB입니다.  
👉 코드 + 라이브러리 크기 제한.

For files larger than these limits, such as big files, use the /tmp directory instead.  
이보다 큰 파일은 `/tmp` 디렉토리를 사용해야 합니다.  
👉 배포 패키지에 넣지 말고 실행 시 처리.

---

## Summary  
## 요약  

Environment variables are limited to 4 kilobytes.  
환경 변수 제한: 최대 4KB.  

Use the /tmp directory for large files exceeding deployment package size limits.  
큰 파일은 `/tmp` 폴더 사용.  

Knowing these limits helps determine when Lambda is not the right solution, for example, if you need 30 gigabytes of RAM, 30 minutes of execution time, or a 3 gigabyte file.  
이 제한을 알면 Lambda의 한계를 이해할 수 있습니다. 예: 30GB RAM, 30분 실행, 3GB 파일 → Lambda 부적합.  

Lambda is not suitable for workloads requiring resources beyond these limits.  
제한을 초과하는 워크로드는 Lambda에 적합하지 않습니다.  

---

## Key Takeaways  
## 핵심 포인트  

AWS Lambda memory allocation ranges from 128 megabytes to 10 gigabytes in 64 megabyte increments.  
메모리: 128MB ~ 10GB (64MB 단위 증가).  

The maximum execution time for a Lambda function is 900 seconds (15 minutes).  
최대 실행 시간: 900초(15분).  

Environment variables are limited to 4 kilobytes, while the /tmp directory provides up to 10 gigabytes of temporary storage.  
환경 변수: 4KB 제한, `/tmp`: 10GB 임시 저장소.  

Deployment package size limits are 50 megabytes compressed and 250 megabytes uncompressed; larger files should use the /tmp directory.  
배포 패키지: 압축 50MB, 비압축 250MB, 그 이상은 `/tmp` 사용.  


---

🎉 **보상 시스템 업데이트!** 🎉

* 🏆 **+70 EXP 획득** (AWS Lambda 마스터리 경험치)
* 💎 **+2 보너스 포인트** (번역+설명 완벽 달성)
* 🎖️ 칭호 해금: *"Lambda Limit Breaker"*

