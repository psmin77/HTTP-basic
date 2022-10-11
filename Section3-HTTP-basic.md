### HTTP(HyperText Transfer Protocol)
- HTTP 메시지를 통해 HTML, TEXT, IMAGE, JSON 등등 거의 모든 형태의 서버 간 데이터를 주고 받음
- HTTP 역사
  - HTTP/0.9 (1991): GET 메서드만 지원, 헤더X
  - HTTP/1.0 (1996): 메서드, 헤더 추가
  - ** HTTP/1.1 (1997): 현재까지 가장 많이 사용, 중요**
  - HTTP/2 (2015): 성능 개선
  - HTTP/3 (~현재):TCP 대신 UDP 사용, 성능 개선
- HTTP 특징
  - 클라이언트/서버 구조
  - 무상태 프로토콜(Stateless)
  - 비연결성
  - HTTP 메시지
  - 단순함과 확장 가능

### 클라이언트 서버 구조
- Request / Response 구조
- 클라이언트가 서버에 요청을 보내면 서버가 요청 결과로 응답

### Stateful, Stateless
- 상태유지(Stateful) : 항상 같은 서버가 유지되어야 함
-> 연결이 끊기거나 장애 발생 시 문제
- 무상태 프로토콜(Stateless): 서버가 클라이언트의 상태를 보존하지 않음, 장애 발생 시에도 다른 서버와 연결 가능
->  확장성 높음(스케일 아웃, 수평 확장 유리)
-> 추가 데이터 전송해야 함
- 일반적으로 무상태로 설계하면서 필요한 경우에만 상태 유지(ex. 로그인)를 최소한으로 사용

### 비연결성(Connectionless)
- HTTP는 기본으로 연결 유지하지 않음
- 처음 요청 시 연결/응답하고, 데이터 송수신 후 연결 종료하는 형태(최소한의 자원만 사용)
- 서버 자원을 효율적으로 사용할 수 있음
- 한계와 극복
![](https://velog.velcdn.com/images/psmin77/post/64974701-e4b0-4403-9a3c-5b1dde2df37f/image.jpeg)
  - 매번 TCP/IP 연결 다시하여 낭비
  - HTTP 지속 연결(Peristent Connections) 및 최적화로 개선

### HTTP 메시지
#### HTTP 메시지 구조
- start-line 시작 라인
  - [요청] HTTP 메서드 / 요청 대상 / HTTP Version
  - (EX) GET / search?q=hello&hl=ko HTTP/1.1
  - [응답] HTTP 버전 / 상태 코드 / 문구
  - (EX) HTTP/1.1 200 OK
    - 상태코드: 200 성공, 400 클라이언트 요청 오류, 500 서버 내부 오류 등

- header 헤더
  - HTTP 전송에 필요한 모든 부가 정보(메시지 바디의 내용, 크기, 인층, 요청 정보 등)
  - field-name":" OWS field-values OWS (OWS 띄어쓰기 허용)
  - (EX) [요청] Host: www.google.com 
  - (EX) [응답] Content-Type: text/html

- empty line 공백 라인(CRLF) 
- message body 메시지 바디
  - 실제 전송할 데이터
  - HTML, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능

### 단순함과 확장 가능
- HTTP 단순하고 확장 가능한 기술 -> 성공 요인
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
