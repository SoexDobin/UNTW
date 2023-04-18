# 자바 1차시
```java
// 한 줄 주석
/*
여러
줄
주석
*/
public class Test1 { // Test1 클래스 정의 (보통 클래스명은 대문자 시작)
	public static void main(String[] args) { // 메인 메소드(프로그램 시작 위치, 단 1개) 정의
		// 변수 선언 및 초기화
		int a = 100; // 100을 변수 a에 대입
		double b = 12.345;
		char c = 'A';
		boolean d = true; 

		// 자바 출력 메소드에는 println(), print(), printf()가 있음
		
		System.out.printf("a = %d, b = %.2f, c = \"%c\"\n", a, b, c);
		System.out.println(b);
		System.out.println(c);
		System.out.println(d);
	}
}
```
## 자바 기본형(8개)
* boolean(1byte): true/false 만 저장 가능!
* char(2byte): 문자 1개
* byte(1byte = 8bit): 정수
* short(2byte): 정수
* int(4byte): 정수 -> 기본
* long(8byte): 정수
* float(4byte): 실수
* double(8byte): 실수 -> 기본

## printf()에서 형식지정자 사용 가능!
* 형식지정자
* %d: 정수
* %f: 실수
* %c: 문자 1개
* %s: 문자열
* %%: % 출력

## 이스케이프 문자
* \n: 줄바꿈
* \t: tab(약 빈칸 6개)
* \': '출력
* \": "출력
* \\: \출력 

```java
public class Test2 {
	public static void main(String[] args) {
		int a = 123;
		double b = 12.123;
		char c = 'A';
		
		System.out.println("a는 " + a + "입니다.");
		System.out.println("b는 " + b + "입니다.");
		
		// a = 123, b = 12.123, c = A 입니다.
		System.out.println("a = " + a + ", b = " + b + ", c = " + c + " 입니다.");
		
	}
}
```
+ println(): 마지막에 줄바꿈
+ print(): 마지막에 줄바꿈 x 

* ```"문자열" + anytype => "문자열"```
* ```anytype + "문자열" => "문자열"```
* ```"hello" + 123 => "hello123"```
* ```100 + 200 + "hello" => "300hello"```
* ```100 + "hello" + 200 => "100hello200"```

```java
public class Test3 {
	public static void main(String[] args) {
		int age = 20;
		double grade = 3.5;

		grade = age; // 4->8byte, 작->큰, 값 손실x, 자동형변환!
		// age = (int)grade; // 8->4byte, 큰->작, 값 손실!, 강제형변환!
		
		// 당신은 "20"세이고, 학점은 '3.5' 입니다. 
		System.out.println("당신은 \"" + age + "\"세이고, 학점은 \'" + grade + "\' 입니다.");
	}
}
```

* 형변환 (Type Casting)
* char(2) ---------ㄱ
* byte(1)-short(2)-int(4)-long(8)-float(4)-double(8)
* 작 --------------- (자동형변환) ------------------> 큰
* 작 <---------------- 강제형변환 ------------------- 큰

# 자바 2차시

## 연산자
* 단항연산자(피연산자 1개)
* ! : NOT, true<->false 반전
* +5(양수), -5(음수)
* ++a(선증가), a++(후증가), --a(선감소), a--(후감소)

+ 이항연산자(피연산자 2개)
+ 산술연산자: +, -, *, /(정수/정수=>정수), %(나머지)
+ 비교연산자: >, <, >=, <=, ==(같으면 참), !=(같지 않으면 참)
+ 논리연산자: &&(AND, 모두 참일 때 참), ||(OR, 하나라도 참이면 참) 
+ 복합대입연산자: +=, -=, *= 등 (예: a += 5; 은 a = a + 5; 와 같음)
+ 대입연산자: = (오른쪽->왼쪽, 우선순위 낮음)

- 삼항연산자(피연산자 3개)
- 조건식 ? 참일 때 : 거짓일 때

