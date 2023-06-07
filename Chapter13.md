# 쓰레드

## 1. 프로세스와 쓰레드
프로세스 = 실행중인 프로그램           
쓰레드 = 프로세스안에서 자원을 이용하여 실제 작업을 수행하는것     
두가지 이상의 쓰레드를 갖고 있는 프로세스를 *멀티쓰레드 프로세스* 라고 한다.       

**멀티쓰레딩의 장단점**      
장점   
    
    1. CPU의 사용률을 향상 시킨다.
    2. 자원을 보다 효율적으로 사용할 수 있다.
    3. 사용자에 대한 응답성이 향상된다.
    4. 작업이 분리되어 코드가 간결해진다.


단점 

    여러 쓰레드가 같은 프로세스 내에서 자원을 공유하면서 작업을 하기 때문에
    동기화,교착상태 와 같은 문제들을 고려해서 프로그래밍 해야한다.     


## 2. 쓰레드의 구현과 실행

 구현 
 
 Thread클래스를 상속받는 방법
 ```java
 class MyThread extends Thread{
    public void run(){/* 작업 내용 */} // Thread클래스의 run()오버라이딩
 }
 ```
 Runnable인터페이스 구현
 ```java
  class MyThread implements Runnable{
    public void run(){/* 작업 내용 */} // Runnable인터페이스의 run()구현
 }
 ```
Thread클래스 상속을 받을경우 다른 클래스 상속을 받지 못하여     
Runnable인터페이스 구현을 하는것이 일반적이다.     
Runnable인터페이스 에는 run()만 정의되어있어 run()의 {}몸통 만 만들어 주면 된다.      
  
**인스턴스 생성 방법**         

Thread클래스 상속의 경우
```java
ThreadEx1_1 t1 =new ThreadEx1_1();//인스턴스 t1생성
	t1.start(); // t1실행
```
Runnable인터페이스 구현의 경우
```java
Runnable r = new ThreadEx1_2();//Runnable을 구현한 클래스의 인스턴스 r생성
		Thread t2 = new Thread(r);// r을 매개변수로 Thread(Runnable target) 생성자 통한 인스턴스 생성
    
    t2.start(); // t2 실행   
```
Runnable인터페이스 구현의 경우           
인터페이스를 구현한 클래스 인스턴스 생성후     
Thread생성자로 인스턴스를 생성해 주어야 한다.     


