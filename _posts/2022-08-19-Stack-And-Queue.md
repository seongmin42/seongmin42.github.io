---
layout: post
title: 스택(Stack)과 큐(Queue)
subtitle: 
categories: Algorithms
tags: [stack, queue, data structure]
---

## 스택

- 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료 구조
- 스택에 저장된 자료는 선형 구조를 갖는다.
  - 선형구조 : 자료 간의 관계가 1대 1의 관계를 갖는다.
  - 비선형구조 : 자료 간의 관계가 1대 N의 관계를 갖는다.

- 마지막에 삽입한 자료를 가장 먼저 꺼낸다. **(Last In First Out)**
- top을 기준으로 원소를 넣고 뺄 수 있다.


#### 연산
- push : 저장소에 자료를 저장한다. (top을 증가시키고 값 넣기, arr[++top])
- pop : 저장소에서 자료를 꺼낸다. 꺼낸 자료는 삽입한 자료의 역순으로 꺼낸다. (값을 넣고 top을 감소시키기,  arr[top--])
- isEmpty : 스택이 공백인지 아닌지를 확인하는 연산
- peek : 스택의 top에 있는 원소를 반환하는 연산


#### 구현 코드


```java
package stack;

public class MyStack {
	static int[] stack = new int[100];
	static int top = -1;
	
	static boolean isFull() {
		return top == stack.length-1;
	}
	
	static boolean isEmpty() {
		return top == -1;
	}
	
	static void stackPush(int value) {
		if(isFull()) {
			System.out.println("stack is full.");
		} else {
			stack[++top] = value;
		}
		
	}
	
	static int stackPop() {
		if(isEmpty()) {
			System.out.println("stack is empty.");
			return -1;
		} else {
			return stack[top--];
		}
	}
	
}

```

```java
package stack;

public class LinkedStackTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MyStack stack = new MyStack();
		stack.push(2);
		stack.push(4);
		stack.push(6);
		
		System.out.println(stack.pop());
		System.out.println(stack.pop());
		System.out.println(stack.pop());
		System.out.println(stack.pop());
	}

}

/*
6
4
2
stack is empty.
-1
/*
```

#### 활용 예시

괄호검사와 계산기, 실행 취소에서 스택을 이용한다. 계산기에 활용한 예제는 
https://seongmin42.github.io/algorithms/2022/08/18/infix-and-postfix.html
를 참고.

## 큐

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
- 큐의 뒤에서는 삽입(enQueue)만 일어나고 큐의 앞에서는 삭제(deQueue)만 이루어진다.
- 선입선출구조(First In First Out)

#### 연산

- enQueue : 큐에 자료를 삽입한다. (rear를 증가시키고 그 자리에 원소를 넣기, queue[++rear])
- deQueue : 큐에서 자료를 삭제하고 그 값을 반환한다. (front를 증가시키고 그 자리에 원소를 넣기, queue[++front])


#### 구현 코드

```java
package queue;

public class MyQueue {
	public static int[] queue = new int[10];
	public static int front = -1, rear = -1;
	
	public static boolean isEmpty() {
		return front == rear;
	}
	
	public static boolean isFull() {
		return rear == queue.length-1;
	}
	
	public static void enQueue(int item) {
		if(isFull()) {
			System.out.println("Queue is full.");
		} else {			
			queue[++rear] = item;
		}
	}
	
	public static int deQueue() {
		//공백인지 검사를 하고,
		if(isEmpty()) {
			System.out.println("Queue is empty.");
			return -1;
		} else {
			return queue[++front];
		}		
	}
	
	public static void main(String[] args) {
		MyQueue queue = new MyQueue();
		queue.enQueue(3);
		queue.enQueue(4);
		queue.enQueue(5);
		System.out.println(queue.deQueue());
		System.out.println(queue.deQueue());
		System.out.println(queue.deQueue());
		System.out.println(queue.deQueue());		
	}
	
}

```

