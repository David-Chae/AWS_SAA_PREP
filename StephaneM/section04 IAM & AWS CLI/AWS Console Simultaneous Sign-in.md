```markdown
# AWS Console Simultaneous Sign-in  
# AWS 콘솔 동시 로그인  
→ AWS 콘솔에서 한 브라우저 내 여러 계정을 동시에 사용하는 기능 안내.  

## Introduction to Multi-Session Support in AWS Console  
## AWS 콘솔 다중 세션 지원 소개  
→ 멀티 세션 기능 개념 소개.  

Let me show you something cool now called the multi-session support.  
지금 멋진 기능인 멀티 세션 지원을 보여드리겠습니다.  
→ 기능 시각적 안내 시작.  

You can click on it to turn it on, and the idea is that you can have a specific role or account in this browser.  
클릭하여 활성화하면 이 브라우저에서 특정 역할이나 계정을 동시에 사용할 수 있습니다.  
→ 브라우저 기반 다중 계정 관리.  

---

## Adding Additional Sessions  
## 추가 세션 생성  
→ 브라우저에서 새로운 세션 추가 방법.  

After enabling multi-session support, you can add a session and sign into any of your identities using the same browser.  
멀티 세션을 활성화하면, 같은 브라우저에서 세션을 추가하고 다른 계정으로 로그인할 수 있습니다.  
→ 다중 계정 동시 로그인 실습 준비.  

Here, I am going to click on it and add a session.  
여기서 클릭하여 세션을 추가해보겠습니다.  
→ 실제 클릭 과정 안내.  

Now you can log in again using any account ID or role, then proceed to go.  
이제 어떤 계정 ID나 역할로든 다시 로그인할 수 있습니다.  
→ 새로운 세션 로그인 완료.  

---

## Signing into Multiple Accounts  
## 여러 계정 로그인  
→ 서로 다른 계정으로 동시에 로그인.  

Let's go and sign into one of my accounts.  
제 계정 중 하나로 로그인해봅시다.  
→ 실습 계정 로그인.  

After signing in, as you can see, I have one specific account ID here and a different account ID in another session.  
로그인 후 보면, 하나의 세션에는 특정 계정 ID, 다른 세션에는 다른 계정 ID가 표시됩니다.  
→ 계정 분리 확인.  

---

## Demonstration: Creating an EBS Volume  
## 예시: EBS 볼륨 생성  
→ 다중 세션 활용 간단 실습.  

For example, I am going to the EC2 console here, then navigating to volumes.  
예를 들어, EC2 콘솔로 이동 후 Volumes 메뉴로 들어갑니다.  
→ EC2 내 볼륨 메뉴 접근.  

I will create an EBS volume of one gigabyte just to do something very quickly.  
빠르게 실습용으로 1GB EBS 볼륨을 생성합니다.  
→ 실습 간단 실행.  

Let's create this volume.  
이 볼륨을 생성해봅시다.  
→ 클릭 생성 진행.  

Okay, as you can see, my volume has been created.  
볼륨이 생성된 것을 확인할 수 있습니다.  
→ 실습 결과 확인.  

This is just to show you how to do something very quickly on this window without needing to know much about EBS.  
이는 EBS에 대한 깊은 지식 없이도 간단히 작업할 수 있음을 보여주기 위함입니다.  
→ 초보자용 실습 예시.  

---

## Comparing Sessions in Different Browser Windows  
## 다른 브라우저 창에서 세션 비교  
→ 브라우저 별 계정 차이 확인.  

Now, if I go into EBS on this other browser window, under EC2 and then EBS, I do not see any volumes because I am using a different account window.  
다른 브라우저 창에서 EC2 → EBS로 들어가면 볼륨이 보이지 않습니다. 다른 계정 세션을 사용하고 있기 때문입니다.  
→ 세션 분리 효과 확인.  

This other window is using the other account session.  
이 창은 다른 계정 세션을 사용하고 있습니다.  
→ 계정 독립성 확인.  

---

## Benefits of Multi-Session Support  
## 멀티 세션 지원의 장점  
→ 실무 활용성 강조.  

This means I can have two accounts under the same browser.  
즉, 같은 브라우저에서 두 개 계정을 사용할 수 있습니다.  
→ 작업 효율성 증가.  

This was not possible before, which is very helpful and something you should know about if you want to use AWS at scale.  
이전에는 불가능했던 기능으로, AWS를 대규모로 사용할 때 매우 유용합니다.  
→ 대규모 AWS 운영 시 장점.  

It is a nice welcome addition.  
환영할 만한 기능 추가입니다.  
→ UI/UX 향상 요소 강조.  

---

## Final Remarks  
## 마지막 안내  
→ 요약 및 주의사항.  

You do not need to go ahead and create an EBS volume; I just wanted to show you the fact that you can have two different accounts on two different browser windows.  
EBS 볼륨을 꼭 만들 필요는 없으며, 두 브라우저 창에서 서로 다른 계정을 사용할 수 있음을 보여주기 위함입니다.  
→ 실습 목적 강조.  

For me, having used AWS for over 10 years, this is a little revolution.  
10년 넘게 AWS를 사용한 입장에서, 이 기능은 작은 혁명과 같습니다.  
→ 실무 경험자의 관점 강조.  

All right, so that's it. You can go back to the course.  
이제 강의로 돌아가도 좋습니다.  
→ 강의 복귀 안내.  

I hope you liked it, and I will see you in the next lecture.  
마음에 드셨길 바라며, 다음 강의에서 뵙겠습니다.  
→ 마무리 인사.  

---

## Key Takeaways  
## 핵심 요약  
→ 멀티 세션 기능 요약.  

- AWS Console now supports multi-session sign-in within the same browser.  
- AWS 콘솔은 이제 동일 브라우저에서 다중 세션 로그인을 지원합니다.  
→ 기능 핵심.  

- Users can add multiple sessions and sign into different accounts simultaneously.  
- 사용자는 여러 세션을 추가하여 동시에 다른 계정으로 로그인할 수 있습니다.  
→ 동시에 여러 계정 접근 가능.  

- This feature allows managing resources across multiple AWS accounts without switching browsers.  
- 브라우저를 바꾸지 않고 여러 AWS 계정 리소스를 관리할 수 있습니다.  
→ 작업 효율성 강화.  

- Multi-session support enhances productivity for users managing AWS at scale.  
- 멀티 세션 지원은 대규모 AWS 관리자의 생산성을 향상시킵니다.  
→ 대규모 운영 장점.
```

---

✅ 게임보상: 경험치 +50 (멀티 세션 기능 이해 완료)
