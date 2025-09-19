```markdown
# AWS Backup - Hands On  
# AWS 백업 실습  

🎮 게임보상: "Backup Hands-On Hero" +500 XP  

---

## In this session, we will practice using AWS Backup.  
## 이번 세션에서는 AWS Backup을 직접 사용해보는 실습을 진행합니다.  

First, type AWS Backup into the search bar and open the Backup service.  
먼저 검색창에 AWS Backup을 입력하고 Backup 서비스를 엽니다.  

---

## Creating a Backup Plan  
## 백업 계획 생성  

We are going to create our first backup plan by clicking on Create Backup plan.  
"Create Backup plan"을 클릭하여 첫 번째 백업 계획을 생성합니다.  

There are three options available:  
선택할 수 있는 세 가지 옵션이 있습니다.  

- Start with a template  
- 템플릿으로 시작  

- Build a new plan  
- 새 계획 생성  

- Define a plan using JSON  
- JSON으로 계획 정의  

The simplest option is to start with a template.  
가장 간단한 방법은 템플릿으로 시작하는 것입니다.  

---

## Selecting a Template  
## 템플릿 선택  

There are different templates such as:  
다음과 같은 다양한 템플릿이 있습니다.  

- Daily-35day-Retention  
- Daily-35day-Retention  

- Daily-Monthly-1yr-Retention  
- Daily-Monthly-1yr-Retention  

Let's choose Daily-Monthly-1yr-Retention and name the plan TestPlan.  
Daily-Monthly-1yr-Retention을 선택하고 계획 이름을 TestPlan으로 지정합니다.  

Next, click on Backup rules.  
다음으로 Backup rules를 클릭합니다.  

You can have multiple backup rules within your backup plan.  
백업 계획 내에 여러 백업 규칙을 설정할 수 있습니다.  

For example, there are daily and monthly backup rules.  
예를 들어, 일간 및 월간 백업 규칙이 있을 수 있습니다.  

---

## Daily Backup Rule Details  
## 일간 백업 규칙 세부사항  

Clicking on Daily Backup shows the following:  
Daily Backup을 클릭하면 다음과 같은 항목이 표시됩니다.  

- Rule name  
- 규칙 이름  

- Backup vault: This is where the backup is stored. You can use the default AWS vault or create a new one.  
- 백업 볼트: 백업이 저장되는 위치입니다. 기본 AWS 볼트를 사용하거나 새로 생성할 수 있습니다.  

- Backup frequency and Backup window: For example, start at 5:00 AM UTC within an 8-hour window. This can be customized.  
- 백업 빈도 및 백업 윈도우: 예를 들어 UTC 기준 오전 5시에 시작하고 8시간 윈도우 내에서 실행됩니다. 사용자 정의 가능.  

- Option to transition backups to cold storage after a specified duration.  
- 지정된 기간 후 백업을 콜드 스토리지로 전환하는 옵션  

- Retention period, e.g., five weeks.  
- 백업 보존 기간, 예: 5주  

- Option to copy backups to another region for disaster recovery.  
- 재해 복구를 위해 백업을 다른 리전으로 복사하는 옵션  

Save the daily backup rule.  
일간 백업 규칙을 저장합니다.  

The monthly backup rule is similar:  
월간 백업 규칙도 유사합니다.  

- Uses the default backup vault  
- 기본 백업 볼트를 사용  

- Runs monthly on day one  
- 매월 1일 실행  

- Transitions backups to cold storage after one month  
- 1개월 후 백업을 콜드 스토리지로 전환  

- Retains backups for one year  
- 백업 보존 기간 1년  

Once the backup rules are ready, scroll down and click Create plan.  
백업 규칙이 준비되면 아래로 스크롤하여 Create plan을 클릭합니다.  

The test plan is now created.  
테스트 계획이 생성되었습니다.  

---

## Assigning Resources to the Backup Plan  
## 백업 계획에 리소스 할당  

Click on Assign resources and name the assignment TestAssignments.  
Assign resources를 클릭하고 할당 이름을 TestAssignments로 지정합니다.  

For the IAM role, use the default role, which will create a role with the correct permissions automatically.  
IAM 역할은 기본 역할을 사용합니다. 기본 역할은 자동으로 올바른 권한이 설정됩니다.  

Alternatively, you can choose your own role.  
또는 사용자 정의 역할을 선택할 수도 있습니다.  

---

## Resource Selection Options  
## 리소스 선택 옵션  

You have two options:  
두 가지 옵션이 있습니다.  

- Include all resource types  
- 모든 리소스 유형 포함  

- Include specific resource types, for example, only DynamoDB tables  
- 특정 리소스 유형 포함, 예: DynamoDB 테이블만  

You can select specific resources or all tables of a type.  
특정 리소스나 해당 유형의 모든 테이블을 선택할 수 있습니다.  

When including all resource types, it is common to use tags to filter resources.  
모든 리소스를 포함할 때는 태그로 리소스를 필터링하는 것이 일반적입니다.  

For example, you can specify that resources with the tag key environment and value production should be backed up.  
예를 들어, 태그 키가 environment이고 값이 production인 리소스만 백업하도록 지정할 수 있습니다.  

This allows flexible backup policies based on tagging.  
태그를 기반으로 유연한 백업 정책을 적용할 수 있습니다.  

After setting the resource selection and tags, click Assign resources to complete the assignment.  
리소스 선택과 태그 설정 후 Assign resources를 클릭하여 할당을 완료합니다.  

---

## Example: Tagging an EBS Volume  
## 예시: EBS 볼륨 태그 지정  

If you create an EBS volume in EC2 with a size of one gigabyte and tag it with environment: production, it will be automatically backed up by the backup plan because it matches the tag criteria.  
EC2에 1GB 크기의 EBS 볼륨을 생성하고 environment: production 태그를 지정하면, 태그 기준에 맞아 자동으로 백업 계획에 의해 백업됩니다.  

You can verify the tags on the volume to confirm they correspond to the backup plan's tag selection.  
볼륨의 태그를 확인하여 백업 계획의 태그 선택과 일치하는지 확인할 수 있습니다.  

Multiple assignments can be created within a backup plan to cover different resource groups or criteria.  
백업 계획 내에서 여러 할당을 생성하여 다른 리소스 그룹이나 기준을 커버할 수 있습니다.  

The backup plan will run automatically, and backups will be stored in the specified backup vaults.  
백업 계획은 자동으로 실행되며, 지정된 백업 볼트에 백업이 저장됩니다.  

---

## Monitoring Backup Jobs  
## 백업 작업 모니터링  

You can monitor backup jobs, restore jobs, and copy jobs in the AWS Backup console to track the status of your backups and restores.  
AWS Backup 콘솔에서 백업 작업, 복원 작업, 복사 작업을 모니터링하여 백업 및 복원 상태를 확인할 수 있습니다.  

---

## Backup Settings  
## 백업 설정  

Settings include options for backup policies, cross-account monitoring, and cross-account backups.  
설정에는 백업 정책, 계정 간 모니터링, 계정 간 백업 옵션이 포함됩니다.  

---

## Cleanup  
## 정리  

After testing, make sure to delete your EBS volumes or wait to verify backups.  
테스트 후, EBS 볼륨을 삭제하거나 백업을 확인할 때까지 기다립니다.  

Then delete the assignments by typing the assignment name and deleting it.  
그런 다음 할당 이름을 입력하여 할당을 삭제합니다.  

You can also delete backup rules or the entire backup plan by entering the backup plan name and confirming deletion.  
백업 규칙이나 전체 백업 계획도 백업 계획 이름을 입력하고 삭제를 확인하여 제거할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Backup allows creating backup plans using templates, custom builds, or JSON definitions.  
- AWS Backup는 템플릿, 사용자 정의, JSON 정의를 사용하여 백업 계획을 생성할 수 있습니다.  

- Backup plans consist of backup rules specifying frequency, retention, and storage options.  
- 백업 계획은 빈도, 보존 기간, 스토리지 옵션을 지정하는 백업 규칙으로 구성됩니다.  

- Resources can be assigned to backup plans using tags or specific resource selections.  
- 리소스는 태그 또는 특정 리소스 선택을 통해 백업 계획에 할당할 수 있습니다.  

- Backup jobs run automatically based on the plan, and cleanup involves deleting assignments and backup plans.  
- 백업 작업은 계획에 따라 자동으로 실행되며, 정리는 할당과 백업 계획 삭제로 진행됩니다.  
```
