
# 파이썬
```python
# list
a = [1,2,3,4,5]
len(a) # 5
a[4] = 99
print(a) # [1,2,3,4,99]

nums = list(range(5))
print(nums[2:4]) # [2, 3]
print(nums[2:]) # [2, 3, 4]
print(nums[:2]) # [0, 1]
print(nums[:]) # [0, 1, 2, 3, 4]
print(nums[:-1]) # [0, 1, 2, 3]

# dictionary
me = {'height':180} # me['height] = 180
me['weight'] = 70
print(me) # {'height:180', 'weight':70}

# for
for i in [1,2,3]:
print(i) # 1 2 3

# 함수
def hello(object):
  print(“Hello ”+object+“!”)

# 클래스
class Man:
  def__init__(self, name):
    self.name = name
    print("초기화!")
  def hello(self):
    print("Hello "+self.name+"!")
  def goodbye(self):
    print("Goodbye"+self.name+"!")

m = Man("David")
m.hello() # Hello David!
m.goodbye() # Goodbye David!

# numpy array
b = np.array([[1,2],[3,4],[5,6]])
print(b.ndim) # 3
print(b.shape) # (3, 4)

print(b[:,-1]) # [2 4 6]
print(b[-1]) # [5, 6]
print(b[-1,:]) # [5, 6]
print(b[-1,...]) # [5, 6]
print(b[0:2,:]) # [[1,2] [3,4]]
```

**reshape!**

