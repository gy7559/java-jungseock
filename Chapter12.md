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

'<? extends Fruit>" = 상한 제한으로 Fruit와 그 자손들만 가능하다.   


	"<? extends T>"	: 상한제한 T와 그 자손만 가능
	"<? super T>"	: 하한제한 T와 그 조상만 가능
	"<?>"		: 제한없음 모든 타입 가능

	

와일드 카드를 이용한 제한으로   
	 
```java
	FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
	FruitBox<Apple> appleBox = new FruitBox<Apple>();
	 ...
	 System.out.println(Juicer.makeJuice(fruitBox));
	 System.out.println(Juicer.makeJuice(appleBox));
```
	
Fruit와 Apple둘다 Juicer의 메서드인 makeJuice의 매개변수 FruitBox의 변수타입으로 사용이 가능하다.    
	
	
	
### 6. 지네릭 메서드
	
	
```java
	static <T> void sort(List<T> list, Comparator<? super T> c)	
```
와 같이 메서드에 지네릭 타입을 선언된것을 지네릭 메서드라고 한다.    

지네릭클래스에 정의된 타입 매개변수와 지네릭 메서드에 정의된 타입 매개변수는 전혀 별개의 것이다.       

```java
class FruitBox<T>{
	static <T> void sort(List<T> list, Comparator<? super T> c){}	
	}
```
위 코드에서  FruitBox<T> T와 메서드에 선언된 타입 T는 문자만 같을뿐 서로 다른 것이다.       
 
makeJuice()를 지네릭 메서드로 바꾸면 다음과 같다.
```java
	static Juice makeJuice(FruitBox<? extends Fruit> box) 
```
```java
	static <T extends Fruit> Juice makeJuice(FruitBox<T> box) 
```
이제 이메서드를 호출할때는 타입변수에 타입을 대입해야한다.

```java
	FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
	FruitBox<Apple> appleBox = new FruitBox<Apple>();
	 ...
	 System.out.println(Juicer.<Fruit>makeJuice(fruitBox));
	 System.out.println(Juicer.<Apple>makeJuice(appleBox));
```
단 클래스이름인 Juicer를 생략할수 없다.

예시로 타입이 복잡할 경우 간략화 할수있다.
```java
public static void priontAll(ArrayList<? extends Product> list1,ArrayList<? extends Product> list2){}
```
와 같은 경우에 
```java
public static <T extends Product> void priontAll(ArrayList<T> list1,ArrayList<T> list2){}
```
와 같이 간략화가 가능하다.     


### 7. 지네릭 타입의 형변환
지네릭 타입에서 다른 지네릭 타입으로 형변환은 불가능하다.      
다만 <? extends Object> 를 사용하면 가능하다.      
Box<? extends Object> wBox = new Box<String>
과 같이 가능하다.

전에사용한코드인 makeJuice메서드에서 다형성이 적용된이유와 같다.
```java
static Juice makeJuice(FruitBox<? extends Fruit> box){}
	FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
	FruitBox<Apple> appleBox = new FruitBox<Apple>();
```
위 코드가 아래의 코드와 같기 때문이다.
```java
static Juice makeJuice(FruitBox<? extends Fruit> box){}
	FruitBox<? extends Fruit> fruitBox = new FruitBox<Fruit>();
	FruitBox<? extends Fruit> appleBox = new FruitBox<Apple>();
```
하지만 반대의 경우 확인되지 않은 형변환이라는 경고가 발생한다.     
'<? extends Fruit>'에 대입될수 있는 타입이 여러개이며       
'FruitBox<Apple>'를 제외한 다른타입은 'FruitBox<Apple>'로 형변환 될수 없기 때문이다.      

### 8. 지네릭 타입의 제거
캄파일러는 지네릭 타입을 이용해서 소스파일을 체크하고, 필요한 곳에 형변환을 넣어준다.      
그후 지네릭타입을 제거한다.
	
1. 지네릭 타입의 경계를 제거한다.
	'<T extends Fruit>' 라면 T는 Fruit로 치환된다. <T>의 경우 Object로 치환 된다.
2. 지네릭 타입을 제한 후에 타입이 일치하지 않으면, 형변환을 추가한다.
```java
	T get(int i){
		return list.get(i);
	}
```
와 같은 경우는 List의 get()은 Object타입 반환하므로 형변환이 필요하다.
```java
	Fruit get(int i){
		return (Fruit)list.get(i);
	}
```

	와일드 카드가 포함된 경우에는 적절한 타입으로의 형변환이 추가된다.


## 2. 열거형
### 1. 열거형
서로 관련된 상수를 편리하게 선언하기 위한것     
ex)
```java
class Card{
	static final int CLONER = 0;
	static final int HEART = 1;
	static final int DIAMOND = 2;
	static final int SPADE = 3;

	static final int TWO = 0;
	static final int THREE = 1;
	static final int FOUR = 2;

	final int kind;
	final int num;
}
```
```java
class Card{
	enum Kind {CLONER,HEART,DIAMOND,SPADE } //열거형 Kind정의
	enum Value {TWO,THREE,FOUR} // 열거형 Value정의

	final Kind kind;
	final Value num;
}
```
자바의 열거형은 타입에 안전한 열거형 이라서 실제 값이 같아도 타입이 다르면 컴파일 에러가 난다.
```javai
if(Card.Kind.CLOVER == Card.Value.TWO) // 컴파일 에러
```
위와같이 값은 0으로 같지만 타입이 달라 컴파일 에러가 난다.        

