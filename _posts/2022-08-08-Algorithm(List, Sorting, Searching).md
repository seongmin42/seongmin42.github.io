---
layout: post
title: Algorithm1
subtitle: List, Sorting, Searching
categories: Algorithms
tags: [algorithms]
---

## 알고리즘

**무엇이 좋은 알고리즘인가?**

  1. 정확성 : 얼마나 정확하게 동작하는가
  2. 작업량 : 얼마나 적은 연산으로 원하는 결과를 얻어내는가
  3. 메모리 사용량 : 얼마나 적은 메모리를 사용하는가
  4. 얼마나 단순한가
  5. 최적성 : 더이상 개선할 여지 없이 최적화 되었는가

**주어진 문제를 해결하기 위해 여러개의 다양한 알고리즘이 가능**

  → 어떤 알고리즘을 사용해야 하는가

**알고리즘의 성능 분석 필요**
- 많은 문제에서 성능 분석의 기분으로 알고리즘의 작업량을 비교한다.

- 등차수열의 합 문제에서 n-1번의 연산을 할 것인지, 3번의 연산을 할 것인지


| 알고리즘 1 | 알고리즘 2 |
|---|---|
|1+2+3+... = 100| $ 100 \times (100+1) \over 2 $=5500|
| 99번의 연산 | 3번의 연산|


알고리즘의 작업량을 표현할 때 시간 복잡도로 표현한다.

**시간 복잡도(Time Complexity)**

  + 실제 걸리는 시간을 측정
  + 실행되는 명령문의 개수를 계산


**시간 복잡도 ~ 빅-오(O) 표기법**

  + 시간 복잡도 함수 중에서 가잔 큰 영향력을 주는 n에 대한 항 만을 표시
  + 계수는 생략하여 표시
  + Example
    + O(3n+2) = O(3n) = O(n)
    + O(2n^2 + 10n + 100) = O(n^2)
    + O(4) = O(1)
<br>

## 배열

<b>배열이란?</b>

- 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료 구조

**배열의 필요성**
- 프로그램 내에서 여러 개의 변수가 필요할 때 일일이 다른 변수명을 이용하여 자료에 접근하는 것은 매우 비효율적일 수 있다.
- 배열을 사용하면 하나의 선언을 통해서 둘 이상의 변수를 선언할 수 있다.
- 단순히 다수의 변수 선언을 의미하는 것이 아니라, 다수의 변수로는 하기 힘든


**1차원 배열의 선언**
- 자료형 : 배열을 이루는 자료형
- 이름 : 프로그램에서 사용할 배열의 이름
- 길이 : 배열을 이루는 원소의 수
- 배열을 선언하면 힙 영역에 배열의 value들이 할당


**1차원 배열의 접근**
- array[idx]를 통해 접근


**1차원 배열의 순회**

배열의 요소를 빠짐없이 조사하는 방법
```
for(int i = 0; i < N; i++){
    ...
}
```
→ 값에 접근이 가능하다.

```
for(int i : arr){
    ...
}
```
→ 값에 접근이 불가능하다.

거꾸로 순회
```
for(int i = N-1 ; i >= 0 ; i--){
    ...
}
```
```
for(int i=0 ; i<N ; i++){
    ...arr[n-1-i]...
}
```
→ 인덱스를 조정하는 방법
<br>

## 정렬

#### 정렬

**2개 이상의 자료를 특정 기준에 의해 작은 값부터 큰 값(오름차순), 혹은 그 반대의 순서대로 재배열하는 것**

**키** : 자료를 정렬하는 기준이 되는 특정 값

**대표적인 정렬 방식의 종류**
- 버블 정렬 (Bubble Sort)
- 선택 정렬 (Selection Sort)
- 카운팅 정렬 (Counting Sort)
- 삽입 정렬 (Insertion Sort)
- 병합 정렬 (Merge Sort)
- 퀵 정렬 (Quick Sort)
<br>

#### 버블 정렬

**인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식**

**정렬과정**

