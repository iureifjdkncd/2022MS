## 한국 수출금액 예측 모델 기반 기업수요 맞춤형 서비스

### 디렉토리 구조
- `1.) ARIMA.ipynb` 
- `2.) Vector Error Corretion.ipynb` 
- `3.) LSTM Seq2Seq.ipynb` 
---

### 문제 정의

- 1.) 2022.01 ~ 2022.06의 한국 수출금액 시계열 예측 
---

### 주요 전처리 
  - 1.) 월별 수출금액 외에 추가 경제 & 무역 데이터 수집 (2000.01 ~ 2021.12)

  - 2.) 통계 시계열 Vs 딥러닝 시계열 데이터 활용 및 전처리 차이 

  - 3.) 전체 데이터 학습 & 2022.01 ~ 2022.06 Test 정의 

---
### 학습 프로세스 1 --> 통계 시계열 Multi Horizon Forecast 

  - 1.) 단변량 ARIMA & HoltWinters 학습

  - 2.) 다변량 VECM 학습

       → ADF 검정 기반 변수선택

       → Johansen 공정분 검정 & AIC 기반 VECM 모델 구축

       → Granger 인과관계 & 충격반응분석에 의한 다각적 해석 제공 

--- 

### 학습 프로세스 2 --> 딥러닝 시계열 Multi Horizon Forecast

  - 1.) 다변량 LSTM Seq2Seq 적용

       → 기존 다변량 수집데이터 중 1970년부터 기록이 존재하는 데이터 일부 활용

       → 수출금액의 분해요소 중 Residual요소 추가 입력변수로 활용

       → 전체 데이터 MinMax Scaling 적용 & T+1 ~ T+6 Multi Horizon Forecast 문제 정의

       → Monte Carlo Dropout기반 확률적 추론모델 구축 (30개의 Multi Horizon Forecast 수행)

  - 2.) 모델 해석 추가 

       → Target(수출금액)에 대한 입력변수들의 Gradient Tape 계산 & Y=Ax모델에 대한 입력값들의 기울기 기반 가중치 나열

      <img width="445" height="396" alt="다운로드 (4)" src="https://github.com/user-attachments/assets/1cec0708-839f-4802-a678-724250a55209" />


---

### 추론 프로세스 

   - 1.) 통계시계열 예측 결과 

       → ARIMA,HoltWinters,VECM 점추정 예측결과 & VECM 기반 Prediction Interval 정의

        <img width="493" height="270" alt="다운로드" src="https://github.com/user-attachments/assets/f577f59c-58c9-45bc-92cd-f4736a929303" />

        <img width="498" height="270" alt="다운로드 (1)" src="https://github.com/user-attachments/assets/6064dc37-79d0-4c07-9a82-8b494824651f" />


   - 2.) 딥러닝 시계열 예측 결과 

        → 최초 N-30기반 Monte Carlo Dropout기반 추론 결과 정의 

        <img width="708" height="274" alt="다운로드 (2)" src="https://github.com/user-attachments/assets/b5ef7eb5-b3da-489d-b571-09124adbc481" />

        → 통계시계열 점추정 예측결과의 평균 움직임 벤치마크 정의 & 해당 벤치마크의 최근접 MCD예측결과 30개중 1 선택 

        <img width="493" height="270" alt="다운로드 (3)" src="https://github.com/user-attachments/assets/d5aa4a71-7aa2-4c17-a9d3-f9d44ef34a32" />


   - 3.) 추론 결합

        → 점추정은 VECM & Monte Carlo Dropout LSTM Seq2Seq 상호보완 

        → Prediction Interval은 VECM기반으로 정의 

        <img width="544" height="290" alt="화면 캡처 2025-08-04 151209" src="https://github.com/user-attachments/assets/da83d847-dd74-49df-bd22-a01e0631055a" />



---

### BI 활용방안 예시

  - 1.) 수출금액 품목별 예측구간 제공 

      <img width="739" height="284" alt="화면 캡처 2025-08-04 150728" src="https://github.com/user-attachments/assets/a17c4b4c-f834-4463-a39d-399df86368ba" />

---


#### 한국지능정보시스템학회 논문작성 링크 

  - 다변량 시계열 예측을 활용한 수출금액 예측에 관한 연구

   https://www.dbpia.co.kr/Journal/articleDetail?nodeId=NODE11207563

---
