# Predicting MBTI for Internet Users

한국통계학회 포스터 논문 발표 프로젝트입니다. 인터넷 사용자가 남긴 텍스트 데이터를 기반으로 별도의 MBTI 검사 없이 MBTI 유형을 예측하는 문제를 다룹니다.

![image](https://user-images.githubusercontent.com/73769046/181724820-38aedc57-d199-40b6-a83a-436131c2899e.png)

## Overview

기존 MBTI 예측 접근은 `E-I`, `S-N`, `T-F`, `J-P`의 4가지 지표를 각각 독립적인 binary classification 문제로 나누는 경우가 많습니다. 하지만 MBTI 유형은 네 지표의 단순한 독립 조합이라기보다, 데이터상에서 특정 조합이 더 자주 나타나는 상관 구조를 가질 수 있습니다.

본 프로젝트는 4개 지표를 따로 예측하는 방식이 유형 간 상관 정보를 손실할 수 있다는 문제의식에서 출발했습니다. 이에 따라 16개 MBTI 유형 전체를 하나의 multi-class classification 문제로 다루고, 여러 모델의 성능을 비교했습니다.

## Repository Contents

| File | Description |
|---|---|
| [`predicting.ipynb`](./predicting.ipynb) | Main prediction workflow |
| [`kaggle.SVM.tuning.ipynb`](./kaggle.SVM.tuning.ipynb) | SVM hyperparameter tuning experiment |
| [`othermodelCV.ipynb`](./othermodelCV.ipynb) | Cross-validation experiments for other models |
| [`Vis.ipynb`](./Vis.ipynb) | Visualization and exploratory analysis |
| [`tf.ipynb`](./tf.ipynb) | Text feature processing experiments |
| [`DQN_Tutorial (1).ipynb`](./DQN_Tutorial%20(1).ipynb) | DQN-based optimization reference/experiment |
| [`포스터_고경수.pdf`](./%ED%8F%AC%EC%8A%A4%ED%84%B0_%EA%B3%A0%EA%B2%BD%EC%88%98.pdf) | Poster paper file |

## Method

### 1. 16-class MBTI classification

Instead of training four independent binary classifiers for `E-I`, `S-N`, `T-F`, and `J-P`, the project formulates MBTI prediction as a single 16-class classification problem.

This formulation aims to preserve relationships among MBTI dimensions, such as patterns where certain dimensions co-occur more frequently in the data.

### 2. Text feature representation

The input text is transformed into numerical features for machine learning models. TF-IDF-style sparse text representation is used as the main feature representation for linear classifiers.

### 3. Model comparison

Several machine learning models were compared for MBTI text classification.

| Model | Accuracy |
|---|---:|
| SVM | 84.41% |
| Logistic Regression | 83.83% |
| Random Forest | 48.71% |

SVM achieved the best performance among the compared models.

### 4. Hyperparameter optimization

The SVM regularization parameter `C` was tuned because it strongly affects the decision boundary and generalization performance.

This project explored an intelligent optimization approach that combines:

- Grid search for broad-range exploration
- DQN-based reinforcement learning for finer search around promising regions

The best reported setting was:

- `C = 0.246`
- Final accuracy: 84.88%

## Results

- Proposed a 16-class MBTI classification approach to reduce information loss from independent binary classification.
- Compared SVM, Logistic Regression, and Random Forest models.
- Achieved the best performance with SVM.
- Improved SVM performance through hyperparameter tuning.
- Presented the project as a poster paper at the Korean Statistical Society.

## Key Takeaways

- Problem formulation matters: treating MBTI as 16 classes can preserve type-level correlations better than independently predicting four dimensions.
- Linear models such as SVM and Logistic Regression are strong baselines for sparse text classification.
- Accuracy alone may not fully explain model behavior when class imbalance exists; macro-F1, weighted-F1, class-wise recall, and confusion matrix analysis can further strengthen evaluation.
- MBTI prediction from text should be interpreted as text-pattern-based type estimation, not as a replacement for formal psychological assessment.

## Related Repository

- Dataton competition version: <https://github.com/ksko0424/Dataton_Competition_2022>
