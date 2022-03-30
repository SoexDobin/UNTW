# untw
#1 Stack, Queue, Heap
  1.1 Stack
  후입선출방식으로 가장 나중에 메모리에 할당된 데이터가 먼저 빠져나감
  프로그램 전역변수, 정적변수가 저장되는 영역이다. 컴파일전에 실행
  1.2 Queue
  선입선출방식으로 가장 먼저 메모리에 할당된 데이터가 먼저 빠져나감
  1.3 Heap
  이진트리 자료구조 최대, 최소 값을 찾아내는 연산을 잘함
  Node 비선형메모리 형태가 예시를 가짐
#2 new, delete 동적메모리(Heap) 할당
  1.1 new 
    
  1.2 delete 
#3차시
  int main() {
    Point pt(2, 3);
    // stack영역 Point의 객체 pt생성

    Point* p = nullptr;
    // stack영역 Point의 주소객체 p생성하고 nullptr로 초기화

    p = new Point(4, 5);
    // *p는 heap동적 메모리영역에 할당
    
    pt.Print();
    p->Print();

    delete p; 
    // 할당된 p메모리 제거 }

  인터페이스부에 객체를 참조 받을때는
  무조건 const 를 붙여야함 ex)void Print(const Point& arg)
  const와 &를 빼먹고 받아올 경우 값복사가 일어남 효율적이지 않음

  void Print() const { //const 메소드
    cout << x << y << endl; }
  void Set(int _x){ //비const 메소드
  x = _x; }
  int main() {
    Point p1; 
    // R, W (mutable)
    const Point P2; 
    // R (Imutable)
    
    pt.Print(); //R
    p->Print(); //R }
  c++에서는 비const 객체를 통해 setter이외에는 객체 변경을 불가능하게 하자 약속함
  반대로 const 객체는 그냥 변경 불가능 

  c++ 빈클래스 정의시 함수4개가 기본정의됨 (중간고사)
  1. default 생성자 T(){}
  Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}

  2. default 소멸자 ~T(){}
  ~Point(){}

  3. default 복사 생성자 T(const T&){}
  Point(const Point& = arg){}
  객체복사 shallow copy & deep copy
  둘다 속성만 복사함 ex.변수값 함수들은 논리적으로 실행되기에 속성만 이루어짐
  shallow copy는 객체의 값속성 복사(값복사)
  값속성만 가진 클래스를 객체복사호출하면 문제x (int x;)
  하지만 주소속성을 객체복사하면 같은 메모리를 참조하기 때문에 문제발생 (int* px;)
  deep copy는 객체의 참조속성을 복사
  class Point{ //좋은 코드는 아님
    int* px = nullptr;
    int* py = nullptr;
  public:
    Point (int _x = 0, int _y = 0){
    px = new int(_x);
    py = new int(_y); }
    ~Point(){ 
      delete px;
      delete py; }
    Point (const Point& arg) { //사용자 정의 복사 생성자를 만들어야함 (중간)
      px = new int();
      *px = *arg.px;
      py = new int();
      *py = *arg.py; }
  int main(){ 
    Point p1(2, 3);
    Point p2(p1); }

  4. default 복사 대입연산자 const T& operator = (const T&){ return this; }
  == 모던c++ 추가사항 (의미없는 객체들을 효율적으로 다루기위해서)
  5. 이동 생성자
  6. 이동 대입 연산자

 
