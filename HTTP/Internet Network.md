# 인터넷 통신
서버와 클라이언트 사이에 인터넷이 껴서 통신을 하게 해줌

인터넷 망은 매우 복잡함

# IP(Internet Protocol)

# IP의 역할
* 지정한 IP주소(IP Address)에 데이터 전달
* 패킷(Packet)이라는 통신 단위로 데이터 전달

# IP 프로토콜의 한계
* 비연결성: 패킬을 받을 대상이 없거나 서비스 불능 상태여도 패킬 전송
* 비신뢰성: 중간에 패킷이 사라지거나 패킷이 순서대로 안갈 때
* 프로그램 구분: 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

# TCP, UDP

![image](https://user-images.githubusercontent.com/74352543/220024740-88f9da41-8b94-45c9-9c7b-1b262461660a.png)

![image](https://user-images.githubusercontent.com/74352543/220024909-e2c24e24-4824-4026-83e8-1dee634cbe7b.png)

# 채팅 프로그램으로 친구에게 채팅을 보낼 때 과정
1. 프로그램이 Hello, world 메시지 생성
2. SOCKET 라이브러리를 통해 전달
3. TCP 정보생성, 메시지 데이터 포함
4. IP 패킬 생성, TCP 데이터 포함
5. 이더넷 프레임을 씌워서 인터넷을 통해 서버로 감

# IP 패킷 정보

![image](https://user-images.githubusercontent.com/74352543/220025770-7ca1aa4d-61ab-48b8-873e-213aed0852a9.png)

# TCP/IP 패킷 정보

![image](https://user-images.githubusercontent.com/74352543/220025871-2093440e-aa43-4441-8ad2-03178d615cd3.png)

# TCP 특징
* 전송 제어 프로토콜
* 연결 지향 - TCP 3 way handshake (가상 연결)
* ![image](https://user-images.githubusercontent.com/74352543/220026915-2adf5195-ec17-41f8-973b-c596f5dca4d5.png)
* 데이터 전달 보증
* 순서 보장
* 신뢰할 수 있는 프로토콜
* 현재는 대부분 TCP 사용
