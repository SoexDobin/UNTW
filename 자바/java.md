# 2차시

## 돼지, 닭, 소 총 다리 수를 구하는 프로그램
```java
// 결과화면 
// 모든 동물의 다리 수는 xx입니다.
import java.util.*; 
public class Test1 {

	public static void main(String[] args) {
		int a1 = 4, a2 = 3, a3 = 5, total;
		Scanner sc = new Scanner(System.in);
		System.out.print("추가 돼지의 수");
		a1 += sc.nextInt();
		System.out.print("추가 닭의 수");
		a2 += sc.nextInt();
		System.out.print("추가 소의 수");
		a3 += sc.nextInt();
		
		total = a1*4 + a2*2 + a3*4;
		System.out.printf("모든 동물의 다리 수는 %d입니다.", total);
	}
}
```

## 돈을 입력받아 다음결과와 같이 출력하는 프로그램
```java
/*
>>결과화면<<
돈 입력: 2340
500원: 4개
100원: 3개
50원: 0개
10원: 4개
*/
import java.util.*;
public class Test2 {
	public static void main(String[] args) {
		int money, thousand, hundred, fifty, ten;
		Scanner sc = new Scanner(System.in);
		
		while(true) {
			System.out.println("돈 입력: ");
			money = sc.nextInt();
			if(money%10 != 0) {
				System.out.println("10원 단위까지 입력하세요.");
			} else {
				thousand = money/500;
				hundred = (money%500)/100;
				fifty = (money%100)/50;
				ten = (money%50)/10;
				System.out.printf("500원 %d개\n", thousand);
				System.out.printf("100원 %d개\n", hundred);
				System.out.printf("50원 %d개\n", fifty);
				System.out.printf("10원 %d개\n", ten);
				break;
			}
		}
	}
```

## 반복문 (for문, while문) 10에서 1까지 홀수를 역으로 출력하고 누적합을 구하는 프로그램
```java
/*
>>결과화면<<
9 + 7 + 5 + 3 + 1 = 25
누적합: 25
*/
public class Test3 {
	public static void main(String[] args) {
		int total = 0;
		for(int i = 10; i > 0; i--) {
			if(i % 2 == 1) {
				if(i == 1) {
					System.out.print(i + " = ");
				}
				else {
					System.out.print(i + " + ");
				}				
				total += i;
			}
		}
		System.out.printf("%d", total);
	}
}
```

## 사용자의 입력을 받아 나누기의 합 계산
```java
/*
>>결과화면<<
정수입력: 6
1 + 1/2 + 1/3 + 1/4 + 1/5 + 1/6 = xx.x 
*/
import java.util.*;
public class Test4 {
	public static void main(String[] args) {
		int num;
		double total = 0;
		Scanner sc = new Scanner(System.in);
		System.out.print("정수 입력: ");
		num = sc.nextInt();
		for(int i = 1; i <= num; i++) {
			if(i == 1) {
				System.out.printf("1 + ", i);
			} else if(i == num) {
				System.out.printf("1/%d = ", i);
			} else {
				System.out.printf("1/%d + ", i);
			}
			// 중요한부분! 1이 아닌 1.0으로 형변환하여 계산해야 나누기가 잘 이루어짐!
			total += 1.0/i; 
		}
		System.out.printf("%.1f", total);
	}
}
```
## p1(x, y)와 p2(x, y)사이의 거리를 구하는 프로그램
```java
/*
랜덤 4개(1~9)
Math.random(): 0.0 <= r < 1.0

>>결과화면<<
p1(5, 3)
p2(9, 1)
두점 사이 거리는 xx.xx입니다.
*/
public class Test5 {
	public static void main(String[] args) {
		int p1_x, p1_y, p2_x, p2_y, width, height;
		double distance;
		p1_x = (int)(Math.random()*9)+1;
		p1_y = (int)(Math.random()*9)+1;
		p2_x = (int)(Math.random()*9)+1;
		p2_y = (int)(Math.random()*9)+1;
		
		System.out.printf("p1(%d, %d)\n", p1_x, p2_x);
		System.out.printf("p1(%d, %d)\n", p1_y, p2_y);
		
		width = p1_x - p2_x;
		height = p1_y - p2_y;
		distance = Math.sqrt(width*width + height*height);
		
		System.out.printf("두점 사이의 거리는 %.2f입니다.", distance);
	}
}
```

