
# How to SSH using Linux or Mac  
# 리눅스 또는 맥에서 SSH 접속 방법  
→ EC2 인스턴스에 접속하기 위해 Linux/Mac 환경에서 SSH 사용하는 방법을 설명하는 제목입니다.  

---

## Introduction to SSH on EC2 Instances  
## EC2 인스턴스에서 SSH 소개  
→ SSH(보안 셸)는 원격 서버 제어에 필수적이며, AWS EC2 환경에서 많이 사용됩니다.  

In this lecture, we will learn how to SSH into our EC2 instance using a Linux or Mac computer.  
이번 강의에서는 리눅스나 맥을 사용하여 EC2 인스턴스에 SSH로 접속하는 방법을 배웁니다.  
→ SSH 접속은 클라우드 서버를 원격 제어하기 위한 첫 단계입니다.  

SSH, or Secure Shell, is one of the most important functions when working with Amazon Cloud.  
SSH(보안 셸)는 아마존 클라우드 작업에서 가장 중요한 기능 중 하나입니다.  
→ 서버에 안전하게 접속하고 명령어를 실행할 수 있습니다.  

It allows you to control a remote machine or server entirely through your terminal or command line interface.  
터미널이나 명령줄 인터페이스를 통해 원격 서버를 완전히 제어할 수 있게 합니다.  
→ 즉, 직접 접속하지 않고도 서버 내부 작업을 할 수 있습니다.  

---

## How SSH Works with EC2  
## EC2에서 SSH 작동 방식  
→ 보안 그룹과 포트 설정이 SSH 접속에 중요한 역할을 합니다.  

Imagine we have an EC2 machine running Amazon Linux 2 with a public IP address.  
퍼블릭 IP 주소를 가진 Amazon Linux 2 EC2 인스턴스를 가정해봅시다.  
→ 퍼블릭 IP는 외부 접속이 가능하게 해줍니다.  

To access this machine, we use a security group that allows inbound traffic on Port 22, which is the SSH port.  
이 인스턴스에 접근하기 위해 SSH 포트(22번 포트)를 허용하는 보안 그룹을 사용합니다.  
→ 보안 그룹 규칙에 포트 22가 반드시 열려 있어야 합니다.  

From your computer, you connect over the web through Port 22 to the EC2 machine.  
컴퓨터에서 포트 22를 통해 EC2 인스턴스로 접속합니다.  
→ 인터넷을 통해 암호화된 연결이 형성됩니다.  

This connection makes your command line interface behave as if you were directly inside the remote machine.  
이 연결로 명령줄이 원격 서버 내부에서 실행되는 것처럼 동작합니다.  
→ 마치 원격 서버 안에 직접 로그인한 것과 같습니다.  

---

## Preparing Your PEM Key File  
## PEM 키 파일 준비하기  
→ SSH 접속을 위해서는 PEM 키 파일이 필수입니다.  

Before connecting, ensure you have downloaded your PEM file, for example, named EC2Tutorial.pem.  
접속하기 전에 PEM 파일(예: EC2Tutorial.pem)을 다운로드해야 합니다.  
→ 키 파일은 EC2 생성 시 발급됩니다.  

It is important to remove any spaces in the filename.  
파일 이름에 공백이 없어야 합니다.  
→ 공백이 있으면 SSH 명령 실행 시 오류가 발생합니다.  

If you have a PPK file, rename it to remove spaces as well.  
PPK 파일이 있다면 이름에서 공백을 제거해야 합니다.  
→ PPK는 주로 Windows PuTTY용 키 파일 형식입니다.  

Place this PEM file in a directory you prefer; for instance, I placed mine in a folder called aws-course.  
PEM 파일은 원하는 디렉터리에 저장하세요. 예: aws-course 폴더.  
→ 관리하기 쉬운 폴더에 두는 것이 좋습니다.  

---

## Finding Your EC2 Instance Public IP  
## EC2 인스턴스 퍼블릭 IP 찾기  
→ 퍼블릭 IP 주소는 SSH 접속 시 꼭 필요합니다.  

Next, navigate to your EC2 instance overview page and locate your instance.  
AWS EC2 콘솔에서 인스턴스 개요 페이지로 이동해 인스턴스를 확인합니다.  
→ 실행 중인 인스턴스를 찾아야 합니다.  

Copy the public IPv4 address, which you will use to connect via SSH.  
SSH 접속에 사용할 퍼블릭 IPv4 주소를 복사합니다.  
→ 이 주소가 접속 대상 서버 주소입니다.  

Also, verify your security group settings to ensure Port 22 is open to allow SSH connections from anywhere (0.0.0.0/0).  
보안 그룹 설정에서 포트 22가 어디서든 접속 가능(0.0.0.0/0)으로 열려 있는지 확인합니다.  
→ 그렇지 않으면 외부에서 접속할 수 없습니다.  

If this rule is missing, add it to your security group.  
해당 규칙이 없다면 보안 그룹에 추가하세요.  
→ SSH가 차단되지 않도록 반드시 설정해야 합니다.  

---

## Initial SSH Attempt Without Key  
## 키 없이 SSH 접속 시도  
→ 기본 접속을 해보면 인증 오류가 발생합니다.  

