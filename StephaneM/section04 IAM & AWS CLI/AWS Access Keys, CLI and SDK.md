
# AWS Access Keys, CLI and SDK  
# AWS 액세스 키, CLI 및 SDK  
→ 이 문서는 AWS에 접근하는 세 가지 주요 방법(콘솔, CLI, SDK)과 액세스 키 관리에 대해 설명합니다.  

---

## Introduction to AWS Access Methods  
## AWS 접근 방법 소개  
→ AWS에 접근할 수 있는 다양한 방법을 개괄적으로 설명하는 부분입니다.  

We have seen how to access AWS using the Management Console, which is the web interface covered so far in this course. However, there are actually three different options to access AWS.  
우리는 지금까지 웹 인터페이스인 관리 콘솔을 통해 AWS에 접근하는 방법을 살펴보았습니다. 하지만 실제로 AWS에 접근하는 방법은 세 가지가 있습니다.  
→ 관리 콘솔만 있는 것이 아니라 CLI, SDK까지 포함해 세 가지 방법이 있음을 설명합니다.  

The first option is the Management Console, protected by your username, password, and possibly multifactor authentication.  
첫 번째 방법은 관리 콘솔로, 사용자 이름, 비밀번호, 그리고 다단계 인증으로 보호됩니다.  
→ 일반적인 웹 로그인 방식으로 접근하는 방법입니다.  

The second option is the CLI, or Command Line Interface, which we will set up on our computer. This is protected by access keys, credentials that we will download shortly, allowing us to access AWS from our terminal.  
두 번째 방법은 CLI(명령줄 인터페이스)로, 컴퓨터에 설치하여 사용합니다. 이는 액세스 키로 보호되며, 이 키를 다운로드해 터미널에서 AWS에 접근할 수 있습니다.  
→ CLI는 터미널에서 명령어로 AWS를 다루는 방식입니다.  

The third option is the SDK, the AWS Software Development Kit, used whenever you want to call AWS APIs from within your application code. These are also protected by the same access keys.  
세 번째 방법은 SDK(소프트웨어 개발 키트)로, 애플리케이션 코드에서 AWS API를 호출할 때 사용합니다. 이것 또한 액세스 키로 보호됩니다.  
→ SDK는 코드 내에서 API 호출을 가능하게 하여 개발자가 AWS 서비스를 연동할 수 있게 해줍니다.  

---

## Generating and Managing Access Keys  
## 액세스 키 생성 및 관리  
→ CLI와 SDK에서 필요한 액세스 키 관리 방법을 설명합니다.  

Access keys are generated through the Management Console. Users are responsible for their own access keys, which are secret like passwords. If you generate your own access keys, do not share them with colleagues because they can generate their own access keys as well.  
액세스 키는 관리 콘솔에서 생성됩니다. 사용자는 자신의 액세스 키를 책임져야 하며, 이는 비밀번호처럼 비밀스럽게 다루어야 합니다. 액세스 키를 만들었다면 동료와 공유하지 마십시오. 그들도 각자 자신의 액세스 키를 만들 수 있습니다.  
→ 액세스 키는 개인 전용이며, 공유 금지 원칙을 강조합니다.  

Treat your access key ID like your username and your secret access key like your password. Do not share them with others.  
액세스 키 ID는 사용자 이름처럼, 시크릿 액세스 키는 비밀번호처럼 다뤄야 합니다. 절대 타인과 공유하지 마십시오.  
→ 키 유출은 계정 보안 위험으로 직결됩니다.  

When you go into the Management Console, there is a button to create access keys. Once created, you have the right to download them immediately. For example, here is a fake access key ID and a fake secret access key. When loaded into the Command Line Interface, these would allow access to the AWS API.  
관리 콘솔에 들어가면 액세스 키 생성 버튼이 있습니다. 키를 생성하면 즉시 다운로드할 수 있습니다. 예를 들어, 가짜 액세스 키 ID와 시크릿 액세스 키를 보여줄 수 있습니다. 이를 CLI에 입력하면 AWS API에 접근할 수 있습니다.  
→ 실제 키 대신 예시를 사용하여 설명하는 부분입니다.  

Remember, to avoid any security issues during this course or at work, do not share your access keys as they are private to you.  
이 강의 중이든 업무 중이든 보안 문제를 피하기 위해, 액세스 키는 반드시 본인만 사용해야 합니다.  
→ 보안 수칙 강조.  

---

## Understanding the AWS CLI  
## AWS CLI 이해하기  
→ CLI의 개념과 장점을 소개합니다.  

If you are new to the cloud, programming, or IT, you might not know what a CLI is. CLI stands for Command Line Interface. The AWS CLI is a tool that allows you to interact with AWS services using commands from your command-line shell.  
클라우드, 프로그래밍, 또는 IT가 처음이라면 CLI가 무엇인지 모를 수도 있습니다. CLI는 명령줄 인터페이스의 약자입니다. AWS CLI는 터미널 명령어를 통해 AWS 서비스를 다룰 수 있게 해주는 도구입니다.  
→ CLI는 콘솔 대신 명령어 기반으로 AWS를 다루는 도구입니다.  

