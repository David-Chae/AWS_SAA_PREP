```md
# SSH Overview  
# SSH 개요  
👉 클라우드 서버 접속을 위한 **SSH 기본 개념** 정리입니다.  

---

## Introduction to SSH for Cloud Servers  
## 클라우드 서버를 위한 SSH 소개  

Connecting inside your servers to perform maintenance or actions is one of the trickier aspects of running in the Cloud.  
클라우드에서 서버 내부에 접속해 유지보수나 작업을 수행하는 것은 까다로운 부분 중 하나입니다.  

For Linux servers, we can use SSH to securely shell into our servers.  
리눅스 서버에서는 SSH를 사용해 안전하게 서버에 쉘 접속할 수 있습니다.  

---

## SSH Tools Based on Operating System  
## 운영체제별 SSH 도구  

Depending on the operating system on your computer, there are different ways to achieve SSH connections:  
사용 중인 운영체제에 따라 SSH 접속 방식이 다릅니다:  

- Mac and Linux: Use the SSH command line interface utility.  
  Mac과 Linux: **SSH 명령줄 도구** 사용.  

- Windows before version 10: Use Putty, which performs the exact same function as SSH.  
  Windows 10 이전: **Putty** 사용 (SSH와 동일한 기능).  

- Windows version 10 and later: Use the SSH command line interface utility.  
  Windows 10 이상: **SSH 명령줄 도구** 사용 가능.  

Putty is valid for any version of Windows and allows you to use the SSH protocol to connect to your EC2 instances.  
Putty는 모든 버전의 Windows에서 사용 가능하며, EC2 인스턴스에 SSH 프로토콜로 접속할 수 있게 합니다.  

---

## EC2 Instance Connect  
## EC2 인스턴스 커넥트  

There is a new method called EC2 Instance Connect that uses your web browser instead of a terminal or Putty to connect to your EC2 instance.  
터미널이나 Putty 대신 **웹 브라우저**로 EC2 인스턴스에 접속할 수 있는 새로운 방법이 EC2 Instance Connect입니다.  

This method is compatible with Mac, Linux, and all versions of Windows.  
이 방식은 Mac, Linux, 모든 Windows 버전에서 호환됩니다.  

The advantage of EC2 Instance Connect is its simplicity and broad compatibility.  
EC2 Instance Connect의 장점은 **간단함**과 **광범위한 호환성**입니다.  

However, it currently only works with Amazon EC2 instances ...  
하지만 현재는 **Amazon EC2 인스턴스에서만** 동작합니다.  

---

## Choosing the Right SSH Method  
## 적절한 SSH 방식 선택하기  

If you are on Mac or Linux, please watch the SSH lecture specific to Mac/Linux.  
Mac/Linux 사용자는 해당 SSH 강의를 참고하세요.  

If you are on Windows, you can either watch the Putty lecture or, if you have Windows 10, watch the SSH on Windows 10 lecture.  
Windows 사용자는 Putty 강의를 보거나, Windows 10 이상이면 **Windows 10 SSH 강의**를 참고하세요.  

Personally, in future lectures, EC2 Instance Connect will be used ...  
앞으로는 설치나 명령어 지식이 필요 없는 **EC2 Instance Connect**를 활용할 예정입니다.  

---

## Troubleshooting SSH  
## SSH 문제 해결  

SSH has been the source of most troubles in this course ...  
이 강의에서 가장 많은 문제가 발생한 부분이 **SSH**입니다.  

If you encounter problems with SSH, consider the following:  
SSH 문제가 생긴다면 다음을 확인하세요:  

- Re-watch the lecture to ensure nothing was missed.  
  강의를 다시 보며 놓친 부분이 없는지 확인.  

- Check security group rules.  
  **보안 그룹 규칙** 확인.  

- Verify your commands for typos.  
  **명령어 오타** 확인.  

A troubleshooting guide has been provided after these lectures ...  
강의 후반부에 문제 해결 가이드가 제공됩니다.  

Trying EC2 Instance Connect may also resolve many issues.  
EC2 Instance Connect를 시도하면 많은 문제가 해결될 수 있습니다.  

---

## Final Notes  
## 마무리  

If one SSH method works, you are good to go; you do not need all methods to work.  
SSH 방식 중 하나만 잘 되면 충분하며, 모든 방식이 작동할 필요는 없습니다.  

If none of the methods work, that is completely okay.  
어느 방식도 작동하지 않아도 괜찮습니다.  

This course is introductory, and SSH will not be used extensively, so you will be fine.  
이 강의는 입문용이므로 SSH를 많이 쓰지 않으니 큰 문제는 없습니다.  

This concludes the introduction. Please find the lecture appropriate for your operating system ...  
이것으로 소개를 마칩니다. 운영체제에 맞는 강의를 참고하세요.  

---

## Key Takeaways  
## 핵심 요약  

- SSH is a secure shell protocol used to connect to Linux servers for maintenance or actions.  
  SSH는 리눅스 서버에 안전하게 접속해 유지보수나 작업을 수행하는 **보안 쉘 프로토콜**입니다.  

- Different operating systems require different SSH tools:  
  OS마다 다른 SSH 도구 필요:  
  - Mac/Linux: SSH CLI  
  - Windows < 10: Putty  
  - Windows ≥ 10: SSH CLI  

- EC2 Instance Connect allows connecting via web browser, supporting all OS.  
  EC2 Instance Connect는 웹 브라우저를 통해 접속 가능하며 모든 OS 지원.  

- Troubleshooting SSH issues often involves checking security group rules, commands, or typos.  
  SSH 문제 해결은 주로 **보안 그룹 규칙, 명령어, 오타**를 확인하는 것.  

- EC2 Instance Connect can resolve many common problems.  
  EC2 Instance Connect는 많은 일반적인 문제를 해결할 수 있습니다.  

---

🎮 **게임 보상**: "원격 접속 마스터" 칭호 획득!  
👉 이제 당신은 EC2에 자유자재로 접속할 수 있는 자격을 얻었습니다. 🚀
```
