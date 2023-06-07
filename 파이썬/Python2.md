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


# 파이썬 기말고사 범위

## tkinter pack() & grid()
```python
from tkinter import *
window = Tk()
window.title("타이틀 작성")

Label(window, text="pack() 함수 사용").pack()
Label(window, text="grid() 함수 사용").grid(row=1, columm=1, sticky=W)

label = Label(window, text="grid() 함수 사용")
label.grid(row=2, columm=1, sticky=E)

window.mainloop()
```

## tkinter Button()
```python
from tkinter import *
window = Tk()
window.title("타이틀 작성")

button = Button(window, text="btn", width=25, fg="White", bg="lightgreen")
button.grid(row=0, column=0, sticky=W)

button2 = Button(window, text="as", width=50, fg="Black", bg="Black")
button2.grid(row=2, column=0, columnspan=2 , sticky=W)

window.mainloop()
```

## tkinter toolkit
```python
from tkinter import *

window = Tk()
window.title("로그인 페이지 만들어 보기")

Label(window, text="Student ID").grid(row=0, column=0, sticky=E)
Label(window, text="Name").grid(row=1, column=0, sticky=E)
Label(window, text="Phone Number").grid(row=2, column=0, sticky=E)

entry1 = Entry(window, width=20, bg="White")
entry1.grid(row=0, column=1)
entry2 = Entry(window, width=20, bg="White")
entry2.grid(row=1, column=1)
entry3 = Entry(window, width=20, bg="White")
entry3.grid(row=2, column=1)

Button(window, width=30, text="로그인", fg="White", bg="Black").grid(row=3, column=0, columnspan=2, rowspan=2)

window.mainloop()
```

## 경고창
```python
import tkinter.messagebox as mb
import tkinter.simpledialog as sd
import tkinter.color

isYes = mb.askyesno("askyesno", "계속하시겠습니까?")
isOk = mb.askokcancel("askokcancel", "맞나요?")
isYesNoCancel = mb.askyesnocancel("askyesnocancel", "Yes, No, Cancel?") 
print(isYesNoCancel)

name = sd.askstring("askstring", "Enter your name")
print(name)
age = sd.askinteger("askinteger", "Enter your age")
print(age)
weight = sd.askfloat("askfloat", "Enter your weight")
print(weight)
```

## String 참조 메모리는 다르다
```python
s1 = "안녕하세요내나이는23"
s2 = "안녕"
print(id(s1))
print(id(s2))

print(len(s1))
print(max(s1))
print(min(s1))
```

## String 연산자
```python
s1 = "Welxome"
s2 = "파이썬"
s3 = s1 + " 여기는 " + s2
s4 = 2 * s1

print(s3)
print(s4)
print(s1[3 : 6])
print('W' in s1)
print('오' in s1)
print(s1[-1])
print(s1[-3 : -1])

cs1 = "green"
cs2 = "glow"
print(cs1 == cs2)
print(cs1 != cs2)
print(cs1 >= cs2)
```

## String 테스트
```python
s = "welldone"
print( s.isalnum() )        # True
print( s.isalpha() )        # True
print( s.isdigit() )        # False
print( s.isidentifier() )   # True
```

## String 변환
```python
s1 = "idea for you"
print( s1.capitalize() )        # 첫번째 대문자
print( s1.title() )             # 문자들의 첫번째 모두 대문자
print( "HAPPY".lower() )        # 소문자화
print( "any".upper() )          # 대문자화
print( "You sEE".swapcase() )   # 반대로
print( "Alpha Beta".replace("Beta", "Delta") ) # 교체
```

## String 문자열 공백 제거
```python
s = "       안녕 Hoo Python\t"
print(s)
print( s.lstrip() ) # 좌측 공백 제거
print( s.rstrip() ) # 우측 공백 제거
print( s.strip() )  # 공백 제거
```

## String 정렬 전환 
```python
s = "Welcome"
print( s.center(11) ) # ' welcome '
print( s.ljust(22) ) # 'welcome     '
print( s.rjust(33) ) # '            welcome'
```

## 16진수를 10진수로 변환
```python
# Hex to Decimal
def main() : 
    hex = input("hex 정수 값 입력: ").strip()
    decimal = hexToDecimal(hex.upper())
    if decimal == None :
        print("잘못된 hex 값")
    else : 
        print(f"hex {hex}의 decimal 값 {decimal}")

def hexToDecimal(hex) : 
    decimalValue = 0
    for i in range(len(hex)) : 
        ch = hex[i]
        if 'A' <= ch <= 'F' or '0' <= ch <= '9' :
            decimalValue = decimalValue * 16 + hexCharToDecimal(ch)
        else : 
            return None
    return decimalValue

def hexCharToDecimal(ch):
    if 'A' <= ch <= 'F' : 
        return 10 + ord(ch) - ord('A')
    else : 
        return ord(ch) - ord('0')

main()
```

