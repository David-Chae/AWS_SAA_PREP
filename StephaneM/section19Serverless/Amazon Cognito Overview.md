# Amazon Cognito Overview
# 아마존 코그니토 개요

## Introduction to Amazon Cognito
## Amazon Cognito 소개
> Amazon Cognito는 웹 및 모바일 애플리케이션 사용자를 위한 인증 및 신원 관리 서비스입니다.

Amazon Cognito is a service designed to provide users with an identity to interact with web and mobile applications.
Amazon Cognito는 웹 및 모바일 애플리케이션과 상호작용할 수 있는 사용자의 신원을 제공하기 위해 설계된 서비스입니다.
> 핵심: 사용자 인증 및 신원 제공

These users typically exist outside of your AWS account, which is why the service is named Cognito, as it assigns identities to users that are not yet known to your system.
이 사용자들은 일반적으로 AWS 계정 외부에 존재하며, 아직 시스템에 알려지지 않은 사용자에게 신원을 부여하기 때문에 Cognito라는 이름이 붙었습니다.
> 핵심: AWS 외부 사용자 관리

## Components of Amazon Cognito
## Amazon Cognito 구성 요소
> Cognito의 두 가지 핵심 서비스

Amazon Cognito consists of two main sub-services:
Amazon Cognito는 두 가지 주요 하위 서비스로 구성됩니다.
> 핵심: User Pools + Identity Pools

Cognito User Pools: This service provides sign-in functionality for application users and integrates well with API Gateway and the Application Load Balancer.
Cognito User Pools: 애플리케이션 사용자를 위한 로그인 기능을 제공하며, API Gateway 및 Application Load Balancer와 원활하게 통합됩니다.
> 핵심: 사용자 인증 관리

Cognito Identity Pools: Formerly known as Federated Identity, this service provides temporary AWS credentials to users registered with your application, allowing them to access AWS resources directly.
Cognito Identity Pools: 이전 명칭은 Federated Identity이며, 애플리케이션 등록 사용자에게 임시 AWS 자격 증명을 제공하여 AWS 리소스에 직접 접근할 수 있도록 합니다.
> 핵심: 직접 AWS 리소스 접근 지원

These two components work together to manage user authentication and authorization effectively.
이 두 구성 요소는 사용자 인증과 권한 관리를 효과적으로 수행하기 위해 함께 작동합니다.
> 핵심: 인증 + 권한 관리 통합

## Cognito vs IAM Users
## Cognito와 IAM 사용자 비교
> AWS 계정 내 IAM 사용자와 Cognito 사용자 차이

While AWS Identity and Access Management (IAM) manages users within your AWS account, Cognito is designed for your web and mobile application users who exist outside of AWS.
IAM은 AWS 계정 내 사용자를 관리하지만, Cognito는 AWS 외부의 웹 및 모바일 애플리케이션 사용자를 위해 설계되었습니다.
> 핵심: AWS 계정 외부 사용자 관리

It is particularly suited for scenarios involving hundreds of users, mobile users, or authentication mechanisms such as SAML.
특히 수백 명의 사용자, 모바일 사용자, 또는 SAML과 같은 인증 메커니즘 시나리오에 적합합니다.
> 핵심: 대규모/모바일 사용자 인증 최적화

## Deep Dive into Cognito User Pools
## Cognito User Pools 상세
> 서버리스 사용자 데이터베이스 기능

Cognito User Pools (CUP) act as a serverless user database for your web and mobile applications.
Cognito User Pools(CUP)는 웹 및 모바일 애플리케이션용 서버리스 사용자 데이터베이스 역할을 합니다.
> 핵심: 서버리스 사용자 관리

They allow you to define simple login credentials such as a username or email combined with a password.
사용자 이름 또는 이메일과 비밀번호를 조합한 간단한 로그인 자격 증명을 정의할 수 있습니다.
> 핵심: 기본 로그인 기능 제공

Key features include:
주요 기능:
- Password reset functionality.
- 비밀번호 재설정 기능
- Email and phone number verification.
- 이메일 및 전화번호 인증
- Multi-factor authentication.
- 다단계 인증(MFA)
- Integration with social identity providers like Facebook and Google.
- Facebook, Google 등 소셜 아이디 제공자 통합

These user pools integrate seamlessly with API Gateway and Application Load Balancer to authenticate users and pass verified identities to backend services.
이 사용자 풀은 API Gateway 및 ALB와 원활하게 통합되어 사용자를 인증하고 확인된 신원을 백엔드 서비스로 전달합니다.
> 핵심: 백엔드 인증 위임

