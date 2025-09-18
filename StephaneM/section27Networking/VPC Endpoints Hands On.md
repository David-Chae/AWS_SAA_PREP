````markdown
# VPC Endpoints Hands On  
# VPC 엔드포인트 실습  

🎮 게임보상: "Endpoint Master Badge" +500 XP  

---

## Introduction to VPC Endpoints Hands-On  
## VPC 엔드포인트 실습 소개  

In this session, we will practice using VPC endpoints.  
이번 세션에서는 VPC 엔드포인트 사용을 실습해보겠습니다.  

First, I will stop the default VPC instance since it is not needed.  
먼저, 필요하지 않은 기본 VPC 인스턴스를 중지하겠습니다.  

I will terminate that instance and confirm the termination.  
그 인스턴스를 종료하고 종료가 완료되었는지 확인합니다.  

---

Next, we will connect to our bastion host, which is a public EC2 instance.  
다음으로 퍼블릭 EC2 인스턴스인 배스천 호스트에 연결합니다.  

From this bastion host, I will connect to my private EC2 instance using its private IP address.  
이 배스천 호스트를 통해 프라이빗 EC2 인스턴스에 프라이빗 IP로 연결합니다.  

The SSH command used is:  
사용할 SSH 명령어는 다음과 같습니다.  

