```markdown
# AWS Config - Hands On  
# AWS Config - 실습  

## Introduction to AWS Config Service  
## AWS Config 서비스 소개  
Let's begin by exploring the AWS Config service and start configuring it.  
AWS Config 서비스를 탐색하고 구성하는 것부터 시작합시다.  
(실습 시작 안내)  

I am going to click on Get Started to initiate recording some settings.  
설정을 기록하기 위해 'Get Started'를 클릭하겠습니다.  
(설정 기록 시작)  

We will record all the resources supported in this region. However, if desired, you can record only specific resource types.  
이 리전에서 지원되는 모든 리소스를 기록할 것입니다. 원하면 특정 리소스 유형만 기록할 수도 있습니다.  
(전체 또는 선택적 리소스 기록 가능)  

In that case, you can find resource categories and resource types on the right-hand side.  
그 경우, 오른쪽에서 리소스 카테고리와 유형을 확인할 수 있습니다.  
(리소스 선택 방법 안내)  

Because I want to show you all the resources I can record, I will select to record all resources.  
기록할 수 있는 모든 리소스를 보여주기 위해 '모든 리소스 기록'을 선택합니다.  
(전체 리소스 기록 선택)  

Additionally, you can include global resources such as IAM users, groups, roles, and customer managed policies.  
또한, IAM 사용자, 그룹, 역할, 고객 관리 정책과 같은 글로벌 리소스도 포함할 수 있습니다.  
(글로벌 리소스 포함)  

Be aware that AWS Config is not a free feature. The more resources you record, the more you will pay.  
AWS Config는 무료 기능이 아닙니다. 기록하는 리소스가 많을수록 비용이 증가합니다.  
(비용 경고)  

I am demonstrating everything here, but if you want to avoid charges from this course, please do not follow along with this hands-on.  
여기서는 모든 것을 시연하지만, 비용을 피하고 싶다면 실습을 따라 하지 마세요.  
(실습 주의)  

We will record our resources including global resources. To record all resource configurations, we need to create a Config service-linked role. Let's click on that option.  
글로벌 리소스를 포함하여 모든 리소스를 기록하기 위해 Config 서비스 연결 역할을 생성해야 합니다. 해당 옵션을 클릭합니다.  
(서비스 역할 생성)  

All this information will be delivered into an Amazon S3 bucket. The bucket name is already entered for me, which is perfect.  
모든 정보는 Amazon S3 버킷에 저장됩니다. 버킷 이름이 이미 입력되어 있습니다.  
(S3 저장 위치 안내)  

You can also specify a prefix if you want. This is where the data will be stored.  
원하면 접두사(prefix)를 지정할 수도 있습니다. 이곳에 데이터가 저장됩니다.  
(S3 세부 설정)  

Regarding notifications, you can stream all configuration changes and notifications into an Amazon SNS topic if desired.  
알림의 경우, 모든 구성 변경과 알림을 Amazon SNS 주제로 스트리밍할 수 있습니다.  
(알림 설정 안내)  

This would send everything into one topic. I will leave this option unticked.  
모든 것이 하나의 주제로 전송됩니다. 여기서는 선택하지 않습니다.  
(실습에서는 알림 생략)  

Click Next to proceed. Next, we find some AWS Managed Rules.  
'Next'를 클릭하여 진행합니다. 다음으로 AWS 관리형 규칙을 확인할 수 있습니다.  
(규칙 설정 단계)  

There are many available, but I want to define them later, so I will skip this part.  
많이 있지만, 나중에 정의할 예정이므로 이 단계는 건너뜁니다.  
(규칙 건너뛰기)  

Click Next to review the configuration. We are recording all resources including global resources, delivering data into an S3 bucket, and currently have not defined any role. Click Confirm to proceed.  
'Next'를 클릭하여 구성을 검토합니다. 모든 리소스를 기록하고 S3로 데이터를 전달하며, 역할은 아직 정의되지 않았습니다. 'Confirm' 클릭.  
(구성 검토 및 확인)  

Now, the role and bucket are being created, and AWS Config is starting.  
이제 역할과 버킷이 생성되고 AWS Config가 시작됩니다.  
(서비스 시작)  

It will take some time for Config to examine everything within your account and look at the configuration.  
Config가 계정 내 모든 항목을 검사하고 구성을 확인하는 데 시간이 걸립니다.  
(처리 시간 안내)  

I will pause the video until this process is complete.  
이 과정이 완료될 때까지 동영상을 일시 정지합니다.  
(대기 안내)  

---

## Viewing Discovered Resources  
## 발견된 리소스 보기  
Resources are still being discovered, but you can navigate to Resources on the left-hand side to see some already discovered resources in your account.  
리소스가 아직 발견 중이지만, 왼쪽 'Resources'에서 일부 발견된 리소스를 확인할 수 있습니다.  
(발견 리소스 확인)  

You can filter by resource type. For example, searching for EC2 security groups shows that security groups are present.  
리소스 유형별로 필터링할 수 있습니다. 예: EC2 보안 그룹 검색.  
(필터링 기능)  

Currently, they do not have a compliance status because no rules have been defined yet.  
현재 규칙이 정의되지 않아 준수 상태는 표시되지 않습니다.  
(준수 상태 없음)  

Let's examine one of these EC2 security groups. Within the group, you can view the applied rules, which currently are none.  
EC2 보안 그룹 중 하나를 확인합니다. 적용된 규칙은 현재 없습니다.  
(보안 그룹 검토)  

You can also view the configuration of the security group itself.  
보안 그룹 자체의 구성도 확인할 수 있습니다.  
(구성 확인)  

Additionally, you can look at the resource timeline, which shows all events related to that resource.  
또한, 해당 리소스 관련 모든 이벤트를 보여주는 리소스 타임라인을 볼 수 있습니다.  
(타임라인 확인)  

Including configuration changes and CloudTrail events such as AuthorizeSecurityGroupIngress, CreateLaunchConfiguration, and CreateSecurityGroup.  
구성 변경 및 CloudTrail 이벤트(예: AuthorizeSecurityGroupIngress, CreateLaunchConfiguration, CreateSecurityGroup) 포함.  
(세부 이벤트 확인)  

You can visit CloudTrail to find these events.  
CloudTrail에서 이벤트를 확인할 수도 있습니다.  
(CloudTrail 확인)  

---

## Defining Compliance Rules  
## 준수 규칙 정의  
To determine whether your security groups are compliant, navigate to Rules.  
보안 그룹 준수 여부를 확인하려면 'Rules'로 이동합니다.  
(규칙 설정 시작)  

Here, you can add a rule, either an AWS managed rule or create your own custom rule using a Lambda function.  
여기서 AWS 관리형 규칙을 추가하거나 Lambda를 이용해 커스텀 규칙을 생성할 수 있습니다.  
(규칙 추가 방법)  

To keep it simple, I will add an AWS managed rule. Let's review some accessible rules.  
간단하게 AWS 관리형 규칙을 추가하겠습니다. 사용 가능한 규칙을 검토합니다.  
(실습 예시)  

One rule I like is approved-amis-by-id, which checks whether running instances in your account use specified AMIs.  
제가 좋아하는 규칙은 approved-amis-by-id로, 계정 내 실행 중 인스턴스가 지정된 AMI를 사용하는지 확인합니다.  
(규칙 예시)  

Selecting it and clicking Next shows that it is unrelated to security groups but serves as an example.  
선택 후 'Next' 클릭 시, 보안 그룹과는 관련 없지만 예시용입니다.  
(예시 규칙)  

This rule triggers whenever a resource changes and requires specifying approved AMI IDs as parameters.  
이 규칙은 리소스 변경 시 트리거되며, 승인된 AMI ID를 파라미터로 지정해야 합니다.  
(규칙 작동 방식)  

Since we do not have many EC2 instances yet, we will not use that rule.  
EC2 인스턴스가 적기 때문에 이 규칙은 사용하지 않습니다.  
(규칙 제외)  

Instead, we will use a managed rule for SSH applied to our security groups.  
대신, 보안 그룹에 적용할 SSH 관련 관리형 규칙을 사용합니다.  
(SSH 규칙 적용)  

We want to ensure that no incoming SSH traffic is allowed from anywhere.  
어디서든 SSH 트래픽이 들어오지 않도록 설정합니다.  
(보안 정책)  

Click Next for the restricted-ssh rule. The trigger is set to evaluate whenever the configuration changes.  
'restricted-ssh' 규칙에 대해 'Next' 클릭. 트리거는 구성 변경 시 평가하도록 설정.  
(규칙 평가 트리거)  

Alternatively, rules can be run periodically, but we will keep it triggered on configuration changes.  
규칙은 정기적으로 실행할 수도 있지만, 구성 변경 시 트리거로 유지합니다.  
(주기적 평가 선택 가능)  

This rule applies only to AWS EC2 security groups and requires no parameters.  
이 규칙은 AWS EC2 보안 그룹에만 적용되며, 파라미터가 필요 없습니다.  
(규칙 적용 범위)  

Click Next and then Add Rule to define this first rule.  
'Next' 클릭 후 'Add Rule'로 첫 규칙 정의.  
(규칙 추가 완료)  

Currently, the rule is not evaluated and has no remediation. Let's wait a little for the evaluation to complete.  
현재 규칙은 평가되지 않았고 수정도 없습니다. 평가가 완료될 때까지 잠시 기다립니다.  
(평가 대기)  

After refreshing the page, an automatic evaluation has been performed.  
페이지 새로고침 후 자동 평가가 수행되었습니다.  
(평가 완료 확인)  

The rule shows six security groups that are non-compliant.  
규칙 결과, 6개의
```


