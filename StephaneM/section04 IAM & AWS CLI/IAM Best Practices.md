```markdown
# IAM Best Practices  
IAM 모범 사례  
→ AWS 사용 시 실수를 줄이기 위해 IAM 사용 가이드와 모범 사례를 정리합니다.  

---

## IAM Best Practices  
IAM 모범 사례  
→ IAM 관련 일반 지침과 권장 사항  

Here are some general guidelines on IAM and best practices to help you avoid mistakes when using AWS.  
AWS 사용 시 실수를 피할 수 있도록 IAM 관련 일반 지침과 모범 사례를 안내합니다.  
→ 전체적인 사용 규칙 이해  

Do not use the root account except when you set up your AWS account. By now, you should have two accounts: a root account and your own personal account.  
AWS 계정 설정 시를 제외하고 루트 계정은 사용하지 마세요. 현재 루트 계정과 개인 계정 두 개를 갖고 있어야 합니다.  
→ 루트 계정 최소 사용 원칙  

Remember, one AWS user corresponds to one physical user. If a friend wants to use AWS, do not give them your credentials. Instead, create another user for them.  
AWS 사용자 1명은 실제 사람 1명에 대응됩니다. 친구가 AWS를 사용하려 한다면, 내 자격 증명을 주지 말고 새 사용자를 생성하세요.  
→ 사용자별 계정 관리  

You can assign users to groups and assign permissions to groups to ensure that security is managed at the group level. Additionally, you should create a strong password policy.  
사용자를 그룹에 할당하고 그룹에 권한을 부여하면 그룹 단위로 보안을 관리할 수 있습니다. 또한 강력한 비밀번호 정책을 만들어야 합니다.  
→ 그룹 기반 권한 관리 + 비밀번호 정책  

Also, if possible, use and enforce multi-factor authentication (MFA) to guarantee that your account is safer from hackers.  
가능하다면 다중 인증(MFA)을 사용하고 강제하여 계정을 해커로부터 안전하게 보호하세요.  
→ MFA 사용 권장  

You should create and use roles whenever you are giving permissions to AWS services, including EC2 instances, which are virtual servers.  
AWS 서비스(예: EC2 인스턴스) 권한을 부여할 때는 역할(Role)을 생성하고 사용하세요.  
→ 서비스 권한은 IAM 역할로 관리  

If you use AWS programmatically or via the CLI or SDK, you must generate access keys. These access keys are like passwords and are very secret, so keep them for yourself.  
AWS를 프로그램 방식, CLI, SDK로 사용할 경우 액세스 키를 생성해야 합니다. 액세스 키는 비밀번호와 같으며 매우 비밀이므로 본인만 사용하세요.  
→ 액세스 키 비밀 유지  

To edit the permissions of your account, you can use the IAM credentials reports or the IAM Access Advisor feature.  
계정 권한을 수정하려면 IAM 자격 증명 보고서 또는 IAM Access Advisor 기능을 사용할 수 있습니다.  
→ 권한 점검 및 수정 방법  

Finally, never share your IAM users and access keys. This is very important for your account's security.  
마지막으로, IAM 사용자 및 액세스 키를 절대 공유하지 마세요. 이는 계정 보안에 매우 중요합니다.  
→ 절대 공유 금지  

This concludes the section on IAM. You now know everything about IAM best practices. See you in the next lecture.  
이로써 IAM 섹션을 마칩니다. 이제 IAM 모범 사례를 모두 알게 되었습니다. 다음 강의에서 뵙겠습니다.  
→ 섹션 마무리  

---

## Key Takeaways  
핵심 요약  
→ 기억해야 할 사항  

- Avoid using the root account except during initial AWS account setup.  
  초기 AWS 계정 설정 시를 제외하고 루트 계정을 사용하지 마세요.  
  → 루트 계정 최소 사용 원칙  

- Create individual IAM users for each physical user instead of sharing credentials.  
  각 실제 사용자마다 IAM 사용자를 생성하고 자격 증명을 공유하지 마세요.  
  → 사용자별 계정 생성  

- Manage security by assigning users to groups and applying permissions at the group level.  
  사용자를 그룹에 할당하고 그룹 단위로 권한을 적용하여 보안을 관리하세요.  
  → 그룹 기반 보안 관리  

- Enforce strong password policies and use multi-factor authentication (MFA) to enhance account security.  
  강력한 비밀번호 정책을 시행하고 MFA를 사용하여 계정 보안을 강화하세요.  
  → 비밀번호 + MFA  

- Use IAM roles when granting permissions to AWS services, including EC2 instances.  
  AWS 서비스 권한을 부여할 때 IAM 역할을 사용하세요.  
  → 서비스 권한 관리  

- Keep access keys confidential and never share IAM user credentials or access keys.  
  액세스 키를 비밀로 유지하고 IAM 사용자 자격 증명이나 액세스 키를 공유하지 마세요.  
  → 액세스 키 비밀 유지  

---

🎮 **게임 보상:**  
- IAM 모범 사례 학습 +30  
- 루트 계정 최소 사용 원칙 +10  
- MFA 사용 권장 +10  
- 역할(Role) 활용 권장 +15  
🏆 “IAM Guardian” 칭호 획득!
```
