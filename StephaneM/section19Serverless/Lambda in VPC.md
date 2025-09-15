# Lambda in VPC

**VPC 내의 Lambda**

---

## Introduction to Lambda Networking Fundamentals

**Lambda 네트워킹 기초 소개**
👉 AWS Lambda 함수는 기본적으로 사용자의 VPC가 아닌 AWS가 관리하는 VPC에서 실행된다. 따라서 기본 설정만으로는 사용자의 VPC 내부 리소스에 접근할 수 없다.

---

By default, when you launch your AWS Lambda functions, they are launched outside of your own Virtual Private Cloud (VPC). Instead, they run within an AWS-owned VPC. Consequently, these Lambda functions do not have access to resources inside your VPC.
기본적으로 AWS Lambda 함수는 사용자의 VPC 외부, 즉 AWS가 소유한 VPC에서 실행된다. 따라서 Lambda 함수는 사용자의 VPC 내부 리소스에 접근할 수 없다.
👉 기본 Lambda는 인터넷 리소스 접근에는 문제가 없지만, VPC 내부 DB 등에는 접근할 수 없다.

---

For example, if you launch an Amazon RDS database, an ElastiCache cache, or an internal load balancer within your VPC, your Lambda function will not be able to access these resources by default.
예를 들어, VPC 내부에 Amazon RDS 데이터베이스, ElastiCache, 내부 로드밸런서를 생성해도 Lambda는 기본적으로 접근할 수 없다.
👉 VPC 리소스 접근에는 네트워크 구성이 필요하다.

---

This default Lambda deployment works well if your function needs to access any public API on the internet or services like DynamoDB, which is a public resource on AWS Cloud.
이 기본 배포는 인터넷의 퍼블릭 API나 DynamoDB 같은 AWS 퍼블릭 리소스에 접근할 때는 잘 작동한다.
👉 퍼블릭 서비스와 통신할 때는 기본 Lambda만으로 충분하다.

---

However, if you have a private RDS database, the connectivity will not work unless you take additional steps. Therefore, you need to launch your Lambda function inside your VPC to enable access to private resources.
하지만 프라이빗 RDS 같은 리소스는 기본 Lambda로 접근이 불가능하므로, Lambda를 VPC 내부에서 실행해야 한다.
👉 프라이빗 리소스 접근 → Lambda를 VPC에 배치 필요.

---

To launch a Lambda function in your VPC, you must specify your VPC ID, the subnets where you want the function to run, and attach a security group to your Lambda function.
VPC 내부에서 Lambda를 실행하려면 VPC ID, 실행할 서브넷, 그리고 Lambda에 보안 그룹을 지정해야 한다.
👉 VPC 배치 시 네트워크 인터페이스가 생성되어 VPC 자원 접근이 가능해진다.

---

This setup creates an elastic network interface in your specified subnets, enabling your Lambda function to access resources such as Amazon RDS running within your VPC.
이 설정은 지정된 서브넷에 ENI(Elastic Network Interface)를 생성해, Lambda가 VPC 내부의 RDS 같은 리소스에 접근할 수 있게 한다.
👉 핵심: ENI 생성이 VPC 접근 열쇠.

---

This approach allows your Lambda function to have private connectivity to anything within your VPC, which is highly beneficial for accessing private resources securely.
이 방식으로 Lambda는 VPC 내부의 프라이빗 리소스에 안전하게 접근할 수 있다.
👉 보안성과 확장성 확보 가능.

---

## Using Lambda with RDS Proxy

**Lambda와 RDS Proxy 사용**

---

A major use case of running Lambda functions inside a VPC is to use them with an RDS proxy.
Lambda를 VPC 내부에서 실행하는 주요 사례 중 하나는 RDS Proxy와 함께 사용하는 것이다.
👉 RDS Proxy는 DB 연결 관리 효율화 도구.

---

