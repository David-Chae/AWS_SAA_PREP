# EBS & EFS - Section Cleanup
# EBS & EFS - 섹션 정리
> Section Cleanup Overview
> 섹션 정리 개요
> 설명: 이 섹션에서는 이전 실습에서 생성한 모든 리소스를 정리하는 방법을 안내합니다.

> In this section, we will clean up all the resources we created. This includes deleting the file system, terminating EC2 instances, deleting volumes, snapshots, and security groups to avoid unnecessary charges.
> 이 섹션에서는 우리가 생성한 모든 리소스를 정리합니다. 여기에는 파일 시스템 삭제, EC2 인스턴스 종료, 볼륨, 스냅샷, 보안 그룹 삭제가 포함되며, 불필요한 비용을 방지할 수 있습니다.
> 설명: 정리 과정에서 삭제해야 하는 리소스 종류와 이유

> First, navigate to the Action menu in the file system section and delete the file system. To do this, you need to enter the file system ID, which you can copy and paste accordingly. This will remove the file system from your account.
> 먼저 파일 시스템 섹션의 Action 메뉴로 이동하여 파일 시스템을 삭제합니다. 이를 위해 파일 시스템 ID를 입력해야 하며, 복사 후 붙여넣기 가능합니다. 이렇게 하면 계정에서 파일 시스템이 제거됩니다.
> 설명: 파일 시스템 삭제 절차

> Next, go to your EC2 instances and ensure that you terminate any running instances. This step is crucial to prevent ongoing charges from active instances.
> 다음으로 EC2 인스턴스로 이동하여 실행 중인 인스턴스를 종료합니다. 이 단계는 활성 인스턴스에서 발생하는 지속적인 요금을 방지하는 데 중요합니다.
> 설명: EC2 종료의 중요성 강조

> After terminating instances, you need to clear up any volumes. Identify all available volumes and delete them by right-clicking and selecting delete. This will free up storage space and avoid additional costs.
> 인스턴스 종료 후에는 모든 볼륨을 정리해야 합니다. 사용 가능한 모든 볼륨을 확인하고, 오른쪽 클릭 후 삭제를 선택하여 제거합니다. 이렇게 하면 저장 공간이 확보되고 추가 비용을 방지할 수 있습니다.
> 설명: 볼륨 삭제 절차

> Additionally, delete any snapshots you have created. Removing snapshots is important to ensure you do not pay for snapshot storage unnecessarily.
> 또한 생성한 모든 스냅샷을 삭제합니다. 스냅샷을 제거하는 것은 불필요한 스토리지 비용을 방지하는 데 중요합니다.
> 설명: 스냅샷 비용 관리

> Finally, address the security groups. You can delete many of the security groups except for the default one. Note that security groups will only be deleted once all associated EC2 instances have been terminated. If a security group is still in use, you may need to wait until the instances are fully shut down before deletion is possible.
> 마지막으로 보안 그룹을 처리합니다. 기본 그룹을 제외하고 대부분의 보안 그룹을 삭제할 수 있습니다. 보안 그룹은 연결된 모든 EC2 인스턴스가 종료되어야만 삭제됩니다. 여전히 사용 중인 보안 그룹이 있다면, 인스턴스가 완전히 종료될 때까지 기다려야 삭제할 수 있습니다.
> 설명: 보안 그룹 삭제 조건과 주의사항

> For example, you may delete a security group and the load balancer associated with it successfully. However, if an EC2 instance is still using a security group, you must wait for the instance to shut down properly before deleting that security group.
> 예를 들어, 보안 그룹과 연결된 로드 밸런서를 성공적으로 삭제할 수 있습니다. 하지만 EC2 인스턴스가 여전히 해당 보안 그룹을 사용 중이면, 인스턴스가 완전히 종료될 때까지 기다려야 합니다.
> 설명: 실무에서 발생할 수 있는 삭제 순서 문제 예시

> Once you have cleared all these resources, including file systems, EC2 instances, volumes, snapshots, and security groups, your environment will be clean and ready for the next section.
> 파일 시스템, EC2 인스턴스, 볼륨, 스냅샷, 보안 그룹 등 모든 리소스를 정리하면 환경이 깨끗해지고 다음 섹션을 진행할 준비가 됩니다.
> 설명: 정리 완료 후 환경 상태

## Key Takeaways
## 핵심 요약
- To clean up AWS resources, delete the file system by providing its file system ID.  
- AWS 리소스를 정리하려면 파일 시스템 ID를 입력하여 파일 시스템을 삭제합니다.  
> 설명: 파일 시스템 삭제 핵심

- Terminate all running EC2 instances to avoid ongoing charges.  
- 실행 중인 모든 EC2 인스턴스를 종료하여 지속적인 요금을 방지합니다.  
> 설명: EC2 종료 중요성

- Delete all available volumes to free up storage.  
- 사용 가능한 모든 볼륨을 삭제하여 저장 공간을 확보합니다.  
> 설명: 볼륨 삭제 핵심

- Remove snapshots to prevent storage costs.  
- 스냅샷을 삭제하여 스토리지 비용을 방지합니다.  
> 설명: 스냅샷 삭제 중요

- Delete unnecessary security groups except the default one, ensuring associated EC2 instances are terminated first.  
- 기본 그룹을 제외한 불필요한 보안 그룹을 삭제하며, 관련된 EC2 인스턴스가 먼저 종료되었는지 확인합니다.  
> 설명: 보안 그룹 삭제 순서 주의
