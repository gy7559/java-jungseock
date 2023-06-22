# 입출력

## 1. 자바에서 입출력

### 1. 입출력이란
간단하게 입력과 출력의 줄입말로 컴퓨터내부 또는 외부의 장치와        
프로그램간의 데이터 주고 받기 이다.


### 2. 스트림

  스트립이란 데이터를 운반하는대 사용되는 통로이다.     
  
입출력을 동시에 하기위해서는 두개의 스트림(입력과 출력) 이 필요하다.       

### 3. 바이트 기반스트림

스트림은 바이트단위로 데이터를 전송한다.        

입출력 스트림의 종류는 다음과 같다.
|이름|종류|
|---|---|
|File|파일|
|ByteArray|메모리(byte배열)|
|Piped|프로세스(프로세스간의 통신)|
|Audio|오디오장치|
각각의 종류의 InputStream 과 OutputStream이 있다.     


### 4. 보조스트림
데이터를 주고 받는 스트림이 아닌 스트림의 기능을 항샹시키거나       
새로운 기능을 추가하는 스트림     
Filter와 Bufferd,Data 의InputStream 과 OutputStream이 있고 그외의         
LineNumberInputStream처럼 읽어온 라인번호를 카운트 하는 스트림도 있다.      

### 5. 문자기반 스트림
문자데이터를 입출력할때는 바이트기반 대신 문자기반 스트림을 사용한다.

    InputStream > Reader
    OutputStream > Writer



## 2. 표준입출력과 File
### 1. 표준입출력
콘솔을 통한 데이터 입력과 출력을 의미한다.       
자바에서는 3가지 를 기본 제공해준다.
|표준입출력|용도|
|---|---|
|System.in|콘솔로부터 데이터를 입력받는데 사용|
|System.out|콘솔로 데이터를 출력하는데 사용|
|System.err|콘솔로 데이터를 출력하는데 사용|

위 3가지가 기본제공 되기때문에 출력시 스트림 생성없이 사용할수 있었다.    

in,out,err는 System클래스에 선언된 클래스 변수이며 버퍼를 이용하는 Bufferrd스트림이다.        

### 2. 표준입출력 대상 변경
setIn(),setOut(),setErr()를 사용하면       
입출력을 콘솔이와에 다른 대상으로 변경하는것이 가능하다.


### 3. RandomAccessFile
RandomAccessFile은 DataInput인터페이스와 DataOutput인터페이스를 
구현을 하여 입출력이 모두 가능하다.      


### 4. File
기본적이고 가장 많이 사용되는 입출력대상이다.     
File클래스를 통하여 생성자와 메서드를 사용가능하다.     



## 3. 직렬화
### 1. 직렬화
직렬화란 객체를 데이터 스트림으로 만드는것 이다.     

### 2. 직렬화에 사용하는 스트림

ObjectInputStream과 ObjectOutputStream이 있다.       
두 스트림은 InputStream과 OutputStream을 직접 상속 받지만 기반스트림을 필요로하는 보조 스트림이다.    
직렬화에는  ObjectInputStream을 역질렬화에는 ObjectOutputStream을 사용한다.

### 3. 직렬화 가능한 클래스 만들기
방법은 직렬화 하고자 하는 클래스가 java.io.Serializable인터페이스를     
구현하도록 하면 된다.
