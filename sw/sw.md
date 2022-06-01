# 객체지향
* 캡슐화, 다형성, 상속으로 프로그램의 재사용성, 확장성, 수정용이성 3가지의 유연성을 좋게하고 유지보수를 쉽게하기 위해서 배워야 한다.

* 객체의 구조   
  + 정적요소 : 속성
  + 동적요소 : 메서드


* 추상화
  + 정적요소 프로퍼티와 동적요소 메서드의 정의한 것들을 추상화라고 한다.

* 인터페이스
  + public method의 시그니쳐
  ```c++
  void Print(int n)const //이부분이 시그니쳐이자, 인터페이스
  private void Error(double h) //이건 인터페이스가 아님

  int main(){
    Person p("최재욱", 23, "010-9018-9829");
    p.Print();
  }
  // p.Print();는 main함수가 p객체에게 Print()메세지를 보낸다라는 뜻
  ```

* 계층구조
  + is a 관계를 가지는 객체를 부르는 말이다.
  + 동물 객체는 사자와, 까지 객체를 가질때 두 객체는 (is a 동물) 관계이다.
```c++
class Person {};
class Student : public Person {};
int main(){
  Person p; Student s;
  p = s;  //학생 is a 사람이다. //사용 x
  Person& rp = s; // 부분 참조가 일어나서 사용가능하다.
  Person* pp = &s; // Person부분까지만 주소로 가르키기에 사용가능하다.
}
```
**시험(p = s;)는 맞는 의미지만 메모리상으로 s가 구체화되어있어 p,s내용 두개가 있기 때문에 메모리 아작으로 사용하면 안된다.**

```c++
class Person {
  string name;
public:
  virtual void Print(){ cout << name << endl; } 
}; // 최상위 부모 버츄얼 정의
class Student : public Person {
  int grade;
public:
  void Print(){ cout << name << grade << endl; }
};
int main(){
  Person p; 
  Student s;
  Person& rp = s; 
  Person* pp s&; 
  rp.Print(); // 다형성에 의한 다형적 메서드
  pp->Print(); // 다형성에 의한 다형적 메서드
}
```
**부모클래스 버츄얼 정의를 통해 grade까지 모두 가져올 수 있다.**
* 어느 자식객체든 Person부모 형식으로 만들어야하고 할 수 있다.
* 조립구조
  + has a 관계를 가지는 객체를 부르는 말이다.
  + 삼각형과 사각형은 (has a 점)을 가진 관계이다.

```c++
class Shape { //추상객체
	string name;
public:
	Shape(const string& n = "") :name(n){}
	virtual void Draw() = 0; //순수가상함수(=abstract메서드) <-요놈때문에 추상객체가됨
	virtual void PrintInfo() { cout << "Info: " << name << endl; }
	const string GetName() { return name; }
	const string SetName(const string& n) { name = n; }
};
class Rectangle :public Shape {
	int x, y;
	int width, height;
public:
	Rectangle(int _x = 0, int _y = 0, int w = 0, int h = 0, const string& n = ""):
		Shape(n), x(_x), y(_y), width(w), height(h) {}
	void Draw() { cout << "R: "<< x << "," << y << "," << width << "," << height << endl; }
};
class Circle : public Shape {
	int x, y;
	int radius;
public:
	Circle(int _x = 0, int _y = 0, int r = 0 , const string& n = "") :
		Shape(n), x(_x), y(_y), radius(r) {}
	void Draw() { cout << "C: " << x << "," << y << "," << radius << endl; }
	void PrintInfo() {
		Shape::PrintInfo();
		cout << "--Info:" << "Circle" << endl;
	}
};
int main() {
	Shape* ps = NULL;
	Rectangle r1(10, 10, 4, 500, "Rect");
	Circle c1(0, 0, 5, "Cir");

	ps = &r1;
	ps->Draw();
	ps->PrintInfo();
	ps = &c1;
	ps->Draw();
	ps->PrintInfo();
}
```
* 상속의 3가지 종류
```c++
//			      인터페이스	 구현부   
//(비virtual) 		O		      O     	
//(virtual)		    O		    △선택        
//(astract)		    O		  X(강제구현)
```
* abstract는 virtual void Draw() = 0; 와 같이 선언하며 추상메서드는 반드시 자식 클래스에서 재정의 되어야 한다. 순수가상함수라고도 한다.
* virtual은 추상메서드로 구현부인 implement를 재정의 할수도 있고 또는 상속 만 받을수있게 선택적으로 사용 할 수 있다.

