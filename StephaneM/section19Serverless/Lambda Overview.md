# Lambda Overview  
# 람다 개요  

---

## What is AWS Lambda?  
## AWS Lambda란 무엇인가?  

AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers.  
AWS Lambda는 서버를 직접 준비하거나 관리하지 않고 코드를 실행할 수 있는 서버리스 컴퓨팅 서비스입니다.  

Unlike traditional virtual servers such as Amazon EC2, Lambda functions run on demand and scale automatically.  
Amazon EC2 같은 기존 가상 서버와 달리, Lambda 함수는 요청이 있을 때만 실행되며 자동으로 확장됩니다.  

---

## Comparing Lambda with Amazon EC2  
## Lambda와 Amazon EC2 비교  

EC2 provides virtual servers in the cloud that you must provision with a fixed amount of memory and CPU.  
EC2는 클라우드에서 가상 서버를 제공하며, 사용자가 메모리와 CPU 용량을 미리 설정해야 합니다.  

These servers run continuously, regardless of whether they are actively processing tasks or not.  
이 서버들은 작업을 처리 중이든 아니든 항상 실행 상태를 유지합니다.  

Although you can optimize costs by starting and stopping instances, they generally run continuously.  
인스턴스를 시작하고 중지하여 비용을 최적화할 수 있지만, 일반적으로 지속적으로 실행됩니다.  

Scaling requires setting up Auto Scaling groups to add or remove servers automatically.  
확장을 위해서는 Auto Scaling 그룹을 설정하여 서버를 자동으로 추가하거나 제거해야 합니다.  

---

In contrast, AWS Lambda runs your code as functions without any servers to manage.  
반면 AWS Lambda는 서버 관리 없이 코드를 함수 형태로 실행합니다.  

You simply provide your code, and Lambda executes it.  
사용자는 코드만 제공하면 되고, Lambda가 이를 실행합니다.  

These functions are limited to short executions of up to 15 minutes, which is sufficient for many applications.  
이 함수들은 최대 15분 동안만 실행될 수 있으며, 이는 많은 애플리케이션에 충분합니다.  

Lambda functions run only when invoked, so you are billed only for the compute time used during execution.  
Lambda 함수는 호출될 때만 실행되므로, 실행 중 사용된 컴퓨팅 시간에 대해서만 비용이 청구됩니다.  

This represents a significant shift from the continuous running model of EC2.  
이는 EC2의 지속 실행 모델과 비교했을 때 큰 차이를 보여줍니다.  

---

Lambda automatically scales to handle the number of concurrent executions you require.  
Lambda는 동시에 실행되는 요청 수에 맞게 자동으로 확장됩니다.  

If more instances of your function are needed, AWS provisions them automatically, providing seamless scalability.  
더 많은 함수 인스턴스가 필요하다면, AWS가 자동으로 할당하여 매끄러운 확장을 제공합니다.  

---

## Benefits of AWS Lambda  
## AWS Lambda의 장점  

- **Simple Pricing**: You pay based on the number of requests (invocations) and the compute time your functions consume.  
- **단순한 요금 체계**: 요청 수와 함수가 소비한 컴퓨팅 시간에 따라 비용을 지불합니다.  

- **Generous Free Tier**: Includes 1 million free requests and 400,000 gigabyte-seconds of compute time per month.  
- **넉넉한 무료 사용량**: 매월 100만 건의 무료 요청과 400,000 GB-초의 컴퓨팅 시간을 제공합니다.  

- **Wide Language Support**: Supports multiple programming languages including Node.js, Python, Java, C#, PowerShell, Ruby, and more through custom runtimes.  
- **폭넓은 언어 지원**: Node.js, Python, Java, C#, PowerShell, Ruby 등을 포함해 다양한 언어를 지원하며, 커스텀 런타임으로 더 확장 가능합니다.  

- **Easy Monitoring**: Integrated with CloudWatch for monitoring and logging.  
- **간편한 모니터링**: CloudWatch와 통합되어 모니터링과 로그 관리를 지원합니다.  

- **Resource Provisioning**: You can allocate up to 10 GB of RAM per function, which also improves CPU and network performance.  
- **리소스 할당**: 함수당 최대 10GB RAM을 할당할 수 있으며, 이는 CPU 및 네트워크 성능도 향상시킵니다.  

---

## Supported Languages and Runtimes  
## 지원 언어와 런타임  

AWS Lambda supports several programming languages natively, such as Node.js for JavaScript, Python, Java, C# (.NET Core), PowerShell, and Ruby.  
AWS Lambda는 Node.js, Python, Java, C#(.NET Core), PowerShell, Ruby 같은 언어를 기본적으로 지원합니다.  

Additionally, through the custom runtime API, you can run other languages like Rust and Golang.  
또한, 커스텀 런타임 API를 통해 Rust, Golang 같은 언어도 실행할 수 있습니다.  

Lambda also supports container images, but for running Docker containers, services like ECS or Fargate are generally preferred.  
Lambda는 컨테이너 이미지를 지원하지만, Docker 컨테이너 실행에는 보통 ECS나 Fargate 같은 서비스가 더 적합합니다.  

---

## Integration with AWS Services  
## AWS 서비스와의 통합  

Lambda integrates seamlessly with many AWS services, enabling event-driven architectures.  
Lambda는 다양한 AWS 서비스와 매끄럽게 통합되어 이벤트 기반 아키텍처를 구현할 수 있습니다.  

