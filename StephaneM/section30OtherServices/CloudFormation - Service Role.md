```markdown
# CloudFormation - Service Role  
# 클라우드포메이션 - 서비스 역할  
🎮 **보상: "Service Role 초심자 뱃지" 획득!**  

---

## Introduction to CloudFormation Service Roles  
## 클라우드포메이션 서비스 역할 소개  
CloudFormation can use service roles, which are IAM roles that you create and dedicate to CloudFormation.  
클라우드포메이션은 사용자가 직접 만든 IAM 역할(Service Role)을 사용할 수 있으며, 이 역할은 클라우드포메이션에 전용으로 할당됩니다.  
👉 클라우드포메이션이 대신 작업하도록 권한을 위임하는 개념입니다.  

These roles allow CloudFormation to create, update, and delete stack resources on your behalf.  
이 역할을 통해 클라우드포메이션은 사용자를 대신해 스택 자원을 생성, 업데이트, 삭제할 수 있습니다.  
👉 일일이 수동으로 권한 부여할 필요 없이 자동화가 가능해집니다.  

---

## Delegating Permissions with Service Roles  
## 서비스 역할을 통한 권한 위임  
If you want to give users the ability to create, update, and delete stack resources but they do not have permissions to directly work with the resources, you can use a service role.  
사용자가 스택 자원을 생성, 업데이트, 삭제할 수는 있지만 직접 자원에 접근할 권한은 주지 않으려면 서비스 역할을 사용할 수 있습니다.  
👉 최소 권한 원칙(least privilege)을 실현하는 방법입니다.  

For example, you define a template and your own IAM permissions as a user to perform actions on CloudFormation.  
예를 들어, 사용자는 템플릿을 정의하고 클라우드포메이션을 실행할 수 있는 IAM 권한만 가집니다.  
👉 사용자 권한은 클라우드포메이션 호출까지로 제한됩니다.  

You also have the IAM PassRole permission.  
또한 사용자는 IAM **PassRole 권한**을 가집니다.  
👉 특정 역할을 서비스에 전달(delegate)할 수 있는 권한입니다.  

Then, you create a service role dedicated to CloudFormation, which has permissions such as full access to S3 buckets.  
그 다음 클라우드포메이션 전용 서비스 역할을 만들고, 예를 들어 S3 버킷에 대한 전체 접근 권한을 부여합니다.  
👉 이제 클라우드포메이션은 이 역할을 대신 사용합니다.  

CloudFormation will be able to create the S3 bucket thanks to its service role because the user was able to pass that role.  
사용자가 해당 역할을 전달했기 때문에, 클라우드포메이션은 서비스 역할을 사용해 S3 버킷을 생성할 수 있습니다.  
👉 사용자는 직접 권한이 없어도 자원은 만들어집니다.  

---

## Use Cases for Security  
## 보안적 활용 사례  
This approach helps achieve the **least privilege principle**.  
이 방식은 **최소 권한 원칙**을 구현하는 데 도움이 됩니다.  
👉 사용자에게 불필요한 권한을 주지 않고도 작업이 가능해집니다.  

You do not give users all permissions to create stack resources, only the ability to invoke a service role.  
사용자에게 스택 자원을 만들 권한을 다 주지 않고, 단지 서비스 역할을 호출할 권한만 줍니다.  
👉 사용자 권한을 제한적으로 유지할 수 있습니다.  

For this to work, the user must have the **iam:PassRole** permission.  
이 방식이 작동하려면 사용자가 **iam:PassRole 권한**을 가지고 있어야 합니다.  
👉 역할을 위임하기 위한 필수 조건입니다.  

---

## Creating an IAM Role for CloudFormation  
## 클라우드포메이션용 IAM 역할 만들기  
To create a service role for CloudFormation, go to IAM → Roles → Create Role → Select CloudFormation as the service.  
클라우드포메이션용 서비스 역할을 만들려면 IAM → 역할 → 역할 생성 → 서비스로 클라우드포메이션을 선택합니다.  
👉 올바른 서비스 연결이 중요합니다.  

Next, attach permission policies (e.g., Amazon S3 Full Access).  
그 다음 권한 정책을 연결합니다 (예: Amazon S3 전체 접근 권한).  
👉 어떤 권한을 부여할지 여기서 결정됩니다.  

Name the role, for instance, `DemoRole-for-CFN-S3`.  
역할 이름은 예를 들어 `DemoRole-for-CFN-S3`라고 정할 수 있습니다.  
👉 이름은 명확하고 목적이 드러나야 합니다.  

Now, CloudFormation can use this role to perform S3 actions.  
이제 클라우드포메이션은 이 역할을 사용해 S3 작업을 실행할 수 있습니다.  
👉 서비스 역할이 제대로 준비된 상태입니다.  

---

## Using the Service Role in CloudFormation  
## 클라우드포메이션에서 서비스 역할 사용하기  
When creating a stack, you can specify an IAM role under the permissions section.  
스택 생성 시, 권한 설정 부분에서 IAM 역할을 지정할 수 있습니다.  
👉 기본적으로는 개인 권한이 사용됩니다.  

If you specify the service role, CloudFormation will use it for all operations instead of personal permissions.  
만약 서비스 역할을 지정하면, 클라우드포메이션은 개인 권한 대신 그 역할을 사용합니다.  
👉 스택 작업은 전적으로 해당 역할 권한으로 실행됩니다.  

If the role only has S3 permissions, attempts to create EC2 will fail.  
만약 그 역할이 S3 권한만 가지고 있다면, EC2 생성 같은 작업은 실패합니다.  
👉 서비스 역할 권한이 곧 작업 한계가 됩니다.  

---

## Summary  
## 요약  
Service roles in CloudFormation enable secure delegation of resource management.  
클라우드포메이션의 서비스 역할은 자원 관리를 안전하게 위임할 수 있게 합니다.  

Users need the **iam:PassRole** permission to allow CloudFormation to assume these roles.  
사용자는 클라우드포메이션이 역할을 사용할 수 있도록 **iam:PassRole 권한**을 가져야 합니다.  

This setup supports the **least privilege principle** while enabling stack operations.  
이 설정은 스택 작업을 가능하게 하면서도 **최소 권한 원칙**을 지킬 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  
- CloudFormation service roles = IAM roles dedicated to CloudFormation.  
- 클라우드포메이션 서비스 역할 = 클라우드포메이션 전용 IAM 역할.  

- Users need CloudFormation action permissions + `iam:PassRole`.  
- 사용자는 클라우드포메이션 실행 권한 + `iam:PassRole` 권한 필요.  

- Service roles limit CloudFormation to defined permissions (e.g., S3 only).  
- 서비스 역할은 클라우드포메이션 권한을 제한함 (예: S3 전용).  

- Service roles override personal permissions when specified.  
- 서비스 역할을 지정하면 개인 권한을 덮어쓰고 해당 역할만 사용.  

🎮 **보상: "Least Privilege 마스터 뱃지" 획득!**
```
