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
  
  
    Box<T>
    T
    Box     
      
    
