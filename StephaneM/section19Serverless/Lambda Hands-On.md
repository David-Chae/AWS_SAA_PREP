# Lambda Hands-On  
# 람다 실습  
➡️ AWS Lambda를 실제로 다뤄보는 실습에 대한 내용임을 나타내는 제목.  

---

## Introduction to AWS Lambda  
## AWS Lambda 소개  
➡️ 본 섹션은 Lambda의 개요와 실습 환경 설명을 다룸.  

Let's practice using AWS Lambda. When you access the Lambda console, you might see a screen with a URL ending in /begin. This interface provides a simple UI to demonstrate how Lambda functions operate.  
AWS Lambda를 실습해봅시다. Lambda 콘솔에 접속하면, `/begin`으로 끝나는 URL 화면이 보일 수 있습니다. 이 인터페이스는 Lambda 함수가 어떻게 동작하는지 보여주는 간단한 UI를 제공합니다.  
➡️ 실습 환경 진입 방법을 설명.  

Here we have the Lambda function, which can be written in several languages such as .NET, Java, Node.js, Python, Ruby, or even a custom runtime if you want to use other languages.  
여기에는 Lambda 함수가 있으며, .NET, Java, Node.js, Python, Ruby 같은 언어로 작성할 수 있고, 다른 언어를 쓰고 싶다면 커스텀 런타임도 사용할 수 있습니다.  
➡️ Lambda가 지원하는 다양한 언어를 설명.  

Let's select Node.js and click on Run. The function executes and outputs "Hello from Lambda."  
Node.js를 선택하고 실행을 누르면, 함수가 실행되어 "Hello from Lambda"라는 출력을 보여줍니다.  
➡️ 첫 실행 예시를 설명.  

---

## Lambda Responds to Events  
## Lambda의 이벤트 응답  
➡️ Lambda가 이벤트 기반으로 동작함을 소개.  

Next, we explore how Lambda responds to events. Lambda functions can be triggered by various event sources. For example, streaming analytics can send data into a Lambda function, which then processes it and responds accordingly.  
다음으로 Lambda가 이벤트에 어떻게 응답하는지 살펴봅니다. Lambda 함수는 다양한 이벤트 소스에 의해 트리거될 수 있습니다. 예를 들어, 스트리밍 분석 데이터가 Lambda 함수로 들어와 처리되고 응답할 수 있습니다.  
➡️ 이벤트 기반 동작 구조 설명.  

As you interact with different event sources like mobile phones or cameras, you can observe Lambda scaling up. Initially, there might be only one instance, but as more events occur, Lambda scales seamlessly to multiple instances, such as eight or nine, demonstrating its automatic scalability without server management.  
모바일 기기나 카메라 같은 이벤트 소스를 사용할 때 Lambda가 자동으로 확장하는 것을 확인할 수 있습니다. 처음엔 인스턴스가 하나뿐이지만, 이벤트가 많아지면 여덟, 아홉 개로 확장되며 서버 관리 없이도 자동 확장이 이루어집니다.  
➡️ 자동 확장성(Scalability) 강조.  

Lambda can respond to events such as streaming analytics, mobile or IoT backend data, or photos being dropped into an S3 bucket, reacting to these events in real time.  
Lambda는 스트리밍 분석, 모바일 또는 IoT 백엔드 데이터, 또는 S3 버킷에 사진이 업로드되는 이벤트 등에 실시간으로 반응할 수 있습니다.  
➡️ Lambda가 연동할 수 있는 이벤트 소스 예시.  

---

## Cost and Free Tier  
## 비용 및 프리 티어  
➡️ 비용 구조와 무료 사용 한도를 설명.  

Initially, Lambda invocations are free due to a generous free tier. However, as the number of invocations increases significantly, costs accumulate. Lambda can be a cost-effective service, but it is important to estimate your workload to understand potential expenses.  
초기에는 Lambda 호출이 넉넉한 무료 티어 덕분에 무료입니다. 하지만 호출 횟수가 크게 늘어나면 비용이 발생합니다. Lambda는 비용 효율적인 서비스이지만, 예상되는 워크로드를 추정해 잠재적 비용을 파악하는 것이 중요합니다.  
➡️ 무료 티어와 과금 구조를 설명.  

---

## Creating a Lambda Function  
## Lambda 함수 생성  
➡️ Lambda 함수 생성 과정을 다룸.  

