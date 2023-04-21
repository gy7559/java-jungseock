조건문과 반복문
===
1.조건문
----
### 1_if
 ```
 if(조건식){   
	}
  ```
	조건식이 참일경우 {}안의 문장을 실행함
  
### 2_if-else

```
if(조건식){
	}
	else{
	}
```
	조건식이 거짓일경우 else{}안의 문장을 실행함
  
### 3_if-else if 문
```
if(조건식1){
	}조건식1이 참일떄 실행
	else if(조건식2){
	}조건식2가 참일떄 실행
	else{
	}위조건식이 모두 거짓일때 실행
 ```
### 4_중첩 if문 
```
if문안에 if문을 사용하는것
	if(조건식1){
		if(조건식2){
		}
	}
```
 ### 5_switch문
 ```
 switch(조건식){
		case 값1:case 1내용
			break;
		case 값2:case2내용
			break;
		case 값3:case 3내용
			break;
		default:
	}
 ```
 조건식의 계산된값과 같은 case의 내용을 실행 같은것이 없을경우 default실행
 
 **제약조건**   
* 조건식의 결과는 정수 또는 문자열 이여야 한다.
*	case문의 값은 상수 만 가능하며 중복되지 않아야 한다.

---
2.반복문
---
### 1_for문
1. for문
```
for(초기화;조건시;증감식;){
		수행될 문장
	}
```
2. 중첩 for문
```
 for(){
		for(){
		}
	 }
```
3. 향상된 for문
for(타입 변수명 : 배열 또는 컬렉션){
	반복내용
	}
```
for(int i=0;i<arr.length; i++){
		System.out.println(arr[i]);
	}
```
 ->
 ```
 for(int tmp : arr){
		System.out.println(tmp);
	}
```
위와같이 표현 가능

