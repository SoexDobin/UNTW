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
구조체
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
클래스
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
	p = n;							// 길잡이 노드 p에 n의 주소넣기
	n = AllocNode(20);	// n은 다른 노드에 20 할당
	p->link = n;				// p는의 link는 n의 주소를 담음
	// <--메모리
	n = AllocNode(30);	// n노드에 30 할당
	p = n;							// 길잡이 노드 p에 n의 주소넣기
	n = AllocNode(40);	// n은 다른 노드에 40 할당
	n->link = p;				// n의 링크에 p가 가진 전메모리 주소 할당
	p = n;							// p에 새로만든 n의 주소 할당

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
	tail = p;					// 끝노드로 tail 위치 옮겨줌
	
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
void InitList(List* lt) {
	lt->head = AllocNode(0xffffff);
	lt->tail = AllocNode(0xffffff);
	lt->head->next = lt->tail;
	lt->tail->prev = lt->head;
}
Node* GetHead(List* lt) { return lt->head->next; }
int HasNext(List* lt, Node* p) { return p->next ? 1 : 0; }
Node* Next(List* lt, Node* p) { return p->next; }
Node* GetTail(List* lt) { return lt->tail->prev; }
int HasPrev(List* lt, Node* p) { return p->prev ? 1 : 0; }
Node* Prev(List* lt, Node* p) { return p->prev; }
int GetData(List* lt, Node* p) { return p->data; }
int main() {
	List lt;
	
	InitList(&lt);
	AddTailList(&lt, 10);
	AddTailList(&lt, 20);
	AddTailList(&lt, 30);
	
	//원소의 조회(순회)
	for (Node* p = GetHead(&lt); HasNext(&lt, p); p = Next(&lt, p)) {
		printf("%5d", GetData(&lt, p)); }
	// 10 20 30
	for (Node* p = GetTail(&lt); HasPrev(&lt, p); p = Prev(&lt, p) )
		printf("%5d", GetData(&lt, p)); }
	// 30 20 10	
```