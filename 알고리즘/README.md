# 알고리즘
## 문법
#### 참조방법
``` c++
int main(){
  int n = 10;
  int* p1 = &n; // c언어 참조법 c++에서는 포인터
  int& p2 = n // c++언어 참조
}
```
모두 같은 주소값을 가지며 n을 참조한다. 
#### 클래스와 구조체
* 구조체
``` c++
struct Point{
  int x, y;
};
void Print(Point* p){
  printf("&d %d\n", p->x, p->y)
}
void Print(Point& r){
  cout << x << " " << y << endl;
}
int main(){
  Point pt = (1, 2); //구조체 객체 선언
  Print(&pt); //c
  Print(pt); //c++
}
```
* 클래스
``` c++
class Point{
  int x, y;
public:
  Point(int _x, int _y) { x = _x; y = _y; }
  void Print(){ printf("&d %d\n", x, y) }
};
int main(){
  Point pt(2, 3); //클래스 객체 선언
  pt.Print(); // 내부함수 선언
}
```
값복사를 자제하고 참조를 통해 효율적인 코드를 쳐야한다.
## 배열 알고리즘
```c++
void CreateArray(int**& arr, int row ,int col) {
	arr = new int*[row];
	for (int i = 0; i < row; ++i)
		arr[i] = new int[col];
}
void Init(int** arr, int row, int col) {
	for (int i = 0; i < row; ++i)
		for (int j = 0; j < col; ++j)
			arr[i][j] = i * j;
}
void Print(int** arr, int row, int col) {
	for (int i = 0; i < row; ++i) {
		for (int j = 0; j < col; ++j) {
			printf("%3d ", arr[i][j]);
		}
		printf("\n");
	}
}
void Delete(int** arr, int row, int col) {
	for (int i = 0; i < row; ++i)
		delete[] arr[i];
	delete[] arr;
}
int main() {
	int** arr = NULL;
	CreateArray(arr, 5, 5);
	Init(arr, 5, 5);
	Print(arr, 5, 5);
	Delete(arr, 5, 5);
}
```
* 2진 배열은 arr, arr[], arr[][] 3가지 주소를 할당해야하기에 **형식으로 받는다.
* 함수로 만들시 함수가 직적 참조 할 수 있게 &연산자를 붙여 간소화 한다.
* delete는 col메모리 삭제후에 row를 없에게 두번 돌려 제거해준다.

## 연속메모리기반 큐와 스택