```java
public class Test1 {
	public static void main(String[] args) {
		int a = 10, b = 3;
		double c = 1.5;
	
		System.out.println(a + " == " + b + " 의 결과는 " + (a == b));	
		System.out.println(a + " + " + b + " = " + (a+b));
		System.out.println(a + " / " + b + " = " + ((double)a/b)); // 실수/정수 => 실수 
		System.out.printf("%d / %d = %.2f", a, b, (double)a/b);

		int a = 10, b = 5;

        b--; // b = b - 1; 와 같음 
		System.out.println("b = " + b); // 4
		System.out.println("b = " + --b); // 3
		System.out.println("b = " + b--); // 3
		System.out.println("b = " + b); // 2
		
		a++; // a = a + 1; 와 같음 
		System.out.println("a = " + a); // 11
		System.out.println("a = " + ++a); // 12
		System.out.println("a = " + a++); // 12
		System.out.println("a = " + a); // 13
	}
}
```

## Scnner와 시간초 출력기

```java
// >> 결과화면 <<
// 초 입력: 54321
// 54321초 입니다.
// x시간 x분 x초 

import java.util.*; // Scanner 클래스 사용하기 위해

public class Test5 {
	public static void main(String[] args) {
		int s;
		Scanner sc = new Scanner(System.in);
		
		System.out.print("초 입력: ");
		s = sc.nextInt();
		
		System.out.println(s + "초 입니다.");
		System.out.printf("%d시간 %d분 %d초\n", s/3600, s/60%60, s%60);
	}
}
```

## 조건문(선택문): if문, switch문

* if문 3가지 형태
* 1. 참일 때 만 실행할 문장 있을때
* if(조건식) { 문장들; }

+ 2. 참/거짓 모두 실행할 문장 있을때
+ if(조건식) { 문장들; } else { 문장들; }

- 3. 조건식이 2개 이상일 때
- if(조건식1) { 문장들; } else if(조건식2) { 문장들; }

```java
import java.util.*;
public class Test2 {
	public static void main(String[] args) {
		int n;
		Scanner sc = new Scanner(System.in);
		
		System.out.print("정수 입력: ");
		n = sc.nextInt();
		
		if(n > 0) {
			System.out.println(n + "은(는) 양수입니다.");
		} else if(n < 0) {
			System.out.println(n + "은(는) 음수입니다.");
		} else { // 이도저도 아닐 때, else 뒤에 조건식x
			System.out.println(n + "은(는) 0입니다.");
		}

		if(n % 2 == 0) {
			System.out.println(n + "은(는) 짝수입니다.");
		} else {
			System.out.println(n + "은(는) 홀수입니다.");
		}

	}
}
```

* switch문
* switch(찾을값) { 문장들 };

```java
public class Test3 {
	public static void main(String[] args) {
		int n = 5;
		
		switch(n) {
		case 5:
			System.out.print("★");
		case 4:
			System.out.print("★");
		case 3:
			System.out.print("★");
		case 2:
			System.out.print("★");
		case 1:
			System.out.print("★");
			break; // 나와 가장 가까운 조건/반복문 {블럭}을 빠져나감(단, if문 제외) 
		default: // if문의 else와 같음!(이도저도 아닐 때)
			System.out.println("1~5만 가능합니다.");
		}

	}
}
```

## 반복문 예제

```java
// >> 결과화면1 <<
// 시작 숫자 입력: 5
// 끝 숫자 입력: 9
// 5, 6, 7, 8, 9

// >> 결과화면2 <<
// 시작 숫자 입력: 15
// 끝 숫자 입력: 9
// 시작 숫자는 끝 숫자보다 작아야 합니다.

import java.util.*; 

public class Test5 {
	public static void main(String[] args) {
		int start, end, i;
		Scanner sc = new Scanner(System.in);
		
		System.out.print("시작 숫자 입력: "); 
		start = sc.nextInt();
		
		System.out.print("끝 숫자 입력: "); 
		end = sc.nextInt();
		
		if(start >= end) {
			System.out.println("시작 숫자는 끝 숫자보다 작아야 합니다."); // 11:56~~~
		} else {
			for(i = start; i <= end; i++) {
				if(i == end) {
					System.out.println(i);
				} else {
					System.out.print(i + ", ");
				}
			}
		}	
	}
}
```

