

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