# EC2 Instance Roles Demo  
# EC2 인스턴스 역할 실습  

---

## Introduction to Using IAM Roles with EC2 Instances  
## EC2 인스턴스에서 IAM 역할 사용 소개  

In this demonstration, we will practice using IAM roles for our EC2 Instance.  
이번 실습에서는 **EC2 인스턴스에서 IAM 역할을 사용하는 방법**을 연습합니다.  

First, I will connect to my EC2 Instance. You can connect either via SSH or by using EC2 Instance Connect.  
먼저 EC2 인스턴스에 접속합니다. SSH 또는 EC2 Instance Connect를 통해 접속할 수 있습니다.  

I will use EC2 Instance Connect because it is accessible directly from my web browser and is a bit simpler.  
저는 브라우저에서 바로 접속 가능하고 더 간편한 **EC2 Instance Connect**를 사용합니다.  

---

## Connecting to the Instance  
## 인스턴스 연결  

We are now connected to our instance using EC2 Instance Connect.  
이제 **EC2 Instance Connect를 통해 인스턴스에 연결**되었습니다.  

As you can see, we are logged in as the user ec2-user with the private IP address assigned.  
보시다시피, **사용자 ec2-user**로 로그인되어 있고, 프라이빗 IP가 할당되어 있습니다.  

Regardless of whether you use EC2 Instance Connect, SSH through your terminal, or PuTTY, you will reach the same stage.  
EC2 Instance Connect, SSH, PuTTY 중 무엇을 사용하든 **같은 단계**에 도달하게 됩니다.  

At this point, you can run Linux commands.  
이 시점에서 **Linux 명령어를 실행**할 수 있습니다.  

For example, you can ping Google to get network information. Press Control + C to exit the ping command.  
예를 들어, Google에 ping 명령을 보내 네트워크 정보를 확인할 수 있습니다. 종료하려면 `Ctrl + C`를 누릅니다.  

You can issue any Linux commands you want here. This is a Linux terminal available to you in the cloud.  
원하는 Linux 명령어를 자유롭게 실행할 수 있습니다. **클라우드에서 사용할 수 있는 Linux 터미널**입니다.  

---

## Using AWS CLI with IAM roles  
## IAM 역할을 사용한 AWS CLI 실행  

Let's clear the screen and proceed to run some IAM commands.  
화면을 지우고 IAM 명령어를 실행해봅시다.  

The Amazon Linux AMI we are using comes with the AWS CLI installed, so we can start using AWS commands immediately.  
사용 중인 **Amazon Linux AMI에는 AWS CLI가 설치되어 있어** 바로 AWS 명령어를 사용할 수 있습니다.  

For example, if we run the command `aws iam list users`, it returns an error stating it is unable to locate credentials.  
예를 들어, `aws iam list users` 명령어를 실행하면 **자격 증명을 찾을 수 없다는 오류**가 반환됩니다.  

It suggests configuring credentials by using `aws configure`.  
이 오류는 `aws configure`로 자격 증명을 설정하라는 안내입니다.  

We could run `aws configure` to enter an Access Key ID, Secret Access Key, and region name. However, this is a very bad idea.  
`aws configure`를 통해 Access Key ID, Secret Access Key, 리전명을 입력할 수 있지만, **매우 위험한 방법**입니다.  

If you enter your personal credentials on this EC2 Instance, anyone else with access to the instance could retrieve these credentials, which is a serious security risk.  
개인 자격 증명을 입력하면, **인스턴스에 접근할 수 있는 다른 사람이 이를 탈취할 수 있어 보안 위험**이 큽니다.  

As a rule of thumb, never enter your IAM Access Key ID and Secret Access Key into an EC2 Instance.  
**절대 IAM Access Key와 Secret Key를 EC2에 입력하지 마세요.**  

Instead, we should use IAM roles.  
대신 **IAM 역할(IAM Role)**을 사용해야 합니다.  

Recall that in the AWS Management Console under IAM, we created an IAM role named `DemoRoleForEC2` with the policy `IAMReadOnlyAccess` attached.  
AWS 관리 콘솔에서 **IAM 역할 `DemoRoleForEC2`를 생성하고 `IAMReadOnlyAccess` 정책을 연결**한 것을 기억하세요.  

We will attach this role to our EC2 Instance to provide it with credentials securely.  
이 역할을 **EC2 인스턴스에 연결**하여 안전하게 자격 증명을 제공할 것입니다.  