## 2진수를 10진수로
```python
def binaryToDecimal(binaryStr) :
    decimal = 0
    length = len(binaryStr) - 1
    for digit in binaryStr :
        decimal += int(digit) * (2 ** length)
        length -= 1
    return decimal

mainBinary = input("이진수 입력 : ")
mainDecimal = binaryToDecimal(mainBinary)

print(f"{mainBinary}의 십진수 값 : {mainDecimal}")
```

# 14 주차

## 행 열 주기
import random as r 

matrix = []
Row = eval(input("행 입력 : "))
Col = eval(input("열 입력 : "))

for row in range(0, Row) : 
    matrix.append([])
    for col in range(0, Col) :
        matrix[row].append(r.randint(0, 99))

print(matrix)

## 행 열 추적
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] 
total = 0

for row in range(0, len(matrix)): 
    for column in range(0, len(matrix[row])): 
        total += matrix[row][column]
print("총합은 : " + str(total)) 

for column in range(0, len(matrix[0])) :
    total = 0
    for row in range(0, len(matrix)) :
        total += matrix[row][column]
    print(f"{str(column)}은 {str(total)}입니다.")

## 조건으로 합이 가장 큰 행 찾아내기
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
maxRow = sum(matrix[0])

indexOfMaxRow = 0
for row in range(1, len(matrix)): 
    if sum(matrix[row]) > maxRow:
        maxRow = sum(matrix[row])
        indexOfMaxRow = row

print(f"{str(indexOfMaxRow)}번째 행 이 가장 큰 값을 가지고 있습니다.")

## 배열 섞기
import random
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] 

for row in range(0, len(matrix)):
    for column in range(0, len(matrix[row])):
        i = random.randint(0, len(matrix)-1)
        j = random.randint(0, len(matrix[row])-1)
        
        matrix[row][column], matrix[i][j] = matrix[i][j], matrix[row][column]

print(matrix) 

## 배열 구성 함수화
import random as r
def getMatrix() : 
    matrix = []

    Rows = eval(input("열 입력: "))
    Cols = eval(input("행 입력: "))
    for row in range(Rows) : 
        matrix.append([])
        for column in range(Cols) :
            matrix[row].append(r.randint(0, 99))
    return matrix

def accumulate(m):
    total = 0
    for row in m:
        total += sum(row)
    return total


def main() :
    m = getMatrix()
    print(m)
    print(f"배열의 총 합 : {accumulate(m)}")

main()

## 두점 사이거리 구하기 공식으로 점사이 거리가 가장 가까운 좌표 구하기
def distance(x1, y1, x2, y2) :
    return ( (x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1)) ** 0.5

def nearestPoints(points):
    p1, p2 = 0, 1
    shortesDistance = distance(points[p1][0], points[p1][1], points[p2][0], points[p2][1])

    for i in range(len(points)) :
        for j in range(i + 1, len(points)) :
            d = distance(points[i][0], points[i][1], points[j][0], points[j][1])

            if shortesDistance > d :
                p1, p2 = i, j
                shortesDistance = d

    return p1, p2


import NearestPoints
  
def main():
    numberOfPoints = eval(input("Enter the number of points: "))

    points = []
    print("Enter", numberOfPoints, "points:", end = '')
    for i in range(numberOfPoints):
        point = 2 * [0]
        point[0], point[1] = \
            eval(input("Enter coordinates separated by a comma: "))
        points.append(point)

    p1, p2 = NearestPoints.nearestPoints(points)  

    print("The closest two points are (" +
        str(points[p1][0]) + ", " + str(points[p1][1]) + ") and (" +
        str(points[p2][0]) + ", " + str(points[p2][1]) + ")")

main()

## 3차원 배열 생일 날짜 구하기

def main():
    day = 0 # Day to be determined

    dates = [
        [[ 1,  3,  5,  7],
        [ 9, 11, 13, 15],
        [17, 19, 21, 23],
        [25, 27, 29, 31]],
        [[ 2,  3,  6,  7],
        [10, 11, 14, 15],
        [18, 19, 22, 23],
        [26, 27, 30, 31]],
        [[ 4,  5,  6,  7],
        [12, 13, 14, 15],
        [20, 21, 22, 23],
        [28, 29, 30, 31]],
        [[ 8,  9, 10, 11],
        [12, 13, 14, 15],
        [24, 25, 26, 27],
        [28, 29, 30, 31]],
        [[16, 17, 18, 19],
        [20, 21, 22, 23],
        [24, 25, 26, 27],
        [28, 29, 30, 31]]]

    for i in range(5):
        print(f"생일이 {str(i + 1)}번째 세트 안에 있나요?")       
        for j in range(4):
            for k in range(4):
                print(format(dates[i][j][k], '4d'), end = " ")
            print()
        answer = eval(input("Enter 0 for No and 1 for Yes: "))

    if answer == 1:
        day += dates[i][0][0]

    print("당신의 생일 날은 " + str(day))
   
main() 