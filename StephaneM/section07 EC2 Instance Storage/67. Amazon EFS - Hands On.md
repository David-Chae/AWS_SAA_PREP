# Amazon EFS - Hands On
# 아마존 EFS - 실습
> Amazon Elastic File System(EFS)의 실습 과정 안내
> 설명: Hands-on 실습을 통해 EFS 사용법을 배우는 문서입니다.

## Introduction to Amazon Elastic File System (EFS)
## 아마존 EFS 소개
> Let's proceed with practicing the use of the Amazon Elastic File System service.
> 아마존 EFS 서비스를 직접 사용해보는 실습을 진행합니다.
> 설명: 이 세션에서 EFS 실습을 진행함을 안내합니다.

## Creating an EFS File System
## EFS 파일 시스템 생성
> We will create our file system. Here, we can optionally provide a name, but we will leave it empty. Next, we must select a Virtual Private Cloud (VPC) to connect our file system to. We will leave it as the default VPC. We could simply click on create and finish, but let's explore the options by clicking on Customize.
> 파일 시스템을 생성합니다. 이름은 선택적으로 입력할 수 있지만, 여기서는 비워둡니다. 다음으로 파일 시스템을 연결할 VPC를 선택해야 합니다. 기본 VPC를 사용합니다. 바로 생성할 수도 있지만, Customize를 클릭하여 옵션을 확인합니다.
> 설명: EFS 생성 과정에서 기본 옵션과 커스터마이즈 방법 안내

> Again, we leave the name empty. Next, we choose the file system type. There are two options:
> 이름은 다시 비워둡니다. 다음으로 파일 시스템 유형을 선택합니다. 옵션은 두 가지가 있습니다:
> 설명: 파일 시스템 유형 선택 단계

- Regional: Provides a file system within the region across multiple availability zones, offering very high availability and data durability.  
- 지역(Regional): 여러 가용 영역에 걸쳐 파일 시스템을 제공하며, 매우 높은 가용성과 데이터 내구성을 제공합니다.  
> 설명: 프로덕션 환경에 적합한 고가용성 옵션

- One Zone: Requires selecting a specific availability zone. This option is cost-effective but suitable only for development environments because if that availability zone becomes unavailable, the data will be inaccessible.  
- 단일 영역(One Zone): 특정 가용 영역을 선택해야 합니다. 비용 효율적이지만, 해당 영역이 장애가 나면 데이터 접근이 불가능하므로 개발 환경용으로 적합합니다.  
> 설명: 저비용, 개발 환경용 옵션

> For production environments, regional is recommended. We will use regional for this hands-on session.
> 프로덕션 환경에는 Regional이 권장됩니다. 실습에서는 Regional을 사용합니다.
> 설명: 실습 환경 설정 안내

## Backup and Lifecycle Management
## 백업 및 라이프사이클 관리
> Automatic backups can be enabled or disabled; it is recommended to keep them enabled.
> 자동 백업은 활성화 또는 비활성화할 수 있으며, 활성화 상태 유지가 권장됩니다.
> 설명: 백업 설정 중요성

> Lifecycle management allows moving data across different storage tiers to save costs. For example:
> 라이프사이클 관리는 데이터를 서로 다른 스토리지 계층으로 이동시켜 비용을 절감할 수 있습니다. 예를 들어:
> 설명: 라이프사이클 기능 개념

- Files not accessed for 30 days can be transitioned to the infrequent access storage tier, which is cheaper except when accessed.  
- 30일간 접근하지 않은 파일은 EFS-IA(저빈도) 스토리지로 이동할 수 있으며, 접근 시를 제외하면 비용이 저렴합니다.  
> 설명: 저빈도 스토리지 활용 예

- Files not accessed for 90 days can be moved to the archive storage class, which is even cheaper.  
- 90일간 접근하지 않은 파일은 아카이브 스토리지로 이동할 수 있으며, 비용이 더 저렴합니다.  
> 설명: 아카이브 스토리지 활용 예

> Upon first access after transition, files can be moved back to the standard tier assuming they will be reused frequently.
> 이동 후 처음 접근 시 파일은 다시 표준 계층으로 이동할 수 있으며, 자주 사용될 것으로 가정합니다.
> 설명: 접근 기반 자동 복귀 기능

> This lifecycle management helps optimize storage costs effectively.
> 이러한 라이프사이클 관리는 스토리지 비용을 효율적으로 최적화하는 데 도움을 줍니다.
> 설명: 비용 최적화 효과 강조

## Encryption and Performance Settings
## 암호화 및 성능 설정
> Encryption is enabled by default, which is appropriate.
> 암호화는 기본적으로 활성화되어 있으며, 적절한 설정입니다.
> 설명: 기본 암호화 상태 안내

> Performance settings include throughput mode with three options:
> 성능 설정에는 처리량 모드(Throughput Mode) 세 가지 옵션이 포함됩니다:
> 설명: 처리량 모드 설명

- Bursting: Throughput scales with the amount of storage used, allowing temporary bursts above the baseline.  
- 버스팅(Bursting): 사용량에 따라 처리량이 증가하며, 일시적으로 기준치 이상으로 증가할 수 있습니다.  
> 설명: 단기 고처리량 지원

