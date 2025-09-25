# EBS Encryption
# EBS 암호화
> Amazon EBS 볼륨 암호화 기능 소개  
> 설명: EBS Encryption을 주제로 하는 문서의 제목입니다.

## EBS Volume Encryption Overview
## EBS 볼륨 암호화 개요
> When you create an encrypted EBS volume, data at rest inside the volume is encrypted immediately. Additionally, all data in transit between the instance and the volume is encrypted. Snapshots taken from the volume are also encrypted, and any volumes created from those snapshots inherit encryption. This comprehensive encryption and decryption process is handled transparently by EC2 and EBS, requiring no manual intervention.
> 암호화된 EBS 볼륨을 생성하면, 볼륨 내부에 저장된 데이터는 즉시 암호화됩니다. 또한 인스턴스와 볼륨 간 전송되는 모든 데이터도 암호화됩니다. 볼륨에서 생성된 스냅샷도 암호화되며, 그 스냅샷으로 생성된 모든 볼륨도 암호화를 상속받습니다. 이 전체적인 암호화 및 복호화 과정은 EC2와 EBS가 투명하게 처리하며, 사용자의 수동 개입이 필요하지 않습니다.
> 설명: EBS 암호화가 데이터 저장, 전송, 스냅샷, 파생 볼륨까지 포괄적으로 적용됨을 강조합니다.

> Encryption has a very minimal impact on latency, almost negligible. It leverages keys from AWS Key Management Service (KMS) and uses AES-256 encryption standards.
> 암호화는 지연(latency)에 거의 영향을 주지 않으며, 무시할 수준입니다. AWS Key Management Service(KMS)의 키를 사용하고 AES-256 암호화 표준을 적용합니다.
> 설명: 암호화 성능 영향과 KMS 연동, AES-256 사용을 명확히 언급합니다.

## Encrypting an Unencrypted EBS Volume
## 암호화되지 않은 EBS 볼륨 암호화
> To encrypt an existing unencrypted EBS volume, follow these steps:
> 기존에 암호화되지 않은 EBS 볼륨을 암호화하려면 다음 단계를 따릅니다:
> 설명: 기존 볼륨 암호화 절차를 안내합니다.

1. Create a snapshot of the unencrypted volume.  
1. 암호화되지 않은 볼륨의 스냅샷을 생성합니다.  
> 설명: 원본 볼륨의 현재 상태를 스냅샷으로 저장합니다.

2. Copy the snapshot and enable encryption during the copy process.  
2. 스냅샷을 복사하고, 복사 과정에서 암호화를 활성화합니다.  
> 설명: 복사 과정에서 암호화를 적용하여 새 스냅샷을 생성합니다.

3. Create a new EBS volume from the encrypted snapshot.  
3. 암호화된 스냅샷으로 새로운 EBS 볼륨을 생성합니다.  
> 설명: 암호화된 새 볼륨을 생성하는 단계입니다.

4. Attach the new encrypted volume to the original instance.  
4. 새로 생성된 암호화 볼륨을 원래 인스턴스에 연결합니다.  
> 설명: 기존 인스턴스에 암호화 볼륨을 적용하여 완료합니다.

## Demonstration in AWS Console
## AWS 콘솔에서 시연
> Let's explore the encryption options for EBS volumes in the AWS Management Console.
> AWS Management Console에서 EBS 볼륨의 암호화 옵션을 살펴봅시다.
> 설명: 콘솔에서 실제 설정 방법을 안내하는 섹션입니다.

> First, create a one gigabyte EBS volume without encryption by leaving the encryption setting unchecked. Upon creation, the volume's encryption status will show as "not encrypted."
> 먼저, 암호화 설정을 체크하지 않고 1GB EBS 볼륨을 생성합니다. 생성 후 볼륨의 암호화 상태는 "암호화되지 않음(not encrypted)"으로 표시됩니다.
> 설명: 기본 상태에서의 볼륨 생성과 암호화 상태 확인 방법입니다.

> Creating a snapshot from this unencrypted volume will result in a snapshot that is also not encrypted. This is because snapshots inherit the encryption status of their source volumes.
> 이 암호화되지 않은 볼륨에서 스냅샷을 생성하면, 스냅샷 역시 암호화되지 않습니다. 이는 스냅샷이 원본 볼륨의 암호화 상태를 상속하기 때문입니다.
> 설명: 스냅샷의 암호화 상태 상속 규칙을 설명합니다.

