### 악플 분류기

(실전 빅데이터 분석 프로젝트, 2022-05-30 ~ 2022-06-16)

#### 주제

: 입력되는 댓글의 악플 유무 및 종류를 판별하는 모델을 개발하여 악플 입력을 선제적으로 차단하는 서비스 개발



#### 프로젝트 수행

- 수행방법
    Smilegate AI에서 제공하는 한국어 혐오표현 ‘Unsmile’ 데이터셋
    + 악플 유/무만 구분되어 있는 데이터셋을 라벨링해서 추가

    - 기존 Smilegate 데이터셋은 여성/가족, 남성, 성소수자, 인종/국적, 연령, 지역, 종교, 기타혐오, 악플/욕설, 개인지칭, clean 라벨링
    - 개인지칭의 경우 판별 기준이 애매하다고 판단, 최종적으로 제외하기로 결정
    
    - 추가된 데이터셋에는 예시로 ‘10년차 방탄팬인데 방탄처럼 성공은 못 하겠다’ 처럼 분쟁을 유발하는 새로운 유형의 라벨 존재
        - 분쟁유발 라벨을 추가하여 총 11개로 라벨링

- 도구
    - Okt, Mecab 형태소 분석기
    - Colab Pro
    - Github
    - hanspell(Python 한국어 맞춤법 검사기), pykospacing etc...
    - Flask
    
- 사용 모델
  
    - GRU 
    - LSTM
    - BiLSTM
    - Transformer etc...

#### 역할
- 고은혜 – 데이터 라벨링 및 모델 개발, 기획안 발표 
- 원동찬 – 데이터 라벨링 및 모델 개발, Flask 개발
- 윤민영 – 데이터 라벨링 및 모델 개발, 최종 발표 
- 정태완 – 데이터 라벨링 및 모델 개발, Github 관리 

#### 프로젝트 진행 과정
- 1, 데이터셋 수집
	- smilegate ai 센터에서 공개한 한국어 혐오표현 UnSmile dataset
	- Kaggle Korean News Comments dataset
	- Korean HateSpeech Dataset
	
- 2, 데이터셋 라벨링
    - UnSmile dataset label + 분쟁유발 label
	
- 3, 데이터 전처리
	- null값 제거, 한국어를 제외한 문자 치환(이모티콘, 영어 등 제외)
	
	- 데이터 불균형 분포 처리(Undersampling)
	
	- 데이터셋 3가지로 확장
        - hanspell을 활용한 맞춤법 검사 및 변환 데이터
            - pykospacing을 활용한 띄어쓰기 검사 및 변환 데이터
            - 맞춤법과 띄어쓰기 검사 및 변환을 거치지 않은 데이터

	- Mecab 활용, 형태소 분석
	- Tokenzier 활용, 데이터 토큰화
	- Sequence padding
	
- 3, 학습 내용을 바탕으로 모델 생성(GRU, LSTM, RNN 등)

- 4, 모델 추가 생성(BiLSTM, Attention, Transformer 등)

- 5, 학습 모델 정확도 비교 및 최종 모델 선정(BiLSTM+LSTM 모델)
	-  1위 BiLSTM+LSTM: 0.71
	-  2위 Conv1D+LSTM: 0.67
	-  3위 BiLSTM: 0.64
	-  4위 Conv1D+BiLSTM: 0.53

- 6, Flask를 활용한 서비스 구현
	- 악플 유형 분류, 악플 선제 차단
