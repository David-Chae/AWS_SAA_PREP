```markdown
# IAM - Policy Evaluation Logic  
# IAM - 정책 평가 로직  

## IAM Permission Boundaries  
## IAM 권한 경계  

Let's get into IAM Permission Boundaries. These permission boundaries are supported for users and roles but are not available for groups, so remember this. They are an advanced feature that allows you to define the maximum amount of permissions an IAM entity can get.  
IAM 권한 경계(IAM Permission Boundaries)에 대해 알아봅시다. 이 권한 경계는 사용자와 역할에는 적용되지만 그룹에는 적용되지 않으니 기억하세요. 이것은 IAM 엔티티가 가질 수 있는 최대 권한을 정의할 수 있는 고급 기능입니다.  
(권한 경계 정의 및 적용 대상 설명)  

For example, we have this IAM permission boundary. It looks just like an IAM policy. We are saying, allow everything on S3, CloudWatch, and EC2. We attach this, for example, to an IAM user, and that's its permission boundary. That means that it can only do things within S3, CloudWatch, and EC2. Then you need to specify on top of that an IAM permission through policy.  
예를 들어, 이 IAM 권한 경계를 생각해봅시다. 이것은 일반 IAM 정책과 거의 동일하게 보입니다. S3, CloudWatch, EC2에서 모든 작업을 허용한다고 정의합니다. 이를 IAM 사용자에게 첨부하면, 이것이 권한 경계가 됩니다. 즉, 해당 사용자는 S3, CloudWatch, EC2 안에서만 작업할 수 있습니다. 이후 추가로 정책을 통해 IAM 권한을 지정해야 합니다.  
(권한 경계와 IAM 정책의 관계 설명)  

So here, say we attach to the very same user an IAM policy that allows iam:CreateUser on a resource. There is a boundary and there is an IAM policy with permissions. What is going to be the resulting permission in this case? Nothing, no permissions because the IAM policy is outside the IAM permission boundary. Therefore, our user is not allowed to create other IAM users because that is not in its IAM permission boundary.  
예를 들어, 같은 사용자에게 iam:CreateUser 권한을 부여하는 IAM 정책을 첨부했다고 합시다. 권한 경계와 IAM 정책이 존재하는 상황입니다. 결과 권한은 무엇일까요? 아무것도 아닙니다. 권한이 부여되지 않습니다. 이유는 IAM 정책이 권한 경계 밖에 있기 때문입니다. 따라서 사용자는 다른 IAM 사용자를 생성할 수 없습니다.  
(권한 경계가 정책을 제한함을 설명)  

---

## Creating a User with Permission Boundaries  
## 권한 경계를 적용하여 사용자 생성  

Let's see where IAM permission boundaries are created. Let's go create a user. I'm going to call the user John, and then I'm going to give him programmatic access. Next, permissions. I will not set anything, then next tags, review, and create user. So we have created John, and we're going to set permission boundaries for John.  
IAM 권한 경계를 어디서 생성하는지 살펴봅시다. 사용자를 생성해보겠습니다. 사용자 이름은 John으로 하고, 프로그래밍 접근 권한을 부여합니다. 다음 단계에서 권한은 아무 것도 설정하지 않고, 태그, 검토 후 사용자 생성합니다. 이렇게 John이라는 사용자가 생성되었고, 이제 John에게 권한 경계를 설정할 것입니다.  
(사용자 생성 및 권한 경계 설정 준비)  

Imagine John is a developer in our company and he needs to have certain permissions, but we want to make sure that he has a permission boundary. For this, we could assign a policy, for example, for John. If I add permission and say, "Hey, John, I'm going to attach to you AdministratorAccess," it seems like John can do everything right now. John is a super user.  
John이 우리 회사의 개발자라고 가정해봅시다. 특정 권한이 필요하지만, 권한 경계를 설정하고 싶습니다. 이를 위해 John에게 정책을 할당할 수 있습니다. 예를 들어 AdministratorAccess 정책을 첨부하면, John은 지금 모든 것을 수행할 수 있는 슈퍼 유저처럼 보입니다.  
(정책과 권한 경계의 차이 이해)  

But I'm also going to set a permission boundary on John. I'm going to say, okay, here is your boundary, and this is an advanced feature. I'm going to say the only thing you can do, actually, John, is to have AmazonS3FullAccess. So here, what I've been setting is a permission boundary for John.  
하지만 John에게 권한 경계도 설정할 것입니다. 여기서 경계를 정의하고, John이 할 수 있는 것은 AmazonS3FullAccess뿐이라고 설정합니다. 이렇게 해서 John의 권한 경계를 설정했습니다.  
(권한 경계를 통한 제한 적용)  

Through this AWS S3 full access managed policy, even though John has AdministratorAccess, when John logs in, the only thing he can do is access S3 because S3 is his boundary. So here we've seen that even though there is a policy attached to John that gives him AdministratorAccess, the boundary is actually going to be more restrictive.  
이 AWS S3 전체 액세스 관리 정책을 통해, John이 AdministratorAccess를 가지고 있어도 로그인 시 S3에만 접근할 수 있습니다. 권한 경계가 정책보다 더 제한적임을 확인할 수 있습니다.  
(권한 경계가 정책보다 우선함 강조)  

---

## Combining Permission Boundaries with AWS Organizations SCP  
## 권한 경계를 AWS Organizations SCP와 결합  

IAM permission boundaries can be used in combination with AWS Organizations Service Control Policies (SCP). Looking at this diagram, we have the effective permissions in the middle, which are determined by your identity-based policy (whatever is attached to your user or your group), the permission boundary (which only applies to a user or a role and not a group), and your organization SCP, which applies to every single IAM entity in your account.  
IAM 권한 경계는 AWS Organizations의 서비스 제어 정책(SCP)과 결합하여 사용할 수 있습니다. 다이어그램을 보면, 가운데에는 실제 권한이 있습니다. 이는 사용자 또는 그룹에 첨부된 ID 기반 정책, 권한 경계(사용자나 역할에만 적용), 조직 SCP(계정 내 모든 IAM 엔티티에 적용)에 의해 결정됩니다.  
(권한 경계와 SCP의 결합 이해)  

In the middle lies what the users can do. We can use permission boundaries for a few use cases, for example, to delegate responsibilities to non-administrators within their permission boundaries, such as creating new IAM users. Or to allow developers to self-assign and manage their own permissions while making sure they cannot escalate their privileges, meaning they cannot make themselves administrators. Or, for example, restrict one very specific user inside your organization instead of applying an entire SCP to your account and restricting everyone in your whole account.  
가운데는 사용자가 실제로 수행할 수 있는 작업입니다. 권한 경계는 몇 가지 사례에서 활용될 수 있습니다. 예: 권한 경계 내에서 비관리자에게 IAM 사용자 생성 같은 책임을 위임, 개발자가 스스로 권한을 관리하도록 허용하면서 관리자 권한 상승을 막기, 특정 사용자만 제한하고 전체 계정에 SCP를 적용하지 않는 경우 등.  
(권한 경계 활용 사례)  

---

## IAM Policy Evaluation Logic  
## IAM 정책 평가 로직  

Let's have a look at the IAM Policy Evaluation Logic. This diagram basically explains how you are authorized, or not, to perform actions within AWS. You don't need to memorize it, but it should make sense to you. There is a whole flow, and at every step, there is an evaluation.  
IAM 정책 평가 로직을 살펴봅시다. 이 다이어그램은 AWS 내에서 작업 수행 권한이 있는지 없는지를 설명합니다. 외울 필요는 없지만, 의미를 이해해야 합니다. 전체 흐름이 있으며, 각 단계마다 평가가 이루어집니다.  
(평가 로직 개요 설명)  

We look at deny evaluation, Organizations SCP, resource-based policy, identity-based policy, IAM permission boundaries, and finally session policies to allow or deny a specific IAM action. Let's look in detail to see how that works.  
Deny 평가, Organizations SCP, 리소스 기반 정책, ID 기반 정책, IAM 권한 경계, 세션 정책을 통해 특정 IAM 작업의 허용/거부가 결정됩니다. 세부적으로 살펴보겠습니다.  
(평가 과정 단계)  

We check all possible policies. If there is an explicit deny, then it is denied automatically. Then we look at the Organizations SCP: is there an allow? If yes, then go to the next step; if not, then it's a deny because it is an implicit deny. Then we look at resource-based policies, for example, applied to S3 buckets or SQS. Again, we check if there is an allow. Then we look at identity-based policies to see if there is an allow or implicit deny. Then we look at IAM permission boundaries, and finally session policies (which are more related to STS).  
모든 가능한 정책을 확인합니다. 명시적 거부가 있으면 자동으로 거부됩니다. 그다음 Organizations SCP를 확인하고 허용 여부를 판단합니다. 허용이면 다음 단계로, 아니면 암묵적 거부로 처리됩니다. 이후 S3, SQS 등에 적용된 리소스 기반 정책, ID 기반 정책, IAM 권한 경계, 마지막으로 세션 정책(STS 관련)을 확인합니다.  
(정책 평가 단계 상세)  

All these things are evaluated when making a specific IAM action. Only if all these things allow the action and do not explicitly deny it, then you will have a final decision of allow, and you will be able to perform your action. This overview helps you understand how security works in AWS.  
모든 요소가 평가된 후에야 특정 IAM 작업 수행 여부가 결정됩니다. 모든 요소가 허용하고 명시적 거부가 없을 때만 최종적으로 허용되며, 작업을 수행할 수 있습니다. 이 개요는 AWS 보안 작동 원리를 이해하는 데 도움이 됩니다.  
(정책 평가 결론)  

---

## Policy Example  
## 정책 예제  

Let's look at this policy to make it more concrete. We have sqs:* deny on resource
```