- Elastic (recommended): Provides all the I/O needed regardless of file system size, scales automatically, and charges only for usage. Ideal for workloads with unpredictable I/O.  
- 탄력적(Elastic, 권장): 파일 시스템 크기와 관계없이 필요한 모든 I/O 제공, 자동 확장, 사용량에 따라 비용 청구. 예측 불가 워크로드에 적합.  
> 설명: 자동 확장, 유연한 I/O 옵션

- Provisioned: Allows specifying throughput in advance, suitable when throughput needs are known. Charges apply regardless of usage.  
- 프로비저닝(Provisioned): 처리량을 사전에 지정 가능, 요구량이 명확한 경우 적합. 사용량과 관계없이 비용 청구.  
> 설명: 고정 처리량 설정 옵션

> Additional settings include:
> 추가 성능 설정 옵션:
> 설명: 성능 관련 부가 설정 안내

- General Purpose: Low latency, suitable for latency-sensitive applications.  
- 일반용(General Purpose): 지연 시간이 낮아, 지연 민감 애플리케이션에 적합합니다.  
> 설명: 기본 용도 성능 모드

- Max I/O: Higher throughput with higher latency, suitable for highly parallelized workloads like big data.  
- 최대 I/O(Max I/O): 처리량 높음, 지연 높음, 빅데이터와 같이 병렬 처리 높은 워크로드에 적합.  
> 설명: 병렬 처리용 성능 모드

> The recommended configuration is enhanced mode with general purpose and elastic throughput.
> 권장 구성은 General Purpose + Elastic 처리량의 향상 모드입니다.
> 설명: 실습 권장 설정 안내

## Network Access Settings
## 네트워크 접근 설정
> Next, we configure network access. We select the default VPC and the mount targets. Since we chose a regional file system, all availability zones are available, each assigned to a subnet. We leave the default subnets and IP assignment as automatic.
> 다음으로 네트워크 접근을 구성합니다. 기본 VPC와 마운트 대상(Mount Targets)을 선택합니다. Regional 파일 시스템이므로 모든 가용 영역 사용 가능하며, 각 서브넷에 할당됩니다. 기본 서브넷과 IP 할당은 자동으로 둡니다.
> 설명: 네트워크 연결 기본 설정

> We must assign a security group. To do this, we create a specific security group for the EFS file system in the EC2 console under Security Groups. We name it sg-efs-demo with the description "EFS Demo SG". Initially, it has no inbound rules. After creation, we refresh the page to select this security group for our EFS file system.
> 보안 그룹을 할당해야 합니다. EC2 콘솔의 Security Groups에서 EFS 파일 시스템용 보안 그룹을 생성합니다. 이름은 sg-efs-demo, 설명은 "EFS Demo SG"로 합니다. 초기에는 인바운드 규칙이 없습니다. 생성 후 페이지를 새로고침하여 EFS 파일 시스템에 할당합니다.
> 설명: 보안 그룹 생성 및 할당 과정

## File System Policy and Creation
## 파일 시스템 정책 및 생성
> File system policy is optional and advanced; we skip it for now. We review all settings and create the file system. The file system creation process begins, and once complete, the file system is available with a current size of six kilobytes. EFS charges only for storage used, so costs are currently zero.
> 파일 시스템 정책은 선택적 고급 옵션으로, 여기서는 생략합니다. 모든 설정을 검토하고 파일 시스템을 생성합니다. 생성 후 현재 크기는 6KB이며, 사용한 저장 용량에 대해서만 비용이 청구되므로 현재 비용은 0입니다.
> 설명: 정책 생략, 생성 과정 및 비용 구조 안내

## Launching EC2 Instances and Mounting EFS
## EC2 인스턴스 실행 및 EFS 마운트
> We proceed to launch EC2 instances to mount the EFS file system.
> EFS 파일 시스템을 마운트하기 위해 EC2 인스턴스를 실행합니다.
> 설명: 실습 단계 안내

- Instance A: Launched in subnet of availability zone A, using Amazon Linux 2, t2.micro (free tier eligible), with EC2 instance connect enabled and default security group allowing SSH from anywhere.  
- 인스턴스 A: 가용 영역 A의 서브넷에서 실행, Amazon Linux 2 사용, t2.micro(무료 티어 가능), EC2 인스턴스 연결 활성화, 기본 보안 그룹으로 SSH 허용.  
> 설명: 인스턴스 A 설정 상세

- We configure storage by adding the EFS file system directly from the EC2 console. We select the subnet eu-west-1a and add the EFS file system with mount point /mnt/efs/fs1. The console automatically creates and attaches the required security groups and user data scripts to mount the shared file system.
- EC2 콘솔에서 EFS 파일 시스템을 추가하여 스토리지를 구성합니다. 서브넷 eu-west-1a를 선택하고 마운트 포인트 /mnt/efs/fs1로 추가합니다. 콘솔이 자동으로 필요한 보안 그룹과 사용자 데이터 스크립트를 생성 및 연결합니다.  
> 설명: EFS 마운트 자동 구성

