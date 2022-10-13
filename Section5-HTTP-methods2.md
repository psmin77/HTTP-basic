### 클라이언트 -> 서버 데이터 전송
#### 데이터 전달 방식
- 쿼리 파라미터: GET, 주로 검색 또는 정렬 필터 등
- 메시지 바디: POST PUT PATCH, 회원가입 또는 상품 주문 등 리소스 등록과 변경

#### 데이터 전달 상황
- 정적 데이터 조회(GET)
  - 이미지, 정적 텍스트 문서
  - 쿼리 파라미터 없이 리소스 경로로 단순 조회

- 동적 데이터 조회(GET)
  - 주로 검색, 정렬 필터 등
  - 쿼리 파라미터를 통해 전달받은 데이터로 동적 결과를 생성

- HTML Form(GET, POST)
![](https://velog.velcdn.com/images/psmin77/post/41953551-1fb1-470d-82be-372f55fa17c3/image.jpeg)
  - 회원가입, 상품 주문 등 데이터 변경
  - HTML Form submit=GET/POST만 지원
   - Content-Type: application/x-www-form-urlencoded (기본)
    - 메시지 바디를 통해 form 내용을 쿼리 파라미터 형식으로 전송
    - 전송 데이터를 url encoding 처리
  - Content-Type: multipart/form-data
    - 파일 업로드 같은 바이너리 데이터 전송 시 사용
    - 다른 종류의 여러 파일과 내용을 함께 전송 가능

- HTTP API(GET,POST,PUT,PATCH)
  - 회원가입, 상품주문 등 데이터 변경
  - 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)
  - Content-Type: application/json 주로 사용 (사실상 표준)

### HTTP API 설계 예시
- 컬렉션 Collection (POST 기반 등록)
  - 클라이언트는 등록될 리소스의 URI를 모른다 -> 서버가 새로 등록된 리소스 URI 생성함
  - 서버가 생성/관리하는 리소스 디렉터리 

- 스토어 Store (PUT 기반 등록)
  - 클라이언트가 리소스 URI를 알고 있음, 직접 지정함
  - 클라이언트가 직접 리소스를 관리하는 저장소

- HTML FORM 사용 (컨트롤러 Controller, 컨트롤 URI)
  - GET, POST만 지원
  - 동사로 된 리소스 경로 사용 (EX) /members/{id}/delete
  - HTTP 메서드로 해결하기 어려운 경우 사용
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
