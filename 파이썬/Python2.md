# 파이썬 1차시

## eval의 사용법 (eval 사용은 지향할 것!)
```python
radius = int(input("반지름의 길이 입력: "))
area = radius * radius * 3.14159

print("반지름은", radius, "면적은", area)
print(type(radius))
```

## 평균 계산기
```python
num1, num2, num3 = eval(input("3가지수를 ', '(컴마)로 분리하여 입력해주세요: "))
num1, num2, num3 = input("3가지수를 ' '공백으로 분리하여 입력해주세요: ").split()
average = (int(num1) + int(num2) + int(num3)) / 3
print(f"평균은 {average} 입니다.")
```

## 시간 계산 import time
```python
import time

curTime = time.time()

totalSec = int(curTime)
curSec = totalSec % 60

totalMin = totalSec // 60
curMin = totalMin % 60

totalHour =  totalMin // 60
curHour = totalHour % 24

print(f"현재시간은 {curHour} : {curMin} : {curSec} GMT")
```

# 파이썬 2차시

## 랜덤 모듈 사용하기
```python
import random as r

num1 =  r.randint(0, 9)
num2 =  r.randint(0, 9)

answer = eval(input(f"{num1} 더하기 {num2} 는? : "))

print(f"{num1} + {num2} = {answer} is {num1 + num2 == answer}")
```

## if문 사용해보기 2진수 생일자 찾는 알고리즘
```python
num = eval(input("정수 입력: "))

if num % 5 == 0 :
    print("5의 배수")

if num % 2 == 0 :
    print("2의 배수")

day = 0

q1 = "1번째 달력에 생일이 있습니까?\n" + \
    " 1  3  5  7\n" + \
    " 9 11 13 15\n" + \
    "17 19 21 23\n" + \
    "25 27 29 31\n" + \
    "있다면 1을 입력해주시고 아니라면 0을 입력해 주세요.: " 

answer = eval(input(q1))

if answer == 1:
    day += 1

q2 = "2번째 달력에 생일이 있습니까?\n" + \
    " 2  3  6  7\n" + \
    "10 11 14 15\n" + \
    "18 19 22 23\n" + \
    "26 27 30 31\n" + \
    "있다면 1을 입력해주시고 아니라면 0을 입력해 주세요.: " 

answer = eval(input(q2))

if answer == 1:
    day += 2

q3 = "3번째 달력에 생일이 있습니까?\n" + \
    " 4  5  6  7\n" + \
    "12 13 14 15\n" + \
    "20 21 22 23\n" + \
    "28 29 30 31\n" + \
    "있다면 1을 입력해주시고 아니라면 0을 입력해 주세요.: " 

answer = eval(input(q3))

if answer == 1:
    day += 4

q4 = "4번째 달력에 생일이 있습니까?\n" + \
    " 8  9 10 11\n" + \
    "12 13 14 15\n" + \
    "24 25 26 27\n" + \
    "28 29 30 31\n" + \
    "있다면 1을 입력해주시고 아니라면 0을 입력해 주세요.: " 

answer = eval(input(q4))

if answer == 1:
    day += 8

q5 = "5번째 달력에 생일이 있습니까?\n" + \
    "16 17 18 19\n" + \
    "20 21 22 23\n" + \
    "24 25 26 27\n" + \
    "28 29 30 31\n" + \
    "있다면 1을 입력해주시고 아니라면 0을 입력해 주세요.: " 

answer = eval(input(q5))

if answer == 1:
    day += 16

print(f"당신의 생일은 {str(day)}!")
```

## if else
```python
import random as r

num1 =  r.randint(0, 9)
num2 =  r.randint(0, 9)

if num1 < num2:
    num1, num2 = num2, num1

answer = eval(input(f"{num1} - {num2} = ? :"))

if num1 - num2 == answer:
    print("정답")
else:
    print(f"틀림 정답은 {num1 - num2}")

# 연산자 사용해 보기
number = eval(input("Enter an integer: "))

if number % 2 == 0 and number % 3 == 0:
    print(number, "is divisible by 2 and 3")

if number % 2 == 0 or number % 3 == 0:
    print(number, "is divisible by 2 or 3")

if (number % 2 == 0 or number % 3 == 0) and not (number % 2 == 0 and number % 3 == 0):
    print(number, "divisible by 2 or 3, but not both")
```

