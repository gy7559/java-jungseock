# 1. java.lang패키지
---
## 1. java.lang패키지

### 1. object클래스
멤버변수는 없고 오직 11개의 메서드만 존재

#### equals(Object obj)
매개변수로 객체의 참조변수를 받아서 비교하여 글결과를 boolean값으로 알려준다.   

#### hasjCode()
해싱 기법에 사용되는 해시함수응 구현한것.
해시함수는 찾고자 하는 값을 입력하면,그 값이 저장된 위치를알려주는 해시코드를 반환 한다.

#### toString()
인스턴스에 대한 정보를 문자열로 제공     
오버라이딩 하지 않는다면 클래스이름에 16진수의 해시코드를 얻게된다.     

#### clone()
자신을 복제하여 새로운 인스턴스를 생성하는 일을 한다.


### 2. String클래스

#### 변경 불가능 클래스
문자형 배열 참조변수를 인스턴스 변수로 정의해놓고 있기에 변경불가능하다.     

#### 문자열 비교
문자열 리터럴 지정방법과 String클래스 생성자 사용 방법두가지가 있는대   
리터럴 지정 방법의 경우 ==을 사용하여 비교를 할수있지만       
생성자 사용시 == 사용할경우 실패한다.

**equals()** 를 사용하면 문자열의 내용을 비교하기때문에 두경우 모두 제대로된 비교가 된다.    

#### 생성자와 메서드

|메서드|설명|
|---|---|
|boolean startsWith(String x)|주어진 문자열로 시작하는지 검사한다.|
|String substring(int begin) or (int begin,int end)|주어진 시작위치에서 끝위치 범위에 포함된 문자열을 얻는다.(끝위치 문자는 미포함)|
|String trim()|문자열의 왼쪽끝과 오른쪽 끝의 공백을 없앤 결과를 반환|
|char charAt(int i)|지정된 위치에 있는 문자를 알려줌|
|int indexOf(int ch)|주어진 문자가 문자열에 존재하는지 확인후 위치 반환|
|int indexOf(int ch, int pos)|주어진 문자가 문자열에 존재하는지 지정위치(pos)부터 확인후 반환|
|int indexOf(String str)|주어진 문자열이 존재하는지 확인후 위치 반환 없으면 -1반환|
|toCharArray()|이 인스턴스의 문자를 유니코드 문자 배열에 복사|
|static valueOf()|지정된 값을 문자열로 반환하여 변환|


### 3. StringBuffer클래스와 StringBuilder클래스    
인스턴스를 생성할때 크기지정이 가능하다.   

#### StringBuffer의 생성자 
  StringBuffer(int length)를 사용해서 여유있는 크기로 지저어하는것이 좋다.    
  크기지정을 하지 않으면 16개의 문자를 저장할수있는 크기로 생성한다.    
  

#### StringBuffer의 비교
StringBuffer의 인스턴스에 toString()을 호출해서 String인스턴스를 얻은후     
equals메서드를 사용해서 비교해야한다.

#### StringBuffer의 생성자와 메서드
|메서드|설명|
|---|---|
|reverse|StringBuffer인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열한다.|
|toStirng|StringBuffer인스턴스의 문자열을 String으로 반환|



### 4. Math클래스
기본적인 수학계산에 유용한 메서드로 구성되어있다.    
**반올림**     
round() = 반환값 : int      
rint() = 반환값 : double
**올림**
ceil() = 반환값 : float
**버림**
floor = 반환값 : float

#### 예외를 발생시키는 메서드
메서드이름에 'Exact'가 포함된 메서드들이 추가되었다.      
오버플로우가 발생하면 예뢰를 발생시킨다.    
      
      
#### Math클래스의 메서드 
|메서드|설명|
|---|---|
|max|주어진 두 값의 큰쪽을 반환|
|min|주어진 두 값의 작은쪽을 반환|
|ceil|주어진값을 올림하여 반환|
|round|소수점 첫째자리에서 반올림한 정수값 을 반환|
|random|0.0~1.0범위의 임의의 double값을 반환 1.0은 범위에 미포함|
|pow(int a,double b)|a의 b제곱을 구함ex) a= 2 b =5 반환값 = 32|
|sqrt|주어진 수의 제곱근을 구함|



### 5. 래퍼 클래스
기본형 변수를 객체로 다뤄야할때 사용    
|기본형|래퍼클래스|
|---|---|
|boolean|Boolean|
|char|Character|
|byte|Byte|
|short|Boolean|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|


#### Numbe클래스
 래퍼클래스의 조상 클래스
 



