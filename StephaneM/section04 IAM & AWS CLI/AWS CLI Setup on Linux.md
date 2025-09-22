````markdown
# AWS CLI Setup on Linux  
AWS CLI 리눅스 설치하기  
→ 리눅스 환경에서 AWS CLI를 설치하는 방법을 설명합니다.  

---

## Installing AWS CLI Version 2 on Linux  
리눅스에 AWS CLI 버전 2 설치하기  
→ 최신 버전인 AWS CLI v2를 리눅스에 설치하는 절차입니다.  

---

To install the AWS CLI on Linux, start by searching for the official installation instructions for AWS CLI Version 2, which is the latest version available.  
리눅스에 AWS CLI를 설치하려면, 먼저 공식 문서에서 제공하는 AWS CLI v2 설치 지침을 확인합니다.  
→ 항상 최신 버전을 설치해야 하므로 공식 문서를 참고하는 것이 중요합니다.  

---

The installation process involves running three main commands:  
설치 과정은 크게 세 가지 명령어로 진행됩니다.  
→ 다운로드, 압축 해제, 설치 실행 세 단계입니다.  

- Download the AWS CLI installer zip file.  
  AWS CLI 설치 프로그램(zip 파일) 다운로드  
  → 먼저 설치 파일을 가져옵니다.  

- Unzip the downloaded installer.  
  다운로드한 설치 파일 압축 해제  
  → 압축을 풀어 설치 준비를 합니다.  

- Run the installer with root privileges.  
  루트 권한으로 설치 실행  
  → 관리자 권한으로 설치해야 정상 적용됩니다.  

---

### bash Code Sample  
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
````

설치 파일 다운로드 명령어
→ 인터넷에서 AWS CLI zip 파일을 받아옵니다.

---

After copying the download command, open a terminal and paste it to download the installer zip file. The download will begin immediately.
명령어를 복사하여 터미널에 붙여넣으면 즉시 다운로드가 시작됩니다.
→ 인터넷 연결이 필요합니다.

---

### bash Code Sample

```bash
unzip awscliv2.zip
```

압축 해제 명령어
→ zip 파일을 풀어 설치 파일을 준비합니다.

---

Next, unzip the installer by running the unzip command in the terminal. This will extract the installer files.
터미널에서 `unzip` 명령어를 실행하면 설치 파일이 풀립니다.
→ 설치 실행 파일이 생성됩니다.

---

### bash Code Sample

```bash
sudo ./aws/install
```

루트 권한으로 설치 실행
→ `sudo`를 사용하여 관리자 권한으로 설치합니다.

---

Finally, run the installer with root privileges using sudo. You will be prompted to enter your password. After entering it, the installation will proceed.
마지막으로 `sudo` 명령어로 설치를 실행합니다. 암호 입력 후 설치가 진행됩니다.
→ 관리자 인증이 필요한 단계입니다.

---

To verify the installation, you can run the following command:
설치가 정상적으로 되었는지 확인하려면 아래 명령어를 실행합니다.
→ 버전 확인은 설치 검증의 핵심입니다.

### bash Code Sample

```bash
/usr/local/bin/aws --version
```

절대 경로를 이용한 설치 확인
→ 정확한 실행 경로를 지정하여 버전을 확인합니다.

---

Alternatively, if /usr/local/bin is included in your system's PATH environment variable, you can simply run:
만약 `/usr/local/bin`이 환경 변수 PATH에 포함되어 있다면, 단순히 다음처럼 실행할 수 있습니다.
→ 보통 기본 환경에 설정되어 있어서 짧게 실행 가능합니다.

### bash Code Sample

```bash
aws --version
```

PATH 설정이 되어 있을 때 버전 확인
→ 간단하게 `aws --version` 만 입력해도 됩니다.

---

The output will display the installed AWS CLI version, for example, aws-cli/2.x.x Python/3.x.x Linux/ followed by the Botocore version, confirming a successful installation.
출력값에 설치된 AWS CLI 버전, Python 버전, Botocore 버전이 표시되면 성공적으로 설치된 것입니다.
→ 예시: `aws-cli/2.15.10 Python/3.11.6 Linux/ Botocore/2.16.10`

---

Once the AWS CLI is installed and verified, you can proceed to run any AWS CLI commands as needed for your projects or further lectures.
설치와 검증이 끝나면, AWS CLI 명령어를 프로젝트나 학습에 활용할 수 있습니다.
→ 실습이나 실제 업무에 바로 적용 가능합니다.

---

If you encounter any issues during installation, refer to the official AWS documentation or troubleshooting guide to resolve them.
설치 중 문제가 발생하면, 공식 AWS 문서나 문제 해결 가이드를 참고하세요.
→ 대부분의 오류는 공식 문서에 해결책이 나와 있습니다.

---

## Key Takeaways

핵심 요약
→ 설치 과정을 간단히 정리합니다.

* Installed AWS CLI Version 2 on Linux using official commands.
  공식 명령어로 리눅스에 AWS CLI v2 설치 완료
  → 안전하고 표준적인 방법입니다.

* Downloaded the installer zip file, unzipped it, and ran the installer with root privileges.
  설치 파일 다운로드 → 압축 해제 → 루트 권한 실행
  → 설치 순서 핵심 3단계입니다.

* Verified the installation by checking the AWS CLI version.
  설치 후 버전 확인으로 검증 완료
  → 확인은 필수입니다.

* Ensured the AWS CLI executable is in the system path for easy access.
  시스템 PATH 환경 변수에 추가하여 쉽게 실행 가능
  → 환경 설정으로 편리성 확보.

---

🎮 **게임 보상:**

* AWS 설치 경험치 +50
* 리눅스 명령어 숙련도 +30
* 클라우드 관리 능력 +20
  → 🌟 “리눅스 클라우드 초심자” 칭호 획득!

```
