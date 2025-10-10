# EBS Snapshots - Hands On  
# EBS 스냅샷 실습  
👉 이 강의에서는 EBS 스냅샷 생성, 복사, 복원, 삭제 및 보호 기능을 실습합니다.  

---

## Introduction to EBS Snapshots  
## EBS 스냅샷 소개  

We have a two-gigabyte GP2 EBS volume available to us, and we can take a snapshot from it.  
우리는 2GB GP2 EBS 볼륨을 가지고 있으며, 여기서 스냅샷을 생성할 수 있습니다.  
👉 실제 볼륨 데이터를 기준으로 스냅샷 생성 실습을 시작합니다.  

To do this, under Actions, select Create snapshot.  
이를 위해 Actions 메뉴에서 Create snapshot을 선택합니다.  

You can add a description, for example, "DemoSnapshots," and then click on Create snapshots.  
설명을 추가할 수 있습니다(예: "DemoSnapshots") 후 Create snapshots를 클릭합니다.  
👉 설명을 통해 나중에 스냅샷을 쉽게 식별할 수 있습니다.  

---

## Viewing Snapshots  
## 스냅샷 확인  

On the left-hand side menu, instead of Volumes, click on Snapshots.  
왼쪽 메뉴에서 Volumes 대신 Snapshots를 클릭합니다.  

This shows a list of all the snapshots you have.  
이 메뉴에서 모든 스냅샷 목록을 확인할 수 있습니다.  

As you can see, we have one right here. It is completed and 100% available.  
여기서 하나의 스냅샷이 완료되었고 100% 사용 가능함을 확인할 수 있습니다.  

We also get some information about the snapshot itself.  
스냅샷 자체에 대한 세부 정보도 확인할 수 있습니다.  

---

## Copying Snapshots Across Regions  
## 리전 간 스냅샷 복사  

First, we can copy this snapshot into another region.  
먼저, 이 스냅샷을 다른 리전으로 복사할 수 있습니다.  

Right-click and select Copy Snapshots.  
스냅샷을 마우스 오른쪽 버튼으로 클릭 후 Copy Snapshots를 선택합니다.  

You can then copy the snapshot into any destination region you want.  
원하는 대상 리전으로 스냅샷을 복사할 수 있습니다.  

This is very useful if you want, for example, to have a disaster recovery strategy to ensure data is backed up in another AWS region.  
예를 들어, 재해 복구 전략을 위해 다른 AWS 리전에 데이터를 백업하려는 경우 유용합니다.  

I will not perform this action now, but you get the idea.  
지금은 실행하지 않지만, 기능 이해에는 충분합니다.  

---

## Creating a Volume from a Snapshot  
## 스냅샷에서 볼륨 생성  

Another option is to take the snapshot and recreate a volume from it.  
또 다른 옵션은 스냅샷을 이용해 새로운 볼륨을 생성하는 것입니다.  

Under Actions, select Create volume from snapshots.  
Actions 메뉴에서 Create volume from snapshots를 선택합니다.  

Choose a two-gigabyte GP2 volume.  
2GB GP2 볼륨을 선택합니다.  

The target Availability Zone does not have to remain eu-west-1a; it can be, for example, eu-west-1b.  
대상 가용 영역(AZ)은 반드시 eu-west-1a일 필요 없으며, 예를 들어 eu-west-1b를 선택할 수 있습니다.  

You can also encrypt these volumes if desired and add tags.  
원하면 볼륨을 암호화하고 태그를 추가할 수 있습니다.  

When you click on Create volume, the volume will be created.  
Create volume를 클릭하면 볼륨이 생성됩니다.  

---

## Managing Volumes  
## 볼륨 관리  

If we go back into our Volumes, we now have two volumes.  
볼륨 메뉴로 돌아가면, 이제 두 개의 볼륨이 존재합니다.  

One of them was restored through a snapshot, and it is in eu-west-1b.  
그 중 하나는 스냅샷으로 복원되었으며, eu-west-1b에 위치합니다.  

Thanks to snapshots, we can effectively copy EBS volumes across different Availability Zones, which is very handy.  
스냅샷 덕분에 EBS 볼륨을 다른 AZ로 손쉽게 복사할 수 있습니다.  

---

## The Recycle Bin for Snapshots  
## 스냅샷 휴지통  

Looking again at Snapshots, we can explore the Recycle Bin.  
스냅샷 메뉴에서 Recycle Bin 기능을 살펴봅니다.  

