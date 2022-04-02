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
  Point(int _x, int _y) {
    x = _x;
    y = _y;
  }
  void Print(){
    printf("&d %d\n", x, y)
  }
};
int main(){
  Point pt(2, 3); //클래스 객체 선언
  pt.Print(); // 내부함수 선언
}
```
값복사를 자제하고 참조를 통해 효율적인 코드를 쳐야한다.
## 큐의 진화
### 다른 함수를 참조하는 선형큐(c활용)
```c
struct Queue {
	int queue[100];
	int front; //꺼낼 위치
	int rear; //저장할 위치
};
void AddQueue(Queue* q, int data) {
	q->queue[q->rear++] = data;
}// c언어 참조 함수 
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
class Queue {
	int queue[5];
	int front;
	int rear;
public:
	Queue(int f = 0, int r = 0):front(f), rear(r){}
	void AddQueue(int data) {
		if (rear + 1 == front)
			return;
			// 빈 메모리상태 

		queue[rear++] = data;
		rear = rear == 5 ? 0 : rear;
		// 큐가 5개의 공간에 의해 rear값이 5가되면 
		// rear를 처음 큐로 되돌린다.
	}
	int DeleteQueue() {
		if (front == rear)
			return 0xffffff;
		// 큐메모리가 빈상태를 정의 

		int value = queue[front++];
		front = front == 5 ? 0 : front;
		// 반환식으로 인해 fornt값을 보관해야 함
		return value;
	}
};
int main(){}
```
DeleteQueue함수에서는 메모리가 텅비었을때 rear와 fornt 값이 같으므로 빈메모리라는 것을 알리기 위해 0값을 준다.
AddQueue함수에는 메모리가 꽉차면 DeleteQueue의 if문과 겹치지 않고 더 할당 할수 없도록 꽉 찼을때 if로 메모리 할당을 멈춘다.
* 함수 반환에따라 return 식이 달라진다. int > 0xffffff / void > 아무값도 보내지 않음

```
class Queue {
	int queue[5];
	int front;
	int rear;
public:
	Queue(int f = 0, int r = 0):front(f), rear(r){}
	void AddQueue(int data) {
		if ((rear + 1) % 5 == front) { return; }
		//5번재큐에서 돌리면 5 == 0이되어버려 front와 rear가만남
		//그러므로 (rear+1)%5로 0 == 0만들어 실행되게해야한다.

		queue[rear = (rear+1)%5] = data;
		// 큐 rear값으로 자동으로 돌리기
	}
	int DeleteQueue() {
		if (front == rear) { return 0xffffff; }
			
		int value = queue[front = (front+1)%5];
		// 큐 front값으로 자동으로 돌리기
		return value;
	}
};
```