- 첫 번째 원소부터 인접한 웒소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다.
- 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다.
- 교환하며 자리를 이동하는 모습이 물 위에 올라오는 거품 모양과 같다고 하여 버블 정렬이라고 한다.

**시간 복잡도**
- O($ n^{2} $)

*참고 : 컴퓨터에서 swap을 하기 위해서는 빈 변수가 필요하다.*


Ex > [55, 7, 78, 12, 42] 5개 원소를 정렬해보자.
>**첫번째 사이클**<br>
>첫 번쨰에서 인접한 두 원소 정렬<br>
>[<span style="color:red">7, 55</span>, 78, 12, 42]<br>
>두 번째에서 55와 78은 swap이 일어나지 않는다.<br>
>78과 12에서는 swap이 발생한다.<br>
>[7, 55, <span style="color:red">12, 78,</span> 42]<br>
>[7, 55, 12, <span style="color:red">42, 78</span>]<br>
>**두번째 사이클**<br>
>[7, <span style="color:red">12, 55,</span> 42, 78]<br>
>[7, 12, <span style="color:red">42, 55,</span> 78]<br>
>**세번째 사이클**<br>
>더 이상 swap이 발생하지 않는다.<br>

반복문이 두개가 필요하며, 첫 번째 반복문은 몇 회를 시행할 지, 두 번째 반복문은 인접한 원소를 비교하기 위해 필요하다.

**코드 구현**
```java
import java.util.Arrays;

public class BubbleSort {
	
	public static void main(String[] args) {		
		int[] arr = {7, 55, 12, 78, 42};
		
		int temp;
		for(int i=0; i<arr.length; i++) {
			for(int j=i; j<arr.length-1; j++) {
				if(arr[j] > arr[j+1]) {
					temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
		
		System.out.println(Arrays.toString(arr));
	}
}
```
<br>

#### 셀렉션 알고리즘
저장되어 있는 자료로부터 k번재로 큰 혹은 작은 원소를 찾는 방법

**선택 과정**
- 셀렉션은 아래와 같은 과정을 통해 이루어진다.
  - 정렬 알고리즘을 이용하여 자료 정렬하기
  - 원하는 순서에 있는 원소 가져오기

**아래로부터 k번재로 작은 원소를 찾는 알고리즘**
- 1부터 k번째까지 작은 원소들을 찾아 배열의 앞쪽으로 이동시키고, 배열의 k번째를 반환한다.
- k가 비교적 작을때 유용하며 O(kn)의 수행시간을 필요로 한다.
<br>

#### 선택정렬
포켓볼 공을 순서대로 정렬하는 방식
- 셀렉션 알고리즘을 전체 자료에 적용한 것

**정렬 과정**
1. 주어진 리스트 중에서 최소값을 찾는다.
2. 그 값을 리스트의 맨 앞에 위치한 값과 교환한다.
3. 맨 처음 위치를 제외한 나머지 리스트를 대상으로 위의 과정을 반복한다.

Ex > [123, 64, 321, 88, 87, 12, 8] 정렬해보기

> 1. 현재 첫 번째 위치에서 가장 작은 값 123을 담고 있는 인덱스 0으로 초기화를 한다.
> 2. 두 번째 위치에서 가장 작은 값은 64이고 minidx는 1이 된다.
> 3. 계속 뒤의 원소들과 비교해가며 minidx를 갱신한다. → minidx = 6
> 4. minidx에 있는 원소를 첫 번째 idx(idx=0)에 있는 원소와 swap한다.
> 5. 두 번째 위치부터 다시 minidx를 갱신하고, 그를 두번재 위치(idx=1)에 위치시킨다.
> 6. 위 시행을 반복한다.

**구현**
```java
import java.util.Arrays;

public class SelectionSort {
	public static void main(String[] args) {
		int[] arr = { 123, 64, 321, 88, 87, 12, 8 };

		for (int i = 0; i < arr.length - 1; i++) {
			int minIdx = i;
			for (int j = i + 1; j < arr.length; j++) {
				if (arr[j] < arr[minIdx]) {
					minIdx = j;
				}
			}
			int temp = arr[i];
			arr[i] = arr[minIdx];
			arr[minIdx] = temp;
		}

		System.out.println(Arrays.toString(arr));
	}
}

```