Whenever you see code where you type a command line and it returns a result, for example, aws s3 cp, this is the CLI. We use the AWS CLI because every command starts with the word aws.  
명령줄에 aws s3 cp 같은 코드를 입력하고 결과가 출력된다면, 이것이 CLI입니다. AWS CLI의 모든 명령어는 `aws`라는 단어로 시작합니다.  
→ CLI 사용 예시를 보여줍니다.  

With the CLI, you get direct access to the public APIs of your AWS services, which is very helpful in this course. Using the CLI, you can develop scripts to manage your resources and automate tasks.  
CLI를 사용하면 AWS 서비스의 공개 API에 직접 접근할 수 있으며, 이는 학습 과정에서 매우 유용합니다. CLI로 스크립트를 작성해 리소스를 관리하고 작업을 자동화할 수 있습니다.  
→ CLI의 자동화 기능이 핵심 장점입니다.  

The CLI is open-source, with all source code available on GitHub. It is an alternative to using the AWS Management Console. Some people only use the CLI and never use the Management Console.  
CLI는 오픈소스로, 전체 소스 코드가 GitHub에서 제공됩니다. 관리 콘솔의 대체제로 사용할 수 있으며, 어떤 사람들은 CLI만 쓰고 관리 콘솔은 전혀 사용하지 않기도 합니다.  
→ CLI가 고급 사용자들에게 인기 있는 이유를 설명합니다.  

---

## Overview of the AWS SDK  
## AWS SDK 개요  
→ SDK의 특징과 언어별 지원 범위를 설명합니다.  

SDK stands for Software Development Kit. It is a set of libraries that are language-specific. You will have an SDK for different programming languages.  
SDK는 소프트웨어 개발 키트의 약자로, 언어별 라이브러리 모음입니다. 각 프로그래밍 언어에 맞는 SDK가 존재합니다.  
→ 언어 맞춤형 라이브러리를 제공.  

The SDK allows you to access and manage your AWS services and APIs programmatically. Unlike the CLI, the SDK is not used within your terminal but embedded within the application code you write.  
SDK는 프로그램 코드에서 AWS 서비스와 API에 접근하고 관리할 수 있도록 해줍니다. CLI와 달리 터미널이 아닌, 작성하는 애플리케이션 코드 내부에서 사용됩니다.  
→ SDK는 코드 기반 접근 방식입니다.  

Your application will include the AWS SDK to interact with AWS services.  
애플리케이션에 AWS SDK를 포함시켜 AWS 서비스와 상호작용합니다.  
→ SDK는 애플리케이션 통합에 활용됩니다.  

The AWS SDK supports many programming languages such as JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, and C++. There is also a mobile SDK for Android and iOS, and an IoT SDK for Internet of Things devices like thermal sensors or connected backlogs.  
AWS SDK는 JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++ 등 다양한 언어를 지원합니다. 또한 안드로이드와 iOS용 모바일 SDK, IoT 기기를 위한 IoT SDK도 있습니다.  
→ SDK는 범용적이며 다양한 환경을 지원합니다.  

To give an example of what you can build with the SDK, the AWS CLI that we will use in this course is actually built on the AWS SDK for Python, named Boto.  
SDK로 무엇을 만들 수 있는지 예로 들자면, 우리가 이 강의에서 사용할 AWS CLI는 사실 Python용 AWS SDK인 Boto로 만들어졌습니다.  
→ CLI조차 SDK 기반으로 만들어졌음을 보여줍니다.  

---

## Conclusion and Next Steps  
## 결론 및 다음 단계  
→ 강의 정리와 다음 학습 예고.  

That concludes this lecture. In the next lecture, we will practice setting up the CLI and managing access keys. I look forward to seeing you then.  
이번 강의를 마치겠습니다. 다음 강의에서는 CLI 설정과 액세스 키 관리를 실습하겠습니다. 곧 다시 뵙기를 기대합니다.  
→ 강의 마무리 및 예고.  

---

## Key Takeaways  
## 핵심 요약  
→ 이번 강의에서 꼭 기억해야 할 내용 정리.  

- AWS can be accessed via three methods: Management Console, CLI, and SDK.  
- AWS는 관리 콘솔, CLI, SDK 세 가지 방법으로 접근할 수 있습니다.  
→ 세 가지 접근 방법.  

- Access keys are essential credentials for CLI and SDK access and must be kept private.  
- 액세스 키는 CLI와 SDK 접근에 필수적인 자격 증명이며 반드시 비밀로 유지해야 합니다.  
→ 액세스 키 보안 중요.  

- The AWS CLI allows command-line interaction with AWS services and supports automation.  
- AWS CLI는 명령줄로 AWS 서비스와 상호작용하며, 자동화를 지원합니다.  
→ CLI 장점 요약.  

- The AWS SDK provides language-specific libraries to programmatically interact with AWS services within applications.  
- AWS SDK는 언어별 라이브러리를 제공하여 애플리케이션 내부에서 프로그래밍적으로 AWS 서비스와 상호작용할 수 있게 합니다.  
→ SDK 장점 요약.  
