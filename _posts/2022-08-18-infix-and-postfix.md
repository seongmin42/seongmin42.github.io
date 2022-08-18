---
layout: post
title: 중위표기법(Infix Notation)과 후위표기법(Postfix Notation)
subtitle: 문자열로 표현된 중위표기식을 연산해보자.
categories: Algorithms
tags: [algorithms, stack]
---

**중위 표기법(infix notation)**

연산자를 피연산자의 가운데 표기하는 방법

> 예 : A+B

<br>

**후위 표기법(postfix notation)**

연산자를 피연산자 뒤에 표기하는 방법

> 예 : AB+

<br>

----------

<br>

우리는 보통 연산식을 입력할 때 중위 표기법을 많이 사용한다. 하지만 컴퓨터가 식을 연산하기 위해서는 후위 표기법이 더 적절한데, 이를 위해 중위 표기법을 후위 표기법으로 바꾸어준 후 연산을 진행시킬 필요가 있다. 여기에 Stack이 유용하게 사용된다.

중위 표현식을 후위 표현식으로 나타내기 위한 방법은 다음과 같다.

<br>

> 0) 연산자(괄호 포함)를 담을 Stack을 선언한다.<br> 
> 
> 1) 중위 표현식의 토큰을 하나씩 읽으면서,<br>
> 
> 1-1) 토큰이 피연산자라면, 토큰을 출력한다.<br>
> 
> 1-2) 토큰이 연산자이라면, <br>
> 
> 1-2-1) 해당 토큰의 icp(in-coming priority, 토큰 밖 우선순위)가 Stack의 top에 있는 토큰의 isp(in-stack priority)보다 크면 Stack에 push하고,<br>
> 
> 1-2-2) 그렇지 않으면 top 원소의 isp보다 커질 때까지 pop을 반복하며 출력한다. <br>
> 
> 1-2-3) 해당 토큰이 닫는 괄호라면, top에 여는 괄호가 올 때까지 pop을 반복하고, pop된 원소는 출력한다. 여는 괄호는 출력하지 않고 pop한다.<br>
> 
> 2) 중위 표현식에 더 읽을 것이 없으면 중지하고, 있으면 1로 돌아간다.<br>
> 
> 3) 스택에 남아있는 연산자를 모두 pop하여 출력한다.<br>

<br>

위 알고리즘을 ( 6 + 5 * ( 2 - 8 ) / 2 ) 에 적용해보면,

```
1. String = ; Stack = { ( }
2. String = 6 ; Stack = { ( }
3. String = 6 ; Stack = { (, + }  // +의 icp가 (의 isp보다 크기 때문  
4. String = 65 ; Stack = { (, + }
5. String = 65 ; Stack = { (, +, * }  // *의 icp가 *의 isp보다 크기 때문
6. String = 65 ; Stack = { (, +, *, ( }  // 여는 괄호는 icp가 3이기 때문에 무조건 들어간다.
7. String = 652 ; Stack = { (, +, *, (, - }
8. String = 6528 ; Stack = { (, +, *, (, - }
9. String = 6528- ; Stack = { (, +, * }  // 여는 괄호를 만날 때까지 pop한 값을 출력하고, 여는 괄호를 만나면 pop만 하고 출력하지 않는다.
10. String = 6528-* ; Stack = { (, +, / }  // 나누기 /의 icp가 Stack top의 isp보다 커질때까지 pop을 하고 출력한다.
11. String 6528-*2 ; Stack = { (, +, / }
12. String 6528-*2/+ ; Stack = {}  // 여는 괄호를 만날 때까지 pop한 값을 출력하고, 여는 괄호를 만나면 pop만 하고 출력하지 않는다.
```
<br>

이젠 후위표기식을 이용하여 연산을 해야 한다.
후위표기식을 이용한 연산은 다음 알고리즘을 따른다.

<br>

> 0) 피연산자를 담을 스택을 선언한다.<br>
> 
> 1) 후위 표기식의 토큰을 앞에서부터 읽어나가면서,<br>
> 
> 1-1) 피연산자를 만나면 스택에 push한다.<br>
> 
> 1-2) 연산자를 만나면 필요한 a = Stack.pop(), b = Stack.pop()을 하여 두 개의 피연산자를 pop한 뒤, b - a 값을 다시 Stack에 push한다.<br>
> 
> 2) 위 실행을 반복하여 후위 표기식의 토큰을 모두 소진하면, Stack에 남은 하나의 원소를 출력한다.

<br>

아까 만든 후위 표기식을 연산해보면

```
1~4. Stack = { 6, 5, 2, 8}
5-1. Stack.pop2 - Stack.pop1 = 2 - 8 = -6
5-2. Stack.push(-6) ; Stack = { 6, 5, -6 }
6. 5 * (-6) = -30 ; Stack = { 6, -30 }
7. Stack = { 6, -30, 2 }
8. -30 / 2 = -15 ; Stack = { 6, -15 }
9. -15 + 6 = -9 ; Stack = { -9 } 
```

<br>
검산 : ( 6 + 5 * ( 2 - 8 ) / 2 ) = -9
<br>

#### 코드 구현

- 제약사항 : 피연산자는 한 자릿수 자연수이다.

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.util.Stack;

public class InfixCalc {

	public static String infixToPostfix(String infixString) {
		Stack<Character> postfixStack = new Stack<>();
		char[] infixCharArr = infixString.toCharArray();
		StringBuilder sb = new StringBuilder();
		Map<Character, Integer> isp = new HashMap<>();
		isp.put('*', 2);
		isp.put('/', 2);
		isp.put('+', 1);
		isp.put('-', 1);
		isp.put('(', 0);

		Map<Character, Integer> icp = new HashMap<>();
		icp.put('*', 2);
		icp.put('/', 2);
		icp.put('+', 1);
		icp.put('-', 1);
		icp.put('(', 3);
		postfixStack.add('('); // NullpointerException을 막기 위해

		for (char x : infixCharArr) {
			if (48 <= x && x <= 57) { // 연산자일때
				sb.append(x);
			} else if (x == ')') { // 피연산자 중 닫는 괄호일 때
				while (true) {
					char a = postfixStack.pop();
					if (a == '(') {
						break;
					} else {
						sb.append(a);
					}
				}
			} else { // 피연산자 중 닫는 괄호가 아닐 때
				if (icp.get(x) > isp.get(postfixStack.peek())) {
					postfixStack.push(x);
				} else {
					while (!(icp.get(x) > isp.get(postfixStack.peek()))) {
						char a = postfixStack.pop();
						sb.append(a);
					}
					postfixStack.push(x);
				}
			}
		}

		while (postfixStack.peek() != '(') {
			sb.append(postfixStack.pop());
		}
		return sb.toString();
	}

	public static int calcPostfix(String expr) {
		char[] PostfixChar = expr.toCharArray();
		Stack<Integer> intStack = new Stack<>();

		for (char x : PostfixChar) {
			if (48 <= x && x <= 57) {
				intStack.push(((int) x - 48));
			} else {
				int a = intStack.pop();
				int b = intStack.pop();
				if (x == '-')
					intStack.push(b - a);
				else if (x == '+')
					intStack.push(b + a);
				else if (x == '*')
					intStack.push(b * a);
				else if (x == '/')
					intStack.push(b / a);
			}
		}
		return intStack.pop();
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int testCase = 10;
		for (int tc = 1; tc <= testCase; tc++) {
			sc.next();
			String infixString = sc.next();
			System.out.printf("#%d %d\n", tc, calcPostfix(infixToPostfix(infixString)));
		}
	}

}

```