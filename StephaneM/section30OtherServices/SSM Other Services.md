```markdown
# SSM Other Services  
# SSM 기타 서비스  
🎮 **보상: "관리 자동화 탐험가" 뱃지 획득!**  

---

## Overview of Additional Systems Manager Services  
## Systems Manager 추가 서비스 개요  
Let's discuss some other services within the Systems Manager service that may appear as exam questions.  
시험 문제로 등장할 수 있는 Systems Manager 내 다른 서비스들을 살펴봅시다.  

If you do not understand every detail, just remember the general idea of these services.  
모든 세부 사항을 이해하지 못해도, 각 서비스의 전반적인 개념만 기억하면 됩니다.  

---

## Run Command  
## Run Command  
The first service is Run Command, which is used to execute a document, such as a script or a single command.  
첫 번째 서비스는 Run Command로, 스크립트나 단일 명령과 같은 문서를 실행하는 데 사용됩니다.  

These commands can be run on multiple instances using resource groups.  
이 명령들은 리소스 그룹을 사용하여 여러 인스턴스에서 실행할 수 있습니다.  

The instances can be EC2 instances or on-premises servers that are registered with the Systems Manager service because the SSM agent is running on them.  
인스턴스는 SSM 에이전트가 실행 중인 EC2 인스턴스 또는 Systems Manager에 등록된 온프레미스 서버일 수 있습니다.  

When running commands with Run Command, there is no need for SSH.  
Run Command를 사용해 명령을 실행할 때 SSH는 필요하지 않습니다.  

It uses the same mechanism as Session Manager, running commands through the agents on the instances.  
세션 매니저와 동일한 메커니즘을 사용하며, 인스턴스의 에이전트를 통해 명령을 실행합니다.  

Any output from the command can be sent to Amazon S3 or CloudWatch Logs.  
명령의 출력 결과는 Amazon S3 또는 CloudWatch Logs로 전송할 수 있습니다.  

In case of failures, notifications are sent to Amazon SNS.  
실패 시 알림이 Amazon SNS로 전송됩니다.  

You can receive updates on in-progress, success, or failure statuses via SNS.  
진행 중, 성공, 실패 상태에 대한 업데이트를 SNS를 통해 받을 수 있습니다.  

Run Command has full integration with IAM for security and CloudTrail to track who ran which commands.  
Run Command는 IAM과 완벽히 통합되어 보안을 유지하며, CloudTrail을 통해 누가 어떤 명령을 실행했는지 추적할 수 있습니다.  

Additionally, EventBridge can directly trigger Run Command executions.  
또한, EventBridge를 사용하여 Run Command 실행을 직접 트리거할 수 있습니다.  

---

## Run Command Workflow  
## Run Command 워크플로우  
- Managed instances (EC2 or on-premises) run the SSM agent.  
- 관리되는 인스턴스(EC2 또는 온프레미스)에 SSM 에이전트가 실행됩니다.  

- Run Command executes commands on these instances without SSH.  
- Run Command는 SSH 없이 이러한 인스턴스에서 명령을 실행합니다.  

- Command output can be sent to Amazon S3 or CloudWatch Logs.  
- 명령 출력은 Amazon S3 또는 CloudWatch Logs로 전송할 수 있습니다.  

- Status notifications are sent to Amazon SNS.  
- 상태 알림은 Amazon SNS로 전송됩니다.  

- Execution can be triggered manually or automatically via EventBridge.  
- 실행은 수동 또는 EventBridge를 통해 자동으로 트리거할 수 있습니다.  

---

## Patch Manager  
## 패치 매니저  
Patch Manager automates the process of patching managed instances.  
Patch Manager는 관리 인스턴스의 패치 과정을 자동화합니다.  

It applies operating system updates, application updates, and security updates.  
운영체제 업데이트, 애플리케이션 업데이트, 보안 업데이트를 적용합니다.  

Patch Manager supports EC2 instances and on-premises servers, including Linux, Mac, and Windows platforms.  
Patch Manager는 Linux, Mac, Windows 플랫폼을 포함한 EC2 및 온프레미스 서버를 지원합니다.  

You can patch instances on-demand or schedule patches using Maintenance Windows, which define when instances are ready to be patched.  
인스턴스를 필요 시 패치하거나, Maintenance Window를 사용하여 패치 시기를 예약할 수 있습니다.  

Patch Manager also allows scanning instances to generate patch compliance reports.  
Patch Manager는 인스턴스를 스캔하여 패치 준수 보고서를 생성할 수도 있습니다.  

These reports help identify if all instances are patched correctly or if any patches are missing.  
이 보고서는 모든 인스턴스가 올바르게 패치되었는지, 누락된 패치가 있는지 확인하는 데 도움을 줍니다.  

---

## Using Patch Manager  
## Patch Manager 사용  
- Invoke Patch Manager via console, SDK, or Maintenance Windows.  
- 콘솔, SDK, 또는 Maintenance Window를 통해 Patch Manager를 실행합니다.  

- Use the run command document named AWS-RunPatchBaseline to patch instances.  
- AWS-RunPatchBaseline라는 Run Command 문서를 사용하여 인스턴스를 패치합니다.  

- Patch all EC2 instances or on-premises servers as needed.  
- 필요에 따라 모든 EC2 인스턴스 또는 온프레미스 서버를 패치합니다.  

- Review patch compliance reports to ensure proper patching.  
- 패치 준수 보고서를 검토하여 올바르게 패치되었는지 확인합니다.  

---

## Maintenance Windows  
## Maintenance Window  
Maintenance Windows define schedules for performing actions on your instances.  
Maintenance Window는 인스턴스에서 작업을 수행할 스케줄을 정의합니다.  

For example, you can schedule OS patching, driver updates, software installation, or other tasks.  
예: 운영체제 패치, 드라이버 업데이트, 소프트웨어 설치 등의 작업을 예약할 수 있습니다.  

When defining a Maintenance Window, you specify:  
Maintenance Window를 정의할 때 다음을 지정합니다:  

- The schedule for when it will be triggered.  
- 실행될 스케줄.  

- The duration for how long it will run.  
- 작업이 진행될 기간.  

- The target instances to which it applies.  
- 적용 대상 인스턴스.  

- The tasks that will be executed during the window.  
- 창 기간 동안 수행될 작업.  

For instance, a Maintenance Window can be triggered every 24 hours to run patching commands on EC2 instances.  
예: 24시간마다 트리거되어 EC2 인스턴스에 패치 명령을 실행할 수 있습니다.  

You can also customize it creatively for other maintenance tasks.  
다른 유지보수 작업에도 창을 창의적으로 커스터마이징할 수 있습니다.  

---

## Automation  
## 자동화  
Automation simplifies common maintenance and deployment tasks on EC2 instances or other AWS resources.  
Automation은 EC2 인스턴스 및 AWS 리소스에서 일반적인 유지보수와 배포 작업을 단순화합니다.  

Examples include restarting multiple instances simultaneously, creating AMIs, or taking EBS snapshots.  
예: 여러 인스턴스 동시 재시작, AMI 생성, EBS 스냅샷 생성 등.  

Automation uses runbooks, which are SSM documents representing predefined actions on EC2 instances or AWS resources.  
Automation은 runbook을 사용하며, 이는 EC2 인스턴스 또는 AWS 리소스에서 사전 정의된 작업을 나타내는 SSM 문서입니다.  

These runbooks can be executed by SSM Automation to perform tasks such as restarting instances or taking snapshots of RDS databases.  
이 runbook은 SSM Automation으로 실행되어 인스턴스 재시작, RDS 스냅샷 생성 등의 작업을 수행할 수 있습니다.  

Automation can be triggered via the console, SDK, CLI, Amazon EventBridge, Maintenance Windows, or AWS Config.  
Automation은 콘솔, SDK, CLI, EventBridge, Maintenance Window, AWS Config를 통해 트리거할 수 있습니다.  

For example, if AWS Config detects a non-compliant resource, it can automatically trigger an SSM Automation runbook to remediate the issue.  
예: AWS Config가 비준수 리소스를 감지하면, SSM Automation runbook을 자동으로 실행하여 문제를 해결할 수 있습니다.  

---

## Summary  
## 요약  
This concludes the overview of additional Systems Manager services including Run Command, Patch Manager, Maintenance Windows, and Automation.  
이로써 Run Command, Patch Manager, Maintenance Window, Automation을 포함한 Systems Manager 추가 서비스 개요를 마칩니다.  

These services help manage and automate tasks on EC2 instances and on-premises servers efficiently and securely.  
이들 서비스는 EC2 인스턴스 및 온프레미스 서버에서 작업을 효율적이고 안전하게 관리하고 자동화하는 데 도움을 줍니다.  

---

## Key Takeaways  
## 핵심 요약  
- Run Command allows execution of scripts or commands on multiple managed instances without SSH, with output sent to S3 or CloudWatch Logs and status notifications via SNS.  
- Run Command는 SSH 없이 여러 관리 인스턴스에서 스크립트 또는 명령 실행이 가능하며, 출력은 S3/CloudWatch Logs로, 상태 알림은 SNS로 전달됩니다.  

- Patch Manager automates patching of operating systems and applications on EC2 and on-premises servers, supporting Linux, Mac, and Windows, with options for on-demand or scheduled patching using maintenance windows.  
- Patch Manager는 EC2 및 온프레미스 서버의 운영체제/애플리케이션 패치를 자동화하며, Linux, Mac, Windows를 지원하고, Maintenance Window를 이용한 즉시 또는 예약 패치가 가능합니다.  

- Maintenance Windows define schedules, durations, target instances, and tasks for performing actions such as patching or software installation.  
- Maintenance Window는 패치, 소프트웨어 설치 등 작업 수행을 위한 스케줄, 기간, 대상 인스턴스, 작업을 정의합니다.  

- Automation simplifies common maintenance and deployment tasks on AWS resources using predefined runbooks, with triggers from console, SDK, CLI, EventBridge, Maintenance Windows, or AWS Config remediation.  
- Automation은 사전 정의된 runbook을 이용해 AWS 리소스의 유지보수 및 배포 작업을 단순화하며, 콘솔, SDK, CLI, EventBridge, Maintenance Window, AWS Config 트리거가 가능합니다.  

🎮 **보상: "SSM 마스터 자동화 뱃지" 획득!**
```
