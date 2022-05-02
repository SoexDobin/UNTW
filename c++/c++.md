# untw
# 1 Stack, Queue, Heap
1. Stack
후입선출방식으로 가장 나중에 메모리에 할당된 데이터가 먼저 빠져나감
프로그램 전역변수, 정적변수가 저장되는 영역이다. 컴파일전에 실행
2. Queue
선입선출방식으로 가장 먼저 메모리에 할당된 데이터가 먼저 빠져나감
3. Heap
이진트리 자료구조 최대, 최소 값을 찾아내는 연산을 잘함
Node 비선형메모리 형태가 예시를 가짐
# 다형성
* 함수 중복 overloading
* overriding 상속 받은 메서드 재정의
**시험 public 메소드의 시그니쳐 == 인터페이스 == 퍼블릭 클래스의 인스턴스**

# 1차시
* 기본
```c++
int main() {
  int a1 = 10; // 변수 할당 법
  int a2(20); // 객체 할당 법

	int* pn2 = (int*)new int;
	*pn2 = 200;
	cout << *pn2 << endl;
	delete pn2;
}
```
* c++의 구조체 정의
```c++
struct Data{
  int n;
  double d;
};
void PrintData(Data arg){
  cout << arg.n << ", " << arg.d << endl;
}
int main(){
  Data d1 = { 5, 10.5 };
  PrintData(d1);
}
```
**참조와 포인터**
* (*)와 (&)둘다 주소위치를 표현한다.
* pointer와 reference라고 한다.
* 참조는 초기화시에만 가능하다.
```c++
int n = 10;
int* p = &n;
int& r = n;
//모두 같은 주소를 가르키고 있다.
//참조를 통한 값 변경
void Swap(int& pa, int& pb) {
	int t = pa;
	pa = pb;
	pb = t;
}
int main() {
	int a = 10, b = 20;
	cout << a << ", " << b << endl;
	Swap(a, b);
	cout << a << ", " << b << endl;
}
```
**중요 const R, W매개변수 설정**
* 아웃파라미터 같은 변경 목적은 const를 안붙인다.
* 인파라미터는 변경 목적이 아니기에 const를 붙여야 한다.
```c++
void Increment(int& pn) {//출력 매개변수(out parameter)
	++pn; // pn = pn + 1
}
void Print(const int& pn) { //입력 매개변수(in parameter)
	cout << pn << endl;
}
int main() {
	int num = 1;
	Increment(num); // R, W
	Print(num); // R
}
```
* R, w요소가 R요소로 사용가능하지만 R요소가 R, W요소가 될 순 없다.
```c++
int n = 10; //R, W
const int* p = &n;// R
int* p2 = p; // 이건 오류
```
# 2차시
* 정적 요소: 상태값 (프로퍼티 ex.n = 1)
* 동적 요소 : 상태의 변화 (메서드)
* 객체지향은 이 두가지 속성과 메서드를 가진다.
* c++객체는 멤버변수와 멤버함수를 가진다.
```c++
class Point{
public:
  int x, y; //Type 정의! 중요
};
int main(){
  Point pt1 = {1, 2};
  // Type pt1메모리생성
}
```
* 객체는 항상 (정의)를 보고 만들어 진다.
* 클래스는 객체들의 공통된 개념정의
**중요!!! 인스턴스**
* 클래스 --인스턴스-> 객체
  + 클래스의 인스턴스는 객체이다.
* 프로그램의 --인스턴스-> 프로세스

**중요!! 객체의 값복사**
```c++
Point p = 10;
```

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
* 인터페이스부에 객체를 참조 받을때는 무조건 const 를 붙여야함 ex)void Print(const Point& arg)
* const와 &를 빼먹고 받아올 경우 값복사가 일어남 효율적이지 않음
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

* string 사용자 함수 
```c++
class String {
	char* buf;
public:
	String(const char* s = "") {
		buf = new char[strlen(s) + 1];
		strcpy_s(buf, strlen(s) + 1, s);
	}
	const char* c_str()const { 
		return buf;
	}
	void append(const char* s) {
		size_t sz = strlen(s) + strlen(buf) + 1;
		char* t = new char[sz];
		strcpy_s(t, strlen(buf) + 1, buf);
		strcat_s(t, sz, s);
		delete[] buf;
		buf = t;
	}
	~String() {
		delete[] buf;
	}
	int compare(const char* s)const { 
		return strcmp(buf, s);
	}
};
int main() {
	String s="GEee";

	cout << s.c_str() << endl;
	s.append("A");
	cout << s.c_str() << endl;
	if (s.compare("GEeeA") == 0) { // 0, 1 불린값 반환
		cout << true << endl;
	}
	else {
		cout << false << endl;
	}
}
```
* strcpy_s(): 문자열복사 string copy 문자열 끝에는 반드시 NULL
	- 참조위치랑, 문자열길이값, 넣을 문자열을 받는다.
