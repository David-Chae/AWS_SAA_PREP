```md
# IAM MFA Hands On
# IAM MFA 실습
# AWS 계정 보호를 위한 MFA 실습 단계 안내

## Defining a Password Policy
## 비밀번호 정책 정의
# AWS 계정 보안을 위해 비밀번호 정책을 설정하는 단계입니다.

To begin, we will define a password policy.
먼저, 비밀번호 정책을 정의하겠습니다.
# 실습의 첫 단계로 비밀번호 정책 설정을 안내합니다.

Navigate to Account Settings on the left-hand side of the IAM console.
IAM 콘솔 왼쪽에서 '계정 설정(Account Settings)'으로 이동합니다.
# 콘솔에서 설정 위치를 안내합니다.

Here, you will find the option to edit the password policy.
여기서 비밀번호 정책을 편집할 수 있는 옵션을 찾을 수 있습니다.
# 비밀번호 정책 편집 위치를 안내합니다.

You can either use the IAM default password policy, which includes a set of predefined requirements, or customize the password policy according to your needs.
IAM 기본 비밀번호 정책(사전 정의된 요구사항 포함)을 사용하거나, 필요에 따라 맞춤 설정할 수 있습니다.
# 기본 정책과 사용자 지정 정책 옵션을 설명합니다.

Customization options include enforcing a minimum password length, requiring uppercase letters, lowercase letters, numbers, and non-alphanumeric characters.
맞춤 옵션에는 최소 비밀번호 길이, 대문자/소문자/숫자/특수문자 요구가 포함됩니다.
# 비밀번호 강도 강화 방법 설명.

Additionally, you can enable password expiration, for example, setting passwords to expire after 90 days.
추가로 비밀번호 만료 기능을 활성화할 수 있으며, 예를 들어 90일 후 만료하도록 설정 가능합니다.
# 정기 비밀번호 변경 설정 안내.

You can also require administrative password resets, allow users to change their own passwords, or prevent password reuse.
관리자 강제 비밀번호 초기화, 사용자의 비밀번호 변경 허용, 비밀번호 재사용 방지 기능도 설정 가능합니다.
# 다양한 정책 옵션 설명.

This password policy can be edited directly from the IAM console, representing the first part of securing your AWS account.
이 비밀번호 정책은 IAM 콘솔에서 직접 편집할 수 있으며, AWS 계정을 보호하는 첫 번째 단계입니다.
# 비밀번호 정책이 계정 보호의 시작임을 강조합니다.

## Setting Multi-Factor Authentication (MFA) for the Root Account
## 루트 계정에 다단계 인증(MFA) 설정
# 계정 보안을 강화하기 위한 두 번째 단계, 루트 계정 MFA 설정 안내

The second part of enhancing security involves setting up multi-factor authentication (MFA) for your root account.
보안을 강화하는 두 번째 단계는 루트 계정에 MFA를 설정하는 것입니다.
# MFA 설정의 목적과 대상 설명.

To do this, click on your account name and then select Security Credentials.
이를 위해 계정 이름을 클릭한 후 '보안 자격증명(Security Credentials)'을 선택합니다.
# 콘솔 내 MFA 설정 경로 안내.

If you are logged in as the root user, you will see the My Security Credentials section for the root user.
루트 사용자로 로그인하면 루트 사용자 전용 '내 보안 자격증명(My Security Credentials)' 섹션이 표시됩니다.
# 루트 사용자 접근권한 확인 안내.

Protecting your root user is critical as it is the most important account in your AWS environment.
루트 사용자는 AWS 환경에서 가장 중요한 계정이므로 보호가 필수적입니다.
# 루트 계정 보호의 중요성 강조.

MFA adds an additional layer of security by requiring a second form of authentication beyond the password.
MFA는 비밀번호 외 추가 인증 수단을 요구하여 보안 계층을 추가합니다.
# MFA의 기본 원리 설명.

Before proceeding, be aware that losing access to your MFA device can lock you out of your account.
진행하기 전에, MFA 장치 접근을 잃으면 계정에 로그인할 수 없게 될 수 있음을 인지해야 합니다.
# MFA 장치 분실 시 위험 안내.

If you think you might lose your device, it is advisable not to enable MFA until you have a secure backup plan.
장치를 잃을 가능성이 있다면, 안전한 백업 계획을 마련한 후 MFA를 활성화하는 것이 좋습니다.
# MFA 설정 전 주의 사항 안내.

Keep your device safe and follow along carefully if you wish to practice this setup.
장치를 안전하게 보관하고, 실습을 원하면 안내를 주의 깊게 따라야 합니다.
# MFA 실습 전 안전 수칙 안내.

## Assigning an MFA Device
## MFA 장치 지정
# MFA 장치를 계정에 연결하는 단계 안내

To assign an MFA device, you can name it as you prefer; for example, "My iPhone".
MFA 장치를 지정할 때 원하는 이름을 붙일 수 있습니다. 예: "My iPhone".
# MFA 장치 이름 지정 방법 안내.

Then, select the type of MFA device. Options include an authenticator app, a security key, or a hardware TOTP token.
그 다음, MFA 장치 유형을 선택합니다. 옵션에는 인증 앱, 보안 키, 하드웨어 TOTP 토큰이 있습니다.
# MFA 장치 유형 안내.

In this demonstration, we will use an authenticator app, which is a virtual device.
이번 실습에서는 가상 장치인 인증 앱을 사용합니다.
# 실습용 MFA 장치 유형 선택 설명.

Next, proceed to set up the app. A list of compatible applications for Android and iOS is provided.
다음으로 인증 앱 설정을 진행합니다. Android와 iOS용 호환 앱 목록이 제공됩니다.
# 앱 설정 단계 안내.

For this example, the Twilio Authenticator app is used.
이번 예시에서는 Twilio Authenticator 앱을 사용합니다.
# 예시 앱 안내.

## Setting Up the Authenticator App
## 인증 앱 설정
# MFA 인증 앱 구성 단계 안내

Launch the authenticator app on your phone and click on Show QR Code in the AWS console.
휴대폰에서 인증 앱을 실행하고 AWS 콘솔에서 'QR 코드 표시(Show QR Code)'를 클릭합니다.
# QR 코드 스캔 준비 안내.

You need to scan this QR code directly with your phone.
이 QR 코드를 휴대폰으로 직접 스캔합니다.
# QR 코드 스캔 방법 안내.

In the app, add a new account and scan the QR code displayed on the screen.
앱에서 새 계정을 추가하고 화면에 표시된 QR 코드를 스캔합니다.
# MFA 계정 추가 단계 안내.

Once scanned, the account will be added and named accordingly.
스캔이 완료되면 계정이 추가되고 이름이 자동 지정됩니다.
# 계정 추가 완료 안내.

After saving, the app will generate an MFA code in real-time. This code changes periodically to ensure security.
저장 후 앱은 실시간으로 MFA 코드를 생성하며, 보안을 위해 주기적으로 코드가 변경됩니다.
# MFA 코드 생성 및 주기적 변경 설명.

## Verifying the MFA Device
## MFA 장치 확인
# 설정한 MFA 장치가 정상적으로 작동하는지 검증하는 단계

AWS requires you to enter two consecutive MFA codes to verify that the device is set up correctly and that the codes are accurate.
AWS는 장치가 올바르게 설정되었는지 확인하기 위해 연속된 두 개의 MFA 코드를 입력하도록 요구합니다.
# MFA 장치 검증 방법 안내.

Enter the first MFA code generated by your app, followed by the second code. Once both codes are entered, click on Add MFA.
앱에서 생성된 첫 번째 MFA 코드와 두 번째 코드를 입력한 후, 'Add MFA'를 클릭합니다.
# MFA 검증 완료 방법 안내.

You can have up to eight MFA devices assigned, and you can view or remove them from the list in the IAM console.
최대 8개의 MFA 장치를 지정할 수 있으며, IAM 콘솔에서 확인하거나 제거할 수 있습니다.
# MFA 장치 관리 옵션 안내.

## Using MFA for Login
## 로그인 시 MFA 사용
# MFA 설정 후 로그인 과정 안내

After setting up MFA, when you log out and log back into AWS using your root account and password, you will be prompted to enter an MFA code.
MFA 설정 후, 루트 계정과 비밀번호로 로그아웃 후 다시 로그인하면 MFA 코드를 입력하라는 요청이 표시됩니다.
# MFA 로그인 과정 설명.

Open your authenticator app, enter the current code displayed, and submit it.
인증 앱을 열고 현재 표시된 코드를 입력한 후 제출합니다.
# MFA 코드 입력 방법 안내.

This process adds an extra level of security to your account by requiring both your password and the MFA code for access.
이 과정은 비밀번호와 MFA 코드 모두를 요구하여 계정에 추가적인 보안 계층을 제공합니다.
# MFA가 제공하는 보안 강화 효과 강조.

This concludes the lecture on setting up IAM MFA.
이로써 IAM MFA 설정 실습 강의를 마칩니다.
# 강의 종료 안내.

Implementing these security measures helps protect your AWS account from unauthorized access.
이 보안 조치를 구현하면 AWS 계정을 무단 접근으로부터 보호할 수 있습니다.
# 실습 목적과 효과 요약.

## Key Takeaways
## 핵심 요약
# 이번 실습에서 반드시 기억할 점

- Defined and customized password policies in IAM to enhance security.
- IAM에서 보안을 강화하기 위해 비밀번호 정책을 정의하고 맞춤 설정했습니다.
# 비밀번호 정책 설정 핵심 요약.

- Enabled multi-factor authentication (MFA) for the root AWS account to add an extra security layer.
- 루트 계정에 MFA를 활성화하여 추가 보안 계층을 적용했습니다.
# 루트 계정 MFA 핵심 요약.

- Demonstrated the setup process of an authenticator app as an MFA device.
- 인증 앱을 MFA 장치로 설정하는 과정을 시연했습니다.
# MFA 앱 설정 실습 요약.

- Highlighted the importance of safeguarding MFA devices to prevent account lockout.
- 계정 잠금 방지를 위해 MFA 장치 보호의 중요성을 강조했습니다.
# MFA 장치 안전 관리 핵심 요약.
```