중요한것은 *상수의 값이 바뀌면* 해당상수를 참조하는 모든 소스를 다시 컴파일 해야한다.        
하지만 열거형 상수를 사용하면 기존의 소스를 다시 컴파일 하지 않아도 된다.       

## 2. 열거형 정의와 사용
정의하는 방법
	
	enum 열거형 이름 {상수명 1, 상수명2,...}

사용방법

	열거형이름.상수명
ex)
```java
	enum Direction {EAST, SOUTH,WEST,NORTH}

class Unit{
	int x,y;
 	Direction dir;
	
	void init(){
		dir = Direction.EAST;
	}
}
```

열거형 상수간의 비교에는 "=="이 사용가능하다.       
그러나 '<','>'와같은 비교연산자는 사용할수 없고 compareTo()는 사용가능하다.      
compareTo()는 비교대상이 같으면 0, 왼쪽이크면 양수, 오른쪽이 크면 음수를 반환한다.

**모든 열거형의 조상 - java.lang.Enum**

Direction에 정의된 모든 함수를 출력하는법
```java
Direction[] dArr = Direction.values();

for(Direction d : dArr)
	System.out.printf("%s = %d%n",d.name(),d.ordinal());
```
values()는 모든 상수를 배열에 담아 반환 한다.           
ordinal()은 java.lang.Enum에서 정의된것으로 열거형 상수가 정의된 순서(0부터)를 정수로 반환한다.       

Enum클래스의 메서드
|메서드|설명|
|---|---|
|Class<E> getDeclaringClass()|열거형의 Class객체를 반환한다.|
|String name()|열거형 상수의 이름을 반환한다.|
|int ordinal()|열거형 상수가 정의된 순서를 반환|
|T valueOf(Class<T> enumType, String name)|지정된 열거형에서 name과 일치하는 열거형 상수를 반환한다.|

valueOf()는 컴파일러가 자동적으로 추가해주는 메서드로 values()와 같다.        
valueOf()는 열거형 상수의 이름으로 문자열 상수에 대한 참조를 얻을 수 있게 해준다.


### 3. 열거형에 멤버 추가하기
ordinal()이 정의된 순서를 반환하지만 이값은 상수값으로 사용하지 않는것이좋다.       
상수의 값이 불연속적일경우 상수옆에 괄호()와 함께 적어주면된다.
```java
	enum Ditrection {EAST(1), SOUTH(5),WEST(-1),NORTH(10)}
```
그리고 지정된 값을 저장할 수 있는 인스턴스 변수와 생성자를 새로 추가해야 한다.  

```java
enum Ditrection {
	EAST(1), SOUTH(5),WEST(-1),NORTH(10);
	
	private final int value ; //정수를 저장할 필드(인스턴스 변수)추가
	Direction(int value){this.value=value;} // 생성자 추가
	
	public int getValue(){return value;}
}
```
하지만 생성자를 만들었다고 외부에서 생성자를 호출하여 열거형 객체를 만들수는 없다.       

**열거형에 추상메서드 추가하기**
예제
```java
enum Transportation{
	BUS(100) {int fare(int distance){return distance*BASIC_FARE;}},
	TRAIN(150) {int fare(int distance){return distance*BASIC_FARE;}},
	SHIP(100) {int fare(int distance){return distance*BASIC_FARE;}},
	AIRPLANE(300) {int fare(int distance){return distance*BASIC_FARE;}};
	
	protected final int BASIC_FARE;
	
	Transportation(int basicFare){
		BASIC_FARE = basicFare;
	}
	public int getBasicFare() {
		return BASIC_FARE;
	}
	
	abstract int fare(int distance);//거리에 따른 요금 계산 추상메서드
}
```
열거형에 int fare(int distance)를 선언하면 각 열거형 상수가 이메서드를 반드시 구현해야한다.        
전부 똑같이 구현하지않고 각 상수마다 다르게 구현하는것또한 가능하다.       

## 3. 애너테이션

### 1. 애너테이션(annotation)
프로그램 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨것      
정보제공용 주석이라고 생각하면 간단하다.       
내부적으로 처리하는 방법은 현쳅터에서 다루지 않음.
           
### 2.에너테이션의 종류
|에너테이션|설명|
|---|---|
|@Override|컴파일러에게 오버라이딩하는 메서드라는 것을 알린다.|
|@Deprecated|앞으로 사용하지 않을 것을 권장하는 대상에 붙인다.|
|@SuppressWarnings|컴파일러의 특정 경고메시지가 나타나지 않게 해준다.|
|@SafeVarargs|지네릭스 타입의 가변인자에 사용한다.|
|@FunctionalInterfacce|함수형 인터페이스라는 것을 알린다.|
|@Native|native메서드에서 참조되는 상수 앞에 붙인다.|
|@Target*|애너테이션이 적용가능한 대상을 지정하는데 사용한다|
|@Documented*|야노태아숀 정보가 javadoc으로 작성된 문서에 포함되게 한다. |
|@Inherited*|애너테이션이 자손 클래스에 상속되도록 한다.|
|@Retention*|애너테이션이 유지되는 범위를 지정하는대 사용한다.|
|@Repeatable*|애너테이션을 반복해서 적용할 수 있게 한다.|

*는 메타 애너테이션


### 3. 애너테이션 타입정하기
애너테이션의 요소는 반환값이 있고 매개변수는 없는 추상 메서드 의 형태를 가진다.     
싱속을 통해 구현하지 않아도 되지만 애너테이션을 적용할때 요소들의 값을 빠짐없이 지정해 주어야한다.   
