```markdown
# AWS IAM Identity Center  
# AWS IAM 아이덴티티 센터  

## Introduction to AWS IAM Identity Center  
## AWS IAM 아이덴티티 센터 소개  

AWS IAM Identity Center is the successor to the AWS Single Sign-On service. It provides a single login, hence the name single sign-on (SSO), for all your AWS accounts within AWS Organizations as well as your business cloud applications.  
AWS IAM 아이덴티티 센터는 AWS 싱글 사인온(SSO) 서비스의 후속 서비스입니다. AWS Organizations 내의 모든 AWS 계정과 비즈니스 클라우드 애플리케이션에 대해 하나의 로그인, 즉 SSO를 제공합니다.  
(SSO 개념 및 적용 범위 설명)  

You can connect to applications such as Salesforce, Box, Microsoft 365, or any application that supports SAML 2.0 integration. Additionally, it provides single login access to your EC2 Windows Instances, enabling one login access to everything.  
Salesforce, Box, Microsoft 365 등 SAML 2.0 통합을 지원하는 애플리케이션과 연결할 수 있습니다. 또한 EC2 Windows 인스턴스에도 단일 로그인으로 접근 가능해 모든 서비스에 하나의 로그인으로 접근할 수 있습니다.  
(애플리케이션 및 EC2 접근 통합)  

The exam will most likely ask about one login into multiple AWS accounts, which is a key feature of this service.  
시험에서는 여러 AWS 계정에 하나의 로그인으로 접근하는 기능에 대해 묻는 경우가 많으며, 이는 이 서비스의 핵심 기능입니다.  
(시험 대비 포인트 강조)  

---

## Identity Providers for AWS IAM Identity Center  
## AWS IAM 아이덴티티 센터용 아이덴티티 제공자  

The identity provider, where your users are stored for this login, can be one of two options:  
사용자가 로그인에 사용되는 아이덴티티 제공자는 두 가지 옵션 중 하나입니다:  

- A built-in identity store within the IAM Identity Center.  
- IAM 아이덴티티 센터 내장 아이덴티티 저장소  

- A third-party identity provider such as Active Directory (AD), OneLogin, or Okta.  
- Active Directory(AD), OneLogin, Okta와 같은 타사 아이덴티티 제공자  

(Login flow의 ID 제공자 설명)  

---

## Login Flow  
## 로그인 흐름  

The login flow works as follows:  
로그인 흐름은 다음과 같이 작동합니다:  

1. You navigate to the login page.  
1. 로그인 페이지로 이동합니다.  

2. Enter your username and password.  
2. 사용자 이름과 비밀번호를 입력합니다.  

3. You are then directed to the AWS IAM Identity Center portal.  
3. AWS IAM 아이덴티티 센터 포털로 이동됩니다.  

4. From there, you can select the AWS account you want to access and connect directly to the management console without needing to log in separately to each console.  
4. 포털에서 접근하려는 AWS 계정을 선택하고 각 콘솔에 개별 로그인 없이 바로 관리 콘솔에 접속할 수 있습니다.  
(SSO를 통한 단일 로그인 강조)  

This means you only need to log in once to the IAM Identity Center portal to gain SSO access to multiple AWS accounts and business applications, eliminating the need to enter your password multiple times.  
즉, IAM 아이덴티티 센터 포털에 한 번 로그인하면 여러 AWS 계정과 비즈니스 애플리케이션에 SSO로 접근할 수 있어 비밀번호를 여러 번 입력할 필요가 없습니다.  
(효율적인 로그인 관리 설명)  

---

## Integration with User Stores  
## 사용자 저장소와의 통합  

The browser interface connects to the login page of your AWS IAM Identity Center. You can integrate it with different user stores such as:  
브라우저 인터페이스가 AWS IAM 아이덴티티 센터 로그인 페이지와 연결됩니다. 다양한 사용자 저장소와 통합할 수 있습니다:  

- Active Directory, either cloud-based or on-premises, to manage users and groups.  
- 클라우드 또는 온프레미스 Active Directory를 사용하여 사용자와 그룹 관리  

- The built-in IAM Identity Center store where you define users and groups similarly to IAM.  
- IAM과 유사하게 사용자를 정의하고 그룹을 관리할 수 있는 내장 IAM 아이덴티티 센터 저장소  

IAM Identity Center integrates with your organization to provide SSO for AWS accounts, Windows EC2 Instances, business cloud applications, or custom SAML 2.0 enabled applications, all through one login.  
IAM 아이덴티티 센터는 조직과 통합되어 AWS 계정, Windows EC2 인스턴스, 비즈니스 클라우드 애플리케이션 또는 SAML 2.0 지원 커스텀 애플리케이션에 대해 하나의 로그인으로 SSO를 제공합니다.  
(SSO 적용 범위 요약)  

---

## Permission Sets and Access Control  
## 권한 세트 및 접근 제어  

When you log in, you do not have access to everything by default. You define permission sets in the Identity Center to specify which users have access to which resources.  
로그인 시 기본적으로 모든 권한이 부여되지는 않습니다. IAM 아이덴티티 센터에서 권한 세트를 정의하여 사용자가 어떤 리소스에 접근할 수 있는지 지정합니다.  
(권한 세트 개념)  

### Example: Managing Access for Developers  
### 예제: 개발자 접근 관리  

Consider an organization with two organizational units (OUs): development and production, each with their own AWS accounts. Two developers, Bob and Alice, are part of the company.  
개발과 운영 두 개의 조직 단위(OU)를 가진 조직을 생각해봅시다. 각 OU에는 자체 AWS 계정이 있습니다. Bob과 Alice라는 두 개발자가 회사에 소속되어 있습니다.  

1. Create a group called "developers" including Bob and Alice.  
1. Bob과 Alice를 포함하는 "developers" 그룹 생성  

2. Create a permission set granting admin access to the development OU.  
2. 개발 OU에 관리자 접근 권한을 부여하는 권한 세트 생성  

3. Associate this permission set with the development OU.  
3. 권한 세트를 개발 OU와 연결  

4. Assign the permission set to the developers group, allowing Bob and Alice to assume a role with full access in any development account.  
4. 권한 세트를 developers 그룹에 할당하여 Bob과 Alice가 개발 계정에서 전체 접근 권한을 가진 역할을 맡도록 설정  

5. Similarly, create a ReadOnlyAccess permission set for the production OU and assign it to the developers group.  
5. 운영 OU에는 ReadOnlyAccess 권한 세트를 만들고 developers 그룹에 할당  

This setup relates users to groups, permission sets, and specific account assignments within IAM Identity Center.  
이 설정은 IAM 아이덴티티 센터 내에서 사용자, 그룹, 권한 세트 및 계정 할당을 연결합니다.  
(권한 구조 이해)  

---

## Fine-Grained Permissions and Assignments  
## 세부 권한 및 할당  

### Multi-Account Permission Management  
### 다중 계정 권한 관리  

Using IAM Identity Center, you can manage access across multiple AWS accounts in your organization. Permission sets define one or more IAM policies that you assign to users or groups to specify their access rights.  
IAM 아이덴티티 센터를 사용하면 조직 내 여러 AWS 계정의 접근을 관리할 수 있습니다. 권한 세트는 사용자나 그룹에 할당할 하나 이상의 IAM 정책을 정의하여 접근 권한을 지정합니다.  
(다중 계정 권한 관리)  

For example, a permission set for database administrators might include policies granting access to RDS and Aurora in both development and production accounts. IAM Identity Center automatically creates corresponding IAM roles for users.  
예를 들어, 데이터베이스 관리자를 위한 권한 세트에는 개발 및 운영 계정의 RDS와 Aurora 접근 권한이 포함될 수 있습니다. IAM 아이덴티티 센터는 자동으로 해당 사용자용 IAM 역할을 생성합니다.  
(자동 역할 생성 설명)  

When users log in through IAM Identity Center and access the console of development or production accounts, they automatically assume the appropriate IAM role with the assigned permissions.  
사용자가 IAM 아이덴티티 센터로 로그인하여 개발 또는 운영 계정 콘솔에 접근하면, 할당된 권한을 가진 적절한 IAM 역할을 자동으로 맡습니다.  
(자동 역할 전환)  

---

### Application Assignments  
### 애플리케이션 접근 할당  

You can define which users or groups have access to specific applications. IAM Identity Center provides the required URLs, certificates, and metadata for these applications out of the box.  
어떤 사용자나 그룹이 특정 애플리케이션에 접근할 수 있는지 정의할 수 있습니다. IAM 아이덴티티 센터는 필요한 URL, 인증서, 메타데이터를 기본으로 제공합니다.  
(애플리케이션 접근 관리)  

---

### Attribute-Based Access Control (ABAC)  
### 속성 기반 접근 제어 (ABAC)  

IAM Identity Center supports fine-grained permissions based on user attributes stored in the identity store. This means you can assign tags such as cost center, job title (e.g., junior, senior), or locale to users.  
IAM 아이덴티티 센터는 저장소에 있는 사용자 속성을 기반으로 세부 권한을 지원합니다. 예: 비용 센터, 직책(주니어/시니어), 지역 태그를 사용자에게 할당 가능  

Using these attributes, you can define IAM permission sets once and leverage the attributes to modify user access dynamically without changing the underlying permission sets. This advanced use case simplifies managing access across your organization.  
이 속성을 활용하면 권한 세트를 한 번 정의하고, 속성을 기반으로 사용자 접근을 동적으로 조정할 수 있습니다. 권한 세트를 변경할 필요가 없어 조직 전반의 접근 관리가 단순해집니다.  
(ABAC 활용)  

---

## Conclusion  
## 결론  

AWS IAM Identity Center simplifies access management by providing a single login for multiple AWS accounts and business applications, integrating with various identity providers, and enabling fine-grained permission control through permission sets and attribute-based access control.  
AWS IAM 아이덴티티 센터는 여러 AWS 계정과 비즈니스 애플리케이션에 대한 단일 로그인을 제공하고, 다양한 아이덴티티 제공자와 통합되며,
```