## Integration with API Gateway
## API Gateway와 통합
> API Gateway 연동 흐름

When a user connects to your application via API Gateway, the flow is as follows:
사용자가 API Gateway를 통해 애플리케이션에 연결될 때의 흐름:
- The user authenticates with the Cognito User Pool and retrieves a token.
- 사용자가 Cognito User Pool에서 인증하고 토큰을 가져옵니다.
- The token is passed to the API Gateway.
- 토큰이 API Gateway로 전달됩니다.
- API Gateway verifies the token.
- API Gateway가 토큰을 검증합니다.
- Upon successful verification, the token is translated into a user identity.
- 검증 성공 시 토큰이 사용자 신원으로 변환됩니다.
- This identity is passed to your backend Lambda function.
- 이 신원이 백엔드 Lambda 함수로 전달됩니다.

This process ensures that your backend knows exactly which authenticated user it is dealing with.
이 과정은 백엔드가 정확히 어떤 인증된 사용자와 상호작용하는지 알 수 있도록 보장합니다.
> 핵심: 백엔드 인증 책임 분리

## Integration with Application Load Balancer
## Application Load Balancer와 통합
> ALB 연동 흐름

Similarly, Cognito User Pools can be integrated with an Application Load Balancer (ALB):
Cognito User Pools는 ALB와도 통합될 수 있습니다.
- The application connects to the Cognito User Pool.
- 애플리케이션이 Cognito User Pool에 연결됩니다.
- The authenticated token is passed to the ALB.
- 인증된 토큰이 ALB로 전달됩니다.
- The ALB verifies the login.
- ALB가 로그인 정보를 검증합니다.
- If valid, the ALB redirects the request to the backend.
- 유효하면 ALB가 요청을 백엔드로 리디렉션합니다.
- Additional headers containing the user's identity are included.
- 사용자 신원을 포함한 추가 헤더가 포함됩니다.

This shifts the responsibility of user authentication from your backend to the API Gateway or ALB, simplifying backend logic.
이로써 사용자 인증 책임이 백엔드에서 API Gateway 또는 ALB로 이동하여 백엔드 로직이 단순화됩니다.
> 핵심: 인증 위임 + 로직 단순화

## Cognito Identity Pools (Federated Identities)
## Cognito Identity Pools (페더레이티드 아이덴티티)
> 임시 AWS 자격증명 제공

Cognito Identity Pools provide identities for users who access AWS resources directly, rather than through API Gateway or ALB.
Cognito Identity Pools는 API Gateway나 ALB를 거치지 않고 AWS 리소스를 직접 접근하는 사용자에게 신원을 제공합니다.
> 핵심: 직접 AWS 리소스 접근 지원

This service issues temporary AWS credentials to users, enabling them to interact with AWS services such as S3 or DynamoDB.
이 서비스는 사용자가 S3, DynamoDB 등 AWS 서비스와 상호작용할 수 있도록 임시 AWS 자격 증명을 발급합니다.
> 핵심: 임시 자격 증명

Users can originate from various sources, including:
사용자는 다양한 소스로부터 올 수 있습니다:
- Cognito User Pools.
- Cognito User Pools
- Third-party login providers.
- 외부 소셜 로그인 제공자
IAM policies associated with these temporary credentials are defined within the Identity Pool and can be customized based on the user's identity for fine-grained access control.
이 임시 자격증명과 관련된 IAM 정책은 Identity Pool 내에서 정의되며, 사용자 신원에 따라 세분화된 접근 제어를 위해 맞춤 설정 가능합니다.
> 핵심: 세밀한 접근 제어

A default IAM role can be assigned for guest or authenticated users without specific roles.
기본 IAM 역할은 특정 역할이 없는 게스트 또는 인증 사용자에게 할당될 수 있습니다.
> 핵심: 기본 역할 제공

## Example Use Case: Direct AWS Resource Access
## 사용 사례: AWS 리소스 직접 접근
> 실전 예시

