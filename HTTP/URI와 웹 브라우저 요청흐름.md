# URI(Uniform Resource Identifier)

![image](https://user-images.githubusercontent.com/74352543/220031855-7c20bd13-e79b-425f-949d-0d4205752068.png)

# URL
* 리소스의 위치
* 거의 URL만 씀

# URN
* 리소스의 이름

# URI의 뜻
* Uniform: 리소스 식별하는 통일된 방식
* Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
* Identifier: 다른 항목과 구분하는데 필요한 정보

# URL, URN 뜻
* URL - Locator: 리소스가 있는 위치를 지정
* URN - Name: 리소스에 이름을 부여
* 위치는 변할 수 있지만, 이름은 변하지 않음
* URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
* **URI를 URL과 같은 의미로 이해하면됨**

# URL 전체 문법

![image](https://user-images.githubusercontent.com/74352543/220033193-ff5057ac-f9e6-464e-b9bd-52801793a9f9.png)

* 프로토콜(https)
* 호스트명(www.google.com)
* 포트 번호(443)
* 패스(/search)
* 쿼리 파라미터(q=hello&hl=ko)

# scheme
* 주로 프로토콜 사용
* 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙 예) http,https,ftp  등등
* http는 80 포트, https는 443포트를 주로 사용, 포트는 생략 가능
* https는 http에 보안 추가

# userinfo
* URL에 사용자정보를 포함해서 인증
* 거의 사용하지 않음

# host
* 호스트명
* 도메인명 또는 IP 주소를 직접 사용가능

# path
* 리소스 경로(path), 계층적 구조
* 예)
* * /members
* * /members/100
* members에서 100번째 회원 조회 경로

# query
* key=value 형태
* ?로 시작, &로 추가 가능
* query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

# 웹 브라우저 요청 흐름
1. 먼저 DNS 서버를 조회하여 IP를 응답 값으로 받음, PORT 정보도 찾음
2. 웹브라우저가 HTTP 요청 메시지 생성함
![image](https://user-images.githubusercontent.com/74352543/220035302-9a1d0ed8-31a3-46b6-8bec-d1eb4aee9a14.png)
3. SOCKET 라이브러리를 통해 전달
4. TCP/IP 패킷 생성, HTTP 메시지 포함
![image](https://user-images.githubusercontent.com/74352543/220035678-bed46183-cc17-4e7d-86db-cde6bdfd8a14.png)
5. 구글 서버가 HTTP 메시지를 해석하여 HTTP 응답 메시지를 만듬
6. 앞의 과정과 똑같이 웹 브라우저에 도착
7. HTTP 응답 메시지를 보고 HTML 렌더링을 하여 결과를 확인


