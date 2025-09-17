```markdown
# AWS Directory Services  
# AWS 디렉터리 서비스  

## Introduction to Microsoft Active Directory and AWS Directory Services  
## 마이크로소프트 액티브 디렉터리 및 AWS 디렉터리 서비스 소개  

Microsoft Active Directory (AD) is software found on any Windows Server with Active Directory Domain Services.  
마이크로소프트 액티브 디렉터리(AD)는 Active Directory 도메인 서비스가 설치된 모든 Windows Server에서 실행되는 소프트웨어입니다.  
(AD 정의)  

It functions as a database of objects, which can include user accounts, computers, printers, file shares, and security groups.  
사용자 계정, 컴퓨터, 프린터, 파일 공유, 보안 그룹 등 객체를 관리하는 데이터베이스 역할을 합니다.  
(AD 객체 관리 설명)  

All users within a Microsoft ecosystem on-premises are managed through Microsoft Active Directory, providing centralized security management.  
온프레미스 Microsoft 환경 내 모든 사용자는 AD를 통해 관리되며, 중앙 집중식 보안 관리가 가능합니다.  
(중앙 관리 강조)  

This allows for creating accounts, assigning permissions, and organizing all objects into a hierarchical tree structure.  
계정 생성, 권한 할당, 객체를 계층 트리 구조로 조직화할 수 있습니다.  
(AD 계층 구조 설명)  

A group of such trees is called a forest.  
이러한 트리 그룹을 포리스트(forest)라고 합니다.  
(포리스트 개념)  

---

## Example of Active Directory Usage  
## 액티브 디렉터리 사용 예시  

Consider a domain controller where an account is created with the username "John" and password "Password".  
사용자 이름이 "John", 비밀번호가 "Password"인 계정을 생성한 도메인 컨트롤러를 가정해봅시다.  

All Windows machines within the network connect to this domain controller.  
네트워크 내 모든 Windows 기기가 이 도메인 컨트롤러에 연결됩니다.  

When John attempts to log in on any machine, the machine queries the domain controller to verify the credentials.  
John이 어떤 기기에서든 로그인하면, 해당 기기는 도메인 컨트롤러에 자격 증명을 확인하도록 요청합니다.  

If the credentials match, access is granted.  
자격 증명이 일치하면 접근이 허용됩니다.  

This setup allows users to access any machine within the network using their centralized credentials.  
이 설정을 통해 사용자는 중앙 관리된 자격 증명으로 네트워크 내 모든 기기에 접근할 수 있습니다.  
(중앙 인증 설명)  

---

## AWS Directory Services Overview  
## AWS 디렉터리 서비스 개요  

AWS Directory Services provides a way to create and manage Active Directory environments within AWS.  
AWS 디렉터리 서비스는 AWS 내에서 Active Directory 환경을 생성하고 관리할 수 있는 방법을 제공합니다.  

There are three main options:  
주요 옵션은 세 가지입니다:  

1. **AWS Managed Microsoft AD:** Allows you to create your own Active Directory in AWS. Users can be managed locally, and it supports multi-factor authentication (MFA). It also supports trust relationships with on-premise AD, enabling shared user authentication.  
1. **AWS 관리형 Microsoft AD:** AWS 내에서 자체 AD를 생성 가능. 사용자 로컬 관리 가능, MFA 지원, 온프레미스 AD와 트러스트 관계 지원하여 사용자 인증 공유 가능  

2. **AD Connector:** Acts as a proxy gateway to redirect authentication requests to your on-premise AD. It supports MFA, but users are solely managed on-premise.  
2. **AD 커넥터:** 온프레미스 AD로 인증 요청을 전달하는 프록시 역할, MFA 지원, 사용자는 온프레미스에서만 관리  

3. **Simple AD:** An AD-compatible managed directory on AWS that does not use Microsoft Directory Services. It cannot be joined with an on-premise AD and is suitable for standalone AWS environments without on-premise AD.  
3. **심플 AD:** Microsoft Directory Services를 사용하지 않는 AWS용 AD 호환 관리 디렉터리, 온프레미스 AD와 연결 불가, 온프레미스 AD가 없는 독립형 AWS 환경에 적합  

---

## AWS Managed Microsoft AD  
## AWS 관리형 Microsoft AD  

This option creates a standalone Active Directory in AWS where you can manage users locally.  
AWS에서 독립형 AD를 생성하여 사용자를 로컬로 관리할 수 있습니다.  

It supports multi-factor authentication and allows establishing a trust relationship with your on-premise Active Directory.  
MFA를 지원하며 온프레미스 AD와 트러스트 관계를 설정할 수 있습니다.  

This means AWS Managed Microsoft AD and your on-premise AD trust each other, enabling users authenticated in one directory to be recognized by the other.  
AWS 관리형 Microsoft AD와 온프레미스 AD가 서로를 신뢰하여, 한 디렉터리에서 인증된 사용자가 다른 디렉터리에서도 인식됩니다.  

This setup allows shared user access between AWS and on-premise environments.  
AWS와 온프레미스 환경 간 사용자 접근을 공유할 수 있습니다.  
(트러스트 관계 설명)  

---

## AD Connector  
## AD 커넥터  

AD Connector serves as a direct proxy to your on-premise Active Directory.  
AD 커넥터는 온프레미스 AD로 직접 연결되는 프록시 역할을 합니다.  

It supports multi-factor authentication, but all user management occurs on the on-premise AD.  
MFA를 지원하지만 모든 사용자 관리는 온프레미스 AD에서 수행됩니다.  

When users authenticate through AD Connector, the requests are proxied back to the on-premise AD for verification.  
사용자가 AD 커넥터를 통해 인증하면 요청이 온프레미스 AD로 전달되어 검증됩니다.  

This setup does not store user information in AWS but facilitates seamless authentication for AWS resources using existing on-premise credentials.  
AWS에는 사용자 정보를 저장하지 않지만, 기존 온프레미스 자격 증명을 사용하여 AWS 리소스 인증을 원활하게 수행할 수 있습니다.  
(프록시 인증 설명)  

---

## Simple AD  
## 심플 AD  

Simple AD is an AD-compatible managed directory service on AWS that does not use Microsoft Directory Services.  
심플 AD는 Microsoft Directory Services를 사용하지 않는 AWS용 AD 호환 관리 디렉터리 서비스입니다.  

It cannot be joined with an on-premise Active Directory.  
온프레미스 AD와 연결할 수 없습니다.  

This option is suitable if you do not have an on-premise AD and need a standalone Active Directory for your AWS cloud environment.  
온프레미스 AD가 없고 AWS 클라우드 환경에서 독립형 AD가 필요한 경우 적합합니다.  

It enables Windows EC2 instances to join the domain and share logins and credentials within AWS.  
Windows EC2 인스턴스가 도메인에 가입하고 AWS 내에서 로그인 및 자격 증명을 공유할 수 있습니다.  

---

## Use Cases and Exam Tips  
## 사용 사례 및 시험 팁  

- If you want to proxy users to an on-premise Active Directory, use AD Connector.  
- 사용자를 온프레미스 AD로 프록시하려면 AD 커넥터 사용  

- If you want to manage users in the cloud with multi-factor authentication, use AWS Managed Microsoft AD.  
- MFA를 사용하여 클라우드에서 사용자를 관리하려면 AWS 관리형 Microsoft AD 사용  

- If you do not have an on-premise Active Directory and need a simple directory in AWS, use Simple AD.  
- 온프레미스 AD가 없고 AWS에서 간단한 디렉터리가 필요하면 심플 AD 사용  

---

## Integration with IAM Identity Center  
## IAM 아이덴티티 센터와의 통합  

When integrating IAM Identity Center with Active Directory:  
IAM 아이덴티티 센터와 Active Directory를 통합할 때:  

- If your Active Directory is managed on AWS using Directory Services, integration is straightforward and out of the box. You simply configure IAM Identity Center to connect to your AWS Managed Microsoft AD.  
- AWS에서 Directory Services로 관리되는 AD라면 통합이 간단하며, IAM 아이덴티티 센터를 AWS 관리형 Microsoft AD에 연결하도록 설정하면 됩니다.  

- If your Active Directory is self-managed on-premises, there are two options:  
- 온프레미스에서 자체 관리되는 AD라면 두 가지 옵션이 있습니다:  

  1. Establish a two-way trust relationship between your on-premise AD and AWS Managed Microsoft AD. This allows single sign-on integration via IAM Identity Center.  
  1. 온프레미스 AD와 AWS 관리형 AD 간 양방향 트러스트 관계 설정. IAM Identity Center를 통한 SSO 통합 가능  

  2. Use an AD Connector to proxy authentication requests from IAM Identity Center to your on-premise AD.  
  2. AD 커넥터를 사용하여 IAM Identity Center에서 온프레미스 AD로 인증 요청 프록시  

The choice depends on whether you want to manage users within AWS or only proxy authentication requests to your on-premise directory.  
선택은 AWS에서 사용자를 관리할지, 온프레미스 디렉터리에 대한 인증 요청만 프록시할지에 따라 달라집니다.  

---

## Summary  
## 요약  

AWS Directory Services offers flexible options to integrate and manage Active Directory environments in the cloud or proxy to on-premise directories.  
AWS 디렉터리 서비스는 클라우드에서 AD 환경을 통합 및 관리하거나 온프레미스 디렉터리로 프록시할 수 있는 유연한 옵션을 제공합니다.  

Understanding the differences between AWS Managed Microsoft AD, AD Connector, and Simple AD is essential for selecting the right solution based on your infrastructure and management preferences.  
AWS 관리형 Microsoft AD, AD 커넥터, 심플 AD 간의 차이를 이해하는 것은 인프라와 관리 요구에 맞는 적절한 솔루션 선택에 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Microsoft Active Directory (AD) is a centralized database for managing users, computers, and other resources within a Windows network.  
- Microsoft AD는 Windows 네트워크 내 사용자, 컴퓨터 및 기타 리소스를 관리하는 중앙 데이터베이스입니다.  

- AWS Directory Services offers three main options: AWS Managed Microsoft AD, AD Connector, and Simple AD, each serving different integration and management needs.  
- AWS 디렉터리 서비스는 AWS 관리형 Microsoft AD, AD 커넥터, 심플 AD의 세 가지 주요 옵션을 제공하며, 각기 다른 통합 및 관리 요구를 충족합니다.  

- AWS Managed Microsoft AD allows creating and managing an Active Directory in AWS with support for trust relationships to on-premise AD.  
- AWS 관리형 Microsoft AD는 AWS에서 AD를 생성하고 관리하며, 온프레미스 AD와 트러스트 관계를 지원합니다.  

- AD Connector acts as a proxy to on-premise AD, enabling authentication without managing users in AWS.  
- AD 커넥터는 온프레미스 AD로의 프록시 역할을 하며, AWS에서 사용자 관리 없이 인증 가능  

- Simple AD is a standalone, AD-compatible directory for AWS without integration to on-premise AD.  
- 심플 AD는 온프레미스 AD와 통합되지 않은 독립형 AD 호환 디렉터리입니다.  

- Integration of IAM Identity Center with Active Directory depends on whether the directory is managed in AWS or self-managed on-premises, with options for two-way trust or AD Connector proxy.  
- IAM 아이덴티티 센터와 AD 통합은 디렉터리가 AWS에서 관리되는지 아니면 온프레미스에서 자체 관리되는지에 따라 달라지며, 양방향 트러스트 또는 AD 커넥터 프록시 옵션을 제공합니다.  
```

게임보상: 🗄️ AWS Directory Services 완전 정복! AD 구조, Managed AD, AD Connector, Simple AD 완벽 이해! 🎯✅
