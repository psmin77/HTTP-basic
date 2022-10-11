### URI (Uniform Resource Identifier)
- Uniform: 리소스를 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것
- Identifier: 다른 항목과 구분하는데 필요한 정보

#### URL / URN
- URL (Resource Locator) : 자원의 위치 정보
- URN (Resource Name) : 자원의 이름
- 위치는 변할 수 있지만 이름은 변하지 않음
- 하지만 URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화되지 않음
- 대체로 URI = URL 같은 의미로 볼 수 있음

#### 전체 문법
- scheme://[userinfo@]host[:port]/[path][?query][#fragment]
- http://www.google.com:443/search?q=hello&hl=ko
- 프로토콜(https)
- 호스트명: 도메인명 또는 IP 주소
- 포트번호: 주로 http 80, https 443 사용
- 패스
- 쿼리 파라미터

### 웹 브라우저 요청 흐름
- HTTP 요청 메시지 생성
- HTTP 메시지 전송(TCP/IP 패킷), 요청 패킷 전달
- HTTP 응답 메시지 전달(Content-Type, Length, HTML Body 등)
- 웹 브라우저 HTML 렌더링
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
