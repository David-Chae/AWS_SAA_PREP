# S3 Versioning - Hands On  
# S3 버전 관리 실습  

---

## Introduction to S3 Versioning  
## S3 버전 관리 소개  

Let's explore how to use S3 versioning.  
S3 버전 관리 기능을 어떻게 사용하는지 알아봅시다.  
👉 설명: 버전 관리를 통해 파일 업데이트와 삭제를 안전하게 관리 가능.  

First, navigate to the bucket's properties where you will find the bucket versioning setting.  
먼저 버킷의 속성으로 이동하여 버전 관리 설정을 찾습니다.  
👉 설명: 버전 관리 활성화는 버킷 단위에서 이루어짐.  

We will edit this setting to enable versioning.  
이 설정을 편집하여 버전 관리를 활성화합니다.  
👉 설명: 기존 파일을 덮어쓰지 않고 새 버전을 생성하도록 설정.  

Enabling bucket versioning ensures that any files we override will add new versions into our bucket rather than replacing the existing ones.  
버전 관리를 활성화하면, 파일을 덮어쓸 때 기존 파일을 대체하지 않고 새 버전이 생성됩니다.  
👉 설명: 데이터 안전성을 확보하고 이전 상태 복원이 가능.  

---

## Updating Website Content with Versioning  
## 버전 관리로 웹사이트 콘텐츠 업데이트  

Next, let's update our website content.  
다음으로 웹사이트 콘텐츠를 업데이트해보겠습니다.  

Locate the website URL and note the current content, which says "I love coffee."  
웹사이트 URL을 확인하고 현재 콘텐츠인 "I love coffee."를 기록합니다.  
👉 설명: 현재 상태 확인 후 업데이트 준비.  

We want to change this to "I really love coffee."  
이를 "I really love coffee."로 변경하고자 합니다.  

To do this, edit the file accordingly and save it.  
파일을 수정하고 저장합니다.  
👉 설명: 기존 파일 덮어쓰기 없이 새 버전 생성 가능.  

After saving, upload the updated file again as index.html.  
저장 후, 업데이트된 파일을 다시 index.html로 업로드합니다.  
👉 설명: 동일 키에 업로드 시 새 버전 생성.  

This upload will overwrite the previous content but, due to versioning, it will create a new version rather than deleting the old one.  
이 업로드는 이전 콘텐츠를 덮어쓰지만, 버전 관리 덕분에 새 버전이 생성되고 기존 버전은 삭제되지 않습니다.  
👉 설명: 파일 변경 이력 유지.  

---

## Verifying the Updated Content  
## 업데이트된 콘텐츠 확인  

After uploading, the update is successful.  
업로드 후 업데이트가 성공적으로 적용되었습니다.  

Refreshing the webpage now displays "I REALLY love coffee."  
웹페이지를 새로고침하면 "I REALLY love coffee."가 표시됩니다.  

Let's examine what happened behind the scenes.  
이제 백그라운드에서 무슨 일이 일어났는지 살펴봅시다.  

By toggling "Show versions" in the S3 console, we can see the version IDs associated with each file.  
S3 콘솔에서 "Show versions"를 켜면 각 파일에 연결된 버전 ID를 확인할 수 있습니다.  

Files uploaded before enabling versioning, such as beach.jpg and coffee.jpg, have a null version ID.  
버전 관리 활성화 이전에 업로드된 파일, 예를 들어 beach.jpg와 coffee.jpg는 null 버전 ID를 가집니다.  

The index.html file, however, now has two versions: one with a null version ID from before versioning was enabled, and a new one with a unique version ID created after the update.  
그러나 index.html 파일은 이제 두 가지 버전을 갖습니다: 버전 활성화 이전의 null 버전과 업데이트 후 생성된 고유 버전 ID.  
👉 설명: 기존 콘텐츠 유지 + 새 버전 생성 확인.  

---

## Rolling Back to a Previous Version  
## 이전 버전으로 롤백  

Thanks to versioning, we can roll back to a previous version of our page.  
버전 덕분에 이전 페이지 버전으로 롤백할 수 있습니다.  

For example, to revert from "I REALLY love coffee" back to "I love coffee," select the specific version ID you want to restore.  
예를 들어, "I REALLY love coffee"를 "I love coffee"로 되돌리려면 복원할 버전 ID를 선택합니다.  

Ensure "Show versions" is enabled, then delete the newer version.  
"Show versions"가 켜져 있는지 확인한 후, 새 버전을 삭제합니다.  