```bash
ssh ec2-user@<private-ip> -i demoKeyPair.pem
````

---

Now, to access Amazon S3 from the private instance, we need to create and attach an IAM role with appropriate permissions.
이제 프라이빗 인스턴스에서 Amazon S3에 접근하려면 적절한 권한이 있는 IAM 역할을 생성하고 연결해야 합니다.

Currently, no IAM role is attached to the instance.
현재 인스턴스에는 IAM 역할이 연결되어 있지 않습니다.

We will create a new IAM role for EC2 instances with Amazon S3 read-only access policy.
Amazon S3 읽기 전용 권한을 가진 EC2용 새로운 IAM 역할을 생성합니다.

The steps are:
단계는 다음과 같습니다.

1. Create a new role for EC2 service.

2. EC2 서비스용 새로운 역할 생성

3. Attach the AmazonS3ReadOnlyAccess policy.

4. AmazonS3ReadOnlyAccess 정책 연결

5. Name the role DemoRoleEC2-S3ReadOnly.

6. 역할 이름을 DemoRoleEC2-S3ReadOnly로 지정

7. Attach this role to the private EC2 instance.

8. 이 역할을 프라이빗 EC2 인스턴스에 연결

---

After attaching the IAM role, we verify by running the command `aws s3 ls` on the private instance.
IAM 역할을 연결한 후, 프라이빗 인스턴스에서 `aws s3 ls` 명령을 실행해 확인합니다.

This lists the four S3 buckets in the account, confirming that the instance can access S3.
계정의 4개 S3 버킷이 나열되어 인스턴스가 S3에 접근할 수 있음을 확인합니다.

Additionally, the instance currently has internet access, verified by running `curl google.com` successfully.
추가로, `curl google.com` 명령어로 인터넷 접근도 확인할 수 있습니다.

---

## Removing Internet Access from the Private Instance

## 프라이빗 인스턴스에서 인터넷 접근 제거

To demonstrate private connectivity to S3, we will remove internet access from the private instance.
S3에 대한 사설 연결을 시연하기 위해 프라이빗 인스턴스의 인터넷 접근을 제거합니다.

This is done by editing the route table of the private subnet and removing the route through the NAT gateway.
프라이빗 서브넷의 라우트 테이블을 수정하고 NAT 게이트웨이 경로를 삭제하여 수행합니다.

After this change:
이 변경 후:

* Running `aws s3 ls` fails.

* `aws s3 ls` 실행 실패

* Running `curl google.com` also fails.

* `curl google.com` 실행도 실패

This confirms that the instance no longer has internet access.
이로써 인스턴스가 더 이상 인터넷에 접근할 수 없음을 확인했습니다.

---

## Creating a VPC Endpoint

## VPC 엔드포인트 생성

To enable private access to Amazon S3 without internet connectivity, we create a VPC endpoint.
인터넷 없이 Amazon S3에 사설 접근하려면 VPC 엔드포인트를 생성합니다.

Steps:
단계:

1. Navigate to the VPC console and select "Endpoints".

2. VPC 콘솔에서 "Endpoints" 선택

3. Click "Create Endpoint".

4. "Create Endpoint" 클릭

5. Choose the endpoint type as "AWS service".

6. 엔드포인트 유형을 "AWS 서비스"로 선택

7. Select the service name for Amazon S3, which is a gateway type endpoint.

8. Amazon S3 서비스를 선택 (게이트웨이 타입 엔드포인트)

9. Select the VPC where the endpoint will be created.

10. 엔드포인트를 생성할 VPC 선택

11. Associate the endpoint with the private route table so that traffic to S3 is routed through the endpoint.

12. 엔드포인트를 프라이빗 라우트 테이블과 연결하여 S3 트래픽이 엔드포인트를 통해 라우팅되도록 설정

13. Choose full access policy for the endpoint.

14. 엔드포인트의 전체 액세스 정책 선택

15. Create the endpoint.

16. 엔드포인트 생성

---

After creation, the route table for the private subnet is updated automatically with a route directing S3 traffic to the VPC endpoint.
생성 후 프라이빗 서브넷 라우트 테이블이 자동으로 업데이트되어 S3 트래픽이 VPC 엔드포인트로 라우팅됩니다.

This route cannot be deleted manually as it is linked to the endpoint.
이 경로는 엔드포인트와 연결되어 있어 수동으로 삭제할 수 없습니다.

This setup allows instances in the private subnet to access S3 privately without internet access.
이 구성으로 프라이빗 서브넷의 인스턴스가 인터넷 없이 S3에 사설 접근할 수 있습니다.

---

## Testing the VPC Endpoint Connectivity

## VPC 엔드포인트 연결 테스트

We reconnect to the private instance through the bastion host.
배스천 호스트를 통해 프라이빗 인스턴스에 다시 연결합니다.

Running `curl google.com` still fails, confirming no internet access.
`curl google.com` 실행이 여전히 실패하여 인터넷 접근이 없음을 확인

Running `aws s3 ls` also fails initially because the AWS CLI defaults to the US East 1 region.
`aws s3 ls` 실행도 처음에는 실패 (AWS CLI 기본 지역이 US East 1이기 때문)

To fix this, specify the correct region in the CLI command, for example:
이를 해결하려면 CLI 명령에서 올바른 지역을 지정합니다. 예:

```bash
aws s3 ls --region eu-central-1
```

After specifying the correct region, the command succeeds, listing all S3 buckets.
올바른 지역을 지정하면 명령이 성공하고 모든 S3 버킷이 나열됩니다.

This confirms that traffic is routed through the VPC endpoint in the correct region.
이로써 트래픽이 올바른 지역의 VPC 엔드포인트를 통해 라우팅됨을 확인했습니다.

---

## Summary

## 요약

This hands-on demonstrated the power of VPC endpoints, allowing private EC2 instances without internet access to connect securely to AWS services like Amazon S3.
이번 실습에서는 VPC 엔드포인트를 통해 인터넷 없이도 프라이빗 EC2 인스턴스가 Amazon S3와 같은 AWS 서비스에 안전하게 연결되는 방법을 보여주었습니다.

We covered:
다음 항목을 다뤘습니다:

* Terminating unnecessary default instances.

* 불필요한 기본 인스턴스 종료

* Attaching IAM roles with S3 read-only permissions.

* S3 읽기 전용 권한 IAM 역할 연결

* Removing internet access by modifying route tables.

* 라우트 테이블 수정으로 인터넷 접근 제거

* Creating and configuring gateway VPC endpoints for S3.

* S3용 게이트웨이 VPC 엔드포인트 생성 및 구성

* Testing connectivity through the VPC endpoint with the AWS CLI.

* AWS CLI를 통해 VPC 엔드포인트 연결 테스트

Thank you for following along, and I look forward to seeing you in the next lecture.
수업 따라와 주셔서 감사하며, 다음 강의에서 뵙겠습니다.

---

## Key Takeaways

## 핵심 요약

* Demonstrated how to terminate unnecessary default VPC instances to clean up resources.

* 불필요한 기본 VPC 인스턴스를 종료하여 리소스를 정리하는 방법 시연

* Showed how to attach an IAM role with Amazon S3 read-only access to an EC2 instance.

* EC2 인스턴스에 S3 읽기 전용 IAM 역할을 연결하는 방법 시연

* Explained the creation and configuration of VPC endpoints, including interface and gateway types.

* 인터페이스 및 게이트웨이 타입을 포함한 VPC 엔드포인트 생성 및 구성 설명

* Illustrated how to use a gateway VPC endpoint to access Amazon S3 privately without internet access.

* 인터넷 없이 Amazon S3에 사설 접근하는 게이트웨이 VPC 엔드포인트 사용 방법 시연

```
```
