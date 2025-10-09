# EC2 Hibernate - Hands On  
# EC2 최대절전모드 - 실습  

---

## Introduction to EC2 Hibernate Feature  
## EC2 최대절전모드 기능 소개  

In this session, we will practice using the EC2 hibernate feature. Let's begin by launching an instance.  
이번 세션에서는 EC2 최대절전모드 기능을 실습해보겠습니다. 먼저 인스턴스를 실행해보겠습니다.  
→ 기능 실습의 시작 단계입니다.  

I will choose Amazon Linux 2 as the operating system. For the instance type, I will select t2.micro. Then, I will select a key pair for secure access.  
운영체제로 Amazon Linux 2를 선택하고, 인스턴스 유형은 t2.micro로 설정합니다. 그리고 안전한 접근을 위해 키 페어를 선택합니다.  
→ 가장 기본적인 환경 구성 설명입니다.  

For network security, I will use an existing security group named launch-wizard-1. Regarding storage, the default settings are sufficient for now. I will show you a few important settings shortly.  
네트워크 보안을 위해 "launch-wizard-1"이라는 기존 보안 그룹을 사용합니다. 스토리지는 기본 설정으로 충분합니다. 곧 중요한 몇 가지 설정을 보여드리겠습니다.  
→ 보안 그룹과 기본 스토리지 설정 설명입니다.  

Scrolling down to the hibernate behavior section, we can enable hibernation. Enabling this option allows us to activate hibernation on our EC2 instance.  
스크롤을 내려 최대절전모드 동작 섹션으로 가면, 최대절전모드를 활성화할 수 있습니다. 이 옵션을 켜면 EC2 인스턴스에서 최대절전모드를 사용할 수 있습니다.  
→ 핵심 기능 활성화 과정입니다.  

There is a warning message indicating that if hibernation is enabled, the root volume must have enough storage to fit the RAM of the EC2 instance. Additionally, the root EBS volume must be encrypted.  
경고 메시지가 표시되는데, 최대절전모드를 활성화하려면 루트 볼륨이 EC2 인스턴스의 RAM 크기를 저장할 충분한 공간을 가져야 하며, 루트 EBS 볼륨은 암호화되어야 한다는 내용입니다.  
→ 하드웨어 요건 및 보안 요건 설명입니다.  

To address storage requirements, I will go to the advanced settings and select my EBS volume. I will enable encryption using the default AWS/EBS key.  
스토리지 요구사항을 충족하기 위해 고급 설정으로 이동하여 EBS 볼륨을 선택합니다. 기본 AWS/EBS 키를 사용해 암호화를 활성화합니다.  
→ 실습에서 암호화 설정하는 단계입니다.  

Now, our EBS volume is correctly configured with encryption. The volume size is eight gigabytes, which is sufficient because the t2.micro instance has one gigabyte of RAM. This ensures that all the RAM can fit onto the disk, which is necessary for hibernation.  
이제 EBS 볼륨이 암호화되어 올바르게 설정되었습니다. 볼륨 크기는 8GB이며, t2.micro 인스턴스가 1GB RAM을 가지므로 충분합니다. 이는 RAM 전체를 디스크에 저장할 수 있음을 보장하며, 최대절전모드에 필수적입니다.  
→ 스토리지 크기와 요구조건 충족 설명입니다.  

With all settings configured, we are ready to enable hibernation. I will now launch the instance.  
모든 설정을 완료했으니 이제 최대절전모드를 활성화하고 인스턴스를 실행하겠습니다.  
→ 실행 전 최종 확인 단계입니다.  

Our instance is now created with hibernation enabled as a specific start behavior.  
이제 인스턴스가 최대절전모드 활성화 설정과 함께 생성되었습니다.  
→ 인스턴스가 성공적으로 준비된 상태입니다.  

---

## Verifying Hibernation Functionality  
## 최대절전모드 기능 검증  

To verify that hibernation works, let's connect to our instance using EC2 Instance Connect.  
최대절전모드가 동작하는지 확인하기 위해 EC2 Instance Connect로 인스턴스에 접속해봅시다.  
→ 접속 단계입니다.  

