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
![image](https://user-images.githubusercontent.com/74352543/220026915-2adf5195-ec17-41f8-973b-c596f5dca4d5.png)
* 데이터 전달 보증
* 순서 보장
* 신뢰할 수 있는 프로토콜
* 현재는 대부분 TCP 사용

# UDP 특징
* 사용자 데이터그램 프로토콜
* 하얀 도화지에 비유 (기능이 없음)
* 연결지향 X
* 데이터 전달 보증 X
* 순서 보장 X
* 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
* 정리
* * IP와 거의 같다 + PORT + 체크섬 정도만 추가
* * 애플리에키션에서 추가 작업 필요

기본으로 TCP 프로토콜을 사용하지만 최근에는 UDP 프로토콜이 뜨고 있음, TCP 핸드셰이크의 과정을 줄이기 위해

# PORT

![image](https://user-images.githubusercontent.com/74352543/220029162-e2cc0e66-f1ef-412c-b258-9598427f30fa.png)

다음과 같이 하나의 IP에서 여러가지 어플리케이션을 사용할 때 이 어플리케이션을 구분하기 위한 것이 PORT임

그래서 TCP에는 출발 PORT 정보와 목적지 PORT 정보가 있다.

비유를 하자면 IP는 아파트이고 PORT는 몇동, 몇호라고 비유할 수 있다.

![image](https://user-images.githubusercontent.com/74352543/220029973-2d1b953b-b2cc-424f-a43d-fc86e38b648b.png)

# DNS
IP는 기억하기 어렵고 변겨될 수 있음

# DNS(Domain Name System)
* 전화번호부
* 도메인 명을 IP 주소로 변환
* DNS 서버에 도메인을 등록함 (예를 들어 google.com)
* 클라이언트에서 DNS서버에 도메인 명으로 요청을 하면 구글에 해당하는 IP주소를 응답값으로 반환함
* 그리고 응답 받은 IP주소 값으로 구글에 접속함