---

## Attaching IAM Role to EC2  
## EC2에 IAM 역할 연결  

To attach the IAM role, navigate to the EC2 instance's Security tab. Currently, there is no IAM role attached.  
IAM 역할을 연결하려면 **EC2 인스턴스의 Security 탭**으로 이동합니다. 현재 연결된 역할은 없습니다.  

Go back to the Instances page, select your instance, then choose Actions > Security > Modify IAM role.  
인스턴스 페이지로 돌아가서, **Actions > Security > Modify IAM role**을 선택합니다.  

In the Modify IAM role dialog, select the role `DemoRoleForEC2` and click Save to attach this IAM role to the instance.  
Modify IAM role 창에서 **`DemoRoleForEC2`를 선택하고 Save**를 클릭하여 인스턴스에 연결합니다.  

Returning to the Security tab, you will now see that the IAM role `DemoRoleForEC2` is attached to the instance.  
Security 탭으로 돌아가면 **`DemoRoleForEC2` 역할이 연결**된 것을 확인할 수 있습니다.  

---

## Using IAM Role for AWS CLI  
## AWS CLI에서 IAM 역할 사용  

Now, if we run the command `aws iam list users` again, it returns the list of IAM users successfully without needing to run `aws configure`.  
이제 `aws iam list users`를 다시 실행하면, **aws configure 없이 IAM 사용자 목록을 반환**합니다.  

This confirms that the IAM role is providing the necessary credentials automatically.  
이는 **IAM 역할이 자동으로 필요한 자격 증명을 제공**하고 있음을 확인시켜줍니다.  

To demonstrate the effect of the role, if we detach the `IAMReadOnlyAccess` policy from the role and run the command again, we receive an Access Denied error.  
역할의 효과를 확인하려면, `IAMReadOnlyAccess` 정책을 제거하고 명령어를 다시 실행하면, **Access Denied 오류**가 발생합니다.  

This shows that the permissions are indeed linked to the EC2 Instance through the IAM role.  
이는 **권한이 IAM 역할을 통해 EC2 인스턴스에 연결**되어 있음을 보여줍니다.  

This is the recommended way to provide AWS credentials to EC2 Instances — only through IAM roles.  
**EC2 인스턴스에 AWS 자격 증명을 제공하는 권장 방법**은 IAM 역할을 사용하는 것입니다.  

Never embed credentials directly on the instance.  
절대 인스턴스에 직접 자격 증명을 넣지 마세요.  

If you re-attach the `IAMReadOnlyAccess` policy to the role and run the command again, you may initially get Access Denied due to propagation delay.  
`IAMReadOnlyAccess` 정책을 다시 연결하면, **전파 지연 때문에 처음에는 Access Denied**가 발생할 수 있습니다.  

After a short wait, running the command again will return the expected output.  
잠시 기다린 후 명령어를 다시 실행하면 **정상 출력**이 반환됩니다.  

---

## Security Importance  
## 보안 중요성  

Understanding and using IAM roles for your EC2 Instances is very important for security and proper AWS credential management.  
EC2 인스턴스에서 **IAM 역할을 이해하고 사용하는 것**은 보안과 AWS 자격 증명 관리에 매우 중요합니다.  

I hope you found this hands-on demonstration useful. I will see you in the next lecture.  
이번 실습이 도움이 되었길 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- Never enter your IAM Access Key ID and Secret Access Key directly into an EC2 Instance.  
- IAM Access Key와 Secret Key를 EC2 인스턴스에 직접 입력하지 마세요.  

- Use IAM roles to securely provide AWS credentials to EC2 Instances.  
- **IAM 역할**을 사용하여 안전하게 AWS 자격 증명을 제공하세요.  

- IAM roles attached to EC2 Instances allow running AWS CLI commands without manual credential configuration.  
- EC2에 연결된 IAM 역할을 통해 **수동 자격 증명 구성 없이 AWS CLI 명령어 실행 가능**.  

- Changes to IAM role permissions may take some time to propagate and reflect on the EC2 Instance.  
- IAM 역할 권한 변경은 **전파되어 인스턴스에 반영되기까지 시간이 걸릴 수 있음**.  

🎮 **게임보상**: "IAM Role 챔피언" 칭호 획득! 🛡️  
👉 이제 EC2에서 안전하게 AWS CLI를 사용할 수 있습니다.
