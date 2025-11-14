# S3 MFA Delete Hands On  
# S3 MFA Delete 실습  

---

## Demonstrating MFA Delete in S3  
## S3에서 MFA Delete 시연  

This demonstration covers how to enable and test MFA Delete on an S3 bucket.  
이 실습에서는 S3 버킷에서 MFA Delete를 활성화하고 테스트하는 방법을 다룹니다.  

---

## Creating the S3 Bucket and Enabling Versioning  
## S3 버킷 생성 및 버전 관리 활성화  

A new bucket named demo-stephane-MFA-delete-2020 is created in the eu-west-1 region. Bucket versioning is enabled during creation.  
eu-west-1 리전에 demo-stephane-MFA-delete-2020라는 새 버킷을 생성하고, 생성 시 버전 관리를 활성화합니다.  

---

## MFA Delete Setting in the Console  
## 콘솔에서 MFA Delete 설정  

When accessing the bucket properties and versioning settings, it is observed that Multi-Factor Authentication (MFA) Delete is currently disabled. The AWS Console UI does not allow enabling this setting. Therefore, enabling MFA Delete must be done using the AWS CLI.  
버킷 속성과 버전 관리 설정에 접근하면 MFA Delete가 현재 비활성화되어 있는 것을 확인할 수 있습니다. AWS 콘솔 UI에서는 이 설정을 활성화할 수 없으므로, MFA Delete는 AWS CLI를 통해 활성화해야 합니다.  

---

## Prerequisites: Setting Up MFA for the Root Account  
## 사전 준비: 루트 계정에 MFA 설정  

Before proceeding, ensure an MFA device is set up for the root account under IAM. The demonstration uses a virtual MFA device, and its ARN is noted for later use.  
진행하기 전에 IAM에서 루트 계정에 MFA 장치를 설정해야 합니다. 이 실습에서는 가상 MFA 장치를 사용하며, 나중에 사용할 ARN을 기록해둡니다.  

---

## Configuring AWS CLI with Root Account  
## 루트 계정으로 AWS CLI 구성  

It is necessary to configure the AWS CLI to use the root account. This is only recommended for enabling MFA Delete on the S3 bucket. New access keys are created and downloaded, but it is emphasized that root access keys and secret access keys should never be shared. The CLI is configured with these credentials and a profile named root-MFA-delete-demo.  
AWS CLI를 루트 계정으로 구성해야 합니다. 이는 S3 버킷에서 MFA Delete를 활성화할 때만 권장됩니다. 새 액세스 키를 생성하고 다운로드하지만, 루트 액세스 키와 시크릿 키는 절대 공유하지 않아야 합니다. 이 자격 증명을 사용해 root-MFA-delete-demo라는 프로필로 CLI를 구성합니다.  

---

## Verifying CLI Configuration  
## CLI 구성 확인  

A command is run to list S3 buckets using the newly created profile. The correct buckets are listed, confirming the profile is set up properly.  
새로 생성한 프로필을 사용하여 S3 버킷 목록을 조회하는 명령을 실행합니다. 올바른 버킷이 표시되어 프로필이 정상적으로 설정되었음을 확인합니다.  

---

## Enabling MFA Delete via CLI  
## CLI로 MFA Delete 활성화  

To enable MFA Delete, a specific AWS CLI command is used. The bucket name, versioning configuration, MFA Delete status, MFA device ARN, and a current MFA code are required.  
MFA Delete를 활성화하려면 특정 AWS CLI 명령을 사용합니다. 버킷 이름, 버전 관리 구성, MFA Delete 상태, MFA 장치 ARN, 현재 MFA 코드가 필요합니다.  