Consider a web or mobile application that needs to access an S3 bucket or a DynamoDB table directly.
S3 버킷이나 DynamoDB 테이블에 직접 접근해야 하는 웹/모바일 애플리케이션을 생각해보세요.
- The application logs in via Cognito User Pools, a social identity provider, SAML, or OpenID Connect.
- 애플리케이션이 Cognito User Pools, 소셜 로그인, SAML 또는 OpenID Connect를 통해 로그인합니다.
- The application receives a token.
- 애플리케이션이 토큰을 받습니다.
- The token is passed to the Cognito Identity Pool service.
- 토큰이 Cognito Identity Pool로 전달됩니다.
- The Identity Pool validates the token.
- Identity Pool이 토큰을 검증합니다.
- The Identity Pool generates an IAM policy specific to the user.
- Identity Pool이 사용자별 IAM 정책을 생성합니다.
- Temporary AWS credentials with this policy are issued.
- 해당 정책을 가진 임시 AWS 자격증명이 발급됩니다.
- The application uses these credentials to access AWS resources directly, bypassing API Gateway or ALB.
- 애플리케이션이 이 자격증명을 사용하여 AWS 리소스에 직접 접근합니다.

This setup enables scenarios such as row-level security in DynamoDB, where access is restricted to items matching the Cognito identity user ID.
이 설정은 DynamoDB에서 행 단위 보안(row-level security)과 같이, Cognito 사용자 ID와 일치하는 항목만 접근할 수 있는 시나리오를 가능하게 합니다.
> 핵심: 세밀한 접근 제어

## Row-Level Security in DynamoDB
## DynamoDB 행 단위 보안
> 세부 권한 관리

Using Cognito Identity Pools, you can enforce row-level security by crafting IAM policies with conditions.
Cognito Identity Pools를 사용하면 조건이 포함된 IAM 정책을 만들어 행 단위 보안을 적용할 수 있습니다.
> 핵심: 조건 기반 접근 제어

For example, a policy can specify that the leading key in DynamoDB must equal the Cognito identity user ID.
예를 들어, DynamoDB의 선행 키가 Cognito 사용자 ID와 같아야 한다고 정책을 지정할 수 있습니다.
> 핵심: 사용자별 접근 제한

This ensures that users can only read and write items they are authorized to access, preventing excessive permissions.
이로써 사용자가 접근 권한이 없는 항목을 읽거나 쓰지 못하도록 하여 과도한 권한을 방지합니다.
> 핵심: 권한 제한 보장

## Summary
## 요약
> Cognito의 핵심 기능 정리

Amazon Cognito is a complex but powerful service that enables you to:
Amazon Cognito는 복잡하지만 강력한 서비스로, 다음을 가능하게 합니다:
- Create and manage a user base for your web and mobile applications.
- 웹 및 모바일 앱 사용자 기반 생성 및 관리
- Enable fine-grained access control such as row-level security in DynamoDB.
- DynamoDB 행 단위 보안 등 세밀한 접근 제어 지원
- Integrate user authentication seamlessly with API Gateway and Application Load Balancer.
- API Gateway 및 ALB와 사용자 인증 원활 통합

Understanding these components at a high level is essential for implementing secure and scalable user authentication and authorization in AWS environments.
이 구성 요소를 높은
```


수준에서 이해하는 것은 AWS 환경에서 안전하고 확장 가능한 사용자 인증 및 권한 부여를 구현하는 데 필수적입니다.

> 핵심: 보안 인증/권한 구현 필수 지식

## Key Takeaways

## 핵심 요약

* Amazon Cognito provides identity management for users outside of AWS accounts, primarily for web and mobile applications.
* Amazon Cognito는 AWS 외부 사용자, 특히 웹/모바일 앱 사용자를 위한 신원 관리 서비스 제공
* Cognito consists of two main components: User Pools for user sign-in and Identity Pools for granting temporary AWS credentials.
* Cognito는 User Pools(로그인)과 Identity Pools(임시 AWS 자격증명) 두 구성 요소로 구성
* Cognito User Pools integrate with API Gateway and Application Load Balancer to authenticate users and pass verified identities to backend services.
* User Pools는 API Gateway 및 ALB와 통합되어 사용자 인증 및 신원 전달 지원
* Cognito Identity Pools enable direct AWS resource access with fine-grained permissions, supporting use cases like row-level security in DynamoDB.
* Identity Pools는 세밀한 권한으로 AWS 리소스 직접 접근 지원, DynamoDB 행 단위 보안 같은 시나리오 가능

```

🎮 **게임 보상 포인트:**  
- Cognito 개념 이해 = 10 XP  
- User Pools vs Identity Pools 차이 이해 = 10 XP  
- API Gateway/ALB 연동 개념 = 10 XP  
- Identity Pools를 통한 세밀한 AWS 리소스 접근 = 10 XP  
총: **40 XP**  
