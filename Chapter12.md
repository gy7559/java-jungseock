# 12. 지네릭스, 열거형, 애너테이션

## 1. 지네릭스


### 1. 지네릭스란?
다양한 타입의 객체를 다루는 메서드나 컬랙션 클래스에 컴파일시 타입체크를 해주는 기능이다. 
타입 안정성을 높히고 형변환의 번거로움이줄어든다. 


  타입 안정성이 높다 : 의도치않은 타입의 객체가 저장되는것 을 막고 저장된 객체를 꺼내올때 잘못된 형변환이 발생하여 생기는 오류를 줄여준다.
  
  
  **장점** 
        
        1. 타입안정성이 높다
        2. 타입체크와 형변환을 생략할수 있어 코드가 간결해진다.


### 2. 지네릭 클래스의 선언

클래스 선언
```java
class Box{
  Object item;
  
  void setItem(Object item){this.item = item;}
  Object getItem(){return item;}
}
```

위와 같은 코드에서       
지네릭 클래스로 변경시     

```java
class Box<T>{
  <T> item;
  
  void setItem(T item){this.item = item;}
  T getItem(){return item;}
}
```

와 같이 클래스에 지네릭 타입<T>을 정해주어 Object를 변경해주면 된다.     
T는 Type의 T다.    
  
**지네릭스 용어**
  
class Box<T>의 경우     
  
  
    Box<T>  : 지네릭 클래스 T의 Box 또는 T Box라고 읽는다.
    T       : 타입 변수 또는 타입 매개변수.
    Box     : 원시 타입    
  

 매개변수에 타입을 지정하는 것을 지네릭 타입 호출 이라고 한다.
 
 Box<String>,Box<Integer>는 둘다 컴파일 후에는 원시타입인 Box로 바뀐다. 즉 지네릭 타입은 컴파일 전까지만 유효하다.     
  
    
 **지네릭스 제한**
  
 static멤버는 모든 객체에 동일하게 동작해야 하기 때문에 타입변수 T로 사용될수 없다.     
 T는 인스턴스변수로 간주되기 때문이다. 
  
 지네릭 타입은 배열을 생성할수 없다.
 지네릭 배열타입의 참조변수를 선언하는것은 가능하지만 new연산자를 사용하는 배열생성은 안된다.
  
 new연산자를 사용할때는 컴파일 시점에 T가 뭔지 정확히 알아야 하는대 컴파일 시점에는 T가 어떤 타입이 될지 전혀 알수없기 때문이다.    
 
        배열을 생성해야 한다면 Object 배열을 생성해서 T[]에 복사넣기를 하거나     
        newInstance()와 같이 동적으로 객체를 생성하는 메서드로 배열을 생성하는 방법이 있다.

### 3. 지네릭 클래스의 객체 생성과 사용
  
지네릭 클래스가 아래와 같이 정의 되어있을때 
```java
  class Box<T>{
  	ArrayList<T> list = new ArrayList<T>();
  
	  void add(T item) {list.add(item);}
	  T get(int i) {return list.get(i);}
	  ArrayList<T> getList(){return list;}
	  int size() {return list.size();	}
	  public String toString() {return list.toString();}
}
```

객체 생성시
```java
  Box<Apple> appleBox = new Box<Apple>();
  Box<Grape> grapeBox = new Box<Apple>();//에러
```
위와 같이 참조자와 생성자에 대입된 타입을 일치 시켜줘야 한다.   
두 타입이 상속 관계여도 일치시켜줘야 하며   
단 클래스 타입이 상속관계에 있을경우 대입된 타입이 같은것은 괜찮다.         
  

```java
  Box<Apple> appleBox = new FruitBox<Apple>();
```
FruitBox가 Box의 자손이라 가정하였을경우
  
 또한 .add(T item)를 사용하여 객체를 추가할때 대입된 타입과 다른 타입은 추가할수없다.
  단 대입된 타입의 자손 타입들은 매개변수가 될수있다.
  
 
### 4. 제한된 지네릭 클래스
  타입 매개변수 T에 지정할 타입의 종류를 제한하는 방법
  
  ```java
    class FruitBox<T extends Fruit> {
      ArrayList<T> list = new ArrayList<T>();
    ...
  }
  ```
  
  위와 같이 지네릭 타입에 extends를 사용하여 Fruit클래스와 그 자손들만 담을수있게 제한을 추가했다.       
  클래스가 아닌 인터페이스를 구현해야되는 제약 또한 extends를 사용한다.     
  
  Fruit의 자손이면서 Eatable의 인터페이스 또한 구현해야 한다면 &기호로 연결하여 준다.
  ```java
    class FruitBox<T extends Fruit & Eatable> {}
  ```
  

	
### 5. 와일드 카드
static 메서드에서 지네릭타입을 사용해야될때
오버로딩을 통한 구현이 되지 문제가 발생한다.
	
	```java
		class Juicer{
	static Juice makeJuice(FruitBox<Fruit> box) { 
		String tmp = "";
		
		for(Fruit f : box.getList())
			tmp += f + " ";
		return new Juice(tmp);
	}
	}
	```
위와 같은 상황일 경우 Fruit가 아닌 Apple을 넣기위해서 오버로딩(같은이름의 메서드를 다른 매개변수를 지정하여 만드는것)을 하면      
컴파일 에러가 발생한다.   
지네릭타입은 컴파일후 제거되기 때문에 중복 메서드 정의가 되어버린다.
	
이때 와일드 카드를 이용하여 상한제한 혹은 하한 제한을 두어 대입타입의 자손 혹은 조상 만사용할수있도록 정의해주는것이다.
```java
		class Juicer{
	static Juice makeJuice(FruitBox<? extends Fruit> box) { 
		String tmp = "";
		
		for(Fruit f : box.getList())
			tmp += f + " ";
		return new Juice(tmp);
	}
	}
```	
<? extends Fruit> = 상한 제한으로 Fruit와 그 자손들만 가능하다.

	<? extends T> 	: 상한제한 T와 그 자손만 가능
	<? super T>	: 하한제한 T와 그 조상만 가능
	<?>		: 제한없음 모든 타입 가능

	
와일드 카드를 이용한 제한에 
		```java
		FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
		FruitBox<Apple> appleBox = new FruitBox<Apple>();
		 ...
		 System.out.println(Juicer.makeJuice(fruitBox));
		 System.out.println(Juicer.makeJuice(appleBox));
		```
Fruit와 Apple둘다 Juicer의 메서드인 makeJuice의 매개변수 FruitBox의 변수타입으로 사용이 가능하다.
	
	
	
### 6. 지네릭 메서드
	