- We launch the instance.  
- 인스턴스를 실행합니다.  
> 설명: 인스턴스 실행 완료

- Instance B: Launched similarly in availability zone B (eu-west-1b), using the same Amazon Linux 2 AMI, without a key pair, and attaching the same EFS file system with the same mount point and options.  
- 인스턴스 B: 가용 영역 B(eu-west-1b)에서 동일 AMI로 실행, 키 페어 없음, 동일 EFS 파일 시스템 동일 마운트 포인트와 옵션으로 추가  
> 설명: 인스턴스 B 설정

- We launch this instance as well.  
- 인스턴스 B도 실행합니다.  
> 설명: 인스턴스 실행 완료

## Security Groups and Access Configuration
## 보안 그룹 및 접근 설정
> In the EFS console under the network tab, each availability zone has multiple security groups:
> EFS 콘솔 네트워크 탭에서 각 가용 영역은 여러 보안 그룹을 가집니다:
> 설명: 보안 그룹 구성 안내

- The manually created EFS Demo security group.  
- 수동 생성된 EFS Demo 보안 그룹  
> 설명: 실습용 보안 그룹

- Auto-created security groups efs-sg-1 and efs-sg-2 by the EC2 console.  
- EC2 콘솔이 자동 생성한 efs-sg-1, efs-sg-2  
> 설명: 자동 생성 보안 그룹

> For example, security group efs-sg-2 allows inbound NFS protocol on port 2049 from the security group attached to Instance B. This setup permits Instance B to access the EFS file system securely. AWS manages this configuration automatically.
> 예를 들어, efs-sg-2는 포트 2049 NFS 인바운드를 인스턴스 B에 연결된 보안 그룹에서 허용합니다. 이를 통해 인스턴스 B가 EFS 파일 시스템에 안전하게 접근할 수 있습니다. AWS가 자동으로 구성합니다.
> 설명: 보안 그룹 NFS 접근 설정 설명

## Verifying EFS Mount and File Sharing
## EFS 마운트 및 파일 공유 확인
> We connect to Instance A using EC2 instance connect. Navigating to /mnt/efs/fs1/, we create a file named hello.txt with the content "hello world" using elevated privileges.
> EC2 인스턴스 연결을 통해 인스턴스 A에 접속합니다. /mnt/efs/fs1/로 이동하여 hello.txt 파일을 "hello world" 내용으로 생성합니다.  
> 설명: 파일 생성 및 권한 확인

> On Instance B, we verify the presence of hello.txt in the same mount point and confirm the content is "hello world". This demonstrates that the EFS file system is mounted as a network drive on both EC2 instances in different availability zones, sharing the same storage.
> 인스턴스 B에서 동일 마운트 포인트에 hello.txt 존재를 확인하고, 내용이 "hello world"임을 확인합니다. 이는 서로 다른 가용 영역의 EC2 인스턴스가 동일 스토리지를 공유함을 보여줍니다.
> 설명: EFS 공유 및 마운트 검증

## Cleanup
## 정리
> To clean up resources after the demo:
> 실습 후 리소스 정리:
> 설명: 리소스 삭제 안내

- Terminate both EC2 instances.  
- 두 EC2 인스턴스를 종료합니다.  
> 설명: 인스턴스 종료

- Delete the EFS file system by entering its file system ID.  
- 파일 시스템 ID를 입력하여 EFS 삭제  
> 설명: EFS 삭제

- Remove any extra security groups created during the demo.  
- 실습 중 생성한 추가 보안 그룹 삭제  
> 설명: 보안 그룹 정리

> This concludes the EFS hands-on demonstration.
> EFS 실습 데모가 종료되었습니다.  
> 설명: 실습 종료 안내

## Key Takeaways
## 핵심 요약
> Amazon Elastic File System (EFS) offers regional and one zone file system types, with regional recommended for production due to high availability.
> 아마존 EFS는 Regional과 One Zone 타입을 제공하며, 높은 가용성 때문에 프로덕션에는 Regional이 권장됩니다.  
> 설명: 파일 시스템 유형 요약

> Lifecycle management in EFS allows automatic transition of files to infrequent access or archive storage tiers based on last access time to optimize costs.
> EFS 라이프사이클 관리는 마지막 접근 시간을 기반으로 파일을 자동으로 저빈도 또는 아카이브 스토리지로 이동시켜 비용을 최적화합니다.  
> 설명: 라이프사이클 관리 요약

> Performance modes include bursting, elastic (recommended), and provisioned throughput, with elastic mode providing scalable I/O without manual configuration.
> 성능 모드는 Bursting, Elastic(권장), Provisioned 처리량이 있으며, Elastic 모드는 수동 설정 없이 확장 가능한 I/O를 제공합니다.  
> 설명: 성능 모드 요약

> Mounting EFS on EC2 instances can now be automated via the EC2 console, simplifying setup and security group management.
> EC2 인스턴스에 EFS를 마운트하는 과정은 이제 EC2 콘솔을 통해 자동화 가능하며, 설정과 보안 그룹 관리가 단순화됩니다.  
> 설명: 마운트 자동화 및 관리 요약
