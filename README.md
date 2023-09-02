

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



**

피어슨 상관 계수(Pearson Correlation Coefficient ,PCC)는 두 변수 X 와 Y 간의 선형 상관 관계를 계량화한 수치로, 보통 상관관계라 함은 피어슨 상관관계를 칭합니다.

코시-슈바르츠 부등식에 의해 -1~1 사이의 값을 가지며, +1은 완벽한 양의 선형 상관 관계, 0은 선형 상관 관계 없음, -1은 완벽한 음의 선형 상관 관계를 의미합니다.

**

**

![](https://lh5.googleusercontent.com/xONAwpoq9MXiZKe-09QUGU8so9pRhMboPTxOEG_Q2Z4QorEgtJamBFcOz6zjqt4IdCXw0z1NN3mCHIN805uWPUSTtVvKDyutCpB1AekQi2iBFaJou5DlFgwvidIR5Fcu75TydYmURYY90VXwdBbVX5I)**



**

피어슨 상관 계수는 정답과 예측이 일치하지 않더라도 증감율이 일치하면 1에 가까운 값을 보입니다.

반대로 정답값과 예측이 근사하더라도 증감율이 다르면 -1에 가까운 값을 보일 수 있습니다.

이는 정답을 정확히 예측하는 것 보다, 높은 값은 확실히 높게, 낮은 값은 확실히 낮게, 즉 전체적인 경향을 잘 예측하는 것이 중요함을 의미합니다.

**





**

- 프로젝트 전체 기간 (2주) : 4월 10일 (월) 10:00 ~ 4월 20일 (목) 19:00

- 팀 병합 기간 : 4월 11일 (화) 16:00 까지

- 팀명 컨벤션 : 도메인팀번호(2자리)조 / ex) CV_03조, NLP_02조, RecSys_08조

- 리더보드 제출 오픈 : 4월 12일 (수) 10:00

- 리더보드 제출 마감 : 4월 20일 (목) 19:00

- 최종 리더보드 (Private) 공개 : 4월 20일 (목) 20:00

- GPU 서버 할당 : 4월 10일 (월) 10:00

- GPU 서버 회수 : 4월 28일 (금) 16:00

**



**

대회 룰

- [대회 참여 제한] NLP 도메인을 수강하고 있는 캠퍼에 한하여 리더보드 제출이 가능합니다.

- [팀 결성 기간] 팀 결성은 대회 페이지 공개 후 2일차 오후 4시까지 필수로 진행해 주세요. 팀이 완전히 결성되기 전까지는 리더보드 제출이 불가합니다.

- [일일 제출횟수] 일일 제출횟수는 '팀 단위 10회'로 제한합니다. (일일횟수 초기화 자정 진행)

- [외부 데이터셋 규정] 본 대회에서는 외부 데이터셋 사용을 금지합니다. (외부 데이터에 의존하는 것이 아니라, 주어진 데이터셋을 기반으로 모델링 성능 개선에 집중해 보시길 바랍니다)

- [기학습 가중치 사용] 저작권상 사용이 불가한 경우를 제외하고는 모든 기학습 가중치 사용은 허용됩니다.

- [테스트셋 활용 가능 여부] 참가자는 모델 학습에 테스트셋을 활용하거나, 테스트셋의 정보를 학습에 활용하여 최종 결과를 낼 수 없습니다.

- [데이터 증강] Train/Dev 데이터에 한해 증강 가능합니다. 다만 기술적/통계적 근거가 존재해야하며, 누구나 동일한 증강 결과물을 생성할 수 있어야 합니다.

- [데이터셋 저작권] 대회 데이터셋은 '캠프 교육용 라이선스' 아래 사용 가능합니다. 저작권 관련 세부 내용은 부스트코스 공지사항을 반드시 참고 해주세요.

**



**

AI Stages 대회 공통사항

- [Private Sharing 금지] 비공개적으로 다른 팀과 코드 혹은 데이터를 공유하는 것은 허용하지 않습니다.  
  코드 공유는 반드시 대회 게시판을 통해 공개적으로 진행되어야 합니다.

