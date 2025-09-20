```md
# IAM Policies Hands On
# IAM 정책 실습
# 실습을 통해 IAM 정책이 실제로 어떻게 적용되고 상속되는지 확인합니다.

## Introduction to IAM Policies
## IAM 정책 소개
# IAM 정책 실습의 목적과 기본 개념을 안내합니다.

Let's examine IAM policies in depth. 
IAM 정책을 자세히 살펴보겠습니다.
# 실습을 통해 정책 적용과 권한 변화를 직접 경험하도록 합니다.

First, navigate to the users section. 
먼저, Users 섹션으로 이동합니다.
# IAM 콘솔에서 사용자 관리 위치를 안내합니다.

For example, the user Stephane is part of the admin group, which grants administrator access permissions to AWS.
예를 들어, 사용자 Stephane는 Admin 그룹에 속해 있으며, 이 그룹은 AWS 관리자 권한을 부여합니다.
# 그룹 상속을 통한 관리자 권한 예시를 보여줍니다.

Using the user Stephane to access the IAM console, you can see the user listed under users.
Stephane 계정을 사용해 IAM 콘솔에 접근하면, Users 목록에서 해당 사용자를 확인할 수 있습니다.
# 실제 콘솔에서 사용자 확인 방법을 안내합니다.

Since Stephane belongs to the admin group, they have permission to perform any action as an administrator.
Stephane는 Admin 그룹에 속해 있으므로, 관리자 권한으로 모든 작업을 수행할 수 있습니다.
# 그룹 상속으로 권한이 부여됨을 명확히 합니다.

### Removing User from Admin Group
### Admin 그룹에서 사용자 제거
# 권한 변경 실습을 위해 사용자를 그룹에서 제거합니다.

To demonstrate permission changes, remove the user Stephane from the admin group. 
권한 변화를 보여주기 위해, Stephane를 Admin 그룹에서 제거합니다.
# 그룹 제거 시 권한 상실을 실습합니다.

Once removed, Stephane loses the administrator permissions previously granted by the group.
제거되면, Stephane는 그룹을 통해 부여받았던 관리자 권한을 잃습니다.
# 그룹 기반 권한 상실 효과를 확인합니다.

After removal, refreshing the users page results in an access denied error, indicating that the user no longer has permission to perform the iamListUsers action.
제거 후 Users 페이지를 새로고침하면 접근 거부(Access Denied) 오류가 발생하며, 사용자가 iamListUsers 작업 권한을 더 이상 가지지 않음을 확인할 수 있습니다.
# 실제 권한 제거 효과를 실습으로 보여줍니다.

This confirms that removing a user from a group revokes their permissions accordingly.
이는 사용자를 그룹에서 제거하면 권한이 함께 해제된다는 것을 확인시켜 줍니다.
# 그룹 기반 권한 상속과 해제 구조를 이해하도록 합니다.

### Restoring Permissions by Attaching Policies
### 정책을 직접 부착하여 권한 복원
# 그룹 대신 직접 정책을 부착하여 권한을 복원하는 실습입니다.

To restore permissions for Stephane, navigate to the user and add permissions.
Stephane의 권한을 복원하려면, 사용자 화면으로 이동해 권한을 추가합니다.
# 직접 정책 부착 방법 안내.

Instead of adding the user back to a group, attach policies directly to the user.
사용자를 다시 그룹에 추가하는 대신, 정책을 사용자에게 직접 부착합니다.
# 직접 부착(In-line policy) 방식의 장점과 활용법을 설명합니다.

For example, attach the IAMReadOnlyAccess policy to allow read-only access to IAM resources.
예를 들어, IAMReadOnlyAccess 정책을 부착하여 IAM 리소스에 대한 읽기 전용 권한을 부여합니다.
# 읽기 전용 정책 예시를 보여줍니다.

After attaching the IAMReadOnlyAccess policy, refreshing the users page allows viewing users and user groups but restricts creating new groups.
IAMReadOnlyAccess 정책을 부착한 후, Users 페이지를 새로고침하면 사용자 및 그룹 조회는 가능하지만 새 그룹 생성은 제한됩니다.
# 읽기 전용 권한의 제한 범위를 실습으로 보여줍니다.

Attempting to create a group results in an access denied error, demonstrating that read-only access limits modification capabilities.
그룹 생성을 시도하면 접근 거부 오류가 발생하며, 읽기 전용 권한이 수정 작업을 제한함을 확인할 수 있습니다.
# 정책 효과를 직접 확인하도록 안내합니다.

This example illustrates that permissions should be granted strictly according to the user's required actions.
이 예시는 권한을 사용자가 실제 수행해야 하는 작업에 맞게 정확히 부여해야 함을 보여줍니다.
# 최소 권한 원칙(Principle of Least Privilege)을 강조합니다.

To allow creating groups, a broader permission set such as IAM full access must be attached.
그룹 생성을 허용하려면, IAM Full Access와 같은 더 넓은 권한 세트를 부착해야 합니다.
# 권한 수준별 차이를 실습으로 이해하도록 안내합니다.

### Creating User Groups and Assigning Policies
### 사용자 그룹 생성 및 정책 부착
# 새 그룹 생성과 정책 상속 실습을 진행합니다.

Next, create a new group named developers. 
다음으로, Developers라는 새 그룹을 생성합니다.
# 그룹 생성 실습 안내.

Add the user Stephane to this group and attach any policy, such as AlexaForBusiness, to demonstrate policy inheritance through groups.
사용자 Stephane를 이 그룹에 추가하고 AlexaForBusiness와 같은 정책을 부착하여 그룹 상속 정책을 실습합니다.
# 그룹 기반 정책 상속 예시를 보여줍니다.

Also, re-add Stephane to the admin group.
또한 Stephane를 Admin 그룹에 다시 추가합니다.
# 다중 그룹 상속 예시를 실습합니다.

Now, the user Stephane has multiple permission policies attached: administrator access inherited from the admin group, AlexaForBusiness managed policy from the developers group, and the IAMReadOnlyAccess policy attached directly.
이제 Stephane는 Admin 그룹에서 상속받은 관리자 권한, Developers 그룹에서 상속받은 AlexaForBusiness 관리 정책, 직접 부착한 IAMReadOnlyAccess 정책 등 여러 권한 정책을 가지게 됩니다.
# 다중 출처 정책 상속 구조를 확인합니다.

This demonstrates how permissions can be inherited from multiple sources, including groups and direct attachments.
이는 권한이 그룹과 직접 부착 등 여러 출처에서 상속될 수 있음을 보여줍니다.
# 실무에서 발생할 수 있는 복합 권한 상속 구조를 이해하도록 합니다.

### Understanding IAM Policies in Detail
### IAM 정책 상세 이해
# 정책의 JSON 구조와 권한 범위를 확인합니다.

Navigate to the policies section to examine specific policies.
Policies 섹션으로 이동하여 특정 정책을 확인합니다.
# 정책 확인 위치 안내.

For example, the AdministratorAccess policy grants full access to all AWS services and resources.
예를 들어, AdministratorAccess 정책은 모든 AWS 서비스와 리소스에 대한 전체 권한을 부여합니다.
# 관리자 권한 정책 예시 설명.

Viewing the JSON of this policy reveals that it allows all actions (Action: "*") on all resources (Resource: "*").
이 정책의 JSON을 보면, 모든 리소스(Resource: "*")에 모든 작업(Action: "*")을 허용함을 알 수 있습니다.
# JSON에서 정책 내용을 직접 확인하도록 안내.

This effectively grants administrator access.
이는 사실상 관리자 권한을 부여하는 것과 동일합니다.
# 권한 적용 효과를 설명합니다.

In contrast, the IAMReadOnlyAccess policy authorizes specific API calls such as List and Get actions on IAM resources.
반면, IAMReadOnlyAccess 정책은 IAM 리소스에 대해 List, Get과 같은 특정 API 호출만 허용합니다.
# 읽기 전용 정책의 제한 범위를 설명합니다.

The JSON document lists allowed actions like iam:ListUsers and iam:GetUser with effect set to allow.
JSON 문서에는 iam:ListUsers, iam:GetUser 등 허용된 액션과 Effect가 Allow로 설정되어 있습니다.
# JSON에서 허용된 액션과 효과 확인 방법 안내.

Using wildcards such as Get* or List* groups multiple API calls together, simplifying policy definitions.
Get*, List*와 같은 와일드카드를 사용하면 여러 API 호출을 그룹화하여 정책 정의를 간소화할 수 있습니다.
# 와일드카드 활용으로 정책 작성 효율화 방법 안내.

### Creating Custom IAM Policies
### 커스텀 IAM 정책 생성
# 사용자 맞춤 정책 작성 방법 안내.

You can create custom policies using either the visual editor or the JSON editor.
커스텀 정책은 Visual Editor 또는 JSON Editor를 사용해 만들 수 있습니다.
# 정책 작성 방식 안내.

For example, to create a policy that allows only ListUsers and GetUser actions on IAM, select these actions in the visual editor and specify the resources to which the policy applies.
예를 들어, IAM에서 ListUsers와 GetUser 액션만 허용하는 정책을 만들려면 Visual Editor에서 해당 액션을 선택하고 적용할 리소스를 지정합니다.
# 커스텀 정책 작성 예시 설명.

After creating the policy, review the JSON to confirm that it includes the intended permissions.
정책을 만든 후 JSON을 검토하여 의도한 권한이 포함되었는지 확인합니다.
# 정책 검증 과정 안내.

This custom policy can then be attached to users or groups as needed.
이 커스텀 정책은 필요에 따라 사용자 또는 그룹에 부착할 수 있습니다.
# 실제 정책 적용 방법 안내.

### Cleaning Up and Finalizing
### 정리 및 마무리
# 실습 종료 전 권한과 그룹을 정리합니다.

To conclude, delete the developers group if it is no longer needed.
마무리로, 필요 없으면 Developers 그룹을 삭제합니다.
# 실습 환경 정리 안내.

Remove any directly attached policies such as IAMReadOnlyAccess from the user Stephane, leaving only the admin group membership with administrator access.
사용자 Stephane에게 직접 부착한 IAMReadOnlyAccess 정책 등은 제거하고, Admin 그룹으로 상속된 관리자 권한만 남깁니다.
# 불필요한 정책 제거와 권한 최종 상태 확인.

Verifying the IAM console shows that the user Stephane has full access again, confirming that permissions are correctly managed through group memberships and attached policies.
IAM 콘솔을 확인하면 Stephane가 다시 전체 접근 권한을 가지며, 그룹과 부착 정책을 통해 권한이 올바르게 관리됨을 확인할 수 있습니다.
# 실습 결과 검증.

## Key Takeaways
## 핵심 요약
# 실습의 주요 포인트 정리.

- IAM user permissions are managed through group memberships and attached policies.
- IAM 사용자 권한은 그룹 소속과 부착된 정책을 통해 관리됩니다.
# 권한 관리 구조 요약.

- Removing a user from an admin group revokes their administrator access immediately.
- 사용자를 Admin 그룹에서 제거하면 관리자 권한이 즉시 해제됩니다.
# 권한 상실 효과 요약.

- Read-only access policies allow viewing but restrict modification actions.
- 읽기 전용 정책은 조회만 가능하며 수정은 제한됩니다.
# 읽기 전용 정책 핵심 요약.

- Custom IAM policies can be created using the visual or JSON editor to specify precise permissions.
- Visual 또는 JSON Editor를 사용해 커스텀 IAM 정책을 만들어 정확한 권한을 지정할 수 있습니다.
# 커스텀 정책 작성 요약.
```
