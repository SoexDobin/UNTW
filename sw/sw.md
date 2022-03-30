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
  *어떤 클래스가 다른클래스에 의존하는지 빠르게 파악가능하다.
  *단! 칠판에 그리고 없앨수 있을만큼 간단해야 한다.
  *반복하여 그리고 차근차근 진행해야한다.
 
## 클래스다이어그램
![Alt Text](C:\Users\a9018\Desktop\UNTW\sw\refPicture\classDiagram.png)
박스를 클래스라고한다.   
화살표는 관계를 맺는다고한다.   
클래스안에를 나누어 중요한 함수 or 변수를 표현한다.   
클래스내 함수는 +를 붙인다.   
-TreeMap 클래스   
  -박스안에는 add()클래스와 get()클래스 2개를 담고있다.   
    -add()는 key와value값을 받는다.   
    -get()은 key값을 받는다.   
-TreeMapNode 클래스   
  -TreeMapNode는 참조변수로써 topNode라고한다.   
  -박스안에는 add()클래스와 find()클래스 2개를 담고있다.   
    -add()는 key와value값을 받는다.   
    -find()은 key값을 받는다.   
    -nodes로 인스턴스를 2개 를 받는다.   
-itskey라는 요소로 인터페이스 Comparable()클래스에 접근한다.   
-itsvalue라는 요소로 Object()클래스에 접근한다.   
## 객체다이어그램
![Alt Text](C:\Users\a9018\Desktop\UNTW\sw\refPicture\objectDiagram.png)
시스템 실행중 어느 순간의 객체와의 관계를 포착해 보여준다.   
박스안에 :와 밑줄을 써서 표현한다. ex. :<u>TreeMap</u>   
화살표는 link 연결이라고한다.   
"-"는 감추어져있는 private멤버 변수이다.   
-TreeMap 객체   
-TreeMapNode   
  -TreeMap객체는 참조형식으로써  TreeMapNode객체의 topNode라고한다.   
  -프라이빗변수 itsKey는 "Martin"이라는 값을 가진다.   
    *nodes[LESS]배열과 nodes[GREATER]배열 두 배열은 itsKey="Martin"이 참조하고 있다.   
## 상태다이어그램
![Alt Text](C:\Users\a9018\Desktop\UNTW\sw\refPicture\stateDiagram.png)
유한 상태 기계를 나타내기위한 다이어그램이다.   
상태는 둥근사각형으로 감싼다.   
화살표는 transition 전이라고한다.   
*전이의 좌측은 이벤트라고한다.   
+전이의 우측은 이벤트 발생시 수행되는 행동이라고한다.   
  *pass하면 Alarm을 울리겠다.   