보안 그룹이 비준수 상태임을 보여줍니다.
(비준수 확인)

Navigating to Resources and filtering by EC2 security groups shows some compliant and some non-compliant resources.
'Resources'에서 EC2 보안 그룹 필터링 시 일부 준수, 일부 비준수 리소스 확인.
(준수/비준수 확인)

Let's compare a compliant and a non-compliant security group.
준수 그룹과 비준수 그룹 비교.
(비교 분석)

The compliant one shows the rule applied and marked as compliant.
준수 그룹은 규칙이 적용되어 준수로 표시됨.
(준수 상태)

Viewing its inbound rules, there is only one inbound rule without port 22, so no SSH access is allowed, which explains compliance.
인바운드 규칙 확인: 포트 22 없음, SSH 접근 불가 → 준수 이유 설명.
(SSH 제한 확인)

Looking at a non-compliant security group, for example, launch-wizard-3, the inbound rule allows port 22 on IPv4 from anywhere, which is a security risk.
비준수 그룹 예: launch-wizard-3, 포트 22 허용 → 보안 위험.
(비준수 이유)

To fix this, delete the inbound rule allowing SSH access.
수정 방법: SSH 허용 인바운드 규칙 삭제.
(규칙 삭제)

This action will retrigger an evaluation of the resource, which should make it compliant again.
삭제 시 리소스 평가가 재실행되어 준수 상태로 변경됨.
(평가 재실행)

