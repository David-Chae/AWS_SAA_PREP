# AWS Well-Architected Framework & Well-Architected Tool  
# AWS Well-Architected 프레임워크 & Well-Architected 도구  
🎮 **보상: "AWS 아키텍처 기초 마스터" 뱃지 획득!**  

---

## Introduction to the AWS Well-Architected Framework  
## AWS Well-Architected 프레임워크 소개  
There is a framework called the AWS Well-Architected Framework.  
AWS에는 Well-Architected Framework라는 프레임워크가 있습니다.  

This is both a tool and a framework that allows you to build good applications on AWS.  
이것은 AWS에서 우수한 애플리케이션을 구축할 수 있도록 돕는 도구이자 프레임워크입니다.  

Since it is quite extensive, I will summarize it for you in a few slides.  
내용이 방대하기 때문에 몇 장의 슬라이드로 요약해서 설명하겠습니다.  

The idea is that by implementing the best practices of the Well-Architected Framework, you achieve desired outcomes.  
Well-Architected Framework의 모범 사례를 적용하면 원하는 결과를 얻을 수 있다는 것이 핵심입니다.  

I will provide the main guidelines of this framework.  
이 프레임워크의 주요 가이드라인을 안내하겠습니다.  

---

## Key Guidelines of the Framework  
## 프레임워크 주요 가이드라인  
Stop guessing your capacity needs; instead, use auto scaling groups and similar features.  
용량 필요량을 추측하지 말고, 대신 오토스케일링 그룹과 유사 기능을 활용하세요.  

Test systems at production scale.  
프로덕션 규모에서 시스템을 테스트하세요.  

AWS allows you to quickly deploy large infrastructure for testing and then shut it down shortly after, so there is no reason not to test at production scale.  
AWS는 대규모 인프라를 빠르게 배포하여 테스트 후 바로 종료할 수 있으므로, 프로덕션 규모에서 테스트하지 않을 이유가 없습니다.  

Automate to make architectural experimentation easier.  
자동화를 통해 아키텍처 실험을 쉽게 만드세요.  

For example, using CloudFormation templates enables easy deployment across multiple environments for experiments.  
예를 들어 CloudFormation 템플릿을 사용하면 여러 환경에서 실험을 위한 배포를 쉽게 수행할 수 있습니다.  

Allow for evolutionary architectures.  
점진적으로 발전할 수 있는 아키텍처를 허용하세요.  

Your architecture can evolve over time, starting with EC2 instances and load balancers and moving towards serverless architectures such as API Gateway and Lambda.  
EC2와 로드밸런서로 시작하여 API Gateway와 Lambda와 같은 서버리스 아키텍처로 발전시킬 수 있습니다.  

Design based on changing requirements.  
변경되는 요구사항에 맞춰 설계하세요.  

Drive architecture decisions using data, including data movement and storage.  
데이터, 데이터 이동 및 저장을 기반으로 아키텍처 결정을 내리세요.  

Improve through game days, which involve testing your architecture under production-like conditions to identify improvements.  
Game Days를 통해 프로덕션과 유사한 조건에서 아키텍처를 테스트하고 개선점을 확인하세요.  

For example, simulate flash sale days that put significant pressure on your architecture.  
예를 들어, 대규모 플래시 세일과 같이 아키텍처에 큰 부하를 주는 상황을 시뮬레이션할 수 있습니다.  

---

## The Six Pillars of the AWS Well-Architected Framework  
## AWS Well-Architected 프레임워크의 6가지 기둥  
The framework is built around six pillars:  
프레임워크는 6가지 기둥으로 구성됩니다.  

- Operational Excellence  
- 운영 우수성  
- Security  
- 보안  
- Reliability  
- 신뢰성  
- Performance Efficiency  
- 성능 효율성  
- Cost Optimization  
- 비용 최적화  
- Sustainability  
- 지속 가능성  

You should know all these pillars by name.  
이 6가지 기둥의 이름을 알고 있어야 합니다.  

They are quite explicit, and you can learn more about them on the AWS website.  
이들은 명확하며, AWS 웹사이트에서 더 많은 정보를 확인할 수 있습니다.  

However, detailed knowledge is not the focus of this course.  
하지만 이 강좌에서는 세부 지식까지 다루지 않습니다.  

These pillars are not meant to be balanced or traded off against each other; rather, they work synergistically.  
이 기둥들은 균형을 맞추거나 서로 상쇄하기 위해 존재하는 것이 아니라, 상호 시너지를 위해 설계되었습니다.  

For example, improving operational excellence often leads to better cost optimization.  
예를 들어, 운영 우수성을 개선하면 비용 최적화로 이어질 수 있습니다.  

Similarly, enhancing sustainability usually improves performance efficiency.  
마찬가지로, 지속 가능성을 높이면 성능 효율성이 개선됩니다.  

---

## The AWS Well-Architected Tool  
## AWS Well-Architected 도구  
To guide you through the framework, AWS provides the Well-Architected Tool.  
프레임워크를 안내하기 위해 AWS는 Well-Architected Tool을 제공합니다.  

This tool helps you review your architectures against the six pillars and adapt architectural best practices accordingly.  
이 도구는 아키텍처를 6가지 기둥 기준으로 검토하고, 모범 사례를 적용하도록 도와줍니다.  

---

## How the Tool Works  
## 도구 작동 방식  
You select your workload.  
워크로드를 선택합니다.  

You answer a series of questions related to the six pillars.  
6가지 기둥 관련 질문에 답합니다.  

You review your answers.  
답변을 검토합니다.  

