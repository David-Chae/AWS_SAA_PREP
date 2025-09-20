```markdown
# IAM Users & Groups Hands On  
# IAM 사용자 및 그룹 실습  
→ IAM 실습 강의 시작. 사용자를 생성하고 그룹과 권한을 설정하는 과정입니다.  

## Introduction to IAM Users  
## IAM 사용자 소개  
→ IAM 사용자를 만드는 실습 안내.  

Let's begin by practicing how to use the IAM service to create users in AWS.  
이제 IAM 서비스를 사용하여 AWS에서 사용자를 생성하는 방법을 실습해보겠습니다.  
→ 직접 실습을 통해 개념 이해 강화.  

To start, type "IAM" in the search bar and navigate to the IAM console.  
먼저 검색창에 "IAM"을 입력하고 IAM 콘솔로 이동합니다.  
→ AWS 콘솔 탐색 방법 안내.  

Upon arriving at the IAM Dashboard, you will notice some security recommendations which we will not focus on for now.  
IAM 대시보드에 도착하면 몇 가지 보안 권장 사항이 보이지만, 지금은 신경 쓰지 않습니다.  
→ 초점은 사용자 생성에 맞춤.  

Instead, direct your attention to the left-hand side where you will find the "Users" section. This is where we create IAM users.  
대신 왼쪽 메뉴의 "Users" 섹션에 주목합니다. 여기서 IAM 사용자를 생성합니다.  
→ 사용자 생성 위치 안내.  

---

## IAM as a Global Service  
## IAM은 글로벌 서비스  
→ IAM이 전역 서비스임을 설명.  

Notice that in the top right corner, the region selection is inactive.  
오른쪽 상단의 리전 선택이 비활성화된 것을 확인하세요.  
→ IAM은 지역에 구애받지 않음.  

This indicates that IAM is a global service, so there is no region to select.  
이는 IAM이 글로벌 서비스라는 것을 의미하며, 선택할 리전이 없습니다.  
→ 전역적으로 사용자 관리 가능.  

When you create a user in IAM, it will be available everywhere.  
IAM에서 사용자를 만들면 모든 리전에서 사용 가능합니다.  
→ 글로벌 접근 가능.  

This contrasts with some other AWS services that are region-specific.  
일부 다른 AWS 서비스는 특정 리전에 종속되는 것과 대조됩니다.  
→ 리전별 서비스 vs 글로벌 서비스 차이.  

---

## Why Create IAM Users?  
## 왜 IAM 사용자를 만드는가?  
→ 루트 계정 사용 제한과 권한 관리 이유.  

Currently, you are using the root user, which is identified by the account ID.  
현재 계정 ID로 식별되는 루트 사용자를 사용하고 있습니다.  
→ 루트 계정 사용 중임 안내.  

It is not best practice to use the root account for everyday tasks.  
루트 계정을 일상적인 작업에 사용하는 것은 권장되지 않습니다.  
→ 보안 관점에서 권장되지 않음.  

Therefore, we create IAM users, such as admin users, to manage accounts more securely.  
따라서 관리 계정(admin)과 같은 IAM 사용자를 만들어 보다 안전하게 계정을 관리합니다.  
→ 안전한 권한 분리 실습 목적.  

---

## Creating an IAM User  
## IAM 사용자 생성  
→ IAM 사용자 생성 단계 안내.  

Let's create a user. Provide a username, for example, "Stephane".  
사용자를 생성해봅시다. 예시로 사용자명을 "Stephane"으로 입력합니다.  
→ 사용자 계정 생성 과정 실습.  

We want to grant this user access to the management console, so select that option.  
이 사용자에게 관리 콘솔 접근 권한을 부여하고 싶으므로 해당 옵션을 선택합니다.  
→ 콘솔 접근 권한 부여 방법 안내.  

You have two options for user creation: using the Identity Center, which is recommended, or creating an IAM user.  
사용자 생성 방법은 두 가지가 있습니다. 권장되는 Identity Center 사용 또는 IAM 사용자 생성.  
→ 실습 및 시험 대비 IAM 사용자 선택.  

For simplicity and exam purposes, choose to create an IAM user.  
단순성과 시험 목적을 위해 IAM 사용자 생성을 선택합니다.  
→ 실습 편의상 단일 방법 선택.  

---

## Setting the Password  
## 비밀번호 설정  
→ 사용자 비밀번호 설정 단계.  

Set the password for the user.  
사용자의 비밀번호를 설정합니다.  
→ 로그인 인증 정보 설정.  

If this user was someone else, you might leave the password auto-generated and require the user to change it at next sign-in.  
다른 사용자의 경우, 비밀번호를 자동 생성하고 다음 로그인 시 변경하도록 요구할 수 있습니다.  
→ 보안 모범 사례 안내.  

Since this is your own user, enter a custom password and untick the option to require a password change at next login.  
이번 사용자는 자신의 계정이므로, 비밀번호를 직접 설정하고 다음 로그인 시 변경 요구 옵션을 해제합니다.  
→ 개인 사용자 실습 상황.  

---

## Assigning Permissions  
## 권한 부여  
→ 사용자에게 권한을 할당하는 단계.  

Next, add permissions to the user.  
다음으로 사용자에게 권한을 추가합니다.  
→ IAM 권한 연결.  

You can add permissions directly or start by creating groups.  
권한을 직접 추가하거나 그룹을 만들어 시작할 수 있습니다.  
→ 그룹 기반 권한 부여 안내.  

Let's create a group named "admin" and attach the "Administrator Access" policy to it.  
"admin" 그룹을 만들고 여기에 "Administrator Access" 정책을 연결합니다.  
→ 관리자 권한 그룹 생성 실습.  

Then add the user to this admin group.  
그런 다음 사용자를 이 admin 그룹에 추가합니다.  
→ 그룹 기반 권한 상속 확인.  

---

## Reviewing User Details  
## 사용자 세부 정보 확인  
→ 생성 완료 후 사용자 정보 검토 단계.  

Review the username, group permissions, and tags.  
사용자명, 그룹 권한, 태그를 검토합니다.  
→ 권한과 메타데이터 확인.  

Tags are optional metadata that can be added to AWS resources.  
태그는 선택적 메타데이터로 AWS 리소스에 추가할 수 있습니다.  
→ 관리 편의성을 위해 태그 활용 가능.  

For example, you could tag the user with a department such as "engineering".  
예를 들어, 사용자를 "engineering" 부서로 태그할 수 있습니다.  
→ 조직 관리 용도 예시.  

This is not mandatory but useful to know.  
필수는 아니지만 알아두면 유용합니다.  
→ 실무 팁 안내.  

The user is now created successfully. You can email signing instructions or download CSV files containing credentials.  
사용자가 성공적으로 생성되었습니다. 로그인 안내를 이메일로 보내거나 CSV 파일로 자격 증명을 다운로드할 수 있습니다.  
→ 생성 후 후속 조치 안내.  

Let's return to the user list to review all users.  
사용자 목록으로 돌아가 모든 사용자를 확인합니다.  
→ 전체 사용자 관리 확인.  

---

## Users and Groups Overview  
## 사용자 및 그룹 개요  
→ 생성된 사용자와 그룹 확인.  

Here is the user list, including the newly created user "Stephane."  
새로 생성한 "Stephane" 사용자를 포함한 사용자 목록입니다.  
→ 목록 확인.  

On the left, under "User Groups," you will see the "admins" group.  
왼쪽의 "User Groups"에서 "admins" 그룹을 확인할 수 있습니다.  
→ 그룹 위치 안내.  

This group contains the user "Stephane" and has the "Administrator Access" policy attached.  
이 그룹에는 "Stephane" 사용자가 포함되어 있으며 "Administrator Access" 정책이 연결되어 있습니다.  
→ 권한 상속 구조 이해.  

Looking at the permissions for the user "Stephane," you will see that administrative access is granted via the admin group, not directly attached.  
"Stephane" 사용자의 권한을 보면, 관리자 권한은 그룹을 통해 부여되고 직접 연결되지 않았음을 알 수 있습니다.  
→ 그룹 기반 권한 상속 원리.  

This means the user inherits permissions from the group, which simplifies permission management.  
사용자는 그룹에서 권한을 상속받으며, 권한 관리가 단순화됩니다.  
→ 실무 관리 효율성.  

---

## Signing in with the IAM User  
## IAM 사용자로 로그인  
→ 생성한 사용자로 로그인 과정 안내.  

Return to the dashboard and prepare to sign in with the IAM user "Stephane."  
대시보드로 돌아가 "Stephane" 사용자로 로그인 준비를 합니다.  
→ 로그인 실습 시작.  

Your AWS account has an account ID and a sign-in URL.  
AWS 계정에는 계정 ID와 로그인 URL이 있습니다.  
→ 로그인 정보 구조.  

You can customize this URL by creating an account alias, such as "aws-stephane-v3," which must be unique.  
계정 별칭(예: "aws-stephane-v3")을 만들어 로그인 URL을 맞춤 설정할 수 있으며, 고유해야 합니다.  
→ 사용자 편의 로그인 URL 생성.  

Using this alias simplifies the sign-in URL.  
이 별칭을 사용하면 로그인 URL이 간단해집니다.  
→ 접근 편의성 향상.  

To sign in with the "Stephane" account, you can use the same browser or open a new private browser window.  
"Stephane" 계정으로 로그인할 때 동일 브라우저 또는 새로운 프라이빗 브라우저 창을 사용합니다.  
→ 다중 세션 관리 방법.  

Using a private window allows you to have two AWS sessions side by side without being logged out of one when signing into the other.  
프라이빗 창을 사용하면 서로 다른 세션을 동시에 유지할 수 있습니다.  
→ 루트 계정과 IAM 사용자 동시 로그인 가능.  

Paste the sign-in URL into the private window. You will see the sign-in page for IAM users.  
프라이빗 창에 로그인 URL을 붙여넣으면 IAM 사용자 로그인 페이지가 나타납니다.  
→ 로그인 화면 확인.  

Enter the account ID or alias, then enter the username "Stephane" and the password you set earlier to sign in.  
계정 ID 또는 별칭, 사용자명 "Stephane", 설정한 비밀번호를 입력하여 로그인합니다.  
→ 실제 로그인 절차 안내.  

Once signed in, the top right corner will display the account ID and the IAM user name, confirming you are logged in as an IAM user.  
로그인 후 오른쪽 상단에 계정 ID와 IAM 사용자명이 표시됩니다.  
→ 로그인 상태 확인.  

In contrast, the root account window will only show the account ID.  
루트 계정 창과 비교하면 계정 ID만 표시됩니다.  
→ 루트 계정과 구분.  

---

## Important Recommendations  
## 중요 권장 사항  
→ 안전한 계정 관리 팁.  

Please ensure you do not lose your root account or admin login credentials.  
루트 계정 또는 관리자 로그인 정보를 잃지 않도록 주의하세요.  
→ 계정 분실 시 위험성 경고.  

Losing access could cause significant issues requiring AWS support.  
접근 권한을 잃으면 AWS 지원이 필요할 정도로 심각한 문제가 발생할 수 있습니다.  
→ 실무 사례 경고.  

For this course, it is recommended to use your IAM user rather than the root user.  
이 강의에서는 루트 계정 대신 IAM 사용자를 사용할 것을 권장합니다.  
→ 안전한 실습 환경 권장.  

Sometimes, the course will specify when to use the root account or an IAM user.  
강의 중 루트 계정 또는 IAM 사용자 사용 시점을 안내합니다.  
→ 필요 시 예외 안내.  

For the remainder of this section, keep both the root and IAM user windows open.  
이 섹션에서는 루트와 IAM 사용자 창을 모두 열어둡니다.  
→ 다음 강의 연결 준비.  

We will continue from here in the next lecture.  
다음 강의에서 여기서 계속 진행합니다.  
→ 실습 연속성 안내.  

---

## Key Takeaways  
## 핵심 요약  
→ IAM 사용자 실습 핵심 정리.  

- IAM is a global service in AWS, meaning users created are available across all regions.  
- IAM은 AWS에서 글로벌 서비스로, 생성된 사용자는 모든 리전에서 사용할 수 있습니다.  
→ 전역 사용자 관리 이해.  

- It is best practice to avoid using the root account and instead create IAM users with appropriate permissions.  
- 루트 계정 사용을 피하고 적절한 권한을 가진 IAM 사용자를 만드는 것이 최선의 방법
```


입니다.
→ 보안 원칙 요약.

* Users can be organized into groups to simplify permission management.

* 사용자는 그룹으로 조직하여 권한 관리를 단순화할 수 있습니다.
  → 그룹 기반 권한 관리 핵심.

* AWS allows customization of the sign-in URL via account aliases for easier access.

* AWS는 계정 별칭을 통해 로그인 URL을 맞춤 설정하여 접근성을 높일 수 있습니다.
  → 로그인 편의성 팁.

```

✅ 게임보상: 경험치 +70 (IAM Hands-On 이해도 +1)  
