# How to SSH using Windows  
# 윈도우에서 SSH 사용하는 방법  
→ 윈도우 환경에서 EC2 인스턴스에 SSH 접속하는 과정을 설명하는 제목입니다.  

---

## Introduction to SSH on Windows  
## 윈도우에서 SSH 소개  
→ 윈도우 사용자를 위한 SSH 접속 튜토리얼입니다.  

In this tutorial, we will learn how to SSH into our EC2 instance using Windows.  
이번 튜토리얼에서는 윈도우를 사용하여 EC2 인스턴스에 SSH 접속하는 방법을 배웁니다.  
→ 윈도우 환경에서의 접근 방식을 단계별로 안내합니다.  

SSH, or Secure Shell, is one of the most important functions, especially when dealing with Amazon Cloud.  
SSH(보안 셸)는 특히 아마존 클라우드에서 중요한 기능 중 하나입니다.  
→ 서버 관리와 보안을 위해 필수적인 기술입니다.  

It allows you to control a machine remotely using the command line.  
명령줄을 통해 원격으로 서버를 제어할 수 있게 합니다.  
→ 물리적으로 접속하지 않아도 서버 조작이 가능합니다.  

---

## Understanding the Setup  
## 설정 이해하기  
→ 접속 환경을 이해하는 단계입니다.  

We have our EC2 machine running Amazon Linux 2 with a public IP address.  
퍼블릭 IP 주소를 가진 Amazon Linux 2 EC2 인스턴스를 준비합니다.  
→ 퍼블릭 IP가 있어야 외부에서 접속 가능합니다.  

Remember, we configured an SSH security group that allows SSH on port 22 from any IP.  
SSH 보안 그룹에서 포트 22를 모든 IP(0.0.0.0/0)에 대해 허용한 상태여야 합니다.  
→ 보안 그룹 설정이 올바르지 않으면 접속 불가합니다.  

This setup enables our Windows machine to connect over the internet directly to the EC2 instance and control it via the command line.  
이 설정을 통해 윈도우 컴퓨터에서 인터넷으로 EC2 인스턴스에 접속하고 명령줄로 제어할 수 있습니다.  
→ 포트 22 개방과 퍼블릭 IP가 핵심입니다.  

---

## Using PuTTY for SSH  
## SSH를 위한 PuTTY 사용하기  
→ 윈도우에서 자주 쓰이는 무료 SSH 클라이언트입니다.  

We will use PuTTY, a free SSH client available online, to establish the SSH connection.  
온라인에서 무료로 제공되는 SSH 클라이언트 PuTTY를 사용하여 접속합니다.  
→ 윈도우에서 가장 보편적으로 사용되는 SSH 도구입니다.  

Although PuTTY can be a bit tricky to use initially, we will guide you through the process to SSH from Windows into Linux using PuTTY.  
PuTTY는 처음 사용 시 다소 복잡할 수 있지만, 본 강의에서 윈도우에서 리눅스로 접속하는 과정을 안내합니다.  
→ 단계별 설명으로 쉽게 따라 할 수 있습니다.  

---

## Windows Versions and Alternatives  
## 윈도우 버전 및 대체 방법  
→ 윈도우 버전에 따라 접속 방법이 다를 수 있습니다.  

This tutorial assumes you are using Windows 7, Windows 8, or an older version of Windows.  
본 튜토리얼은 Windows 7, 8, 혹은 그 이전 버전을 사용하는 것을 가정합니다.  
→ 최신 버전이 아닌 경우 PuTTY가 필수입니다.  

If you have Windows 10, there is an alternative method covered in the next lecture.  
Windows 10을 사용하는 경우 다음 강의에서 다른 방법을 다룹니다.  
→ Windows 10 이상은 기본 SSH 클라이언트를 지원합니다.  

Both methods work, but you can follow this technique even if you are on Windows 10.  
두 방법 모두 사용 가능하며, Windows 10에서도 이 방식을 그대로 따라 할 수 있습니다.  
→ PuTTY는 모든 윈도우 버전에서 호환됩니다.  

---

