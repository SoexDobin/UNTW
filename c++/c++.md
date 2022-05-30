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

# 기말 1차시
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
class Point{
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	void SetX() { this->x = x; }
	void SetY() { this->y = y; }
	int GetX()const { return x; }
	int GetY()const { return y; }
// 연산자 중복
// 참조 붙이면 안된다.
// 일시적인 메모리가 아닌 전역으로 쓰이는 객체이기 때문이다.
	const Point operator+(const Point& arg) const{
		return Point(x + arg.x, y + arg.y);
	}
	const Point operator-(const Point& arg) const{
		return Point(x - arg.x, y - arg.y);
	}
	bool operator==(const Point& arg) const{
		return x == arg.x && y == arg.y;
	}
	const Point operator+=(const Point& arg) {
		x += arg.x;
		y += arg.y;
		return *this; //return Point(x, y);
	}
	const Point operator++() { //전위
		++x, ++y;
		return *this;
	}
	const Point operator++(int) { //후위
		Point t = *this;
		x++, y++;
		return *this;
	}
};
int main() {
	Point p1(2, 3), p2(1, 2);
	Point pp = p1 + p2; //p1.operator + p2;
	Point pm = p1 - p2; //p1.operator - p2;
	if(p1 == p2) {} //p1.operator == (p2);
	Point ppe = p1 += p2; //p1.operator += p2;
	Point ppb = ++p1; //p1.operator++(); //전위
	Point ppf = p1++; //p1.operator++(0); //후위
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
	void Add(int data) { buf[size++] = data; }
	int Size()const { return size; }
	int At(int idx) const { return buf[idx]; }
	int& operator[](int idx){ return buf[idx]; }
};
int main() {
	Array arr;
	arr.Add(10);
	arr.Add(20);
	arr[2] = 100; // arr.buf[2] = 100;
	for (int i = 0; i < arr.Size(); ++i) {
		cout << arr[i] << endl; //arr.operator[](i);
	}
}
```
* 각 오퍼레이터의 약속을 잘 기억할 것.
#기말 2차시
```c++
a.operator+(n); // 단항 연산자
operator+(a, b) // 이항 
```
```c++
x.operator()();
// 첫번쨰는 함수이름의 일부()이다.
// 두번째가 연사자 함수로써 매개변수 입력칸 연산자 기호가 된다.
```

**복사 대입 연산자 시험!**
```c++
class Array {
	int* buf;
	int size;
	int capacity;
public:
	Array(int cap = 100) :buf(nullptr), size(0), capacity(cap) {
		buf = new int[capacity];
	}
	Array(const Array& arg) { _Copy(arg); }
	const Array& operator=(const Array& arg) {
		delete[] buf;
		_Copy(arg);
		return *this;
	}
	int& operator[](int idx) { return buf[idx]; }
	~Array() { delete[] buf; }
	void Add(int data) { buf[size++] = data; }
	int Size() { return size; }
private:
	void _Copy(const Array& arg) {
		this->size = arg.size;
		this->capacity = arg.capacity;
		buf = new int[capacity];
		for (int i = 0; i < size; ++i)
			buf[i] = arg.buf[i];
	}
};
int main() {
		Array arr;
		arr.Add(10);
		arr.Add(20);
		arr.Add(30);
		for (int i = 0; i < arr.Size(); ++i)
			cout << arr[i] << endl; // arr.operator[](i)

		//복사생성자
		Array arr2 = arr;
		for (int i = 0; i < arr2.Size(); ++i)
			cout << arr2[i] << endl;

		//복사대입연산자
		Array arr3;
		arr3 = arr; //arr3.operator=(arr);
		for (int i = 0; i < arr3.Size(); ++i)
			cout << arr3[i] << endl;
}
```
* 복사 대입 연산자 operator 표기법 알아둘 것. 
* 복생과 복연의 차이점 잘 이해해두기.

**이항연산을 통한 연산자중복**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; } // 정식 출력을 위한 GetX
	int GetY()const { return y; } // 정식 출력을 위한 GetY
	friend Point operator+(const Point& a, const Point& b); //꼼수
};
Point operator+(const Point& a, const Point& b) {
	return Point(a.GetX() + b.GetX(), a.GetY() + b.GetY());
}
Point operator+(int n, const Point& pt) {
	return Point(n + pt.GetX(), n + pt.GetY());
}
int main() {
	Point a(2, 3), b(4, 5);
	Point c = a + b;
	c.Print();

	int n = 10;
	Point d = a + n; // operator+(a, n); 이건 주타입 함수가 없어서 안됨
	Point f = n + a; // operator+(n, a);
	d.Print();
	f.Print();
}
```
* 연산자 중복이 가능하다.
* 함수 만들때 매개변수 주의 할 것.