This deletion is a permanent, destructive operation and cannot be undone.  
이 삭제는 영구적이며 되돌릴 수 없습니다.  

You must confirm by typing "permanently delete" before proceeding.  
진행하기 전에 "permanently delete"를 입력하여 확인해야 합니다.  

After deletion, refreshing the webpage will display the original content "I love coffee."  
삭제 후 웹페이지를 새로고침하면 원래 콘텐츠인 "I love coffee."가 표시됩니다.  

---

## Deleting Objects with Versioning Disabled  
## 버전 관리 비활성 시 객체 삭제  

If you disable "Show versions" and delete an object, such as coffee.jpg, the underlying version is not deleted.  
"Show versions"를 끄고 coffee.jpg 같은 객체를 삭제해도 실제 버전은 삭제되지 않습니다.  

Instead, a delete marker is added.  
대신 삭제 마커가 추가됩니다.  

This marker hides the object without removing its versions.  
이 마커는 객체를 숨기지만 버전은 삭제하지 않습니다.  

When deleting this way, you simply confirm the deletion without typing "permanently delete."  
이 방식으로 삭제할 때는 "permanently delete"를 입력할 필요 없이 삭제를 확인하면 됩니다.  

The object appears deleted in the bucket, but the versions still exist.  
버킷에서는 객체가 삭제된 것처럼 보이지만, 실제 버전은 남아 있습니다.  

---

## Understanding Delete Markers  
## 삭제 마커 이해  

With versioning enabled, deleting an object adds a delete marker with its own version ID.  
버전 관리가 활성화된 경우 객체를 삭제하면 고유 버전 ID가 있는 삭제 마커가 추가됩니다.  

The actual previous versions remain in the bucket but are hidden by this marker.  
실제 이전 버전은 버킷에 남아있지만 마커에 의해 숨겨집니다.  

For example, after deleting coffee.jpg, the delete marker hides the image.  
예를 들어 coffee.jpg를 삭제하면 삭제 마커가 이미지를 숨깁니다.  

Refreshing the webpage results in a "404 Not Found" error because the image is not accessible while the delete marker exists.  
웹페이지를 새로고침하면 삭제 마커가 존재하기 때문에 "404 Not Found" 오류가 나타납니다.  

---

## Restoring Deleted Objects  
## 삭제된 객체 복원  

To restore a deleted object, locate and delete the delete marker itself.  
삭제된 객체를 복원하려면 삭제 마커 자체를 찾아 삭제합니다.  

This is a permanent deletion of the marker, which reveals the previous version of the object.  
이 작업은 마커를 영구적으로 삭제하며, 이전 버전을 다시 보여줍니다.  

After removing the delete marker, refreshing the webpage will display the restored image again.  
삭제 마커를 제거하면 웹페이지를 새로고침했을 때 이미지가 복원되어 표시됩니다.  

This demonstrates how versioning allows recovery from accidental deletions.  
이는 버전 관리가 실수로 삭제한 경우에도 복구할 수 있음을 보여줍니다.  

---

## Conclusion  
## 결론  

You can experiment with S3 versioning by adding multiple file versions, deleting specific versions, and observing the effects.  
S3 버전 관리로 여러 파일 버전을 추가하고, 특정 버전을 삭제하며 효과를 실험할 수 있습니다.  

Versioning provides a powerful way to manage object histories and recover from unintended changes or deletions.  
버전 관리는 객체 이력을 관리하고 의도치 않은 변경이나 삭제로부터 복구할 수 있는 강력한 방법입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Enabled S3 bucket versioning to maintain multiple versions of objects.  
- 객체의 여러 버전을 유지하기 위해 S3 버킷 버전 관리 활성화.  

- Updated files create new version IDs while preserving previous versions.  
- 파일 업데이트 시 새 버전 ID가 생성되고 이전 버전은 유지됨.  

- Deleting an object without specifying a version adds a delete marker, hiding the object without removing its versions.  
- 버전을 지정하지 않고 객체를 삭제하면 삭제 마커가 추가되어 객체를 숨기지만 버전은 삭제되지 않음.  

- Removing the delete marker restores access to the previous version of the object.  
- 삭제 마커를 제거하면 이전 버전에 다시 접근 가능.  

---

🎮 **게임보상:**

* **“S3 버전 관리 실습 완료!”**

  * 버전 업로드 및 롤백 이해 +25
  * 삭제 마커 개념 숙지 +25
  * 객체 복원 실습 +25
  * 웹페이지 업데이트 확인 +25

총 **100 XP 획득!** 🎉
