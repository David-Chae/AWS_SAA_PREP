```markdown
# CloudWatch Agent & CloudWatch Logs Agent  
# CloudWatch 에이전트 및 CloudWatch 로그 에이전트  
(제목: EC2 인스턴스 및 온프레미스 서버에서 로그와 메트릭을 수집하는 CloudWatch 에이전트 강의)  

---

Now let's discuss how we can use CloudWatch Agents to collect logs from EC2 instances, as well as metrics, and send them to CloudWatch.  
이제 CloudWatch 에이전트를 사용하여 EC2 인스턴스에서 로그와 메트릭을 수집하고 CloudWatch로 전송하는 방법을 살펴보겠습니다.  
(CloudWatch Agent를 활용해 로그와 시스템 상태 정보를 중앙으로 보내는 방법 소개)  

By default, no logs are sent from your EC2 instance to CloudWatch.  
기본적으로 EC2 인스턴스에서 CloudWatch로 로그가 전송되지 않습니다.  
(설정하지 않으면 로그는 자동 전송되지 않음)  

To enable this, you need to create and start an agent, which is a small program running on your EC2 instances that pushes the log files you want to CloudWatch.  
이를 활성화하려면 에이전트를 생성하고 시작해야 합니다. 에이전트는 EC2 인스턴스에서 실행되는 작은 프로그램으로, 원하는 로그 파일을 CloudWatch로 전송합니다.  
(에이전트는 로그를 전송하는 핵심 구성 요소임)  

The idea is that your EC2 instances will have the CloudWatch Log Agents running, sending logs into CloudWatch Logs.  
즉, EC2 인스턴스에 CloudWatch 로그 에이전트를 실행시켜 로그를 CloudWatch Logs로 보내는 것이 핵심입니다.  
(로그 전송 구조의 기본 개념 설명)  

For this to work, your EC2 instance must have an IAM role that allows it to send logs to CloudWatch Logs.  
이 기능을 사용하려면 EC2 인스턴스에 로그를 CloudWatch Logs로 전송할 권한이 있는 IAM 역할이 필요합니다.  
(권한 설정 중요)  

It is important to note that these CloudWatch log agents can also be set up on on-premises servers.  
CloudWatch 로그 에이전트는 온프레미스 서버에도 설치할 수 있다는 점이 중요합니다.  
(클라우드뿐 아니라 사설 서버 환경에서도 적용 가능)  

This means you can have your services running on virtual servers like VMware on-premises, install the exact same agent (a small Linux program), and your logs will also end up in CloudWatch Logs.  
즉, VMware와 같은 온프레미스 가상 서버에 서비스를 운영하면서 동일한 에이전트를 설치하면, 로그가 CloudWatch Logs로 전송됩니다.  
(온프레미스 환경에서도 중앙 로그 수집 가능)  

---

There are two different agents available in CloudWatch:  
CloudWatch에는 두 가지 에이전트가 있습니다:  
(CloudWatch 에이전트 종류 구분)  

- The CloudWatch Logs Agent, which is the older version.  
- CloudWatch 로그 에이전트(구버전)  
(기본적으로 로그만 전송 가능)  

- The CloudWatch Unified Agent, which is the newer version.  
- CloudWatch Unified Agent(신버전)  
(로그와 시스템 메트릭 모두 수집 가능)  

Both agents are designed for virtual servers such as EC2 instances and on-premises servers.  
두 에이전트 모두 EC2와 같은 가상 서버 및 온프레미스 서버용으로 설계되었습니다.  
(적용 대상 서버 환경 설명)  

The CloudWatch Logs Agent is the old version and can only send logs to CloudWatch Logs.  
CloudWatch 로그 에이전트는 구버전으로, 로그만 CloudWatch Logs로 전송할 수 있습니다.  
(제한적 기능)  

In contrast, the Unified Agent collects additional system-level metrics such as RAM and processes, and also sends logs into CloudWatch Logs.  
반면 Unified Agent는 RAM, 프로세스 등 시스템 수준 메트릭도 수집하고, 로그도 CloudWatch Logs로 전송합니다.  
(통합형 에이전트 장점)  

---

The Unified Agent is better because it can handle both metrics and logs, hence the name "Unified Agent."  
Unified Agent가 더 나은 이유는 로그와 메트릭을 모두 처리할 수 있기 때문이며, 이름 그대로 "통합 에이전트"입니다.  
(에이전트 이름의 의미 설명)  

Additionally, you can configure this agent very easily using the SSM Parameter Store, a feature that the previous agent did not have.  
또한 이전 에이전트에는 없던 **SSM Parameter Store**를 통해 매우 쉽게 설정할 수 있습니다.  
(중앙 관리 가능)  

This allows centralized configuration for all your Unified Agents.  
이 기능을 통해 모든 Unified Agent를 중앙에서 구성할 수 있습니다.  
(대규모 운영 환경에서 유용)  

---

The CloudWatch Unified Agent can send logs to CloudWatch Logs, but let's take a closer look at the metrics it can collect.  
CloudWatch Unified Agent는 로그를 CloudWatch Logs로 전송할 수 있으며, 수집 가능한 메트릭도 살펴보겠습니다.  
(로그뿐 아니라 다양한 시스템 메트릭 수집 가능)  

If you install the Unified Agent on your EC2 instances or Linux servers, you can collect metrics such as CPU metrics at a very granular level.  
EC2 인스턴스 또는 Linux 서버에 Unified Agent를 설치하면, CPU 메트릭을 매우 세밀하게 수집할 수 있습니다.  
(세부적인 CPU 상태 모니터링 가능)  

These include active, guest, idle, system, user, and steal CPU states.  
예를 들어 active, guest, idle, system, user, steal CPU 상태를 수집합니다.  
(다양한 CPU 상태 정보 수집 예시)  

You do not need to memorize all these, but this illustrates the granularity of the metrics collected.  
모두 암기할 필요는 없지만, 수집되는 메트릭의 세밀함을 보여줍니다.  
(세부 모니터링 가능성을 강조)  

Other metrics include disk metrics such as free, used, and total space, as well as disk IO in terms of number of writes, reads, bytes, and IOPS.  
다른 메트릭으로는 디스크의 free, used, total 공간 및 쓰기/읽기 수, 바이트, IOPS와 같은 디스크 IO 메트릭이 있습니다.  
(스토리지 상태와 성능 정보 수집 가능)  

RAM metrics include free, inactive, used, total, and cached memory.  
RAM 메트릭은 free, inactive, used, total, cached 메모리를 포함합니다.  
(메모리 사용 상태 상세 확인 가능)  

Network statistics include the number of TCP and UDP connections, network packets, and bytes.  
네트워크 통계에는 TCP/UDP 연결 수, 네트워크 패킷 및 바이트가 포함됩니다.  
(네트워크 트래픽 상태 모니터링 가능)  

Regarding processes, the agent collects metrics on the total number of processes, including dead, blocked, idle, running, and sleeping states.  
프로세스 관련으로, 전체 프로세스 수와 dead, blocked, idle, running, sleeping 상태를 수집합니다.  
(프로세스 상태 모니터링 가능)  

It also monitors swap space, which is memory spilling onto disk, including how much is free, used, and the percentage used.  
또한 스왑 공간(메모리 부족 시 디스크 사용)도 모니터링하며, free, used, 사용률을 확인할 수 있습니다.  
(메모리 부족 상황 분석 가능)  

---

In summary, the CloudWatch Unified Agent provides a lot more metrics at much more granular detail than the normal monitoring available for EC2 instances.  
요약하면, CloudWatch Unified Agent는 일반 EC2 모니터링보다 훨씬 더 많은 세부 메트릭을 제공합니다.  
(디폴트 EC2 모니터링보다 훨씬 정밀함)  

As a reminder, out of the box, EC2 instances provide some information on disk, CPU, and network, but not memory or swap, and all of this at a high level.  
참고로 기본 EC2는 디스크, CPU, 네트워크 정도만 제공하며, 메모리나 스왑 정보는 제공하지 않고 모두 높은 수준의 정보입니다.  
(기본 모니터링 한계 설명)  

If you want more granularity, consider using the CloudWatch Unified Agent.  
더 세밀한 모니터링이 필요하다면 CloudWatch Unified Agent를 고려하세요.  
(정밀 모니터링 권장)  

That concludes this lecture. I hope you found it helpful, and I will see you in the next lecture.  
이 강의를 마칩니다. 도움이 되었기를 바라며, 다음 강의에서 뵙겠습니다.  
(강의 종료)  

---

## Key Takeaways  
## 핵심 요약  

- CloudWatch Agents are essential for sending logs and metrics from EC2 instances and on-premises servers to CloudWatch.  
- CloudWatch 에이전트는 EC2 인스턴스 및 온프레미스 서버에서 로그와 메트릭을 CloudWatch로 전송하는 데 필수적입니다.  

- The CloudWatch Logs Agent is the older version that only sends logs, while the CloudWatch Unified Agent sends both logs and detailed system metrics.  
- CloudWatch 로그 에이전트는 로그만 전송하는 구버전이며, Unified Agent는 로그와 상세 시스템 메트릭 모두 전송합니다.  

- The Unified Agent supports centralized configuration via the SSM Parameter Store.  
- Unified Agent는 SSM Parameter Store를 통해 중앙 구성 관리가 가능합니다.  

- The Unified Agent provides granular metrics including CPU states, disk IO, RAM usage, network stats, process states, and swap space, offering more detailed monitoring than default EC2 metrics.  
- Unified Agent는 CPU 상태, 디스크 IO, RAM 사용량, 네트워크 통계, 프로세스 상태, 스왑 공간 등 세밀한 메트릭을 제공하여 기본 EC2 모니터링보다 훨씬 정밀합니다.  
```

🎮 **게임 보상**: 이번 강의 완주로 **+150 EXP**와 **“시스템 감시자” 배지 🖥️** 획득!