* strlen() 문자열길이리턴 문자열 끝 NULL\0값을 제외하고 계산
	- 반환할 문자열을 받는다. 
* strcat_s(): 문자열 붙이기 위 특성과 비슷하다.
	- 넣을 위치, 문자사이즈 , 넣을 문자열을 매개변수로 가진다.
* strcmp(): 문자열 비교 매개변수로 비교할 문자열을 받고 불린값을 반환한다.

## Vector
* Vector
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
* Vector로 Point클래스 메모리 할당
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print() const{
		cout << x << ", " << y << endl;
	}
};
class PointVector {
   Point* buf;
   int sz;
   int capacity;
   const PointVector& operator = (const PointVector&);
public:
   PointVector(int cap = 100) :buf(nullptr), sz(0), capacity(cap) {
       buf = new Point[capacity];
   }
   PointVector(const PointVector& arg) :buf(nullptr), sz(arg.sz), capacity(arg.capacity) {
       buf = new Point[capacity];
       for (int i = 0; i < sz; ++i)
           buf[i] = arg.buf[i];
   }
   ~PointVector() { delete[] buf; }
   void Add(const Point& data) {
       if (sz < capacity)
           buf[sz++] = data;
   }
   int Size() { return sz; }
   const Point& At(int idx)const { return buf[idx]; }
};
int main() {
   PointVector ptVector; // vector<Point>

   ptVector.Add(Point(1, 2));
   ptVector.Add(Point(2, 3));
   for (int i = 0; i < ptVector.Size(); ++i) {
       const Point& pt = ptVector.At(i);
       pt.Print();
  }
}
```
* Vector로 Point주소클래스 메모리 할당
```c++
class Point
{
    int x, y;
public:
    Point(int _x = 0, int _y = 0) :x(_x), y(_y) { }
    void Print()const {
        cout << x << "," << y << endl;
    }
};
class PointptrVector {
    typedef Point* PPoint;
    PPoint* buf;
    int sz;
    int capacity;
    const PointptrVector& operator = (const PointptrVector&);
public:
    PointptrVector(int cap = 100) :buf(nullptr), sz(0), capacity(cap) {
        buf = new PPoint[capacity];
    }
    PointptrVector(const PointptrVector& arg) :buf(nullptr), sz(arg.sz), capacity(arg.capacity) {
        buf = new PPoint[capacity];
        for (int i = 0; i < sz; ++i)
            buf[i] = arg.buf[i];
    }
    ~PointptrVector() { delete[] buf; }
    void Add(const PPoint& data) {
        if (sz < capacity)
            buf[sz++] = data;
    }
    int Size() { return sz; }
    const PPoint& At(int idx)const { return buf[idx]; }
};
int main()
{
    PointptrVector ptVector; // vector<Point*>

    ptVector.Add(new Point(2, 3));
    ptVector.Add(new Point(3, 4));
    for (unsigned i = 0; i < ptVector.Size(); ++i) {
        const Point* p = ptVector.At(i);
        p->Print();
    }
    for (unsigned i = 0; i < ptVector.Size(); ++i) {
        delete ptVector.At(i);  //동일 레벨에서 delete
    }
}
```

* 객체지향 3요소와 추상화
```c++
class Person {
protected:
	string name;
	int age;
public:
	Person(const string& n = "", int a = 0) : name(n), age(a){ 
		cout << "Person()" << endl;
	}
	~Person(){ cout << "~Person()" << endl; }
	virtual void Print()const { cout << "name: " << name << " age: " << age << endl; } //별표세개 매우중요!!!!!!!!!!!!!!!!!
	const string& GetName() const { return name; }
	int GetAge() const { return age; }
};
class Student : public Person {
	int grade;
public:
	Student(const string& n = "", int a = 0, int g = 0) : Person(n, a), grade(g) {
		cout << "Student()" << endl;
	}
	~Student(){ cout << "~Student()" << endl; }
	virtual void Print()const { cout << "name: " << name << " age: " << age << " grade: " << grade << endl; }
	int GetGrade() const { return grade; }
};