You receive advice, including videos, documentation, and reports.  
비디오, 문서, 보고서를 포함한 조언을 받습니다.  

You see results in a dashboard.  
대시보드에서 결과를 확인합니다.  

---

## Defining a Workload in the Tool  
## 도구에서 워크로드 정의하기  
For example, you can define a demo workload and specify it as your production application.  
예를 들어, 데모 워크로드를 정의하고 이를 프로덕션 애플리케이션으로 지정할 수 있습니다.  

You provide details such as the review owner, environment (e.g., production), and AWS regions involved.  
검토자, 환경(예: 프로덕션), 관련 AWS 리전 등의 세부 정보를 제공합니다.  

You can also specify non-AWS regions, account IDs, and other infrastructure information.  
AWS가 아닌 리전, 계정 ID, 기타 인프라 정보도 지정할 수 있습니다.  

Next, you apply lenses to your workload.  
다음으로, 워크로드에 렌즈를 적용합니다.  

Lenses are sets of questions tailored to specific architectures.  
렌즈는 특정 아키텍처에 맞춘 질문 세트입니다.  

The default is the Well-Architected Framework lens, but there are others such as the FTR lens, serverless lens, SaaS lens, and even custom lenses you can create.  
기본 렌즈는 Well-Architected Framework 렌즈이며, FTR 렌즈, 서버리스 렌즈, SaaS 렌즈, 맞춤 렌즈 등도 있습니다.  

For simplicity, we focus on the Well-Architected Framework lens.  
단순화를 위해 Well-Architected Framework 렌즈에 집중합니다.  

---

## Reviewing Your Architecture  
## 아키텍처 검토  
Once the workload is defined, you start reviewing it by answering questions across the six pillars.  
워크로드 정의가 완료되면, 6가지 기둥 관련 질문에 답하며 검토를 시작합니다.  

For example, there might be 11 questions on operational excellence, 10 on security, and 6 on sustainability.  
예를 들어, 운영 우수성 11문항, 보안 10문항, 지속 가능성 6문항 등이 있을 수 있습니다.  

These numbers can change over time.  
이 숫자는 시간이 지남에 따라 변경될 수 있습니다.  

You answer each question, such as how you determine priorities or how your organization is structured.  
각 질문에 답하며, 예를 들어 우선순위 결정 방법이나 조직 구조 등을 작성합니다.  

After answering several questions, you save and continue.  
몇 가지 질문에 답한 후 저장하고 계속 진행합니다.  

The tool then provides a risk overview, showing high, medium, and low risks.  
도구는 이후 위험 개요를 제공하며, 고위험, 중위험, 저위험을 표시합니다.  

You can click on each risk to see recommendations and detailed guidance from the framework on how to address them.  
각 위험을 클릭하면 대응 방법에 대한 프레임워크 권장 사항과 상세 지침을 확인할 수 있습니다.  

---

## Using the Tool for Continuous Improvement  
## 지속적인 개선을 위한 도구 활용  
The tool gives you feedback and allows you to define milestones and improvement plans.  
도구는 피드백을 제공하며, 마일스톤과 개선 계획을 정의할 수 있습니다.  

Over time, as you address risks and implement best practices, your application becomes production-ready, compliant, and well-architected.  
시간이 지나면서 위험을 해결하고 모범 사례를 적용하면 애플리케이션은 프로덕션 준비가 되고, 규정 준수 및 Well-Architected 상태가 됩니다.  

This process supports continuous improvement and confidence in your architecture's quality.  
이 과정은 지속적인 개선과 아키텍처 품질에 대한 신뢰를 지원합니다.  

---

## Conclusion  
## 결론  
The AWS Well-Architected Framework and Tool provide structured guidance and practical means to build and maintain high-quality applications on AWS.  
AWS Well-Architected 프레임워크와 도구는 고품질 애플리케이션을 AWS에서 구축하고 유지하기 위한 구조적 지침과 실용적인 방법을 제공합니다.  

By following the six pillars and using the tool to assess and improve your workloads, you ensure operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability.  
6가지 기둥을 따르고 도구를 활용해 워크로드를 평가하고 개선하면, 운영 우수성, 보안, 신뢰성, 성능 효율성, 비용 최적화, 지속 가능성을 확보할 수 있습니다.  

Thank you for your attention, and I look forward to seeing you in the next lecture.  
경청해 주셔서 감사합니다. 다음 강의에서 뵙겠습니다.

Key Takeaways
핵심 요약
The AWS Well-Architected Framework provides best practices to build reliable, secure, efficient, and cost-effective applications on AWS.


AWS Well-Architected Framework는 AWS에서 신뢰성 있고, 안전하며, 효율적이고 비용 효율적인 애플리케이션을 구축하기 위한 모범 사례를 제공합니다.


The framework is structured around six pillars: operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability.


프레임워크는 6가지 기둥으로 구성됩니다: 운영 우수성, 보안, 신뢰성, 성능 효율성, 비용 최적화, 지속 가능성.


The AWS Well-Architected Tool helps review workloads against these pillars by answering structured questions and receiving recommendations.


AWS Well-Architected Tool은 구조화된 질문에 답하고 권장 사항을 받아 워크로드를 6가지 기둥 기준으로 검토하는 데 도움을 줍니다.


Continuous testing, architectural evolution, and improvement through game days are essential practices for maintaining well-architected applications.


지속적인 테스트, 아키텍처 진화, Game Days를 통한 개선은 Well-Architected 애플리케이션을 유지하는 데 필수적인 실무 관행입니다.


🎮 보상: "Well-Architected 전문가" 뱃지 획득!