- [최종 결과 검증 절차] 리더보드 상위권 대상으로추후 코드 검수가 필요한 대상으로 판단될 경우 개별 연락을 통해 추가 검수 절차를 안내드릴 수 있습니다. 반드시 결과가 재현될 수 있도록 최종 코드를 정리 부탁드립니다. 부정행위가 의심될 경우에는 결과 재현을 요구할 수 있으며, 재현이 어려울 경우 리더보드 순위표에서 제외될 수 있습니다.

- [공유 문화] 공개적으로 토론 게시판을 통해 모델링에 대한 아이디어 혹은 작성한 코드를 공유하실 것을 권장 드립니다. 공유 문화를 통해서 더욱 뛰어난 모델을 대회 참가자 분들과 같이 개발해 보시길 바랍니다.

- [대회 참가 기본 매너] 좋은 대회 문화 정착을 위해 아래 명시된 행위는 지양합니다.

- 대회 종료를 앞두고 (3일 전) 높은 점수를 얻을 수 있는 전체 코드를 공유하는 행위

- 타 참가자와 토론이 아닌 단순 솔루션을 캐내는 행위

**



  **

주요 데이터는 csv 형태로 제공되며 주어지는 두 문장 간의 유사도를 예측하는 것이 최종 목표입니다. 데이터셋의 train/dev/test 은 85/5/10의 비율로 나누어졌습니다.

아래는 각 데이터의 개수와 Label 점수의 의미입니다.

- 총 데이터 개수 : 10,974 문장 쌍

- Train 데이터 개수: 9,324

- Test 데이서 개수: 1,100

- Dev 데이터 개수: 550

- Label 점수: 0 ~ 5사이의 실수

- 5점 : 두 문장의 핵심 내용이 동일하며, 부가적인 내용들도 동일함

- 4점 : 두 문장의 핵심 내용이 동등하며, 부가적인 내용에서는 미미한 차이가 있음

- 3점 : 두 문장의 핵심 내용은 대략적으로 동등하지만, 부가적인 내용에 무시하기 어려운 차이가 있음

- 2점 : 두 문장의 핵심 내용은 동등하지 않지만, 몇 가지 부가적인 내용을 공유함

- 1점 : 두 문장의 핵심 내용은 동등하지 않지만, 비슷한 주제를 다루고 있음

- 0점 : 두 문장의 핵심 내용이 동등하지 않고, 부가적인 내용에서도 공통점이 없음

각 데이터별 Label 점수는 여러명의 사람이 위의 점수 기준을 토대로 평가한 두 문장간의 점수를 평균낸 값입니다. 두 문장간의 유사도는 사람마다 다르게 평가될 수 있다는 점을 고려하여 데이터를 확인해주세요.

데이터 구조인 각 column 별 설명입니다. 예측 타겟 값은 0 ~ 5점 사이의 값입니다. 데이터는 id를 기준으로 정렬되어 있습니다.

**

