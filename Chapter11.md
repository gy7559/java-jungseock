# 컬랙션 프레임웍
## 1. 컬렉션 프레임웍
**데이터 군 을 저장하는 클래스들을 표준화한 설계**       
컬렉션,다수의 데이터를 다루는대 팔요한 많은 클래스들을 제공해줌     
객체지향적 설계를 통해 표준화 되어 익히기 쉽고 재사용성높은 코드를 작성할수있다.    


### 1. 핵심 인터페이스
컬렉션 데이터 그룹은 크게 3가지로 나뉨    
1. List
2. Set
3. Map
여기서 List와 Set의 공통부분을 가져와서 Collection을 추가로 정의 하여      
컬렉션 프레임웍 의 인터페이스로 정의하였다.

|인터페이스|특징|
|---|---|
|List|순서가 있는 데이터의 집합. 데이터의 중복을 허용함|
|Set|순서를 유지하지 않는 데이터의 집합. 중복을 허용안함|
|Map|키 와 값을 쌍으로 이루어진 데이터의 집합. 순서유지X 키=중복X 값=중복O|


**Collection인터페이스**
|메서드|설명|
|---|---|
|boolean add(object o)|지정된 객체(o)를 Collection에 초가한다.|
|void clear()|Collection의 모든 객체를 삭제한다.|
|boolean remove(Object o)|지정 객체 삭제|

등 여러 메서드가 존재한다.

**List 인터페이스**
중복을허용하고 저장순서를 유지하는 컬렉션을 구현하는대 사용된다.
|메서드|설명|
|---|---|
|Void add(int index, Object element),boolean addAll(int index, Collection c) |지정된 위치(index)에 객체 또는 컬렉션에 포함된 객체들을 추가한다.|
|int indexOf(Object o)|지정된 객체의 위치 반환|
|Object remove(int index)|지정 위치에 있는 객체를 삭제하고 삭제된 객체를 반환|

등 여러 메서드가 존재

**Set인터페이스**
중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현 하는대 사용된다.     
구현한 클래스로는 HashSte,TreeSet등이 있다.     


**Map인터페이스**
키와 값을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는대 사용된다.        
Hashtable, HashMap,LinkedHashMap,SortedMap, TreeMap등이 있다.         


### 2.ArrayList

컬렉션 프레임웍에서 가장 많이 사용되는 컬렉션 클래스이다.      
List인터페이스를 구현  List의 특징을 가진다.

   장점 : 구조가 간단하며 사용하기 쉽다.
          데이터를 읽어오는대 걸리는 시간이 가장 빠르다.
   단점 : 크기를 변경할수 없다.
           비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.
           
위와 같은 단점으로 크기를 변경하여 주기 위해서는 더큰 배열을 만든후 복사를 하여야 하며,     
중간의 데이터를 추가 하기 위해서는 다른 데이터를 복사해서 이동해서 빈자리를 만들어야 한다.    


|메서드|설명|
|---|---|
|boolean add(Integer e)|ArrayList 마지막에 객체(e)를 추가 성공하면 true를 반환|
|void add(int index,Integer element)|지정위치(index)에 객체(e)를 추가|
|boolean contains(Object o)|지정된 객체(o)가 ArrayList에 포함되어있는지 확인|
|boolean addAll(Collection c)|주어진 컬랙션의 모든 객체를 저장한다.|
|boolean addAll(int index,Collection c)|지정된 위치부터 주어진 컬렉션의 모든 객체를 저장한다.|
|int indexOf(Object o)|지정된 객체가 저장된 위치를 찾아 반환한다.|



### 3. LinkedList
배열의 단점을 보완하기위해서 LinkedList라는 자료구조가 고안 되었다.      

데이터를 서로 연결한 형태로 되어있다.
각 요소들이 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 이루어져 있다.     
중간에 새로운 요소가 들어올경우 새로운 값의 주소를 이어질 전 요소에 입력하고      
다음 요소의 주소를 넣을 요소에 넣어주면 되어 속도가 바르다.