## 가위(1), 바위(2), 보(3) 프로그램
```java
/*
>>결과화면<<
숫자 입력: 3
컴퓨터 가위(1)에 졌습니다.
*/
import java.util.*;
public class Test6 {
	public static void main(String[] args) {
		int com, user;
		Scanner sc = new Scanner(System.in);
		com = (int)(Math.random()*3)+1; // 1~3 랜덤 값 생성
		System.out.print("숫자 입력: ");
		user = sc.nextInt();
		
		String hand;
		if(com == 1) {
			hand = "가위";
		} else if(com == 2) {
			hand = "바위";
		} else {
			hand = "보";
		}
		
		System.out.println(">>결과화면<<");
		if(com == 1) { //가위
			if(com == user) {
				System.out.printf("컴퓨터랑 %s(%d)로 비겼습니다.\n",hand ,com);
			} else if(user == 2) {
				System.out.printf("컴퓨터 %s(%d)에 이겼습니다.\n",hand ,com);
			} else {
				System.out.printf("컴퓨터 %s(%d)에 졌습니다.\n",hand ,com);
			}
		} else if(com == 2) { //바위
			if(com == user) {
				System.out.printf("컴퓨터랑 %s(%d)로 비겼습니다.\n",hand ,com);
			} else if(user == 3) {
				System.out.printf("컴퓨터 %s(%d)에 이겼습니다.\n",hand ,com);
			} else {
				System.out.printf("컴퓨터 %s(%d)에 졌습니다.\n",hand ,com);
			}
		} else { //보
			if(com == user) {
				System.out.printf("컴퓨터랑 %s(%d)로 비겼습니다.\n",hand ,com);
			} else if(user == 1) { 
				System.out.printf("컴퓨터 %s(%d)에 이겼습니다.\n",hand ,com);
			} else {
				System.out.printf("컴퓨터 %s(%d)에 졌습니다.\n",hand ,com);
			}
		}
	}
}
```
# 3차시

## 배열 
* 배열(array): 연속된 공간에 값을 저장하여 사용한다.
* 첨자(index): 배열 속 index는 0부터 시작
```java
/*
arr 배열에서 상자 입력으로 배열 원소 초기화하기!
배열명.length는 배열의 사이즈를 구해준다!

>>결과화면<<
정수1 입력: 10
정수2 입력: 20
정수3 입력: 30
정수4 입력: 40

4개 숫자의 총합: xxx
4개 숫자의 평균: xx.x
*/
import java.util.*;

public class Test1 {

	public static void main(String[] args) {
		int arr[] = new int[4]; // 1차원 배열을 다루는 변수 arr를 선언
		int arr2[] = new int[] {10, 20, 30, 40}; // 1차원 초기화 방법 int[]괄호 안에 숫자사용불가
		int arr3[] = {101, 202, 303}; // {1차원 초기화방법}을 사용할경우 new int[] 생략가능
		Scanner sc = new Scanner(System.in);
		int i;
		// 사용자 입력 부분
//		for(i = 0; i<arr.length; i++) {
//			System.out.print("정수 입력: ");
//			arr[i] = sc.nextInt();
//		}
//		// 출력 부분
//		for(i = 0; i<arr.length; i++) {
//			System.out.print(arr[i] + " ");
//		}
		
		int total = 0;
		System.out.println(">>결과화면<<");
		for(i = 0; i < arr.length; i++) {
			System.out.printf("정수%d 입력: ", i+1);
			arr[i] = sc.nextInt();
			total += arr[i];
		}
		System.out.printf("4개 숫자의 총합: %d\n", total);
		System.out.printf("4개 숫자의 평균: %.1f", (float)total/arr.length);
	}
}
``` 

## 알고리즘을 통한 로또 프로그램
```java
public class Test2 {
	static void Swap(int arr, int a, int b) {
		int temp;
		temp = arr[a];
		arr[a] = arr[b];
		arr[b] = temp;
	}

	public static void main(String[] args) {
		int i, lotto[] = new int[6];
		Random r = new Random();

		System.out.println("로또 원본 출력");
		for(i=0;i<lotto.length;i++){
			lotto[i] = r.nextInt(45)+1 // 1~45 사이
			System.out.printf("%d ", lotto[i];)
		}

		System.out.println("로또 정렬 부분 출력");
		int temp, j;
		for(i=0;i<lotto.length-1;i++){
			for(j=1;j<lotto.length-1;j++){
				if(lotto[i]>lotto[j]) {
					// Swap(arr, i, j);
					temp = lotto[i];
					lotto[i] = lotto[j];
					lotto[j] = temp;
				}
			}
		}
		System.out.println("\n정렬된 원본 출력");
		for(i=0;i<lotto.length;i++) {
			System.out.printf("%d ", lotto[i]);
		}
	}
}
```