Consider an RDS database deployed in a private subnet and Lambda functions that access it directly. This direct access can cause significant problems under high load.
프라이빗 서브넷에 배치된 RDS에 Lambda가 직접 접근하면, 부하가 커질 때 심각한 문제가 발생할 수 있다.
👉 다수의 Lambda 연결이 DB를 압박할 수 있다.

---

If many Lambda functions appear and disappear over time, they may open too many connections to the RDS database. This can overwhelm the database, leading to timeouts and other issues.
Lambda 함수가 대량으로 생성·소멸하면, RDS에 너무 많은 연결을 열어 DB 과부하와 타임아웃을 유발할 수 있다.
👉 "DB 연결 폭발 문제".

---

To solve this, you can launch an RDS proxy. The proxy manages and pools connections, reducing the number of direct connections to your RDS database instance.
이를 해결하기 위해 RDS Proxy를 배치한다. Proxy는 연결을 관리·풀링하여 RDS로의 직접 연결 수를 줄인다.
👉 연결 풀링 → DB 부담 감소.

---

Lambda functions connect to the RDS proxy, which in turn connects to the database instance, effectively solving architectural problems related to connection management.
Lambda는 RDS Proxy에 연결하고, Proxy가 DB에 연결한다. 이렇게 해서 연결 관리 문제를 해결한다.
👉 중간 계층을 둬서 확장성과 안정성 확보.

---

## Benefits of RDS Proxy

**RDS Proxy의 장점**

* **Improved Scalability:** It pulls and shares database connections efficiently.
  **확장성 개선:** DB 연결을 효율적으로 풀링·공유한다.
  👉 대규모 트래픽 대응에 유리.

* **Enhanced Availability:** In case of a failover, it reduces failover time by \~66% and preserves connections. Works with RDS & Aurora.
  **가용성 향상:** 장애 조치 시 시간을 66% 단축하고 연결을 유지한다. RDS와 Aurora에 적용 가능.
  👉 빠른 장애 대응.

* **IAM Authentication Enforcement:** You can enforce IAM auth at the RDS proxy and securely store credentials in AWS Secrets Manager.
  **IAM 인증 적용:** IAM 인증을 RDS Proxy 레벨에서 강제하고, Secrets Manager에 자격 증명을 안전하게 저장 가능.
  👉 보안 강화.

---

For Lambda functions to connect to your RDS proxy, they must be launched inside your VPC. This is because the RDS proxy is never publicly accessible.
Lambda가 RDS Proxy와 연결하려면 반드시 VPC 내부에서 실행돼야 한다. RDS Proxy는 퍼블릭 접근이 불가능하기 때문이다.
👉 VPC 내부 배치 필수.

---

If you launch your Lambda functions publicly, they will have no network connectivity to the RDS proxy.
퍼블릭에 Lambda를 실행하면 RDS Proxy와 네트워크 연결이 되지 않는다.
👉 외부 실행 불가 → VPC 내 실행 필요.

---

## Key Takeaways

**핵심 요약**

* By default, AWS Lambda functions run outside your own VPC, limiting access to private resources.
  기본적으로 Lambda는 VPC 외부에서 실행되므로 프라이빗 리소스 접근이 제한된다.

* To access private resources like RDS databases, Lambda functions must be launched within your VPC with specified subnets and security groups.
  RDS 같은 프라이빗 리소스 접근을 위해 Lambda는 VPC 내부에서 서브넷·보안 그룹을 지정해 실행해야 한다.

* Using an RDS proxy between Lambda functions and RDS databases improves scalability, availability, and allows IAM authentication enforcement.
  Lambda와 RDS 사이에 RDS Proxy를 두면 확장성, 가용성, IAM 인증 적용이 가능하다.

* Lambda functions must reside in the VPC to connect to the RDS proxy, as the proxy is never publicly accessible.
  RDS Proxy는 퍼블릭 접근이 불가능하므로, Lambda는 반드시 VPC 내부에서 실행돼야 한다.

---

🎉 **레벨업 보상:** +120 XP 획득!
👏 당신은 이제 **Lambda Networking Master** 칭호를 얻었습니다.
