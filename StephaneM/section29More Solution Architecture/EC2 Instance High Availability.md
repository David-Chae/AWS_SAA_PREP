```markdown
# EC2 Instance High Availability  
# EC2 인스턴스 고가용성  
(EC2 인스턴스를 장애에도 끊김 없이 사용할 수 있도록 만드는 방법)  

---

## Introduction to EC2 Instance High Availability  
## EC2 인스턴스 고가용성 소개  
(기본 동작과 이를 고가용성으로 전환하는 개요)  

Let's discuss solution architecture to understand how we can make an EC2 instance highly available.  
EC2 인스턴스를 어떻게 고가용성으로 만들 수 있는지 아키텍처 관점에서 살펴보자.  
(설계 기반 접근 필요)  

By default, an EC2 instance is launched in one Availability Zone and is not highly available.  
기본적으로 EC2 인스턴스는 하나의 가용 영역(AZ)에만 생성되며 고가용성이 아니다.  
(단일 AZ 장애에 취약)  

However, we can engineer solutions to achieve high availability, which is the purpose of this lecture.  
하지만 아키텍처 설계를 통해 고가용성을 구현할 수 있으며, 이것이 이번 설명의 목적이다.  
(솔루션 설계를 통한 개선)  

There are different approaches depending on your requirements and the amount of work you want to undertake.  
요구사항과 작업량에 따라 여러 가지 접근 방법이 있다.  
(비용·복잡도별 대안 존재)  

---

## Using Elastic IP with a Standby EC2 Instance  
## 대기(Standby) EC2 인스턴스와 Elastic IP 사용  
(Elastic IP로 장애 시 IP를 신속 전환하는 방법)  

Suppose we have a public EC2 instance running a web server.  
웹 서버가 실행 중인 퍼블릭 EC2 인스턴스가 있다고 가정하자.  

To enable access, we attach an Elastic IP to that EC2 instance.  
사용자가 접근할 수 있도록 Elastic IP를 해당 인스턴스에 연결한다.  

Users can then access the website directly through this Elastic IP, communicating with the EC2 instance and receiving responses from the web server.  
사용자는 Elastic IP를 통해 웹 서버와 직접 통신하고 응답을 받는다.  

To achieve high availability, we want to have a standby EC2 instance in case the primary instance fails.  
고가용성을 위해 기본 인스턴스가 실패했을 때 대비할 대기 인스턴스를 둔다.  

We need a failover mechanism to switch to the standby instance when necessary.  
필요할 경우 대기 인스턴스로 전환하는 장애 조치 메커니즘이 필요하다.  

---

## Monitoring and Failover Mechanism  
## 모니터링 및 장애 조치 메커니즘  
(장애 감지 및 자동 복구 프로세스)  

To detect failures, monitoring must be in place.  
장애를 감지하기 위해 모니터링이 필수다.  

We can create a CloudWatch Event or CloudWatch Alarm based on specific events.  
특정 이벤트에 기반해 CloudWatch 이벤트 또는 알람을 설정할 수 있다.  

For example, a CloudWatch Event can detect if an instance is terminated.  
예를 들어, CloudWatch 이벤트는 인스턴스 종료 여부를 감지할 수 있다.  

Alternatively, a CloudWatch Alarm can monitor the CPU utilization of a web server, triggering if the CPU reaches 100%, indicating a potential problem.  
또는 CloudWatch 알람은 CPU 사용률을 감시하여 100%에 도달하면 문제를 알릴 수 있다.  

From the Alarm or Event, a Lambda function can be triggered.  
알람 또는 이벤트 발생 시 Lambda 함수가 실행된다.  

This Lambda function can perform actions such as starting the standby instance if it is not running and attaching the Elastic IP to the standby instance.  
Lambda 함수는 대기 인스턴스를 실행하고 Elastic IP를 연결하는 등의 작업을 한다.  

Since an Elastic IP can only be attached to one instance at a time, it will be detached from the failed instance and attached to the standby instance, effectively failing over without users noticing any disruption.  
Elastic IP는 동시에 하나의 인스턴스에만 연결 가능하므로, 장애 인스턴스에서 분리되어 대기 인스턴스에 연결된다. 사용자 입장에서는 끊김 없는 전환이 이루어진다.  

---

## Auto Scaling Group Approach  
## Auto Scaling Group(ASG) 접근법  
(ASG를 활용한 자동 장애 복구 방식)  

Another method involves using an Auto Scaling Group (ASG) spanning two Availability Zones.  
또 다른 방법은 두 개의 가용 영역에 걸쳐 ASG를 사용하는 것이다.  

Users access the application through an Elastic IP for simplicity.  
사용자는 Elastic IP를 통해 단순하게 애플리케이션에 접근한다.  

We configure the ASG with a minimum, maximum, and desired capacity of one instance, distributed across two Availability Zones.  
ASG의 최소·최대·목표 용량을 1로 설정하고 두 AZ에 분산 배치한다.  

This means only one EC2 instance runs at a time, possibly in the first Availability Zone.  
즉, 항상 하나의 인스턴스만 실행되며 보통 첫 번째 AZ에서 실행된다.  

The EC2 instance's user data script acquires and attaches the Elastic IP based on tags when it launches, allowing users to communicate with the web server.  
인스턴스 실행 시 사용자 데이터 스크립트가 Elastic IP를 자동으로 가져와 연결하여 사용자와 통신 가능하게 한다.  

If the instance is terminated or fails, the ASG automatically launches a replacement instance in the other Availability Zone.  
인스턴스가 종료되거나 실패하면 ASG는 자동으로 다른 AZ에 대체 인스턴스를 실행한다.  

The new instance runs its user data script to attach the Elastic IP, providing seamless failover without the need for CloudWatch Alarms or Events.  
새 인스턴스는 사용자 데이터 스크립트를 실행하여 Elastic IP를 연결하고, CloudWatch 알람 없이도 원활한 장애 조치를 제공한다.  

---

## Instance Role for API Calls  
## API 호출을 위한 인스턴스 역할  
(Elastic IP 연결에 필요한 권한 관리)  

Since the EC2 instance performs API calls to attach the Elastic IP, it must have an instance role with permissions to execute these API calls successfully.  
EC2 인스턴스가 Elastic IP를 연결하기 위해 API 호출을 수행하므로, 해당 권한을 가진 인스턴스 역할이 필요하다.  

This combination of EC2 user data and instance role ensures the Elastic IP is correctly attached during instance launch.  
EC2 사용자 데이터와 인스턴스 역할을 함께 사용하면 Elastic IP가 인스턴스 실행 시 올바르게 연결된다.  

---

## Extending to Stateful Instances with EBS Volumes  
## EBS 볼륨을 가진 상태 저장 인스턴스로 확장  
(데이터 보존을 고려한 고가용성 패턴)  

We can extend this pattern to stateful EC2 instances with attached EBS volumes, such as a database instance.  
이 패턴은 데이터베이스 같은 EBS 볼륨이 연결된 상태 저장 인스턴스에도 확장할 수 있다.  

The EBS volume contains all data but is locked to a specific Availability Zone.  
EBS 볼륨은 데이터를 저장하지만 특정 AZ에 묶여 있다.  

When the EC2 instance is terminated, the ASG can use lifecycle hooks to trigger scripts that create snapshots of the EBS volume.  
EC2 인스턴스가 종료되면, ASG는 라이프사이클 훅을 사용해 EBS 스냅샷 생성 스크립트를 실행할 수 있다.  

This snapshot is tagged appropriately.  
생성된 스냅샷은 태깅된다.  

The ASG then launches a replacement EC2 instance in another Availability Zone.  
ASG는 다른 AZ에 대체 인스턴스를 실행한다.  

Using a lifecycle hook on the launch event, an EBS volume is created from the snapshot in the correct Availability Zone and attached to the new instance.  
실행 이벤트 시 라이프사이클 훅으로 스냅샷에서 새로운 EBS 볼륨을 생성해 올바른 AZ에 연결한다.  

The EC2 user data script then attaches the Elastic IP address.  
이후 EC2 사용자 데이터 스크립트가 Elastic IP를 연결한다.  

Proper API call permissions via the instance role are necessary to complete these operations.  
이 모든 작업을 위해 인스턴스 역할에 API 호출 권한이 필요하다.  

This approach provides a highly available EC2 instance with persistent storage across Availability Zones.  
이 접근법은 AZ 간 지속적 스토리지를 가진 고가용성 EC2 인스턴스를 제공한다.  

---

## Summary  
## 요약  

The possibilities for creating highly available EC2 architectures are extensive.  
고가용성 EC2 아키텍처를 만드는 방법은 매우 다양하다.  

While these solutions require more custom work and automation, they enable robust failover and stateful recovery mechanisms.  
이러한 솔루션들은 추가 작업과 자동화가 필요하지만, 강력한 장애 복구 및 상태 저장 복구 메커니즘을 제공한다.  

Automation through CloudWatch, Lambda, Auto Scaling Groups, lifecycle hooks, and instance roles allows for seamless high availability of EC2 instances and their associated resources.  
CloudWatch, Lambda, ASG, 라이프사이클 훅, 인스턴스 역할을 통한 자동화로 EC2 인스턴스와 관련 리소스의 매끄러운 고가용성이 가능하다.  

---

## Key Takeaways  
## 핵심 정리  

- EC2 instances are launched in a single Availability Zone by default and are not highly available without additional architecture.  
- 기본적으로 EC2 인스턴스는 단일 AZ에서 실행되며, 추가 아키텍처 없이는 고가용성을 제공하지 않는다.  

- Elastic IPs can be used to provide a consistent public IP address that can be reassigned to standby instances for failover.  
- Elastic IP를 사용하면 장애 시 대체 인스턴스로 IP를 재할당해 지속적인 접근성을 제공할 수 있다.  

- CloudWatch Events and Alarms can monitor instance health and trigger Lambda functions to automate failover processes.  
- CloudWatch 이벤트와 알람으로 인스턴스 상태를 모니터링하고 Lambda 함수로 장애 조치를 자동화할 수 있다.  

- Auto Scaling Groups configured with minimum, maximum, and desired capacity of one across multiple Availability Zones can provide automatic replacement of failed instances.  
- 여러 AZ에 걸쳐 최소·최대·목표 용량을 1로 설정한 ASG는 장애 인스턴스를 자동으로 대체할 수 있다.  

- Lifecycle hooks in Auto Scaling Groups enable snapshotting and restoration of EBS volumes to maintain stateful data across instance replacements.  
- ASG의 라이프사이클 훅은 EBS 스냅샷 생성 및 복구를 가능하게 하여 상태 데이터를 유지한다.  

- Combining EC2 User Data scripts, instance roles, and lifecycle hooks allows for automated, highly available EC2 architectures with stateful storage.  
- EC2 사용자 데이터 스크립트, 인스턴스 역할, 라이프사이클 훅을 조합하면 자동화된 상태 저장 고가용성 아키텍처를 구현할 수 있다.  
```