### 스택
```c++
struct Stack { int stack[100]; int top; };
void Push(Stack* st, int data) 
{ st->stack[st->top++] = data; }
int Pop(Stack* st)
 { return st->stack[--st->top]; }
int main() {
	Stack st = { 0 };

	Push(&st, 10);
	Push(&st, 20);
	printf("%d\n", Pop(&st));
	printf("%d\n", Pop(&st)); 
}
```
10, 20 넣고 출력하면 20 10 출력됨
### 함수 이용한 스택
```c++
class Stack {
	int* stack;
	int top;
	int capacity;
public:
	Stack(int cap = 100) :top(0), capacity(cap) 
	{ stack = new int[capacity]; }
	~Stack() { free(stack); }
	void Push(int data) { stack[top++] = data; }
	int Pop() { return stack[--top]; }
};
int main() {
	Stack st;

	st.Push(10);
	st.Push(20);
	st.Push(30);
	printf("%d\n", st.Pop());
	printf("%d\n", st.Pop());
	printf("%d\n", st.Pop());

}				
```
### 다른 함수를 참조하는 선형큐(c활용)
```c++
struct Queue {
	int queue[100];
	int front; //꺼낼 위치
	int rear; //저장할 위치
};
void AddQueue(Queue* q, int data) {
	q->queue[q->rear++] = data;
} // c언어 참조 함수 
int DeleteQueue(Queue& q) {
	return q.queue[q.front++];
}// c++언어 참조 함수
int main() {
	Queue q = { 0 };
	// 멤버변수 모두 값 0 초기화
	AddQueue(&q, 10);
	printf("%d", DeleteQueue(q));
}
```
### 선형큐(c++활용)
```c++
class Queue {
	int queue[100];
	int front;
	int rear;
public:
	Queue(int f, int r):front(f), rear(r){}
	void AddQueue(int data) {
		queue[rear++] = data;
	}
	int DeleteQueue() {
		return queue[front++];
	}
};
int main() {
	Queue q(0, 0);
	q.AddQueue(10);
	printf("%d\n", q.DeleteQueue());
}
```
**선형큐는 메모리가 한정적이기 때문에 사용하지않는다.**
### 원형큐
```c++
class Queue {
	int queue[5];
	int front;
	int rear;
public:
	Queue(int f = 0, int r = 0):front(f), rear(r){}
	void AddQueue(int data) {
		queue[rear++] = data;
		rear = rear == 5 ? 0 : rear;
		// 큐가 5개의 공간에 의해 rear값이 5가되면 
		// rear를 처음 큐로 되돌린다.
	}
	int DeleteQueue() {
		return queue[front++];
	}
};
int main(){}
```
이렇게되면 5의 값을 가질때마다 rear와 front가 초기화되어 돌아간다.
![queue](https://user-images.githubusercontent.com/56966606/161318378-2185732d-5e4c-4d7d-8ea2-2c7ca09ef6ed.png)   
**그러나 rear와 front의 메모리상 위치가 같게 되면 값할당과 출력에 문제가 생긴다.**
### rear와 front의 중복 문제점을 잡은 원형큐
```c++
class Queue { int* queue; int front; int rear; int capacity;
public:
	Queue(int f = 0, int r = 0, int cap = 0) :front(f), rear(r), capacity(cap) {}
	void Allocate(int cap) {
		capacity = cap;
		queue = (int*)malloc(sizeof(int)*capacity); // c
		queue = new int[capacity]; //c++
		//큐의 새로운 동적 메모리 배열을 할당
	}
	void DeAllocate(){
		free(queue); // c
		delete[] queue; // c++
	}
	void AddQueue(int data) {
		if ((rear + 1) % capacity == front) { return; }
		queue[rear = (rear + 1) % capacity] = data;
	}
	int DeleteQueue() {
		if (front == rear) { return 0xffffff; }

		int value = queue[front = (front + 1) % capacity];
		return value;
	}
};
int main(){
	Queue q;
	q.Allocate(10);
	q.DeAllocate();
}
```
큐 메모리를 클라이언트가 직접 할당 가능하게 바꾸고 rear와 front의 문제점을 수정했다.   
Allocate와 DeAllocate 함수로 할당과 제거를 하게 만들었다.
```c++
class Queue { int* queue; int front; int rear; int capacity;
public:
	Queue(int cap) { //생성자
		front = 0;
		rear = 0;
		capacity = cap;
		queue = (int*)malloc(sizeof(int) * capacity);
	}
	~Queue() { free(queue); } //소멸자
	void AddQueue(int data) {
		if ((rear + 1) % capacity == front) { return; }
		queue[rear = (rear + 1) % capacity] = data;
	}
	int DeleteQueue() {
		if (front == rear) { return 0xffffff; }
		int value = queue[front = (front + 1) % capacity];
		return value;
	}
};
int main() {
	Queue q(10);
}
```
마무리는 생성자와 소멸자를 이용해 정리해준다.

### <stack>과 <queue>
* <stack>
	- 선언: stack<타입> 변수;
	- push(): 저장
	- top(): 값 반환
	- pop(): 제거
* <queue>
	- 선언: queue<타입> 변수;
	- push(): 저장
	- front(): 값 반환
	- pop(): 제거	

### 노드기반 비연속메모리 
* 이중 연결 리스트
```c++
struct Node { int data; Node* link; };
Node* AllocNode(int data) {
	Node* n = (Node*)malloc(sizeof(Node));
	//노드형 주소인것을 밝히고 Node사이즈의 메모리를 할당
	//Node* n = new Node[NULL];
	n->data = data;
	//노드n 데이터에 접근하여 매개변수 할당
	n->link = NULL;
	// 값 할당한 노드의 주소에 NULL값을 넣어둠
	// 비워두면 개발자들이 안좋아한데여
	return n;
}
int main() {
	Node* n = NULL;		// 계속 움직일 메모리
	Node* p = NULL;		// 기존 변수

	// -->메모리
	n = AllocNode(10);	// n노드에 10변수 할당
	p = n;	// 길잡이 노드 p에 n의 주소넣기
	n = AllocNode(20);	// n은 다른 노드에 20 할당
	p->link = n;	// p는의 link는 n의 주소를 담음
	// <--메모리
	n = AllocNode(30);	// n노드에 30 할당
	p = n;	// 길잡이 노드 p에 n의 주소넣기
	n = AllocNode(40);	// n은 다른 노드에 40 할당
	n->link = p;	// n의 링크에 p가 가진 전메모리 주소 할당
	p = n;	// p에 새로만든 n의 주소 할당

	printf("%d\n", p->data);
	printf("%d\n", p->link->data);
	// --> 10 20
	// <-- 40 30
}
```
**하지만 노드의 중간이 끊어저 버리는 형태로 연결 노드가 아님 10 20 30을 만들면 20노드의 주소를 알아갈 수 없음**
* tail 끝노드를 통한 연결 메모리
```c++
//노드 이중 연결리스트
struct Node { int data; Node* link; };
Node* AllocNode(int data) {
	Node* n = (Node*)malloc(sizeof(Node));
	n->data = data;
	n->link = NULL;
	return n;
}
Node* GetTail(Node* p) { //끝노드를 찾아주며 중간노드들을 거침
	Node* t = p;
	while (t->link != NULL)
		t = t->link;
	return t;
}
int main() {
	Node* n = NULL;		
	Node* p = NULL;		// p노드는 초기 주소
	Node* t = NULL;		// t노드는 함수를 통해 계속해서 링크를 이어나감
	n = AllocNode(10);	
	p = n;
	t = p;
	n = AllocNode(20);	
	t = GetTail(p);
	t->link = n;
	n = AllocNode(30);
	t = GetTail(p);
	t->link = n;
	for(Node* cur = p; cur!=NULL; cur=cur->link)
	printf("%d\n", cur->data);
}
```

### 이중연결리스트
* 인터페이스는 서버와 클라이언트사이 소통을 연결해준다.
* 노드기반 선형적으로 앞뒤 메모리 참조가 가능해야한다.

**★★★시험 이중리스트 끝노드tail과 p 관계 tail을 찾는 2가지 방법**
* tail은 null값을 가지고 있으므로 null가진 끝값을 찾으면 된다.
*	메모리는 낭비가 되지만 tail의 값을 계속 저장해두기
* 이중변수는 앞뒤 메모리 참조가 가능하므로 Add메서드가 2개이다. 
```c++
struct Node { int data; Node* prev; Node* next; };
Node* AllocNode(int data) { // 노드생성 및 값 리턴
	Node* n = NULL;
	n = (Node*)malloc(sizeof(Node));
	n->data = data;
	//노드만큼 메모리 생성
	n->prev = n->next = NULL;
	return n; }
int main() {
	Node* head = NULL;	// 맨앞 노드
	Node* tail = NULL;	// 맨뒤 노드
	Node* p = NULL;			// 추가 노드
	
	p = AllocNode(0xffffff);
	tail = head = p;

	p = AllocNode(10);
	tail->next = p;		// 선언노드 next에 다음노드주소 할당
	p->prev = tail;		// 생성된노드prev에 이전주소 tail할당
	tail = p;		// 끝노드로 tail 위치 옮겨줌
	
	for (Node* cur = head->next; cur != NULL; cur = cur->next)
		printf("%d\n", cur->data);	// 정방향
	for (Node* cur = tail; cur->prev != NULL; cur = cur->prev)
		printf("%d\n", cur->data);	// 역방향
}
```
* 앞뒤로 Add메서드를 달아주고 tail, head둘다 더미노드로 만들기
```c++
struct Node { int data; Node* prev; Node* next; };
struct List { Node* head; Node* tail; };
Node* AllocNode(int data) { 
	Node* n = NULL;
	n = (Node*)malloc(sizeof(Node));
	n->data = data;
	n->prev = n->next = NULL;
	return n; }
void AddTailList(List* lt, int data) {
	Node* n = AllocNode(data);
	Node* t = lt->tail;	// t = 더미tail
	Node* pt = t->prev;	// pt = 더미head 
	pt->next = n;		// head 뒤는 새노드 n
	n->prev = pt;		// 새노드 앞 head요소
	n->next = t;		// 새노드 뒤 tail요소
	t->prev = n;		// tail의 앞은 새노드 n
}
void AddHeadList(List* lt, int data) {
	Node* n = AllocNode(data);
	Node* h = lt->head;	// t = 더미tail
	Node* ph = h->next;	// pt = 더미head 
	ph->prev = n;		// head 뒤는 새노드 n
	n->prev = h;		// 새노드 앞 head요소
	n->next = ph;		// 새노드 뒤 tail요소
	h->next = n;		// tail의 앞은 새노드 n
}
```
* 삽입함수와 제거함수 만들기
```c++
void EraseList(List* lt, Node* p) { //어디에 있는걸 없에야 하는지
	Node* pp = p->prev;
	Node* pn = p->next;
	free(p);
	pp->next = pn;
	pn->prev = pp;
}
void InsertTailList(List* lt, Node* p, int data ) { //어디에 집어 넣어야하는지
	Node* pp = p->prev;
	Node* n = AllocNode(data);
	pp->next = n;
	n->next = p;
	n->prev = pp;
	p->prev = n;
}
void InsertHeadList(List* lt, Node* p, int data) {
	Node* pn = p->next;
	Node* n = AllocNode(data);
	pn->prev = n;
	n->next = pn;
	n->prev = p;
	p->next = n;
}
```
* 최종 c로 만들어보는 비연속 이중리스트
```c++
struct Node { int data; Node* prev; Node* next; };
struct List { Node* head; Node* tail; };
Node* AllocNode(int data) {
	Node* n = NULL;
	n = (Node*)malloc(sizeof(Node));
	n->data = data;
	n->prev = n->next = NULL;
	return n;
}
void InitList(List* lt) {
	lt->head = AllocNode(0xffffff);
	lt->tail = AllocNode(0xffffff);
	lt->head->next = lt->tail;
	lt->tail->prev = lt->head;
}
void InsertTailList(List* lt, Node* p, int data) { 
	Node* pp = p->prev;
	Node* n = AllocNode(data);
	pp->next = n;
	n->next = p;
	n->prev = pp;
	p->prev = n;
}
void InsertHeadList(List* lt, Node* p, int data) {
	Node* pn = p->next;
	Node* n = AllocNode(data);
	pn->prev = n;
	n->next = pn;
	n->prev = p;
	p->next = n;
}
void AddTailList(List* lt, int data) {
	InsertTailList(lt, lt->tail, data);
}
void AddHeadList(List* lt, int data) {
	InsertHeadList(lt, lt->head, data);
}
void EraseList(List* lt, Node* p) { //어디에 있는걸 없에야 하는지
	Node* pp = p->prev;
	Node* pn = p->next;
	free(p);
	pp->next = pn;
	pn->prev = pp;
}
void UnInitList(){
	Node* p = head;
	while(p != NULL) {
		Node* pn = p->next;
		free(p);
		p = pn;
	}
}
Node* GetHead(List* lt){ return lt->head->next; }
int HasNext(List* lt, Node* p){ return p->next ? 1 : 0; }
Node* Next(List* lt, Node* p){ return p->next; }
Node* GetTail(List* lt) { return lt->tail->prev; }
int HasPrev(List* lt, Node* p) { return p->prev ? 1 : 0; }
Node* Prev(List* lt, Node* p) { return p->prev; }
int GetData(List* lt, Node* p) { return p->data; }

Node* FindLinkedList(List* plt, int key) {
	for (Node* p = GetHead(plt); HasNext(plt, p); p = Next(plt, p)) {
		if (GetData(plt, p) == key)
			return p;

		return NULL; } }
void PrintHeadLinkedList(List* plt) {
	for (Node* p = GetHead(plt); HasNext(plt, p); p = Next(plt, p)) {
		printf("%d\n", GetData(plt, p));
	}
}
void PrintTailLinkedList(List* plt) {
	for (Node* p = GetTail(plt); HasPrev(plt, p); p = Prev(plt, p)) {
		printf("%d\n", GetData(plt, p));
	}
}
int main() {
	List lt; 
	InitList(&lt);
	AddHeadList(&lt, 10);
	AddHeadList(&lt, 20);
	AddHeadList(&lt, 30);

	PrintHeadLinkedList(&lt);
	printf("\n");

	Node* p = FindLinkedList(&lt, 20);
	if (p != NULL) {
		InsertHeadList(&lt, p, 450);
		p = Prev(&lt, p);
		//EraseList(&lt, p);
	}

	printf("\n");
	PrintTailLinkedList(&lt);
}
```
* c++로 바꿔보기
```c++
struct Node { int data; Node* prev; Node* next; };
class List { 
	Node* head; 
	Node* tail;
public:
	Node* AllocNode(int data) {
		Node* n = NULL;
		n = (Node*)malloc(sizeof(Node));
		n->data = data;
		n->prev = n->next = NULL;
		return n;
	}
	void Init() {
		head = AllocNode(0xffffff);
		tail = AllocNode(0xffffff);
		head->next = tail;
		tail->prev = head;
	}
	void InsertTail(Node* p, int data) {
		Node* pp = p->prev;
		Node* n = AllocNode(data);
		pp->next = n;
		n->next = p;
		n->prev = pp;
		p->prev = n;
	}
	void InsertHead(Node* p, int data) {
		Node* pn = p->next;
		Node* n = AllocNode(data);
		pn->prev = n;
		n->next = pn;
		n->prev = p;
		p->next = n;
	}
	void AddTail(int data) {
		InsertTail(tail, data);
	}
	void AddHead(int data) {
		InsertHead(head, data);
	}
	void Erase(Node* p) { //어디에 있는걸 없에야 하는지
		Node* pp = p->prev;
		Node* pn = p->next;
		free(p);
		pp->next = pn;
		pn->prev = pp;
	}
	void UnInit() {
		Node* p = head;
		while (p != NULL) {
			Node* pn = p->next;
			free(p);
			p = pn;
		}
	}
	Node* GetHead() { return head->next; }
	int HasNext(Node* p) { return p->next ? 1 : 0; }
	Node* Next(Node* p) { return p->next; }
	Node* GetTail() { return tail->prev; }
	int HasPrev(Node* p) { return p->prev ? 1 : 0; }
	Node* Prev(Node* p) { return p->prev; }
	int GetData(Node* p) { return p->data; }
};
// client
Node* FindLinkedList(List& plt, int key) {
	for (Node* p = plt.GetHead(); plt.HasNext(p); p = plt.Next(p)) {
		if (plt.GetData(p) == key) {
			return p;
		}
	}
	return NULL;
}
void PrintHeadLinkedList(List& plt) {
	for (Node* p = plt.GetHead(); plt.HasNext(p); p = plt.Next(p)) {
		printf("%d\n", plt.GetData(p));
	}
}
void PrintTailLinkedList(List& plt) {
	for (Node* p = plt.GetTail(); plt.HasPrev(p); p = plt.Prev(p)) {
		printf("%d\n", plt.GetData(p));
	}
}
int main() {
	List lt; 
	lt.Init();
	lt.AddHead(10);
	lt.AddHead(20);
	lt.AddHead(30);

	PrintHeadLinkedList(lt);
	printf("\n");

	Node* p = FindLinkedList(lt, 20);
	if (p != NULL) {
		lt.InsertHead(p, 450);
		p = lt.Prev(p);
		//EraseList(&lt, p);
	}
	PrintTailLinkedList(lt);
	lt.UnInit();
```

#### 콜백 함수
```c++
void PrintArray(int* pa, int size) {
	for (int i = 0; i < size; ++i) {
		printf("%d ", pa[i]);
	} }
int Search(int* pa, int size, int (*cmp)(int data)) {
	for (int i = 0; i < size; ++i) {
		if (cmp(pa[i]))			 // 콜백
			return i;

	return -1;
}
///아래는 클라이언트 코드
int cmp(int data) {			// 콜백 함수
	printf("\n찾아본 값은 %d\n", data);
	return 50 < data && data % 2 == 0;
}
int main() {
	int arr[10] = { 50, 69, 35, 62, 19, 90, 93, 72, 45, 27 };
	int size = 10;

	PrintArray(arr, size);
	int idx = Search(arr, size, cmp);
	if (-1 != idx) {
		printf("\n[%d] : %d\n", idx, arr[idx]);
	}
}
```
```c++
void Print(int (*cf)(int a)) {
	printf("server start!\n");
	if( cf(100) )		//callback
	printf("middle print!\n");
	printf("server close!\n");
}

int predicate(int data) {	//callback function
	printf("client code!\n");
	return data%2 == 0 ;
}
int main() {
	Print(predicate);
}
```

**콜백함수**
```c++
void PrintArray(int* pa, int size) {
	for (int i = 0; i < size; ++i) {
		printf("%d\n", pa[i]);
	}
}
int Search(int* pa, int size, int (*cmp)(int data)) {
	for (int i = 0; i < size; ++i) {
		if (cmp(pa[i])) {
			return i;
		}
	}
	return -1;
}
int cmp(int data) {
	printf("검색한 값은 %d\n", data);
	return 50 < data && data%2 == 0;
}
int main() {
	int arr[10] = { 50, 69, 35, 62, 19, 90, 93, 72, 45, 27 };
	int size = 10;

	PrintArray(arr, size);
	int idx = Search(arr, size, cmp);
	if (-1 != idx) {
		printf("[%d] : %d\n", idx, arr[idx]);
	}
}
server
void Print(void (*f)()) {
	printf("1. start Print()\n");
	f(); //callback(caller)
	printf("2. End Print()\n");
}
//client
void cb1() { //callback function(callee)
	printf("client hello\n");
}
void cb2() { //callback function(callee)
	printf("=====\n");
}
int main() {
	Print(cb1);
	Print(cb2);
}
```
* 콜백함수는 서버코드와 클라이언트코드를 잘 분리해서 사용해야한다.
* callback함수가 무엇이고 기능을 해주는 함수는 무엇인지 잘 구분 할 것.
```c++
void Print(int (*f)(int)) {
	printf("1. start Print()\n");
	if (f(100))
		printf("3.middle Print()\n");
	printf("2. End Print()\n");
}

int predicate(int data) {
	return data%2 == 0;
}
int main() {
	Print(predicate);
}
```

**2진배열**
```c++
void PrintArray(int* pa, int size) {
	for (int i = 0; i < size; ++i) {
		printf("%5d", pa[i]);
	}
	printf("\n");
}
int Search(int* list, int size, int key) {
	int left = 0;
	int right = size - 1;
	while(left <= right) {
		int middle = (left + right) / 2;
		if (key < list[middle]) {
			left = left;
			right = middle - 1;
		}
		else if (key > list[middle]) {
			left = middle + 1;
			right = right;
		}
		else { return middle; }
	}
	return -1;
}
int main() {
	int arr[10] = { 10, 17, 24, 38, 47, 57, 77, 89, 92, 99 };
	int size = 10;

	int idx = Search(arr, size, 30);
	if (idx != -1)
		printf("[%d] : %d\n", idx, arr[idx]);
	else
		printf("원소가 존재하지 않음\n");

	PrintArray(arr, size);
}
```

**재귀함수**
```c++
// 정수 반환형
int Fact(int n) {
	return n == 1 ? 1 : n * Fact(n - 1);
}
int main() {
	int result = Fact(5);
	printf("result : %d\n", result);
}
==========================================
// 호출형 
void Fact(int n, int * pr) {
	if (n == 1)
		*pr = 1;
	else {
		int t = 0;
		Fact(n - 1, &t);
		*pr = n * t;
	}
}
int main() {
	int result = 0;
	Fact(5, &result);
	printf("%d\n", result);
}
```
* 피보나치 수열
```c++
int Fibonacci(int n) {
	if (n == 1)
		return 1;
	if (n == 2)
		return 2;
	return Fibonacci(n - 2) + Fibonacci(n - 1);
}
int main() {
	int result = Fibonacci(10);
	printf("result : %d\n", result);
}	
```	
**루프문을 통한 이진배열 시험**
```c++
int _Search(int* list, int left, int right, int key) {
	if (left > right)
		return -1;
	int middle = (left + right) / 2;
	if (key < list[middle]) {
		int idx = _Search(list, left, middle - 1, key);
		return idx;
	}
	else if (key > list[middle]) {
		int idx = _Search(list, middle + 1, right, key);
		return idx;
	}
	else
		return middle;
}
int Search(int* list, int size, int key) {
	return _Search(list, 0, size - 1, key);
	//상한과 하한이 존재해야한다.
}
int main() 
{
	int list[10] = { 12,15,20,25,50,58,60,69,74,85 };
	// 이진검색은 기본적으로 배열이 순차적이어야 한다.
	int size = 10;
	int idx = -1;

	idx = Search(list, size, 58);
	if (idx != -1)
		printf("[%d] : %d\n", idx, list[idx]);
}
```
* 재귀함수 그림판 
```c++
int map[10][10] = {
	0,0,0,0,0,0,0,0,0,0,
	0,1,1,1,1,0,0,0,0,0,
	0,0,0,0,1,0,0,0,0,0,
	0,0,1,1,1,0,0,0,0,0,
	0,0,1,1,1,0,2,2,2,2,
	0,0,0,1,0,0,2,2,2,0,
	0,0,0,1,1,0,0,0,2,0,
	0,0,0,1,1,0,0,0,2,0,
	0,0,0,0,0,0,0,2,2,0,
	0,0,0,0,0,0,0,2,2,0
};
void PrintMap() {
	system("cls");
	for (int i = 0; i < 10;++i) {
		for (int j = 0; j < 10;++j) {
			printf("%2d", map[i][j]);
		}
		printf("\n");
	}
	Sleep(300);
}
void _Fill(int row, int col, int newColor, int oldColor) {
	// 종료조건
	// 1. 캔버스 밖을 벗어날 때
	if (0 > row || row > 9 || 0 > col || col > 9)
		return;
	// 2. 바꾸고자하는 색상이 oldColor가 아닐 때
	if (map[row][col] != oldColor)
		return;
	map[row][col] = newColor;
	PrintMap();
	_Fill(row-1, col, newColor, oldColor);
	_Fill(row, col+1, newColor, oldColor);
	_Fill(row+1, col, newColor, oldColor);
	_Fill(row , col-1, newColor, oldColor);
}
void Fill(int row, int col, int newColor) {
	if (map[row][col] == newColor)
		return;
	_Fill(row, col, newColor, map[row][col]);
}
int main() {
	int row, col;
	printf("행과 열 입력:");
	scanf_s("%d %d\n", &row, &col);
	//Fill(3, 3, 7); // s, y, color
	Fill(row, col, 6);
	PrintMap();
}	
```	
* 재귀함수 미로
```c++
int map[10][10] = {
	0,0,0,0,0,0,0,0,0,0,
	1,1,1,0,1,1,1,1,0,1,
	0,0,1,0,1,0,0,1,0,1,
	0,0,1,0,1,0,1,0,0,1,
	1,1,1,0,0,0,0,1,1,1,
	0,0,0,0,1,1,1,1,1,1,
	1,1,0,1,0,0,0,0,0,1,
	1,0,0,0,0,1,1,1,1,1,
	1,0,1,1,0,0,0,1,9,1,
	1,1,1,0,1,1,0,0,0,1,
};
void PrintMap() {
	system("cls");
	for (int i = 0; i < 10;++i) {
		for (int j = 0; j < 10;++j) {
			printf("%2d", map[i][j]);
		}
		printf("\n");
	}
	Sleep(300);
}
int Maze(int row, int col, int goal) {
	if (0 > row || row > 9 || 0 > col || col > 9)
		return 0;
	// 순서 잘 이해하기
	if (map[row][col] == goal) {
		map[row][col] = 5;
		return 1;
	}
	if (map[row][col] != 0)
		return 0;

	map[row][col] = 4;
	PrintMap();

	// 무조건 0 || 1중 한개를 반환해야 한다.
	// 갈린길에서 갔다온 곳을 돌아가게하지 않게하기 위해서
	if (Maze(row - 1, col, goal))
		return 1;
	if (Maze(row, col + 1, goal))
		return 1;
	if (Maze(row + 1, col, goal))
		return 1;
	if (Maze(row, col - 1, goal))
		return 1;
}
int main() {
	PrintMap();
	Maze(0, 0, 9);
}	
```		
# 기말 2차시
### 시험!!! 배열에서 제일 큰 값을 찾아내는 출력
```c++
void PrintList(int list[], int size) {
   for (int i = 0; i < size; ++i)
      printf("%d ", list[i]);
   printf("\n");
}
int Max(int list[], int size) {
   int maxIdx = 0;
   for (int i = 1; i < size; ++i) {
       if (list[maxIdx] < list[i])
           maxIdx = i;
   }
   return maxIdx;
}
int main() {
   int list[10] = { 35, 65, 25, 92, 68, 75, 46, 59, 84, 15 };

   int maxidx = Max(list, 10);
   printf("list[%d]: %d\n", maxidx, list[maxidx]);
   //초기화
   list[maxidx] = 0;
   PrintList(list, 10);
}
```
* 배열의 값이 아닌 위치를 찾아내 출력하는것을 이해해야 한다.

##정렬의 종류
* 선택정렬
* 삽입정렬
* 버블정렬
* 퀵정렬
				  		  
### 선택정렬
**배열을 순회하면서 최고값을 찾아 현재인텍스와 자리를 바꾼다.**				  
```c++
void PrintList(int list[], int size) {
    for (int i = 0; i < size; ++i)
        printf("%d ", list[i]);
    printf("\n");
}
void Swap(int& a, int& b) {
    int t = a;
    a = b;
    b = t;
}
void SelectionSort(int list[], int size) {
    for (int i = 0; i < size; ++i) {
        int maxidx = i;
        for (int j = i + 1; j < size; ++j) //초기값 설정 Max함수
            if (list[maxidx] > list[j])
            	maxidx = j;
        Swap(list[i], list[maxidx]);
    }
}
int main() {
    int list[10] = { 35, 65, 25, 92, 68, 75, 46, 59, 84, 15 };
    SelectionSort(list, 10);
    PrintList(list, 10);
}				  
```
### 삽입정렬				  				  
**첫배열부터 한개씩 다른 배열과 비교하면서 자신보다 값이 크면 자신의 다음배열에 위치하도록 한다.**	
```c++
void PrintList(int list[], int size) {
	for (int i = 0; i < size; ++i)
		printf("%d ", list[i]);
	printf("\n");
}
void Swap(int& a, int& b) {
	int t = a;
	a = b;
	b = t;
}
void InsertionSort(int list[], int size) {
	for (int i = 1; i < size; ++i) {
		int curValue = list[i];
		int j = 0;
		for (j = i - 1; j >= 0; --j)
			if (list[j] > curValue)
				list[j + 1] = list[j];
			else
				break;
		list[j + 1] = curValue;
	}
}
int main() {
	int list[10] = { 15, 25, 35, 65, 27, 68, 75, 46, 59, 84 };

	InsertionSort(list, 10);
	PrintList(list, 10);
}	
```
### 랜덤 배열에서의 삽입정렬 활용
```c++
void PrintList(int list[], int size) {
	for (int i = 0; i < size; ++i)
		printf("%d ", list[i]);
	printf("\n");
}
void Swap(int& a, int& b) {
	int t = a;
	a = b;
	b = t;
}
void InsertionSort(int list[], int size) {
	for (int i = 1; i < size; ++i) {
		int curValue = list[i];
		int j = 0;
		for (j = i - 1; j >= 0; --j)
			if (list[j] > curValue)
				list[j + 1] = list[j];
			else
				break;
		list[j + 1] = curValue;
	}
}
int main() {
	int list[100] = { 0 };
	srand((unsigned)time(NULL));
	for (int i = 0; i < 100; ++i)
		list[i] = rand() % 100;
	PrintList(list, 100);
	InsertionSort(list, 100);

	PrintList(list, 100);
}	
```
				
### 버블정렬
**정렬의 맨 뒤에 배열부터 모든 배열을 순회하면서 비교값보다 크면 뒤로 위치를 옮긴다.**				
```c++
void PrintList(int list[], int size) {
	for (int i = 0; i < size; ++i)
		printf("%d ", list[i]);
	printf("\n");
}
void Swap(int& a, int& b) {
	int t = a;
	a = b;
	b = t;
}
void BubbleSort(int list[], int size) {
	for (int i = size - 1; i <= size; --i) {
		for (int j = 0; j < i; ++j)
			if (list[j] > list[j + 1])
				Swap(list[j], list[j + 1]);
	}
}
int main() {
	int list[10] = { 35, 65, 25, 94, 68, 75, 46, 59, 84, 15 };

	BubbleSort(list, 10);
	PrintList(list, 10);
}				
```
### 중요!! 퀵정렬	
**중강 값을 기점으로 양쪽 정렬을 순회하며 정리한다.또한 재귀함수로 구성한다!**	
![image](https://user-images.githubusercontent.com/56966606/169650420-87c79a75-db0e-4421-8564-5b63d560295d.png)	
```c++
void PrintList(int list[], int size) {
   for (int i = 0; i < size; ++i)
      printf("%d ", list[i]);
   printf("\n");
}
void Swap(int& a, int& b) {
   int t = a;
   a = b;
   b = t;
}
void _QuickSort(int list[], int low, int high) {
    if (low <= high) {
        int pivot = low; //list[pivot]
        int i = pivot + 1; //low + 1 시작값 초기화
        int j = high;
        while (i <= j) {
            while (list[pivot] > list[i]) //pivot보다 작은값 찾기
                ++i;
            while (list[pivot] < list[j]) //pivot보다 큰값 찾기
                --j;
            if (i <= j)//pivot을 중심으로 두개의 계산이 끝나는 지점
                Swap(list[i++], list[j--]);
            PrintList(list, 10);
        }
        printf("\n");
        Swap(list[pivot], list[j]);
        PrintList(list, 10);

        _QuickSort(list, low, j - 1);
        _QuickSort(list, j + 1, high);
    }
}
void QuickSort(int list[], int size) {
    _QuickSort(list, 0, size - 1);
}
int main() {
    int list[10] = { 46, 65, 25, 94, 68, 75, 35, 59, 84, 15 };

    QuickSort(list, 10);
    PrintList(list, 10);
}	
```
![일반 2진 트리](https://user-images.githubusercontent.com/56966606/169471439-6c74a113-5364-4180-a8af-b70e4ea61029.png)
![2진 트리](https://user-images.githubusercontent.com/56966606/169471446-36fb581a-d8b4-48ec-b2f9-0333f8d3869f.png)
