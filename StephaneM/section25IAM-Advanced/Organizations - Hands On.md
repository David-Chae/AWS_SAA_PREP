```markdown
# Organizations - Hands On  
# Organizations - 실습  

## Introduction to AWS Organizations  
## AWS Organizations 소개  
In this hands-on session, we will practice using AWS Organizations.  
이번 실습 세션에서는 AWS Organizations 사용법을 직접 실습합니다.  
(실습 목표 소개)  

Organizations is a global service because it deals with accounts and their grouping.  
Organizations는 계정과 계정 그룹화를 다루므로 글로벌 서비스입니다.  
(계정 중심 글로벌 서비스)  

For this demonstration, I have created two new AWS accounts: one master account named "AWS Course Master Account" and one child account named "AWS Course Child Account".  
이번 데모를 위해, "AWS Course Master Account"라는 마스터 계정과 "AWS Course Child Account"라는 자식 계정 두 개를 생성했습니다.  
(데모용 계정 준비)  

This approach avoids using my main accounts and allows a clean demo with two separate accounts.  
이 방법은 본 계정을 사용하지 않고, 두 개 계정을 활용해 깔끔한 데모를 가능하게 합니다.  
(본 계정 보호)  

If you want to follow along, I suggest creating two new accounts: one to serve as the master and one as the child within your organization.  
따라서 따라하고 싶다면, 마스터 계정용과 자식 계정용 새 계정 두 개를 만드는 것을 추천합니다.  
(실습 참여 안내)  

---

## Creating an Organization and Adding Accounts  
## 조직 생성 및 계정 추가  
From the master account, I will create an organization.  
마스터 계정에서 조직을 생성합니다.  
(조직 생성 시작)  

Once created, the organization has root organizational units, and the master account is designated as the management account.  
조직 생성 후 루트 OU가 생성되고, 마스터 계정은 관리 계정으로 지정됩니다.  
(루트 OU 및 관리 계정)  

Next, we add a second AWS account to the organization.  
다음으로 두 번째 AWS 계정을 조직에 추가합니다.  
(자식 계정 추가)  

There are two options:  
방법은 두 가지가 있습니다:  
(계정 추가 옵션)  

1. Create a new account by specifying the account name, email address, and an IAM role for management.  
1. 계정 이름, 이메일, IAM 역할을 지정하여 새 계정을 생성.  

2. Invite an existing AWS account by providing its email address or account ID.  
2. 이메일 또는 계정 ID를 제공하여 기존 계정을 초대.  

For this demo, I will invite my child account by entering its email address and sending the invitation.  
이번 데모에서는 자식 계정을 이메일로 초대하고 초대장을 보냅니다.  
(자식 계정 초대)  

The invitation will appear in the child account's organization console under "Invitations".  
초대장은 자식 계정 조직 콘솔의 "Invitations"에서 확인 가능합니다.  
(초대 확인 위치)  

Upon accepting the invitation, the child account becomes part of the AWS organization, granting the master account full control as the organization has full features enabled.  
초대를 수락하면 자식 계정이 조직에 속하게 되고, 조직 기능이 활성화되어 마스터 계정이 전체 제어 권한을 가집니다.  
(초대 수락 후 권한)  

---

## Organizing Accounts with Organizational Units (OUs)  
## 조직 단위(OUs)로 계정 구성  
Within the organization, accounts can be organized using Organizational Units (OUs).  
조직 내 계정은 OU를 사용하여 구성할 수 있습니다.  
(OU 활용)  

OUs allow hierarchical grouping of accounts for better management.  
OU는 계정을 계층적으로 그룹화하여 관리 효율을 높입니다.  
(계층적 그룹화)  

For example, under the root OU, I created three OUs:  
예: 루트 OU 아래 세 개의 OU를 생성했습니다:  
(예시 OU)  

- Dev  
- 개발(Dev)  

- Test  
- 테스트(Test)  

- Prod  
- 운영(Prod)  

Within the Prod OU, I further created nested OUs for departments such as HR and Finance.  
Prod OU 안에 HR, Finance 부서용 중첩 OU를 추가 생성했습니다.  
(중첩 OU)  

This nesting can continue as needed to reflect organizational structure.  
조직 구조에 맞게 필요한 만큼 중첩 OU를 계속 생성할 수 있습니다.  
(유연한 구조)  

Currently, the child account is moved into the Finance OU within the Prod OU.  
현재 자식 계정은 Prod OU 내 Finance OU로 이동했습니다.  
(자식 계정 위치)  

It is best practice to leave the management account under the root OU, though it can be moved if desired.  
관리 계정은 루트 OU에 두는 것이 권장되지만 필요 시 이동 가능.  
(관리 계정 권장 위치)  

---

## Enabling and Using Service Control Policies (SCPs)  
## 서비스 제어 정책(SCPs) 활성화 및 사용  
Service Control Policies allow centralized permission management across accounts in an organization.  
SCP는 조직 내 계정에 대한 중앙 집중식 권한 관리를 제공합니다.  
(중앙 권한 관리)  

To enable SCPs, navigate to the Policies section and activate the service control policy feature.  
SCP 활성화는 Policies 섹션으로 이동하여 서비스 제어 정책 기능을 켭니다.  
(SCP 활성화 방법)  

Other policy types include backup policies for organization-wide backup plans and tag policies to standardize tagging across accounts.  
기타 정책 유형으로는 조직 전체 백업 정책과 계정 태그 표준화를 위한 태그 정책이 있습니다.  
(다른 정책 유형)  

However, for this hands-on and exam purposes, service control policies are the primary focus.  
하지만 이번 실습과 시험에서는 SCP가 주요 초점입니다.  
(SCP 초점)  

Once enabled, you can create new SCPs.  
활성화 후 새 SCP를 생성할 수 있습니다.  
(SCP 생성)  

For example, I created a policy named "DenyAccess to S3" that denies all actions on the Amazon S3 service.  
예: Amazon S3 서비스 모든 액션을 거부하는 "DenyAccess to S3" 정책을 생성했습니다.  
(S3 접근 제한 정책)  

This policy can be attached to any OU or account to restrict access accordingly.  
이 정책은 OU나 계정에 적용하여 접근을 제한할 수 있습니다.  
(정책 적용)  

---

## Policy Inheritance and Application  
## 정책 상속 및 적용  
Policies attached to parent OUs are inherited by child OUs and accounts.  
부모 OU에 적용된 정책은 하위 OU와 계정에 상속됩니다.  
(정책 상속)  

For instance, the root OU has a full AWS access policy attached, which is inherited by all child OUs and accounts.  
예: 루트 OU에 전체 AWS 접근 정책이 적용되면 모든 하위 OU와 계정이 상속받습니다.  
(루트 OU 상속)  

After attaching the "DenyAccess to S3" SCP to the Finance OU, the child account within Finance inherits this policy.  
Finance OU에 "DenyAccess to S3" SCP를 적용하면, Finance 내 자식 계정이 이 정책을 상속받습니다.  
(Finance OU 상속 적용)  

This effectively restricts the child account's access to Amazon S3, regardless of user permissions.  
사용자 권한과 상관없이 자식 계정의 Amazon S3 접근이 제한됩니다.  
(SCP 권한 제한 효과)  

To verify, logging into the child account and attempting to access the S3 console results in a permission denial, demonstrating the power of SCPs to enforce restrictions across an organization.  
확인하려면 자식 계정에서 S3 콘솔에 접속 시도를 하면 접근 거부가 나타납니다. 이는 SCP가 조직 전체 제한을 적용할 수 있음을 보여줍니다.  
(제한 검증)  

---

## Conclusion  
## 결론  
AWS Organizations enables centralized management of multiple AWS accounts through hierarchical organization and policy enforcement.  
AWS Organizations는 계층적 조직과 정책 적용을 통해 여러 AWS 계정을 중앙에서 관리할 수 있습니다.  
(조직 관리 요약)  

Service Control Policies provide powerful control over permissions across accounts, ensuring compliance and security at scale.  
SCP는 계정 전반 권한을 강력하게 제어하여 대규모 컴플라이언스와 보안을 보장합니다.  
(SCP 중요성)  

This hands-on demonstration showed how to create an organization, add accounts, organize them into OUs, enable SCPs, create a restrictive policy, and observe its effect on account permissions.  
이번 실습에서는 조직 생성, 계정 추가, OU 구성, SCP 활성화, 제한 정책 생성, 계정 권한 적용 확인을 보여주었습니다.  
(실습 요약)  

---

## Key Takeaways  
## 핵심 요약  
- AWS Organizations is a global service used to group and manage multiple AWS accounts.  
- AWS Organizations는 여러 AWS 계정을 그룹화하고 관리하는 글로벌 서비스입니다.  

- You can create a master (management) account and add child accounts to an organization.  
- 마스터 계정을 생성하고 조직에 자식 계정을 추가할 수 있습니다.  

- Organizational Units (OUs) allow hierarchical grouping of accounts for better management.  
- OU를 사용하면 계정을 계층적으로 그룹화하여 관리 효율을 높일 수 있습니다.  

- Service Control Policies (SCPs) enable centralized permission management and can restrict access across accounts within OUs.  
- SCP를 통해 중앙 집중식 권한 관리가 가능하며 OU 내 계정 접근을 제한할 수 있습니다.  
```

게임보상: 🏆 Hands-On 마스터 달성! AWS Organizations 계정 구성, OU 그룹화, SCP 적용까지 실습 완료! 🔥📂
