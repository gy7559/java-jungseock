# 1. 네트워크

## 1. Socket
소켓은 커널계층의 요소를 유저계층에서 접근할수 있도록 추상화 한 것      

    ex) TCP, IP소켓은 유저계층인 프로세스에서 접근할수 있도록 파일로 추상화 한것이다.    


## 2. Mac, Port번호,IP주소(식별자)
**SW**         
4계층 전송계층        Port번호  ->  Process식별자, 서비스식별자,인터페이스 번호(각 상황과 업무에 따라 다르게 생각한다.)      
3계층 네트워크계층    IP주소  -> Host(인터넷에 연결된 컴퓨터)       

**HW**           
L2(2계층) MAC주소   -> NIC(네트워크 인터페이스 카드)(LAN카드)

HTTP의 포트번호는 TCP[8080]     
IP주소는  NIC하나에 여려게가 연결될수있다.      
MAC주소는 변경 가능하다.     


## 3. Host,Switch,Network의 관계

Host : Network에 연결된 컴퓨터       

    Host :  1. Net자채를 이루는 컴퓨터(Switch) ex)라우터      
            2. Net을 이용하는 컴퓨터(End point = 단말) 

Net = 대표적인 net : 인터넷(라우터+DNS)       


## 4. IP주소
IP = 인터넷 프로토콜의 약자        

IPV4, IPv6의 차이는 주소의 길이로 v4는 32비트 이며  v6는 128비트 이다.

IPv4주소는 8비트씩 끊어서 표시한다.           
Net ID와 Host ID로 나뉜다       
Net ID = 24bit      
Host ID = 8bit      

서브넷마스크와 IP를 비트 AND연산을 하면 Net ID가 나온다.        


## 5.Port번호

Port번호는 16비트 1~65534번호까지 있음              
TCP소켓을 생성할때 소켓에 들어가는 정보가 Port번호        

Port번호 : Process식별자       
 

## 6. Switch
스위치가 하는일은 Switching(경로선택)이다.       
라우터는 각 스위칭이 일어나는 교차점이다.       
패킷단위의 데이터가 각 라우터를 라우팅테이블을 통하여 스위칭을 하여 목적지까지 간다.      


## 7. 네트워크 데이터 단위

Packet : IP에서 다루는 단위
Socket : Process에서 TCP IP에 접근할수있도록 추상화 한것 {File}         

Process가 File에  Stream(시작은 있지만 언재 끝날지 모른다.)데이터를 Segment화 하여 작성을한다.        
Segment화 : 일정길이만큼 자른다.
MSS : 최대 세그멘트 사이즈 = Packet의 최대크기를 따른다.
MTU : 최대전송 크기 보통 1500byte (Packet의 최대크기)

## 8. 네트워크 인터페이스 선택 원리와 기준
어떤Ip주소는 어떤 인터페이스와 연결된다.       
인터페이스 선택 : PC에 한정하면 메트리값(비용)에 따라 결정된다.       

## 9. 웹서비스 구조

창시자 : 티모시 버너스 리        
Text와 Link의 확장을 통하여 HTML이라는 문서형식을 만들고,         
인터넷을 결합하여 전달할수있는것이 HTTP프로토콜        
모양이 거미줄처럼 연결되있다하여 WEB이 라고 명명         

WEB: 논리적으로 문서가 연결된것        

## 10. 웹 서비스 3대요소 
웹 : 원격지 문서 뷰어 {HTML + HTTP}

HTML : 내용을 담고있는 문서
CSS : 스타일 시트 UI개선요소
JavaScript : 동적요소 처리담당(연산)

웹브라우저의 로딩시 받는 정보 : HTML + CSS + 사진 + JS 순서        

## 11. LAN과 WAN의 차이
널널한 개발자의 개인적인 의견이다.

HW적인 설명은 LAN
SW적인 설명은 WAN으로 접근한다.    

## 12. 패킷의 생성 원리   
Socket의 데이터 단위 : Stream      

프로세스가 소켓에 입출력을 시도하면   
Stream을 Segmentation(분해)을 하여 Segment를 생성       
Segment를 캡슐화 하여 Packet 을 생성한다.       

Packet의 길이= 1500byte(MTU)
Packet은 헤더와 Payload로 나뉜다.
Packet의 헤더는 IP와 TCP로 이루어져 각각 20byte를 가진다.     
Payload 를 확인화는것 = DPI(Deep Packet inspection)      

## 13. L2스위치
MAC주소(48bit) = 물리적 주소    
L2스위칭을 한다 = MAC주소로 스위칭을 한다.      

L2 Access = Endpoint와 직접만나는 스위치      
L2 Distribution = 스위치를 위한 스위치      

UpLink : 트래픽이 상향으로 나가는선     

**헷갈리지 말것**       
Link-up : 연결됨       
Link-down : 연결끊김        
