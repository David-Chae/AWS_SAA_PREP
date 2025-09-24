# SSH Troubleshooting  
# SSH 문제 해결  
👉 SSH 접속 시 발생할 수 있는 다양한 문제와 해결 방법 정리입니다.  

---

## 1) There's a connection timeout  
## 1) 연결 시간 초과 발생  

This is a security group issue. Any timeout (not just for SSH) is related to security groups or a firewall.  
이것은 **보안 그룹 문제**입니다. SSH뿐 아니라 모든 연결 시간 초과는 보안 그룹이나 방화벽과 관련이 있습니다.  

Ensure your security group looks like this and correctly assigned to your EC2 instance.  
보안 그룹이 올바르게 EC2 인스턴스에 할당되어 있는지 확인하세요.  

---

## 2) There's still a connection timeout issue  
## 2) 여전히 연결 시간 초과 문제 발생  

If your security group is properly configured as above, and you still have connection timeout issues, then that means a corporate firewall or a personal firewall is blocking the connection.  
보안 그룹이 올바르게 설정되어 있음에도 연결이 안 되면, 회사 방화벽이나 개인 방화벽이 연결을 차단하고 있다는 의미입니다.  

Please use EC2 Instance Connect as described in the next lecture.  
다음 강의에서 설명된 **EC2 Instance Connect**를 사용하세요.  

---

## 3) SSH does not work on Windows  
## 3) Windows에서 SSH가 작동하지 않음  

If it says: ssh command not found, that means you have to use Putty  
"ssh command not found"가 뜨면 **Putty를 사용**해야 합니다.  

Follow again the video. If things don't work, please use EC2 Instance Connect as described in the next lecture.  
영상 강의를 다시 따라하세요. 그래도 안 되면 다음 강의에서 설명된 **EC2 Instance Connect**를 사용하세요.  

---

## 4) There's a connection refused  
## 4) 연결 거부(Connection Refused) 발생  

This means the instance is reachable, but no SSH utility is running on the instance.  
이는 인스턴스에 도달할 수 있지만, SSH 서비스가 실행되고 있지 않다는 의미입니다.  

Try to restart the instance.  
인스턴스를 **재시작**해보세요.  

If it doesn't work, terminate the instance and create a new one. Make sure you're using Amazon Linux 2.  
재시작해도 안 되면, 인스턴스를 삭제 후 새로 생성하세요. **Amazon Linux 2**를 사용해야 합니다.  

---

## 5) Permission denied (publickey,gssapi-keyex,gssapi-with-mic)  
## 5) 권한 거부(Permission denied) 오류  

This means either two things:  
이는 두 가지 중 하나를 의미합니다:  

1. You are using the wrong security key or not using a security key. Please look at your EC2 instance configuration to make sure you have assigned the correct key to it.  
   잘못된 키를 사용하거나 키를 사용하지 않았습니다. EC2 인스턴스에 올바른 키가 할당되었는지 확인하세요.  

2. You are using the wrong user. Make sure you have started an Amazon Linux 2 EC2 instance, and make sure you're using the user `ec2-user`.  
   잘못된 사용자를 사용하고 있습니다. **Amazon Linux 2** EC2 인스턴스를 시작했는지, SSH 명령어나 Putty 설정에서 **ec2-user**를 사용했는지 확인하세요.  
   예: `ec2-user@<public-ip>` (ex: ec2-user@35.180.242.162)  

---

## 6) Nothing is working - "aaaahhhhhh"  
## 6) 아무것도 안 됨 - "aaaahhhhhh"  

Don't panic. Use EC2 Instance Connect from the next lecture.  
당황하지 마세요. 다음 강의에서 설명된 **EC2 Instance Connect**를 사용하세요.  

Make sure you started an Amazon Linux 2 and you will be able to follow along with the tutorial :)  
**Amazon Linux 2**를 시작했는지 확인하면 튜토리얼을 따라갈 수 있습니다.  

---

## 7) I was able to connect yesterday, but today I can't  
## 7) 어제는 접속됐는데 오늘은 안 됨  

This is probably because you have stopped your EC2 instance and then started it again today.  
이는 아마 EC2 인스턴스를 **중지 후 재시작**했기 때문일 가능성이 큽니다.  

When you do so, the public IP of your EC2 instance will change.  
인스턴스를 재시작하면 **퍼블릭 IP가 변경**됩니다.  

Therefore, in your command, or Putty configuration, please make sure to edit and save the new public IP.  
따라서 SSH 명령어나 Putty 설정에서 **새 퍼블릭 IP를 수정하고 저장**해야 합니다.  

---

## Happy troubleshooting!  
## 즐거운 문제 해결 되세요!  

Stephane  

🎮 **게임 보상**: "SSH 수호자" 칭호 획득!  
👉 이제 대부분의 SSH 문제를 스스로 해결할 수 있습니다. 🚀  
