```md
# Comprehend Medical Overview
# Comprehend Medical 개요
# → Amazon Comprehend Medical 서비스 소개

## Introduction to Amazon Comprehend Medical
## Amazon Comprehend Medical 소개
# → 서비스 기본 개념

Amazon Comprehend Medical detects and returns useful information in unstructured clinical text.  
Amazon Comprehend Medical은 비정형 임상 텍스트에서 유용한 정보를 탐지하고 반환합니다.  
→ 비정형 의료 데이터 분석

For example, if your doctor is taking notes, or if you have discharge summaries, test results, or case notes, it will use natural language processing to detect all the protected health information within the document itself using the DetectPHI API.  
예를 들어, 의사가 작성한 진료 기록, 퇴원 요약, 검사 결과, 사례 기록 등이 있을 때, DetectPHI API를 사용하여 문서 내 모든 보호된 건강 정보를 NLP로 탐지합니다.  
→ PHI(Protected Health Information) 탐지 기능 강조

## Architecture Overview
## 아키텍처 개요
# → 시스템 구성 개념

From an architecture perspective, you would store whatever documents you have in Amazon S3, and then invoke the Comprehend Medical API.  
아키텍처 관점에서, 모든 문서를 Amazon S3에 저장한 뒤 Comprehend Medical API를 호출합니다.  
→ S3 + Comprehend Medical 연계

Alternatively, you could use Kinesis Data Firehose to analyze data in real time.  
또는 Kinesis Data Firehose를 사용해 데이터를 실시간 분석할 수도 있습니다.  
→ 실시간 데이터 분석 옵션

Additionally, Amazon Transcribe can be used to first transcribe voice into text.  
또한, Amazon Transcribe를 사용해 음성을 먼저 텍스트로 변환할 수 있습니다.  
→ 음성 → 텍스트 변환

Once the data is in text form, it can be passed to the Amazon Comprehend Medical service.  
데이터가 텍스트 형태가 되면 Amazon Comprehend Medical 서비스로 전달할 수 있습니다.  
→ NLP 분석 단계

## Demonstration of Real-Time Analysis
## 실시간 분석 데모
# → 콘솔 시연

Let's look into the console to see how this works.  
콘솔에서 이 기능이 어떻게 작동하는지 살펴보겠습니다.  
→ 실습 예시 강조

In the Amazon Comprehend Medical service, you can launch a real-time analysis.  
Amazon Comprehend Medical 서비스에서 실시간 분석을 실행할 수 있습니다.  
→ 실시간 분석 가능

Here, you input text, which could be a doctor's note containing various clinical details.  
여기서 텍스트를 입력할 수 있으며, 의사의 기록 등 다양한 임상 정보를 포함할 수 있습니다.  
→ 입력 데이터 예시

After submitting the text for analysis, the service identifies entities such as age, occupation (e.g., high school teacher), procedure names, dates, and times related to procedures.  
텍스트를 분석용으로 제출하면, 서비스는 나이, 직업(예: 고등학교 교사), 시술 이름, 날짜 및 시술 관련 시간을 엔티티로 식별합니다.  
→ 핵심 엔티티 추출

## Extracted Data and Structuring
## 추출 데이터 및 구조화
# → 데이터 구조화

The extracted data becomes quite organized.  
추출된 데이터는 체계적으로 구성됩니다.  
→ 데이터 정리 효과

For instance, it identifies generic names of molecules, their strength, dosage, route, and frequency.  
예를 들어, 약물의 일반명, 용량, 투여 경로, 투여 빈도를 식별합니다.  
→ 의료 데이터 상세 분석

This capability allows you to start structuring all your health data from unstructured text using machine learning.  
이 기능을 통해 머신러닝으로 비정형 텍스트에서 건강 데이터를 구조화할 수 있습니다.  
→ 구조화된 데이터 변환

## Final Remarks
## 마무리
# → 결론 및 참고

You can explore these features further; however, the medical field is complex and requires expertise.  
이 기능들을 더 탐색할 수 있지만, 의료 분야는 복잡하며 전문 지식이 필요합니다.  
→ 전문성 필요 강조

At least, thanks to Amazon Comprehend Medical, you can take information in text form and derive meaningful insights from it.  
적어도 Amazon Comprehend Medical 덕분에 텍스트 형태의 정보를 의미 있는 인사이트로 도출할 수 있습니다.  
→ 실무 활용 가능성 강조

## Key Takeaways
## 핵심 포인트
# → 시험/실무용 요약

Amazon Comprehend Medical detects and extracts useful information from unstructured clinical text using natural language processing.  
Amazon Comprehend Medical은 NLP를 사용해 비정형 임상 텍스트에서 유용한 정보를 탐지하고 추출합니다.  
→ 핵심 기능 요약

It can identify protected health information within documents using the DetectPHI API.  
DetectPHI API를 사용하여 문서 내 보호된 건강 정보를 식별할 수 있습니다.  
→ PHI 탐지

The service integrates with Amazon S3 for document storage, Kinesis Data Firehose for real-time analysis, and Amazon Transcribe for converting voice to text.  
이 서비스는 문서 저장용 S3, 실시간 분석용 Kinesis Data Firehose, 음성 → 텍스트 변환용 Amazon Transcribe와 통합됩니다.  
→ 통합 아키텍처 강조

Comprehend Medical structures unstructured health data such as doctor's notes, discharge summaries, and test results into organized entities like medication details and procedures.  
Comprehend Medical은 의사 기록, 퇴원 요약, 검사 결과와 같은 비정형 건강 데이터를 약물 정보, 시술 등과 같은 구조화된 엔티티로 변환합니다.  
→ 구조화된 의료 데이터 생성
```

🎮 **게임보상: Comprehend Medical 전문가 🏥**
→ 임상 텍스트 분석, PHI 탐지, 의료 데이터 구조화 이해 완료
