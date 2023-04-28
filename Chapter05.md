1.배열 
================
## 1.배열
**같은 타입의 여러 변수를 하나의 묶음으로 다루는 것**   

---
## 2.배열의 길이와 인덱스

### 1.인덱스    
    배열의 각 저장공간을 배열의 요소 라고 하며 배열이름을 인덱스라고 한다.   
    인덱스는 0부터 배열의 길이-1 까지 있음

### 2. 배열의 길이
    배열을 생성할때 "타입[] 배열이름 = new 타입[길이]" 와 같이 길이를 설정하여준다.   
**배열의 길이는 int범위의 양의 정수 이여야 한다.**

### 3. 배열이름.length
    배열이름.length를 통해 배열 길이의 대한 정보를 받을수 있다.
    
---    
## 3.배열의 초기화

```
int[] a = new int[5];
	a[0] = 10;
	a[1] = 20;
``` 
위와 같이 배열을 초기화 하거나   
```
int[] a = new int[]{10,20,30,40,50};
```
과 같이 생성과 초기화를 동시에 해줄수있다.

---
## 4.배열의 복사

### 1. for문을 이용한 배열의 복사
```
int[] arr = new int[5];
	int[] tmp = new int[arr.length*2];
	
	for(int i = 0; i < arr.length;i++){
		tmp[i] = arr[i]; //arr[i]의 값을 tmp[i] 에저장
	}
	arr = tmp;
```
세로운 배열로 저장 된다.

### 2.  System.arraycopy()를 이용한 복사
```
System.arraycopy(num,0,newNum,0,num.length);
```
num[0]에서 newNum[0]으로 num.length개의 데이터를 복사   
for문을 사용하는것보다 효율적이다.

---
2.String배열
===
## 1.배열생성
``` String[] name = new String[3]; ```
3개의 문자열을 담을 수 있는 배열 생성

|자료형|기본값|
|---|---|
|boolean|false|
|char|'\u0000'|
|byte,short,int|0|
|long|0L|
|float|0.0f|
|double|0.0d 또는 0.0|
|참조형 변수|null|

---
##  2. char배열과 String클래스
	String 클래스는 char 배열에 기능을 추가한것 
---
## 3. 커맨드 라인을 통해 입력 받기
	java MainTest abc 123 으로 하여    
	main args에 args[0] 과 args[1] 에 각각 abc, 123으로저장 가능하다 
	
---
## 4. 다차원 배열 
	타입[][] 변수이름;   
	타입 변수이름[][];   
	타입[] 변수이름[];   
위와 같은형태로 생성 가능하다.
