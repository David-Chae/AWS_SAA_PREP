```markdown
# AWS Directory Services - Hands On  
# AWS 디렉터리 서비스 - 실습  

If you go to the AWS console and type "Directory Service," you will see the different options offered to us.  
AWS 콘솔에서 "Directory Service"를 입력하면 제공되는 다양한 옵션을 볼 수 있습니다.  
(콘솔 탐색 방법 설명)  

I will go through them at a high level because they can be complicated to set up individually.  
개별 설정이 복잡할 수 있으므로, 여기서는 높은 수준에서 개요만 살펴보겠습니다.  
(전체 개요 강조)  

We have four options, and actually the fourth one is Amazon Cognito User Pool, which redirects you to the Cognito service. Therefore, do not count this as part of Directory Services.  
옵션은 네 가지가 있으며, 사실 네 번째는 Amazon Cognito User Pool로 Cognito 서비스로 이동합니다. 따라서 디렉터리 서비스의 일부로는 포함하지 않습니다.  
(옵션 구분)  

The first option is AWS Managed Microsoft Active Directory, where you can have an Active Directory integrated with AWS Cloud and establish a trust relationship with your on-premise directory.  
첫 번째 옵션은 AWS 관리형 Microsoft Active Directory로, AWS 클라우드와 통합된 AD를 사용하고 온프레미스 디렉터리와 트러스트 관계를 설정할 수 있습니다.  
(Managed AD 기능 설명)  

To set it up, you can choose between two editions: the Standard Edition, which supports up to 30,000 objects, or the Enterprise Edition, which supports up to 500,000 objects, offering much more capacity.  
설정 시, 두 가지 에디션 중 선택할 수 있습니다: 최대 30,000 객체를 지원하는 Standard Edition, 또는 최대 500,000 객체를 지원하는 Enterprise Edition으로 더 많은 용량 제공  
(에디션 비교)  

The setup process is more Active Directory specific, and it is not necessary to know the details for the exam.  
설정 과정은 AD 특화 사항이며, 시험에서는 세부 사항을 알 필요는 없습니다.  
(시험 대비 안내)  

The next option is Simple AD, which is a standalone managed directory that has an Active Directory-compatible API but cannot be connected to your on-premise Active Directory.  
다음 옵션은 Simple AD로, 독립형 관리 디렉터리이며 AD 호환 API를 제공하지만 온프레미스 AD와 연결할 수 없습니다.  
(Simple AD 특징)  

Another option is AD Connector, which acts as a proxy to redirect directory requests to your existing Microsoft Active Directory on-premise.  
또 다른 옵션은 AD 커넥터로, 디렉터리 요청을 기존 온프레미스 Microsoft AD로 전달하는 프록시 역할을 합니다.  
(AD Connector 역할)  

AD Connector is designed with two levels: one connector supports up to 500 users, and another supports up to 5,000 users.  
AD 커넥터는 두 가지 수준으로 설계되었습니다: 하나는 최대 500명, 다른 하나는 최대 5,000명 사용자 지원  
(사용자 수 제한)  

Remember, the AWS Managed Microsoft Active Directory supports multi-factor authentication (MFA), Simple AD is standalone, and AD Connector functions as a proxy.  
기억하세요: AWS 관리형 Microsoft AD는 MFA를 지원, Simple AD는 독립형, AD 커넥터는 프록시 역할 수행  
(주요 기능 요약)  

That concludes this lecture. I will see you in the next lecture.  
이 강의를 여기서 마치겠습니다. 다음 강의에서 뵙겠습니다.  
(강의 종료)  

---

## Key Takeaways  
## 핵심 요약  

- AWS Directory Services offers multiple options including AWS Managed Microsoft AD, Simple AD, and AD Connector.  
- AWS 디렉터리 서비스는 AWS 관리형 Microsoft AD, Simple AD, AD 커넥터 등 다양한 옵션을 제공합니다.  

- AWS Managed Microsoft AD supports integration with AWS Cloud and trust relationships with on-premise directories, available in Standard and Enterprise editions.  
- AWS 관리형 Microsoft AD는 AWS 클라우드와 통합 및 온프레미스 디렉터리와의 트러스트 관계를 지원하며, Standard 및 Enterprise 에디션에서 사용 가능합니다.  

- Simple AD is a standalone managed directory with Active Directory-compatible API but cannot connect to on-premise Active Directory.  
- Simple AD는 AD 호환 API를 제공하는 독립형 관리 디렉터리이지만, 온프레미스 AD와 연결할 수 없습니다.  

- AD Connector acts as a proxy to redirect directory requests to an existing on-premise Microsoft Active Directory, with user limits depending on the connector type.  
- AD 커넥터는 기존 온프레미스 Microsoft AD로 디렉터리 요청을 전달하는 프록시 역할을 하며, 커넥터 유형에 따라 사용자 수 제한이 있습니다.  
```

게임보상: 🖥️ AWS Directory Services 실습 마스터! Managed AD, Simple AD, AD Connector 완전 정복! 🔑🎮