# 파이썬 3차시

## for문으로 구구단 출력하기
```python
total = 0
rangeNum = int(input("정수 값 입력: "))

for i in range(1, rangeNum, +1):
    numD = 2 * i - 1
    numC = (-1)**(i-1)
    if (i%2 == 1):
        total += numD/numC
    elif (i%2 == 0):
        total -= numD/numC


computePie = total * 4
print(f"Answer : {computePie}")


# for문으로 구구단 출력
for j in range(1, 10):
    print("   ", j, end = "")
print()
print("----------------------------------------------")

for i in range(1, 10):
    print(i, "l", end = "")
    for j in range (1, 10):
        print(format(i * j, "4d"), end = "")
    print()
```

## while로 최대 공약수 찾기
```python
intN1 = int(input("정수 1 입력: "))
intN2 = int(input("정수 2 입력: "))

god = 1
k = 2
while intN1 >= k and intN2 >= k:
    if intN1 % k == 0 and intN2 % k == 0:
        god = k
    k += 1

print(f"{intN1}과 {intN2}의 최대공약수는 {god}")

# 미래 세금률 계산기
year = 0
tuition = 10000

while tuition <= 20000:
      tuition = tuition * 1.07
      year = year + 1
print(f"How much years : {year}")
```


## 소수 출력기
```python
primeNum = 50
primeDisplayPerLine = 10
count = 0
testNum = 2

while count < primeNum:
    isPrime = True

    divisor = 2
    while divisor <= testNum / 2:
        if testNum % divisor == 0:
            isPrime = False
            break
        divisor += 1
    
    if isPrime:
        count += 1
        print(format(testNum, "5d"), end = "")
        if count % primeDisplayPerLine == 0:
            print()
    
    testNum += 1
```

# 파이썬 4차시

## 함수 만들기 
def sort (num1, num2):
    if num1 < num2:
        return num1, num2
    else:
        return num2, num1

num1 = 1
num2 = 2
print(num1)
print(num2)
num1, num2 = sort(3, 2)
print(num1)
print(num2)

## 도형 함수 만들어보기 with turtle
import turtle as t

def drawLine(startPointX, startPointY, endPointX, endPointY):
    t.penup()
    t.goto(startPointX, startPointY)
    t.pendown()
    t.goto(endPointX, endPointY)
    t.exitonclick()

def writeStrings(comments, writePosX, writePosY):
    t.penup()
    t.goto(writePosX, writePosY)
    t.pendown()
    t.write(comments)
    t.exitonclick()

def drawPoint(x, y): 
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.begin_fill()
    t.circle(3) 
    t.end_fill()


def drawCircle(drawPosX, drawPosY, radius = 10):
    t.penup()
    t.goto(drawPosX, drawPosY - radius)
    t.pendown()
    t.circle(radius)
    t.exitonclick()

def drawRectangle(drawPosX, drawPosY, width=10, height=10):
    centerPosX = (drawPosX + width) /2
    centerPosY = (drawPosY + height) /2
    t.penup()
    t.goto(centerPosX, centerPosY)
    t.pendown()
    for i in range(1, 5, +1):
        if(i%2 == 1):
            t.forward(width)
            t.right(90)
        elif(i%2 == 0):
            t.forward(height)
            t.right(90)
    t.exitonclick()
    
#drawLine(0, 0, 30, 30)
#writeStrings("허기진다.", 10, 20)
#drawCircle(0, 0, 50)
drawRectangle(0,0, 50, 100)



















# 숙제 모음

