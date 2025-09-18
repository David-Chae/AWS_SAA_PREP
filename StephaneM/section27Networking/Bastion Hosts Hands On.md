````markdown
# Bastion Hosts Hands On  
# 배스천 호스트 실습  

🎮 게임보상: "Private Network Navigator" +300 XP  

---

## Introduction to Bastion Hosts  
## 배스천 호스트 소개  

The EC2 instance we have created in our public subnet can be designated as a Bastion host.  
퍼블릭 서브넷에 생성한 EC2 인스턴스를 배스천 호스트로 지정할 수 있습니다.  

This is because we can SSH into this Bastion host and from it, connect to an EC2 instance located in a private subnet.  
이유는, 이 배스천 호스트를 통해 SSH 접속 후, 프라이빗 서브넷에 있는 EC2 인스턴스로 연결할 수 있기 때문입니다.  

---

## Creating an EC2 Instance in a Private Subnet  
## 프라이빗 서브넷에 EC2 인스턴스 생성  

To proceed, let's create an EC2 instance in a private subnet.  
다음 단계로 프라이빗 서브넷에 EC2 인스턴스를 생성합니다.  

Before that, if you do not have a key pair, you can create one.  
그 전에, 키 페어가 없다면 새로 생성할 수 있습니다.  

Sometimes, I reuse accounts or create new ones, so I do not necessarily have key pairs already.  
가끔 계정을 재사용하거나 새로 만들기 때문에 기존 키 페어가 없을 수도 있습니다.  

You can simply create a key pair.  
간단히 키 페어를 생성하면 됩니다.  

I will create a demo key pair in PEM format and save this file.  
PEM 형식으로 데모 키 페어를 생성하고 파일로 저장합니다.  

This key pair will be very handy for SSH access into the EC2 instance in the private subnet.  
이 키 페어는 프라이빗 서브넷 EC2 인스턴스 SSH 접속 시 매우 유용합니다.  

---

## Launching the Private EC2 Instance  
## 프라이빗 EC2 인스턴스 실행  

Now, let's go to EC2 instances and launch a new EC2 instance.  
이제 EC2 인스턴스 화면으로 이동하여 새 인스턴스를 실행합니다.  

We will select Amazon Linux 2, t2.micro instance type.  
Amazon Linux 2, t2.micro 인스턴스 타입을 선택합니다.  

For the key pair, we will use the demo key pair we just created.  
키 페어로 방금 만든 데모 키 페어를 사용합니다.  

For network settings, ensure the instance is launched into our demo VPC.  
네트워크 설정에서 인스턴스가 데모 VPC에 생성되도록 확인합니다.  

For subnet association, select a private subnet, for example, Private Subnet A.  
서브넷 연결은 프라이빗 서브넷, 예를 들어 Private Subnet A를 선택합니다.  

Create a security group named privateSG since it is for the private subnet.  
프라이빗 서브넷용이므로 privateSG라는 보안 그룹을 생성합니다.  

We will allow SSH access, but not from anywhere; instead, we will allow SSH from the Bastion host's security group, which is currently named launch-wizard-1.  
SSH 접근을 허용하지만 모든 곳에서 허용하지 않고, 배스천 호스트 보안 그룹(현재 launch-wizard-1)에서만 허용합니다.  

I will rename it later for clarity.  
명확성을 위해 나중에 이름을 변경할 예정입니다.  

This setup allows SSH access to the private instance only through the Bastion host.  
이 설정으로 프라이빗 인스턴스는 배스천 호스트를 통해서만 SSH 접근이 가능합니다.  

---

## Launching and Accessing the Private Instance  
## 프라이빗 인스턴스 실행 및 접근  

After reviewing the settings, launch the private instance.  
설정을 확인한 후 프라이빗 인스턴스를 실행합니다.  

Since it is in a private subnet, we cannot use EC2 Instance Connect to access it directly because it lacks internet gateway access.  
프라이빗 서브넷에 있어 EC2 Instance Connect로 직접 접근할 수 없습니다. 인터넷 게이트웨이가 없기 때문입니다.  

Modifying the route tables to add an internet gateway would make the subnet public, which we want to avoid.  
라우트 테이블을 수정하여 인터넷 게이트웨이를 추가하면 서브넷이 퍼블릭이 되므로 피해야 합니다.  

Therefore, we will SSH into the private instance through the Bastion host.  
따라서 배스천 호스트를 통해 프라이빗 인스턴스에 SSH로 접속합니다.  

---

## Connecting Through the Bastion Host  
## 배스천 호스트를 통한 연결  

To connect, first SSH into the Bastion host.  
연결하려면 먼저 배스천 호스트에 SSH 접속합니다.  

You can use EC2 Instance Connect or your terminal's SSH command.  
EC2 Instance Connect 또는 터미널의 SSH 명령어를 사용할 수 있습니다.  

Once connected to the Bastion host, you can SSH into the private instance using its private IP address.  
배스천 호스트에 연결 후 프라이빗 IP를 사용해 프라이빗 인스턴스로 SSH 접속합니다.  