, and we have action sqs\:DeleteQueue allow on resource. First question: can you perform sqs\:CreateQueue? The answer is no, because there is a deny on sqs:*, and CreateQueue belongs to that block, so it is definitely denied.
정책을 좀 더 구체적으로 살펴봅시다. 리소스에 sqs:* 거부가 있고, sqs\:DeleteQueue 허용이 있습니다. 질문: sqs\:CreateQueue를 수행할 수 있을까요? 답은 아니오입니다. sqs:\*에 거부가 있으며 CreateQueue도 포함되므로 명확히 거부됩니다.
(명시적 거부 우선)

Now, can you perform sqs\:DeleteQueue? There is a deny on the top part and an allow on the bottom part, so they conflict. However, as mentioned, an explicit deny overrides any allow. Because there is an explicit deny on sqs:\* and sqs\:DeleteQueue is within that, this action is denied regardless of the allow. So you cannot perform sqs\:DeleteQueue even though it is explicitly allowed in the second block.
그럼 sqs\:DeleteQueue는 수행할 수 있을까요? 상단은 거부, 하단은 허용으로 충돌합니다. 하지만 명시적 거부는 모든 허용을 무시합니다. sqs:\*에 명시적 거부가 있고 DeleteQueue가 포함되므로 허용 여부와 상관없이 거부됩니다.
(명시적 거부 우선 규칙 예시)