**메서드 체인으로 이항연산자 cout기능 살리기**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; } // 정식 출력을 위한 GetX
	int GetY()const { return y; } // 정식 출력을 위한 GetY
	void SetX(int x) { this->x = x; }
	void SetY(int y) { this->y = y; }
};
ostream& operator<<(ostream& out, Point& pt) {// out연산자
	out << "Point: " << pt.GetX() << ", " << pt.GetY();
	return out;
}
istream& operator>>(istream& in, Point& pt) { // input연산자
	int x, y;
	in >> x >> y;
	pt.SetX(x); pt.SetY(y);
	return in;
}
int main() {
	Point a;
	cin >> a;
	cout << a << endl;
}
```
* ostream은 const를 사용하면 안된다.
* 메서드 체인으로 인해 값변경이 일어남으로 const 제거해야한다.   
**조건자 연산자**
```c++
class MyGreater1 {
public:
	bool operator()(int a, int b)const {
		return a > b;
	}
};
class MyGreater2 {
public:
	bool operator()(int a, int b)const {
		return a < b;
	}
};
int main() {
	int arr[5] = { 5, 8, 3, 9, 6 };
	MyGreater1 m; //functor
	cout << m(5, 6) << endl;
	cout << int() << endl; //임시객체
	cout << MyGreater1()(1, 2) << endl; //임시객체
}
```
* 조건자는 참과 거짓을 bool or 정수값으로 반화하는 함수를 말한다.
# 기말 2차시
### iterator 반복자(배열 요소를 가르키는 포인터)
- 컨테이너와 컨테이너 안의 있는 요소를 구별
- 요소의 값을 확인
- 컨테이너 안에 있는 요소들 간에 이동할수 있는 연산 제공
- 컨테이너가 효과적으로 처리할 수 있는 방식으로 가용한 연산들을 한정
	+ begin() vecctor의 첫번째 요소를 가르키는 반복자 변환 
	+ end() vector의 마지막요소의 바로뒤를(빈 vector)가르키는 반복자 변환

### vector
**vector 포인터형으로 만들어 써보기**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) { }
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}

};
int main() {
	vector<Point> v;
	vector<int> n;
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);

	vector<Point>::iterator iter = find(v.begin(), v.end(), Point(3, 4));
	(*iter).Print();
}
```
* find()는 인자로 탐색할 범위와 탐색할 원소를 받는다.

**vector cmp로 불린을 통해 특정 값 찾아내기**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) { }
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}

};
bool cmp(const Point& arg){
	return arg.GetX() + arg.GetY() >= 100;
}
int main() {
	vector<Point> v;

	v.push_back(Point(2, 3));
	v.push_back(Point(3, 4));
	v.push_back(Point(555, 55));
	v.push_back(Point(5, 6));

	vector<Point>::iterator iter = find_if(v.begin(), v.end(), cmp);
	if (iter != v.end())
		(*iter).Print();
	else
		cout << "없다!" << endl;
}
```
* find_if는 특정 조건에 일치하는 원소를 탐색한다.
**state로 특정값을 검색 해보게 만들자**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}
};
struct Compare {
	int state;
	Compare(int s = 0) :state(s) { }
	bool operator()(const Point& arg) {
		return arg.GetX() + arg.GetY() >= state; //찾은값이 state랑 같거나 큰값
	}
};
int main() {
	vector<Point>v;

	v.push_back(Point(2, 3));
	v.push_back(Point(3, 4));
	v.push_back(Point(4, 5));

	vector<Point>::iterator iter = find_if(v.begin(), v.end(), Compare(9));
	if (iter != v.end())
		(*iter).Print();
	else
		cout << "없다" << endl;
}
```
**predicate가 없으면 안되는 시스템 heap할당 vector**
```c++
class Point {
	int x, y;
public:
	Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}
};
struct Compare {
	int state;
	Compare(int s = 0) :state(s) { }
	bool operator()(const Point* arg) { //조건자 함수
		return arg->GetX() + arg->GetY() >= state; //찾은값이 state랑 같거나 큰값
	}
};
int main() {
	vector<Point*>v;

	v.push_back(new Point(2, 3));
	v.push_back(new Point(3, 4));
	v.push_back(new Point(4, 5));
	v.push_back(new Point(55, 50));

	vector<Point*>::iterator iter = find_if(v.begin(), v.end(), Compare(100));
	if (iter != v.end())
		(*iter)->Print();
	else
		cout << "없다" << endl;
	for (vector<Point*>::iterator iter = v.begin(); iter != v.end(); ++iter)
		delete* iter;
}
```
### 객체의 형식 변환
**객체의 형식변환**
1. 생성자 이용
2. 형식 변환자 이용

