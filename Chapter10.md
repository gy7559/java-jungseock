# 형식화
## 1. 형식화 클래스
알아두면 편리하게 사용할수 있는 기능들을 가지고 있다.

### 1. DecimalFormat

숫자 데이터를 정수, 부동소수점, 금액 등의 **당양한 형식**으로 표현 가능      
```java
import java.text.*;


double n = 123456.78;

String p = "0.0"

DecimalFormat df = new DecimalFormat(p);

```
위와 같이 사용할수있으며 
#,0,E와 +,-,%등으로 패턴을 만들수있다.


### 2. SimpleDateFormat
날짜 데이터를 편하게 사용가능하게 만들어준다.     

기호와 의미는 Java API문서의 SimpleDateFormat을 찾아보면 된다.
 
 ```java
 date today= new Date();
 SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
 
 String result = df.format(today);
 
 ```
 
 출력하고자 하는 Date인스턴스를 가지고  format(Date d)를 호출하면 지정한 출력형식에 맞게 변횐된 문자열을 얻는다.
 
 
       
 ### 3. ChoiceFormat
 특정 범위의 속하는 값을 문자열로 변환해 준다.        
 ```java
 
 public static void main(String[] args){
  String pattern = "60#D|70#C|80#B|90#A";
  int[] scores = {91,90,80,88,70,52,60};
  
  ChoiceFormat form = new ChoiceFormat(pattern);
  
  for(int i = 0;i<scores.length;i++){
      System.out.println(scores[i]+":"+formformat(scores[i]));
  }
 }
 ```
 ChoiceFormat을 사용하여 각 점수별 등급을 지정하였다.     
 #은 값을 포함 하지만 <는 경계값을 포함 하지 않는다.
 
 ### 4. MessageFormat
 
 데이터를 정해진 양식에 맞게 출력할 수 있도록 도와준다.
 ```java
public static void main(String[] args){
  String msg = "Name: {0} \nTel:{1} \nAge:{2} \ nBirthday:{3}";
  
  Object[] argments = {
    "이자바","02-123-1234","27","07-09"
  };
  
  String result =
      MessageFormat.format(msg, arguments);
  System.out.println(result);
}
 ```
 데이터의 양식을 정해두면서 객체배열로 지정 하여 사용한다.
 
 
## 2. java.time패키지
### 1. java/tome 패키지의 핵심 클래스

  시간 : LocalTime클래스
  날짜 : LocalDate클래스
  시간+날짜 : LocalDateTime
  LocalDateTime + 시간대 : ZonedDateTime
  날짜 - 날짜 : Period
  시간 - 시간 : Duration
  


 