Finally, can you perform ec2\:DescribeInstances? There is nothing on EC2 in this policy. Since there is no explicit deny but also no explicit allow, you cannot perform ec2\:DescribeInstances with this IAM policy.
마지막으로 ec2\:DescribeInstances를 수행할 수 있을까요? 정책에 EC2 관련 내용이 없습니다. 명시적 거부도 없고 허용도 없으므로, 해당 IAM 정책으로 수행할 수 없습니다.
(명시적 허용/거부 없을 시 암묵적 거부)

---

## Key Takeaways

## 핵심 요약

* IAM permission boundaries define the maximum permissions an IAM user or role can have, restricting actions beyond the boundary.

* IAM 권한 경계는 IAM 사용자나 역할이 가질 수 있는 최대 권한을 정의하며, 경계 밖의 작업은 제한합니다.

* Permission boundaries apply only to users and roles, not groups.

* 권한 경계는 사용자와 역할에만 적용되며, 그룹에는 적용되지 않습니다.

* Effective permissions are determined by the combination of identity-based policies, permission boundaries, organization SCPs, resource-based policies, and session policies.

* 실제 권한은 ID 기반 정책, 권한 경계, 조직 SCP, 리소스 기반 정책, 세션 정책의 결합으로 결정됩니다.

* Explicit deny policies always override allow policies, resulting in denied access even if an allow exists.

* 명시적 거부 정책은 항상 허용 정책을 무시하여, 허용이 있더라도 접근이 거부됩니다.

```

게임보상: 🛡️ IAM 정책 마스터! 권한 경계와 평가 로직 완전 정복! 🎯✅
```