![image](https://user-images.githubusercontent.com/56966606/206397542-86422059-1760-4b3f-9fd6-4a5dc7389152.png)   


# 파이썬 모듈

<br>

* Numpy : 과학 계산을 위한 모듈
```python
import numpy as np
```
* Pandas : 데이터 분석을 할 때 가장 많이 쓰이는 모듈
```python
import pandas as pd
```
* Matplotlib : 데이터 시각화를 위한 모듈
```python
import matplotlib.pyplot as plt
```
* Seaborn : 통계 시각화를 위한 모듈
```python
import seaborn as sns
```
* Random : 난수 생성 관련 모듈
```python
import random
```
---

**TensorFlow**
- 행렬로 표현할 수 있는 2차원 형태의 배열을 높은 차원으로 확장한 다차원 배열이다.
**Keras**
- Sequential : 순차적 API 모델은 가장 단순한 모델이며 선형 파일(pile) 계층으로 구성되어 대부분 문제점에 계층별(layer-by-layer)로 모델을 구성할 수 있다.
**Scalar**
- 스칼라(scalar)는 방향을 갖지 않고 크기만 갖는 개념이다.
**Vector**
- 벡터(vector)는 크기와 방향을 갖는 개념이다
**Matrix**
- 행렬로써 수 또는 다항식 등을 직사각형 모양으로 배열한 것이다.

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

### 모델 예측
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


## 뉴럴 모델을 통한 hidden layer 활용
- 입력층(input_shape)과 출력층(output_shape) 사이에 넣어준다.
- 이전 층의 가중합으로 새로운 특성을 만들어 낸다.
- 입력 특성으로부터 새로운 특성들이 만들어 지면서 모델이 더 상세한 정보를 학습한다.
- but 너무 많은 hidden layer 사용 시 신경망의 층이 깊어지면 gradient가 0이 되어 backpropagation이잘 작동하지 않는다. > 고로 경사 소실 문제가 발생한다.

<br>

### Activation함수 relu 함수
- 양수 구간의 미분은 1, 음수 구간은 0으로 계산할 필요가 없음
- sigmoid의 – 함수의 양끝에서 미분값이 0이 되는 Gradient 포화가 발생하여 학습 중단하듯 hidden layer을 사용할때 적절한 함수로서 사용한다.

![image](https://user-images.githubusercontent.com/56966606/205503882-815936bc-50e7-4666-b088-f098e9c14c7b.png)

<br>

### Flattern 
- 3차원배열을 1차원 배열로 바꿔준다.

![image](https://user-images.githubusercontent.com/56966606/205503901-b7a1bb66-e481-46c7-a51e-523fff9349d2.png)

**손실함수 sparse_categorical_crossentropy**
- categorical_crossentropy와 같이 다중 클래스 분류시 사용한다.
= sparse는 훈련데이터 값 label이 w정수형일때 사용한다.

**CNN 활용해보기**
```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow
from tensorflow import keras
from keras import Sequential
from keras.layers import Flatten, Dense

mnist = keras.datasets.mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train/255.0, x_test/255.0

# Flatten : 3차원 1차원 배열로 바꿔줌
model = Sequential([
    Flatten(input_shape=(28, 28)),
    Dense(128, activation='relu'),
    Dense(10, activation='softmax')
])
model.summary()

model.compile(optimizer='Adam',
    loss='sparse_categorical_crossentropy',
    metrics=['acc']  
)
history = model.fit(x_train, y_train, validation_data=(x_test, y_test), epochs=10, verbose=0)

loss = history.history['loss']
val_loss = history.history['val_loss']
epochs = range(1, len(loss)+1)
plt.plot(epochs,loss)
plt.plot(epochs,val_loss)
plt.xlabel('Epoch', fontsize=14)
plt.ylabel('Loss', fontsize=14)
plt.show()

acc = history.history['acc']
val_acc = history.history['val_acc']
plt.plot(epochs,acc)
plt.plot(epochs,val_acc)
plt.xlabel('Epoch', fontsize=14)
plt.ylabel('Accuracy', fontsize=14)
plt.show()
```

![image](https://user-images.githubusercontent.com/56966606/206403157-b88c9063-2ab4-4f26-b69c-922ad2daba50.png)



### Convolution 연산과 사용하는 요소
- 여러 개의 필터를 사용하여 입력 이미지의 다른 특성을 학습
- 정방형 filter(kernel)을 사용하여 이미지의 특징을 추출

**Stride** : 컨벌루션 연산시 filter가 이동하는 간격
- Stride를 2로 설정하면 특성맵의 크기가 반으로 줄어든다

![image](https://user-images.githubusercontent.com/56966606/205573409-029bf131-8a7d-495c-a7ea-cfef151d8895.png)

**Padding** : • 컨벌루션 신경망을 원하는 대로 깊게 만들기 위해 특성맵이 줄어들지 않도록 padding을 사용

![image](https://user-images.githubusercontent.com/56966606/205573485-19c04e5f-ad5a-4648-9b39-01720cabb54b.png)

**Pooling 연산**
- Max pooling과 Average pooling이 있다.
- 풀링 필터는 학습을 하지 않으며 채널수는 유지됨

#### Convolution 연산의 성질
- 희소 연결(sparse connectivity) 성질
- 파라미터 공유(parameter sharing) 성질
- 이동등변성(Translation equivariance)

#### Pooling 연산의 성질
- 위치불변성(Translation invariance) 
  + 입력이 작게 이동했을 때 맥스 풀링의 결과는 동일
  + 따라서 입력의 위치가 바뀌어도 같은 결과로 인식
  + 강아지 사진의 강아지 위치가 어느 위치에 있건 상관없이 강아지로 출력

![image](https://user-images.githubusercontent.com/56966606/205576141-128992cc-b2a4-4ea7-be4d-7a49ec8c7c02.png)


```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
from tensorflow import keras
from keras.models import Sequential
from keras.layers import Flatten, Dense, Conv2D, MaxPooling2D

mnist = keras.datasets.mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()

# 정규화 (Normalization)
x_train, x_test = x_train/255.0, x_test/255.0
# Convolution layer에 적용하기 위해 이미지 데이터에 채널 추가(Reshape)
x_train = x_train.reshape(60000, 28, 28, 1)
x_test = x_test.reshape(10000, 28, 28, 1)

model = Sequential([
  Conv2D(32, (3,3), activation='relu', input_shape(28, 28, 1)),
  MaxPooling(2, 2),
  Flatten(),
  Dense(128, activation='relu'),
  Dense(128, activation='relu'),
  Dense(10, activation='softmax'),
])

model.compile(optimizer='Adam', loss='sparse_categorical_crossentropy', metrics=['acc'])
histroy = model.fit(x_train, y_train, validation_data=(x_test, y_test), epochs=100)

loss = history.history['loss']
val_loss = history.history['val_loss']
epochs = range(1,len(loss)+1)
plt.plot(epochs,loss)
plt.plot(epochs,val_loss)
plt.title ('Training and validation loss')
plt.show()
```

![image](https://user-images.githubusercontent.com/56966606/206414657-27b5eb53-3974-4ed4-863a-ace34c2d84d4.png)