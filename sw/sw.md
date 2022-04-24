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
## 템플릿메서드 template Method
* 상위 클래스에서 골격을 정의하고, 하위 클래스에서 세부 처리를 구체화 한다.
* 유사한 서브 클래스를 묶어 공통된 내용을 상위 클래스에 정의한다.
* 코드 양이 줄고 유지보수를 용이하게 해준다.