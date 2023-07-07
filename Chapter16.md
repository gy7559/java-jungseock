# 네트워킹

## 1. 네트워킹

### 1. 클라이언트/서버

	서버 = 서비스를 제공하는 컴퓨터
	클라이언트 = 서비스를 이용하는 컴퓨터

각 클라이언트가 서버의 역할을 하는 것 = P2P


서버기반 모델 
장점   
1. 안정적인 서비스 제공가능     
2. 공유 데이터의 관리 및 보안이 용이하다        

단점      
1. 서버구축과 관리비용이 든다.      
       
P2P모델        
장점

1. 서버구축 및 운용비용 절감 가능
2. 자원 활용을 극대화 할수있음

단점 
1. 자원의 관리가 힘듬
2. 보안이 취약함


### 2. InetAddress
ip주소를 다루기 위한 클래스       
|메서드|내용|
|---|---|
|byte[] getAddress()|ip주소를 btye배열로 반환한다.|
|static InetAddress[], getAllByName(String host)|도메인명(host)에 지정된 모든 호스트의 ip주소를 배열에 담아 반환한다.|
|static InetAddress getByAddress(byte[] addr)|byte배열을 통해 IP주소를 얻는다.|
|static Inet Address, getByName(String host)|도메인명을 통해 IP주소를 얻는다.|
|String getCanonicalHostName|FQDN(filly qualified domain name)을 반환한다|
|String getHostAddress()|호스트의 IP주소를 반환한다.|
|String getHostName|호스트의 이름을 반환한다.|
|static InetAddress getLocalHost()|지역호스트의 IP주소를 반환한다.|
|boolean isMulticastAddress()|IP주소가 멀티캐스트 주소인지 알려준다.|
|boolean isLoopbackAddress()|Ip주소가 loopback주소(127.0.0.1)인지 알려준다.|


### 3. URL
인터넷에 존재하는 여러 서버들이 제공하는 자원에 접근할수 있는 주소를 포현하기 위한것.     

'프로토콜://호스트명:포트번호/경로명/파일명?쿼리스트링#참조'의 형태 이다.     
URL을 다루기위한 URL클래스가 있으며 메소드로는 다음과 같다.

|메서드|내용|
|---|---|
|URL(String spec)|지정된 문자열 정보의 URL객체 생성|
|URL(String protocol,String host, String file)|지정된 값으로 구성된 URL객체생성|
|URL(String protocol,String host,int port ,String file)|지정된 값으로 구성된 URL객체생|

위와같은 메서드로 객체를 생성하여 getHost, getFile등과 같은 메서드로 값을 반환할수있다.    


### 4. URLConnection
어플리케이션과 URL간의 통신연결을 나타내는 클래스의 최상위 클래스로 추상클래스이다.
URLConnection을 상속받아 구현한 클래스로는 HttpURLConnection과 JarURLConnection이 있다.     
URLConnection을 사용하여 원하는 자원에 접근하여 읽고 쓰기가 가능하다.      
getContent()를 통하여 content객체를 반환할수있으며 getURL()을 통하여 URL의 반환등 여러 메서드가 존재한다.       

## 2. 소켓 프로그래밍
소켓을 이용한 통신프로그램       
### 1. TCP와UDP
전송계층에 해달하는 프로토콜로 TCP/IP프로토콜에 포함되어 있다.      

TCP
    연결방식 : 연결후 통신(전화기),1:1통신방식
    특징 : 데이터의 경계를 구분하지 않음, 수신여부 확인과 전송순서가 보장되어 신뢰성있는 전송이 가능(UDP보다 속도가 느림)
    관련 클래스 : Socket, ServerSoket

UDP
    연결방식 : 비연결기반, 연결없이 통신, 1:1 1:n n:n 통신방식
    특징 : 데이터의 경계를 구분함, 수신여부 확인안함과 전송순서가 바뀔수 있음(TCP보다 속도가 빠름),패킷관리 필요
    관련 클래스 : DatagramSocket,DatagramPacket, MulticastSocket


### 3 . TCP소켓 프로그래밍
1. 서버 프로그램에서는 서버소켓을 사용해서 서버 컴퓨터의 특정 포트에ㅐㅔ서 클라이언트의 연결요청을 처리할 준비를 한다.
2. 클라이언트 프로그램은 접속할 서버의 IP주소와 포트정보를 가지고 소켓을 생성해서 서버에 연결을 요청한다.
3. 서버소켓은 클라이언트의 연결요청을 받으면 서버에 새로운 소켓을 생성해서 클라이언트의 소켓과 연결되도록 한다.
4. 이제 클라이언트의 소켓과 새로 생성된 서버의 소켓은 서버소켓과 관계없이 일대일 통신을 한다.


Sokect과 ServerSocket클래스의 특징

  Socket : 프로세스간의 통신을 담당함. InputStream과 OutputStream을 가지고 있으며 이것을 가지고 프로세스간의 통신이 이루어진다.
  ServerSocket : 포트와 연결되어 외부의 연결요청을 기다림, 요청이 들어오면 Socket을 생성해서 통신이 이루어지도록함


### 4. UDP소켓 프로그래밍

DatagramSocket을 소켓으로 사용하며  데이터를DatagramPacket에 담아 전송한다.     
DatagramPacket에는 수신할 호스트의 정보가 저장되어있다.(수신할 상대편의 주소를 적어둔 느낌이다.)     
DatagramPacket을 전송하면 DatagramPacket에 지정된 DatagramSocket으로 도착한다.
