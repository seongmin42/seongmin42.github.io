---
layout: post
title: 재귀를 활용한 부분집합 구현
subtitle: 
categories: Algorithms
tags: [algorithms, subset, recursive, stack, function call]
---

재귀함수를 통해 부분집합을 다음과 같이 구현할 수 있다.

## 코드 구현


```java
public class SubsetImplement {
	static int[] arr = { 3, 6, 9 };  // 모집합
	static boolean[] check = new boolean[arr.length];  // 모집합의 원소를 골랐는지 여부를 파악할 배열

	public static void main(String[] args) {
		powerSet(0);
	}

	static void powerSet(int idx) {
		// 부분 집합이 전부 골라졌으면
		if (idx == arr.length) {
			for (int i = 0; i < arr.length; i++)
				if (check[i])
					System.out.print(arr[i] + " ");
			System.out.println();
			return;
		}
		check[idx] = true;  // idx번째 원소를 고름
		powerSet(idx + 1);
		check[idx] = false;  // idx번째 원소를 안고름
		powerSet(idx + 1);
	}
}
```
```
3 6 9 
3 6 
3 9 
3 
6 9 
6 
9 
    // 공집합
```


## 상세 설명 

1. main함수에서 powerSet(0)이 호출된다.
2. powerSet(0) : 19번째 줄에서 powerSet(1), powerSet(2), powerSet(3)이 순차적으로 시행
3. powerSet(3) : 11번째 줄에서 idx == 22가 만족을 하여 3 6 9 를 출력하고 powerSet(3)을 호출했던 powerSet(2)로 돌아감
4. powerSet(2) : 20번째 줄에서 check[2]가 false로 바뀌고 21번째 줄에서 powerSet(3) 호출
5. powerSet(3) : 3 6을 출력하고 다시 powerSet(2)로 돌아가지만, 모든 시행이 끝난다. 그 뒤에는 powerSet(1)의 21번째 줄에서 powerSet(2)가 시행되고 powerSet(2)의 19번째 줄에서 powerSet(3)을 호출한 뒤 3 9를 호출한다.
6. powerSet(0)의 21번째 줄이 시행될 때까지 이를 반복한다.

function call은 Stack 위에서 이루어진다. 이를 유념하여 생각하면 편하다.

## 주의 사항

다음과 같은 부분집합법 메소드를 작성했다고 하자.

```java
// 잘못된 사례

static void func(int var, StringBuilder sb, int depth){
	// 기저 조건
	if(depth == 7){
		~~~  // (a)
		return;
	}

	depth++;
	sb.append(var);
	func(var, sb, depth);
}
```

위의 경우, depth가 기저 조건을 만족할 때까지 재귀를 반복하다가, 기저조건에 도달하면 해당 조건문(a)을 수행한 후 그 재귀함수를 호출했던 메소드로 돌아간다.
이 때, 재귀 전에 수행한 sb.append("var")은 참조자료형이기 때문에 주소값이 계속해서 공유되기 때문에 잘못된 결과를 초래할 수 있다. 기본 자료형인 int depth는 함수 호출때마다 생성과 소멸을 반복하기 때문에 공유되지 않는다.

이를 해결하기 위해 다음과 같이 함수를 설정하면 된다.

```java
// 올바른 사례

static void func(int var, StringBuilder sb, int depth){
	// 기저 조건
	if(depth == 7){
		~~~  // (a)
		return;
	}

	depth++;
	func(var, sb.append(var), depth);
}
```