```bash
aws s3api put-bucket-versioning --bucket demo-stephane-MFA-delete-2020 --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn-of-mfa-device mfa-code" --profile root-MFA-delete-demo --region eu-west-1
````

After entering the correct MFA code, the command completes successfully, enabling MFA Delete on the bucket.
올바른 MFA 코드를 입력하면 명령이 성공적으로 완료되어 버킷에서 MFA Delete가 활성화됩니다.

---

## Verifying MFA Delete is Enabled

## MFA Delete 활성화 확인

By refreshing the bucket versioning page in the AWS Console, it is confirmed that both bucket versioning and MFA Delete are enabled.
AWS 콘솔에서 버킷 버전 관리 페이지를 새로 고침하여 버킷 버전 관리와 MFA Delete가 모두 활성화되었음을 확인합니다.

---

## Testing Object Upload and Deletion

## 객체 업로드 및 삭제 테스트

An object (such as a JPEG file) is uploaded to the bucket. Deleting the object adds a delete marker due to versioning being enabled.
JPEG 파일과 같은 객체를 버킷에 업로드합니다. 버전 관리가 활성화되어 있으므로 객체를 삭제하면 삭제 마커가 추가됩니다.

---

## Attempting Permanent Delete

## 영구 삭제 시도

When attempting to permanently delete a specific version of the object, an error occurs: deletion is not allowed because MFA Delete is enabled. To perform a permanent delete, the CLI must be used with MFA, or MFA Delete must be disabled.
특정 객체 버전을 영구 삭제하려고 하면 오류가 발생합니다. MFA Delete가 활성화되어 있기 때문에 삭제가 허용되지 않습니다. 영구 삭제를 수행하려면 CLI에서 MFA를 사용하거나 MFA Delete를 비활성화해야 합니다.

---

## Disabling MFA Delete

## MFA Delete 비활성화

To disable MFA Delete, the same CLI command is used, but with MFADelete=Disabled and a new MFA code.
MFA Delete를 비활성화하려면 동일한 CLI 명령을 사용하되, MFADelete=Disabled 및 새로운 MFA 코드를 입력합니다.

```bash
aws s3api put-bucket-versioning --bucket demo-stephane-MFA-delete-2020 --versioning-configuration Status=Enabled,MFADelete=Disabled --mfa "arn-of-mfa-device new-mfa-code" --profile root-MFA-delete-demo --region eu-west-1
```

After disabling MFA Delete, permanent deletion of objects is possible. This is confirmed by deleting the delete marker and checking the bucket properties, which now show MFA Delete as disabled.
MFA Delete를 비활성화하면 객체를 영구 삭제할 수 있습니다. 삭제 마커를 삭제하고 버킷 속성을 확인하여 MFA Delete가 비활성화된 것을 확인합니다.

---

## Security Reminder: Delete Root Access Keys

## 보안 주의: 루트 액세스 키 삭제

At the end of the process, it is strongly recommended to deactivate and delete the root access keys used for this operation to maintain security.
이 작업이 끝난 후에는 보안을 위해 사용한 루트 액세스 키를 비활성화하고 삭제할 것을 강력히 권장합니다.

---

## Key Takeaways

## 핵심 요약

* MFA Delete can only be enabled or disabled using the AWS CLI, not through the AWS Console UI.

* MFA Delete는 AWS 콘솔 UI가 아닌 AWS CLI를 통해서만 활성화 또는 비활성화할 수 있습니다.

* Setting up an MFA device for the root account is a prerequisite for enabling MFA Delete.

* MFA Delete를 활성화하려면 루트 계정에 MFA 장치를 설정해야 합니다.

* Root access keys should never be shared and must be deleted after use for security.

* 루트 액세스 키는 절대 공유해서는 안 되며, 사용 후 보안을 위해 삭제해야 합니다.

* MFA Delete adds an extra layer of protection by requiring MFA for permanent deletions or disabling versioning.

* MFA Delete는 객체의 영구 삭제나 버전 관리 비활성화 시 MFA를 요구함으로써 추가적인 보호 계층을 제공합니다.

🎮 **게임보상:**  
- S3 MFA Delete 실습 과정 이해 +10 XP  
- CLI 명령어를 통한 MFA Delete 활성화/비활성화 +5 XP  
- 객체 삭제와 보안 주의 사항 이해 +5 XP  
총 **20 XP 획득!** 🎉