## Downloading and Installing PuTTY  
## PuTTY 다운로드 및 설치  
→ SSH 클라이언트 설치 단계입니다.  

First, download PuTTY, which is a free SSH client for Windows.  
먼저 무료 SSH 클라이언트인 PuTTY를 다운로드합니다.  

Choose the 64-bit installer, which is usually the first option.  
보통 첫 번째 옵션인 64비트 설치 파일을 선택합니다.  

After downloading, proceed with the installation by clicking next, next, and then yes to install PuTTY.  
다운로드 후 `Next → Next → Yes`를 눌러 설치를 완료합니다.  

Once installed, you will have access to both the PuTTY application and PuTTYgen.  
설치가 완료되면 PuTTY와 PuTTYgen 두 가지 프로그램을 사용할 수 있습니다.  

---

## Generating a PPK File Using PuTTYgen  
## PuTTYgen으로 PPK 파일 생성하기  
→ PEM 키를 PuTTY에서 사용할 수 있도록 변환합니다.  

If you do not have your private key in the PPK format, you can generate it using PuTTYgen:  
PPK 형식의 개인 키가 없다면 PuTTYgen을 사용해 변환할 수 있습니다:  

- Open PuTTYgen.  
  PuTTYgen을 엽니다.  

- Click on "Load" and navigate to your PEM file (for example, on your desktop).  
  `Load`를 눌러 PEM 파일(예: 바탕화면)을 선택합니다.  

- Make sure to select "All Files" to see your PEM file.  
  PEM 파일을 보려면 "All Files"를 선택해야 합니다.  

- Select your PEM file and load it.  
  PEM 파일을 선택 후 로드합니다.  

- After successful import, click "Save private key".  
  가져오기가 끝나면 `Save private key`를 클릭합니다.  

- If prompted about saving without a passphrase, confirm by clicking "Yes".  
  암호 구문 없이 저장하겠냐는 메시지가 나오면 `Yes`를 클릭합니다.  

- Save the PPK file on your desktop or preferred location.  
  PPK 파일을 바탕화면이나 원하는 위치에 저장합니다.  

This process converts your PEM file into a PPK file compatible with PuTTY.  
이 과정은 PEM 파일을 PuTTY에서 사용할 수 있는 PPK 파일로 변환합니다.  

---

## Configuring PuTTY to Access Your EC2 Instance  
## EC2 접속을 위한 PuTTY 설정  
→ PuTTY에서 세션을 생성하고 저장합니다.  

- Open the PuTTY application.  
  PuTTY 프로그램을 실행합니다.  

- In the "Host Name" field, enter the public IPv4 address of your EC2 instance.  
  "Host Name" 입력란에 EC2 퍼블릭 IPv4 주소를 입력합니다.  

- Save this session with a recognizable name, such as "EC2 Instance".  
  세션을 "EC2 Instance" 같은 이름으로 저장합니다.  

However, this is not sufficient to connect; additional configuration is required.  
그러나 이것만으로는 접속이 되지 않으며 추가 설정이 필요합니다.  

---

## Specifying the Username and Private Key in PuTTY  
## PuTTY에서 사용자 이름과 키 지정하기  
→ SSH 인증을 위해 사용자명과 키 파일을 지정해야 합니다.  

- Load your saved session (e.g., "EC2 Instance") in PuTTY.  
  저장된 세션(예: "EC2 Instance")을 불러옵니다.  

- In the "Host Name" field, prepend the username to the IP address in the format: ec2-user@<public-ip>.  
  "Host Name" 입력란에 `ec2-user@<public-ip>` 형식으로 사용자명과 IP를 입력합니다.  

- Save the session again.  
  세션을 다시 저장합니다.  

- Navigate to the "SSH" section in PuTTY's sidebar.  
  왼쪽 메뉴에서 "SSH" 섹션으로 이동합니다.  

- Click on "Auth".  
  "Auth"를 클릭합니다.  

- Click "Browse" and select your PPK private key file.  
  "Browse"를 눌러 PPK 개인 키 파일을 선택합니다.  

