# 1차시

```python
# 주석
ctrl + / # 전체 주석
```

## 파이썬 기초 문법
1. 키워드: 파이썬에서 특정 기능을 가진 단어
2. 식별자: 이름을 붙일때 사용
3. 함수, 변수: 소문자와 (_)언더바 기용 ex.)class_name
4. 클래스 : 대문자 기용

**자료형 기본**
```python
print("안녕하세요")
# 따옴표 출력
print(""안녕"이라고 말해") 
print("\"따옴표 출력\"")
# 줄바꿈
print("""가나다
마바사
아자차""")
print("ABC\nDEF\nGHI")
```
**자료형 선택연산자**
```python
print("안녕하세요"[0]) # 안
print("안녕하세요"[-1]) # 요
print("안녕하세요"[1:4]) # 녕하세요
```
**자료형 숫자 연산자**
```python
print("6+3= ", 6+3)
print("6-3= ", 6-3)
print("6*3= ", 6*3)
print("6/3= ", 6/3)
#나누기 결과를 정수로 표현
print("6//3= ", 6//3)
#거듭제곱
print("6**3= ", 6**3)
#나머지
print("7%3= ", 7%3)
```
**변수 생성**
```python
grade = 3
pi = 3.1415
```
**복합 대입연산자**
```python
#숫자
a += b # a = a + b
a -= b # a = a - b
a *= b # a = a * b
a /= b # a = a / b
a //= b # a = a // b
a **= b # a = a ** b
a %= b # a = a % b
#문자
a += b # a = a + b
a *= b # a = a * b
```

**자료형 확인 type 함수**
```python
print(type("hello"))
print(type(53))
print(type(True))
```
**문자열 길이 확인 len 함수**
```python
print(len("안녕하세요"))
```
**사용자로부터 입력을 받는 input 함수**
```python
# input으로 입력 받으면 문자열로 입력받는다
name = input("이름을 입력하세요> ")
print(name)
# casting 형변환 input 함수
int_a = int(input("정수 입력> "))
float_b = int(input("실수 입력> "))
print("type = ", type(int_a))
print("type = ", type(float_a))
```
**format 함수**
```python
# {}를 사용하며 매개변수에 맞게 쓰는게 중요! 
string = "{} {}".format(10, "hello")

string_plus = "{:+d}".format(10) # 양수면 (+)기호 음수면 (-)기호
string_minus = "{:+d}".format(-20)
string_a = "{: d}".format(30) # 양수면 기로위치를 공백처리
string_b = "{: d}".format(-40)

# 공백처리
string_b = "{:+5d}".format(-40)
string_b = "{:=+5d}".format(-40)
string_b = "{:+05d}".format(-40)
```

**대소문자 변경 upper(), lower()**
```python
string_a = "Hello World"
print(string_a.upper())
print(string_a.lower())
```

**문자열찾기 find(), rfind() 함수**
```python
string_a = "Hello World"
print(string_a.find("World"))
```

**in 연산자**
```python
# in연산자 값은 불린형으로 반환된다.
print("World" in "Hello World!")
```
**문자열 자르는 split() 함수**
```python
string_a = "10 20 30 40 50"
print(string_a.split(" ")) # 공백을 기점으로 문자 자르기
```

## 거북이 프로그램
```python
import turtle
turtle.shape("turtle")
turtle.left(90)
turtle.forward(100)
turtle.mainloop()
```

# 2차시

**자료형 bool**
```python
num = 10
print(num == 100)
print(num != 100)
print(num < 100)
print(num <= 10)
```

**정수 연산 프로그램**
```python
num1 = int(input("정수1 입력>"))
num2 = int(input("정수2 입력>"))
add = "{}+{}={}".format(num1, num2, num1+num2)
sub = "{}-{}={}".format(num1, num2, num1-num2)
div = "{}//{}={}".format(num1, num2, num1//num2)
mul = "{}*{}={}".format(num1, num2, num1*num2)
```

**if문**
```python
fruit = int(input("1, 2중 선택> "))
if fruit == 1:
    print(fruit, "은 사과")
elif fruit == 2:
    print(fruit, "는 배")
else:
    print("1, 2 중의 정수만 입력")
```

**홀짝 판별기**
```python
num = input("정수 입력>")
num = num[-1]
if num in "02468":
    print("짝수입니다!")
else:
    print("홀수입니다!")
```