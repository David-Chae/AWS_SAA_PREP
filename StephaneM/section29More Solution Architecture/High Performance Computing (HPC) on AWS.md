```md
# High Performance Computing (HPC) on AWS  
# AWS의 고성능 컴퓨팅(HPC)  

---

## Introduction to High Performance Computing (HPC) on AWS  
## AWS에서의 고성능 컴퓨팅(HPC) 소개  

There is a concept in AWS that is becoming more and more common and is something that the exam will test you on, which is called High Performance Computing or HPC.  
AWS에서 점점 더 보편화되고 시험에도 자주 등장하는 개념이 있는데, 바로 고성능 컴퓨팅(HPC)입니다.  

The cloud is the perfect place to perform high performance computing because you can create a very high number of resources in no time.  
클라우드는 자원을 빠르게 대량으로 생성할 수 있기 때문에 HPC를 수행하기에 이상적인 장소입니다.  

This allows you to speed up the time to results by adding more resources, and you only pay for what you have used.  
이를 통해 더 많은 자원을 추가해 결과를 빠르게 얻을 수 있고, 사용한 만큼만 비용을 지불합니다.  

Once you are done, you can destroy the entire infrastructure and not be billed a single dime.  
작업이 끝나면 전체 인프라를 삭제하고 추가 비용을 내지 않아도 됩니다.  

The idea here is that we can have an extremely high number of instances performing computation for us, then be done with it and just pay for what we used.  
즉, 엄청나게 많은 인스턴스를 사용해 연산을 수행하고 끝나면 사용량만큼만 지불하는 것입니다.  

This is a great use case for the cloud and something that AWS is encouraging you to do more and more.  
이는 클라우드의 대표적인 활용 사례이며, AWS가 적극적으로 권장하는 방식입니다.  

---

## Use Cases for HPC  
## HPC의 사용 사례  

Where do we use HPC? It is used to perform genomics, computational chemistry, financial risk modeling, weather prediction, machine learning, deep learning, autonomous driving, and so on.  
HPC는 어디에 사용될까요? 유전체 분석, 계산 화학, 금융 리스크 모델링, 날씨 예측, 머신러닝, 딥러닝, 자율주행 등 다양한 분야에서 활용됩니다.  

---

## AWS Services Supporting HPC  
## HPC를 지원하는 AWS 서비스  

What services in AWS will help us perform HPC? Let's have a look.  
HPC를 수행하는 데 어떤 AWS 서비스들이 도움이 될까요? 함께 살펴봅시다.  

---

### Data Management and Transfer  
### 데이터 관리 및 전송  

The first category is how we manage the data and how we transfer the data into AWS.  
첫 번째는 데이터를 어떻게 관리하고 AWS로 전송할지입니다.  

- **Direct Connect**: Moves gigabytes per second of data into the cloud over a private, secure network.  
- **Direct Connect**: 전용 보안 네트워크를 통해 초당 기가바이트 단위의 데이터를 클라우드로 전송합니다.  

- **Snowball and Snowmobile**: Move petabytes of data to the cloud through a physical route, usually for large or one-off transfers.  
- **Snowball & Snowmobile**: 페타바이트 단위의 데이터를 물리적 장치를 통해 클라우드로 옮기며, 대규모 또는 일회성 전송에 적합합니다.  

- **DataSync**: Requires installing DataSync agents to help move large amounts of data between on-premises file systems into AWS storage services like S3, EFS, or FSx for Windows.  
- **DataSync**: 온프레미스 파일 시스템과 AWS 스토리지 서비스(S3, EFS, FSx 등) 간에 대규모 데이터를 전송하기 위해 에이전트를 설치해야 합니다.  

---

### Compute and Networking  
### 컴퓨트와 네트워킹  

Compute and networking are very important for HPC.  
컴퓨트와 네트워킹은 HPC에서 매우 중요합니다.  

- **EC2 Instances**: CPU-optimized or GPU-optimized instances based on the type of computations.  
- **EC2 인스턴스**: 연산 유형에 따라 CPU 최적화 또는 GPU 최적화 인스턴스를 사용합니다.  

- **Spot Instances and Spot Fleets**: Provide huge cost savings.  
- **스팟 인스턴스 & 플릿**: 비용 절감을 크게 제공합니다.  

- **Auto Scaling**: Automatically scales fleets based on computation needs.  
- **오토 스케일링**: 연산 수요에 맞춰 자동으로 인스턴스를 확장/축소합니다.  

- **EC2 Placement Groups (Cluster Type)**: Used when EC2 instances need to communicate with one another and perform distributed computation. Provides low latency and high throughput.  
- **EC2 배치 그룹(클러스터형)**: 인스턴스 간 통신 및 분산 연산에 사용되며, 낮은 지연시간과 높은 처리량을 제공합니다.  

---

### Enhancing EC2 Network Performance  
### EC2 네트워크 성능 향상  

To improve the performance of EC2 instances further, AWS offers Enhanced Networking (SR-IOV).  
EC2 성능을 향상시키기 위해 AWS는 고급 네트워킹(SR-IOV)을 제공합니다.  

This provides higher bandwidth, higher packets per second (PPS), and lower latency.  
이를 통해 더 높은 대역폭, PPS, 더 낮은 지연시간을 제공합니다.  

**Option 1: Elastic Network Adapter (ENA)**  
- Delivers up to 100 Gbps network speed.  
- 네트워크 속도를 최대 100Gbps까지 지원합니다.  
- Most recent and popular option.  
- 최신이자 가장 많이 사용되는 옵션입니다.  

**Option 2: Intel 82599 VF**  
- Provides up to 10 Gbps.  
- 최대 10Gbps를 지원합니다.  
- Legacy option, previously known as ENA.  
- 구형 옵션으로, 이전 ENA입니다.  

Both ENA and Intel 82599 VF allow enhanced networking on your instance.  
두 옵션 모두 인스턴스에서 고급 네트워킹을 사용할 수 있게 합니다.  

---

### Elastic Fabric Adapter (EFA)  
### 엘라스틱 패브릭 어댑터(EFA)  

You can push network performance further by using EFA, which is optimized for HPC.  
EFA는 HPC 전용으로 최적화되어 네트워크 성능을 극대화합니다.  

- Works only on Linux.  
- 리눅스에서만 동작합니다.  
- Ideal for tightly coupled workloads (distributed computing).  
- 분산 연산처럼 긴밀히 연결된 작업에 이상적입니다.  

EFA leverages the MPI standard, bypassing the Linux OS for lower latency and reliable transport.  
EFA는 MPI 표준을 활용하여 리눅스 OS를 우회해 낮은 지연시간과 안정적인 전송을 제공합니다.  

It is common in the exam to be asked to differentiate ENA, EFA, ENI.  
시험에서 ENA, EFA, ENI 차이를 묻는 경우가 많습니다.  

---

### Storage Options for HPC  
### HPC를 위한 스토리지 옵션  

After transferring data and configuring compute/network, we need storage.  
데이터 전송 및 컴퓨트/네트워크 구성이 끝나면 스토리지가 필요합니다.  

- **Instance-Attached Storage**:  
  - **EBS**: 최대 256,000 IOPS(io2 Block Express).  
  - **인스턴스 스토어**: 수백만 IOPS, 매우 빠르지만 인스턴스 손실 시 데이터 소실.  

- **Network Storage**:  
  - **S3**: 대용량 객체 저장, 파일 시스템 아님.  
  - **EFS**: 파일 시스템 크기에 따라 IOPS 확장, 프로비저닝 모드 지원.  

- **HPC-Optimized FS**:  
  - **FSx for Lustre**: HPC 워크로드 전용, 리눅스 클러스터 최적화, 수백만 IOPS, 백엔드는 S3.  

---

### Automation and Orchestration for HPC  
### HPC를 위한 자동화 및 오케스트레이션  

- **AWS Batch**:  
  - 멀티 노드 병렬 작업 지원.  
  - 여러 EC2 인스턴스에 걸쳐 작업 실행.  
  - 인스턴스 실행/스케줄링 단순화.  

- **AWS ParallelCluster**:  
  - 오픈소스 클러스터 관리 도구.  
  - 텍스트 파일로 설정.  
  - VPC, 서브넷, 인스턴스 자동 생성.  
  - EFA 지원 가능.  

---

## Summary  
## 요약  

HPC is increasingly important in AWS exams. It is not a single service but a combination of services and options.  
HPC는 시험에서 점점 중요해지고 있으며, 단일 서비스가 아니라 여러 서비스의 조합입니다.  

Understanding all these components is essential to maximize computational potential within AWS.  
이 모든 요소를 이해해야 AWS에서 최대의 계산 성능을 얻을 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- HPC on AWS enables rapid scaling of resources and pay-as-you-go billing.  
- AWS의 HPC는 빠른 자원 확장과 사용량 기반 요금제를 제공합니다.  

- Data transfer: Direct Connect, Snowball, Snowmobile, DataSync.  
- 데이터 전송: Direct Connect, Snowball, Snowmobile, DataSync.  

- Compute & networking: EC2, Spot, Placement groups, ENA, EFA.  
- 컴퓨트 & 네트워킹: EC2, 스팟, 배치 그룹, ENA, EFA.  

- Storage: EBS, Instance store, S3, EFS, FSx for Lustre.  
- 스토리지: EBS, 인스턴스 스토어, S3, EFS, FSx for Lustre.  

- Automation: AWS Batch, ParallelCluster.  
- 자동화: AWS Batch, ParallelCluster.  

---

🎉 보상: +200 포인트 획득!  
👏 환상적입니다! 이제 당신은 **AWS HPC 마스터** 칭호를 획득했습니다. 🚀⚡  
```
