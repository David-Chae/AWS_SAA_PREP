```markdown
# SSM Session Manager  
# SSM 세션 매니저  
🎮 **보상: "보안 원격 접속 초심자 뱃지" 획득!**  

---

## Introduction to SSM Session Manager  
## SSM 세션 매니저 소개  
The SSM Session Manager feature of Systems Manager allows you to start a secure shell on your EC2 instances and on-premises servers without requiring SSH access, bastion hosts, or SSH keys.  
SSM 세션 매니저 기능을 사용하면 SSH 접속, 배스천 호스트, SSH 키 없이도 EC2 인스턴스 및 온프레미스 서버에서 안전한 셸을 시작할 수 있습니다.  
👉 SSH를 사용하지 않아도 되므로 보안이 향상됩니다.  

This means that port 22 on your EC2 instances can remain closed, enhancing security by eliminating the need for SSH to establish a secure shell connection.  
즉, EC2 인스턴스의 포트 22를 닫아둬도 되며, SSH를 통한 연결이 필요 없어 보안이 강화됩니다.  

The EC2 instance used in this demonstration has an SSM Agent installed, which connects to the Session Manager service.  
이번 데모에서 사용하는 EC2 인스턴스에는 SSM 에이전트가 설치되어 있으며, 세션 매니저 서비스와 연결됩니다.  

This setup enables users to access the instance through the Session Manager service and execute commands securely.  
이 설정을 통해 사용자는 세션 매니저 서비스를 통해 인스턴스에 안전하게 접속하고 명령을 실행할 수 있습니다.  

Session Manager supports Linux, macOS, and Windows operating systems.  
세션 매니저는 Linux, macOS, Windows 운영체제를 지원합니다.  

Additionally, it can send log data to Amazon S3 or CloudWatch Logs to ensure enhanced security and auditing capabilities.  
또한, 세션 로그 데이터를 Amazon S3 또는 CloudWatch Logs로 전송하여 보안과 감사 기능을 강화할 수 있습니다.  

---

## Launching an EC2 Instance for Session Manager  
## 세션 매니저용 EC2 인스턴스 시작  
To begin, we launch an EC2 instance using the Amazon Linux 2 AMI with a t2.micro instance type.  
먼저, Amazon Linux 2 AMI와 t2.micro 인스턴스 유형을 사용하여 EC2 인스턴스를 시작합니다.  

No key pair is used, and SSH traffic is disabled by configuring the security group to allow no inbound traffic, including HTTP, HTTPS, or SSH.  
키 페어를 사용하지 않고, 보안 그룹을 통해 HTTP, HTTPS, SSH 등 모든 인바운드 트래픽을 차단합니다.  

Despite this, we will still be able to access the instance using the SSM Session Manager shell.  
그럼에도 불구하고, SSM 세션 매니저를 통해 인스턴스에 접속할 수 있습니다.  

An IAM instance profile must be attached to the EC2 instance to allow it to communicate with the SSM service.  
SSM 서비스와 통신하려면 EC2 인스턴스에 IAM 인스턴스 프로파일을 연결해야 합니다.  

To do this, we create a new IAM role for Amazon EC2 with the Amazon SSM managed instance core policy attached.  
이를 위해 Amazon SSM 관리형 인스턴스 핵심 정책이 연결된 새로운 EC2용 IAM 역할을 생성합니다.  

This role, named demo EC2 role for SSM, grants the necessary permissions for the instance to be managed by the SSM service and to utilize the Session Manager feature.  
이 역할(이름: demo EC2 role for SSM)은 인스턴스가 SSM 서비스로 관리되고 세션 매니저 기능을 사용할 수 있도록 필요한 권한을 부여합니다.  

After creating and attaching the IAM role, we launch the EC2 instance.  
IAM 역할을 생성하고 연결한 후, EC2 인스턴스를 시작합니다.  

Once the instance boots, we verify its registration with the SSM service by navigating to Systems Manager and selecting Fleet Manager.  
인스턴스가 부팅되면 Systems Manager → Fleet Manager에서 SSM 서비스 등록을 확인합니다.  

Fleet Manager displays all EC2 instances registered with SSM, known as managed nodes.  
Fleet Manager는 SSM에 등록된 모든 EC2 인스턴스(관리 노드)를 표시합니다.  

When the instance appears as running with the SSM Agent online, it is ready for secure shell access via Session Manager.  
인스턴스가 실행 중이고 SSM 에이전트가 온라인 상태이면 세션 매니저를 통한 안전한 셸 접속이 준비된 상태입니다.  

---

## Using Session Manager to Access the EC2 Instance  
## 세션 매니저로 EC2 인스턴스 접속  
Within Systems Manager, selecting Session Manager allows us to start a session on the EC2 instance.  
Systems Manager에서 세션 매니저를 선택하면 EC2 인스턴스에서 세션을 시작할 수 있습니다.  

Despite the security group having zero inbound rules, the session starts successfully, providing a secure shell without SSH access or keys.  
보안 그룹에 인바운드 규칙이 없더라도, SSH 접속이나 키 없이 안전한 셸이 정상적으로 시작됩니다.  

Commands such as ping google.com and hostname can be executed, confirming connectivity and instance identity.  
ping google.com, hostname 등의 명령어를 실행하여 연결성과 인스턴스 확인이 가능합니다.  

The private IP address matches the instance's network configuration, demonstrating direct access through Session Manager.  
인스턴스의 프라이빗 IP가 네트워크 구성과 일치하여 세션 매니저를 통한 직접 접속이 확인됩니다.  

---

## Summary of EC2 Instance Access Methods  
## EC2 인스턴스 접속 방법 요약  
There are three primary ways to access EC2 instances:  
EC2 인스턴스에 접속하는 주요 방법은 세 가지입니다:  

- SSH Access: Requires port 22 to be open and SSH keys to connect via terminal.  
- SSH 접속: 포트 22가 열려 있어야 하며, SSH 키로 터미널 접속 필요.  

- EC2 Instance Connect: Does not require permanent SSH keys but still needs port 22 open for temporary key upload.  
- EC2 Instance Connect: 영구 SSH 키는 필요 없지만, 임시 키 업로드를 위해 포트 22가 열려 있어야 합니다.  

- Session Manager: Requires no open inbound ports and uses an IAM role attached to the instance to enable secure shell access through the SSM service.  
- 세션 매니저: 인바운드 포트가 필요 없으며, IAM 역할을 통해 SSM 서비스로 안전한 셸 접속 가능.  

Session Manager provides enhanced security by eliminating the need to open port 22 and manage SSH keys.  
세션 매니저는 포트 22를 열거나 SSH 키를 관리할 필요가 없어 보안을 강화합니다.  

---

## Session Management and Logging  
## 세션 관리 및 로깅  
After completing the session, it can be terminated, and the session history is saved as logs.  
세션 종료 후, 세션 기록이 로그로 저장됩니다.  

These logs can be reviewed for auditing and security purposes, providing transparency and traceability for all actions performed during the session.  
이 로그는 감사 및 보안 목적으로 검토 가능하며, 세션 동안 수행된 모든 작업의 투명성과 추적성을 제공합니다.  

---

## Conclusion  
## 결론  
This concludes the lecture on the SSM Session Manager feature.  
이것으로 SSM 세션 매니저 기능 강의를 마칩니다.  

Remember to terminate your EC2 instance after use to avoid unnecessary charges.  
사용 후 불필요한 비용을 방지하기 위해 EC2 인스턴스를 종료하는 것을 잊지 마세요.  

---

## Key Takeaways  
## 핵심 요약  
- The SSM Session Manager allows secure shell access to EC2 instances without SSH keys or open port 22.  
- SSM 세션 매니저는 SSH 키나 포트 22 없이 EC2 인스턴스에 안전하게 셸 접속을 제공합니다.  

- EC2 instances require an IAM role with Amazon SSM managed instance core policy to communicate with the SSM service.  
- EC2 인스턴스는 SSM 서비스와 통신을 위해 Amazon SSM 관리형 인스턴스 핵심 정책이 연결된 IAM 역할이 필요합니다.  

- Session Manager supports Linux, macOS, and Windows instances and can log session data to Amazon S3 or CloudWatch Logs.  
- 세션 매니저는 Linux, macOS, Windows 인스턴스를 지원하며, 세션 데이터를 S3 또는 CloudWatch Logs로 기록할 수 있습니다.  

- There are three methods to access EC2 instances: traditional SSH with port 22 open, EC2 Instance Connect requiring port 22, and Session Manager which requires no open inbound ports.  
- EC2 인스턴스 접속 방법은 세 가지: 포트 22를 여는 전통적 SSH, 포트 22 필요 EC2 Instance Connect, 인바운드 포트 필요 없는 세션 매니저.  

🎮 **보상: "보안 접속 전문가 레벨 1 뱃지" 획득!**
