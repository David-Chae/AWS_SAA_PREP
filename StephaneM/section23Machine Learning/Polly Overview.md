```md
# Polly Overview
# Polly 개요
# → Amazon Polly 서비스 소개

## Introduction to Amazon Polly
## Amazon Polly 소개
# → 서비스 개요

Amazon Polly is the counterpart to Transcribe.  
Amazon Polly는 Transcribe의 반대 기능을 제공합니다.  
→ 음성 → 텍스트 vs 텍스트 → 음성

It converts text into speech using deep learning techniques.  
딥러닝 기술을 사용하여 텍스트를 음성으로 변환합니다.  
→ TTS(Text-to-Speech) 기능

This capability allows you to create applications that can speak aloud.  
이를 통해 음성을 출력할 수 있는 애플리케이션을 만들 수 있습니다.  
→ 음성 출력 앱 제작 가능

For example, Polly can say, "Hello, my name is Stephane and this is a demo of Amazon Polly."  
예를 들어, Polly는 "Hello, my name is Stephane and this is a demo of Amazon Polly."라고 말할 수 있습니다.  
→ 예제 문장 재생

It generates audio output that can be played back.  
재생 가능한 오디오 출력물을 생성합니다.  
→ 음성 파일 생성

Hi. My name is Stephane and this is a demo of Amazon Polly.  
안녕하세요. 제 이름은 Stephane이고, Amazon Polly 데모입니다.  
→ 재생 예시

## Features of Amazon Polly
## Amazon Polly 기능
# → 주요 기능

Amazon Polly offers more than simple text-to-speech conversion.  
Amazon Polly는 단순한 텍스트-음성 변환 이상의 기능을 제공합니다.  
→ 고급 TTS

It supports Pronunciation Lexicons and SSML to customize speech output.  
발음 사전(Pronunciation Lexicons)과 SSML을 지원하여 음성을 맞춤 설정할 수 있습니다.  
→ 발음/스타일 맞춤 가능

### Pronunciation Lexicons
### 발음 사전
# → 단어/약어 발음 설정

Pronunciation lexicons allow you to customize how specific words are pronounced.  
발음 사전을 사용하면 특정 단어의 발음을 맞춤 설정할 수 있습니다.  
→ 발음 수정

For example, if a stylized word like "Stephane" contains characters such as "3" and "4", Polly might incorrectly pronounce it as "S-T-3-P-H-4-N-E".  
예를 들어, "Stephane" 같은 단어에 "3", "4" 문자가 포함되면 Polly가 잘못 발음할 수 있습니다.  
→ 발음 오류 예시

Using a lexicon, you can specify the correct pronunciation "Stephane".  
발음 사전을 사용하면 올바른 발음 "Stephane"으로 지정할 수 있습니다.  
→ 발음 교정

Similarly, acronyms like "AWS" can be configured to be spoken as "Amazon Web Services" instead of spelling out each letter.  
마찬가지로 "AWS" 같은 약어도 각 글자를 말하는 대신 "Amazon Web Services"로 발음하도록 설정할 수 있습니다.  
→ 약어 발음 설정

You upload these lexicons and use them during the SynthesizeSpeech operation to ensure correct pronunciation.  
이 사전을 업로드하고 SynthesizeSpeech 작업 시 사용하면 올바른 발음을 보장할 수 있습니다.  
→ TTS 적용

### Speech Synthesis Markup Language (SSML)
### 음성 합성 마크업 언어(SSML)
# → 고급 음성 제어

SSML enables advanced customization of speech synthesis.  
SSML은 음성 합성을 고급으로 맞춤 설정할 수 있습니다.  
→ 강조, 쉼, 속성 설정

It allows you to emphasize specific words or phrases, use phonetic pronunciations, include breathing sounds, whisper, or apply speaking styles such as Newscaster.  
특정 단어/구 강조, 발음 기호 사용, 숨소리 삽입, 속삭임, 뉴스크래스터 같은 스타일 적용이 가능합니다.  
→ 다양한 음성 스타일 적용

Instead of generating speech from plain text, you can include SSML tags to control how the speech sounds, such as adding whispering or breaks.  
단순 텍스트 대신 SSML 태그를 포함하면 속삭임, 쉼 등 음성을 제어할 수 있습니다.  
→ SSML 태그 활용

To summarize:  
요약하면:  
→ 핵심 정리

- Use Pronunciation Lexicons for stylized words or acronyms.  
- 스타일화된 단어나 약어에는 발음 사전 사용  
→ 발음 교정

- Use SSML for detailed speech customization like whispering or phonetic pronunciation.  
- 속삭임, 발음 기호 등 세부 음성 설정에는 SSML 사용  
→ 음성 맞춤

## Using Amazon Polly Service
## Amazon Polly 서비스 사용
# → 실제 사용

Within the Amazon Polly service, you can convert text into lifelike speech.  
Amazon Polly에서 텍스트를 생생한 음성으로 변환할 수 있습니다.  
→ 자연스러운 TTS

You can select neural network voices, which provide the most natural and human-like speech possible.  
신경망 기반 음성을 선택하면 가장 자연스럽고 인간적인 음성을 제공합니다.  
→ 신경망 음성 선택

You can choose the voice you want and input the text.  
원하는 음성을 선택하고 텍스트를 입력할 수 있습니다.  
→ 음성 + 텍스트 입력

For example, entering "Hey, my name is Stephane and I love AWS" will produce corresponding speech.  
예를 들어, "Hey, my name is Stephane and I love AWS"를 입력하면 해당 음성을 생성합니다.  
→ 예제 문장 TTS

Hi, my name is Stephane and I love AWS.  
안녕하세요, 제 이름은 Stephane이고, AWS를 사랑합니다.  
→ 음성 출력 예시

### Demonstrating SSML with Breaks
### SSML을 활용한 음성 쉼 시연
# → SSML 실습

Using SSML, you can add breaks in speech.  
SSML을 사용하면 음성에 쉼을 추가할 수 있습니다.  
→ 음성 간격 제어

For example, saying "Hey, my name is Joanna," followed by a three-second break, and then continuing with "Now there's a break. I will read any text you type here," allows you to control speech pacing.  
예를 들어, "Hey, my name is Joanna,"라고 말하고 3초 쉼을 넣은 뒤, "Now there's a break. I will read any text you type here,"라고 이어서 말하면 말 속도를 제어할 수 있습니다.  
→ 말 속도 제어 예시

Hi, my name is Joanna.  
안녕하세요, 제 이름은 Joanna입니다.  
→ 발화 예시

Now there's a break.  
지금은 잠시 쉼입니다.  
→ SSML 쉼 적용

I will read any text you type here.  
여기에 입력하는 텍스트를 읽겠습니다.  
→ 동적 읽기

And this is how you control the speech itself using the SSML Markup Language.  
이와 같이 SSML 태그를 사용해 음성을 제어할 수 있습니다.  
→ SSML 제어 정리

### Customizing Pronunciation for Acronyms
### 약어 발음 맞춤 설정
# → 약어 발음 교정

If you want Polly to say "Amazon Web Services" instead of "AWS," you need to upload a pronunciation lexicon that maps "AWS" to "Amazon Web Services."  
"Amazon Web Services"로 발음되도록 하려면 "AWS"를 매핑한 발음 사전을 업로드해야 합니다.  
→ 약어 매핑

Once uploaded, Polly will automatically use this pronunciation whenever it encounters "AWS."  
업로드 후 Polly는 "AWS"를 만날 때마다 자동으로 해당 발음을 사용합니다.  
→ 자동 발음 적용

## Conclusion
## 결론
# → 정리

This overview covers everything you need to know about Amazon Polly for the exam.  
이 개요는 시험 대비 Amazon Polly의 핵심 내용을 모두 다룹니다.  
→ 시험 포인트

It provides powerful tools to convert text to speech with customizable pronunciation and speech styles.  
발음과 음성 스타일을 맞춤 설정할 수 있는 강력한 TTS 도구를 제공합니다.  
→ 맞춤형 TTS

## Key Takeaways
## 핵심 요약
# → 시험 & 실무 포인트

Amazon Polly converts text into lifelike speech using deep learning.  
Amazon Polly는 딥러닝을 사용해 텍스트를 자연스러운 음성으로 변환합니다.  
→ 딥러닝 기반 TTS

Pronunciation lexicons customize how specific words or acronyms are spoken.  
발음 사전을 사용해 특정 단어/약어 발음을 맞춤 설정합니다.  
→ 발음 교정

SSML (Speech Synthesis Markup Language) enables advanced speech customization like breaks, emphasis, and whispering.  
SSML은 쉼, 강조, 속삭임 등 고급 음성 설정을 가능하게 합니다.  
→ 고급 음성 제어

Polly supports neural voices for the most natural and human-like speech synthesis.  
Polly는 신경망 음성을 지원하여 가장 자연스러운 음성을 생성합니다.  
→ 자연스러운 음성
```

🎮 **게임보상: Polly 마스터 🏆**
→ TTS, SSML, 발음 사전, 신경망 음성까지 완벽 습득