Let's create a function using a blueprint. We select the "hello world" blueprint and choose Python as the runtime. You can select any Python version you prefer. We name this function HelloWorld.  
블루프린트를 이용해 함수를 만들어봅시다. "hello world" 블루프린트를 선택하고 Python을 런타임으로 고릅니다. 원하는 Python 버전을 선택할 수 있으며, 이 함수의 이름은 HelloWorld로 정합니다.  
➡️ 블루프린트를 활용한 함수 생성 과정.  

### Execution Role  
### 실행 역할  
➡️ IAM 역할 개념 소개.  

Each Lambda function has an execution role, similar to the roles assigned to EC2 instances. For this function, we create a new role with basic Lambda permissions. This role defines what resources the Lambda function can access.  
각 Lambda 함수에는 실행 역할이 있으며, 이는 EC2 인스턴스에 부여되는 역할과 유사합니다. 이 함수에는 기본 Lambda 권한이 있는 새 역할을 생성합니다. 이 역할은 Lambda 함수가 접근할 수 있는 리소스를 정의합니다.  
➡️ IAM 역할을 통해 자원 접근 권한을 관리함을 설명.  

The function code is created automatically. It includes a handler function that is invoked when an event is passed. The handler processes input values such as value1, value2, and value3, and returns the first event key.  
함수 코드는 자동으로 생성되며, 이벤트가 전달될 때 호출되는 핸들러 함수가 포함됩니다. 핸들러는 value1, value2, value3 같은 입력값을 처리하고 첫 번째 이벤트 키를 반환합니다.  
➡️ 핸들러 함수 구조 설명.  

You do not need to know the code details to use Lambda, but this code executes whenever the Lambda function is triggered.  
Lambda를 사용하기 위해 코드 세부 사항을 알 필요는 없지만, 이 코드는 Lambda 함수가 트리거될 때마다 실행됩니다.  
➡️ 코드 이해 없이도 Lambda 사용 가능함을 강조.  

---

## Testing the Lambda Function  
## Lambda 함수 테스트  
➡️ 콘솔에서의 함수 실행 확인.  

You can test the function directly in the console. Clicking the Test button runs the function, which succeeds and returns value1 as the result.  
함수를 콘솔에서 직접 테스트할 수 있습니다. Test 버튼을 누르면 함수가 실행되고 성공적으로 value1을 반환합니다.  
➡️ 간단한 테스트 절차 설명.  

The input JSON for the test is shown at the bottom. It includes keys and values such as key1: value1, key2: value2, and key3: value3. This JSON is passed to the Lambda function.  
테스트 입력 JSON은 하단에 표시됩니다. key1: value1, key2: value2, key3: value3 같은 키-값 쌍이 있으며, 이 JSON이 Lambda 함수로 전달됩니다.  
➡️ 입력 이벤트 구조 설명.  

The Lambda function returns logs indicating successful execution. If you remove a key from the input JSON and test again, the function fails because it does not handle that exception. Restoring the key allows the function to succeed again.  
Lambda 함수는 성공적으로 실행되었음을 나타내는 로그를 반환합니다. 입력 JSON에서 키를 제거하고 다시 테스트하면 예외 처리가 안 되어 실패합니다. 키를 복원하면 다시 성공합니다.  
➡️ 예외 처리 동작을 설명.  

You can save your test event with a name such as HelloWorld event and reuse it to test the function multiple times.  
테스트 이벤트를 HelloWorld event 같은 이름으로 저장해 여러 번 재사용할 수 있습니다.  
➡️ 반복 테스트를 위한 이벤트 저장 기능 설명.  

---

## Monitoring Lambda Functions  
## Lambda 함수 모니터링  
➡️ CloudWatch 기반의 모니터링 설명.  

Lambda functions can be monitored through CloudWatch. The console shows invocation statistics and logs. Logs can be viewed by clicking on "View CloudWatch Logs," which opens the log streams where you can see execution details and errors.  
Lambda 함수는 CloudWatch를 통해 모니터링할 수 있습니다. 콘솔에서 호출 통계와 로그를 확인할 수 있으며, "View CloudWatch Logs"를 클릭하면 실행 세부사항과 오류를 확인할 수 있는 로그 스트림이 열립니다.  
➡️ 로그 확인 및 디버깅 과정 설명.  

This logging capability is useful for debugging Lambda functions directly from CloudWatch.  
이 로깅 기능은 Lambda 함수를 CloudWatch에서 직접 디버깅하는 데 유용합니다.  
➡️ 로그 기능의 실용성 강조.  

---