> To create an encrypted snapshot from an unencrypted one, use the "Copy Snapshot" action. During the copy, you can enable encryption and select the desired KMS key. This process creates a new encrypted snapshot in the same destination region.
> 암호화되지 않은 스냅샷에서 암호화된 스냅샷을 생성하려면, "Copy Snapshot" 기능을 사용합니다. 복사 과정에서 암호화를 활성화하고 원하는 KMS 키를 선택할 수 있습니다. 이렇게 하면 동일한 대상 리전에 새 암호화 스냅샷이 생성됩니다.
> 설명: 암호화되지 않은 스냅샷을 암호화 스냅샷으로 전환하는 방법을 안내합니다.

> Once the encrypted snapshot copy is complete, create a new EBS volume from this encrypted snapshot. The new volume will have encryption enabled by default, reflecting the encryption status of the underlying snapshot.
> 암호화된 스냅샷 복사가 완료되면, 이를 기반으로 새로운 EBS 볼륨을 생성합니다. 새 볼륨은 기본적으로 암호화가 활성화되어 있으며, 이는 기반 스냅샷의 암호화 상태를 반영합니다.
> 설명: 암호화된 새 볼륨 생성 단계와 기본 상태를 명확히 합니다.

> The new encrypted volume can then be attached to the original instance, completing the encryption process for the previously unencrypted volume.
> 새 암호화 볼륨을 원래 인스턴스에 연결하면, 이전에 암호화되지 않았던 볼륨의 암호화 과정이 완료됩니다.
> 설명: 전체 암호화 절차 완료 단계입니다.

## Shortcut for Enabling Encryption
## 암호화 활성화 단축 방법
> Alternatively, when creating a volume from an unencrypted snapshot, you can enable encryption on the fly in the console. Simply select the snapshot, choose "Create Volume," and enable encryption by selecting the appropriate KMS key before creating the volume. This method simplifies the encryption process without needing to copy the snapshot separately.
> 또는, 암호화되지 않은 스냅샷에서 볼륨을 생성할 때 콘솔에서 즉시 암호화를 활성화할 수 있습니다. 스냅샷을 선택하고 "Create Volume"을 선택한 후, 볼륨 생성 전에 적절한 KMS 키를 선택하여 암호화를 활성화하면 됩니다. 이 방법은 스냅샷을 별도로 복사하지 않아도 되므로 암호화 과정을 단순화합니다.
> 설명: 별도의 스냅샷 복사 없이 바로 암호화하는 방법을 안내합니다.

## Cleanup
## 정리
> After completing your tests or operations, remember to delete any snapshots and volumes you no longer need to avoid unnecessary charges.
> 테스트나 작업이 끝난 후, 필요 없는 스냅샷과 볼륨은 삭제하여 불필요한 비용이 발생하지 않도록 합니다.
> 설명: 비용 관리와 정리 방법을 안내합니다.

## Key Takeaways
## 핵심 요약
> Encrypting an EBS volume secures data at rest, in transit, snapshots, and derived volumes transparently.
> EBS 볼륨 암호화는 저장 데이터, 전송 데이터, 스냅샷, 파생 볼륨까지 투명하게 보호합니다.
> 설명: 암호화 범위와 효과 강조

> Encryption uses AES-256 and integrates with AWS KMS keys with minimal latency impact.
> 암호화는 AES-256을 사용하며 AWS KMS 키와 통합되어 지연 영향이 거의 없습니다.
> 설명: 암호화 방식과 성능 영향 강조

> To encrypt an unencrypted EBS volume, create a snapshot, copy it with encryption enabled, then create a new encrypted volume from that snapshot.
> 암호화되지 않은 EBS 볼륨을 암호화하려면, 스냅샷을 생성하고, 암호화를 활성화해 복사한 후, 해당 스냅샷으로 새 암호화 볼륨을 생성합니다.
> 설명: 기존 볼륨 암호화 절차 요약

> The AWS console allows enabling encryption on the fly when creating volumes from snapshots, simplifying the process.
> AWS 콘솔에서는 스냅샷에서 볼륨 생성 시 즉시 암호화를 활성화할 수 있어, 과정을 단순화합니다.
> 설명: 콘솔에서 바로 암호화 활성화 가능성을 요약