# UML
소스코드 작성전 다이어그램으로 쉽게 알수있도록 미리 만들어보는것.
### why?
1. 실제로 잘 작동하는지 알아보려고 만드는것이 "모델"이다.
2. 실수를 줄이고 시간&비용 손해를 덜보기위해 모델을 만들어 설계를 검사한다.
3. UML은 주관적이다.
4. 소스코드보다 비용이 덜들떄 사용한다.
5. 소프트웨어는 모델을 쓰는것이 비용&시간등 모든것이 명확하고 분명하지 않다.

### when?
1. 다른 사람들과 의사소통할때.
2. 알고리즘 표현에는 적절하지 않다.
3. 대규모 sw구조 로드맵을 구현할때 유용하다.
  * 어떤 클래스가 다른클래스에 의존하는지 빠르게 파악가능하다.
  * 단! 칠판에 그리고 없앨수 있을만큼 간단해야 한다.
  * 반복하여 그리고 차근차근 진행해야한다.

### How?
1. 동적인것부터 행위를 제일 먼저 생각하여 다이어그램을 짜본다.
2. 정적관계에서 의미를 조사한다.
3. 정적관계를 개선한다.
4. 위 내용을 바탕으로 기존 동적 다이어그램을 개선한다.

* 정적 다이어그램
  + 클래스
  + 객체
  + 컴포넌트
  + 배치
* 동적 다이어그램
  + 순차
  + 유스케이스
  + 통신
  + 상태
  + 액티비티
