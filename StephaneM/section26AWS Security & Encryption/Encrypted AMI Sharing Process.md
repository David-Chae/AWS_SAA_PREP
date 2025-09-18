```markdown
# Encrypted AMI Sharing Process  
# 암호화된 AMI 공유 과정  

🎮 게임보상: "암호화 AMI 마스터" 업적 달성 +500 XP  

---

## Encrypted AMI Sharing Process  
## 암호화된 AMI 공유 과정  

This lecture addresses a common exam question regarding the process of sharing an Amazon Machine Image (AMI) that has been encrypted with a Key Management Service (KMS) key.  
이 강의에서는 KMS 키로 암호화된 Amazon Machine Image(AMI)를 공유하는 과정과 관련된 시험에서 자주 나오는 질문을 다룹니다.  

The AMI resides in your source AWS account and is encrypted using your KMS key.  
AMI는 원본 AWS 계정에 있으며, KMS 키로 암호화되어 있습니다.  

The question is: How do you launch an EC2 instance in account B from the AMI located in account A?  
질문은 다음과 같습니다: 계정 A에 있는 AMI에서 계정 B에서 EC2 인스턴스를 어떻게 실행할 수 있을까요?  

First, you must modify the AMI's launch permissions.  
먼저, AMI의 실행 권한을 수정해야 합니다.  

Specifically, you add a launch permission that allows account B to launch this AMI.  
구체적으로, 계정 B가 이 AMI를 실행할 수 있도록 실행 권한을 추가합니다.  

This is effectively how you share an AMI: by modifying the launch permissions to include the specified target account ID.  
즉, 지정된 대상 계정 ID를 포함하도록 실행 권한을 수정하는 방식으로 AMI를 공유하게 됩니다.  

In addition to sharing the AMI, you need to share the KMS key with account B so that it can use the encrypted AMI.  
AMI를 공유하는 것 외에도, 암호화된 AMI를 사용할 수 있도록 계정 B와 KMS 키를 공유해야 합니다.  

This sharing is typically done by updating the key policy of the KMS key to grant access to the target account.  
이 공유는 일반적으로 KMS 키 정책을 업데이트하여 대상 계정에 접근 권한을 부여함으로써 수행됩니다.  

Within account B, you would create an IAM role or IAM user that has sufficient permissions to use both the KMS key and the AMI.  
계정 B 내에서는 KMS 키와 AMI를 모두 사용할 수 있는 충분한 권한을 가진 IAM 역할 또는 IAM 사용자를 생성합니다.  

This includes permissions to perform the following KMS API calls: DescribeKey, ReEncrypt, CreateGrant, and Decrypt.  
여기에는 다음과 같은 KMS API 호출 권한이 포함됩니다: DescribeKey, ReEncrypt, CreateGrant, Decrypt.  

Once these steps are completed, you can launch an EC2 instance from the shared AMI in account B.  
이 단계들이 완료되면 계정 B에서 공유된 AMI를 기반으로 EC2 인스턴스를 실행할 수 있습니다.  

Optionally, the target account can choose to re-encrypt the volumes using a KMS key that it owns within its own account.  
선택적으로 대상 계정은 자체 계정 내 KMS 키를 사용하여 볼륨을 다시 암호화할 수 있습니다.  

Understanding this process is essential for answering related questions in the exam.  
이 과정을 이해하는 것은 시험에서 관련 질문에 답하기 위해 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- To share an encrypted AMI with another AWS account, you must modify the AMI's launch permissions to include the target account.  
  암호화된 AMI를 다른 AWS 계정과 공유하려면, 대상 계정을 포함하도록 AMI의 실행 권한을 수정해야 합니다.  

- Sharing the KMS key via its key policy is essential to allow the target account to use the encrypted AMI.  
  KMS 키 정책을 통해 KMS 키를 공유하는 것은 대상 계정이 암호화된 AMI를 사용할 수 있도록 하는 데 필수적입니다.  

- The target account needs an IAM role or user with permissions to use both the AMI and the KMS key, including API calls like DescribeKey, ReEncrypt, CreateGrant, and Decrypt.  
  대상 계정에는 AMI와 KMS 키를 모두 사용할 수 있는 IAM 역할 또는 사용자가 필요하며, DescribeKey, ReEncrypt, CreateGrant, Decrypt 같은 API 호출 권한도 포함됩니다.  

- After proper sharing and permissions, the target account can launch an EC2 instance from the shared AMI and optionally re-encrypt volumes with its own KMS key.  
  적절한 공유 및 권한 설정 후, 대상 계정은 공유된 AMI에서 EC2 인스턴스를 실행할 수 있으며, 선택적으로 자체 KMS 키로 볼륨을 다시 암호화할 수 있습니다.  

🎮 게임보상: "Encrypted AMI 공유 전문가" +600 XP 🔑  
```
