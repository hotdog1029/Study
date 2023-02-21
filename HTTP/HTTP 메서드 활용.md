# 클라이언트에서 서버로 데이터 전송

# 데이터 전달 방식은 크게 2가지
* 쿼리 파라미터를 통한 데이터 전송
  * GET
  * 주로 정렬 필터(검색어)
* 메시지 바디를 통한 데이터 전송
 * POST, PUT, PATCH
 * 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

# 4가지 상황
* 정적 데이터 조회
 * 이미지, 정적 텍스트 문서
* 동적 데이터 조회
 * 주로 검색, 게시판 목록에서 정렬 필터(검색어)
* HTML Form을 통한 데이터 전송
 * 회원 가입, 상품 주문, 데이터 변경
* HTTP API를 통한 데이터 전송
 * 회원 가입, 상품 주문, 데이터 변경
 * 서버 to 서버, 앱 클라이언트, 웹 클라이언트

![image](https://user-images.githubusercontent.com/74352543/220249158-00cff37b-3616-48e2-aeea-a56de3e9c14d.png)

# 정적 데이터 조회
* 이미지, 정적 텍스트 문서
* 조회는 GET 사용
* 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

![image](https://user-images.githubusercontent.com/74352543/220249283-6073ed68-5985-44aa-bb65-3c6b0efa6dcf.png)

# 동적 데이터 조회
* 주로 검색, 게시판 목록에서 정렬 필터(검색어)
* 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
* 조회는 GET 사용
* GET은 쿼리 파라미터 사용해서 데이터 전달

![image](https://user-images.githubusercontent.com/74352543/220249415-aa5c3080-b95e-4ecf-bed3-02ba9bc22ce3.png)

![image](https://user-images.githubusercontent.com/74352543/220249607-d44ca40c-82d6-4823-95e8-9818862d0dd1.png)

![image](https://user-images.githubusercontent.com/74352543/220249639-02f610d9-4b1a-40a9-98f0-f4ab67b10799.png)

![image](https://user-images.githubusercontent.com/74352543/220249654-6d7fc533-05d1-41e1-8e25-8639848d1e4c.png)

# HTML Form 데이터 전송
* HTML Form submit시 POST 전송
 * 예) 회원 가입, 상품 주문, 데이터 변경
* Content-Type: application/x-www-form-urlencoded 사용
 * form의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
 * 전송 데이터를 url encoding 처리
  * 예) abc김 -> abc%EA%B9%80
* HTML Form은 GET 전송도 가능
* Content-Type: multipart/form-data
 * 파일 업로드 같은 바이너리 데이터 전송시 사용
 * 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능 (그래서 이름이 multipart)
* 참고: HTML Form 전송은 POST와 GET만 지원

![image](https://user-images.githubusercontent.com/74352543/220250697-4a568302-b7fb-4bd0-9e59-58a249ab0782.png)