The Recycle Bin protects your EBS snapshots from accidental deletion, as well as your Amazon Machine Images.  
휴지통은 EBS 스냅샷과 AMI를 실수로 삭제하는 것을 방지합니다.  

You can create a retention rule and name it, for example, "DemoRetentionRule."  
보존 규칙을 생성하고, 예를 들어 "DemoRetentionRule"이라고 이름을 지정합니다.  

Select EBS Snapshots, apply to all resources, and retain them for one day.  
EBS 스냅샷을 선택하고, 모든 리소스에 적용하며, 1일 동안 보존하도록 설정합니다.  

For the Rule Lock Setting, leave it unlocked so you can delete this rule whenever you want.  
Rule Lock 설정은 잠금 해제 상태로 두어 언제든지 삭제 가능하게 합니다.  

Then click on Create Retention Rule.  
Create Retention Rule을 클릭합니다.  

---

## Viewing Resources in the Recycle Bin  
## 휴지통 내 리소스 확인  

Now, under Resources, you can see if you have any resources in the Recycle Bin.  
Resources 메뉴에서 휴지통에 리소스가 있는지 확인할 수 있습니다.  

Let's go back into our Snapshots in the EC2 Console.  
EC2 콘솔에서 Snapshots 메뉴로 돌아갑니다.  

Navigate to EC2, then Snapshots.  
EC2 → Snapshots 경로로 이동합니다.  

I will take the snapshot and, before deleting it, show you the storage tiers.  
삭제 전에 스냅샷을 선택하고, 스토리지 티어를 확인합니다.  

---

## Storage Tiers  
## 스토리지 티어  

Currently, the snapshot is in the Standard Storage Tier.  
현재 스냅샷은 Standard Storage Tier에 있습니다.  

You can move the storage tier by archiving snapshots, which moves them into another pricing level.  
스냅샷을 아카이브하여 다른 가격 티어로 이동시킬 수 있습니다.  

However, if you want to restore an archived snapshot, you will have to wait 24 to 72 hours.  
단, 아카이브된 스냅샷을 복원하려면 24~72시간이 소요됩니다.  

---

## Deleting and Recovering Snapshots  
## 스냅샷 삭제 및 복원  

Let's proceed to delete the snapshot.  
이제 스냅샷을 삭제해봅니다.  

After deletion, the snapshot is gone from the Snapshots list.  
삭제 후 스냅샷 목록에서 해당 스냅샷이 사라집니다.  

Previously, deleting snapshots was permanent, and you could not recover them.  
기존에는 스냅샷 삭제가 영구적이어서 복구할 수 없었습니다.  

However, thanks to the Recycle Bin, if you refresh your Resources, you can now see that your snapshot has appeared there.  
하지만 휴지통 덕분에 Resources를 새로고침하면 스냅샷이 휴지통에 나타납니다.  

You can click on it and recover it by selecting Recover Resources.  
스냅샷을 선택하고 Recover Resources를 클릭하면 복원됩니다.  

The snapshot will then be back in your Snapshots on the EC2 console.  
복원 후 스냅샷은 EC2 콘솔의 Snapshots 목록으로 돌아옵니다.  

---

## Conclusion  
## 결론  

That was an overview of EBS snapshots, including creating, copying, restoring, and protecting snapshots using the Recycle Bin.  
이번 강의에서는 스냅샷 생성, 복사, 복원, 휴지통을 통한 보호까지 EBS 스냅샷 개요를 다뤘습니다.  

I hope you found this useful, and I will see you in the next lecture.  
도움이 되었길 바라며, 다음 강의에서 만나요.  

---

## Key Takeaways  
## 핵심 요약  

- Created and managed EBS snapshots to back up volumes.  
- 볼륨 백업을 위해 EBS 스냅샷을 생성하고 관리했습니다.  

- Demonstrated copying snapshots across AWS regions for disaster recovery.  
- 재해 복구를 위해 리전 간 스냅샷 복사를 실습했습니다.  

- Restored volumes from snapshots in different Availability Zones.  
- 스냅샷을 이용해 다른 가용 영역(AZ)에서 볼륨을 복원했습니다.  

- Utilized the Recycle Bin feature to protect snapshots from accidental deletion.  
- 휴지통 기능을 활용해 스냅샷의 실수 삭제를 방지했습니다.  
