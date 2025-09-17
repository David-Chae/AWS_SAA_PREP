```markdown
# IAM - Advanced Policies  
# IAM - 고급 정책  

## Introduction to IAM Conditions  
## IAM 조건 소개  

IAM conditions apply to policies within IAM. These policies can be for users, resource policies such as those for S3 buckets, endpoint policies, and more. Essentially, IAM conditions can be applied to any policy within AWS IAM.  
IAM 조건은 IAM 내 정책에 적용됩니다. 이러한 정책은 사용자 정책, S3 버킷과 같은 리소스 정책, 엔드포인트 정책 등 다양한 정책에 적용될 수 있습니다. 기본적으로 IAM 조건은 AWS IAM 내 모든 정책에 적용 가능합니다.  
(IAM 조건의 적용 범위 설명)  

---

## aws:SourceIp Condition  
## aws:SourceIp 조건  

The aws:SourceIp condition is used to restrict the client IP addresses from which API calls are made. For example, a policy can deny all actions ("Deny" on "*") unless the API call originates from specific IP address ranges defined by CIDR blocks. This ensures that only clients within these IP ranges can access AWS resources.  
aws:SourceIp 조건은 API 호출을 수행할 수 있는 클라이언트 IP 주소를 제한하는 데 사용됩니다. 예를 들어, 특정 CIDR 블록으로 정의된 IP 범위에서 API 호출이 발생하지 않으면 모든 작업("*")을 거부("Deny")할 수 있습니다. 이를 통해 지정된 IP 범위 내 클라이언트만 AWS 리소스에 접근할 수 있습니다.  
(IP 기반 접근 제어)  

This condition can be used to restrict AWS usage to a company's internal network, guaranteeing that only the company can access its AWS environment.  
이 조건은 AWS 사용을 회사 내부 네트워크로 제한하여, 회사만이 AWS 환경에 접근하도록 보장할 수 있습니다.  
(내부망 접근 제한 활용)  

---

## aws:RequestedRegion Condition  
## aws:RequestedRegion 조건  

The aws:RequestedRegion condition restricts the AWS regions where API calls can be made. For example, a policy can deny access to services like EC2, RDS, and DynamoDB if the request is made in specific regions such as eu-central-1 or eu-west-1.  
aws:RequestedRegion 조건은 API 호출이 허용되는 AWS 리전을 제한합니다. 예를 들어, eu-central-1 또는 eu-west-1과 같은 특정 리전에서 요청이 발생하면 EC2, RDS, DynamoDB 등의 서비스 접근을 거부할 수 있습니다.  
(리전 기반 접근 제어)  

This condition can be applied globally, for instance in an organization’s Service Control Policy (SCP), to allow or deny access to particular regions.  
이 조건은 조직의 서비스 제어 정책(SCP) 등 글로벌 정책에도 적용 가능하며, 특정 리전에 대한 접근을 허용하거나 거부할 수 있습니다.  
(SCP 적용 예시)  

---

## ec2:ResourceTag and aws:PrincipalTag Conditions  
## ec2:ResourceTag 및 aws:PrincipalTag 조건  

The ec2:ResourceTag condition applies to tags on EC2 instances. For example, a policy can allow starting and stopping instances only if the EC2 instance has a tag Project with the value DataAnalytics.  
ec2:ResourceTag 조건은 EC2 인스턴스의 태그에 적용됩니다. 예를 들어, EC2 인스턴스에 Project 태그가 DataAnalytics 값일 때만 인스턴스를 시작하거나 중지할 수 있도록 정책을 설정할 수 있습니다.  
(리소스 태그 기반 권한 제어)  

The aws:PrincipalTag condition applies to tags on the IAM user making the request. For example, the user must have a tag Department with the value Data to perform certain actions.  
aws:PrincipalTag 조건은 요청을 수행하는 IAM 사용자의 태그에 적용됩니다. 예를 들어, 사용자가 특정 작업을 수행하려면 Department 태그가 Data여야 합니다.  
(사용자 태그 기반 권한 제어)  

These conditions ensure that both the resource and the user meet specific tagging criteria before allowing actions.  
이 조건들은 리소스와 사용자가 특정 태그 기준을 모두 충족해야 작업을 허용하도록 보장합니다.  
(태그 기반 접근 조건)  

---

## aws:MultiFactorAuthPresent Condition  
## aws:MultiFactorAuthPresent 조건  

The aws:MultiFactorAuthPresent condition enforces multi-factor authentication (MFA). For example, a user can perform any action on EC2, but can only stop or terminate instances if MFA is present. This is implemented by denying these actions when MFA is not present ("Bool": {"aws:MultiFactorAuthPresent": "false"}).  
aws:MultiFactorAuthPresent 조건은 다중 인증(MFA)을 강제합니다. 예를 들어, 사용자는 EC2에서 모든 작업을 수행할 수 있지만, 인스턴스를 중지하거나 종료하려면 MFA가 필요합니다. MFA가 없는 경우 이러한 작업을 거부("false")하여 구현됩니다.  
(MFA 기반 권한 강화)  

---

## S3 Bucket Policies  
## S3 버킷 정책  

S3 bucket policies distinguish between bucket-level and object-level permissions:  
S3 버킷 정책은 버킷 수준과 객체 수준 권한을 구분합니다.  
(S3 권한 수준 이해)  

Bucket-level permissions (e.g., ListBucket) apply to the bucket itself and use ARNs like arn:aws:s3:::test.  
버킷 수준 권한(ListBucket 등)은 버킷 자체에 적용되며 arn:aws:s3:::test 같은 ARN을 사용합니다.  
(버킷 권한)  

Object-level permissions (e.g., GetObject, PutObject, DeleteObject) apply to objects within the bucket and use ARNs like arn:aws:s3:::test/* to represent all objects within the bucket.  
객체 수준 권한(GetObject, PutObject, DeleteObject 등)은 버킷 내 객체에 적용되며, arn:aws:s3:::test/*와 같이 모든 객체를 나타내는 ARN을 사용합니다.  
(객체 권한)  

Understanding this distinction is important for correctly configuring S3 permissions.  
이 구분을 이해하는 것은 S3 권한을 올바르게 구성하는 데 중요합니다.  
(S3 권한 설정 중요성)  

---

## aws:PrincipalOrgID Condition  
## aws:PrincipalOrgID 조건  

The aws:PrincipalOrgID condition restricts resource policies to only allow access from accounts that are members of a specific AWS Organization. For example, an S3 bucket policy can allow PutObject and GetObject actions only if the API call originates from an account with the specified PrincipalOrgID.  
aws:PrincipalOrgID 조건은 특정 AWS 조직의 계정만 리소스 접근을 허용하도록 제한합니다. 예를 들어, S3 버킷 정책은 지정된 PrincipalOrgID를 가진 계정에서만 PutObject 및 GetObject 작업을 허용할 수 있습니다.  
(조직 기반 접근 제한)  

This ensures that only accounts within your AWS Organization can access the resource, denying access to any users outside the organization.  
이를 통해 조직 외부 사용자는 접근할 수 없으며, 조직 내부 계정만 리소스에 접근할 수 있습니다.  
(조직 내 계정 접근 보장)  

---

## Conclusion  
## 결론  

IAM conditions provide powerful ways to fine-tune access control in AWS. By using conditions such as aws:SourceIp, aws:RequestedRegion, resource and principal tags, MFA enforcement, and organization membership, you can create advanced security policies tailored to your use cases.  
IAM 조건은 AWS에서 접근 제어를 세밀하게 조정할 수 있는 강력한 방법을 제공합니다. aws:SourceIp, aws:RequestedRegion, 리소스/사용자 태그, MFA 강제, 조직 멤버십 등의 조건을 활용하면, 사용 사례에 맞는 고급 보안 정책을 만들 수 있습니다.  
(IAM 조건 요약)  

---

## Key Takeaways  
## 핵심 요약  

- IAM conditions can be applied to various policies including user, resource, and endpoint policies.  
- IAM 조건은 사용자, 리소스, 엔드포인트 정책 등 다양한 정책에 적용 가능합니다.  

- The aws:SourceIp condition restricts API calls to specified client IP address ranges.  
- aws:SourceIp 조건은 API 호출을 지정된 클라이언트 IP 범위로 제한합니다.  

- The aws:RequestedRegion condition limits access to specific AWS regions.  
- aws:RequestedRegion 조건은 특정 AWS 리전으로 접근을 제한합니다.  

- Resource and principal tags can be used to control permissions based on EC2 instance tags and user tags respectively.  
- 리소스 및 사용자 태그를 활용해 EC2 인스턴스와 사용자 태그 기반 권한을 제어할 수 있습니다.  

- Multi-factor authentication can be enforced using the aws:MultiFactorAuthPresent condition.  
- aws:MultiFactorAuthPresent 조건으로 다중 인증(MFA)을 강제할 수 있습니다.  

- S3 bucket policies distinguish between bucket-level and object-level permissions using different ARNs.  
- S3 버킷 정책은 버킷과 객체 수준 권한을 각각 다른 ARN으로 구분합니다.  

- The aws:PrincipalOrgID condition restricts resource access to accounts within a specific AWS organization.  
- aws:PrincipalOrgID 조건은 특정 AWS 조직 계정 내에서만 리소스 접근을 허용합니다.  
```

게임보상: 🔐 IAM 조건 전문가! 조건 기반 접근 제어 설정 완료! 🏆✅
