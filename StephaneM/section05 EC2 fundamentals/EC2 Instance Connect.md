# EC2 Instance Connect  
# EC2 인스턴스 연결  

---

## Introduction to EC2 Instance Connect  
## EC2 인스턴스 연결 소개  

I want to show you an alternative to SSH that I found a lot easier, which is the EC2 Instance Connect.  
저는 SSH보다 훨씬 쉽게 느껴지는 **대안 방법인 EC2 Instance Connect**를 소개하고자 합니다.  

To use this, click on "My First Instance" and then click on the top where it says "Connect."  
사용하려면 "My First Instance"를 클릭한 후 상단의 "Connect" 버튼을 클릭합니다.  

You have multiple options, including the SSH client we saw before. One option I want to show you is the EC2 Instance Connect.  
이전에 본 SSH 클라이언트를 포함해 여러 옵션이 나오는데, 제가 보여드릴 옵션은 **EC2 Instance Connect**입니다.  

---

## Browser-based SSH session  
## 브라우저 기반 SSH 세션  

EC2 Instance Connect allows us to do a browser-based SSH session into our EC2 instance.  
EC2 Instance Connect는 **브라우저에서 직접 SSH 세션**을 수행할 수 있게 해줍니다.  

For this, we verified the public IP address, which is good. The username is provided by default, which is ec2-user because AWS guesses that we are using Amazon Linux 2, and therefore ec2-user is the right username.  
이를 위해 퍼블릭 IP를 확인했으며, 기본 사용자 이름은 **ec2-user**입니다. AWS가 Amazon Linux 2를 사용한다고 추정하기 때문입니다.  

If you wanted to, you could override it, but it does not work unless you enter ec2-user. So we'll leave it as is for now.  
원한다면 사용자 이름을 바꿀 수도 있지만, **ec2-user**가 아니면 작동하지 않습니다. 따라서 기본값을 사용합니다.  

---

## Temporary SSH key  
## 임시 SSH 키  

As you see, there is no SSH key option because when we connect, it uploads a temporary SSH key for us and establishes a connection this way.  
보시다시피 SSH 키 옵션이 없는 이유는, 연결 시 **임시 SSH 키를 업로드하여 연결**을 생성하기 때문입니다.  

With this methodology, we do not even need to manage SSH keys, which I found lovely.  
이 방법을 사용하면 SSH 키를 직접 관리할 필요조차 없어 매우 편리합니다.  

---

## Connecting via browser  
## 브라우저를 통한 연결  

You click on "Connect," and it opens a new tab. Very quickly, you are into your Amazon Linux 2 AMI, and you can start running some commands such as whoami or ping google.com.  
"Connect"를 클릭하면 새 탭이 열리고, **즉시 Amazon Linux 2 AMI**에 접속해 `whoami`나 `ping google.com` 같은 명령어를 실행할 수 있습니다.  

The cool thing about it is that your session is in the browser instead of using a different command line interface such as Terminal.  
이 방법의 장점은 **브라우저에서 세션을 수행**하므로 Terminal 같은 별도 CLI를 사용할 필요가 없다는 점입니다.  

---

## Using EC2 Instance Connect in this course  
## 이 강의에서 EC2 Instance Connect 사용  

In this course, if I say use SSH, you have either the option to use your own terminal, mssh, or to use, for example, PuTTY, or to use the SSH command on Windows, or to use, regardless of whether you are on Windows, Linux, or Mac, the EC2 Instance Connect.  
강의에서 SSH를 사용하라고 하면, 자신의 터미널, mssh, PuTTY, Windows SSH CLI, 또는 **EC2 Instance Connect**를 사용할 수 있습니다.  

Now, this is relying on SSH behind the scenes.  
이 방법도 내부적으로는 SSH를 사용합니다.  

---

## Security Group Port Requirement  
## 보안 그룹 포트 설정  

EC2 Instance Connect requires port 22 to be open in the security group's inbound rules for successful connection.  
성공적인 연결을 위해 **보안 그룹의 인바운드 규칙에서 포트 22**를 열어야 합니다.  

It is important to allow both IPv4 and IPv6 SSH inbound rules depending on your network setup.  
네트워크 설정에 따라 **IPv4와 IPv6 SSH 인바운드 규칙**을 모두 허용하는 것이 중요합니다.  

---

## Quick Demo and Troubleshooting  
## 빠른 데모 및 문제 해결  

If there’s a problem connecting, ensure SSH inbound rules exist for both IPv4 and IPv6 in your security group.  
연결 문제가 발생하면 보안 그룹에서 **IPv4 및 IPv6 SSH 인바운드 규칙**이 존재하는지 확인하세요.  

We are good to go now. If we try to connect to the instance itself, let's try to connect here. Voila, we are into the instance.  
이제 준비 완료입니다. 인스턴스에 연결을 시도하면, **바로 접속**됩니다.  

That was a quick demo of EC2 Instance Connect. I will use it a lot in this course.  
짧은 EC2 Instance Connect 데모였습니다. 강의 내내 자주 사용할 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- EC2 Instance Connect provides a browser-based SSH session to EC2 instances, simplifying access without managing SSH keys.  
- EC2 Instance Connect는 브라우저 기반 SSH 세션을 제공하며, SSH 키 관리 없이 쉽게 접근할 수 있습니다.  

- The default username for Amazon Linux 2 AMI is ec2-user, which is automatically set by AWS.  
- Amazon Linux 2 AMI 기본 사용자 이름은 **ec2-user**이며, AWS가 자동으로 설정합니다.  

- EC2 Instance Connect requires port 22 to be open in the security group's inbound rules for successful connection.  
- 성공적인 연결을 위해 보안 그룹의 인바운드 규칙에서 포트 22를 열어야 합니다.  

- It is important to allow both IPv4 and IPv6 SSH inbound rules depending on your network setup.  
- 네트워크 설정에 따라 IPv4와 IPv6 SSH 인바운드 규칙을 모두 허용하는 것이 중요합니다.  

🎮 **게임보상**: "브라우저 SSH 마스터" 칭호 획득! 🚀  
👉 이제 브라우저에서 바로 EC2에 접속할 수 있습니다.
