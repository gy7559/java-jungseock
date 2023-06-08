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

Thread클래스를 상속받으면 Thread의 메서드를 직접 호출이 가능하지만      
Runnable을 구현하였을경우 Thread클래스의 static메서드인 currentThread()를 호출하여 쓰레드에대한 참조를 받아와야 호출이 가능하다.     

	static Thread currentThread()	: 현재 실행중인 쓰레드의 참조를 반환
	String getName			: 쓰레드의 이름을 반환
	
ex)
```java
class ThreadEx1_1 extends Thread{
	public void run() {
		for(int i =0; i<5; i++) {
			
			System.out.println(getName());//조상인 Thread의 gryName()을 호출
		}
	}
}

class ThreadEx1_2 implements Runnable{
	public void run() {
		for(int i =0; i<5;i++) {
			// Thread.currentThread() - 현재 실행중인 Thread를 반환한다.
			System.out.println(Thread.currentThread().getName());
		}
	}
}
```

**쓰레드의 실행**
쓰레드를 생성했다고 자동으로 실행되는것이 아닌         
start()를 호출해야 실행된다.      
start()를 호출하면 실행대기상태로 호출스택에 쌓이게된다.       

start()를 호출하고 다시 호출하기위해서는 쓰레드를 새로 생성 해주어야 한다.     

 
## 3. start()와 run()

start()가 main메서드에서 run()을 호출하여 main과 별개로 호출스택을 생성 run()이 작업을 한다.    
run()이 호출되고나면 start()는 사라진다.     
실행중인 사용자 쓰레드가없을경우 프로그램은 종료 된다.     

## 4. 싱글 쓰레드와 멀티 쓰레드 
싱글코어의 경우 CPU만을 사용하는 계산작업의 경우는 싱글쓰레드의 경우가 더 효율적이다.        


멀티코어의 경우는 실글코어와 다르게 두작업이 겹치면서 실행되기때문에 자원들두고 경쟁하게 된다.     
하지만 다른 자원을 사용하는 경우 멀티쓰레드의 경우가 효율적이다.      



## 5. 쓰레드 우선순

특정작업에서 중요도에 따라 우선순위를 다르게 두어 작업하는것      

**우선순위 지정하는법**
```java
void setPriority(int newPriority)	// 쓰레드의 우선순위를 지정한 값으로 변경한다.
int getPriority()			// 쓰레드의 우선순위를 반환

public static final int MAX_PRIORITY = 10 // 최대우선순위
public static final int MIN_PRIORITY = 1  // 최소우선순위
public static final int NORM_PRIORITY = 5  // 보통우선순위
```

## 6. 쓰레드 그룹
쓰레드를 모아두는 폴더처럼 서로 관련된 쓰레드를 묶어서 관리하는 것이다.      

ThreadGroup을 사용해서 생성할수 있다.        
주요 생성자와 메서드
|생성자/메서드|내용|
|---|---|
|ThreadGroup(String name)|지정된 이름의 새로운 쓰레드 그룹을 생성|
|ThreadGroup(ThreadGroup parent,String name)|지정된 쓰레드 그룹에 포함되는 새로운 쓰레드 그룹을생성|
|int activeCount()|쓰레드 그룹에 포함된 활성상태에 있는 쓰레드의 수를 반환|
|int activeGroupCount()|쓰레드그룹에 포함된 활성상태에 있는 쓰레드 그룹의 수를 반환|
|void checkAccess()|현재 실행중인 쓰레드가 쓰레드 그룹을 변경할 권한이 있는지 체크. 권한이없으면 SecurityException을 발생시킨다.|
|void destroy()|쓰레드 그룹과 하위 쓰레드 그룹까지 모두 삭제한다. 단, 쓰레드그룹이나 하위 쓰레드그룹이 비어있어야 한다.|
|int getMaxPriority()|쓰레드 그룹의 최대 우선순위를 반환|
|String getName()|쓰레드 그룹의 이름을 반환|
|ThreadGroup getParent()|쓰레드 그룹에 상위 쓰레드 그룹을 반환|
|void interrupt()|쓰레드 그룹에 속한 모든 쓰레드를 interrupt|
|boolean isDaemon()|쓰레드 그룹이 데몬쓰레드 그룹인지 확인|
|boolean isDestroyed|쓰레드 그룹이 삭제되었는지 확인|
|void list()|쓰레드 그룹에 속한 쓰레드와 하위 쓰레드그룹에 대한 정보를 출력|
|boolean parentOf(ThreadGroup g)|지정된 쓰레드 그룹의 상위 쓰레드그룹 인지 확인|
|void setDaemon(boolean daemon)|쓰레드 그룹을 데몬 쓰레드그룹으로 설정/해제|
|void setMaxPriority(int pri)|쓰레드 그룹의 최대우선순위를 설정|
|int enumerate(Thread[] list),(Thread[] list, boolean recurse),(ThreadGroup[] list),(ThreadGroup[] list,boolean recurse)|쓰레드 그룹에 속한 쓰레드 또는 하위 쓰레드 그룹의 목록을 지정된 배열에 담고 그 개수를 반환,   두번째 매개변수인 recurse의 값을 true로 하면 쓰레드 그룹에 속한하위 쓰레드 그룹에 쓰레드 또는 쓰레드 그룹까지 배열에 담는다.|