```java
// 구구단 프로그램

// >> 결과화면 <<
// 단(2~9) 입력: 1
// 2~9 사이 숫자만 입력 가능합니다.
//
// 단(2~9) 입력: 5
// 5 * 1 = 5
// 5 * 2 = 10
// ...
// 5 * 9 = 45

import java.util.*;

public class Test6 {
	public static void main(String[] args) {
		int dan, i;
		Scanner sc = new Scanner(System.in);
		
		while(true) { // 무한루프
			System.out.print("단(2~9) 입력: "); 
			dan = sc.nextInt();
			
			if(dan >= 2 && dan <= 9) { // 2~9 사이면 참!
				for(i = 1; i <= 9; i++) {
					System.out.printf("%d * %d = %2d\n", dan, i, (dan*i));
					// System.out.println(dan + " * " + i + " = " + (dan*i));
				}
				break; // if문 제외, while문을 벗어남!
			} else {
				System.out.println("2~9 사이 숫자만 입력 가능합니다.\n");
			}
		}		
	}
}
```

## 배열 예제
```java
// 1차원 배열

public class Test1 {
	public static void main(String[] args) {
		int i, arr[]; // 1차원 배열을 다루는 변수 arr 선언
		arr = new int[3];
		
		int arr2[] = new int[5];
		
		int arr3[] = new int[] {1,2,3,4,5};
		int arr4[] = {1,2,3,4,5}; 
		// 배열을 다루는 변수 선언 및 {1차원배열초기화}를 할 경우 new int[] 생략 가능
		
		// 배열명.length 은 배열의 사이즈를 리턴!
		for(i = 0; i < arr2.length; i++) { // i = 0,1,2,3,4
			arr2[i] = i + 1;
			System.out.println("arr2[" + i + "] = " + arr2[i]);
		}
	}
}
```

```java
// 5명 학생 점수 총점과 평균을 구하는 프로그램   

// >> 결과화면 <<
// 학생1 점수: 97.5
// 학생2 점수: 75.9
// 학생3 점수: 80.2
// 학생4 점수: 77.7 
// 학생5 점수: 84.7
//
// 5명 학생의 총점: xxx
// 5명 학생의 평균: xx.xx

public class Test3 {
	public static void main(String[] args) {
		double total = 0, score[] = {97.5, 88.2, 75.9, 80.2, 77.7};
		int i;
		
		for(i = 0; i < score.length; i++) {
			total += score[i]; // total = total + score[i];
			System.out.println("학생" + (i+1) + " 점수: " + score[i]);
		}
		
		System.out.println(); // 줄바꿈
		System.out.println(score.length + "명 학생의 총점: " + total);
		
		System.out.printf("%d명 학생의 평균: %.2f\n", 
				score.length, total/score.length);
		
		// System.out.println(score.length 
		//			+ "명 학생의 평균: " + total/score.length);
	}
}
```

## 랜덤 발생기
```java
// 랜덤 발생하기

// 1~10 사이 랜덤(난수) 발생
// Math.random()					: 0.0 <= r < 1.0
// Math.random() * 10				: 0.0 <= r < 10.0
// (int)(Math.random() * 10)		: 0 <= r < 10
// (int)(Math.random() * 10) + 1	: 1 <= r < 11 (따라서, 1~10)

// 1~45 사이 6개 숫자 출력하는 프로그램

// >> 결과화면 <<
// 이번 주 로또 번호입니다.
// 45 1 32 5 23 30

import java.lang.*; // 컴파일러가 자동으로 추가해 줌!

public class Test4 { 
	public static void main(String[] args) {
		int i, lotto[] = new int[6];
		
		System.out.println("이번 주 로또 번호입니다.");
		
		for(i = 0; i < lotto.length; i++) {
			lotto[i] = (int)(Math.random() * 45) + 1; // 1~45
			System.out.print(lotto[i] + " ");
		}

	}
}
```