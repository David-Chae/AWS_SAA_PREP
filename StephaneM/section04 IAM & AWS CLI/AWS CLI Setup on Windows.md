
# AWS CLI Setup on Windows  
# Windows에서 AWS CLI 설정하기  
→ Windows 환경에서 AWS CLI v2를 설치, 검증, 업그레이드하는 과정을 설명합니다.  
🎮 게임보상: 이 섹션을 끝까지 읽으면 **[설치 마스터 배지 🏅]** 획득!  

---

## Installing AWS CLI on Windows  
## Windows에 AWS CLI 설치하기  
→ 설치 시작 단계입니다.  

To install the AWS Command Line Interface (CLI) on Windows, begin by searching for "aws CLI install windows" on Google. This search will provide a list of relevant links. The goal is to install AWS CLI version 2 on Windows, which is the latest version and ensures you are up to date.  
Windows에서 AWS 명령줄 인터페이스(CLI)를 설치하려면, 먼저 구글에서 "aws CLI install windows"를 검색하세요. 그러면 관련 링크들이 나옵니다. 최신 버전인 AWS CLI v2를 설치하는 것이 목표이며, 이를 통해 최신 환경을 유지할 수 있습니다.  
→ CLI v2는 최신 버전으로 안정성과 성능이 개선되었습니다.  
🎮 게임보상: 검색 완료 시 **[탐험가 포인트 +10]** 획득!  

Version 2 does not differ significantly from version 1; it mainly offers improved performance and additional capabilities. Importantly, the API remains exactly the same. Additionally, version 2 features an improved installer.  
버전 2는 버전 1과 크게 다르지 않으며, 주로 성능 향상과 추가 기능이 있습니다. 중요한 점은 API가 동일하게 유지된다는 것입니다. 또한 버전 2는 개선된 설치 프로그램을 제공합니다.  
→ 기존 학습 호환성 보장 + 설치 편의성 강화.  

Scroll down to the section titled "Install on Windows." Here, you can install the AWS CLI simply by using the MSI installer. Click on the provided link to download the MSI installer.  
"Install on Windows"라는 섹션까지 스크롤하세요. 여기서 MSI 설치 프로그램을 통해 간단히 설치할 수 있습니다. 제공된 링크를 클릭해 MSI 설치 프로그램을 다운로드하세요.  
→ MSI 설치 파일은 Windows에서 표준 설치 방식입니다.  

After downloading, run the installer. The installation process is straightforward. When the installer starts, click "Next," accept the terms of the license agreement, and click "Next" again. Then click "Install" and wait for the installation to complete.  
다운로드 후 설치 프로그램을 실행하세요. 설치 과정은 간단합니다. "Next"를 클릭하고, 라이선스 동의에 체크 후 다시 "Next"를 클릭하세요. 그런 다음 "Install"을 눌러 설치가 완료될 때까지 기다립니다.  
→ Windows 소프트웨어 설치와 동일한 절차.  

If prompted by Windows, allow the installer to make changes to your device. Once the installation is complete, click "Finish."  
Windows에서 권한 요청이 나오면 설치 프로그램이 장치 변경을 허용하도록 승인하세요. 설치가 끝나면 "Finish"를 클릭합니다.  
→ 설치 마무리 단계.  
🎮 게임보상: 설치 완료 시 **[세팅 완료 EXP +50]** 획득!  

---

## Verifying the AWS CLI Installation  
## AWS CLI 설치 확인하기  
→ 설치가 잘 되었는지 검증하는 단계입니다.  

To confirm that the AWS CLI is properly installed, open the Command Prompt on Windows. You can do this by searching for "Command Prompt" and opening it.  
AWS CLI가 정상적으로 설치되었는지 확인하려면 Windows에서 명령 프롬프트를 엽니다. "Command Prompt"를 검색하여 실행하세요.  
→ CLI 설치 확인은 CMD 실행부터 시작합니다.  

In the Command Prompt, type the following command and press Enter:  
명령 프롬프트에 다음 명령어를 입력하고 Enter를 누르세요:  

```

aws --version

```

If the installation was successful, you will see output similar to this:  
설치가 성공했다면 아래와 같은 출력이 나타납니다:  

```

aws-cli/2.x.x Python/3.x.x Windows/10

```

This output indicates that your AWS CLI version 2 is properly installed on Windows and ready for use.  
이 출력은 AWS CLI v2가 정상적으로 설치되었으며 Windows에서 사용할 준비가 되었음을 의미합니다.  
→ 설치 검증 성공!  
🎮 게임보상: 검증 성공 시 **[디버거 뱃지 🛡️]** 획득!  

---

## Upgrading AWS CLI on Windows  
## Windows에서 AWS CLI 업그레이드하기  
→ 최신 상태 유지 방법을 설명합니다.  

If you need to upgrade your AWS CLI, simply re-download the MSI installer from the official source and run it again. The installer will automatically upgrade your existing AWS CLI installation.  
AWS CLI를 업그레이드하려면, 공식 사이트에서 MSI 설치 프로그램을 다시 다운로드하고 실행하면 됩니다. 기존 설치는 자동으로 업그레이드됩니다.  
→ 재설치 = 업그레이드 방식.  

Once you see the version output as described earlier, you are ready to proceed with using the AWS CLI. You can continue following tutorials or lectures from this point onward.  
앞서 설명한 버전 출력이 나타나면 AWS CLI 사용 준비가 완료된 것입니다. 이제 튜토리얼이나 강의를 계속 따라가면 됩니다.  
→ 최신 버전 확인 후 학습 이어가기.  
🎮 게임보상: 업그레이드 완료 시 **[레벨업 +1 🎉]** 획득!  

---

## Key Takeaways  
## 핵심 요약  
→ 설치 과정 전체를 정리합니다.  

- The AWS CLI version 2 for Windows can be installed using the MSI installer.  
- Windows에서 AWS CLI v2는 MSI 설치 프로그램으로 설치할 수 있습니다.  
→ 간단한 설치 방법.  

- Version 2 offers improved performance and capabilities while maintaining the same API as version 1.  
- 버전 2는 성능과 기능이 향상되었지만 API는 버전 1과 동일합니다.  
→ 호환성 보장.  

- After installation, verifying the AWS CLI version via the command prompt confirms a successful setup.  
- 설치 후 명령 프롬프트에서 버전을 확인하면 성공적으로 설치되었음을 알 수 있습니다.  
→ 검증 필수.  

- Upgrading the AWS CLI on Windows involves re-downloading and running the MSI installer again.  
- Windows에서 AWS CLI 업그레이드는 MSI 설치 파일을 다시 다운로드하고 실행하면 됩니다.  
→ 업그레이드도 간단.  
🎮 최종 보상: 모든 단계 완료 시 **[AWS CLI 설치 챔피언 트로피 🏆]** 획득!  
