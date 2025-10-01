# S3 Storage Classes Hands On  
# S3 스토리지 클래스 실습  

---

## Creating an S3 Bucket and Uploading an Object  
## S3 버킷 생성 및 객체 업로드  

Let's create a new bucket named s3-storage-classes-demos-2022 in any region.  
어떤 리전에서든 s3-storage-classes-demos-2022라는 이름으로 새로운 버킷을 생성합니다.  

After creating the bucket, we can upload an object by clicking on "Add files" and selecting coffee.JPEG.  
버킷을 생성한 후, "Add files"를 클릭하고 coffee.JPEG 파일을 선택하여 객체를 업로드합니다.  
👉 설명: 먼저 버킷을 만들고 그 안에 파일을 업로드하는 기본 과정을 실습합니다.  

---

## Exploring Storage Class Options  
## 스토리지 클래스 옵션 탐색  

Upon uploading, we can view the properties of the object.  
파일 업로드 후, 객체의 속성을 확인할 수 있습니다.  

Under the storage class section, AWS provides a wide range of storage classes for objects.  
스토리지 클래스 섹션에서 AWS는 객체용 다양한 스토리지 클래스를 제공합니다.  

These include details such as the number of Availability Zones (AZs), minimum storage duration, minimum billable object size, monitoring, and auto-tiering fees.  
여기에는 AZ 수, 최소 저장 기간, 최소 청구 대상 객체 크기, 모니터링 및 자동 계층 조정 비용 등의 정보가 포함됩니다.  

The available storage classes are:  
사용 가능한 스토리지 클래스는 다음과 같습니다:  

- **Standard**: The default basic storage class.  
- **Standard**: 기본 스토리지 클래스  

- **Intelligent-Tiering**: Automatically moves data between tiers based on access patterns when data patterns are unknown.  
- **Intelligent-Tiering**: 데이터 접근 패턴이 불분명할 때, 접근 빈도에 따라 자동으로 계층 이동  

- **Standard-IA (Infrequent Access)**: For data accessed infrequently but requiring low latency.  
- **Standard-IA (Infrequent Access)**: 드물게 접근하지만 저지연이 필요한 데이터용  

- **One-Zone-IA**: Stores data in a single AZ, suitable if data can be recreated; carries risk if the AZ is destroyed.  
- **One-Zone-IA**: 단일 AZ에 데이터 저장, 데이터 재생 가능 시 적합, AZ가 파괴되면 위험 존재  

- **Glacier Storage Classes**:  
- **Glacier 스토리지 클래스**:  

  - Glacier Instant Retrieval  
  - Glacier Instant Retrieval - 즉시 조회 가능  

  - Glacier Flexible Retrieval  
  - Glacier Flexible Retrieval - 유연 조회  

  - Glacier Deep Archive  
  - Glacier Deep Archive - 장기 보관  

- **Reduced Redundancy**: A deprecated storage tier not covered in this course.  
- **Reduced Redundancy**: 폐기된 스토리지 계층, 이번 강의에서는 다루지 않음  

---

## Uploading an Object with Standard-IA Storage Class  
## Standard-IA 스토리지 클래스로 객체 업로드  

For example, if we select the Standard-IA storage class and upload an object, the object will be stored accordingly.  
예를 들어 Standard-IA 스토리지 클래스를 선택하고 객체를 업로드하면 해당 클래스에 맞게 저장됩니다.  

After upload, the object's storage class is shown as Standard-IA.  
업로드 후, 객체의 스토리지 클래스가 Standard-IA로 표시됩니다.  

---

## Changing the Storage Class of an Existing Object  
## 기존 객체의 스토리지 클래스 변경  

We can also change the storage class of an existing object.  
기존 객체의 스토리지 클래스도 변경할 수 있습니다.  

By going into the object's properties and scrolling down, we can edit the storage class.  
객체 속성에서 스크롤하여 스토리지 클래스를 편집합니다.  

For instance, changing it to One-Zone-IA will store the object in a single AZ only.  
예를 들어 One-Zone-IA로 변경하면 객체가 단일 AZ에만 저장됩니다.  

After saving, the object's storage class updates accordingly.  
저장 후, 객체의 스토리지 클래스가 업데이트됩니다.  

Similarly, we can change it to Glacier Instant Retrieval or Intelligent-Tiering, allowing automatic tiering based on access patterns.  
마찬가지로 Glacier Instant Retrieval이나 Intelligent-Tiering으로 변경하면 접근 패턴에 따라 자동 계층 이동이 가능합니다.  

---

## Automating Storage Class Transitions with Lifecycle Rules  
## 라이프사이클 규칙으로 스토리지 클래스 자동 전환  

To automate moving objects between storage classes, navigate to the bucket's Management tab and create lifecycle rules.  
객체를 스토리지 클래스 간 자동 전환하려면 버킷 Management 탭에서 라이프사이클 규칙을 생성합니다.  

For example, create a rule named "DemoRule" that applies to all objects in the bucket.  
예를 들어 모든 객체에 적용되는 "DemoRule" 규칙을 생성합니다.  

Configure the rule to transition current object versions between storage classes:  
규칙을 다음과 같이 설정합니다:  

- Move to Standard-IA after 30 days.  
- 30일 후 Standard-IA로 이동  

- Move to Intelligent-Tiering after 60 days.  
- 60일 후 Intelligent-Tiering으로 이동  

- Move to Glacier Flexible Retrieval after 180 days.  
- 180일 후 Glacier Flexible Retrieval로 이동  

These transitions can be reviewed and adjusted as needed, enabling automated tiering of objects based on their lifecycle.  
필요 시 전환을 검토하고 조정할 수 있으며, 객체의 라이프사이클에 따라 자동 계층 이동을 가능하게 합니다.  

---

## Conclusion  
## 결론  

We have explored the various AWS S3 storage classes, how to upload objects with specific storage classes, change storage classes of existing objects, and automate transitions using lifecycle rules.  
AWS S3의 다양한 스토리지 클래스, 특정 스토리지 클래스로 객체 업로드, 기존 객체의 클래스 변경, 라이프사이클 규칙으로 자동 전환 기능을 실습했습니다.  

This knowledge enables efficient and cost-effective data storage management in AWS S3.  
이 지식을 통해 AWS S3에서 효율적이고 비용 효과적인 데이터 관리가 가능합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS S3 offers multiple storage classes tailored for different data access patterns and durability needs.  
- AWS S3는 다양한 데이터 접근 패턴과 내구성 요구에 맞춘 여러 스토리지 클래스를 제공합니다.  

- Storage classes include Standard, Intelligent-Tiering, Standard-IA, One-Zone-IA, and various Glacier options.  
- 스토리지 클래스에는 Standard, Intelligent-Tiering, Standard-IA, One-Zone-IA, 다양한 Glacier 옵션이 포함됩니다.  

- Storage class of an object can be changed after upload via the object's properties.  
- 객체 업로드 후 속성에서 스토리지 클래스를 변경할 수 있습니다.  

- Lifecycle rules enable automated transitioning of objects between storage classes based on specified time intervals.  
- 라이프사이클 규칙을 통해 지정된 기간에 따라 객체를 자동으로 스토리지 클래스 간 이동시킬 수 있습니다.  

🎮 **게임보상:**

* **“S3 스토리지 클래스 실습 완료!”**

  * 버킷 생성 +10
  * 객체 업로드 +10
  * 스토리지 클래스 변경 +20
  * 라이프사이클 자동 전환 +30
    총 **70 XP 획득!** 🎉
