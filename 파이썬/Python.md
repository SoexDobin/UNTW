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

**datetime모듈 불러오가**
```python
import datetime # 모듈 불러오기

now = datetime.datetime.now()

## datetime 프로퍼티
print(now.year, "년")
print(now.month, "월")
print(now.day, "일")
print(now.hour, "시")
print(now.minute, "분")
print(now.second, "초")

## 오전, 오후 계산기
if now.hour < 12:
    print(f"현재 시간은 {now.hour}시이며, 오전입니다.")
else:
    print(f"현재 시간은 {now.hour}시이며, 오후입니다.")

## 사계절 계산기
if now.month==12 or 1<=now.month<=2:
    print(f"현재 {now.month}월이며, 겨울입니다!")
elif now.month<=5:
    print(f"현재 {now.month}월이며,  봄입니다!")
elif now.month<=8:
    print(f"현재 {now.month}월이며, 여름입니다!")
else:
    print(f"현재 {now.month}월이며, 가을입니다!")
```

**if문 활용**
```python
## 정수 사칙연산 계산기
n1 = int(input("정수1를 입력하세요> "))
n2 = int(input("정수2를 입력하세요> "))

print("1. 덧셈")
print("2. 뺄셈")
print("3. 곱셈")
print("4. 나눗셈")
select = int(input("선택하세요> "))
if select==1:
    print("{}+{}={}".format(n1, n2, n1+n2))
elif select==2:
    print("{}-{}={}".format(n1, n2, n1-n2))
elif select==3:
    print("{}x{}={}".format(n1, n2, n1*n2))
elif select==4:
    print("{}//{}={}".format(n1, n2, n1//n2))
else:
    #print("1~4사이 정수만 입력 가능합니다.")
    pass
```

**list 배열 활용**
```python
list_a = [10, 20, 30, "hello", True]
print(list_a[0:2])
print(list_a[-2])
list_a[1] = "world"
print(list_a[1])
print(list_a[3][1])

## 배열 삽입
print("배열 삽입")
list_a.append([40, 50])
print(list_a)
list_a.insert(5, "bye")
print(list_a)
list_a.extend([9, 8])
print(list_a)

## 배열 제거
print("배열 제거")
del list_a[0]
print(list_a)
a = list_a.pop(0)                                                                                                            
print(list_a)
print(a)
list_a.remove(30)
print(list_a)

## 2차원 배열
print("2차원 배열")
list_b = [[10, 20, 30], ['a', 'b', 'c'], [True, False]]
print(list_b[2][0])
print(len(list_b[2]))
list_b.clear
```

# 3차시
**dictionary**
```python
# for i in dict
dic_a=["name":"정창식", "grade":1, "score":100]
for i in dict_a :
    print(i,":", dict_a[i])
```

**range함수**                                                                                                                                 
```python
 # 초기값이 2일때 i += 3
for i in range(2,10,3):
    print(i)  
```

**별 짓기**
```python
star = ""
floor = int(input("층수를 입력하세요> "))
for i in range(0, floor, 1):
    star = star + "*"
    print(star)
print("줄바꾸고")
for i in range(floor):
    for j in range(i+1):
        star+="*"
    star+="\n"
```

# 4차시

**while문**
```python
# 기본 while
i=0
while i<10:
    print(i ," 번째 반복")
    i = i + 1

# list를 활용한 while
list_a = [1,2,3,4,2,1,3,2,1,2,3,2,2,4,1]
value = 2
while value in list_a:
    list_a.remove(value)
print(list_a)

# while 활용
i=0
while True:
    print(f"{i}번째 반복")
    i+=1
    input_a = input("종료?(y/n)> ")
    if input_a in ['y', 'Y']:
        print("종료합니다.")
        break
```

**continue**
```python
list_a = [10,15,20,25,30,5]
for i in list_a:
    if i<20:
        continue
    print(i)
```
* 현재 반복을 생략하고 다음 반복으로 넘어간다.


**while로 10000이 넘어갈때 변수 값 추출하기**
```python
i = 1
total = 0
while total < 10000:
    print(f"{i}")
    total = total + i
    i = i + 1
print(f"{i-1}을 더할 때 10000을 넘는다.")
```


**사용자가 입력한 정수 두개 사이 값의 합을 구하기**
```python
total = 0
total2 = 1
temp = 0
num1 = int(input("사용자 정수1 입력> "))
num2 = int(input("사용자 정수2 입력> "))

if num2 < num1:
    temp = num1
    num1 = num2
    num2 = temp

while num1 <= num2:
    total += num1
    num1 += 1
print(f"총합은 {total}입니다.")

while num1 <= num2:
    total2 *= num1
    num1 += 1
print(f"총 곱한 값은 {total2}입니다.")
```

**파이썬 기본함수**
```python

```