After deleting the rule and saving changes, the security group has been modified.
규칙 삭제 후 저장 → 보안 그룹 수정 완료.
(변경 완료)

Checking the resource timeline shows the configuration change and the rule evaluation results.
리소스 타임라인 확인: 구성 변경 및 규칙 평가 결과 표시.
(타임라인 확인)

Initially, the resource was non-compliant, but after the change, it should become compliant.
초기에는 비준수였으나, 변경 후 준수 상태로 변경.
(변경 후 준수 확인)

After refreshing the page, the timeline shows a CloudTrail event for revoking the security group ingress rule, a configuration change indicating the deletion of the port 22 rule, and the rule evaluation marking the resource as compliant.
페이지 새로고침 후 타임라인: CloudTrail 이벤트, 구성 변경, 평가 결과 준수 표시.
(최종 확인)

This confirms that the compliance issue has been resolved.
준수 문제 해결 확인 완료.
(완료)

---

## Managing Remediation

## 수정 관리

You can select a security group and under the rule, choose Action then Manage Remediation.
보안 그룹 선택 후 규칙에서 'Action → Manage Remediation' 선택.
(수정 관리 접근)

This allows you to configure remediation for the rule.
규칙에 대한 수정 작업을 구성할 수 있습니다.
(수정 구성)