하지만 단방향이기때문에 다음요소에 대한 접근은 쉽지만 이전 요소에 대한 접근은 힘들다.      
그단점을 보완 하기 위해 더블 링크드 리스트를 만들었다.     
간단하게 이전 요소의 주소도 가지고있는 링크드 리스트이다.

 
 |컬랙션|읽기|추가/삭제|비고|
 |---|---|---|---|
 |ArrayList|빠르다|느리다|순차적인 추가삭제는 더 빠름.|
 |LinkedList|느리다|빠르다|데이터가 많을수록 접근성이 떨어짐|
 
 
 
 ### 4. Stack과 Queue
 
        Stack : 마지막에 저장한 데이터가 먼저나오는 구조
        Queue : 처음저장한 데이터가 먼저 나오는 구조
               
**Stack의 메서드**
|메서드|설명|
|---|---|
|pop()|맨 위에 저장된 객체를 꺼낸다|
|peek()|맴위에 저장된 객체를 반환 꺼내지는 않음|
|push()|Stack에 객체 저장|
|empty()|Stack이 비어있는지 확인|


**Queue의 메서드**
|메서드|설명|
|---|---|
|Object poll()|객체를 꺼내서 반환 비어있으면 null을 반환|
|boolean offer()|객체를 저장 성공하면 ture 실패하면 false를 반환|
|boolean add()|지정된 객체를 Queue에 추가 |
|boolean isEmpty()|Queue가 비어있는지 확인|
|peek()|삭제없이 요소를 읽어옴 비었으면 null|

 
데이터를 추가/삭제가 쉬운 LinkedList가 적합하다.      


**활용**

   스택 :  수식 계산,수식돨호검사,웹브라우저의 뒤로/앞으로
   큐 : 최근사용문서 인쇄작업 대기목록, 버퍼
   
**Queue의 변형**

1. PriorityQueue
         저장 순서에 상관없이 운선숭위가 높은것부터 꺼낸다.
2. Deque
         한쪽 끝으로만 추가 삭제가 가능하다.
         끝에저장,삭제(offerLast,pollLast)
         앞에 저장,앞에 삭제(offerFirst,pollFirst)
    
    
    
### 5. Iterator, ListIterator, Enumeration
컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스      
Enumeration = Iterator의 구버전,ListIterator = Iterator의 향상     


Iterator는  요소를 읽어오는 방법을 표준화 하였으며
메서드로는 
|메서드|설명|
|---|---|
|boolean hasNext()|읽어올 요소가 남아 있는지 확인한다. 있으면 true,없으면 false를 호출|
|Object next()|다음요소를 읽어온다.|
|void remove()|next로 읽어온 요소를 삭제한다.|

ex)Iterator의 hasNext를 사용하여 while문의 조건으로 활용

```java
import java.util.*;

public class IteratorEx1 {

	public static void main(String[] args) {
		ArrayList list = new ArrayList();
		
		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");
		
		ListIterator it = list.listIterator();
		
		while(it.hasNext()) {
			System.out.print(it.next());
		}
		System.out.println();
		while(it.hasPrevious()) {
			System.out.print(it.previous());
		}
	}

}

```

 Enumeration은 프레임웍이 만들어지기 이전에 사용하던것으로 호환을 위해 남겨둔것이라 Iterator를 사용하면된다.     

 ListIterator는 List인터페이스를 구현한 경우에 양방향으로 이동이 가능하게 만들어둔것이다.     
 
 ListIterator 의 메소드는  Iterator메소드에서 이전 요소에대한 접근도 추가 되었다.      
 
 
 ### 6. Arrays
 배열을 다루는데 유용한 메서드가 정의 되어 있다.
 
 **배열의 복사**      
 
      copyOf()     : 배열의 전채 복사
      copyOfRange()  : 배열의 특정 부분 복사    
      