class Professor : public Person {
	string position;
public:
	Professor(const string& n = "", int a = 0, const string& pos = "") : Person(n, a), position(pos) {
		cout << "Professor()" << endl;
	}
	~Professor(){ cout << "~Professor()" << endl; }
	virtual void Print() const { cout << "name: " << name << " age: " << age << " position: " << position << endl; }
	const string& GetPostion() const { return position; }
};
int main() {
	모든 학생과 교수는 사람(Person)이다 부모 클래스 형식
	{
		Student s1("김수아", 29, 3);
		Professor pr("아잉이", 30, "교수");

		Person per1 = s1;
		Person per2 = pr; //x

		Person& r1 = (Person&)s1;
		Person& r2 = pr; // o
		(Student&)r1.GetName();

		Person* p1 = (Person*)&s1;
		Person* p2 = &pr; // o
		((Student*)p2)->GetGrade();
	}
	{
		Student s1("김수아", 29, 3);
		Professor pr("아잉이", 30, "교수");
		Person* r1 = &s1;
		cout << r1->GetName() << endl;
		r1->Print(); //*** 동적 바인딩!!!!!!!!!!!!!!!!!!!!!!!!!!
		r1 = &pr;
		r1->Print();
	}
	{
		Person* parr[5] = { new Student("홍길동", 24, 2), new Professor("김교수", 40, "조교수"),
			new Student("장길신", 27, 4), new Professor("성춘향", 48, "조교수"), new Student("루시드", 18, 1) };
		for (int i = 0; i < 5; ++i) {
			parr[i]->Print();
		}
	}
}
```




* binding : 연결하다.
	- virtual을 통한 실행할때 객체 타입을 파악하여 동적할당
* compiletime : static
	- 정적 할당
* runtime : dynamic
	- 동적 할당
* 추상클래스는 구체화를 위해 사용된다.
	- 인스턴스화가 목적이 아니다. & 사용도 안된다.
	- 순수가상함수는 무조건 상속, 오버라이딩 되어야 한다.

**중요 연산자 중복**
* 연산자 중복
```c++
class Point {
	int x, y;
public:
	Point(int x = 0, int y = 0) :x(x), y(y) {}
	void Print()const { cout << x << ", " << y << endl; }
	void SetX(int x) {
		this->x = x;
	}
	void SetY(int y) {
		this->y = y;
	}
	int GetX()const { return x; }
	int GetY()const { return y; }
	const Point operator+(const Point& arg) const {
	// 참조 붙이면 안된다.
	// 일시적인 메모리가 아닌 전역으로 쓰이는 객체이기 때문이다.
		return Point(x+arg.x, y+arg.y);
	}
};
int main() {
	Point p1(2, 3), p2(4, 5);
	Point p3 = p1 + p2; //p1.operator+(p2); // p1 + p2
	p3.Print();
}
```
```c++
class Point {
	int x, y;
public:
	Point(int x = 0, int y = 0) :x(x), y(y) {}
	void Print()const { cout << x << ", " << y << endl; }
	void SetX(int x) {
		this->x = x;
	}
	void SetY(int y) {
		this->y = y;
	}
	int GetX()const { return x; }
	int GetY()const { return y; }
	const Point operator+(const Point& arg) const {
		// 참조 붙이면 안된다.
		// 일시적인 메모리가 아닌 전역으로 쓰이는 객체이기 때문이다.
		return Point(x + arg.x, y + arg.y);
	}
	bool operator==(const Point& arg)const {
		return x == arg.x && y == arg.y;
	}
	const Point& operator+=(const Point& arg) {
		x += arg.x;
		y += arg.y;
		return *this; // Point(x, y)
	}
	const Point operator++() { // ++n 전위
		++x;
		++y;
		return *this;
	}
	const Point operator++(int ) { //n++ 후위
		Point t = *this;
		++x;
		++y++;
		return *this;
	}
};
int main() {
	Point p1(2, 3), p2(4, 5);
	p2 = p1++; // p1.operator++(0);후위 // p1.operator++(); 전위
	p1.Print();
	p2.Print();
}
```
* 배열 연산자 
```c++
class Array {
	int* buf;
	int size;
	int capacity;
public:
	Array(int cap = 100):buf(nullptr), size(0), capacity(cap) {
		buf = new int[capacity];
	}
	~Array() { delete[] buf; }
	void Add(int data) {
		buf[size++] = data;

	}
	int Size()const {
		return size;
	}
	int At(int idx) const {
		return buf[idx];
	}
	int& operator[](int idx){ return buf[idx]; }
};
int main() {
	Array arr;
	arr.Add(10);
	arr.Add(20);
	arr.Add(30);
	arr[2] = 100; // arr.buf[2] = 100;
	for (int i = 0; i < arr.Size(); ++i) {
		cout << arr[i] << endl; //arr.operator[](i);
	}
}
```
* 각 오퍼레이터의 약속을 잘 기억할 것.