## 클래스다이어그램
![classDiagram](https://user-images.githubusercontent.com/56966606/161099775-fc161555-3026-4680-93c7-a93d091f5ce6.png)
* 박스를 클래스라고한다.     
* -->는 연관관계를 맺는다고한다.     
* 클래스안에를 나누어 중요한 함수 or 변수를 표현한다.   
* 클래스내 함수는 +를 붙인다.   
* ※ 화살표 방향을 헷갈리는 경우가 있는데 자식이 부모에게 겨누면 된다.
* ※ 상속은 반대!!
* TreeMap 클래스   
  - 박스안에는 add()클래스와 get()클래스 2개를 담고있다.   
    + add()는 key와value값을 받는다.   
    + get()은 key값을 받는다.   
* TreeMapNode 클래스   
* TreeMapNode는 참조변수로써 topNode라고한다.   
* 박스안에는 add()클래스와 find()클래스 2개를 담고있다.   
  - add()는 key와value값을 받는다.   
  - find()은 key값을 받는다.   
  - nodes로 인스턴스를 2개 를 받는다.   
* itskey라는 요소로 인터페이스 Comparable()클래스에 접근한다.   
* itsvalue라는 요소로 Object()클래스에 접근한다.   
## 객체다이어그램
![objectDiagram](https://user-images.githubusercontent.com/56966606/161100206-96c76913-45d4-4701-91fc-99add21f273b.png)
**시스템 실행중 어느 순간의 객체와의 관계를 포착해 보여준다.**   
* 박스안에 :와 밑줄을 써서 표현한다. ex. :<U>TreeMap</U>   
* -->는 link 연결이라고한다.   
* "-"는 감추어져있는 private멤버 변수이다.   

* TreeMap 객체   
* TreeMapNode   
  - TreeMap객체는 참조형식으로써  TreeMapNode객체의 topNode라고한다.   
  - 프라이빗변수 itsKey는 "Martin"이라는 값을 가진다.   
  - nodes[LESS]배열과 nodes[GREATER]배열 두 배열은 itsKey="Martin"이 참조하고 있다.   
## 상태다이어그램
![stateDiagram](https://user-images.githubusercontent.com/56966606/161100249-3195415a-f56b-4996-84f7-2155caf428eb.png)
* 유한 상태 기계를 나타내기위한 다이어그램이다.   
* 상태는 둥근사각형으로 감싼다.   
* -->는 transition 전이라고한다.   

* 전이의 좌측은 이벤트라고한다.   
* 전이의 우측은 이벤트 발생시 수행되는 행동이라고한다.   
  - pass하면 Alarm을 울리겠다.   
## 시퀀스 다이어그램(절차) == 커뮤니케이션 다이어그램(객체) 
![comunicateDiagram](https://user-images.githubusercontent.com/56966606/161102339-898e5a45-0228-44e4-ba8e-5d577ce29013.png)   
* 시간에 따른 변화에 포커스르 두지만 절차에 집중하면 시퀀스이고 
* 객체 중점이면 커뮤니케이션 으로 나눈다.   
* -->는 메세지를 보낸다.
* 1은 첫번째로 *은 여러개의 digit메세지를 n값으로 보낸다는 뜻이다.
![comunicateDiagram2](https://user-images.githubusercontent.com/56966606/161108176-02a50be0-3741-48ed-a8b4-8f1a9037df62.png)
<U>send:Button</U>이라는 두번째 메세지의 의존도 추가되었다.   
<U>:Button</U> 객체 박스를 겹치면 여러개의 객체를 사용한다는 것을 나타낸다. 

**그러나 이 객체를 점검해볼 필요가 있다.**
* Button객체는 단지 전화기 뿐만 아니라 리모콘, 정수기 등 여러 곳에서 쓰일수 있는 객체이기 때문에 다이얼에 의존하는 형태는 아쉽다고 할 수있다.
![Adapter1](https://user-images.githubusercontent.com/56966606/161108126-48fda55c-f0a0-4ea1-b12d-d5ee1c323256.png)
* 식별자 코드는 각 객체가 어떤 속성인지를 알려주는 값이다.
* 인터페이스는 의존의 관계가 아니다.
* Button의 의존관계는 풀리지만 다이얼이 역의존 관계이기에 이걸 풀어줄 어뎁터를 추가한다.
* Button은 이로써 가진 기능을 다이얼어뎁터로 보낸다.
**인터페이스 추가로 다이어그램 변화가 생김으로 원래 동적 다이어 그램도 수정해야한다.**
![Adapter2](https://user-images.githubusercontent.com/56966606/161108167-edc35dc8-f91a-4314-a63d-82104d1c4cd1.png)

## 클래스 다이어그램 깊게 공부해보기
**기본**
* 내부 정적 내용이나 클래스 관계표기한다.
* 클래스 상속과 참조를 알 수 있다.
![classDiagram2](https://user-images.githubusercontent.com/56966606/161286100-a2728fa0-52cf-4749-a007-0e5e3d06a235.png)
* 클래스 다이어그램은 클래스이름 / 변수 / 맴버함수로 나뉜다.
* ( - )는 private ( + )는 public ( # ) protected로 표현한다.
* ( : )는 정의한 타입을 쓸때 이용한다.
```c++
public class Dialler​
{​
  private Vector digits;​
  int nDigits;​
  public void digit(int n);​
  protected boolean recordDigit(int n);​
}​
```
**연관**
![classDiagram3](https://user-images.githubusercontent.com/56966606/161286143-0e1d97be-aae9-40dd-b108-a1293689202a.png)
* 연관을 지을때 선언 변수와 변수의 개수를 보여준다.
![classDiagram4](https://user-images.githubusercontent.com/56966606/161286149-6669a7b9-3820-4e39-b51b-658404d54c34.png)
* ( * )은 여러개라는 뜻을 가지며 컨테이너 타입이라는 뜻도가진다. ex.vector
**상속**
![classDiagram5](https://user-images.githubusercontent.com/56966606/161286154-54a52f68-b411-4411-9966-c3e605c3969c.png)
* 관계에있어 상속은 세로로 일반 연관관계는 가로로 그려 가시성을 편하게 한다.
* 인터페이스의 상속 방식도 알고 있을 것.
* 화살표 방향은 소스코드의 의존방향이다.
```java
public class UI implements WithdrawlUI, DepositUI, TransferUI​
{​
  private Screen itsScreen;​
  private MessageLog itsMessageLog;​
  public void displayMessage(String message)​
  {​
    itsMessageLog.logMessage(message);
    itsScreen.displayMessage(message);​
  }​
}​
```


**클래스 스테레오타입**
* << ? >> 길러멧 사이에 적는다
* <<interface>> 클래스
* <<utility>> 클래스

**Math객체 중요!**
![Math](https://user-images.githubusercontent.com/56966606/164891148-772c3b2a-07bc-4abf-9ad6-4eafd9e78993.png)

```java
public class Math​
{​
  public sin(); //일반적으로 만들어지면 인스턴스 안 쓴다.
  public static final double PI =​  // 클래스 메서드
  3.14159265358979323;​
  public static double sin(double theta){...}​
  public static double cos(double theta){...}​
}​
```
* static을 붙이면 Math만이 가지는 클래스 속성이다 **암기**!!!!
* Math로 만든 객체는 무조건 Math에서 기능을 가져다 쓰기에 주로 public으로 쓴다.

**추상 클래스**
![Abstract](https://user-images.githubusercontent.com/56966606/164896188-4de42776-97be-4f58-a91c-4dde6d75d0a8.png)
* 인스터스 클래스를 생성하지 않는 클래스
* 특징 적어도 하나 이상의 추상 메서드를 가진다.
* 이텔릭체로 표현하거나 {abstract}를 붙여준다.
* 추상화된 메서드와 변수에도 동일하게 적용해야 한다.

**association 연관의 3가지 구체화**
**암기** 그리는 방법 
![Aggregation](https://user-images.githubusercontent.com/56966606/164896456-dc6ff0af-35cb-45cd-ae71-f3159bbac280.png)

![Composition](https://user-images.githubusercontent.com/56966606/164896454-94811a2c-d123-4157-bd88-cea42401cca1.png)

**의존은 ------> 그대로 그리면된다.**

* 집합과 구성의 의존은 쓰임새는 같지만 차이점이 있다.
* aggreagation (집합) A -> B면 B를 선택적 변경가능한다.
  - A, B가 같이 또는 다르게 등 피드백 방법을 선택적이다.
  - 자기 자신에 관한 내용에 재집합, 상호집합 등 할 수 없다.
* composition (구성) A -> B면 A영향이 B에게 그대로 전해진다.
  - 주인 객체 한개당 하나의 하나의 인스턴스만 가질 수 있다.
  - 소유관계이다. (A가 B를 소유)
  - 깊은 복사 상태이다.
  - A, B둘다 같이 피드백을 받게된다.
```java
// 자바
class A{
  B b;
}
```
```c++
// c++
class Car{
  Tire* t = new Tire();
  ~Car() {delete Car;}
  Car() { 깊은 복사 } // 복사 생성자
  // c++은 소멸자와 복생이 꼭 필요하다.
};
```
* dependency (의존)

* 연관클래스
* 템플릿 클래스

## 객체지향 설계 원칙 SOLID
* 단일 책임 원칙 Single Responsibility Principle 88 
  - 객체 == 서비스를 제공하는 책임이다.
  - 클래스는 단 하나의 책임을 가져야한다.
  - 너무 많은 변수, 함수등의 선언을 자제하라는 것이다.
  - 다양한 인터페이스 클래스 분할로 책임을 나누어야한다.
  - SRP => 변화
  - ★★ 데이터 추상화 중요!
* 개방 패쇄 원칙 Open Closed Principle 94
  - 확장은 열려있고 수정에 닫혀 있어야한다.
  - 다운 캐스팅 과 if else 사용이 최대한 없어야한다.
  - 다형성과 상속을 이용 인터페이스 기반으로 코드변경없이 들어야한다.
  - OCP => 유연성
  - ★★추상화를 이용한 OCP구현
* 리스코프 치환 원칙 Liskov Substitution Principle
  - 똑바로 상속해라
  - 파생된 클래스에 대하여 알 필요없이 사용하게 해야한다.
  - 서브 타입이 베이스 타입에 교체될 수 있어야함.
  - 굳이 연결 할때 연관으로 이어주는 것이 아닌 호출로써 불러오는게 안전하다.
    + 명시된 명세에서 벗어난 값을 리턴​
    + 명시된 명세에서 벗어난 함수, 명령 발생​
    + 명시된 명세에서 벗어난 기능을 수행​
* 인터페이스 분리 원칙 Interface Segregation Principle
  - 인터페이스에 너무 많은 메서드를 가지지말고 분리하여 세부적인것만 가지게 해야한다.
  - 클라이언트는 자신이 사용하는 메서드에만 의존해야 한다.
  - 클라이언트가 추상클래스, 메서드가 구체화된 클래스에 의존하면 안된다.
  - 인터페이스, 추상클래스가 더 안전하다.(높은 수준 개념)
* 의존 역전 원칙 Dependency Inversion Principle
  - 모듈과 패키지는 객체가 모여만들어진 하나의 기능을 의미한다.
    + 모듈은 가르키는 의존 객체를 제외하고 단일(한개)의 파일만을 의미한다.
    + 패키지는 다른 의존 객체를 모두 포함해서 패키지라도 한다.
  - 인터페이스는 클라이언트를 위해 있는 것이다.  
  - 낮은 수준의 모듈들이 높은 수준의 모듈에 의존하게 만들어야 한다.
  - 자신이 사용하지 않을 메서드에 의존하면 안된다.
  - 클라이언트 하나당 인터페이스 하나같이 기능을 분배한다.

### 전략패턴 strategy pattern
* OCP원칙이 따라오지만 때론 SRP, ISP 원칙도 따라온다. 
* 동일 계열 알고리즘을 개별적으로 캡슐화하여 상호작용 할 수있게 정의한다.
* 클라이언트에 영향없이 전략을 바꾸어 변경이 가능하다.
* 클라이언트는 독립적으로 원하는 알고리즘을 선택하여 사용할 수 있다.
### 템플릿메서드 template Method
* 상위 클래스에서 골격을 정의하고, 하위 클래스에서 세부 처리를 구체화 한다.
* 유사한 서브 클래스를 묶어 공통된 내용을 상위 클래스에 정의한다.
* 코드 양이 줄고 유지보수를 용이하게 해준다.
* 일반적으로 템플릿이 적용된 메서드 이외에는 protected로 메서드가 정의 된다.
# 기말 1차시
### 커맨드 패턴 command pattern
1. 변경될것 같은 코드와 아닐 것 같은 코드를 분리한다.
2. 국지화를 통해 변경 될때 파급효과가 가장 작을 수있게 수정해야 한다.
3. 명령을 추상화해서 객체로 만드는 것이 커맨드패턴의 핵심이다.
* 실행될 기능을 캡슐화 함으로써 주어진 기능들을 재사용성이 높은 클래스로 설계하는 패턴이다.
* 반복적인 수정이 이루어지는 코드는 재사용이 용의하게 만들어야 할 필요가 있는지 생각해봐야 한다.	
* invoke작업으로 선언하고 Excute로 불러온다.
![image](https://user-images.githubusercontent.com/56966606/169700754-82542f32-3580-4c29-a3d0-a681828c34d8.png)
![image](https://user-images.githubusercontent.com/56966606/169701044-428bf5cc-6433-40aa-af22-7061732e1952.png)

### 프로토타입  prototype pattern
* 객체생성에 시간과 비용이 많이들고 유사객체가 있는 경우 사용한다.
* 주로 객체의 깊은 복사를 이하여 사용한다. 상황에 따라 shallow도 가능은 하다.
* 복사를 통해 클라이언트 필요에 따라 불필요한 if, case를 줄이고 추상메서드를 기반으로 메서드가 파생될수 있게 된다.
* 단 내부적으로 추상메서드만의 자료구조가 필요하며 부모 메서드에 is_a 상속관계여야 한다.
* 같은 계층 집합객체 상속에 있어 분명해야 한다.(형제끼리의 추상화가 확실해야 한다.) 
![image](https://user-images.githubusercontent.com/56966606/169701743-da703d07-07dc-4bef-89df-716371c1a629.png)
* 주소 참조 주의 해야 한다.
	
# 기말 2차시
### 상태 패턴
* 일련의 규칙에따라 객체의 상태를 변화시켜, 객체가 할 수 있는 행위르 바꾼다.
* 각상태를 분리하여 보기쉽게 유지보수가 이롭도록한다.
* 각 상태는 서로를 알고있으며 각각 요소가 서로 반응한다.
![image](https://user-images.githubusercontent.com/56966606/169703090-8877453f-1fe7-416e-976d-f549921fe416.png)
![image](https://user-images.githubusercontent.com/56966606/169703102-9297957f-959b-4cfa-a8b8-c756f8222d60.png)
![image](https://user-images.githubusercontent.com/56966606/169703117-7e79b197-4a72-4c60-9b3e-b3f3cd345f61.png)
**상태 변경에 잘 주의 할 것**

### 데코레이터 패턴 Decorator pattern
* 객체위에 기능들을 입혀서 사용 목적에 걸맞는 객체로 만드는 것을 데코레이터 패턴이라 한다.
* 조립구조를 개선하고 데코레이터는 자신조차도 자신을 재상속 한다.
* 데코레이터는 operator를 가져야한다.
* operator는 부모의 operator기능을 상속 받아 호출된다.
* ex)게임속 로그라이크 아이템처럼 먹으면 충첩되게 만드는 게임에 적용하기 쉽다. 	
**중요!! out의 3가지 종류**
![image](https://user-images.githubusercontent.com/56966606/169703435-07a97c44-199c-4219-9570-7bbf957dd5aa.png)
![image](https://user-images.githubusercontent.com/56966606/169703445-9a357d9a-b71a-49aa-9b2f-f3ecf2cc4984.png)
![image](https://user-images.githubusercontent.com/56966606/169703453-b32d07e3-63f7-480d-8081-836aeaf37275.png)

### 옵저버 패턴 Observer pattern(중요!)
*  옵저버들의 목록을 객체에 등록하여 상태 변화가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 한다.
* view 클래스들이 객체데이터를 계속해서 보면서 특정 조건이나 변화에대해 view에게 신호를 주면 (pull방식으로)데이터를 받아간다.
* 필요한 사람들 한테만 주어야하기 때문에 객체는 자신만의 view리스트를 가진다.
* 옵저버를 등록하고 제거하는 메서드와 상태 체크를 하는 메서드가 꼭 필요하다.
* 코드에서 옵저버의 이벤트 메서드는 다른 옵저버들에게 알림을 주어야하기 때문에 public으로 구성된다.
* onAbnormalStatus(Status status);라는 알림을 받는 코드가 필요하다.
* 콘크리트는 기본적인 메서드에 상속을 받아와 구체화하는 클래스를 말한다.
* ex.)유튜브 구독 시스템
**옵저버의 상태 전달 방법**
* 기본 subject에 상태가 주어지면 호출되는 방식.
* subject 객체의존주입으로 많은 내용을 다른 상태를 내보내 호출 할때.
**GUI 구현 중요!! 여러 옵저버가 다양한 subject에 의존 될 수 있다.**
	- 한 개의 옵저버 객체를 여러 주제 객체에 등록할 수 있다. ex.)회원 로그인, 비회원 로그인
	- 주제를 구분 할 수 있는 밥법을 강구하고 객체참조를통해 여러 객체에 등록 가능하다. 
**옵저버 패턴 구현 고려사항 중요!!**
	- 주제 객체의 통지 기능 실행 주체
	![image](https://user-images.githubusercontent.com/56966606/168521305-ac28208f-f845-401b-8fae-7f4ed8180f5c.png)
	- 옵저버 인터페이스 분리
	![image](https://user-images.githubusercontent.com/56966606/168521459-371389a9-6cf4-49fa-a374-385a024df498.png)
		+ isp처럼 인터페이스를 구현이 안되있더라도 효율적인 운영을 위해 구현해야한다.
	- 통지 시점에서의 주제 객체 상태
	![image](https://user-images.githubusercontent.com/56966606/168523520-2dd492d1-db8f-4db1-afe2-dcf3920fe4d2.png)
		+ 통지시점에 객체의 결함이 없어야한다.
	- 옵저버 객체의 실행 제약 조건
	![image](https://user-images.githubusercontent.com/56966606/168523852-f74ab7ee-42e3-4c39-bb32-a09242c7682c.png)
		+ 러닝타임이 길다면 예외나 별도의 방안을 추구해야 한다.
	![image](https://user-images.githubusercontent.com/56966606/168524606-465cb901-7bcd-4bac-b2cd-ec83d637f529.png)

**최종 옵저버 패턴 다이어그램**
![image](https://user-images.githubusercontent.com/56966606/168524126-39a68944-063a-4466-8414-75cf73c2fa7a.png)
### 미디에이터 패턴 Mediator pattern
* 다른 요소끼리 소통하지 못하고 미디에이터 하나를 통해 다를 요소들과 간접 통신하는 방식이다. 
* 옵저버와 다르게 상호 작용이 아니 중재자 자기 자신을 중심으로 프로그램화 된다.
![image](https://user-images.githubusercontent.com/56966606/169704110-881a76be-0cca-4c81-954b-c9f73dff6e81.png)
![image](https://user-images.githubusercontent.com/56966606/169704253-cdf546d6-0015-4bf1-a1f2-0167a5212d2e.png)

### 퍼사드 패턴 Fasade pattern 
* 클라이언트와 주체 클래스사이 퍼사드를 둠으로써 필터마냥 퍼사드로 쓸것만 사용 할 수 있도록한다.
* 이로 인해 클라이언트는 사용하려는 메서드를 모두 알 필요가 없다.
* 데이터 베이스 형식에 있어 입출력에 다양한 의존형태로 인해 코드와 관계가 복잡해질때 사용한다.
* 의존과 중복코드 제거를 위해 뷰어와 데이터베이스 사이 스트림이 퍼사드 역할을 하여 의존 형태를 깔끔하게 맞춰준다.
* 모든 클라이언트는 퍼사드를 통해 이야기하기 때문에 서버시스템 쪽을 변경해도 클라이언트를 변경할 필요가 없어진다.
* 유닛을 수정&변경하려면 모의객체(Mock Object)를 만들어 시험하고 유용한 코드로 변경해야 한다.
![image](https://user-images.githubusercontent.com/56966606/168535191-2ab63028-0d9b-4f81-9889-ac4dd745fe7f.png)
**중요! FlleStream(빨간색) 부분만 소켓으로 바꿔 용도 변경가능하다.**

### 추상 팩토리 패턴 Abstract Factory pattern 중요!!!!
* 객체 호출시 관련된 객체 군을 통체로 팩토리 클래스로 만들어 조건에따라 객체를 생성한다.
* 게임을 예시로 팩토리 메서드는 필요로 하는 객체들 모두를 선언 해준다. (Enemy가 필요하면 모든 Enemy에서 필요한 enemy객체를 호출해준다.)
	* 객체 생성에 있어 OCP를 정확히 구현해야하는  패턴이다.
![image](https://user-images.githubusercontent.com/56966606/169742879-6357d9ad-a245-4112-805f-fae63eaaee65.png)
* getFactory()메서드는 자식 팩토리를 호출해주는 역할을 한다.
	
### 프록시 패턴 Proxy pattern 요즘 안쓴다.
* 모든 객체를 한번에 가져와 클라이언트에 보여주면 성능이 저하된다.
* proxy메서드를 통해 일부 이미지를 미리 보여주면서 나머지는 필요에따라 끌어오면서 성능 저하를 막는다.
* 목록 중에 일부를 타임라인을 만들어 정해진 것들을 일부만 보여주게 만든다.
* 프록시 패턴의 기본 3가지
	- 가상 프록시 : 꼭 필요로 하는 시점까지 객체 생성을 연기하고, 해당 객체가 생성된것 처럼 동작하도록 만든다.
	- 보호 프록시 : 주체 클래스 접근 제어를 클라이언트가 결정 가능하게 한다.
	- 원격 프록시 : 프록시객체와 실제 로컬 객체두개가 마치 같은 주소 공간에 있는 것처럼 동작하게 한다.	
* 중간에 놓여져서 실제 실행되는 메서드 대신에 위에 3개가 돌아가며 성능 저하를 막는다.
![image](https://user-images.githubusercontent.com/56966606/169749107-03e65542-827f-4e05-b910-72851a590aa8.png)	

### 어뎁터 패턴 Adapter pattern
* 서로 호환되지 않는 다른 인터페이스를 클라이언트가 그대로 사용가능 하게한다.
* 필요로 인해서 수정할 필요가 없으니 인터페이스의 정체성을 지키고 인터페이스를 분리시킬수 있다.
![image](https://user-images.githubusercontent.com/56966606/169752856-a44f5145-0a54-452c-9f9d-8b27eb8754f4.png)
* 주로 사용하는 조립방식의 어뎁트 패턴
![image](https://user-images.githubusercontent.com/56966606/169752144-494186fa-621c-463a-b141-bcfbdcb15d36.png)
```c++
	private SearchResult convertToResult(QueryResponse response)로 Serch형식으로 반환을 맞춰준다.
```
![image](https://user-images.githubusercontent.com/56966606/169752946-82601ee2-92a7-40e0-a84b-4c5206b8fa31.png)
* 상속 방식의 어뎁트 패턴 (c++ 관련이라는 것을 참조만 할 것)
![image](https://user-images.githubusercontent.com/56966606/169752979-c3bca282-d605-403e-b2db-5d60a3a5eb22.png)
* 시험때 private에 유의하여 상속 코드 구현할 것. query는 오직 adapter 구현을 위한 인터페이스이다.
* 상속과 조립은 둘다 같은 인터페이스를 가진다. 그러나 다른점은 노출되는 인터페이스가 다르다.
* 상속으로 모든기능을 가져가면 자원 낭비니 주로 조립기능을 사용한다.


### 컴포지트 패턴 Composite pattern 중요!
* 단일화된 요소(단말)을 컴포넌트 라고 한다.
* 그룹화된 요소를 컴포지트라고 한다.
* 컴포지틀에 많은 요소를 가지고있기에 목록을 제어할 add와 remove 인터페이스가 필요하다.
* **전체 부분을 구성하는 클래스가 동일 인터페이스를 구현하며** 개별, 집합 요소를 같은 타입으로 추상화 한다. 컴포넌트 책임 중요!!
* 컴포지트 기능은 2개로 나뉜다.
	- 컴포넌트 관리
	- 컴포넌트의 기능과 인터페이스를 컴포지트에 위임하여 중복코드를 방지해야한다. (코드 잘 숙지)
* **컴포넌트 패턴 구현 고려 사항 중요!!!**
	- 컴포지트 패턴에서! 컴포넌트 객체는 메모리에 자신을 root로 트리구조를 가진다. ex.) 메뉴속에 > 메뉴, 2진 트리
	- 인터페이스를 꼭 컴포넌트에 선언할 필요는 없다.
![image](https://user-images.githubusercontent.com/56966606/171122209-8fe1e964-6bc9-4226-91c1-8ade055dc69f.png)

### 이터레이터 패턴 Iterator pattern
* 배열과 리스트 같이 순회를 목적으로 하는 객체에 유용하게 사용된다.
* 집합객체를 순차적으로 접근 할 수 있다.
* 인터페이스를 일괄적으로 제공한다.

### 싱글톤 패턴 Singleton pattern
* 프로그램 내 제한한 1개의 객체를 구성한다. ex.) 스타의 유닛 제한 
* 전역 변수를 사용하지 않고 객체를 하나만 생성 하도록하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴이다.
* 객체가 1개라는 것을 염두하며 new가 한번만 생성되어야 한다.
* 클라이언트에 제한을 가진 **생성자와 복사 생성자가 매우중요하다.** (public요소를 없는걸 확인 할 것)
* 인스턴스를 만들지않고 기능을 제공하기 위해 변수와 메서드를 static으로 만들어야 한다.
* c#과 java에 경우 enum이있고 유니티의 코루틴도 동일하겠지 뭐...
	
13일 시험문제는 개념과, 의도를 파악하고 괄호넣기, 문구작성

