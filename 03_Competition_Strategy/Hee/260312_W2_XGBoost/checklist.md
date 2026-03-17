# 📌 머신러닝 워크플로우 체크리스트: K-Fold 교차 검증 방식
> Train 데이터 안에서 스스로 모의고사를 반복하며 가장 단단한 모델을 찾는 실무/대회 표준 방식입니다.

## [ ] 1. 최초 데이터 분할 (Train / Test)
- [ ] 전체 데이터를 `train_test_split`으로 2분할 (예: 8:2 비율)
- [ ] **분류(Classification) 문제:** `stratify=y` 옵션을 주어 클래스 비율 유지
- [ ] **회귀(Regression) 문제:** `stratify` 옵션 없이 무작위로 분할
- [ ] 🔒 **주의:** 분리된 Test 데이터는 최종 평가 전까지 절대 열어보지 않고 따로 보관할 것

## [ ] 2. 교차 검증(CV) 객체 생성
- [ ] **분류 문제:** `StratifiedKFold` 객체 생성 (폴드마다 정답 클래스 비율 유지)
- [ ] **회귀 문제:** 일반 `KFold` 객체 생성

## [ ] 3. 하이퍼파라미터 튜닝 (`GridSearchCV` 또는 `RandomizedSearchCV`)
- [ ] 탐색할 파라미터 그물망(Grid)을 딕셔너리로 세팅 (예: `max_depth`, `learning_rate`)
- [ ] 탐색 객체에 '2번에서 만든 CV 객체'와 'Train 데이터 전체'를 넣어 학습 시작
- [ ] **분류 문제 평가 지표(`scoring`):** `accuracy`, `roc_auc`, `f1` 등
- [ ] **회귀 문제 평가 지표(`scoring`):** `neg_root_mean_squared_error`, `r2` 등

## [ ] 4. 최적 모델(Best Estimator) 추출 및 진단
- [ ] `.best_estimator_`를 호출하여 평균 점수가 가장 높은 1등 모델 추출
- [ ] (선택) `.cv_results_`를 확인하여 폴드별 점수 편차가 크지 않은지 데이터의 안정성(이상치 여부) 진단

## [ ] 5. 최종 검정 (Test)
- [ ] 1번 단계에서 보관해 두었던 Test 데이터 불러오기
- [ ] 4번에서 추출한 최적의 모델(`.best_estimator_`)로 Test 데이터를 예측
- [ ] 예측값과 실제 Test 정답을 비교하여 최종 성능(일반화 성능) 리포팅