Some key integrations include:  
주요 통합 사례는 다음과 같습니다:  

- **API Gateway**: To create REST APIs that invoke Lambda functions.  
- **API Gateway**: Lambda 함수를 호출하는 REST API를 생성합니다.  

- **Kinesis**: For real-time data processing.  
- **Kinesis**: 실시간 데이터 처리를 지원합니다.  

- **DynamoDB**: To trigger functions on database changes.  
- **DynamoDB**: 데이터베이스 변경 시 함수를 트리거합니다.  

- **S3**: To trigger functions on file uploads.  
- **S3**: 파일 업로드 시 함수를 실행합니다.  

- **CloudFront (Lambda@Edge)**: For content delivery network customization.  
- **CloudFront (Lambda@Edge)**: CDN 사용자 정의에 사용됩니다.  

- **CloudWatch Events / EventBridge**: To react to infrastructure events.  
- **CloudWatch Events / EventBridge**: 인프라 이벤트에 대응합니다.  

- **CloudWatch Logs**: For log streaming.  
- **CloudWatch Logs**: 로그 스트리밍을 지원합니다.  

- **SNS and SQS**: For message processing.  
- **SNS 및 SQS**: 메시지 처리를 담당합니다.  

- **Cognito**: To react to user authentication events.  
- **Cognito**: 사용자 인증 이벤트에 대응합니다.  

---

## Example: Serverless Thumbnail Creation  
## 예시: 서버리스 썸네일 생성  

Consider an S3 bucket where images are uploaded.  
S3 버킷에 이미지가 업로드된다고 가정해봅시다.  

When a new image is added, an S3 event notification triggers a Lambda function.  
새 이미지가 추가되면 S3 이벤트 알림이 Lambda 함수를 트리거합니다.  

This function generates a thumbnail version of the image and uploads it to the same or another S3 bucket.  
이 함수는 이미지의 썸네일 버전을 생성하여 동일하거나 다른 S3 버킷에 업로드합니다.  

Additionally, the function can insert metadata about the image, such as name, size, and creation date, into DynamoDB.  
또한, 함수는 이미지의 이름, 크기, 생성일 같은 메타데이터를 DynamoDB에 기록할 수 있습니다.  

This architecture automates image processing reactively without managing servers.  
이 아키텍처는 서버 관리 없이 이미지 처리를 자동화합니다.  

---

## Example: Serverless CRON Jobs  
## 예시: 서버리스 CRON 작업  

Traditional CRON jobs run on virtual servers like EC2 instances to schedule tasks at specific intervals.  
전통적인 CRON 작업은 EC2 인스턴스 같은 가상 서버에서 특정 주기로 작업을 예약 실행합니다.  

However, this requires the server to be running continuously, even when the CRON job is idle.  
하지만 이는 CRON 작업이 유휴 상태일 때도 서버가 항상 실행 상태여야 합니다.  

With AWS, you can create serverless CRON jobs using CloudWatch Events or EventBridge rules that trigger Lambda functions on a schedule.  
AWS에서는 CloudWatch Events나 EventBridge 규칙을 사용해 일정 주기로 Lambda 함수를 실행하는 서버리스 CRON 작업을 만들 수 있습니다.  

For example, every hour or every Monday at 10:00 AM.  
예: 매시간, 혹은 매주 월요일 오전 10시 실행.  

This eliminates the need for always-on servers and reduces costs.  
이는 상시 실행 서버의 필요성을 없애고 비용을 절감합니다.  

---

## AWS Lambda Pricing Overview  
## AWS Lambda 요금 개요  

Pricing is based on the number of requests and the duration of compute time:  
요금은 요청 수와 실행 시간에 따라 청구됩니다:  

- The first 1 million requests per month are free.  
- 매월 처음 100만 건의 요청은 무료입니다.  

- After that, requests cost $0.20 per additional 1 million requests.  
- 이후에는 100만 건당 $0.20이 부과됩니다.  

- Compute time is billed in increments of 1 millisecond.  
- 실행 시간은 1밀리초 단위로 청구됩니다.  

- The first 400,000 gigabyte-seconds of compute time per month are free.  
- 매월 처음 400,000 GB-초의 실행 시간은 무료입니다.  

Gigabyte-seconds represent the amount of memory allocated multiplied by the execution time.  
GB-초는 할당된 메모리 크기와 실행 시간을 곱한 값입니다.  

For example, 400,000 seconds of execution with 1 GB of RAM is free.  
예: 1GB RAM으로 400,000초 실행 시 무료입니다.  

If your function uses 128 MB of RAM, you get proportionally more execution time for free.  
만약 함수가 128MB RAM을 사용한다면, 그만큼 더 많은 실행 시간을 무료로 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Lambda provides serverless functions that run on demand without managing servers.  
- AWS Lambda는 서버 관리 없이 요청 시 실행되는 서버리스 함수를 제공합니다.  

- Lambda functions have a maximum execution time of 15 minutes and scale automatically.  
- Lambda 함수는 최대 15분 동안 실행 가능하며 자동으로 확장됩니다.  

- Pricing is based on the number of requests and compute time, with a generous free tier.  
- 요금은 요청 수와 실행 시간 기반이며, 넉넉한 무료 사용량이 포함됩니다.  

- Lambda integrates with many AWS services such as API Gateway, S3, DynamoDB, CloudWatch, and more.  
- Lambda는 API Gateway, S3, DynamoDB, CloudWatch 등 다양한 AWS 서비스와 통합됩니다.  
`
