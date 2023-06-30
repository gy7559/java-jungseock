# 1. 네트워크

## 1. Socket
소켓은 커널계층의 요소를 유저계층에서 접근할수 있도록 추상화 한 것      

    ex) TCP, IP소켓은 유저계층인 프로세스에서 접근할수 있도록 파일로 추상화 한것이다.    


## 2. Mac, Port번호,IP주소(식별자)
**SW**         
4계층 전송계층        Port번호  ->  Process식별자, 서비스식별자,인터페이스 번호(각 상황과 업무에 따라 다르게 생각한다.)      
3계층 네트워크계층    IP주소  -> Host(인터넷에 연결된 컴퓨터)       

**HW**           
MAC주소   -> NIC(네트워크 인터페이스 카드)(LAN카드)

HTTP의 포트번호는 TCP[8080]     
IP주소는  NIC하나에 여려게가 연결될수있다.      
MAC주소는 변경 가능하다.     


## 3. Host,Switch,Network의 관계

Host : Network에 연결된 컴퓨터       

    Host :  1. Net자채를 이루는 컴퓨터(Switch) ex)라우터      
            2. Net을 이용하는 컴퓨터(End point = 단말) 

Net = 대표적인 net : 인터넷(라우터+DNS)       