권한 세트와 속성 기반 접근 제어를 통해 세부 권한 관리가 가능합니다.
(서비스 요약)

---

## Key Takeaways

## 핵심 요약

* AWS IAM Identity Center is the successor to AWS Single Sign-On, providing one login for multiple AWS accounts and business cloud applications.

* AWS IAM 아이덴티티 센터는 AWS SSO의 후속 서비스로, 여러 AWS 계정과 비즈니스 클라우드 애플리케이션에 대한 단일 로그인 제공

* Users can be stored in the built-in IAM Identity Center store or connected through third-party identity providers like Active Directory, OneLogin, or Okta.

* 사용자는 내장 IAM 아이덴티티 센터 저장소에 저장되거나 AD, OneLogin, Okta와 같은 타사 제공자와 연결 가능

* Permission sets define user access across multiple AWS accounts and applications, enabling fine-grained control.

* 권한 세트는 여러 AWS 계정과 애플리케이션에 대한 사용자의 접근을 정의하여 세부 제어 가능

* Attribute-Based Access Control allows permissions to be managed based on user attributes, simplifying access management.

* 속성 기반 접근 제어(ABAC)를 통해 사용자 속성에 기반한 권한 관리 가능, 접근 관리 단순화

```
게임보상: 🗝️ IAM Identity Center 완전 정복! SSO와 ABAC 이해 완료! 🎯✅
```
