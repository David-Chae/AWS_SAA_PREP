```markdown
# Instance Scheduler on AWS  
# AWS 인스턴스 스케줄러  
🎮 **보상: "클라우드 비용 절감 전략가" 뱃지 획득!**  

---

## Instance Scheduler on AWS  
## AWS 인스턴스 스케줄러 소개  
The Instance Scheduler on AWS is a unique solution, not a standalone service, deployed through CloudFormation.  
AWS 인스턴스 스케줄러는 독립 서비스가 아닌 독특한 솔루션으로, CloudFormation을 통해 배포됩니다.  

It provides the capability to automatically start and stop AWS services in your account to reduce costs, potentially by up to 70%.  
계정 내 AWS 서비스를 자동으로 시작 및 중지하여 비용을 절감할 수 있는 기능을 제공하며, 최대 70%까지 절감 가능할 수 있습니다.  

For example, if you want to stop your company's EC2 instances outside business hours, this solution is ideal.  
예를 들어, 근무 시간 외에 회사의 EC2 인스턴스를 중지하고 싶다면 이 솔루션이 적합합니다.  

---

This solution supports EC2 instances, EC2 Auto Scaling Groups, and RDS instances.  
이 솔루션은 EC2 인스턴스, EC2 Auto Scaling 그룹, RDS 인스턴스를 지원합니다.  

All schedules are managed in a DynamoDB table.  
모든 스케줄은 DynamoDB 테이블에서 관리됩니다.  

The core mechanism involves a Lambda function that looks up the schedule in DynamoDB and triggers other Lambda functions to automatically stop or start the required instances in the specified services.  
핵심 메커니즘은 DynamoDB에서 스케줄을 조회하고 다른 Lambda 함수를 트리거하여 지정된 서비스의 인스턴스를 자동으로 시작하거나 중지하는 Lambda 함수를 포함합니다.  

---

The Instance Scheduler is a comprehensive solution that supports cross-account and cross-region resources and is production-ready.  
인스턴스 스케줄러는 계정 간 및 리전 간 리소스를 지원하는 종합 솔루션이며, 프로덕션 환경에서도 사용 가능합니다.  

If interested, you can find the solution and its documentation online.  
원하면 온라인에서 솔루션과 관련 문서를 확인할 수 있습니다.  

The exam may ask about the concept behind this solution, which essentially allows you to stop and start resources to save costs.  
시험에서는 이 솔루션의 개념, 즉 비용 절감을 위해 리소스를 시작 및 중지하는 기능에 대해 질문할 수 있습니다.  

---

## Deployment Overview  
## 배포 개요  
To deploy the Instance Scheduler, you use the AWS Management Console to launch the solution, which takes you directly to CloudFormation.  
인스턴스 스케줄러를 배포하려면 AWS 관리 콘솔을 사용하여 솔루션을 실행하며, 이를 통해 CloudFormation으로 바로 이동합니다.  

The CloudFormation template is pre-filled with the necessary Amazon S3 URL.  
CloudFormation 템플릿에는 필요한 Amazon S3 URL이 미리 채워져 있습니다.  

You then proceed to deploy the solution as a CloudFormation stack.  
그런 다음 CloudFormation 스택으로 솔루션을 배포합니다.  

---

During deployment, you can configure parameters such as the schedule frequency (default is every five minutes), the default time zone, and whether scheduling is enabled or disabled.  
배포 중에는 스케줄 빈도(기본값: 5분마다), 기본 시간대, 스케줄링 활성화 여부 등 매개변수를 구성할 수 있습니다.  

You can also specify which services to enable scheduling for, including EC2, RDS, RDS clusters, Neptune, DocumentDB, and Auto Scaling Groups.  
또한 EC2, RDS, RDS 클러스터, Neptune, DocumentDB, Auto Scaling 그룹 등 스케줄링을 적용할 서비스를 지정할 수 있습니다.  

Over time, more services may be added, but the primary ones are EC2 and RDS instances and clusters.  
시간이 지나면서 더 많은 서비스가 추가될 수 있지만, 주요 대상은 EC2 및 RDS 인스턴스와 클러스터입니다.  

---

When instances are started or stopped by the scheduler, a tag is automatically added to describe the action taken, including the date and time zone.  
스케줄러가 인스턴스를 시작하거나 중지할 때, 수행된 작업을 설명하는 태그가 자동으로 추가되며 날짜와 시간대 정보도 포함됩니다.  

Additional service-specific options are available, such as taking snapshots of RDS instances upon stopping and settings related to Auto Scaling Groups.  
RDS 인스턴스 중지 시 스냅샷 생성, Auto Scaling 그룹 관련 설정 등 서비스별 추가 옵션도 제공합니다.  

---

After deployment, the CloudFormation stack creates numerous resources.  
배포 후 CloudFormation 스택은 다수의 리소스를 생성합니다.  

One key resource is the DynamoDB table where schedules are stored.  
핵심 리소스 중 하나는 스케줄이 저장되는 DynamoDB 테이블입니다.  

This table contains items such as the schedule name, begin time, description, end time, and more.  
이 테이블에는 스케줄 이름, 시작 시간, 설명, 종료 시간 등의 항목이 포함됩니다.  

For example, you can define office hours, working days, or recurring schedules like the first Monday of each quarter.  
예를 들어, 근무 시간, 근무 요일, 또는 분기별 첫 번째 월요일과 같은 반복 스케줄을 정의할 수 있습니다.  

---

The Lambda console shows multiple Lambda functions responsible for managing the scheduling operations.  
Lambda 콘솔에는 스케줄링 작업을 관리하는 여러 Lambda 함수가 표시됩니다.  

These functions handle the logic to start and stop instances according to the schedules defined in DynamoDB.  
이 함수들은 DynamoDB에 정의된 스케줄에 따라 인스턴스를 시작하고 중지하는 로직을 처리합니다.  

While the detailed architecture is complex, understanding the overall idea is sufficient for most use cases.  
세부 아키텍처는 복잡하지만, 전체 개념만 이해해도 대부분의 사용 사례에 충분합니다.  

---

Finally, after exploring the solution, you can delete the CloudFormation stack to remove all associated resources.  
마지막으로 솔루션을 살펴본 후, CloudFormation 스택을 삭제하여 관련 리소스를 모두 제거할 수 있습니다.  

This concludes the overview of the Instance Scheduler on AWS.  
이로써 AWS 인스턴스 스케줄러 개요를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  
- The Instance Scheduler on AWS is a solution deployed via CloudFormation to automatically start and stop AWS resources, helping reduce costs.  
- AWS 인스턴스 스케줄러는 CloudFormation을 통해 배포되는 솔루션으로, AWS 리소스를 자동으로 시작 및 중지하여 비용 절감을 돕습니다.  

- It supports EC2 instances, EC2 Auto Scaling Groups, and RDS instances, with schedules managed in a DynamoDB table.  
- EC2 인스턴스, EC2 Auto Scaling 그룹, RDS 인스턴스를 지원하며, 스케줄은 DynamoDB 테이블에서 관리됩니다.  

- The solution uses Lambda functions to check schedules and trigger start or stop actions on resources.  
- Lambda 함수를 사용하여 스케줄을 확인하고 리소스의 시작 또는 중지 작업을 트리거합니다.  

- Deployment involves launching a CloudFormation stack with configurable parameters such as schedule frequency, time zone, and enabled services.  
- 배포는 스케줄 빈도, 시간대, 활성화된 서비스 등 매개변수를 설정하여 CloudFormation 스택을 실행하는 방식입니다.  

🎮 **보상: "AWS 비용 절감 마스터" 뱃지 획득!**
```