To attempt an SSH connection, use the command:  
SSH 접속을 시도하려면 다음 명령어를 사용합니다:  
```bash
ssh ec2-user@[Public_IP]
````

The user ec2-user is the default user set up on Amazon Linux 2 AMIs.
`ec2-user`는 Amazon Linux 2의 기본 사용자 계정입니다.

However, without specifying the PEM key, you will likely receive an error such as "too many authentication failures".
PEM 키를 지정하지 않으면 “too many authentication failures” 오류가 발생할 수 있습니다.
→ 인증에 실패했음을 의미합니다.

---

## Specifying the PEM Key and Directory

## PEM 키와 디렉터리 지정하기

→ PEM 키를 지정해야 정상적으로 접속할 수 있습니다.

To fix the authentication error, include the PEM key in your SSH command and ensure your terminal is in the directory containing the PEM file.
인증 오류를 해결하려면 SSH 명령어에 PEM 키를 포함시키고 터미널이 PEM 파일이 위치한 디렉터리에 있어야 합니다.

For example, if your PEM file is named EC2Tutorial.pem and located in the aws-course folder, navigate there using:
예: PEM 파일 이름이 EC2Tutorial.pem이고 aws-course 폴더에 있다면 다음 명령어를 실행합니다:

```bash
cd aws-course
```

Then verify the file is present with:
그 다음 파일이 있는지 확인합니다:

```bash
ls
```

Your SSH command should be:
SSH 접속 명령어는 다음과 같습니다:

```bash
ssh -i EC2Tutorial.pem ec2-user@[Public_IP]
```

---

## Setting Correct Permissions for the PEM File

## PEM 파일 권한 설정하기

→ 키 파일 권한이 올바르지 않으면 보안 오류가 납니다.

If you encounter an error about an "unprotected key file," you need to change the file permissions to be more secure.
“unprotected key file” 오류가 나오면 파일 권한을 변경해야 합니다.

Use the following command:
다음 명령어를 사용합니다:

```bash
chmod 0400 EC2Tutorial.pem
```

This command restricts the file permissions so that only the owner can read it, which is required for SSH to accept the key.
이 명령은 오직 소유자만 읽을 수 있도록 권한을 제한하며, SSH에서 키를 허용하기 위해 필수입니다.

---

## Successful SSH Connection

## 성공적인 SSH 접속

→ 올바른 키와 권한을 설정하면 접속이 성공합니다.

After setting the correct permissions, try the SSH command again:
권한을 설정한 후 다시 SSH 명령어를 실행합니다:

```bash
ssh -i EC2Tutorial.pem ec2-user@[Public_IP]
```

If prompted to trust the host, type yes.
호스트 신뢰 여부를 물으면 `yes`를 입력합니다.

Upon successful connection, your terminal prompt will change to indicate you are logged into the EC2 instance.
성공하면 터미널 프롬프트가 EC2 인스턴스에 로그인된 형태로 바뀝니다.

Example:
예시:

```bash
ec2-user@[Public_IP]
```

---

## Basic Commands on the EC2 Instance

## EC2 인스턴스에서 기본 명령어

→ 접속 후 몇 가지 테스트 명령어를 실행할 수 있습니다.

Try running commands such as:
다음과 같은 명령어를 실행해 보세요:

* `whoami` → 사용자 이름 확인 (ec2-user)
* `ping google.com` → 인터넷 연결 테스트
* Control + C → ping 명령 중지

---

## Exiting the SSH Session

## SSH 세션 종료하기

→ 접속을 끝내려면 종료 명령을 사용합니다.

To exit the SSH session, you can either type:
SSH 세션을 종료하려면 다음을 입력합니다:

```bash
exit
```

or press Control + G.
또는 Control + G를 누릅니다.

This will close the connection to your EC2 instance.
이렇게 하면 EC2 인스턴스와의 연결이 종료됩니다.

---

## Reconnecting to Your EC2 Instance

## EC2 인스턴스에 재접속하기

→ 인스턴스를 재시작하면 IP가 바뀔 수 있습니다.

To reconnect, use the SSH command with the PEM key, user, and current public IP address:
재접속하려면 PEM 키, 사용자, 현재 퍼블릭 IP로 SSH 명령어를 실행합니다:

```bash
ssh -i EC2Tutorial.pem ec2-user@[Public_IP]
```

Note that if you stop and start your instance, the public IP address may change, so ensure you use the updated IP address each time.
인스턴스를 중지 후 시작하면 퍼블릭 IP가 바뀔 수 있으니, 항상 최신 IP를 확인해야 합니다.

---

## Key Takeaways

## 핵심 요약

→ SSH 접속 시 반드시 지켜야 할 포인트들입니다.

* SSH allows remote control of an EC2 instance through the terminal.
  SSH는 터미널을 통해 EC2 인스턴스를 원격 제어할 수 있습니다.

* The PEM key file must be correctly named and located in the current directory.
  PEM 키 파일은 올바른 이름으로 현재 디렉터리에 있어야 합니다.

* The SSH command requires specifying the user, key file, and public IP address.
  SSH 명령어에는 사용자, 키 파일, 퍼블릭 IP를 지정해야 합니다.

* File permissions for the PEM key must be set to 0400 to avoid security errors.
  PEM 키 파일의 권한은 0400으로 설정해야 보안 오류를 피할 수 있습니다.


