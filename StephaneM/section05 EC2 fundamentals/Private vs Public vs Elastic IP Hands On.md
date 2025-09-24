# Private vs Public vs Elastic IP Hands On  
# 프라이빗 vs 퍼블릭 vs 엘라스틱 IP 실습  
→ AWS 환경에서 IP 동작 방식을 실습으로 확인.

---

## Understanding IP Address Behavior in AWS  
## AWS에서 IP 주소 동작 이해  
→ 퍼블릭과 프라이빗 IP 사용법 차이 설명.

Let's examine the behavior of IP addresses in AWS environments.  
AWS 환경에서 IP 주소의 동작을 살펴봅시다.  
→ 퍼블릭/프라이빗 IP가 어떻게 작동하는지 테스트.

We have a public IPv4 address assigned to our instance.  
우리 인스턴스에는 퍼블릭 IPv4 주소가 할당되어 있습니다.  
→ 외부 접속용 주소.

This public IPv4 address is used to SSH into the machine and works effectively.  
이 퍼블릭 IPv4 주소를 사용하여 SSH로 접속할 수 있으며 정상적으로 동작합니다.  
→ 인터넷에서 접근 가능.

Once logged in, you will notice a private IP attached as the hostname of the instance.  
로그인 후 인스턴스의 호스트네임으로 프라이빗 IP가 붙어 있는 것을 볼 수 있습니다.  
→ 내부 식별용 주소도 있음.

While connected, you can use the private IP address internally.  
연결된 상태에서는 내부적으로 프라이빗 IP를 사용할 수 있습니다.  
→ 동일 네트워크 내부에서 통신 가능.

However, if you disconnect and attempt to SSH using the private IPv4 address, it will not work.  
하지만 연결을 끊고 프라이빗 IPv4 주소로 SSH 접속을 시도하면 동작하지 않습니다.  
→ 외부에서는 접근 불가.

The reason is that private IPv4 addresses belong to a private network.  
그 이유는 프라이빗 IPv4 주소가 사설 네트워크에 속하기 때문입니다.  
→ 내부망 전용.

Since you are not connected to AWS's private network externally, you cannot access the instance using the private IP.  
외부에서 AWS의 프라이빗 네트워크에 연결되지 않았기 때문에 프라이빗 IP로 인스턴스에 접근할 수 없습니다.  
→ VPN 없이는 불가능.

You can only connect to AWS via the internet, which requires using the public IP address.  
AWS에 접근하려면 인터넷을 통해야 하며, 이때 퍼블릭 IP 주소가 필요합니다.  
→ 외부 접속 필수 조건.

---

## Observing IP Address Changes on Instance Stop and Start  
## 인스턴스 중지 및 시작 시 IP 주소 변화 관찰  
→ 퍼블릭 IP 변경 여부 확인.

Let's observe the behavior of the instance's IP addresses when stopping and starting the instance.  
인스턴스를 중지하고 시작할 때 IP 주소의 동작을 살펴봅시다.  
→ Stop/Start 시 변화 실험.

First, we stop the instance and save the current public IPv4 address for reference.  
먼저 인스턴스를 중지하고 현재 퍼블릭 IPv4 주소를 기록해 둡니다.  
→ 비교용 저장.

After stopping the instance, we start it again.  
인스턴스를 중지한 후 다시 시작합니다.  
→ 새롭게 시작.

Note that stopping and starting is different from rebooting.  
중지 후 시작은 재부팅과 다릅니다.  
→ 중요한 차이점.

Stopping and starting the instance causes the public IPv4 address to change, whereas rebooting does not.  
인스턴스를 중지 후 시작하면 퍼블릭 IPv4 주소가 바뀌지만, 재부팅은 그렇지 않습니다.  
→ Stop/Start 시만 IP 변경.

Once the instance is running again, you will notice it has a new public IPv4 address.  
인스턴스가 다시 실행되면 새로운 퍼블릭 IPv4 주소를 얻게 됩니다.  
→ 새 IP 확인.