# 4차시

## 배열
```java
// 가변 배열
int arr[][] = {{1,2,3,4,5},{1,2,3},{1,2,3,4}};
// 기본 배열
int arr[3][3] = {{1,2,3},{1,2,3},{1,2,3}};
```

## 3명의 국어, 영어, 수학 점수의 총점을 구하는 프로그램
 
```java
/*
번호 국어 수학 영어 총점  평균
 1  90  88  77 XXX xx.x
 2  90  88  77 XXX xx.x
 3  90  88  77 XXX xx.x
총합 xxx xxx xxx 000 00.0
*/

public class Test3 {
	public static void main(String[] args){
		int arr[][] = {{90, 88, 73}, {100, 91, 82}, {82, 84, 90}};
		int i, j, total = 0;
		int kor_total = 0, eng_total = 0, math_total = 0, average_total = 0;
		double all_total = 0;
		System.out.println("번호\t국어\t영어\t수학\t총점\t평균");
		
		for(i=0;i<arr.length;i++) {
			System.out.printf(" %d\t", i+1);
			for(j=0;j<arr[i].length;j++) {
				System.out.printf("%d\t", arr[i][j]);
				total += arr[i][j];
			}
			average_total += total;
			System.out.printf("%d\t", total);
			System.out.printf("%.1f", total/3.0);
			all_total += total/3.0;
			System.out.println("\t");
			total = 0;
		}
		System.out.print("총합\t");
		for(i=0;i<arr.length;i++) {
			kor_total += arr[i][0];
			eng_total += arr[i][1];
			math_total += arr[i][2];
		}
		System.out.printf("%d\t", kor_total);
		System.out.printf("%d\t", eng_total);
		System.out.printf("%d\t", math_total);
		System.out.printf("%d\t", average_total/3);
		System.out.printf("%.1f\t", all_total/3.0);
	}
}
```

## 클래스 특성
* 지역변수 지정된 함수 내에서 사용한 변수(초기값이 없으면 쓰리기 값 들어감)
* 멤버변수는 클래스 내에 선언하는 변수 (초기값이 없으면 기본값 설정)
* 멤버변수를 인스턴스라고 하며 객체를 생성해서 접근
* 정적변수 static을 사용한 변수와 클래스는 공유를 목적으로 사용한다.
```java
public class Card {
	static int width; 
	static int height;
	// 클래스/static/공유변수
	
	String kind; 
	int number;
	// 멤버변수(인스턴스)
}	
```

```java
public class Test2 {
	int n; // 멤버변수
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int r; // 지역 변수
		Card c1 = new Card();
		Card c2 = new Card();
		Scanner sc = new Scanner(System.in); 
		
		System.out.print("카드 넓이 입력: ");
		Card.width = sc.nextInt();
		System.out.print("카드 높이 입력: ");
		Card.height = sc.nextInt();
		
		//Card.width = 70;
		//Card.height = 100;

		c1.kind = "heart";
		c1.number = 7;

		c2.kind = "heart";
		c2.number = 3;
		
		System.out.println("c1(" + c1.kind + ", " + c1.number +") => " 
				+ c1.width + ", " + c1.height);
		System.out.println("c2(" + c2.kind + ", " + c2.number +") => " 
				+ c2.width + ", " + c2.height);
	}
}
```

# 객체지향
* 객체지향 특성 3가지
	1. 다형성
	2. 캡슐화
	3. 상속
* 메소드 오버로딩
	1. 메소드 명이 같으면서 
	2. 매개변수의 객수가 다르거나,
	3. 매개변수의 타입이 다르면 오버로딩이라고 함
```java
class Data{
	int value;
}
pulbic class Test3 {
	public static void main(String[] args) {
		Data d1 = new Data();
		Data d2 = new Data();

		d1.value = 3;
		d1.value = 7;

		System.out.println("Swap()함수 호출 전: (" + d1.value + ", "+ d2.value +")");
		Swap(d1, d2);
		
		System.out.println("Swap()함수 호출 후: (" + d1.value + ", "+ d2.value +")");		
	}
	// 오버로딩은 하나의 객체에서 이름이 같은 메소드를 여러개 정의하여 사용하는 것이다.
	static void Swap(Data a, Data b) {
		int temp
		temp = a.value;
		a.value = b.value;
		b.value = temp;
	}
}
```