The SSH command format is:  
SSH 명령어 형식은 다음과 같습니다.  

```bash
ssh ec2-user@<private-ip> -i <key-pair.pem>
````

However, this requires the private instance to have the appropriate key pair installed.
단, 프라이빗 인스턴스에 적절한 키 페어가 설치되어 있어야 합니다.

---

## Installing the Key Pair on the Private Instance

## 프라이빗 인스턴스에 키 페어 설치

Since the private instance requires the key pair for SSH, we need to create the key pair file on the Bastion host.
프라이빗 인스턴스는 SSH에 키 페어가 필요하므로, 배스천 호스트에 키 페어 파일을 생성해야 합니다.

Use a text editor such as vi or nano to create a file named demo-key-pair.pem and paste the content of the key pair you downloaded earlier.
vi나 nano 같은 편집기를 사용해 demo-key-pair.pem 파일을 생성하고, 이전에 다운로드한 키 페어 내용을 붙여넣습니다.

Ensure the formatting is correct, including new lines. Save and exit the editor.
줄바꿈 등 형식이 올바른지 확인 후 저장하고 편집기를 종료합니다.

Then, change the permissions of the key pair file to be secure using:
그 후, 키 페어 파일 권한을 안전하게 변경합니다.

```bash
chmod 400 demo-key-pair.pem
```

---

## Troubleshooting Key Pair Formatting Issues

## 키 페어 형식 문제 해결

If you encounter issues such as permission denied or passphrase errors when attempting to SSH, it may be due to incorrect formatting of the key pair file.
SSH 접속 시 permission denied나 passphrase 오류가 발생하면 키 페어 파일 형식 문제일 수 있습니다.

Remove the existing file and recreate it using a different text editor to ensure proper formatting.
기존 파일을 삭제하고 다른 텍스트 편집기로 다시 생성하여 올바른 형식을 보장합니다.

After correcting the file, retry the SSH command:
파일을 수정한 후 SSH 명령어를 다시 실행합니다.

```bash
ssh -i demo-key-pair.pem ec2-user@<private-ip>
```

This should successfully connect you to the private EC2 instance.
이제 프라이빗 EC2 인스턴스에 정상적으로 연결됩니다.

---

## Verifying Connection and Internet Access

## 연결 및 인터넷 접근 확인

Once connected, you will be logged into the Amazon Linux 2 AMI in the private subnet.
연결되면 프라이빗 서브넷의 Amazon Linux 2 AMI에 로그인됩니다.

This confirms that SSH through the Bastion host to the private instance works correctly.
배스천 호스트를 통한 프라이빗 인스턴스 SSH 접속이 정상 작동함을 확인합니다.

However, if you try to ping an external address such as Google, it will fail because the private EC2 instance does not have outbound internet access by default.
하지만 Google 같은 외부 주소를 ping하면 실패합니다. 프라이빗 인스턴스는 기본적으로 아웃바운드 인터넷 접근이 없기 때문입니다.

We will address enabling internet access for the private instance in the next lecture.
프라이빗 인스턴스 인터넷 접근은 다음 강의에서 다룹니다.

---

## Summary

## 요약

In this session, we have learned how to use a Bastion host to securely access EC2 instances in a private subnet.
이번 세션에서는 배스천 호스트를 사용해 프라이빗 서브넷 EC2 인스턴스에 안전하게 접근하는 방법을 배웠습니다.

We created a key pair, launched a private EC2 instance, configured security groups to allow SSH only from the Bastion host, and successfully connected through the Bastion host to the private instance.
키 페어 생성, 프라이빗 EC2 인스턴스 실행, 배스천 호스트만 SSH 접근 허용하도록 보안 그룹 구성 후, 배스천 호스트를 통해 정상 접속을 수행했습니다.

Next, we will explore how to enable internet access for private instances.
다음으로 프라이빗 인스턴스의 인터넷 접근을 활성화하는 방법을 다룹니다.

---

## Key Takeaways

## 핵심 요약

* A Bastion host is an EC2 instance in a public subnet used to securely access instances in a private subnet.

* 배스천 호스트는 퍼블릭 서브넷에 위치한 EC2 인스턴스로, 프라이빗 서브넷 인스턴스에 안전하게 접근할 수 있습니다.

* To connect to a private EC2 instance, SSH through the Bastion host using a key pair.

* 프라이빗 EC2 인스턴스에 연결할 때는 배스천 호스트를 통해 키 페어로 SSH 접속합니다.

* Proper key pair management and permissions are essential for successful SSH connections.

* SSH 접속 성공을 위해 키 페어 관리 및 권한 설정이 필수


입니다.

* Private instances do not have internet access by default; additional configuration is required to enable outbound internet connectivity.
* 프라이빗 인스턴스는 기본적으로 인터넷 접근이 없으며, 아웃바운드 인터넷 연결을 위해 추가 구성이 필요합니다.

```

🎮 게임보상 완료: "Private Network Navigator" +300 XP 🏆  
