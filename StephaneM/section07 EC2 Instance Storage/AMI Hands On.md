# AMI Hands On  
# AMI 실습  

Let's proceed to practice using AMI.  
AMI를 활용한 실습을 진행해보겠습니다.  

I will launch an instance and navigate into this new experience.  
인스턴스를 시작하고 새로운 실습 환경으로 이동합니다.  

I will scroll down and select Amazon Linux 2 as the operating system.  
스크롤하여 운영체제로 Amazon Linux 2를 선택합니다.  

Next, I scroll down again and choose the t2.micro instance type.  
다시 스크롤하여 인스턴스 유형으로 t2.micro를 선택합니다.  

I select the 'easy to draw' key pair, although the choice does not significantly matter here.  
'Easy to draw' 키 페어를 선택합니다. 여기서는 선택이 크게 중요하지 않습니다.  

Scrolling down further, I edit the network settings and select an existing security group named 'launch wizard one' from before.  
더 아래로 스크롤하여 네트워크 설정을 수정하고, 이전에 만든 'launch wizard one' 보안 그룹을 선택합니다.  

The storage settings remain the same. In advanced details, I scroll down to the user data section.  
스토리지 설정은 그대로 두고, 고급 세부 설정에서 사용자 데이터(User Data) 섹션으로 스크롤합니다.  

Here, I copy all the user data script lines except the last one.  
여기서 마지막 줄을 제외한 모든 사용자 데이터 스크립트를 복사합니다.  

The first four lines of the script install HTTPD, which is the Apache web server.  
스크립트의 첫 4줄은 Apache 웹 서버(HTTPD)를 설치합니다.  

The last line creates an index file, but currently, we do not want to create the index file because we intend to create an AMI from this instance.  
마지막 줄은 인덱스 파일을 생성하지만, 현재는 AMI를 생성할 예정이므로 인덱스 파일은 만들지 않습니다.  

Therefore, we copy everything except the last systemctl command line.  
따라서 마지막 systemctl 명령어 줄을 제외한 나머지를 복사합니다.  

After setting this up, we launch the instance.  
이 설정 후 인스턴스를 시작합니다.  

Once the instance is launched, it will run the EC2 user data script to install the Apache web server.  
인스턴스가 시작되면 EC2 사용자 데이터 스크립트를 실행하여 Apache 웹 서버를 설치합니다.  

If you try to access the public IPv4 address immediately, it will not work and will result in a connection error because the script has not finished running yet.  
스크립트 실행이 완료되기 전에 공용 IPv4 주소에 접속하면 연결 오류가 발생합니다.  

Make sure to use the HTTP protocol when accessing the address, but be patient as it may take a minute or two for the script to complete.  
접속 시 HTTP 프로토콜을 사용하고, 스크립트 완료까지 1~2분 정도 기다립니다.  

After waiting approximately two minutes, refreshing the page will display the default Apache web server test page.  
약 2분 후 페이지를 새로고침하면 Apache 기본 테스트 페이지가 표시됩니다.  

Now that the Apache server is running, we proceed to create an AMI to save the state of this EC2 instance for reuse.  
Apache 서버가 실행 중이므로, EC2 상태를 저장하기 위해 AMI를 생성합니다.  

Right-click the instance, select 'Image and templates', then choose 'Create image'.  
인스턴스를 우클릭하고 'Image and templates' → 'Create image'를 선택합니다.  

Name the image 'demo image' and keep the default settings before clicking 'Create image'.  
이미지 이름을 'demo image'로 설정하고, 기본값을 유지한 채 'Create image'를 클릭합니다.  

The AMI creation process begins, and you can monitor its status by navigating to the AMIs section on the left-hand side.  
AMI 생성이 시작되며, 왼쪽 AMIs 섹션에서 상태를 확인할 수 있습니다.  

Initially, the status will be 'pending' while the AMI is being created.  
처음에는 AMI 생성 중 'pending' 상태로 표시됩니다.  

Once the AMI status changes to 'available', it is ready for use.  
AMI 상태가 'available'로 변경되면 사용 준비가 완료된 것입니다.  

You can launch new instances from this AMI by selecting it and clicking 'Launch'.  
이 AMI를 선택하고 'Launch'를 클릭하면 새 인스턴스를 시작할 수 있습니다.  

Alternatively, during instance creation, you can choose the 'From AMI' option and select your custom AMI from the 'My AMIs' tab.  
또는 인스턴스 생성 시 'From AMI' 옵션을 선택하고 'My AMIs' 탭에서 커스텀 AMI를 선택할 수 있습니다.  

Select the 'demo image' AMI you created earlier.  
앞서 생성한 'demo image' AMI를 선택합니다.  

Scroll down to configure key pair and network settings as desired, selecting the existing 'launch wizard one' security group again.  
스크롤하여 키 페어와 네트워크 설정을 구성하고, 기존 'launch wizard one' 보안 그룹을 다시 선택합니다.  

In the advanced section at the bottom, enter user data consisting of the first three lines of the original script and the last line that echoes the new index file.  
고급 설정에서 원본 스크립트 첫 3줄과 새로운 인덱스 파일을 만드는 마지막 줄을 사용자 데이터로 입력합니다.  

This user data writes a new index file without reinstalling HTTPD, since the AMI already contains the Apache web server.  
AMI에 이미 Apache 서버가 포함되어 있으므로, HTTPD를 재설치하지 않고 새로운 인덱스 파일만 생성합니다.  

Launching the instance from the AMI results in a much faster boot-up time because HTTPD installation is not repeated.  
AMI에서 인스턴스를 실행하면 HTTPD 설치가 반복되지 않아 부팅 시간이 훨씬 빨라집니다.  

Once the instance is running, access its public IP address to see the 'Hello World' message from the new index file.  
인스턴스가 실행되면 공용 IP로 접속해 새 인덱스 파일의 'Hello World' 메시지를 확인합니다.  

This demonstrates the power of AMIs for packaging pre-installed software and speeding up instance deployment.  
AMI를 통해 사전 설치된 소프트웨어를 패키징하고 인스턴스 배포 속도를 높일 수 있음을 보여줍니다.  

You can imagine using AMIs to include security software or other prerequisite applications that take time to install, then quickly launch instances from the AMI with minimal additional setup.  
설치 시간이 오래 걸리는 보안 소프트웨어나 필수 애플리케이션을 AMI에 포함시키고, 최소한의 추가 설정으로 빠르게 인스턴스를 실행할 수 있습니다.  

To conclude, terminate the two instances you created to avoid unnecessary charges.  
마지막으로, 불필요한 비용을 방지하기 위해 생성한 두 인스턴스를 종료합니다.  

That concludes this demonstration.  
이로써 실습 시연을 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

- Launched an EC2 instance using Amazon Linux 2 and configured it with Apache HTTPD server.  
- Amazon Linux 2로 EC2 인스턴스를 실행하고 Apache HTTPD 서버를 설정했습니다.  

- Created an AMI from the configured instance to save its state for faster future deployments.  
- 설정된 인스턴스로부터 AMI를 생성하여 상태를 저장하고, 향후 배포 속도를 높였습니다.  

- Demonstrated launching new instances from the created AMI, significantly reducing setup time.  
- 생성된 AMI에서 새 인스턴스를 실행하여 설정 시간을 크게 줄였습니다.  

- Highlighted the benefits of AMIs for packaging pre-installed software and speeding up instance boot-up.  
- 사전 설치된 소프트웨어 패키징과 인스턴스 부팅 속도 향상이라는 AMI의 장점을 강조했습니다.  
