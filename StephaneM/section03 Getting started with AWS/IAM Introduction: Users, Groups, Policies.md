```markdown
# IAM Introduction: Users, Groups, Policies  
# IAM 소개: 사용자, 그룹, 정책  
→ AWS의 IAM 서비스와 사용자, 그룹, 정책 개념을 소개하는 강의입니다.  

Welcome to the first deep dive on an AWS service called IAM. IAM stands for Identity and Access Management.  
AWS 서비스 중 하나인 IAM(Identity and Access Management)에 대한 첫 심층 학습에 오신 것을 환영합니다.  
→ IAM은 AWS 계정의 사용자와 권한을 관리하는 서비스입니다.  

It is a global service because in IAM, we create users and assign them to groups.  
IAM은 글로벌 서비스입니다. 왜냐하면 여기서 사용자를 만들고 그룹에 할당하기 때문입니다.  
→ IAM은 리전과 무관하게 전역적으로 관리됩니다.  

We have already used IAM without knowing it when we created an account.  
계정을 만들 때 우리는 이미 IAM을 사용했지만, 그것을 인식하지 못했습니다.  
→ 계정 생성 시 루트 계정이 IAM 사용자로 자동 생성됩니다.  

The root account is created by default. This is the root user of our account.  
루트 계정은 기본적으로 생성되며, 이것이 계정의 루트 사용자입니다.  
→ 루트 계정은 AWS 계정 전체 권한을 가진 관리자 계정입니다.  

The only thing you should use it for is to set up your account, as we will do now.  
루트 계정은 계정을 설정할 때만 사용해야 하며, 지금 그렇게 진행할 것입니다.  
→ 초기 설정 후에는 일반 사용에 루트 계정을 쓰지 않아야 합니다.  

After that, you should not use or share that account anymore.  
그 이후에는 이 계정을 사용하거나 공유해서는 안 됩니다.  
→ 보안상 루트 계정은 최소한으로만 사용합니다.  

Instead, you should create users. You create users in IAM, and one user represents one person within your organization.  
대신 사용자 계정을 만들어야 합니다. IAM에서 사용자를 생성하며, 한 사용자는 조직 내 한 사람을 나타냅니다.  
→ 개인별 계정 관리 원칙입니다.  

Users can be grouped together if it makes sense.  
필요에 따라 사용자들을 그룹으로 묶을 수 있습니다.  
→ 역할별 그룹화를 통해 권한 관리가 편리해집니다.  

For example, suppose we have an organization with six people: Alice, Bob, Charles, David, Edward, and Fred. All these people are in your organization.  
예를 들어, 조직에 Alice, Bob, Charles, David, Edward, Fred 여섯 명이 있다고 가정해봅시다.  
→ 예시 조직 구성입니다.  

Alice, Bob, and Charles work together as developers. We will create a group called "developers" that includes Alice, Bob, and Charles.  
Alice, Bob, Charles는 개발자로 함께 일합니다. 이들을 포함한 "developers" 그룹을 만듭니다.  
→ 역할 기반 그룹 예시.  

David and Edward also work together, so we will create an "operations" group for them.  
David와 Edward도 함께 일하므로, 이들을 위한 "operations" 그룹을 생성합니다.  
→ 또 다른 팀 그룹 예시.  

Now we have two groups within IAM. It is important to understand that groups can only contain users, not other groups.  
이제 IAM 내에 두 개의 그룹이 있습니다. 그룹은 사용자만 포함할 수 있고, 다른 그룹은 포함할 수 없다는 점을 이해하는 것이 중요합니다.  
→ 그룹 중첩은 허용되지 않습니다.  

Some users do not have to belong to a group. For example, Fred is alone and does not belong to any group.  
일부 사용자는 그룹에 속하지 않아도 됩니다. 예를 들어, Fred는 혼자이며 어떤 그룹에도 속하지 않습니다.  
→ 권장 사항은 아니지만 가능함.  

Although this is not best practice, it is possible in AWS.  
비록 권장되는 방법은 아니지만 AWS에서는 가능합니다.  
→ 실제 운영에서는 최소 권한 원칙 권장.  

Also, a user can belong to multiple groups. For instance, if Charles and David work together as part of an audit team, you can create a third group with Charles and David.  
또한 한 사용자가 여러 그룹에 속할 수 있습니다. 예를 들어, Charles와 David가 감사팀으로 함께 일한다면, 이들을 포함한 세 번째 그룹을 만들 수 있습니다.  
→ 다중 그룹 소속 가능 예시.  

In this example, Charles and David belong to two different groups.  
이 예시에서 Charles와 David는 두 개의 서로 다른 그룹에 속합니다.  
→ 유연한 권한 관리 가능.  

This illustrates the possible configurations for IAM users and groups.  
이 예시는 IAM 사용자와 그룹의 가능한 구성 방법을 보여줍니다.  
→ 구조 이해용 그림 또는 예시 설명.  

---

## Why do we create users and groups?  
## 왜 사용자와 그룹을 만드는가?  
→ 권한 관리를 위해 사용자와 그룹을 생성합니다.  

Because we want to allow them to use our AWS accounts. To do so, we have to give them permissions.  
사용자가 AWS 계정을 사용할 수 있도록 권한을 부여해야 하기 때문입니다.  
→ IAM 정책을 통해 권한 제어.  

Users or groups can be assigned a JSON document called a policy. This is an IAM policy.  
사용자나 그룹에 JSON 문서 형태의 정책(Policy)을 부여할 수 있습니다. 이것이 IAM 정책입니다.  
→ 정책은 JSON 형식으로 권한을 정의합니다.  

It looks like this. You do not have to be a programmer; this is not programming. It is just describing in plain English what a user or group is allowed to do.  
정책은 이렇게 생겼습니다. 프로그래밍 지식이 필요 없으며, 사용자나 그룹이 할 수 있는 행동을 단순히 기술한 것입니다.  
→ 쉽게 이해 가능한 권한 정의 문서.  

For example, this policy allows people to use the EC2 service and perform describe actions on it, use the Elastic Load Balancing service and describe it, and use CloudWatch.  
예를 들어, 이 정책은 EC2 서비스 사용 및 조회, Elastic Load Balancing 서비스 사용 및 조회, CloudWatch 사용을 허용합니다.  
→ 실제 AWS 서비스 접근 권한 예시.  

We will see what EC2, Elastic Load Balancing, and CloudWatch mean later.  
EC2, Elastic Load Balancing, CloudWatch가 무엇인지 나중에 다룹니다.  
→ 서비스 용어 학습은 추후 강의에서.  

Through this JSON document, we allow our users to use some AWS services.  
이 JSON 문서를 통해 사용자가 일부 AWS 서비스를 사용할 수 있도록 허용합니다.  
→ 정책이 사용자 권한을 제어하는 핵심 역할을 합니다.  

These policies help us define the permissions of our users.  
이 정책들은 사용자 권한을 정의하는 데 도움을 줍니다.  
→ IAM의 핵심 목적: 최소 권한 부여.  

In AWS, you do not allow everyone to do everything because that would be catastrophic.  
AWS에서는 모든 사용자에게 모든 권한을 부여하지 않습니다. 그렇게 하면 심각한 문제가 발생할 수 있습니다.  
→ 권한 남용 방지 필요.  

A new user could launch many services that would cost a lot of money or cause security issues.  
새로운 사용자가 많은 서비스를 실행하면 비용이 많이 들거나 보안 문제가 생길 수 있습니다.  
→ 실제 사례 대비.  

Therefore, AWS applies the principle of least privilege.  
따라서 AWS는 최소 권한 원칙을 적용합니다.  
→ 최소 권한 원칙 = 꼭 필요한 권한만 부여.  

You do not give more permissions than a user needs. If a user only needs access to three services, create a permission for only those services.  
사용자가 필요한 권한보다 더 많은 권한을 주지 않습니다. 예를 들어, 세 서비스만 필요하다면 그 세 서비스에 대한 권한만 부여합니다.  
→ 실무에서 권한 설계 핵심.  

We have now seen an overview of IAM. In the next lecture, we will practice creating users and groups.  
이제 IAM 개요를 살펴보았습니다. 다음 강의에서는 사용자와 그룹 생성 실습을 진행합니다.  
→ 실습 예고.  

---

## Key Takeaways  
## 핵심 요약  
→ IAM 학습에서 반드시 기억할 내용입니다.  

- IAM stands for Identity and Access Management and is a global AWS service for managing users and groups.  
- IAM은 Identity and Access Management의 약자로, 사용자와 그룹을 관리하는 글로벌 AWS 서비스입니다.  
→ 서비스 정의.  

- The root user is created by default and should only be used for initial account setup, not regular use.  
- 루트 사용자는 기본 생성되며, 초기 계정 설정에만 사용해야 하며, 일상적으로 사용하지 않아야 합니다.  
→ 루트 계정 보안 원칙.  

- Users represent individual people and can be organized into groups; groups contain only users, not other groups.  
- 사용자는 개별 사람을 나타내며 그룹으로 조직할 수 있습니다. 그룹은 사용자만 포함하고 다른 그룹은 포함하지 않습니다.  
→ 그룹 구성 규칙.  

- Permissions are assigned via JSON-based IAM policies following the least privilege principle to restrict user access appropriately.  
- 권한은 최소 권한 원칙에 따라 JSON 기반 IAM 정책으로 부여되어 사용자 접근을 적절히 제한합니다.  
→ 권한 관리 핵심 요약.  
```

---

✅ 게임보상: 경험치 +70 (IAM 이해도 +1)

