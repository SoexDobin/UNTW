# Linear Regression
1. 선형회귀
2. 손실함수 Loss
3. 경사하강법
---

### - 학습방법
1. Supervised learning (지도학습)
  * Regression
  * Classification
2. Unsupervised learning (비지도 학습)
  * Clustering
  * Density estimation
  * Visualization 
3. Reinforcement learning (강화학습)
  * Credit assignment problem
---

### **지도학습 / Supervised learning 이란?**
* 입력 데이터로부터 출력 값을 예측
* 출력 값이 수치형이면 Regression (회귀)
* 출력 값이 범주형이면 Classification (분류)

### **지도학습 / Supervised learning 종류**
* Regression (회귀)
  - .ex) 공부시간에 대한 성적 데이터로 부터 예상 점수 예측(수치형)
* Classification (분류)
  - Binary classification .ex) 점수(수치형)가 아닌 Pass/Fail(범주형) 일 때
  - Multi-class classification 성적이 다수의 번주 학점 (A, B, C)등으로 나올 때
---

### **1차 선형 함수를 그리기 위한 변수**
* Feature: ML 모델의 입력 변수 / x
* Label: 예측하고자 하는 변수 / y
* Model: feature와 label의 관계, 예측label / y'
![image](https://user-images.githubusercontent.com/56966606/195992943-ec3d8406-8ca8-46d8-8739-a327923d244f.png)
* Weight: 가중치라 하며 함수의 기울기 / w
* Bias: 절편이라 하며 편향 값을 보여줌 / b
![image](https://user-images.githubusercontent.com/56966606/195993129-0235c5b5-67e5-4fde-8efc-f5a58c65b26b.png)
---

### **손실 Loss**
- 모델 파라미터 w, b를 구하기 위한 평가의 척도
- 모델 예측이 맞으면 작아지고, 틀리면 커지는 penalty값
- 타겟 값 y와 예측 값 y'의 오차
  * Mean Absolute Error (MAE) : 평균절대오차
  * Mean Squared Error (MSE) : 평균제곱오차
![image](https://user-images.githubusercontent.com/56966606/195994138-d4167ab6-1d39-4e48-b8d1-1641b4e057c4.png)

### **손실 함수 Loss Function**
* 선형회귀에서는 평균제곱오차(MSE)를 손실함수로 많이 사용
* Model Training : 입력 데이터로 부터손실을 최소화하는 w, b 파라미터를
구하는(학습하는) 것
---

* 최적화
  - 수학, 경제학, 컴퓨터과학 등 여러 분야에서 사용
  - 선형계획법, 비선형계획법, 동적계획법, 확률계획법, 경사하강법 등

## **최적화 이론에서의 손실함수 4가지 명칭**
* Loss function (손실 함수) 
* Error function (오차 함수) 
* Cost function (비용 함수) 
* Objective function (목적 함수) 

### **경사하강법 알고리즘 : 대표적인 최적화 알고리즘**
* Iteration 방법으로 최적값(손실함수를 최소화 하는 값) 계산
* 데이터 양이 큰 경우 매우 효율적
* 손실함수가 최소가 되는 지점(미분계수가 0) 기울기가 최소여야 최적화가 잘된 것
![image](https://user-images.githubusercontent.com/56966606/195994846-33a7c19c-d212-4eba-ba2a-3b6a8e338f90.png)
* 기울기가 양수이면 왼쪽으로 이동, 기울기가 음수이면 오른쪽으로 이동
* 손실을 줄이는 방향으로 가중치를 업데이트
---

### 모델 정의
```python
model = Squential(Dense[1, input_shape=(1, ), activation=''])
model = Squential(Dense[노드 개수, output y 개수, 활성화함수])
```
**활성화 함수 종류**
- linear : 데이터의 관계가 서로 직선 형태를 띠는 일자선 함수
- sigmod : 실함수로써 유계이고 미분가능하며, 모든 점에서 음이 아닌 미분값을 가지고 단 하나의 변곡점을 가진다. S선 함수
- softmax : 세 개 이상으로 분류하는 다중 클래스 분류에서 사용되는 출력은 0~1 사이의 실수인 곡선 함수

### 모델 컴파일
```python
model.compile(optimizer='', loss='', metrics='')
model.compile(최적화 알고리즘, 손실함수, 평가지표)
```
**최적화 알고리즘**
- sgd : 경사 하강법중에서도 Stochastic Gradient Descent 임의의 하나의 데이터에 대해서 에러를 구한 뒤 기울기를 계산하여, 모델의 parameter 를 업데이트 하는 방법
- adam : Adaptive Moment Estimation

**손실 함수**
- mean_squared_error : 오차값이 작을수록  정답에 가깝다.
- binary_crossentropy : 머신 러닝 분류 모델의 발견된 확률 분포와 예측 분포 사이의 차이를 측정합니다. Loss(또는 Error)는 0은 완벽한 모델로 0과 1 사이의 숫자로 측정됩니다. 일반적인 목표는 모델을 가능한 0에 가깝게 만드는 것입니다.
- categorical_crossentropy : 클래스가 3개 이상인 멀티클래스 분류에 사용됩니다. 출력된 벡터는 각 클래스에 속할 확률이 나오며, 총합은 1이다.

### 모델 트레이닝
```python
model.fit(x, y, epochs=n, verbose=0~2)
model.fit(feature, label, 최적화 회수, 콘솔 출력 타입)
```
* epochs : 데이터들이 한 번씩 모델을 통과한 횟수

### 모델 검증
**훈련 마친 모델 지표계산 함수 evaluate()**
```python
model.evaluate(x, y)
model.evaluate(feature, label)
```
**훈련 마친 모델 가중치, 편향 값 산출 변수 weights**
```python
w, b = model.weights
print(w.numpy(), b.numpy())
```

###모델 예측
```python
model.predict([x'])
model.predict([feature'])
```

### **성적 모델**
```python
import numpy as np
import tensorflow as tf
import matplotlib.pyplot as plt # 지표를 시각적으로 보기위해
from tensorflow import keras 
from keras import Sequential # 모델 정의에 사용
from keras.layers import Dense # 신경망 모델 구성을 위한 layer


# 성적 데이터와 시간 값
xTime = np.array([2.0, 3.0, 9.0, 10.0], dtype=float)
yScore = np.array([30.0, 50.0, 80.0, 90.0], dtype=float)

# 모델 정의
model = Sequential([Dense(1, input_shape=(1, ), activation='linear')])

# 모델 컴파일
model.compile(optimizer='sgd', loss='mean_squared_error')

# 모델 트레이닝
model.fit(xTime, yScore, epochs=500, verbose=1)

#모델 검증 / 훈련결과
model.evaluate(xTime, yScore)
# Evaluation 모델 훈련을 마친 상태의 weight를 적용하여 평가지표 계산
# 검증을 위해서는 별도의 검증 데이터 셋 필요
w, b = model.weights
print(w.numpy(), b.numpy())

#모델 예측
print(model.predict([6]))
```
---

### **Binary classification**
* Logistic function = Sigmoid function
![image](https://user-images.githubusercontent.com/56966606/196001386-371ee397-2124-4628-8f25-c6aa38f6fa6a.png)
* Probability : x가 C1, C2 일 확률
* Odds(승산) : 실패 비율 대비 성공 비율
* Logit : Odds의 자연로그
```python
# 활성화 함수 sigmoid 사용
model = Sequential([Dense(1, input_shape=(1,), activation='sigmoid')])
```

### Logistic Regression
* Logistic Regression → Binary Classification
* 예측 값이 0.5보다 크면 C1 작으면 C2로 분류
```python
# 손실함수 : loss='binary_crossentropy'
# 매트릭스 : metrics=['accuracy']
model.compile(optimizer='sgd', loss='binary_crossentropy', metrics=['accuracy'])
```

### 분류 문제 평가 지표 metrics
* Accuracy (정확도) 
  - 클래스가 불균형 분포이면 왜곡될 수 있음
* Precision (정밀도) 
  - Positive로 예측한 경우 실제 positive인 비율 (예측값이 얼마나 정확한가)
  - 예) 스팸메일 여부 판단할 때는 정밀도가 중요
* Recall (재현율) 
  - 실제 positive 인 것 중 올바르게 positive를 맞춘 비율(실제 정답을 얼마나 맞췄는가)
  - 예) 암검사에서 실제 암인데 아니라고 판단하면 위험하므로 재현율이 중요
* F1-Score
  - Precision과 recall의 조화 평균
  - 주로 분류 클래스 간의 데이터가 불균형이 심각할 때 사용


### Logistic Function
* 가중치 값에 따른 그래프 변화
![image](https://user-images.githubusercontent.com/56966606/196001527-fc79ba19-0e68-4fda-8540-7376237adf81.png)
---

```python
import numpy as np
import tensorflow as tf
import matplotlib.pyplot as plt # 지표를 시각적으로 보기위해
from tensorflow import keras 
from keras import Sequential # 모델 정의에 사용
from keras.layers import Dense # 신경망 모델 구성을 위한 layer

xTime = np.array([1.0, 2.0, 4.0, 10.0, 12.0], dtype=float)
yPass = np.array([0.0, 0.0, 0.0, 1.0, 1.0], dtype=float)

model = Sequential([Dense(1, input_shape=(1, ), activation='sigmoid')])

model.compile(optimizer='sgd', loss='binary_crossentropy', metrics=['accuracy'])
model.fit(xTime, yPass, epochs=500, verbose=0)

w, b = model.weights
print(w.numpy(), b.numpy())

print(model.predict([4]))
```

### **Multi-Class classification**
* 이진 분류를 n번 수행하여 예측 값 벡터 y 계산

### 확률 값으로 변환하기 위해 Softmax 함수
* 지수함수는 단조 증가함수로 대소 관계가 변하지 않는다
* 지수함수를 적용하면 작은 값의 차이가 커져서 구분이 용이해 진다
* 지수함수의 미분은 원래 값과 동일하기 때문에 미분하기 좋다
```python
model = Sequential([
Dense(10, activation='relu', input_shape=(4,)),
Dense(10, activation='relu'),
Dense(3, activation='softmax'),
])

model.compile(optimizer='adam', loss='categorical_crossentropy’, metrics=['acc'])
model.fit(x_train, y_train, validation_data=(x_test, y_test),epochs=400, verbose=0)
model.evaluate(x_test, y_test, verbose=2)
```

## Linear Regression & Binary Classification & Multi-Class Classification 코드 비교
```python
model = Sequential(Dense[1, input_shape=(1, ), activation='linear'])
model = Sequential(Dense[1, input_shape=(1, ), activation='sigmoid'])
model = Sequential(Dense[1, input_shape=(1, ), activation='softmax'])

model.compile(optimizer='sgd', loss='mse')
model.compile(optimizer='sgd', loss='binary_crossentropy', metrics=['acc'])
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['acc'])

model.fit(x, y, epoch=500, verbose=0)
model.evaluate(x, y)
w, b = model,weights
print(w.numpy(), b.numpy())

model.predict([x])
```