## 검색

#### 검색

-   저장되어 있는 자료 중에서 원하는 항목을 찾는 작업
-   목적하는 탐색 키를 가진 항목을 찾는 것
    - 탐색 키 : 자료를 구별하여 인식할 수 있는 키
-   검색의 종류
    - 순차 검색
    - 이진 검색
    - 인덱싱

**순차 검색**
일렬로 되어 있는 자료를 순서대로 검색하는 방법
- 가장 간단하고 직관적인 검색 방법
- 배열이나 연결 리스트 등 순차 구조로 구현된 자료 구조에서 원하는 항목을 찾을 때 유용
- 알고리즘이 단순하여 구현이 쉽지만, 검색 대상의 수가 많은 경우에는 수행 시간이 급격히 증가하여 비효율적
- 정렬되어 있는 경우 / 정렬되어 있지 않음
  → 시간 복잡도는 같으나 구현 방법은 다름

**검색과정(정렬되어 있지 않은 경우)**
1. 첫 번째 원소 부터 순서대로 검색 대상과 키 값이 같은 원소가 잇는지 비교하며 찾는다.
2. 키 값이 동일한 원소를 찾으면 그 원소의 인덱스를 반환한다.
3. 자료구조의 마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패

찾고자 하는 원소의 순서에 따라 비교 횟수가 결정됨
- 첫 번째 원소를 찾을 때는 1번 비교, 두 번째 원소를 찾을 떄는 2번 비교
- 정렬되지 않은 자료에서의 순차 검색의 평균 비교 회수
$(1/n)*(1+2+...+n) = (n+1)/2$
- 시간 복잡도 : O(n)

**구현 코드**
```java
public class SequentialSearch {
	static int[] arr = { 123, 64, 321, 88, 87, 12, 8 };

	static int searchForNoSort(int key) {
		for(int i = 0 ; i < arr.length; i++) {
			if(arr[i]==key) return i;
		}
		return -1;
	}
	
	public static void main(String[] args) {
		System.out.println(searchForNoSort(321));  //2 출력
	}
}
```
**검색과정(정렬되어 있는 경우)**
- 자료가 오름차순으로 정렬되어 있을 때는, 자료를 순차적으로 검색하면서 키 값을 비교하여, 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 것이므로 더 이상 검색하지 않고 검색을 종료한다.
  
**코드**
```java

public class SequentialSearch {
	static int[] arr = { 64, 321, 88, 123, 87, 12, 8 };
	
	static void selectionSort(int[] notSorted)  {
		for (int i = 0; i < notSorted.length - 1; i++) {
			int minIdx = i;
			for (int j = i + 1; j < notSorted.length; j++) {
				if (notSorted[j] < notSorted[minIdx]) {
					minIdx = j;
				}
			}
			int temp = notSorted[i];
			notSorted[i] = notSorted[minIdx];
			notSorted[minIdx] = temp;
		}
	}
		
	static int searchForNoSort(int key) {
		for(int i = 0 ; i < arr.length; i++) {
			System.out.println(i);
			if(arr[i]==key) {
				return i;
			}
		}
		return -1;
	}
	
	static int searchForSort(int key) {
		for(int i = 0 ; i < arr.length; i++) {
			System.out.println((i));
			if(arr[i]==key) return i;
			if(arr[i]>key) {
				break;
			}
		}
		return -1;
	}
	
	public static void main(String[] args) {
		System.out.println("searchForNoSort : " +  searchForNoSort(123));
		selectionSort(arr);
		System.out.println("searchForSort : " + searchForSort(65));
	}
	
}

/*
0
1
2
3
searchForNoSort : 3
0
1
2
3
searchForSort : -1
*/
```
<br>
#### 이진 검색

자료가 정렬되어 있어야 함이 전제

자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법