Using the old public IP to SSH will fail, but using the new public IP will succeed.  
이전 퍼블릭 IP로 SSH 접속은 실패하지만 새 퍼블릭 IP로는 성공합니다.  
→ 이전 IP는 더 이상 유효하지 않음.

The private IP address remains unchanged throughout this process.  
프라이빗 IP 주소는 이 과정 내내 변하지 않습니다.  
→ 내부 주소는 고정됨.

---

## Using Elastic IPs to Maintain a Persistent Public IP  
## 퍼블릭 IP를 고정하기 위한 엘라스틱 IP 사용  
→ 퍼블릭 IP 변경 문제 해결 방법.

To prevent the public IPv4 address from changing when stopping and starting an instance, you can use an Elastic IP.  
인스턴스 중지/시작 시 퍼블릭 IPv4 주소가 변경되지 않도록 하려면 엘라스틱 IP를 사용할 수 있습니다.  
→ 고정 IP 필요 시.

Currently, there are no Elastic IP addresses allocated in this account.  
현재 이 계정에는 할당된 엘라스틱 IP가 없습니다.  
→ 새로 할당해야 함.

Elastic IPs are allocated from Amazon's pool of IPv4 addresses.  
엘라스틱 IP는 아마존의 IPv4 주소 풀에서 할당됩니다.  
→ AWS 제공 자원.

When allocated, you effectively rent an IPv4 address that you own for the duration of the allocation.  
할당 시 해당 IPv4 주소를 임대하여 소유한 것처럼 사용할 수 있습니다.  
→ 임시 소유 개념.

This Elastic IP can be associated with a specific EC2 instance and remains attached as long as you keep it associated.  
엘라스틱 IP는 특정 EC2 인스턴스에 연결할 수 있으며 연결을 유지하는 동안 그대로 붙어 있습니다.  
→ 고정 유지 가능.

---

## Pricing Note  
## 요금 참고  
→ 비용 관련 주의사항.

AWS charges approximately 0.005 per hour for public IPv4 addresses, including Elastic IPs, whether they are used or not.  
AWS는 퍼블릭 IPv4 주소(엘라스틱 IP 포함)에 대해 사용 여부와 관계없이 시간당 약 0.005달러를 청구합니다.  
→ 고정 비용 발생.

This amounts to about 3.50 per month.  
이는 한 달에 약 3.50달러에 해당합니다.  
→ 적지만 꾸준히 나가는 비용.

To avoid unnecessary charges, you should terminate instances and release Elastic IPs when they are no longer needed.  
불필요한 요금을 피하려면 필요하지 않을 때 인스턴스를 종료하고 엘라스틱 IP를 해제해야 합니다.  
→ 비용 최적화 팁.

---

## Allocating and Associating an Elastic IP  
## 엘라스틱 IP 할당 및 연결  
→ 실제 사용 방법.

To allocate an Elastic IP, navigate to the Elastic IPs section and allocate a new address from Amazon's pool.  
엘라스틱 IP를 할당하려면 Elastic IPs 섹션에서 아마존 풀에서 새 주소를 할당합니다.  
→ 콘솔에서 할당 가능.

Once allocated, you can associate the Elastic IP with a running EC2 instance by specifying the instance and the private IP address to associate it with.  
할당 후 실행 중인 EC2 인스턴스와 연결할 수 있으며, 이때 인스턴스와 연결할 프라이빗 IP를 지정합니다.  
→ 연결 절차 필요.

After associating the Elastic IP, the instance's public IPv4 address will match the Elastic IP address.  
엘라스틱 IP를 연결하면 인스턴스의 퍼블릭 IPv4 주소는 엘라스틱 IP와 동일해집니다.  
→ 고정 퍼블릭 IP 확보.

This association persists even if the instance is stopped and started again.  
이 연결은 인스턴스를 중지 후 시작하더라도 유지됩니다.  
→ 고정 효과 확인.