**생성자를 이용한 객체의 형식 변한**
```c++
class Point {
	int x, y;
public:
	Point(const char* s) :x(1), y(1) {}	// 4
	Point(int _x, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}
};
int main(){
	Point p1 = Point(2, 3);	//초기화 c
	Point p2(2, 3);	// 초기화 c++
	Point p3 = 10;	//Point p3 = Point(10); 생성자 확인 해두기.
	Point p4 = "point";	//Point p4 = Point("point");

	p1.Print();
	p2.Print();
	p3.Print(); // 10. 0
	p4.Print(); // 1, 1
}
```
**형식 변환 연산자와 explicit로 명시적 형변환**
```c++
class Point {
	int x, y;
public:
	explicit Point(int _x, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
	bool operator==(const Point& arg) {
		return x == arg.x && y == arg.y;
	}
	operator int()const { // Point 형식을 int형식으로 변환 & 형식 안붙인다.
		return  x + y;
	}
	operator const char* () {
		static char buf[1000]; //함수 종료시 않없어지게 static
		sprintf_s(buf, "%d, %d", x, y);
		return buf;
	}
};
int main() {
	Point p1(2, 3);
	int n = p1; //p1.operator int();
	cout << n << endl;

	const char* str = p1;
	cout << str << endl;
}
```
* explicit 키워드는 자신이 원하지 않은 형변환이 일어나지 않도록 제한하는 키워드이다.
* explicit는 인수가 하나만 받을때 사용해야한다.
### 함수 템플릿
* Template : 클라이언트가 필요할 때마다 타입 변경을 가능하게 해준다.
* class의 Template : 자료구조에 사용
* function의 Template : 알고리즘에서 사용
* 함수 템플릿은 함수가 아니라 함수 트리라고한다.