- Return to the "Session" section and save the session again.  
  다시 "Session"으로 돌아가 세션을 저장합니다.  

This configuration ensures PuTTY uses the correct username and private key for authentication.  
이 설정을 통해 PuTTY가 올바른 사용자명과 개인 키를 사용해 인증하게 됩니다.  

---

## Connecting to the EC2 Instance  
## EC2 인스턴스 접속하기  
→ 설정 완료 후 SSH 연결을 시작합니다.  

After saving all settings:  
모든 설정을 저장한 후:  

- Click "Open" to initiate the SSH connection.  
  "Open"을 눌러 SSH 연결을 시작합니다.  

- If prompted with a security alert about the server's host key, accept it by clicking "Yes".  
  서버 호스트 키 경고가 나오면 "Yes"를 눌러 수락합니다.  

You should now be authenticated as the ec2-user and have command-line access to your Amazon Linux 2 instance.  
이제 ec2-user로 인증되어 Amazon Linux 2 인스턴스에 명령줄 접속이 가능합니다.  

You can verify your login by running commands such as whoami or pinging external sites like ping google.com.  
`whoami` 명령어로 사용자 확인, `ping google.com`으로 인터넷 연결 테스트를 할 수 있습니다.  

---

## Ending the SSH Session  
## SSH 세션 종료하기  
→ PuTTY 접속을 끝내는 방법입니다.  

To stop running commands, use Control + C.  
실행 중인 명령어를 멈추려면 Control + C를 누릅니다.  

To exit the SSH session, simply close the PuTTY window or type exit in the terminal.  
SSH 세션을 종료하려면 PuTTY 창을 닫거나 터미널에서 `exit`을 입력합니다.  

Your session will close, and you will return to your Windows environment.  
세션이 종료되면 윈도우 환경으로 돌아갑니다.  

---

## Reusing Saved PuTTY Sessions  
## 저장된 PuTTY 세션 재사용하기  
→ 같은 설정으로 빠르게 재접속할 수 있습니다.  

When you reopen PuTTY:  
PuTTY를 다시 실행하면:  

- Load your saved session (e.g., "EC2 Instance").  
  저장된 세션을 불러옵니다.  

- All your previous settings, including the host, username, and private key, will be retained.  
  이전의 호스트, 사용자 이름, 키 설정이 그대로 유지됩니다.  

- Click "Open" to connect quickly without reconfiguring.  
  "Open"을 눌러 재설정 없이 빠르게 접속합니다.  

This feature simplifies repeated access to your EC2 instance.  
이 기능 덕분에 반복 접속이 간단해집니다.  

---

## Summary  
## 요약  
→ 강의 전체 내용을 정리합니다.  

We have successfully performed SSH into an EC2 instance using PuTTY on Windows 7 or Windows 8.  
Windows 7 또는 8에서 PuTTY를 사용해 EC2 인스턴스에 SSH 접속을 완료했습니다.  

In the next lecture, we will cover how to SSH using Windows 10.  
다음 강의에서는 Windows 10에서 SSH 접속 방법을 다룹니다.  

---

## Key Takeaways  
## 핵심 요약  
→ 꼭 기억해야 할 사항입니다.  

- SSH allows remote command-line control of machines, essential for managing Amazon EC2 instances.  
  SSH는 EC2 인스턴스 관리에 필수적인 원격 명령줄 제어 기능을 제공합니다.  

- PuTTY is a free SSH client for Windows that requires converting PEM keys to PPK format using PuTTYgen.  
  PuTTY는 무료 SSH 클라이언트로, PEM 키를 PuTTYgen으로 PPK 형식으로 변환해야 합니다.  

- Proper configuration of PuTTY with the EC2 instance's public IP, username, and private key enables successful SSH connections.  
  EC2 퍼블릭 IP, 사용자명, 개인 키를 올바르게 설정해야 SSH 접속이 성공합니다.  

- Saved PuTTY sessions simplify repeated access to EC2 instances without reconfiguring settings each time.  
  저장된 PuTTY 세션을 사용하면 매번 재설정할 필요 없이 빠르게 접속할 수 있습니다.  
