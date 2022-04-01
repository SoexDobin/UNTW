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
1. 행위를 제일 먼저 생각하여 다이어그램을 짜본다.
2. 구조를 점검한다.
  * ㅋ
 
## 클래스다이어그램
![classDiagram](https://user-images.githubusercontent.com/56966606/161099775-fc161555-3026-4680-93c7-a93d091f5ce6.png)
박스를 클래스라고한다.     
-->는 관계를 맺는다고한다.     
클래스안에를 나누어 중요한 함수 or 변수를 표현한다.   
클래스내 함수는 +를 붙인다.   
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
시스템 실행중 어느 순간의 객체와의 관계를 포착해 보여준다.   
박스안에 :와 밑줄을 써서 표현한다. ex. :<U>TreeMap</U>   
-->는 link 연결이라고한다.   
"-"는 감추어져있는 private멤버 변수이다.   
* TreeMap 객체   
* TreeMapNode   
  - TreeMap객체는 참조형식으로써  TreeMapNode객체의 topNode라고한다.   
  - 프라이빗변수 itsKey는 "Martin"이라는 값을 가진다.   
  - nodes[LESS]배열과 nodes[GREATER]배열 두 배열은 itsKey="Martin"이 참조하고 있다.   
## 상태다이어그램
![stateDiagram](https://user-images.githubusercontent.com/56966606/161100249-3195415a-f56b-4996-84f7-2155caf428eb.png)
유한 상태 기계를 나타내기위한 다이어그램이다.   
상태는 둥근사각형으로 감싼다.   
-->는 transition 전이라고한다.   
* 전이의 좌측은 이벤트라고한다.   
* 전이의 우측은 이벤트 발생시 수행되는 행동이라고한다.   
  - pass하면 Alarm을 울리겠다.   
## 시퀀스 다이어그램(절차) == 커뮤니케이션 다이어그램(객체) 
![comunicateDiagram](https://user-images.githubusercontent.com/56966606/161102339-898e5a45-0228-44e4-ba8e-5d577ce29013.png)
시간에 따른 변화에 포커스르 두지만 절차에 집중하면 시퀀스이고 
객체 중점이면 커뮤니케이션 으로 나눈다.   
-->는 메세지를 보낸다.
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
