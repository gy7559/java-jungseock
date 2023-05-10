# 1. 예외처리

## 1. 예외처리

### 1. 프로그램오류
프로그램이 비정상적으로 종료되거나 오작동을 하는경우 프로그램에러 혹은 오류가 있다고 한다.      
이 오류의 발생시점에 따라 2가지로 나눌수 있다.     

    컴파일 에러 : 컴파일시 발생하느 에러
    런타임 에러 : 실행시 발생하는 에러
    
이와 다르게 실행은 되지만 의도한것과 다르게 작동하는것을 **논리적 에러**라고 한다.   
   
오류와 에러의 차이는 아래와 같다.
      
    에러 : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
    오류 : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류
      
  
### 2. 예외 클래스의 계층구조

예외클래스(Exception)와 오류클래스(Error)역시 object클래스의 자손이다.     
그리고 각각 예외클래스와 오류클래스의 최고 조상 클래스이다.      
        
예외 클래스는 두그룹으로 나눠진다.

Exception클래스와 자손, RuntimeException클래스와 자손으로 나눠질수 있다.   


        Exception클래스 : 사용자의 실수와 같은 외적인 요이ㅣㄴ에 의해 발생하는 예외
        RuntimeException클래스 : 프로그래머의 실수로 발생하는 예외  
       
       
### 3. 예외처리하기 - try-catch문        

    예외처리(exception handling)
        정의 - 프로그램 실행 시 발생할 수 있는 예외 에 대비한 코드를 작성 하는것
        목적 - 프로그램의 비정상 종료를 막고, 정상적인 실행 살태를 유지하는것
          
 try-catch문 예제
 ```java
 public class ExceptionEx1 {

	public static void main(String[] args) {
		try {
			try { } catch(Exception e) { }
		} catch(Exception e) {
			try { } catch(Exception e ) {} // 에러. 변수 e가 중복 선언되었다.
		}// try-catch의 끝

		
		try {
			
		} catch (Exception e) {
			
		}//try-catch의 끝
		
		
	}// main메서드의 끝

}
 ```


### 4. try-catch문에서의 흐름   

예외가 발생한 경우와 발생하지 않은경우의 흐름   

발생한경우    
1. 발생한 예외와 일치하는 catch블럭이 있는지 확인
2. 일치하는 블럭이 있다면 블럭내의 문장을 수행후 try-catch문을 빠져나가서 다음문장을 실행   
찾지못하면 예외처리 불가   


발생하지 않은경우   
catch블럭을 거치지 않고 try-catch문을 빠져나가서 다음문장을 실행   

### 5. 메서드의 예외선언

메서드 선언부에 키워드 throws를 사용해서 예외 지정
```java
void method() throws Exception01, Exception2,... ExceptionN{
	///메서드의 내용
}
```

### 6. finally블럭	

예외에 발생여부에 상관없이 실행되어야 할 코드를 포함 시킬 목적으로 사용된다.     

 try-catch-finally의 순서로 구성 된다.
 
 
	
	
	
