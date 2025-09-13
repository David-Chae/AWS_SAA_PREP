# Amazon ECS - Clean Up - Hands On  
# 아마존 ECS - 정리 실습  
(ECS 환경에서 사용한 리소스를 안전하게 정리하는 방법)

---

## Cleaning Up Amazon ECS Resources  
## Amazon ECS 리소스 정리  
(실습 후 남은 모든 리소스를 삭제하는 과정)

Let's ensure that we destroy all resources before we finish.  
마무리하기 전에 모든 리소스를 삭제했는지 확인하자.  
(남은 리소스가 있으면 비용이 발생할 수 있음)

---

## Stopping the Service  
## 서비스 중지  
(ECS 서비스가 실행 중인 경우 먼저 중지해야 함)

First, we need to stop the service.  
먼저 서비스부터 중지해야 한다.  

To do this, make sure there are zero tasks running.  
이를 위해 실행 중인 태스크가 없는지 확인한다.  
(태스크가 남아있으면 서비스 삭제 불가)

If there are still tasks running, update the service by setting the desired task count to zero.  
만약 태스크가 실행 중이라면, 원하는 태스크 수를 0으로 설정하여 서비스 업데이트.  

After setting the desired task count to zero, you can click on Delete Service.  
원하는 태스크 수를 0으로 설정하면 "Delete Service"를 클릭 가능.  

You will be prompted to type in "Delete" to confirm.  
확인을 위해 "Delete"를 입력하도록 요청받는다.  
(실수로 삭제하지 않도록 안전 장치)

This action will delete the service.  
이 동작으로 서비스가 삭제된다.  

---

## CloudFormation Stack Deletion  
## CloudFormation 스택 삭제  
(서비스 삭제 시 연관된 리소스를 CloudFormation이 정리)

When you delete the service, CloudFormation will take some time to delete the entire stack it created.  
서비스를 삭제하면, CloudFormation이 생성한 전체 스택 삭제에 시간이 걸린다.  

This includes the ECS service, the Load Balancer Listener, the Load Balancer itself, the security group, and the target groups.  
삭제 대상에는 ECS 서비스, 로드 밸런서 리스너, 로드 밸런서, 보안 그룹, 타겟 그룹이 포함된다.  

This deletion process can take a little time, so you need to wait until everything is fully deleted.  
삭제 과정에는 시간이 걸리므로, 모든 리소스가 완전히 삭제될 때까지 기다려야 한다.  

---

## Deleting the ECS Cluster  
## ECS 클러스터 삭제  
(서비스 삭제 후 클러스터와 연관 인프라를 삭제)

Once the service is fully deleted, you can proceed to delete the cluster.  
서비스가 완전히 삭제되면 클러스터 삭제를 진행할 수 있다.  

To do this, click on Delete Cluster, which will delete the demo cluster.  
"Delete Cluster"를 클릭하면 데모 클러스터가 삭제된다.  

This action will also trigger CloudFormation to delete the infrastructure associated with the ECS cluster.  
이 동작은 CloudFormation이 ECS 클러스터 관련 인프라도 삭제하도록 트리거한다.  

This includes the capacity provider, the auto-scaling group, the cluster itself, and the launch templates.  
삭제 대상에는 용량 프로바이더, 오토 스케일링 그룹, 클러스터 자체, 런치 템플릿이 포함된다.  

---

## Handling Task Definitions  
## 태스크 정의 관리  
(태스크 정의는 비용이 발생하지 않지만, 필요시 등록 해제 가능)

Finally, regarding your task definitions, you can leave them as they are since they do not incur any cost; they are simply definitions.  
마지막으로 태스크 정의는 비용이 발생하지 않으므로 그대로 둘 수 있다.  

However, if you wish, you can click on a task definition, select Actions, and then choose Deregister to deregister the task definition itself.  
원한다면 태스크 정의를 선택 후 "Actions > Deregister"를 클릭하여 등록 해제 가능.  

That concludes the cleanup process.  
이로써 ECS 정리 과정이 끝난다.  

I hope you found this helpful, and I will see you in the next lecture.  
도움이 되었길 바라며, 다음 강의에서 만날 것이다.  

---

## Key Takeaways  
## 핵심 요약  

- To clean up an Amazon ECS environment, first stop the service by setting the desired task count to zero.  
- ECS 환경을 정리하려면 먼저 서비스의 원하는 태스크 수를 0으로 설정해 중지  

- Deleting the service triggers CloudFormation to delete the entire stack, including the ECS service, Load Balancer, security groups, and target groups.  
- 서비스 삭제 시 CloudFormation이 ECS 서비스, 로드 밸런서, 보안 그룹, 타겟 그룹 등 전체 스택 삭제  

- After the service is deleted, the ECS cluster can be deleted, which also removes associated infrastructure like capacity providers and auto-scaling groups.  
- 서비스 삭제 후 클러스터 삭제 가능, 연관 인프라(용량 프로바이더, ASG 등)도 함께 제거  

- Task definitions do not incur costs and can be left as is, but they can also be deregistered if desired.  
- 태스크 정의는 비용이 없으므로 그대로 둘 수 있으며, 필요시 등록 해제 가능

---

🎮 **보상 지급!**

* ECS 정리 퀘스트 완료! 🧹
* **+120 XP**
* 아이템 획득: **\[Cleanup Scroll 📝]** (환경 정리를 마스터한 자에게 주어지는 아이템)