**![](https://lh5.googleusercontent.com/fmyJjwGukIcg2MIVXKFI5tz68X6M1OVF0qUDuTLFzBkWNpc3L1NUi817FtQxvFC28Q6fa5RPis4dESiM7Gglas6UopR7m7WjkX4lyvHIQgNAmbeDun7ldx_LA1buNMnyRnHmWeiC-BDy-cldqS1rddQ)**



**

- id (문자열) : 문장 고유 ID입니다. 데이터의 이름과 버전, train/dev/test가 적혀 있습니다.

- source (문자열) : 문장의 출처로 총 3가지 source 가 있습니다.

- petition (국민청원 게시판 제목 데이터)

- NSMC (네이버 영화 감성 분석 코퍼스, Naver Sentiment Movie Corpus)

- slack (업스테이지(Upstage) 슬랙 데이터)

- sentence1 (문자열) : 문장 쌍의 첫번째 문장입니다.

- sentence2 (문자열) : 문장 쌍의 두번째 문장입니다.

- label : 문장 쌍에 대한 유사도로 0~5 점으로 소수 첫째 자리까지 있습니다.

- binary-label : 문장 쌍에 대한 유사도가 2점 이하인 경우엔 0으로, 3점 이상인 경우엔 1로 변환한 binary label 입니다.

제공되는 데이터는 train.csv / dev.csv / test.csv / sample_submission.csv의 4개의 파일로 되어있으며 train.csv, dev.csv 파일로 학습하여 모델을 생성합니다.

**



**

- id (문자열) : 문장 고유 ID입니다. 데이터의 이름과 버전, train/dev/test가 적혀 있습니다.

- source (문자열) : 문장의 출처로 총 3가지 source 가 있습니다.

- petition (국민청원 게시판 제목 데이터)

- NSMC (네이버 영화 감성 분석 코퍼스, Naver Sentiment Movie Corpus)

- slack (업스테이지(Upstage) 슬랙 데이터)

- sentence1 (문자열) : 문장 쌍의 첫번째 문장입니다.

- sentence2 (문자열) : 문장 쌍의 두번째 문장입니다.

- label : 문장 쌍에 대한 유사도로 0~5 점으로 소수 첫째 자리까지 있습니다.

- binary-label : 문장 쌍에 대한 유사도가 2점 이하인 경우엔 0으로, 3점 이상인 경우엔 1로 변환한 binary label 입니다.

제공되는 데이터는 train.csv / dev.csv / test.csv / sample_submission.csv의 4개의 파일로 되어있으며 train.csv, dev.csv 파일로 학습하여 모델을 생성합니다.

**

**

![](https://lh6.googleusercontent.com/f1yvqoNZwuLLHj_uSWs36M1DeANRBkWZwDcdQkr4r3vpsMaso4WmmTmNgu3218TNWdeWkUd-VgyMQsqaNojd-faJPQhFMzpODntPgZ9zCO1SgZONdO0wkOO6ainnvZX6NT7s9-pTaW7eh_0ZDTJ_lGA)**



**여러분의 과제는 학습된 모델로 test.csv 파일을 활용하여 출력되는 예측 값을 제출하는 것입니다. 제출 파일은 sample_submission.csv 와 같은 구조를 가져야 합니다. sample_submission.csv 파일의 구조는 테스트 데이터의 id가 있어야 하고 target 에 테스트 데이터의 id와 맞게 예측된 0~5점의 label 값이 들어가야 합니다.**



**![](https://lh3.googleusercontent.com/NJCFJUCXEULWV_AGPlw8i217tGTw34dEm5sEWIy0kxGWLw5V9XLwizMEzFN04zgOKZFtrzGju0XdNRfWEhs5KIOii54h8P_6ufRDJKMBU7i8BxAqyQGONLc_qCjA9ObtG1yh528D-_R_Vio81k7K9nA)**





**

테스트 데이터셋은 학습 데이터셋과 다르게 label 과 binary-label이 없습니다.

├─code.tar.gz

│  │  train.py

│  │  inference.py

│  │  requirements.txt

코드 파일은 [train.py](http://train.py), [inference.py](http://inference.py), requirements.txt 세 가지로 구성되어 있습니다.

- train.py : 데이터 학습에 사용되는 코드입니다.

- inference.py : 학습된 모델로 데이터를 예측하는 코드입니다.

- requirements.txt : train.py와 inference.py를 실행하는데 필요한 라이브러리들이 담겨있는 txt 파일입니다.

코드는 requirements.txt 설치, [train.py](http://train.py), [inference.py](http://inference.py) 순서로 실행합니다.

---

requirements.txt

- requirements.txt에는 train.py와 inference.py를 실행하기 위해 필요한 라이브러리들이 담겨있습니다.

- train.py와 [inference.py](http://inference.py) 코드를 제작할 때 활용되었던 버전을 명시하였습니다.

- pip install -r requirements.txt를 통해 requirements.txt의 라이브러리들을 한번에 설치할 수 있습니다.

[train.py](http://train.py)

- train.py는 데이터 호출 및 전처리를 위한 Dataset과 Dataloader, 학습에 사용되는 Model이 구현되어 있습니다.

- 코드는 python3 train.py 를 통해 실행할 수 있습니다.

- 선학습 모델은 [KLUE-bencmark](https://github.com/KLUE-benchmark/KLUE/blob/main/README.md)에서 STS task에 좋은 성능을 보였던 RoBERTa를 사용하였습니다. 학습의 편의를 위해 RoBERTa-small을 사용합니다.

- ArgumentParser에는 다음과 같은 인자가 있습니다. :

- --model_name은 학습에 사용되는 선학습 모델 입니다.

- --batch_size는 학습에 사용되는 배치 크기 입니다.

- --max_epoch은 학습의 총 에폭 입니다.

- --shuffle은 train 데이터셋의 순서를 섞을지 말지 결정하는 인자입니다.

- --learning_rate는 모델의 learning rate입니다.

- --trainpath, devpath, testpath, predictpath는 각 데이터의 경로 입니다.

- 코드 실행 시 원하는 인자를 변경하여 실행할 수 있습니다. 인자가 없으면 자동으로 default 값으로 설정되어 실행합니다.

- ex) python3 train.py  
  → model_name = klue/roberta-small

- ex) python3 train.py --model_name=klue/bert-base  
  → model_name = klue/bert-base

- 학습은 에폭당 약 3분 소요됩니다.

- 학습이 완료되면, torch.save(model, 'model.pt') 를 통해 선학습된 모델을 model.pt라는 파일로 저장하게 됩니다.

[inference.py](http://inference.py)

- inference.py는 train.py에서 학습된 모델을 호출하여 문제 데이터셋을 예측하는 코드입니다.

- 코드는 python3 inference.py 를 통해 실행할 수 있습니다.

- Inference part의 순서는 다음과 같습니다 :
1. train.py에서 저장된 model.pt를 호출하여 데이터 예측을 진행합니다.

2. 예측된 결과를 제출 형식에 맞게 변경하여 준비합니다.

3. sample_submission.csv를 불러와 target만 예측된 결과로 변경하고 output.csv로 저장합니다.
- 코드 실행이 끝나면 output.csv라는 예측 결과 파일이 생성되고 리더보드

Download Data Link

https://aistages-prod-server-public.s3.amazonaws.com/app/Competitions/000236/data/data.tar.gz

Download Baseline Code Link

https://aistages-prod-server-public.s3.amazonaws.com/app/Competitions/000236/data/code.tar.gz

![](https://lh4.googleusercontent.com/8mQc-x-HbA7symQiQUJw9g1g1gEu6jXRZiHNdmpAOAkPBrwK9ZkEDw1KkeI058SAX3naUukrbX8MC7CSqTMr9Tg-7RwFxnPbByN72e-q-2MhmcVeckwoovSMs8nX5gsAQg96wKR4adE4_zz1NxpuZsY)

![](https://lh3.googleusercontent.com/J6QbprYyDeniErGlX4nk-7IQViN2LH24UQVJveYg7uATcI4gVSs5ChrYZhLs31pTKBHP2dKbYzVt5LPQP2xauh3dAWy84sNOtkiGkmgVcq714Qm5J_2_7ELEcc-k4eikaCbxsLySZt1HnmtOtuyePiw)

**





**[공유] STS 문제에서 피어슨 상관계수를 사용하는 이유

Posted by 정지수

2023.03.27.15:18

 7

UP

NLP의 많은 문제들을 풀 때, 대체로 우리는 이미 통상적으로 사용하는 평가 지표가 있습니다. 앞서 배운 것처럼, N21, N2N 문제에는 f1-score, N2M 문제에는 BLEU, ROGUE 등이 있죠.

STS 문제에서는 왜 배웠던 지표가 아닌, 피어슨 상관 계수(Pearson Correlation Coefficient)라는 이름도 어려운 지표를 사용할까요?

이 질문의 답은 “출력 형태”에서 찾아볼 수 있습니다.

일반적인 N21 문제에는 Classification 뿐만 아니라, Regression도 포함되어 있습니다. 둘 다 하나의 숫자, 혹은 라벨을 출력한다는 공통점이 있지만, classification은 정해진 범위 내에서 출력이 있고, regression의 경우 실수 범위에서 수치가 출력된다는 차이점이 있습니다.

피어슨 상관 계수는 이런 regression으로 출력된 예측값 집합과 정답 집합간의 유사도를 나타냅니다.

두 집합 x, y에 대한 피어슨 상관계수 식은 다음과 같습니다.

![](https://lh3.googleusercontent.com/zLDWsdlmdXgNwCUcTnAGPMLM2AwvHRczD44vqZbwxymYZIeBXYlCsb32n80LV9HtSi6JaYlTbGZ-bAcKlmcs_FGq3IXWkColD2SsDfokwM4bUmwI97cVyzLZLNKP_o3hWWY_Ovovh8l35_BE8yrY-vM)

r은 항상 -1~1 사이의 실수를 가지게 됩니다. 높을수록 두 집합 사이의 일치도가 높다고 평가하며, 음수일 경우 두 집합은 서로 역수 관계로 평가됩니다. 대체로 아래 표처럼 따라 판별됩니다.

![](https://lh5.googleusercontent.com/X6MbnmL6Gyru_fZ53myqHDcac3mF9K74aX5OIus2Z_G0hbHvXf5-Qk_cu9XZSRFE8d_zLSCgUCC8l5aHalTKwZnZbS9oLhA15CF35aIpcZ6ebPlhhusuwEJ8THJiioGQNcp4meY-d4psq5usYEZD43g)

Hinkle, D. E., Wiersma, W., & Jurs, S. G. (2003). Applied statistics for the behavioral sciences  (Vol. 663). Houghton Mifflin College Division.

피어슨 상관계수에도 단점은 있습니다. 두 집합의 선형적 관계만을 보기 때문에, 점수로만 판단하기에는 너무 다양한 형태가 존재할 수 있다는 점입니다.

![](https://lh5.googleusercontent.com/WC4jcYsp6bqL1xOP_xmZqa2HIwg4gy0kuKOMU__RRfpzi6OSMH8FifNCRXaDbWcKVqTdzUgp8Ky6rIWoXYiOdKqt1SX_UroJM43WEAaOr2tPO25VGpd1zDuI5UKaMCkHNpLCEXmDuKN8-HN0SKaSa90)

Anscombe, F. J. (1973). Graphs in statistical analysis. The american statistician , 27 (1), 17-21.

일례로, 위 그림은 모두 0.82의 상관계수를 가지나 모두 생김새가 다릅니다. 그러므로, 결과 분석 시 꼭 산점도를 그려보며 모델의 취약점을 평가해야합니다.

그렇다면, 실제 코드에서 피어슨 상관계수를 어떻게 적용할까요?

이미 여러 regression 문제에 사용되는 지표인 만큼, torchmetric 라이브러리에 이미 구현되어 있습니다.

적용 예제는 아래와 같습니다.

import torch

from torchmetrics import PearsonCorrcoef

target = torch.tensor([5.0, 6.0, 0.0, 2.0])

preds = torch.tensor([2.5, 4.57, 2, 1.5])

pearson = PearsonCorrcoef()

pearson(preds, target)

해당 예제는 작동 후 0.7692의 상관 계수를 출력합니다.

![](https://lh3.googleusercontent.com/6xu6wLXx0XhiNOaubRGUohh28FnyH_KhvQa4f85c9J93kTfUofqRJ5RgvWn6lYowGKl7tWkxe3bOPGJIZnUNWdckv-tksoXSBrTZKyHWMi0ECyRhwyPs8kVz4a1agCQayFYTS2a8Ny_L3CMvo0XPExQ)

피어슨 상관계수는 두 텐서의 shape이 동일해야한다는 점을 주의하여 적용해주세요!

참고 사이트

https://torchmetrics.readthedocs.io/en/latest/regression/pearson_corr_coef.html**





**

[공유] 거인의 어깨에 올라서기

Posted by 황태욱_조교

2023.03.28.18:07

 5

UP

컴퓨터공학은 다른 학문에 비해 변화 속도가 빠른 편인데, 그 중 AI는 유독 더 빠른편입니다. 최신 기술을 찾는 가장 확실한 방법은 논문을 보는 것입니다.

하지만 다달이 state of the art(SOTA, 최고성능) 모델이 갱신되는 상황이라, 최신 논문을 쫓아가기가 상당히 버겁습니다.

반면에 AI라는 특수한 학문이라서 최신 기술을 빠르게 파악할 수 있는 방법이 있습니다.

1. 태스크 및 데이터셋별로 SOTA를 확인할 수 있는 [PapersWithCode](https://paperswithcode.com/)

2. 세계 최대의 데이터 과학자 커뮤니티 [Kaggle](https://www.kaggle.com/)

3. 국내의 AI 경진대회 플랫폼 [Dacon](https://dacon.io/), [AIFactory](https://aifactory.space/)
- [PapersWithCode](https://paperswithcode.com/)는 태스크와 데이터셋별로 SOTA 모델 히스토리와 해당 모델들의 논문, 깃허브 링크를 모아둔 웹사이트입니다. 이곳을 통해 현재 최신 트렌드와 코드까지 찾을 수 있습니다.  
  ![](https://lh6.googleusercontent.com/e3tGqpbcpyjjrmza4B9abS2v-t9BQg8Farcvlft3zEYG2mkVIKJm7du8O0QaGxfgdd6WFCWa4dc6GKfa-Q99iH6D8qNgSHc3l2oDdtr5Sb44KbW-xPgcFhLhFJTfJhBWcpBMO0wV8aDso66Eb2RPIT8)  

- [Kaggle](https://www.kaggle.com/)은 AI 경진대회와 커뮤니티가 적절히 융합되어있습니다. 집단지성을 통한 문제해결을 표방하기 때문에 Code, Discussions에 수많은 정보가 공유되고 있습니다. 또한 상금이 걸려있는 Competitions에도 실시간으로 각자가 수행한 EDA(탐색적 데이터 분석)결과나 높은 성능을 보이는 모델 코드를 공유하는 최신 기술을 빠르게 접할 수 있습니다.  
  ![](https://lh4.googleusercontent.com/1D84fP0EqtrMTxlj2jkyT03GE5An0e9D2imyMgEzxy5DZ8PbEbHvWpYenc965YO0ovWsmnEQYxq3fFKJVDNzPgnXvEofEziLhTnmrLWgikVuv5unzVOLHcdnCQEDdwJqefMHCaKWOooH2iXLFh9w4W0)  

- [Dacon](https://dacon.io/)과 [AIFactory](https://aifactory.space/)는 국내 AI 경진대회로, Kaggle에 비하면 정보의 공유량은 현저히 낮습니다. 하지만 대회마다 베이스라인 코드를 함께 공개하는 편이며, 수상작의 코드도 공개하는 추세입니다.  
  ![](https://lh4.googleusercontent.com/HlrRRyNkJm8dDwTLjXtpSpCj-sj5Q6ZpI_ubhCHnQGRsuZSyNEfCrslR2sGi9Q2W7DcXVYr2oWKJmt4DsviMXTC3WzIyrsVhLMz23RuZLnubSmLFAVg1SA3bc2k-wl1bo54JsIiSC-BrisLUy31kkdI)

이렇게 최신 기술을 접할 수 있는 방법을 알아보았습니다. 이들을 잘 활용하기 위한 팁은 아래와 같습니다.

1. [PapersWithCode](https://paperswithcode.com/)를 통해 최신 트랜드 모델과 논문참고하기

2. [Kaggle](https://www.kaggle.com/)에 있는 유사 태스크 및 데이터셋을 찾아 최신 기술(EDA, 앙상블, 모델 등) 알아보기

3. 1번과 2번이 어렵다면 [Dacon](https://dacon.io/)과 [AIFactory](https://aifactory.space/)에서 유사 태스크 및 데이터셋을 찾아 베이스라인코드와 공개된 코드 활용하기

이러한 방법만 잘 활용하시면 쉽게 상위권에 근접할 수 있습니다.

아직까지 국내에서는 대회에서 정보 교류가 적은 편인데, 서로 발전할 수 있는 기회가 많아지길 바랍니다!

**



**

[공유] Huggingface 200% 활용하기

Posted by 남궁혁_조교

2023.03.29.13:48

 5

UP

이번 토론에서 Huggingface에 대해 알아봅시다.

1. Huggingface 란 무엇인가?

HuggingFace는 다음을 제공하는 커뮤니티 및 Data Science 플랫폼입니다.

![](https://lh6.googleusercontent.com/uXv8sYf3vHZN4kIj3O5BrgSmPhU1CTPIeQD5Kov-ITrNUCVKGvtKSR-rDKmHoKsdx-803RQi320KUsHPO9PiYQmv_QLxV5tLJzHlV76D8KGHrVhE41SAMtGwSru3MSa8DlJasfEel_QlLHhlCkyHxyE)

- 사용자가 오픈 소스(OS) 코드 및 기술을 기반으로 ML 모델을 구축, 교육 및 배포할 수 있는 도구

- 광범위한 Data Scientist, Researcher 및 ML 엔지니어 커뮤니티가 함께 모여 아이디어를 공유하고, 지원을 받고, 오픈 소스 프로젝트에 기여할 수 있는 곳

- JAX, PyTorch 및 TensorFlow를 지원하는 최첨단 기계 학습

- 참고 링크

- [GitHub - huggingface/transformers: 🤗 Transformers: State-of-the-art Machine Learning for Pytorch, TensorFlow, and JAX.](https://github.com/huggingface/transformers)

- 일반적인 [layer.py](http://layer.py/), [model.py](http://model.py/) 는 transformer.models 로 대응해서 사용할 수 있습니다.

transformers.models

- 트랜스포머 기반의 다양한 모델을 pytorch, tensorflow로 각각 구현해 놓은 모듈입니다.

- 각 모델에 맞는 tokenizer 도 구현되어 있습니다.
1. Huggingface Tasks

HuggingFace는 텍스트, 시각 및 오디오와 같은 다양한 양식에 대한 작업을 수행하기 위해 수천 개의 사전 훈련된 모델을 제공합니다.

이러한 모델은 다음에 적용할 수 있습니다.

![](https://lh4.googleusercontent.com/CqoH4o9KxNV2qkYkNQ6HN2_fQkuclPqmtc-RHy3sctFhFRbKXl9_MsxtXZJ0fns-hh5i369I_EfIxNfCvYUyOGvmX3xFOLO6kqei8pyRYG_GnGM2vdEFEFfJbJo-cXkwuchWyzaedLB-iw2EQD9aWtc)

- 100개 이상의 언어로 된 텍스트 분류, 정보 추출, 질문 답변, 요약, 번역, 텍스트 생성과 같은 작업을 위한 텍스트

- 이미지들로 된 이미지 분류, 객체 감지 및 세분화와 같은 작업들

- 오디오로 된 음성 인식 및 오디오 분류와 같은 작업들

- 또한 테이블 질문 응답, 광학 문자 인식, 스캔 문서에서 정보 추출, 비디오 분류 및 시각적 질문 응답과 같이 여러 작업을 결합하여 수행 가능

Transformers는 주어진 텍스트에서 사전 훈련된 모델을 빠르게 다운로드 및 사용하고, 자체 데이터에서 미세 조정한 다음, 모델 허브 의 커뮤니티와 공유할 수 있는 API를 제공합니다 .

2. Huggingface 모델

https://huggingface.co/models

HuggingFace는 다양한 Transformer 모델들이 배포되어 있습니다. 여러분의 목적을 위한 모델을 찾고 자신의 코드에 적용해 보는 것이 쉽고 간편하게 되어있어요.

Tasks, 라이브러리, 데이터세트 종류, 국가언어등 다양한 조건으로 찾아볼 수 있으며 찾은 모델의 이름을 통해 아래와 같이 자신의 코드에 모델을 쉽게 불러올 수 있습니다.

from transformers import AutoTokenizer, AutoModel

model = AutoModel.from_pretrained("bert-base-cased")

tokenizer = AutoTokenizer.from_pretrained("bert-base-cased")

AutoConfig를 통해 모델의 구성을 불러올 수 있으며 다양한 모델들의 구성을 불러와 설정할 수 있습니다.

from transformers import AutoConfig

# huggingface.co 와 cache에서 모델 구성 다운로드

config = AutoConfig.from_pretrained("bert-base-uncased")

# 해당 경로에 있는 모델 구성 파일 불러오기

config = AutoConfig.frompretrained("./test/bertsavedmodel/myconfiguration.json")

# 학습된 모델의 구성의 설정 수정하기

config, unusedkwargs = AutoConfig.frompretrained("bert-base-uncased", outputattentions=True, foo=False, returnunused_kwargs=True)

print(config.output_attentions) # True

print(unused_kwargs) # {'foo': False}

그외 Tokenizer, 사전학습을 위한 모델 API, 특정 task를 위한 모델 API와 같은 다양한 기능들을 제공하니 아래 링크에서 튜토리얼을 확인해보세요!

https://huggingface.co/docs/transformers/model_doc/auto

3. Huggingface 데이터

[Hugging Face – The AI community building the future.](https://huggingface.co/datasets)

HuggingFace는 여러 작업들을 위한 데이터들이 배포되어 있습니다. 자연어, 오디오, 이미지 등 다양한 데이터들과 모델을 평가하기 위한 벤치마크 데이터들도 제공하니 자신의 모델을 쉽게 평가할 수 있어요!

다양한 조건으로 원하는 모델을 찾을 수 있고 다른 사람이 많이 찾는 데이터나 최신 데이터를 찾아 자신의 코드에 적용하기 쉽게 되어있습니다.

또한 데이터를 선택하면 어떤 모델들이 사용을 해보았는지, 어떤 구조인지, 어떻게 사용하는지 등의 정보가 보기 좋게 정리되어 빠르게 데이터를 파악하고 활용할 수 있습니다.

![](https://lh3.googleusercontent.com/zpdzBcVO0FmPrRXYmA3W8Fau0BsVWFv0qr8MDwLLkDmTUIpKJ3y8BaLdDBwV0oHwHk2X9nmXamMbdVUwE2N7JOUviCo1sj9PmXTm75b5SyYx2kQg2pwDVTRqCjGJouevzTEQaSU2yoI5bMj7jY4-x90)

그리고 데이터 또한 모델처럼 간편하게 불러올 수 있어요. loaddatasetbuilder를 통해 데이터에 대한 설명과 구조를 볼 수 있으며 load_dataset로 데이터를 불러와 여러분의 코드에 활용할 수 있습니다.

from datasets import load_dataset_builder

dsbuilder = loaddatasetbuilder("rottentomatoes")

# 데이터의 설명

ds_builder.info.description

# 데이터의 특징

ds_builder.info.features

# {'label': ClassLabel(num_classes=2, names=['neg', 'pos'], id=None), 'text': Value(dtype='string', id=None)}

from datasets import load_dataset

dataset = load_dataset("rottentomatoes")

'''

DatasetDict({

    train: Dataset({

        features: ['text', 'label'],

        num_rows: 8530

    })

    validation: Dataset({

        features: ['text', 'label'],

        num_rows: 1066

    })

    test: Dataset({

        features: ['text', 'label'],

        num_rows: 1066

    })

})

'''

dataset = loaddataset("rottentomatoes", split="train")

'''

Dataset({

    features: ['text', 'label'],

    num_rows: 8530

})

'''

아래 링크를 통해 더 다양한 기능을 확인할 수 있습니다. 더 자세히 알고 싶으면 튜토리얼을 진행해보세요.

[Overview](https://huggingface.co/docs/datasets/tutorial)

지금까지 Huggingface에 대해 알아보았습니다. Huggingface는 커뮤니티 및 Data Science 플랫폼으로 모델과 데이터 및 다양한 기능을 제공하는데요. 대표적으로 모델들을 찾아 사용하는 방법과 데이터를 활용하는 방법에 대해 이야기 했습니다. 여러분의 코드에 맞는 데이터을 찾아 적용하거나 다양한 모델들을 통해 성능 개선을 해보면 좋을 것 같습니다.

**