**배열 채우기**

      fill()   : 모든 요소를 지정된 값으로 채운다.
      setAll() : 배열을 채우는데 사용할 함수형 인터페이스를 받는다.
 
**배열의 정렬과 검색**

      sort()   : 배열의 정렬
      binarySearch() : 배열에 저장된 요소 검색(단 배열이 정렬되어 있어야함)
 
**배열의 비교와 출력**

      equals()    : 두배열을 비교하여 값으면 true 다르면 false를 출력 
      toSting()   : 배열의 모든 요소를 문자열로 출력 가능
      둘다 다차원 배열에서는 deep을 붙여주어 사용 deepToString(), deepEquals()
      
**베열을 List로 변환**

      asList() 배열을 List로 변환 가능하지만 삭제및 추가가 불가능하다.
               내용의 변경은 가능하다.

### 7. Comparator와 Comparable
컬렉션을 정렬하는대 필요한 메서드를 정의 하고있는 인터페이스 이다.    

Comparable을 구성하고 있는 클래스들은 wrapper클래스와 String,Date,File과 같은 것들이다.      
기본적으로 오름차순 정렬이다.        

Comparator와 Comparable의 실제 소스
```java
public interface Comparator{
   int compare(Object o1,Object o2);
   boolean equals(Object obj);
}

public interface Comparable{
   public int compareTo(Object o);
}
```
예시로 Comparable를 사용하여 역순정렬 구현이있다.

```java
import java.util.*;
public class ComparatorEx {
	public static void main(String[] args) {
		String[] strArr = {"cat","Dog","lion","tiger"};
		
		Arrays.sort(strArr);
		System.out.println("strArr=" + Arrays.toString(strArr));
		
		Arrays.sort(strArr,String.CASE_INSENSITIVE_ORDER);//대소문자 구분안함
		System.out.println("strArr=" + Arrays.toString(strArr));
		
		Arrays.sort(strArr, new Descending());//역순정렬
		System.out.println("strArr=" + Arrays.toString(strArr));
	}
}
class Descending implements Comparator{
	public int compare(Object o1, Object o2) {
		if( o1 instanceof Comparable && o2 instanceof Comparable) {
			Comparable c1 = (Comparable)o1;
			Comparable c2 = (Comparable)o2;
			return c1.compareTo(c2) *-1;//-1을 곱해서 정렬방식을 역순으로
		}
	return -1;
	}
}
```


compare()와 compareTo()는 약간 다를뿐 두객체를 비교한다는 같은 기능을 목적으로 고안함     


### 8. HashSet
Set인터페이스를 구현한 가장 대표적인 컬렉션     
중복요소를 저장하지 않는다.      
저장 순서도 저장하지 않기때문에 필요하다면 LinkedHashSet을 사용해야 한다.


|메서드|설명|
|---|---|
|boolean addAll(Collection c)|주어진 컬렉션에 저장된 모든 객체를 추가한다.(합집합)|
|boolean removeAll(Collection c)|주어진 컬렉션에 저장된 모든 객체와 같은 것들을 모두 삭제한다.(차집합)|
|boolean retainAll(Collection c)|주어진 컬렉션에 저장된 객체와 동일한것만 남기고 삭제한다.(교집합)| 


위 세 메서드는 결과를 성공하면 ture 실패하면 false로 메서드후의 결과는 Set에 저장된다.

```java
HashSet<Integer> ss = new HashSet();
HashSet<Integer> ss2 = new HashSet();
		ss.add(1);
		ss.add(2);
		ss.add(3);
		ss.add(4);

		ss2.add(3);
		ss2.add(4);
		ss2.add(5);
		ss2.add(6);

ss.addAll(ss2);
```


위와 같은 경우에는 ss에 (1,2,3,4,5,6)으로 저장된다. 메서드의 결과는 true이다.
Map의 데이터를 순회하는 방법



