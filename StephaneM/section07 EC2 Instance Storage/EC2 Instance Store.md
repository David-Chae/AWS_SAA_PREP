# EC2 Instance Store  
# EC2 인스턴스 스토어  

## Introduction to EC2 Instance Store  
## EC2 인스턴스 스토어 소개  

We have previously seen how to attach a network drive to our EC2 instances.  
이전에 EC2 인스턴스에 네트워크 드라이브를 연결하는 방법을 살펴보았습니다.  

While these network drives offer good performance, sometimes even higher performance is required.  
이 네트워크 드라이브도 좋은 성능을 제공하지만, 때때로 더 높은 성능이 필요할 수 있습니다.  

This higher performance can be achieved by using a hardware disk attached directly to your EC2 instance.  
이런 고성능은 EC2 인스턴스에 직접 연결된 하드웨어 디스크를 사용하여 얻을 수 있습니다.  

An EC2 instance is a virtual machine, but it is connected to a physical hardware server.  
EC2 인스턴스는 가상 머신이지만 물리적 하드웨어 서버에 연결되어 있습니다.  

Some of these servers have disk space physically attached with a direct connection.  
이 서버들 중 일부는 직접 연결된 물리적 디스크 공간을 갖고 있습니다.  

A special type of EC2 instance can leverage what is called an EC2 Instance Store, which refers to the hard drive attached to the physical server.  
특정 EC2 인스턴스 유형은 EC2 인스턴스 스토어라고 하는 기능을 활용할 수 있으며, 이는 물리 서버에 연결된 하드 드라이브를 의미합니다.  

## Benefits and Characteristics of EC2 Instance Store  
## EC2 인스턴스 스토어의 장점과 특징  

EC2 Instance Store is used to achieve better I/O performance and ensure good throughput.  
EC2 인스턴스 스토어는 향상된 I/O 성능과 안정적인 처리량을 위해 사용됩니다.  

It is an excellent choice when extremely high disk performance is required.  
매우 높은 디스크 성능이 필요한 경우 훌륭한 선택입니다.  

However, there is an important caveat: if you stop or terminate your EC2 instance that has an Instance Store, the storage will be lost.  
하지만 중요한 주의사항이 있습니다. 인스턴스 스토어가 있는 EC2 인스턴스를 중지하거나 종료하면 저장된 데이터가 모두 사라집니다.  

Because of this, EC2 Instance Store is called ephemeral storage.  
이 때문에 EC2 인스턴스 스토어는 휘발성 스토리지(ephemeral storage)라고 불립니다.  

This means it cannot be used as a durable, long-term place to store your data.  
즉, 장기적으로 데이터를 저장하는 내구성 있는 스토리지로 사용할 수 없습니다.  

## Appropriate Use Cases for EC2 Instance Store  
## EC2 인스턴스 스토어의 적절한 사용 사례  

So, what is a good use case for EC2 Instance Store?  
그렇다면 EC2 인스턴스 스토어의 적절한 사용 사례는 무엇일까요?  

It is ideal for buffers, caches, scratch data, or temporary content.  
버퍼, 캐시, 임시 데이터 또는 일시적인 콘텐츠에 적합합니다.  

However, it is not suitable for long-term storage.  
하지만 장기 저장소에는 적합하지 않습니다.  

For long-term storage, Amazon Elastic Block Store (EBS) is a great option.  
장기 저장소의 경우 Amazon Elastic Block Store(EBS)가 좋은 선택입니다.  

In the event that the physical server hosting the EC2 instance fails, you risk data loss because the hardware attached to the EC2 instance will also fail.  
EC2 인스턴스를 호스팅하는 물리 서버가 실패하면, 인스턴스에 연결된 하드웨어도 실패하므로 데이터 손실 위험이 있습니다.  

Therefore, if you decide to use EC2 Instance Store, it is your responsibility to back up and replicate the data according to your needs.  
따라서 EC2 인스턴스 스토어를 사용하기로 결정하면, 데이터 백업과 복제를 직접 관리해야 합니다.  

## Performance Illustration  
## 성능 예시  

To illustrate the performance benefits, consider the instance size I3.x instances, which come with an Instance Store attached.  
성능 예시로, 인스턴스 스토어가 포함된 I3.x 인스턴스를 고려해봅니다.  

The Read IOPS and Write IOPS, which correspond to the number of input/output operations per second, can reach up to 3.3 million and 1.4 million respectively for the most performant instance.  
가장 성능이 높은 인스턴스의 경우, 초당 입출력 연산 수인 Read IOPS와 Write IOPS가 각각 최대 330만과 140만까지 도달할 수 있습니다.  

In comparison, an EBS volume of type gp2 can reach up to 32,000 IOPS.  
비교하면, gp2 타입 EBS 볼륨은 최대 32,000 IOPS까지 도달할 수 있습니다.  

This demonstrates the significantly higher performance of Instance Store volumes.  
이는 인스턴스 스토어 볼륨이 훨씬 높은 성능을 제공함을 보여줍니다.  

From an exam perspective, whenever you see a very high-performance hardware-attached volume for your EC2 instances, think of local EC2 Instance Store.  
시험 관점에서, EC2 인스턴스에 매우 고성능 하드웨어 연결 볼륨이 있다면 로컬 EC2 인스턴스 스토어를 떠올리세요.  

That concludes this lecture on EC2 Instance Store. I will see you in the next lecture.  
이로써 EC2 인스턴스 스토어 강의를 마치며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- EC2 Instance Store provides hardware-attached disk storage for EC2 instances, offering extremely high I/O performance.  
- EC2 인스턴스 스토어는 EC2 인스턴스에 하드웨어 연결 디스크 스토리지를 제공하며, 매우 높은 I/O 성능을 제공합니다.  

- Instance Store storage is ephemeral and data is lost if the instance is stopped or terminated.  
- 인스턴스 스토어는 휘발성이며, 인스턴스를 중지하거나 종료하면 데이터가 손실됩니다.  

- Ideal use cases for Instance Store include buffers, caches, and temporary data, but not long-term storage.  
- 버퍼, 캐시, 임시 데이터 등 단기 저장에 적합하지만 장기 저장에는 적합하지 않습니다.  

- Users are responsible for backing up and replicating data stored on Instance Store to prevent data loss.  
- 사용자는 데이터 손실을 방지하기 위해 인스턴스 스토어에 저장된 데이터를 백업 및 복제할 책임이 있습니다.  