시간복잡도 : $O(log_2 n)$

**검색 과정**
1. 자료 중앙에 있는 원소를 고른다
2. 중앙 원소의 값과 찾고자 하는 목표의 값을 비교한다.
3. 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다.
4. 찾을 때까지 위의 수행을 반복한다.

```java
public class BinarySearch {

	static int[] arr = { 2, 8, 15, 22, 23, 46, 67, 75, 132 };

	static int binarySearch(int key) {
		int ind, a=0, b=arr.length;
		while(true) {
			ind = (a+b)/2;
			if(arr[ind]==key) return ind;
			else if(arr[ind]>key) {
				b=ind;
				if(b-a==1) return -1;
			}
			else if(arr[ind]<key) {
				a=ind;
				if(b-a==1) return -1;
			}
		}
		
	}

	public static void main(String[] args) {
		System.out.println(binarySearch(14));
	}

}
```
**구현**

검색 범위의 시작점과 종료점을 이용하여 검색을 반복 수행한다.

이진 검색의 경우, 자료에 삽입이나 삭제가 발생했을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업이 필요하다.

재귀 함수 이용를 이용하여 구현할 수 있다.
<br>
#### 인덱스

인덱스라는 용어는 Database에서 유래했으며, 테이블에 대한 동작 속도를높여주는 자료 구조를 일컫는다. Database 분야가 아닌 곳에서는 Look up table 등의 용어를 사용하기도 한다.

인덱스를 저장하는데 필요한 디스크 공간은 보통 테이블을 저장하는데 필요한디스크 공간보다 작다. 왜냐하면 보통 인덱스는 키-필드만 갖고 있고, 테이블의다른 세부 항목들은 갖고 있지 않기 때문이다. 

배열을 사용한 인덱스
- 대량의 데이터를 매번 정렬하면, 프로그램의 반응은 느려질 수 밖에 없다. 이러한 대량 데이터의성능 저하 문제를 해결하기 위해 배열 인덱스를 사용할 수 있다.
<br>

## 완전 검색

#### Baby-gin Game

0~9 사이의 숫자 카드에서 중복을 허용하여 임의의 카드 6장을 뽑았을 때, 3장의 카드가 연속적인 번호를 갖는 경우를 run이라 하고, 3장의 카드가 동일한 번호를 갖는 경우를 triplet이라고 한다.

6장의 카드가 run과 triplet으로만 구성된 경우를 baby-gin으로 부른다.
<br>

#### 완전 검색(Brute-force / Generate-and-Test)

완전 검색 방법은 문제의 해법으로 생각할 수 있는 모든 경우의 수를 나열해보고 확인하는 기법

경우의 수가 상대적으로 작을 때 유용

모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만 해답을 찾아내지 못할 확률이 작다.
<br>

#### 완전 검색을 활용한 Baby-gin 접근

고려할 수 있는 모든 경우의 수 생각하기
- 6개의 숫자로 만들 수 있는 모든 숫자를 나열하고, 앞의 세 자리와 뒤의 세 자리의 run과 triplet 여부를 테스트하고 baby-gin 판단
<br>

#### 순열

서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것
<br>

## 탐욕(Greedy) 알고리즘

최적해를 구하는데 사용되는 근시안적인 방법

여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달한다.

각 선택의 시점에서 이루어지는 결정은 지역적으로는 최적이지만, 전역적으로는 아닐 수도 있다.

일반적으로, 머릿속에 떠오르는 생각을 검증 없이 바로 구현하면 Greedy 접근이 된다.

**동작 과정**

1. 해 선택 : 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분 해 집합에 추가한다.
2. 실행 가능성 검사 : 새로운 부분 해 집합이 실행 가능한 지를 확인한다.(문제의 제약 조건을 위반하지 않는지 검사)
3. 해 검사 : 새로운 부분 해 집합이 문제의 해가 되는지를 확인한다. 아직 전체 문제의 해가 완성되지 않았다면 1번부터 다시 시행한다.

eg ) 거스름돈 갯수 최소화하기

