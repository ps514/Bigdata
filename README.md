# [과제3] 특성 공학(Feature Engineering) 파이프라인 — Titanic

Kaggle Titanic 데이터로 결측치 처리, 인코딩, 스케일링, 파생 변수, 변수 선택 전략에 따른 분류 성능 차이를 비교합니다.

## 실행 방법
1. https://www.kaggle.com/competitions/titanic/data 에서 `train.csv`를 받아 `data/` 폴더에 넣습니다.
2. 라이브러리를 설치합니다: `pip install -r requirements.txt`
3. `titanic_feature_engineering.ipynb`를 열고 전체 실행합니다 (약 3~5분).

## 폴더 구조
```
├─ titanic_feature_engineering.ipynb   # 전체 파이프라인 (EDA → 특성 공학 → 변수 선택 → 모델 평가)
├─ requirements.txt
├─ results_main.csv                    # 실행 시 생성: 실험 비교표
└─ data/train.csv                      # Kaggle에서 직접 다운로드
```

## 실험 구성
| 실험 | 결측치 처리 | 인코딩 | 스케일링 | Feature Selection |
|---|---|---|---|---|
| Base | 없음 | 없음 | 없음 | 없음 |
| Exp-1 | Mean | One-Hot | Standard | X |
| Exp-2 | Median | Label | MinMax | O (RF 상위 10개) |
| Exp-3 | Most Frequent | One-Hot | Robust | O (RF 상위 10개) |

모델: Logistic Regression, Random Forest, XGBoost, LightGBM
평가: Stratified 5-Fold CV — Accuracy, Precision, Recall, F1, ROC-AUC
재현성: 모든 난수 시드 `SEED = 42` 고정, 전처리는 sklearn Pipeline 안에서 fold별로 fit