## 두점 사이 거리 구하기 homework
```python
import turtle

x1, y1 = eval(input("첫번째 점 x y 컴마로 칸나누어 입력: "))
x2, y2 = eval(input("두번째 점 x y 컴마로 칸나누어 입력: "))

distance = ((x1-x2) * (x1-x2) + (y1 - y2) * (y1 - y2)) ** 0.5
print(f"두 점사이 거리는 {distance}")

turtle.penup()
turtle.goto(x1, y1)
turtle.write(f"{x1}, {y1}")
turtle.pendown()
turtle.goto(x2, y2)
turtle.write(f"{x2}, {y2}")
turtle.goto(distance, distance)
turtle.write(f"{distance}")
```

## 겹치는 원 확인하기 homework
```python
import turtle
import math
x1, y1 = eval(input("첫번째 원 x, y 좌표: "))
radius1 = eval(input("찻반째 원 반지름: "))
x2, y2 = eval(input("두번째 원 x, y 좌표: "))
radius2 = eval(input("두반째 원 반지름: "))

# Draw the circle
turtle.penup()
turtle.goto(x1, y1 - radius1)
turtle.pendown()
turtle.circle(radius1)

# Draw the circle
turtle.penup()
turtle.goto(x2, y2 - radius2)
turtle.pendown()
turtle.circle(radius2)

distance = math.sqrt((x2 - x1) ** 2 + ((y2) - (y1)) ** 2)

if distance > abs(radius1 - radius2):
    turtle.write("걸쳐짐")
elif distance <= radius1 + radius2:
    print(f"거리 {distance}\n")
    print(f"걸침 {abs(radius1 - radius2)}\n")
    print(f"겹침 {radius1 + radius2}\n")
    turtle.write("겹침")
else:
    turtle.write("안겹침")

turtle.exitonclick()
```

## 파이 계산기 함수로 정리 homework
```python
def m(rangeNum):
    total = 0
    print(format("1\t\t\tm(i)\n"))
    for i in range(1, rangeNum+1, +1):
        numD = 2*i - 1
        numC = (-1)**(i+1)
        if (i%2 == 1):
            total += numC/numD
        elif (i%2 == 0):
            total += numC/numD
        if(i%100==1):
            print(f"{i}\t\t\t{total*4}")

rangeNum = int(input("정수 값 입력: "))
m(rangeNum)
```

## 도형그리기와 오륜기 homework
```python
## 도형 그리기
import turtle as t

t.pensize(3)
t.penup()
t.goto(-200, 50)
t.pendown()
t.setheading(60)
t.begin_fill()
t.color("red")
t.circle(40, steps= 3)
t.end_fill()

t.penup()
t.goto(-100, 50)
t.pendown()
t.setheading(45)
t.begin_fill()
t.color("blue")
t.circle(40, steps= 4)
t.end_fill()

t.penup()
t.goto(0, 50)
t.pendown()
t.setheading(35)
t.begin_fill()
t.color("green")
t.circle(40, steps= 5)
t.end_fill()

t.penup()
t.goto(100, 50)
t.pendown()
t.setheading(30)
t.begin_fill()
t.color("yellow")
t.circle(40, steps=6)
t.end_fill()

t.penup()
t.goto(200, 50)
t.pendown()
t.begin_fill()
t.color("purple")
t.circle(40)
t.end_fill()

## 사용자에게 반지름 입력 받아 올림픽 마크 그리기
radius = int(input("반지름 입력: "))

def DrawCir(gotoX, gotoY, radius):
    t.penup()    
    t.goto(gotoX, gotoY)
    t.pendown()
    t.circle(radius)    

t.pensize(8)
t.color("blue")
DrawCir(-(radius*2.5), 0, radius)

t.color("black")
DrawCir(0, 0, radius)

t.color("red")
DrawCir((radius*2.5), 0, radius)

t.color("green")
DrawCir(radius*1.25, -radius, radius)

t.color("yellow")
DrawCir(-(radius*1.25), -radius, radius)

t.exitonclick()
```
