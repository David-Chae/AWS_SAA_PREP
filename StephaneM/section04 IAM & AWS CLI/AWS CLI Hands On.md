````markdown
# AWS CLI Hands On  
AWS CLI 실습  
→ AWS CLI 사용을 위한 기본 실습을 다룹니다.  

---

## Creating Access Keys  
액세스 키 생성하기  
→ CLI에서 사용할 액세스 키를 만드는 단계입니다.  

To create access keys, click on your username, then navigate to Security credentials. Scroll down to the section for access keys and initiate the creation of a new access key.  
액세스 키를 만들려면 사용자 이름을 클릭하고, **보안 자격 증명(Security credentials)** 메뉴로 이동합니다. 액세스 키 섹션까지 스크롤을 내린 뒤 새 액세스 키 생성(Create new access key)을 실행합니다.  
→ AWS CLI에서 로그인할 때 필요한 키를 생성하는 절차입니다.  

---

Based on your selection, AWS provides recommendations. For example, if you want an access key for the CLI, AWS suggests alternatives such as using CloudShell or the CLI V2 with authentication through the IAM Identity Center. These options are more secure and will be demonstrated in subsequent lectures.  
선택한 항목에 따라 AWS는 권장 사항을 제시합니다. 예를 들어, CLI를 사용하기 위해 액세스 키를 만들려 하면, AWS는 대신 **CloudShell** 또는 **IAM Identity Center 인증**을 사용하는 CLI V2를 권장합니다. 이러한 방법은 더 안전하며 이후 강의에서 다루게 됩니다.  
→ 단순 액세스 키보다는 보안성이 높은 대안을 권장합니다.  

---

For now, we will proceed with creating an access key for the CLI. Confirm that you understand the recommendations by selecting the appropriate checkbox, then create the access key. Remember, this is the only time you will be able to view the access key and secret access key.  
지금은 실습을 위해 CLI용 액세스 키를 직접 생성합니다. 권장 사항을 이해했다는 확인란을 체크한 후 키를 생성하세요. 이때 **액세스 키와 시크릿 키는 처음 한 번만 볼 수 있습니다**.  
→ 시크릿 키는 보안 때문에 다시 확인 불가, 반드시 안전하게 저장해야 합니다.  

---

## Configuring AWS CLI  
AWS CLI 설정하기  
→ CLI에 액세스 키를 등록하는 과정입니다.  

To configure the AWS CLI, open your terminal and type:  
AWS CLI를 설정하려면 터미널을 열고 아래 명령어를 입력합니다:  

```bash
aws configure
````

→ `aws configure` 명령어를 실행하면 설정 단계로 들어갑니다.

---

You will be prompted to enter your access key ID, secret access key, default region name, and default output format.
프로그램은 차례대로 액세스 키 ID, 시크릿 키, 기본 리전 이름, 기본 출력 형식을 입력하라고 요청합니다.
→ CLI가 AWS와 연결되는 데 필요한 네 가지 정보를 설정하는 과정입니다.

---

Enter your access key ID and press Enter. Then enter your secret access key and press Enter. For the default region name, choose the region closest to you, for example, eu-west-1. You can find region codes from the AWS Management Console dropdown menu. Press Enter to accept the default output format.
액세스 키 ID 입력 후 Enter, 시크릿 키 입력 후 Enter를 누릅니다. 기본 리전은 가까운 지역(예: `eu-west-1`)을 선택하세요. 리전 코드는 AWS 콘솔 드롭다운 메뉴에서 확인할 수 있습니다. 출력 형식은 기본값으로 Enter를 눌러도 됩니다.
→ 리전(region) 선택은 서비스 지연과 요금에 직접적인 영향을 줍니다.

---

Once configured, you can verify your setup by listing IAM users with the command:
설정이 완료되면 아래 명령어로 IAM 사용자 목록을 확인하여 정상 동작을 검증할 수 있습니다:

```bash
aws iam list-users
```

→ IAM 사용자 정보가 출력되면 설정 성공입니다.

---

This command will display all users in your AWS account, including details such as UserId, ARN, creation date, and last password usage.
해당 명령어는 UserId, ARN, 생성일, 마지막 비밀번호 사용일 등 AWS 계정에 속한 모든 사용자 정보를 보여줍니다.
→ CLI가 정상적으로 IAM과 연결된 상태를 의미합니다.

---

## Managing User Permissions

사용자 권한 관리
→ CLI 및 콘솔에서 권한 제어는 동일하게 적용됩니다.

If you remove permissions from a user, such as removing the user from an admin group, the user will no longer have access rights. This applies both in the Management Console and when using the CLI.
사용자를 관리자 그룹(admin group)에서 제거하면 더 이상 권한이 없습니다. 이 원칙은 콘솔과 CLI 모두에 적용됩니다.
→ 권한은 인터페이스와 상관없이 동일하게 강제됩니다.

---

For example, after removing the user from the admin group, attempting to list users via the CLI will result in no response due to permission denial. Similarly, the Management Console will display an error indicating insufficient permissions.
예를 들어 관리 그룹에서 사용자를 제거하면, CLI에서 사용자 목록을 보려 해도 권한 거부로 응답이 없습니다. 콘솔에서도 "권한 부족" 오류 메시지가 표시됩니다.
→ 실습 후 권한을 반드시 되돌려야 합니다.

---

## Summary

요약
→ 전체 과정을 다시 정리합니다.

You can access AWS either through the Management Console or by configuring access keys for use with the AWS CLI. Permissions are enforced consistently across both interfaces. Always remember to restore user permissions after testing to avoid access issues.
AWS 접근 방식은 **Management Console** 또는 **CLI(액세스 키 설정)** 두 가지가 있습니다. 권한은 두 인터페이스에서 동일하게 적용됩니다. 테스트 후에는 반드시 권한을 원래대로 복원해야 합니다.
→ 권한 복원하지 않으면 계정 접근이 제한될 수 있습니다.

---

To restore permissions, add your user back into the appropriate group, such as the admin group, to regain administrator access.
권한을 되돌리려면 해당 사용자를 관리자 그룹(admin group) 같은 적절한 그룹에 다시 추가하면 됩니다.
→ 관리 권한은 그룹 단위로 쉽게 복원됩니다.

---

## Key Takeaways

핵심 요약
→ 반드시 기억해야 할 사항입니다.

* Access keys can be created via the AWS Management Console under Security Credentials.
  액세스 키는 AWS 콘솔의 **보안 자격 증명** 메뉴에서 생성 가능
  → CLI 접속 준비 단계

* AWS recommends using CloudShell or IAM Identity Center for CLI authentication over access keys.
  AWS는 액세스 키 대신 **CloudShell** 또는 **IAM Identity Center 인증** 사용을 권장
  → 보안성이 더 높음

* AWS CLI is configured using `aws configure` with access key ID, secret access key, and region.
  `aws configure` 명령어로 액세스 키 ID, 시크릿 키, 리전을 설정
  → CLI 연결 핵심 설정 과정

* Permissions removed from a user affect both the Management Console and CLI access consistently.
  사용자 권한 제거는 콘솔과 CLI 모두에서 동일하게 적용됨
  → 권한 제어는 일관적임

---

🎮 **게임 보상:**

* AWS 보안 지식 +40
* IAM 권한 이해도 +30
* CLI 실습 경험치 +50
  → 🏆 “AWS 초급 관리자” 칭호 획득!

```
