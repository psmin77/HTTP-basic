### HTTP 헤더
- header-field = field-name":" OWS field-value OWS (OWS: 띄어쓰기 허용)
- (EX) Host: www.google.com, Content-Type: text/html;charset=UTF-8
- HTTP 전송에 필요한 모든 부가 정보(메시지 바디 내용, 바디 크기, 압축, 인증, 클라이언트/서버 정보 등)
- (과거) RFC2616 폐기
- (현재) RFC7230~7235 개정

#### RFC723x
- 엔티티(Entity) -> 표현(Representation) = 표현 메타데이터 + 표현 데이터
- HTTP BODY 
  - 메시지 본문을 통해 표현 데이터 전달
  - 메시지 본문 = 페이로드(payload)

#### 표현
- 요청이나 응답에서 전달할 실제 데이터, 요청/응답 모두 가능
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공(데이터 유형, 길이, 압축 정보 등)
- Content-Type: 표현 데이터의 형식
  - 미디어 타입(application/json), 문자 인코딩
- Content-Encoding: 표현 데이터의 압축 방식
  - 압축(gzip, indentity)
- Content-Language: 표현 데이터의 자연 언어
  -  ko, en
- Content-Length: 표현 데이터의 길이
  -  바이트 단위

#### 협상(콘텐츠 네고시에이션)
- 클라이언트가 선호하는 표현 요청, 요청 시에만 사용
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 협상과 우선순위(Quality Values)
  - 0~1 클수록 높은 우선 순위
  - 구체적인 것이 우선 순위 
  - 구체적인 것을 기준으로 미디어 타입을 맞춤

#### 전송 방식
- Transfer-Encoding
  - 단순 전송(Content-Length)
  - 압축 전송(Content-Encoding)
  - 분할 전송(Transfer-Encoding)
- 범위 전송(Range, Content-Range)

#### 일반 정보
- From: 유저 에이전트의 이메일 정보
- Referer: 이전 웹 페이지 주소
  - 유입 경로 분석 가능
- User-Agent: 유저 에이전트 애플리케이션 정보(웹 브라우저 정보 등)
  - 통계, 어떤 브라우저에서 장애가 발생하는지 파악 등
- Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date: 메시지가 생성된 날짜

#### 특별한 정보
- Host: 요청한 호스트 정보(도메인)
  - 하나의 서버가 여러 도메인을 처리해야 할 때
- Location: 페이지 리다이렉션
- Allow: 허용 가능한 HTTP 메서드
- Retry-After: 유저 에이전트가 다음 요청까지 기다려야 하는 시간

#### 인증(Authorization)
- 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate : 리소스 접근 시 필요한 인증 방법을 정의

#### 쿠키(Cookie)
- 무상태성(Stateless)인 HTTP에서 사용자 정보 등을 쿠키 저장소에 임시로 저장하여 사용함
![](https://velog.velcdn.com/images/psmin77/post/334b6993-982f-4cbc-813e-a40d10712af1/image.jpeg)
- 사용자 로그인 세션 관리, 광고 정보 트래킹 등에서 사용
- 쿠키 정보는 항상 서버에 전송됨 -> 네트워크 트래픽 추가 유발, 보안 정보는 저장하면 안됨 
- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버로부터 받은 쿠키를 저장하고, HTTP 요청 시 서버로 전달함
- 쿠키 생명주기
  - Set-Cookie: expires = 날짜 -> 지정한 날짜에 쿠키 삭제
  - 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시까지 유지(세션과 동일)
  - Set-Cookie: max-age=3600 (초단위) 
  - 영속 쿠키: 만료 날짜를 입력하면 지정한 날짜까지 유지
- 쿠키 도메인
  - 명시: 명시한 문서 기준 도메인 + 서브 도메인까지 포함
  - 생략: 현재 문서 기준 도메인만 적용
- 쿠키 경로
  - path=/루트 로 지정 
  - 지정한 경로를 포함한 하위 경로 페이지에만 쿠키 접근 가능
- 쿠키 보안
  - Secure: 일반적으로 http,https 모두 전송하지만 Secure 적용하면 https에만 전송
  - HttpOnly: XSS 공격 방지, 자바스크립트 접근 불가, HTTP 전송에만 사용
  - SameSite: XSRF 공격 방지, 요청 도메인과 쿠기 설정 도메인이 같은 경우에만 전송
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
