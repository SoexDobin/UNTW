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


