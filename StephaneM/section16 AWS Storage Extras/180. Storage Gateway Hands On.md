# Storage Gateway Hands On

## Introduction to Storage Gateway
Let's explore Storage Gateway and how to create a gateway.  
We start by naming the gateway. For this example, we will call it **Demo Gateway**.

**한국어 설명:**  
Storage Gateway는 온프레미스와 AWS 클라우드를 연결하는 다리 역할을 합니다. 이 실습에서는 게이트웨이를 생성하고 주요 옵션을 확인합니다. 예제에서는 게이트웨이 이름을 Demo Gateway로 지정합니다.

---

## Gateway Options
The available gateway types include:  
- **Amazon S3 File Gateway:** Provides access to files in Amazon S3 directly through NFS or SMB file protocols with local caching.  
- **FSx Gateway:** This option is grayed out as it is being deprecated.  
- **Tape Gateway**  
- **Volume Gateway**

**한국어 설명:**  
게이트웨이 종류는 S3 파일 게이트웨이, FSx 게이트웨이(사용 중단 예정), 테이프 게이트웨이, 볼륨 게이트웨이가 있습니다.

---

## Amazon S3 File Gateway Hosting Options
The Amazon S3 file gateway can be hosted in several environments:  
- VMware  
- Microsoft Hyper-V  
- Linux KVM  
- Amazon EC2  

Launching on Amazon EC2 means that your caching and gateway reside within your AWS account, which may or may not be desirable depending on your use case.  

Using VMware, Microsoft Hyper-V, or Linux KVM allows you to set up the storage gateway directly on premises in your data center. Consequently, the Amazon S3 data will reside closer to your servers, which may be more desirable depending on your requirements.

**한국어 설명:**  
S3 파일 게이트웨이는 다양한 환경에서 호스팅할 수 있습니다.  
- EC2에서 실행하면 AWS 계정 내에서 캐싱과 게이트웨이가 관리됩니다.  
- VMware, Hyper-V, Linux KVM을 사용하면 온프레미스에서 직접 설정하여 데이터가 서버에 가까이 위치하게 됩니다.  

---

## Tape Gateway
Tape gateway supports different platform options and provides a tape archive solution using iSCSI-VTL.  
The tapes are stored in Amazon S3 Glacier for long-term archival.

**한국어 설명:**  
테이프 게이트웨이는 iSCSI-VTL을 사용해 가상 테이프 라이브러리를 제공하며, 데이터는 장기 보관을 위해 S3 Glacier에 저장됩니다.

---

## Volume Gateway
Volume gateway offers block storage volumes backed by Amazon S3. There are two main options:  
- **Cached Volume:** Primary data is stored in Amazon S3, while frequently accessed data is retained locally in cache for low-latency access.  
- **Stored Volume:** The entire dataset is stored locally and synchronized asynchronously to Amazon S3.  

You can select different platform options for volume gateway as well, such as VMware, Microsoft Hyper-V, or Linux KVM.

**한국어 설명:**  
볼륨 게이트웨이는 블록 스토리지를 제공하며 S3와 연결됩니다.  
- 캐시드 볼륨: 주 데이터는 S3에, 자주 접근하는 데이터는 로컬 캐시에 유지하여 빠른 접근 제공  
- 저장된 볼륨: 모든 데이터를 로컬에 저장하고 비동기적으로 S3와 동기화  

---

## Conclusion
These are the primary options available for Storage Gateway. I hope this overview was helpful, and I look forward to seeing you in the next lecture.

**한국어 설명:**  
Storage Gateway의 주요 옵션과 각 특성을 확인했습니다. 다음 강의에서는 보다 심화된 실습으로 이어집니다.

---

## Key Takeaways
- Storage Gateway offers multiple gateway types including Amazon S3 file gateway, tape gateway, and volume gateway.  
- Amazon S3 file gateway supports access via NFS or SMB protocols with local caching and can be hosted on VMware, Microsoft Hyper-V, Linux KVM, or Amazon EC2.  
- Tape gateway provides a tape archive solution using iSCSI-VTL with storage in Amazon S3 Glacier.  
- Volume gateway offers cached and stored volume options, balancing local storage and Amazon S3 synchronization based on use case.

**한국어 요약:**  
- Storage Gateway는 S3 파일 게이트웨이, 테이프 게이트웨이, 볼륨 게이트웨이를 포함한 다양한 게이트웨이를 제공합니다.  
- S3 파일 게이트웨이는 NFS/SMB 프로토콜로 접근 가능하며, 로컬 캐싱을 지원하고 다양한 호스팅 환경에서 실행할 수 있습니다.  
- 테이프 게이트웨이는 iSCSI-VTL 기반 가상 테이프 아카이브 솔루션을 제공하며 S3 Glacier에 저장됩니다.  
- 볼륨 게이트웨이는 캐시드/저장 볼륨 옵션을 제공하여 사용 사례에 따라 로컬과 S3 동기화를 조절할 수 있습니다.