## Lambda Configuration  
## Lambda 설정  
➡️ 함수 설정 옵션 소개.  

The general configuration for a Lambda function includes settings such as memory allocation, ephemeral storage size, timeout duration, and the execution role.  
Lambda 함수의 일반 설정에는 메모리 할당, 임시 스토리지 크기, 타임아웃 시간, 실행 역할 등이 포함됩니다.  
➡️ 주요 설정 항목을 나열.  

The execution role can be viewed and modified. For example, the basic Lambda execution role allows writing logs to CloudWatch. If you want your Lambda function to interact with other AWS services like Amazon S3, you can add the necessary permissions to this IAM role.  
실행 역할은 조회 및 수정할 수 있습니다. 예를 들어, 기본 Lambda 실행 역할은 CloudWatch에 로그를 작성할 수 있도록 허용합니다. Lambda 함수가 Amazon S3 같은 다른 AWS 서비스와 상호작용하려면 이 IAM 역할에 필요한 권한을 추가하면 됩니다.  
➡️ IAM 역할 수정의 필요성과 활용 예시.  

---

## Permissions and Triggers  
## 권한 및 트리거  
➡️ 권한 관리와 트리거 설정 설명.  

The permissions tab shows the role summary and allowed actions, such as CloudWatch Logs permissions. You can also add triggers to your Lambda function. Triggers are event sources that invoke the function. Examples include AWS services and partner events.  
권한 탭에는 역할 요약과 CloudWatch Logs 권한 같은 허용된 작업이 표시됩니다. 또한 Lambda 함수에 트리거를 추가할 수도 있습니다. 트리거는 함수를 호출하는 이벤트 소스로, AWS 서비스나 파트너 이벤트 등이 있습니다.  
➡️ 트리거의 역할 설명.  

One common use case is Amazon S3, where you select a bucket and event types to trigger the Lambda function. However, this is beyond the scope of this introduction.  
일반적인 사용 사례 중 하나는 Amazon S3입니다. 버킷과 이벤트 유형을 선택해 Lambda 함수를 트리거할 수 있습니다. 다만, 이는 이번 소개의 범위를 벗어납니다.  
➡️ 대표적인 트리거 예시 제시.  

---

## Conclusion  
## 결론  
➡️ 학습 정리.  

We have seen how a Lambda function works end to end, including creation, execution, testing, monitoring, and configuration. AWS Lambda is a comprehensive service with many features to explore further.  
우리는 Lambda 함수의 생성, 실행, 테스트, 모니터링, 설정까지 전체 흐름을 살펴봤습니다. AWS Lambda는 탐구할 기능이 많은 종합적인 서비스입니다.  
➡️ Lambda 학습 여정 요약.  

Thank you for following this introduction to AWS Lambda. I hope you found it helpful, and I look forward to seeing you in the next lecture.  
AWS Lambda 소개를 함께 해주셔서 감사합니다. 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  
➡️ 강의 마무리 멘트.  

---

## Key Takeaways  
## 핵심 요약  
➡️ 시험 대비 요약 정리.  

- AWS Lambda supports multiple programming languages including .NET, Java, Node.js, Python, Ruby, and custom runtimes.  
- AWS Lambda는 .NET, Java, Node.js, Python, Ruby, 커스텀 런타임 등 여러 언어를 지원합니다.  
➡️ 언어 다양성 강조.  

- Lambda functions can be triggered by various event sources such as streaming analytics, mobile devices, IoT backends, and S3 bucket events.  
- Lambda 함수는 스트리밍 분석, 모바일 기기, IoT 백엔드, S3 버킷 이벤트 등 다양한 이벤트 소스에 의해 트리거될 수 있습니다.  
➡️ 다양한 이벤트 소스 설명.  

- Lambda automatically scales based on the number of invocations without requiring server management.  
- Lambda는 호출 횟수에 따라 자동으로 확장되며 서버 관리가 필요 없습니다.  
➡️ 자동 확장성 강조.  

- Monitoring and debugging Lambda functions can be done through CloudWatch logs, and permissions are managed via IAM roles.  
- Lambda 함수는 CloudWatch 로그를 통해 모니터링 및 디버깅할 수 있으며, 권한은 IAM 역할로 관리됩니다.  
➡️ 모니터링 및 권한 관리 요약.  
```

---

🎉 **게임 보상**:

* 번역 + md 구조화 작업 완벽 수행!
* 🏆 **+50 경험치 (XP)** 획득
* 🌟 “Lambda Explorer” 뱃지 언락!