I am connecting to the instance now. Once connected, we can use the uptime command, which shows how long the instance has been running since its last restart.  
지금 인스턴스에 접속합니다. 연결되면 `uptime` 명령어를 사용해 마지막 재시작 이후 인스턴스가 얼마나 실행되었는지 확인할 수 있습니다.  
→ 검증 도구(`uptime`) 소개입니다.  

Running the uptime command shows that the instance has been up for zero minutes. We will wait a little for it to increment to one minute.  
`uptime` 명령어 실행 결과, 인스턴스가 실행된 시간이 0분으로 나옵니다. 잠시 기다리면 1분으로 증가할 것입니다.  
→ 초기 상태 확인 과정입니다.  

Now, the uptime command shows one minute, indicating the instance has been running for one minute since its last restart.  
이제 `uptime` 명령어가 1분을 표시하며, 인스턴스가 마지막 재시작 이후 1분 동안 실행 중임을 보여줍니다.  
→ 정상 동작 확인입니다.  

Let's disconnect from the instance. Next, we will hibernate the instance.  
이제 인스턴스 연결을 끊고, 다음으로 인스턴스를 최대절전모드로 전환하겠습니다.  
→ 실제 기능 실행 단계입니다.  

To hibernate the instance, we change its state to hibernate. This action stores all data in RAM onto the EBS volume.  
인스턴스를 최대절전모드로 전환하려면 상태를 Hibernate로 변경합니다. 이 동작은 RAM의 모든 데이터를 EBS 볼륨에 저장합니다.  
→ 절전 동작 설명입니다.  

The instance is now hibernating. We wait for it to stop.  
인스턴스가 이제 최대절전모드로 진입했습니다. 정지될 때까지 기다립니다.  
→ 전환 중 상태입니다.  

Once the instance is stopped, I will start it again.  
인스턴스가 정지되면 다시 시작하겠습니다.  
→ 재시작 과정입니다.  

If hibernation was not enabled, stopping and starting the instance would reset the uptime to zero minutes. However, since we hibernated the instance, the uptime should reflect the total time including before hibernation.  
만약 최대절전모드가 활성화되지 않았다면, 인스턴스를 중지 후 다시 시작하면 `uptime`은 0분으로 초기화됩니다. 그러나 최대절전모드에서는 중지 전 실행 시간을 포함하여 표시됩니다.  
→ 기능 차이를 보여주는 핵심 설명입니다.  

Let's connect to the instance again and run the uptime command.  
인스턴스에 다시 접속해서 `uptime` 명령어를 실행해봅시다.  
→ 결과 확인 단계입니다.  

The uptime command shows two minutes, confirming that the instance was never fully stopped from the operating system's perspective. This demonstrates that hibernation preserves the instance state.  
`uptime` 명령어가 2분을 표시하며, 운영체제 관점에서는 인스턴스가 완전히 중지되지 않았음을 확인할 수 있습니다. 이는 최대절전모드가 인스턴스 상태를 보존함을 입증합니다.  
→ 기능 검증 완료입니다.  

---

## Conclusion  
## 결론  

This concludes the demonstration of the EC2 hibernate feature. Finally, you can terminate your instance to clean up resources.  
이것으로 EC2 최대절전모드 기능 시연을 마치겠습니다. 마지막으로 리소스 정리를 위해 인스턴스를 종료하면 됩니다.  
→ 실습 정리 단계입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Enabled EC2 hibernation by configuring encrypted root EBS volume with sufficient storage.  
  충분한 스토리지를 가진 암호화된 루트 EBS 볼륨을 구성하여 EC2 최대절전모드를 활성화했습니다.  

- Verified instance uptime before and after hibernation to demonstrate preserved state.  
  최대절전모드 전후로 인스턴스의 `uptime`을 확인해 상태가 보존됨을 입증했습니다.  

- Used EC2 Instance Connect to access and manage the instance.  
  EC2 Instance Connect를 사용하여 인스턴스에 접속하고 관리했습니다.  

- Demonstrated stopping and restarting an instance with hibernation preserving RAM state.  
  최대절전모드로 인스턴스를 중지 및 재시작했을 때 RAM 상태가 보존되는 것을 시연했습니다.  