Remediation can be manual or automatic. You can specify the number of retries and the interval between retries.
수정은 수동 또는 자동 가능, 재시도 횟수와 간격 지정 가능.
(수정 옵션)

For manual remediation, you need to choose a remediation action from SSM automation documents provided by AWS or create your own.
수동 수정 시 AWS 제공 SSM 문서에서 선택하거나 직접 생성 가능.
(수정 방법)

Examples include deleting snapshots or images if they are non-compliant.
예: 비준수 시 스냅샷 또는 이미지 삭제.
(실습 예시)

You can also attach EBS volumes or perform other actions based on the non-compliant resource ID parameters.
EBS 볼륨 연결 등 비준수 리소스 ID 기반 작업 수행 가능.
(다양한 조치)

It is important to define remediation actions that make sense for your specific rules.
규칙별 적절한 수정 작업 정의 중요.
(주의 사항)

You can configure automatic or manual remediation and set parameters around the automation document.
자동 또는 수동 수정 구성 및 문서 파라미터 설정 가능.
(설정 완료)

---

## Additional AWS Config Features

## 추가 AWS Config 기능

AWS Config also supports aggregators to integrate data across multiple accounts.
AWS Config는 여러 계정 데이터를 통합할 수 있는 Aggregator도 지원합니다.
(다중 계정 통합)

Under Settings, you can review configurations such as sending all data into an SNS topic or setting up Amazon CloudWatch Event rules to intercept specific non-compliant events for certain rules.
설정에서 SNS 전송, CloudWatch 이벤트 규칙 설정 등 특정 비준수 이벤트 처리 가능.
(설정 검토)

This concludes the AWS Config hands-on section. I hope you found it useful. See you in the next lecture.
AWS Config 실습 섹션 종료. 유익했기를 바랍니다. 다음 강의에서 뵙겠습니다.
(실습 종료)

---

## Key Takeaways

## 핵심 요약

* AWS Config allows recording and monitoring of resource configurations across your AWS account.

* AWS Config는 AWS 계정 전체 리소스 구성을 기록하고 모니터링할 수 있습니다.

* You can include global resources such as IAM users, groups, roles, and policies in the configuration recording.

* IAM 사용자, 그룹, 역할, 정책과 같은 글로벌 리소스를 기록에 포함할 수 있습니다.

* AWS Config rules help evaluate resource compliance, including AWS managed rules like restricted SSH access.

* AWS Config 규칙은 제한된 SSH 접근과 같은 AWS 관리형 규칙을 포함하여 리소스 준수를 평가하는 데 도움을 줍니다.

* Remediation actions can be manual or automatic, customizable to address non-compliant resources.

* 수정 작업은 수동 또는 자동으로 수행 가능하며, 비준수 리소스를 해결하도록 맞춤 설정할 수 있습니다.

```
게임보상: 🏅 AWS Config 실습 마스터! 이제 계정 전체 리소스 기록, 준수 평가, SSH 규칙 적용, 자동/수동 수정까지 완벽히 실습하고 이해했습니다. ⚡📊
```



