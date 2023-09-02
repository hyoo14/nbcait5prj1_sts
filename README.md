

# 문장 간 유사도 측정

의미 유사도 판별(Semantic Text Similarity, STS)이란 두 문장이 의미적으로 얼마나 유사한지를 수치화하는 자연어처리 태스크입니다.

#부스트캠프5기 #자연어처리

기간| 2023.04.12 ~ 2023.04.20 19:00



* 소개
  
  **
  
  보고서나 논문 등의 정보 전달 목적의 글을 쓰다보면, 같은 말을 반복해서 쓰게 되는 경우가 많습니다. 중복된 문장들은 가독성을 떨어뜨리는 요인 중 하나로써, 글의 퀄리티가 낮아지게 만들죠. 이런 경우 인간은 교정 작업을 하며, 의미적으로 중복된 문장을 인지하고 수정하게 됩니다. 그렇다면 기계의 경우 서로 구조적으론 다르지만, 의미가 유사한 것을 어떻게 구별할 수 있을까요?
  
  **

**![](https://lh5.googleusercontent.com/veZu5SdKvujQWfYi1_HgnA8J4IARC_51yWIQbZSpfmLhQEuFhBUk4jAmktg-8z1kWKgB62tOot8px6RfJR1BL81RNvhdpirrrXQDFr-cKhg4mroMu2_NNRGwnJAlMyxPQMzA1xTqLn9103KVVuud6-M)**

**

문맥적 유사도 측정이란?

이런 경우에 사용할 수 있는 Task가 바로, Semantic Text Similarity (STS)입니다. STS란 두 텍스트가 얼마나 유사한지 판단하는 NLP Task입니다. 일반적으로 두 개의 문장을 입력하고, 이러한 문장쌍이 얼마나 의미적으로 서로 유사한지를 판단합니다.

**

**![](https://lh5.googleusercontent.com/lMF4vMp9MkHjhw1utnPLTgpGA6fH7NrsU5h9gVMu7BssGfEGDeec0LQU0opahJXCQVz9oArM55SM1o-npfAv96x2q2Y6OzGM9Ph-9D5IZylsbomevV5IGFvY9eawaRfv1gx6lKOXRz8igiTWVOfbI2s)**

**

Textual Entailment와 Semantic Text Similarity의 차이점

관계를 예측한다는 점에서 Textual Entailment (TE)와 헷갈릴 수 있습니다. 두 문제의 가장 큰 차이점은 ‘방향성’입니다. STS는 두 문장이 서로 동등한 양방향성을 가정하고 진행되지만, TE의 경우 방향성이 존재합니다. 예를 들어 자동차는 운송수단이지만, 운송수단 집합에 반드시 자동차만 있는 것은 아닙니다. 또한 출력 형태에 대해서도 차이가 있습니다. TE, STS 모두 관계 유사도에 대해 참/거짓으로 판단할 수 있지만, STS는 수치화된 점수를 출력할 수도 있습니다.

이처럼 STS의 수치화 가능한 양방향성은 정보 추출, 질문-답변 및 요약과 같은 NLP 작업에 널리 활용되고 있습니다. 실제 어플리케이션으로는 데이터 증강, 챗봇의 질문 제안, 혹은 중복 문장 탐지 등에 응용되고 있습니다.

우리는 STS 데이터셋을 활용해 두 문장의 유사도를 측정하는 AI모델을 구축할 것입니다. 유사도 점수와 함께 두 문장의 유사함을 참과 거짓으로 판단하는 참고 정보도 같이 제공하지만, 최종적으로 0과 5사이의 유사도 점수를 예측하는 것을 목적으로 합니다!

학습 데이터셋 9,324개, 검증 데이터셋 550개, 평가 데이터는 1,100개가 제공됩니다. 평가 데이터의 50%는 Public 점수 계산에 활용되어 실시간 리더보드에 표기가 되고, 남은 50%는 Private 결과 계산에 활용되어 대회 종료 후 평가됩니다.

본 대회의 최종 결과물은 CSV 확장자 파일을 제출하게 됩니다.

- input : 두 개의 문장과 ID, 유사도 정보가 담긴 CSV 파일

- output : 평가데이터에 있는 각 문장쌍에 대한 ID와 유사도 점수가 담긴 CSV 파일

**