# Route 53 - Creating Our First Records  
# Route 53 - 첫 번째 레코드 생성하기  

---

## Creating Our First Records in Route 53  
## Route 53에서 첫 번째 레코드 만들기  

Let's proceed to create our first DNS records in Route 53. I will navigate to my hosted zone, where I will create some simple records.  
이제 Route 53에서 첫 번째 DNS 레코드를 만들어봅시다. 저는 제 호스티드 존으로 이동하여 간단한 레코드를 생성할 것입니다.  

To create a record, click on the appropriate button. Here, you can specify a record name. For example, we want it to be test.stephanetheteacher.com. However, you can enter any name you prefer. This is how you create your domain names.  
레코드를 만들려면 해당 버튼을 클릭합니다. 여기서 레코드 이름을 지정할 수 있습니다. 예를 들어, test.stephanetheteacher.com으로 만들 수 있습니다. 하지만 원하는 이름을 입력해도 됩니다. 이렇게 도메인 이름을 생성할 수 있습니다.  

Next, specify the record type. There are many record types available, but for now, we will keep it simple and select an A record. An A record routes an IPv4 address to a domain name.  
다음으로 레코드 유형을 지정합니다. 여러 유형이 있지만, 여기서는 간단히 A 레코드를 선택합니다. A 레코드는 IPv4 주소를 도메인 이름에 연결합니다.  

The value for this record will be 11.22.33.44. This is just a sample IP address; it is not an IP we own currently. Later, we will route to a real EC2 instance.  
레코드 값은 11.22.33.44로 설정합니다. 이는 샘플 IP 주소이며 실제 우리가 소유한 IP가 아닙니다. 나중에 실제 EC2 인스턴스로 라우팅할 것입니다.  

The TTL (Time To Live) is set to 300 seconds by default. We will leave it as is for now. The routing policy will also be left as simple routing, which we will explore in more detail later.  
TTL(Time To Live)은 기본값인 300초로 설정되어 있습니다. 그대로 두겠습니다. 라우팅 정책도 기본값인 단순 라우팅으로 설정하며, 나중에 자세히 다룰 예정입니다.  

Let's go ahead and create this record. The record has been successfully created.  
이제 레코드를 생성합니다. 성공적으로 생성되었습니다.  

The idea is that if you query test.stephanetheteacher.com, the hosted zone will respond with the value 11.22.33.44. If you try to access this URL in a web browser, it will not display anything because there is no server currently running at that IP address.  
즉, test.stephanetheteacher.com을 질의하면 호스티드 존이 11.22.33.44 값을 반환합니다. 다만 웹 브라우저에서 이 주소를 열면 해당 IP에 서버가 없기 때문에 아무것도 표시되지 않습니다.  

To understand what is happening behind the scenes, we will use command line tools. You can use your command line on Windows or Mac, but to ensure everyone follows the same steps, I will demonstrate using AWS CloudShell.  
백그라운드에서 무슨 일이 일어나는지 이해하기 위해 명령줄 도구를 사용합니다. Windows에서는 CMD, Mac에서는 터미널을 사용할 수 있습니다. 모든 사람이 동일한 절차를 따르도록 AWS CloudShell을 예시로 사용하겠습니다.  

Open the AWS Management Console and launch CloudShell. CloudShell provides a standard Linux command line interface where you can run commands.  
AWS Management Console을 열고 CloudShell을 실행합니다. CloudShell은 표준 Linux 명령줄 인터페이스를 제공하며 여기서 명령을 실행할 수 있습니다.  

On Windows, the nslookup command works, and on Mac, the dig command works. However, these commands are not installed by default in CloudShell, so we need to install them.  
Windows에서는 `nslookup`을, Mac에서는 `dig` 명령을 사용할 수 있습니다. 하지만 CloudShell에는 기본 설치되어 있지 않으므로 직접 설치해야 합니다.  

Run the following command to install the necessary utilities:  
다음 명령어로 필요한 유틸리티를 설치합니다:  

```bash
sudo yum install -y bind-utils
````

This installs both nslookup and dig commands in CloudShell.
이 명령은 CloudShell에 nslookup과 dig을 모두 설치합니다.

Clear the screen and run the following command to query your DNS record:
화면을 정리하고 다음 명령어로 DNS 레코드를 질의합니다:

```bash
nslookup test.stephanetheteacher.com
```

You should see a response indicating that test.stephanetheteacher.com resolves to 11.22.33.44, which matches the record you created.
결과에서 test.stephanetheteacher.com이 11.22.33.44로 해석된다는 응답을 볼 수 있으며, 이는 우리가 생성한 레코드와 일치합니다.

Alternatively, you can use the dig command, which provides more detailed output including TTL and record type:
또는 `dig` 명령을 사용하여 TTL 및 레코드 유형 같은 더 자세한 정보를 확인할 수 있습니다:

```bash
dig test.stephanetheteacher.com
```

The output will include an ANSWER SECTION showing that test.stephanetheteacher.com is an A record with the value 11.22.33.44 and the TTL value.
출력에는 ANSWER SECTION이 포함되며, test.stephanetheteacher.com이 A 레코드임을 보여주고 값은 11.22.33.44, TTL 값도 표시됩니다.

In summary, we have created our first Route 53 record and verified it using terminal commands. Although loading it from a web browser does not work yet, we will set up a real server later to make it functional.
정리하자면, 우리는 첫 번째 Route 53 레코드를 생성하고 터미널 명령으로 검증했습니다. 브라우저에서는 아직 작동하지 않지만, 나중에 실제 서버를 설정해 기능하게 할 것입니다.

Thank you for following this lecture. I look forward to seeing you in the next one.
이번 강의를 따라와 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.

---

## Key Takeaways

## 핵심 정리

* Created a simple A record in Route 53 to map a domain name to an IPv4 address.

* Route 53에서 간단한 A 레코드를 생성하여 도메인 이름을 IPv4 주소에 매핑했습니다.

* Used AWS CloudShell to run DNS query commands such as nslookup and dig.

* AWS CloudShell을 사용해 nslookup과 dig 명령으로 DNS 질의를 실행했습니다.

* Installed necessary utilities (bind-utils) in CloudShell to enable DNS queries.

* CloudShell에 bind-utils를 설치해 DNS 질의 도구를 활성화했습니다.

* Verified DNS record resolution using command line tools, understanding TTL and record types.

* 명령줄 도구로 DNS 레코드 해석을 검증하고 TTL과 레코드 유형을 이해했습니다.

---

🎮 **게임 보상 지급**

* 경험치: **+280XP**
* 아이템: **"DNS Query Blade" ⚔️**
* 업적 달성: **"First Record Creator"** 🏆