### 9. TreeSet
이진 검색 트리 라는 자료구조의 형태로 데이터를저장하는 컬렉션 클래스이다.      
하나의 노드에서 계속 추가되어 나갈수있다.    
자식노드와 부모노드로 나뉘며 하나의 부모노드는 최대 2개의 자식 노드를 가질수 있다.     

### 10 HashMap과 Hashtable
Hashtable보다 새로운 버전인 HashMap의 사용을 권장        
HashMap은 Map을 구현한것이기 때문에     
키 와 값을 묶어서 하나의 쌍으로 데이터를 가진다.

      키는 값이 유일해야해서 중복이 되지 않지만
      값은 중복을 혀용한다.


**해싱과 해시함수**
      
      해싱은 해시함수를 이용해서 데이터를 해시테이블에 저장하고 검색하는 기법이다.

배열과 링크드리스트의 조합으로     
특정 키값을 배열에 넣어주고 각 배열의 요소(키값)에 따라 링크드 리스트가 있어     
검색을 할경우 키값을 먼저 찾고 그 키값과 연결되어 있는 링크드리스트에서 검색을 진행하기때문에      
검색속도가 빠르다.


**단점**     
링크드 리스트가 커질수록 검색에 걸리는 시간이 늘어난다.     
빠른 검색을 위해서는 배열의 각 요소마다 하나의 링크드 리스트를 넣는것이      
검색속도에는 더욱 빠르다.


### 11. TerrMap
이진검색트리의 형태로 Map의 형태인 키와 값의 쌍으로 이루어진 데이터를 저장한다.    

### 12. ProPerties
Hashtable을 상속받아 구현한 것으로 (String,Sring)의 형태로 저장하는 단순화된 컬렉션클래스     
애플리케이션의 환경설정과 관련된 속성(property)를 저장하는데 사용됨      
간단한 입출력은 ProPerties을 활용하면 쉽게 해결 가능    


### 13. Collections

**컬렉션의 동기화**
멀티 쓰레드 프로그래밍 에서는 하나의 객체를 여러 쓰레드가 동시에 접근할 수 있기 떄문에    
데이터릐 일관성을 유지하기 위해 객체 동기화가 필요하다.     

동기화 메서드로는 
```java
static Collection synchronizedCollection(Collection c)
```
와 같이
List, Set,Map,SortedSet,SortedMap에서 synchronized를 붙여 주면 된다.

**변경불가 컬렉션 만들기**
데이터를 보호하기위해 읽기전용으로 만들어야 될때 사용한다.
메서드는 동기화에서 synchronized대신 unmodifiable을 작성해주면 된다.
Collection, List, Set,Map,SortedSet,SortedMap, NavigableSet, NavigableMap이 있다.     

**싱글톤 컬렉션 만들기**
단 하나의 객체만을 저장하는 컬렉션을 만들때 사용하는 메서드       
```java
static List singletonList(Objecto) 
static Set  sington(Object o)
static Map  singletonMap(Object key, Object value)
```

**한 종류의 객체만 저장하는 컬렉션 만들기**

컬렉션에 지정된 종류의 객체만 저장하도록 제한 하고 싶을때 사용하는 메서드
```
static Collection    checkedCollection(Collection c,Class type)
static List          checkedList(List list,Class type)
static Set           checkedSet(Set s,Class type)
static Map           checkedMap(Map m,Class keytype,Class valuetype)
static Queue         checkedQueue(Queue queue,Class type)
static SortedSet     checkedSortedSet(SortedSet s, Class type)
static SortedMap     checkedSortedMap(SortedMap m,Class keytype,Class valuetype)
static NavigableSet  checkedNavigableSet(NavigableSet s,Class type)
static NavigableMap  checkedNavigableMap(NavigableMap m,Class keytype,Class valuetype)    
```
사용방법은 두 번째 매개변수에 저장할 객체의 클래스를 저장하면 된다.
```java
List list = new ArrayList();
List checkedList = checkedList(list, String.class);
checkedList.add("abc")
checkedList.add(new Integer(3));//에러
```