You can verify this by refreshing the EC2 instance details.  
EC2 인스턴스 세부정보를 새로고침하여 확인할 수 있습니다.  
→ 콘솔에서 즉시 확인 가능.

The public IPv4 address will now be the Elastic IP address.  
퍼블릭 IPv4 주소는 이제 엘라스틱 IP 주소가 됩니다.  
→ 기존 동적 IP가 대체됨.

Additionally, the Elastic IP address field will show the associated Elastic IP.  
추가로, 엘라스틱 IP 주소 필드에 연결된 IP가 표시됩니다.  
→ UI 상에서도 확인 가능.

---

## Testing SSH Access with Elastic IP  
## 엘라스틱 IP로 SSH 접속 테스트  
→ 실제 접속 동작 확인.

Using the Elastic IP address, you can SSH into the instance successfully.  
엘라스틱 IP 주소를 사용하여 SSH 접속을 성공적으로 할 수 있습니다.  
→ 정상 동작 확인.

If you stop the instance, the Elastic IP remains attached, and the public IPv4 address does not change.  
인스턴스를 중지해도 엘라스틱 IP는 붙어 있으며 퍼블릭 IPv4 주소는 바뀌지 않습니다.  
→ 고정성 보장.

Starting the instance again maintains the same Elastic IP address.  
인스턴스를 다시 시작해도 동일한 엘라스틱 IP가 유지됩니다.  
→ 안정성 확보.

---

## Disassociating and Releasing Elastic IPs  
## 엘라스틱 IP 연결 해제 및 해제  
→ 정리 과정.

To remove the Elastic IP from the instance, you can disassociate it.  
인스턴스에서 엘라스틱 IP를 제거하려면 연결 해제를 할 수 있습니다.  
→ 분리 가능.

After disassociation, release the Elastic IP to avoid incurring charges.  
연결 해제 후에는 요금 발생을 막기 위해 엘라스틱 IP를 해제해야 합니다.  
→ 비용 절감.

Once released, the instance will receive a new public IPv4 address upon refresh.  
해제 후 인스턴스는 새 퍼블릭 IPv4 주소를 받게 됩니다.  
→ 다시 동적 할당.

Finally, you can terminate the instance to complete the cleanup process and avoid further charges.  
마지막으로 인스턴스를 종료하여 정리 작업을 완료하고 추가 요금을 피할 수 있습니다.  
→ 청구 방지.

---

## Key Takeaways  
## 핵심 요약  
→ 중요한 포인트 정리.

- Public IPv4 addresses allow SSH access from the internet, while private IPv4 addresses only work within the AWS private network.  
- 퍼블릭 IPv4 주소는 인터넷에서 SSH 접속을 허용하지만, 프라이빗 IPv4 주소는 AWS 내부 네트워크에서만 작동합니다.  
→ 퍼블릭: 외부, 프라이빗: 내부.

- Stopping and starting an EC2 instance changes its public IPv4 address, but the private IPv4 address remains the same.  
- EC2 인스턴스를 중지 후 시작하면 퍼블릭 IPv4 주소는 바뀌지만, 프라이빗 IPv4 주소는 그대로 유지됩니다.  
→ 퍼블릭만 변경.

- Elastic IP addresses provide a persistent public IPv4 address that remains attached to an instance even after stopping and starting it.  
- 엘라스틱 IP는 인스턴스를 중지/시작해도 유지되는 고정 퍼블릭 IPv4 주소를 제공합니다.  
→ 고정성 보장.

- AWS charges hourly for public and elastic IP addresses; unused resources should be terminated or released to avoid unnecessary costs.  
- AWS는 퍼블릭 및 엘라스틱 IP 주소에 대해 시간당 요금을 부과하므로, 사용하지 않는 자원은 종료하거나 해제해야 합니다.  
→ 불필요한 과금 방지.
