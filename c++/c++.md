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
# 3차시
```c++
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
```
  인터페이스부에 객체를 참조 받을때는
  무조건 const 를 붙여야함 ex)void Print(const Point& arg)
  const와 &를 빼먹고 받아올 경우 값복사가 일어남 효율적이지 않음
```c++
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
```
  c++에서는 비const 객체를 통해 setter이외에는 객체 변경을 불가능하게 하자 약속함
  반대로 const 객체는 그냥 변경 불가능 

  **c++ 빈클래스 정의시 함수4개가 기본정의됨 (중간고사)**
1. default 생성자 T(){}
```c++
  Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
```
2. default 소멸자 ~T(){}
```c++
  ~Point(){}
```
3. default 복사 생성자 T(const T&){}
```c++
  Point(const Point& = arg){}
```
객체복사 shallow copy & deep copy   
둘다 속성만 복사함 ex.변수값 함수들은 논리적으로 실행되기에 속성만 이루어짐   
shallow copy는 객체의 값속성 복사(값복사)   
값속성만 가진 클래스를 객체복사호출하면 문제x (int x;)   
하지만 주소속성을 객체복사하면 같은 메모리를 참조하기 때문에 문제발생 (int* px;)   
deep copy는 객체의 참조속성을 복사   
```c++
  class Point{ //좋은 코드는 아님
    int* px = nullptr;
    int* py = nullptr;
  public:
    Point (int _x = 0, int _y = 0){
    px = new int(_x);
    py = new int(_y); 
    }
    ~Point(){ 
      delete px;
      delete py;
    }
    Point (const Point& arg) { //사용자 정의 복사 생성자를 만들어야함 (중간)
      px = new int();
      *px = *arg.px;
      py = new int();
      *py = *arg.py; 
    }
  }
  int main(){ 
    Point p1(2, 3);
    Point p2(p1); 
  }
```
  4. default 복사 대입연산자 const T& operator = (const T&){ return this; }
  == 모던c++ 추가사항 (의미없는 객체들을 효율적으로 다루기위해서)
  5. 이동 생성자
  6. 이동 대입 연산자

# 4차시
## namespace
* using namespace std; 선언을 안할 경우 3가지
```c++
std::cout << x << std::endl;
//::연산자 사용에 유의할 것
```
* 직접 namespace를 만들어 사용할 수 있다.
```c++
namespace Alpha {
	class Move {
		const char a[14] = "CH24485-31283";
	public:
		void Print() { cout << "좌표: " << a << endl; } }; }
namespace Bravo {
	class Move {
		const char b[14] = "CG24135-31078";
	public:
		void Print() { cout << "좌표: " << b << endl; } }; }
using Bravo::Move;      // 1. 네이밍 지정
using namespace Bravo;  // 2. 네임스페이스 지정      
int main() {
	Alpha::Move r1;       // 3. 직접 지정
	Move r2;
	r1.Print();
	r2.Print();
}
```
* 1.네임스페이스 로컬요소를 꺼낼 경우
* 2.네임스페이스 자체를 가져와서 사용할 경우
* 3.직접 ::연산자로 지정하는 경우
```c++
namespace MyNameA {
	int x = 10;
	void Print(int n) { cout << "n: " << n << endl; }
	struct Data { int k; };
}
int main() {
	MyNameA::Data d = { 200 };
	MyNameA::Print(100);
	cout << MyNameA::x << endl;
	cout << d.k << endl;
}
```
* 직접 네임 스페이스로 값을 가져올 수 있다.

* 복사생성자 re
```c++
class Point { 
	int x;
	int* py;
public: 
	Point(int _x = 0, int _y = 0): x(_x), py(nullptr){
		py = new int(_y); }
	//nullptr 주소값이 아무것도 안가르킨다는 것을 명시
	Point(const Point& arg) : x(arg.x), py(nullptr) {
		py = new int(*arg.py);
	}
	~Point(){ delete py; }
	void Print() { cout << x << ", " << *py << endl; }
};
int main() {
	Point pt1(1, 2);
	pt1.Print();
	Point pt2 = pt1;
	pt2.Print();
	//참조 객체 상태인 깊은 복사 실행
}
```
* 주소의 값을 가져올땐 참조해온다는것을 명시!!

* this에 대해서 알아보자
```c++
struct Data {
	int a, b, c;
	void SetData(int a, int b, int c) {
		this->a = a; // this > Data
		b = b;
		c = c;
	}
	void PrintData() {
		printf("%p %d %d %d\n", this, this->a, b, c);
    // 숨겨진 매개변수로 이미 객체주소를 받아 온다는 것을 알 수 있다.
	}
};
int main() {
	Data d1 = { 1,2,3 };
	d1.SetData(10, 50, 90);
	d1.PrintData();	//PrintData(&d1);
                  // 보이진 않지만 객체의 주소값은 인수로 넘겨줌                 
}
```
* this 객체가 호출될때 그 자신의 주소값을 넘겨준다.
* 객체의 주소값은 인수로 넘겨줌 PrintData(&d1);

* typedef문법
```c++
typedef int I;
typedef int* PI;
typedef int** PPI;
int main() {
	int a = 10;
	int* pa = &a;
	int** ppa = &pa;
	I b = 20;
	PI pb = &b;
	PPI ppb = &pb;
	cout << a << ", " << *pa << ", " << **ppa<< endl;
	cout << b << ", " << *pb << ", " << **ppb << endl;
}
```
* 자료형의 이름이 긴 경우 자료형을 재정의한다.

* Vector와 복사생성자
```c++
class IntVector {
	int* buf;
	int size;
	int capacity;
	const IntVector& operator = (const IntVector&);
public:
	IntVector(int cap) :size(0), buf(nullptr), capacity(cap) {
		buf = new int[capacity]; }
	IntVector(IntVector& pv)      // 복사 생성자
  :size(pv.size), buf(nullptr), capacity(pv.capacity) {
		buf = new int[capacity];
		for (int i = 0; i < capacity; i++)
			buf[i] = pv.buf[i];}
	~IntVector() { delete[] buf; }// 복사 소멸자
	void Add(int data) {
		if (size < capacity) {
			buf[size++] = data; }
		else {
			throw "배열의 용량을 넘었다.";} }
	int Size()const { return size; } // vector의 기본 함수
	int At(int idx)const { return buf[idx]; }
};
int main()
{
	IntVector v(1000);
	v.Add(10); v.Add(20); v.Add(30); v.Add(40); v.Add(50);
	for (int i = 0; i < v.Size(); i++) {
		cout << v.At(i) << endl; }
	IntVector v2(v);
	for (int i = 0; i < v2.Size(); i++) {
		cout << v.At(i) << endl; }
}
```
* 