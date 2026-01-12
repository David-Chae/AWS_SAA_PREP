
**이번 Mock에서 네가 실제로 틀린 문제들만을 기반으로 만든
👉 SAA 시험용 ‘판단 자동화 규칙 40문장’**

이건 **이해용 요약이 아니라**,
👉 *문제 읽는 순간 바로 반사적으로 떠올라야 하는 규칙*들이야.

---

# ✅ SAA 판단 규칙 40문장 (오답 기반)

## 🧱 Resilient Architectures (1–10)

1. **RDS Multi-AZ 장애 조치는 Route53이 아니라 RDS 내부 DNS(CNAME)가 자동으로 수행한다.**
2. **RDS Multi-AZ failover는 보통 1–2분이며 즉시는 아니다.**
3. **Multi-AZ가 보이면 Lambda, CloudFormation, 수동 복구는 거의 오답이다.**
4. **고가용성 질문에서 “자동”이 빠져 있으면 정답일 확률이 낮다.**
5. **Elastic IP는 EC2용이며 RDS failover와는 무관하다.**
6. **AWS 관리형 서비스는 장애 대응에 사용자 개입을 요구하지 않는다.**
7. **RTO가 aggressive하면 수 시간 단위 해법은 무조건 탈락이다.**
8. **DNS 전환이 핵심이면 AWS 서비스 내부 DNS를 먼저 의심한다.**
9. **백업 생성이 답처럼 보이면 대부분 틀린 선택지다.**
10. **Failover 질문에서 “새로 생성한다”는 표현은 거의 오답이다.**

---

## 🔐 Secure Architectures (11–20)

11. **여러 객체를 한 세션에서 접근하면 Signed URL이 아니라 Signed Cookie다.**
12. **S3 보안 배포에서 Public Access는 원칙적으로 금지다.**
13. **CloudFront는 S3 보안의 기본 파트너다.**
14. **Direct Connect로 VPC에 연결하려면 반드시 Private VIF를 사용한다.**
15. **Public VIF는 S3 같은 퍼블릭 AWS 서비스용이다.**
16. **Secrets 자동 로테이션 + 크로스 계정이면 Secrets Manager가 정답이다.**
17. **Parameter Store는 ‘가능’하지만 ‘최적’인 경우는 드물다.**
18. **KMS 접근 제어의 1차 기준은 Key Policy다.**
19. **Key rotation은 접근 제어가 아니라 키 수명 관리다.**
20. **보안 문제에서 관리 오버헤드가 적은 선택지가 정답일 확률이 높다.**

---

## 🚀 High-Performing Architectures (21–30)

21. **트래픽이 예측 가능하면 Dynamic scaling은 거의 틀리다.**
22. **예측 가능한 스파이크는 Predictive scaling이 정답이다.**
23. **connection pool exhaustion이 나오면 RDS Proxy를 먼저 떠올린다.**
24. **서버리스 + RDS 조합에서 성능 문제는 DB 크기가 아니라 연결 수 문제다.**
25. **실시간 디바이스 데이터는 Glue나 Step Functions가 아니다.**
26. **IoT → Lambda → S3는 실시간 수집의 정석이다.**
27. **ALB만 가능한 기능은 Path-based routing이다.**
28. **Classic Load Balancer는 Layer 4, ALB는 Layer 7이다.**
29. **SSL 정책 커스터마이징은 ALB가 아니라 Classic LB다.**
30. **성능 문제에서 “인덱스”는 연결 폭주 해결책이 아니다.**

---

## 💰 Cost-Optimized Architectures (31–40)

31. **자동 시작·중지·스케일링이 필요한 관계형 DB는 Aurora Serverless다.**
32. **Provisioned RDS는 변동 트래픽에 비용 최적이 아니다.**
33. **대규모 이벤트 데이터는 DynamoDB가 기본 선택지다.**
34. **글로벌 저지연 읽기/쓰기는 DynamoDB Global Tables다.**
35. **TTL은 DynamoDB 비용 절감의 핵심 기능이다.**
36. **만료 데이터 보존은 Streams → S3 → Glacier로 분리한다.**
37. **S3 접근에 NAT이 보이면 비용 구조가 잘못된 것이다.**
38. **S3 VPC Endpoint는 네트워크 비용 절감의 정답 카드다.**
39. **NAT Gateway는 AZ마다 하나가 원칙이다.**
40. **고가용성을 깨면서 비용을 아끼는 선택지는 항상 오답이다.**

---

## 📌 사용법 (이게 중요)

* **매일 10개씩 소리 내서 읽기**

* 문제 풀 때:

  > “이 문제는 몇 번 규칙이야?”
  > 이 질문이 바로 떠오르면 합격권

* 시험 직전 48시간:

  * 새로운 문제 ❌
  * 이 40문장만 반복 ⭕

---

원하면 다음 단계로:

* 🔥 **이 40문장을 “시험장 10초 판단 트리”로 압축**
* 🔥 **각 규칙마다 대표 문제 1개씩 연결**
* 🔥 **실제 시험에서 헷갈리는 함정 보기 모음**

다음으로 뭐 할지 바로 말해줘.