**함수 템플릿 사용하기**
``c++
template <typename T> //진짜 함수를 만들어 낼 수 있는 함수를 함수 템플릿 이라고한다.
int Find(T lt[], int size, T key) {
	for (int i = 0; i < size; ++i)
		if (key == lt[i])
			return i;
}
class Point {
	int x, y;
public:
	explicit Point(int _x = 0, int _y = 0) :x(_x), y(_y) {}
	void Print()const { cout << x << ", " << y << endl; }
	int GetX()const { return x; }
	int GetY()const { return y; }
};
int main() {
	int arr[5] = { 5, 8, 2, 6, 3 };
	int idx = Find(arr, 5, 6); // (위치, 개수, 찾을 값)
	if (idx != -1)
		cout << idx << " : " << arr[idx] << endl;

	double darr[5] = { 5.1, 8.2, 2.3 , 6.4, 3.5 };
	idx = Find(darr, 5, 6.4);
	if (idx != -1)
		cout << idx << " : " << darr[idx] << endl;
}
```
**클래스 템플릿 사용하기**
```c++
template <typename T>
class Stack {
	T* buf;
	int top;
	int capacity;
	const Stack& operator=(const Stack& arg) { }
public:
	Stack(int cap = 100) :buf(nullptr), top(0), capacity(cap) {
		buf = new T[capacity];
	}
	Stack(const Stack& arg) :buf(nullptr), top(arg.top), capacity(arg.capacity) {
		buf = new T[capacity];
	}
	~Stack() { delete[] buf; }
	void Push(const T data) { buf[top++] = data; }
	const T& Top()const { return buf[top - 1]; } // 반환 타입에 주의하자
	void Pop() { --top; }
};
int main() {
	Stack<double> s1;

	s1.Push(10.34);
	s1.Push(20.42);
	s1.Push(30.87);

	cout << s1.Top() << endl;
	s1.Pop();
	cout << s1.Top() << endl;
	s1.Pop();
	cout << s1.Top() << endl;
	s1.Pop();
}
```
# 기말 4차시
**iterator은 모든 stl컨테이너 타입이 가지고있는 반복자이다.**
```c++
int main() {
	vector<int> v;

	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	
	// 모든 컨테이너는 iterator 클래스를 보유하고 있다.
	for (vector<int>::iterator iter = v.begin(); iter != v.end(); ++iter)
		cout << *iter << " ";
	cout << endl;
	// 연속 기반 컨테이너에서만 제공한다.
	for (vector<int>::size_type i = 0; i < v.size(); ++i)
		cout << v[i] << " ";
	cout << endl;
}
```
**내부 클래스(iterator)는 외부 클래스(Array)만의 클래스가 된다.**
```c++
class Array { //외부 클래스
public:
	class Iterator { // 내부 클래스
	public:
		void Print()const { cout << "iterator" << endl; }
	};
	typedef Iterator Iterator2; // 내부클래스(내부 정의 형식)
};
int main() {
	Array arr;
	Array::Iterator iter1;
	Array::Iterator2 iter2;

	iter1.Print();
	iter2.Print();
}
```
* iterator는 지역 클래스로써 사용 가능하다.
**살짝 중요! vector에 Person 주소타입 넣어보기**
```c++
class Person {
public:
	void Print()const { cout << "Person" << endl; }
};
int main() {
	vector<Person*> v;

	v.push_back(new Person());
	v.push_back(new Person());
	v.push_back(new Person());

	for (vector<Person*>::iterator iter = v.begin(); iter != v.end(); ++iter)
		(*iter)->Print();
	for (vector<Person*>::iterator iter = v.begin(); iter != v.end(); ++iter)
		delete* iter;
}
```
* 주의점은 리턴 값에 지역객체 반환은 함수 실해시 없어지기에 쓰면 안된다.
* 중요!! 주소 타입일 경우 new 선언을 통해 접근해야한다.
* new가 사용되면 delete는 필수!
**Array배열과 연산자중복으로 At()메서드 간단히 만들기**
```c++
class Array {
	int* buf;
	int size;
	int capacity;
	Array(const Array& arg);
	const Array& operator=(const Array& arg);
public:
	Array(int cap = 100) :buf(nullptr), size(0), capacity(cap) {
		buf = new int[capacity];
	}
	~Array() { delete[] buf; }
	void Add(int data) { buf[size++] = data; }
	int Size()const { return size; }
	int At(int idx)const { return buf[idx]; } 
	int operator[](int idx)const { return At(idx); } // At()연산자 중복
};
int main() {
	Array arr;
	arr.Add(10);
	arr.Add(20);
	arr.Add(30);
	for (int i = 0; i < arr.Size(); ++i)
		cout << arr[i] << endl;
}
```
**template로 사용자 지정 템플릿클래스로 만들기**
* template로 Array객체에 Person 형식으로 출력하는것이 핵심이다.
```c++
template <typename T> 
class Array {
	T* buf;
	int size;
	int capacity;
	Array(const Array& arg);
	const Array& operator=(const Array& arg);
public:
	Array(int cap = 100) :buf(nullptr), size(0), capacity(cap) {
		buf = new T[capacity];
	}
	~Array() { delete[] buf; }
	void Add(const T& data) { buf[size++] = data; }
	int Size()const { return size; }
	const T& At(int idx)const { return buf[idx]; }
	const T& operator[](int idx)const { return At(idx); }
};
class Person {
	string name;
	string phone;
public:
	Person(const string& n = "", const string& ph = "") :name(n), phone(ph) {}
	const string& GetName()const { return name; }
	const string& GetPhone()const { return phone; }
	void Print()const {
		cout << "name: " << name <<
			", " << "phone: " << phone << endl; }
};
int main() {
	Array<Person*> arr;
	arr.Add(new Person("Lee", "010-1234-1234"));
	arr.Add(new Person("kim", "010-4566-6968"));
	arr.Add(new Person("Bak", "010-8984-5485"));
	for (int i = 0; i < arr.Size(); ++i)
		arr[i]->Print();
	cout << endl;
	for (int i = 0; i < arr.Size(); ++i)
		delete arr[i];
}
```
**typeinfo를 통한 객체타입 비교**
* 부모 타입 객체들 중에서 타입검사와 다운 캐스팅을 통해
* 필요한 자식 객체를 걸러내어 사용한다.
* ex.) 광전사와 고위기사가 있으면 고위기사의 Ui에 스톰이 아이콘이 뜨는 경우 
```c++
// typeinfo를 통한 객체타입 비교
int main() {
	int n = 10;
	if (typeid(int) == typeid(n))
		cout << "true" << endl;

	const type_info& ti = typeid(int);
	const type_info& ti2 = typeid(n);
	cout << ti.name() << endl;
	cout << ti.name() << endl;

	if (ti == ti2)
		cout << "true" << endl;
}
```
**부모 자식의 타입검사 후 다운 캐스팅을 통한 호출**
```c++
class Parent {
public:
	virtual void Print()const = 0;
};
class Child1 : public Parent {
public:
	void Print()const { cout << "Child1" << endl; }
};
class Child2 : public Parent {
public:
	void Print()const { cout << "Child2" << endl; }
	void PrintChild2()const { cout << "PrintChild2()" << endl; }
};
int main() {
	Parent* arr[4] = { new Child1, new Child2,  new Child1,  new Child2 };
	for (int i = 0; i < 4; ++i) {
		if (typeid(*arr[i]) == typeid(Child2)) {
			((Child2*)arr[i])->PrintChild2();// 매우 중요 코드!!
		}
	}
}
```
* 타입 비교후 호출 코드를 잘 이해해 둘 것.
![image](https://user-images.githubusercontent.com/56966606/170908057-7f6fc87f-899d-40c6-8638-50deb47fe52a.png)

# 기말 5차시
6월 20일 시험
**c++언어의 타입케스트**
1. static_cast : 정적 형식변환
	* 수치
	* 계층구조 형식변환
2. const_cast : const형식 타입의 const를 제거똔느 주입하는 형변환 하기위해사용한다.
	* 포인트 형식끼리만 가능하다. 참조는 되지만 안한다.
3. reinterpret_cast : 임의 포인터 타입끼리 형변환을 해준다.
	* 전혀 상관없는 타입끼리 가능하다.
4. dynamic_cast : 동적인 형식변환
	* 포인터 또는 참조 타입을 컴파일 하면서 타입 케스팅을 시켜준다.

* 자식이 구체화된 타입을 가지고있을떄 형변환을 & 다운케스팅 반대는 업케스팅

**정적 형식변환 static_cast**
```c++
int main() {
	int n = 10;
 	double d = 3.3;

 	n = (int)d;
 	n = static_cast<int>(d);
 	cout << n << ", " << d << endl;
}
```

**말도 안되는 형식변환에는 reinterpret_cast**
```c++
class Parent {};
class Child : public Parent {};
int main() {
	int n = 0x41424344;
	//char* pc = (char*)&n; //c의 형변환

	char* pc = reinterpret_cast<char*>(&n);
	cout << pc[0] << endl;
	cout << pc[1] << endl;
	cout << pc[2] << endl;
	cout << pc[3] << endl;
}
```

**상수 케스팅 const_cast**
```c++
class Parent {};
class Child : public Parent {};
int main() {
	int n = 100;
	const int* cp = &n;
	// int* p = (int*)cp; // c언어 케스팅
	int* p = const_cast<int*>(cp);
	cout << *cp << endl;
}
```

**주로 자식 객체로 다운케스팅 되는지 확인할때 사용하는 dynamic_cast**
```c++
class Parent {
public:
	virtual void Print()const = 0;
};
class Child1 : public Parent {
public:
	virtual void Print()const {
		cout << "Child1" << endl;
	}
};
class Child2 : public Parent {
public:
	virtual void Print()const {
		cout << "Child2" << endl;
	}
	void PrintChild2()const {
		cout << "PrintChild2" << endl;
	}
};
int main() {
	Parent* p = new Child2;
	Child2* c2 = dynamic_cast<Child2*>(p);
	if (c2 != nullptr)
		c2->PrintChild2();
	else
		cout << "null" << endl;
}
```
## STL(Standard Template Library)
1. 컨테이너 : 객체를 담는 객체
	* 연관(association) 컨테이너 : 자동 정렬 규칙
		- map_multi : 노드기반
		- set_multi : 노드기반
	* 순차(sequence) 컨테이너 : 원소 상대 순서
		- vector : 배열기반
		- deque : 배열기반
		- list : 노드기반
2. 반복자 : 컨테이너 원소를 순회하는 객체
3. 알고리즘 : stl템플릿 함수
4. 함수객체
**위에 4개는 c++ 필수요소**
5. 어뎁터
6. 할당기
 
****
```c++
struct IntPrinter {
	string mark;
	IntPrinter(const string& s = ""): mark(s) { }
	void operator(int data)const {
		cout << data << mark;
	}
};
int main() {
	vector<int> v; // 1. 컨테이너
	v.push_back(40);
	v.push_back(10);
	v.push_back(20);
	v.push_back(70);
	v.push_back(90);

	// 2. 알고리즘
	for_each(v.begin(), v.end(), IntPrinter("")); cout << endl; // 4. 함수객체
	sort(v.begin(), v.end(), greater<int>()); // 4. 함수 객체이면서 (2항 predicate)
	for_each(v.begin(), v.end(), IntPrinter("")); cout << endl; // 4. 함수객체

	// 3. 반복자
	for (vector<int>::const_iterator iter = v.begin();
		iter != v.end(); ++iter)
		cout << endl;
}
```
