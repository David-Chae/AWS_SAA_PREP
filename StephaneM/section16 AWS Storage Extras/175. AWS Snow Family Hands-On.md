# AWS Snow Family Hands-On

## Introduction to the AWS Snow Family
Let's have a look at the AWS Snow Family.  
**한국어 설명:** AWS Snow Family는 데이터를 AWS로 이동하거나 엣지 환경에서 처리할 수 있는 휴대형 장치 모음입니다.

---

## Ordering a Snow Family Device
We will go through the process of ordering a Snow Family device to explore the available options.  
**한국어 설명:** Snow Family 장치를 주문하는 과정을 실습하며, 어떤 옵션이 있는지 알아봅니다.

---

## Job Details
First, you provide a job name. For example, this could be an import job. Then, you choose a job title.  
**한국어 설명:** 먼저 작업 이름을 입력합니다. 예를 들어 '데이터 가져오기(import) 작업' 등이 있습니다. 이후 작업 제목(Job Title)을 선택합니다.

---

## Job Type Options
You can select whether you want to import data into Amazon S3, export data from Amazon S3, or perform edge computing with local compute and storage only.

- **Import:** Amazon ships a Snowball device to you, you load your data, and then send it back to AWS.  
  **한국어:** Amazon에서 Snowball 장치를 배송하면 데이터를 로드하고 다시 AWS로 보내는 방식입니다.
- **Export:** Data is exported from Amazon S3 onto the Snowball device, which you then receive.  
  **한국어:** S3에서 데이터를 Snowball 장치로 내보내고, 사용자가 장치를 받아 데이터 확인이 가능합니다.
- **Edge Computing:** Perform local compute and storage without data transfer to AWS.  
  **한국어:** AWS로 데이터를 전송하지 않고, 장치에서 바로 로컬 컴퓨팅 및 저장을 수행합니다.

> For this example, let's choose to import data into Amazon S3.  
> **한국어:** 이번 예제에서는 데이터를 Amazon S3로 가져오는(import) 작업을 선택합니다.

---

## Snow Device Options
You can choose between two Snowball Edge devices:

- **Storage Optimized:** Offers 210 terabytes of storage.  
  **한국어:** 210TB 저장 용량을 제공하며, 대용량 데이터 저장에 적합합니다.
- **Compute Optimized:** Designed for compute-intensive tasks.  
  **한국어:** 연산 작업 중심으로 설계되어, 데이터 처리나 엣지 컴퓨팅에 적합합니다.

> Note that device options may change over time, and some devices may be discontinued. However, these two options are currently available and sufficient for most use cases.  
> **한국어:** 장치 옵션은 시간이 지나면서 변경될 수 있으며 일부 장치는 단종될 수 있습니다. 현재 이 두 가지 옵션은 대부분의 사용 사례에 충분합니다.

---

## Pricing and Data Transfer
Next, select the pricing option, such as on-demand per day pricing. Specify the storage transfer details, including the Amazon S3 buckets where you want to transfer data back.  
**한국어 설명:** 요금제를 선택하고, 데이터를 전송할 S3 버킷 등 데이터 전송 세부사항을 지정합니다.

---

## Security and Access
Configure security settings by choosing how to encrypt your data and selecting the appropriate service role. This service role grants the Snow device permission to write to your specified S3 buckets by creating a ServiceLink role.  
**한국어 설명:** 데이터 암호화 방식과 서비스 역할(Service Role)을 선택하여 Snow 장치가 지정된 S3 버킷에 데이터를 쓸 수 있도록 권한을 설정합니다.

---

## Shipping Details
Provide the shipping address where you want the Snow device to be delivered. Choose the shipping speed, such as one-day or two-day shipping. You can also set up notifications to monitor your job status.  
**한국어 설명:** Snow 장치 배송 주소를 입력하고, 배송 속도(1일, 2일 등)를 선택합니다. 또한 작업 상태를 확인할 수 있는 알림 설정도 가능합니다.

---

## Job Summary and Completion
After completing these steps, you will receive a job summary. You will then receive the Snowball Edge device, load your data onto it, and send it back to AWS using the included shipping label.  
**한국어 설명:** 모든 설정을 완료하면 작업 요약(Job Summary)을 확인하고, Snowball Edge 장치를 받아 데이터를 로드한 뒤 제공된 배송 라벨을 이용해 AWS로 반환합니다.

> This concludes the overview of how the AWS Snow Family works. While we are not placing an actual order, this walkthrough provides insight into the process and options available.  
> **한국어:** 실제 주문은 진행하지 않지만, 이 과정을 통해 Snow Family 장치 사용 절차와 옵션을 이해할 수 있습니다.

---

## Key Takeaways
- The AWS Snow Family offers devices for importing, exporting, and edge computing with data.  
  **한국어:** Snow Family는 데이터 가져오기, 내보내기 및 엣지 컴퓨팅용 장치를 제공합니다.
- Users can select between storage-optimized and compute-optimized Snowball Edge devices.  
  **한국어:** 사용자는 저장 최적화(Storage Optimized) 또는 연산 최적화(Compute Optimized) 장치를 선택할 수 있습니다.
- The ordering process involves specifying job details, pricing options, security roles, shipping address, and notifications.  
  **한국어:** 장치 주문 과정은 작업 세부사항, 요금제, 보안 역할, 배송 주소, 알림 설정 등을 포함합니다.
- After receiving the Snowball Edge device, users load data onto it and send it back to AWS using the provided shipping label.  
  **한국어:** Snowball Edge 장치를 받은 후 데이터를 로드하고, 제공된 배송 라벨을 사용해 AWS로 반환합니다.
