```md
# Rekognition Overview
# Rekognition 개요
# → 전체 개요

## Introduction to Amazon Rekognition
## Amazon Rekognition 소개
# → 서비스 개요

Amazon Rekognition is a service used to find objects, people, text, and scenes in images and videos using machine learning.  
Amazon Rekognition은 머신러닝을 사용하여 이미지와 비디오에서 객체, 사람, 텍스트, 장면을 찾는 서비스입니다.  
→ 이미지/비디오 분석

It can perform facial analysis and facial search to enable user verification and count how many people are present in an image.  
얼굴 분석과 얼굴 검색을 수행하여 사용자 인증을 가능하게 하고 이미지에 몇 명이 있는지 계산할 수 있습니다.  
→ 얼굴 기능

You can create your own database of familiar faces or compare against a database of celebrities to identify people in your images.  
친숙한 얼굴 데이터베이스를 만들거나 유명인 데이터베이스와 비교하여 이미지 속 인물을 식별할 수 있습니다.  
→ 맞춤 얼굴 DB

## Use Cases of Rekognition
## Rekognition 활용 사례
# → 활용 범위

Rekognition can label images and videos, perform content moderation, detect text, and conduct face detection and analysis.  
Rekognition은 이미지와 비디오에 라벨을 붙이고, 콘텐츠 검열, 텍스트 감지, 얼굴 탐지 및 분석을 수행할 수 있습니다.  
→ 기능 요약

For example, it can determine gender, age range, and emotions associated with faces.  
예를 들어, 얼굴에서 성별, 연령대, 감정을 판단할 수 있습니다.  
→ 얼굴 속성 분석

It supports face search and verification, celebrity recognition, and pathing, such as analyzing player movements in sports videos.  
얼굴 검색 및 인증, 유명인 인식, 경로 추적(예: 스포츠 비디오에서 선수 움직임 분석)을 지원합니다.  
→ 다양한 얼굴/움직임 분석

## Rekognition Website Demonstration
## Rekognition 웹사이트 시연
# → 실습 시연

The Rekognition website demonstrates how the service works by identifying elements in images, such as a person, rock, mountain bike, crest, and outdoors.  
Rekognition 웹사이트는 사람, 바위, 산악자전거, 문장, 야외 등 이미지 속 요소를 식별하여 서비스를 보여줍니다.  
→ 예제 시연

It can label images with objects like golden retrievers or dogs, perform content moderation to ensure appropriateness for all ages, and detect text such as runner numbers in a race.  
골든리트리버나 개 같은 객체 라벨링, 모든 연령대에 적합한 콘텐츠 검열, 레이스 참가자 번호 같은 텍스트 감지가 가능합니다.  
→ 라벨링 + 콘텐츠 검열

Face detection analysis can identify expressions, such as a person smiling with eyes open, and determine attributes like gender.  
얼굴 탐지 분석으로 눈을 뜨고 웃는 표정과 성별 등 속성을 확인할 수 있습니다.  
→ 얼굴 특징 분석

Face search and verification can be used in security applications, and celebrity recognition can identify well-known individuals, such as the CTO of AWS.  
얼굴 검색 및 인증은 보안 앱에서 사용 가능하며, 유명인 인식으로 AWS CTO 같은 인물을 식별할 수 있습니다.  
→ 보안/유명인 기능

Pathing allows monitoring movement in videos, for example, tracking players during a soccer game for real-time analytics.  
경로 추적(Pathing)을 통해 비디오에서 움직임을 모니터링할 수 있으며, 예를 들어 축구 경기에서 선수 이동을 추적할 수 있습니다.  
→ 동작 추적

## Content Moderation Feature
## 콘텐츠 검열 기능
# → 시험 대비 핵심

A key feature to know for the exam is content moderation, which detects inappropriate, unwanted, or offensive content in images and videos.  
시험에 중요한 기능은 콘텐츠 검열로, 이미지와 비디오에서 부적절하거나 원치 않거나 공격적인 콘텐츠를 감지합니다.  
→ 핵심 기능 강조

This feature is useful for social networks, broadcast media, advertising, and e-commerce to create a safe user experience by preventing offensive content from being displayed.  
이 기능은 SNS, 방송, 광고, 전자상거래에서 공격적 콘텐츠 표시를 방지하여 안전한 사용자 경험을 제공합니다.  
→ 실무 활용

Examples of flagged content include racist material, pornography, or other offensive items.  
검출 예시로는 인종차별적 자료, 포르노, 기타 공격적 콘텐츠가 있습니다.  
→ 예시

## How Content Moderation Works
## 콘텐츠 검열 작동 원리
# → 동작 방식

Amazon Rekognition analyzes the image and applies a Minimum Confidence Threshold for flagging items.  
Amazon Rekognition은 이미지를 분석하고 항목을 플래그할 최소 신뢰도 기준을 적용합니다.  
→ 신뢰도 기준

You can set this threshold to any percentage you prefer.  
이 신뢰도 기준은 원하는 퍼센트로 설정할 수 있습니다.  
→ 사용자 설정 가능

A lower confidence threshold results in more matches.  
신뢰도 기준을 낮추면 더 많은 항목이 매칭됩니다.  
→ 신뢰도와 민감도

This confidence percentage represents how certain Rekognition is that the flagged image contains inappropriate or offensive content.  
이 신뢰도는 플래그된 이미지가 부적절하거나 공격적 콘텐츠를 포함했을 가능성에 대한 Rekognition의 확신을 나타냅니다.  
→ 신뢰도 의미

After flagging images, you may want to perform a human manual review to confirm the findings.  
이미지를 플래그한 후에는 결과를 확인하기 위해 사람의 수동 검토를 수행할 수 있습니다.  
→ 수동 검토

## Amazon Augmented AI (A2I)
## Amazon Augmented AI (A2I)
# → A2I 활용

For manual review, you can use Amazon Augmented AI, known as A2I, which allows optional manual review directly within the service.  
수동 검토를 위해 Amazon Augmented AI(A2I)를 사용하여 서비스 내에서 직접 수동 검토를 선택할 수 있습니다.  
→ 선택적 검토

This process enables automatic flagging of sensitive images followed by a final manual review to decide whether to keep or delete them.  
이 과정은 민감한 이미지를 자동 플래그하고 최종적으로 수동 검토를 통해 유지할지 삭제할지 결정하게 합니다.  
→ 자동 + 수동 조합

This approach helps comply with regulations by detecting inappropriate content before it is posted to your applications.  
이 방법은 콘텐츠가 앱에 게시되기 전에 부적절한 내용을 감지하여 규제 준수를 돕습니다.  
→ 규제 준수

## Conclusion
## 결론
# → 정리

This concludes the lecture on Amazon Rekognition.  
이로써 Amazon Rekognition 강의가 마무리됩니다.  
→ 마무리

I hope you found it informative, and I look forward to seeing you in the next lecture.  
유익했기를 바라며, 다음 강의에서 뵙겠습니다.  
→ 인사

## Key Takeaways
## 핵심 요약
# → 시험 & 실무 포인트

Amazon Rekognition is a machine learning service for detecting objects, people, text, and scenes in images and videos.  
Amazon Rekognition은 이미지와 비디오에서 객체, 사람, 텍스트, 장면을 탐지하는 머신러닝 서비스입니다.  
→ 기본 개념

It supports facial analysis, facial search, user verification, and counting people in images.  
얼굴 분석, 얼굴 검색, 사용자 인증, 이미지 속 인원 수 계산을 지원합니다.  
→ 얼굴 기능

Rekognition can label images and videos, moderate content, detect text, analyze faces, recognize celebrities, and track movement paths.  
Rekognition은 이미지와 비디오 라벨링, 콘텐츠 검열, 텍스트 감지, 얼굴 분석, 유명인 인식, 움직임 경로 추적을 수행할 수 있습니다.  
→ 종합 기능

Content moderation uses confidence thresholds to flag inappropriate content, with optional manual review via Amazon Augmented AI (A2I).  
콘텐츠 검열은 신뢰도 기준으로 부적절한 콘텐츠를 플래그하며, Amazon Augmented AI(A2I)를 통한 선택적 수동 검토가 가능합니다.  
→ 검열 및 수동 검토
```

🎮 **게임보상: Rekognition 전문가 🏆**
→ 얼굴 분석, 유명인 인식, 콘텐츠 검열까지 완벽 마스터
