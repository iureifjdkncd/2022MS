## 🏆 Contest

### 제10회 산업통상자원부 공공데이터 활용 BI 공모전 최우수상 (KOTRA 사장상 수상)

- 📊과제명: **한국 수출금액 예측 모델 기반 기업수요 맞춤형 서비스**
- 작성 기간: 2022.05 ~ 2022.08
- 기술 스택: Python, Statsmodels, Scikit-Learn, TensorFlow, Excel, Tableau
- 수상 링크: [Link](https://www.datacontest.kr/board/view/97533073/3694)
---
### 🎯 성과 요약

- 한국의 수출금액을 예측하기 위해 **VECM(벡터오차수정모형)**과 **Monte Carlo Dropout 기반 LSTM Seq2Seq** 모델을 병행 적용하여, 최대 97.1%의 예측 정확도를 달성

- **통계 기반 신뢰구간**과 **딥러닝 기반 확률적 예측** 시나리오를 결합함으로써 정확도 향상, 불확실성 해석 가능성 확보, 비즈니스 적용성 강화의 세 요소를 모두 만족하는 하이브리드 예측 시스템 구축

- 예측 결과를 기반으로 품목 추천 로직도 함께 설계하여, 실질적인 기업 맞춤형 서비스로의 확장 가능성도 제시
---

### 📂 디렉토리 구성
- `1.) ARIMA.ipynb – 단변량 시계열 예측 (ARIMA 기반)
- `2.) Vector Error Correction.ipynb – 다변량 시계열 예측 (VECM 기반)
- `3.) LSTM_Seq2Seq.ipynb – 딥러닝 기반 다변량 예측 (Monte Carlo Dropout 포함)
---

### 🎯 문제 정의

- **목표**: 2022.01 ~ 2022.06 기간의 한국 수출금액 예측
- **접근법**: 전통 통계 모델과 딥러닝 기반 확률 예측 모델을 병행 적용하여, **정확도 향상**과 **불확실성 해석 가능성**을 동시에 확보
---

### 🧹 주요 전처리

- 1.) **2000.01 ~ 2021.12** 기간의 월별 수출금액 및 관련 경제·무역 지표 수집
- 2.) 전체 데이터를 기반으로 학습 후, **2022.01 ~ 2022.06** 기간을 Test Data로 분리


---
### 🧠 학습 프로세스 1 : 통계 기반 Multi-Horizon Forecasting

  - 1.) ARIMA & Holt-Winters: 단변량 기반 기본 예측

  - 2.) VECM

    - ADF 검정을 통한 정상성 확보 및 변수 선택

    - Johansen 검정 및 AIC 기반 최적 공적분 차수 설정

    - Granger 인과성 분석 및 충격 반응 분석(Impulse Response Analysis)을 통한 인사이트 도출

--- 

### 🧠 학습 프로세스 2 : 딥러닝 기반 Multi-Horizon Forecasting

  - 1.) LSTM Seq2Seq(Encoder-Decoder) 모델:

    - 1970년부터의 추가 수집한 일부 장기 다변량 데이터를 기반으로 학습

    - 수출금액의 **Residual 요소**를 추가 입력으로 활용하여 예측 성능 향상

    - **Monte Carlo Dropout** 기반 불확실성 추정 수행 (N=30 반복 생성)

  - 2.) Gradient 기반 기여도 분석:

    - Gradient Tape를 활용한 입력 변수 중요도 분석
    - Linear 모델 해석(Y = Ax) 기반 변수 영향도 정량화

    
---

### 🔍 추론 및 해석 

   - 1.) 통계 기반 예측 결과 

     - ARIMA, Holt-Winters, VECM의 **점추정값** 제시
     - VECM 기반 **Prediction Interval** 제공

        <img width="493" height="270" alt="다운로드" src="https://github.com/user-attachments/assets/f577f59c-58c9-45bc-92cd-f4736a929303" />

        <img width="498" height="270" alt="다운로드 (1)" src="https://github.com/user-attachments/assets/6064dc37-79d0-4c07-9a82-8b494824651f" />


   - 2.) 딥러닝 기반 예측 결과 

     - MCD 기반 예측 결과로부터 **N=30개의 확률 분포 시나리오** 생성
     - MCD모델의 Gradient Tape기반 변수 중요도 해석
     - 통계모델 평균 점추정값을 **벤치마크**로 설정하고, 해당 벤치마크와 가장 가까운 MCD예측 시나리오를 선택 

        <img width="708" height="274" alt="다운로드 (2)" src="https://github.com/user-attachments/assets/b5ef7eb5-b3da-489d-b571-09124adbc481" />

       

        <img width="493" height="270" alt="다운로드 (3)" src="https://github.com/user-attachments/assets/d5aa4a71-7aa2-4c17-a9d3-f9d44ef34a32" />

         <img width="445" height="396" alt="다운로드 (4)" src="https://github.com/user-attachments/assets/1cec0708-839f-4802-a678-724250a55209" />


   - 3.) 결합 추론 전략

     - **점추정**은 VECM과 MCD-LSTM의 상호보완을 통해 안정성 확보 

     - **불확실성 구간**은 VECM 기반 Prediction Interval을 기준으로 정의 

        <img width="544" height="290" alt="화면 캡처 2025-08-04 151209" src="https://github.com/user-attachments/assets/da83d847-dd74-49df-bd22-a01e0631055a" />



---

### 🧭 BI 활용 방안

  - 수출 품목별 예측 구간 제공을 통해 기업 맞춤형 수출 전략 수립 지원
  - 예측값 기반 품목 추천 시스템 구현 가능성 제시

      <img width="739" height="284" alt="화면 캡처 2025-08-04 150728" src="https://github.com/user-attachments/assets/a17c4b4c-f834-4463-a39d-399df86368ba" />

---


#### 📑 관련 논문 [Link](https://www.dbpia.co.kr/Journal/articleDetail?nodeId=NODE11207563)

  - 논문명: 다변량 시계열 예측을 활용한 수출금액 예측에 관한 연구
  - 게재처: 한국지능정보시스템학회

---
