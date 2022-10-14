### 상태 코드
- 클라이언트가 보낸 요청의 처리 상태를 응답하는 코드

### 1xx (Informational)
- 요청이 수신되어 처리중 (거의 사용X)

### 2xx (Successful)
- 요청 정상 처리
  - 200 OK : 요청 성공
  - 201 Created : 요청 성공하여 새로운 리소스 생성 
  - 202 Accepted : 요청이 접수되었으나 처리는 완료되지 않음 (배치 처리 등)
  - 204 No Content : 요청은 성공적으로 수행했으나 응답으로 보낼 결과 데이터가 없음

### 3xx  (Redirection)
- 요청 완료를 위해 추가 조치 필요
  - 300 Multiple Choices
  - 301 Moved Permanently
  - 302 Found
  - 303 See Other
  - 304 Not Modified
  - 307 Temporary Redirect
  - 308 Permanent Redirect

#### 리다이렉션
- 웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면 해당 위치로 자동 리다이렉트(이동)
![](https://velog.velcdn.com/images/psmin77/post/2fcf1f1d-5a99-430d-8010-f709cae573bd/image.jpeg)
- 영구 리다이렉션: 특정 리소스의 URI가 영구적으로 이동, 기존 URL을 사용하지 않음
  - 301 : 요청 메서드가 GET으로 변경, 본문 제거될 수 있음
  - 308 : 요청 메서드와 본문 유지
- 일시 리다이렉션: 일시적인 변경
  - 302 : 요청 메서드 GET, 본문 제거될 수 있음 -> 대부분 애플리케이션 라이브러리들이 기본값으로 사용
  - 307 : 요청 메서드와 본문 유지 -> 메서드가 변하면 안되는 경우 사용
  - 303: 302와 같은 기능, 요청 메서드를 GET으로 변경함(강제)
  - PRG(POST / Redirect / Get) : POST 요청 후에 새로고침으로 인한 중복 요청 방지, 결과화면만 GET으로 다시 요청
- 기타 특수 리다이렉션: 결과 대신 캐시 사용
  - 300 : 거의 사용하지 않음
  - 304 : 캐시를 목적으로 사용
클라이언트에게 리소스가 수정되지 않았음을 알려준 뒤 로컬PC에 저장된 캐시로 리다이렉트함 (응답에 메시지 바디를 포함하면 안됨)

### 4xx (Cilent Error)
- 클라이언트 오류: 잘못된 문법 등으로 요청을 처리할 수 없음, 똑같은 재시도하는 경우 실패
  - 400 Bad Request : 요청 구문, 메시지 등의 오류, 요청 내용을 다시 검토하고 보내야 함
  - 401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함
    - 인증(Authentication) : 확인 (로그인)
    - 인가(Authorization) : 권한 부여, 인가
  - 403 Forbidden : 서버가 요청은 확인했으나 승인을 거부함 (주로 접근 권한이 없는 경우)
  - 404 Not Found : 요청 리소스가 서버에 없음

### 5xx (Server Error)
- 서버 문제로 오류 발생, 다시 재시도하는 경우 성공할 수도 있음
  - 500 Internal Server Error : 서버 내부 문제 오류
  - 503 Service Unavailable : 일시적인 과부하 또는 점검 등으로 인해 처리할 수 없음
    - Retry-After : 헤더 필드에 복구 예정 시간을 보낼 수 있음 
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
