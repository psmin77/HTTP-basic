### 캐시 기본 동작
- 캐시가 없으면 데이터가 변경되지 않아도 계속 같은 데이터를 다운로드 받아야 함 -> 느리고 비용이 많이 듦
- 캐시 적용 -> 비용 절감, 속도 개선, 빠른 사용자 경험 등
  - 캐시 적용: cache-control: max-age=시간 -> 캐시가 유효한 시간(초)
  - 응답 결과를 캐시에 저장
  - 이후 요청 시 캐시 유효 시간 검증
  1. 유효한 경우 캐시에서 조회
  2. 캐시 만료된 경우 서버에 재요청하여 갱신함

### 검증 헤더와 조건부 요청
#### 캐시 만료 후
- 검증 헤더(Validator): 캐시 데이터와 서버 데이터가 동일한지 검증하는 데이터
  - 데이터 최종 수정일(Last-Modified)
    - 캐시 시간 초과 후 두 번째 요청 시 검증 헤더를 통해 최종 수정일 확인
    - 동일한 경우 HTTP Body 없이 header만 전송 받음
    - 캐시에 저장된 기존 응답결과 재사용, 헤더 데이터만 갱신
    - 네트워크 다운로드 용량이 적고 실용적
  - ETag(Entity Tag)
    - 캐시용 데이터에 임의의 고유한 버전 이름 저장

- 조건부 요청 헤더: 검증 헤더로 조건에 따른 분기
  - If-Modified-Since: 이후에 데이터가 수정된 경우 (Last-Modified 사용)
    - 304 Not Modified : 수정되지 않음, 기존 캐시 데이터 사용(헤더만 전송)
    - 200 OK: 모든 데이터 전송
    - 1초 미만 단위로 캐시 조정 불가능
    - 날짜 기반의 로직 사용
    - 데이터를 수정한 날짜는 다르지만 데이터 내용이 동일한 경우 적용이 어려움
  - If-None-Match (Etag 사용)
    - Etag 매치 여부 확인
    - 캐시 제어 로직을 서버에서 완전히 관리하고, 클라이언트는 단순히 Etag 값만 제공함

#### 캐시 제어 헤더
- Cache-Control: 캐시 제어
  - Cache-Control: max-age 
    - 캐시 유효 시간, 초 단위 
  - Cache-Control: no-cache
    - 데이터 캐시 가능하지만, 원서버(Origin) 검증 후 사용 
  - Cache-Control: no-store
    - 캐시 저장 불가, 사용 후 즉시 삭제
- Pragma: 캐시 제어(하위 호환)
- Expires: 캐시 유효 기간(하위 호환)

#### 프록시 캐시
![](https://velog.velcdn.com/images/psmin77/post/fc14343c-3a07-4c86-a59b-c6b47e50dce3/image.jpeg)
- Origin 서버와 요청 브라우저 사이 프록시 캐시 서버(public 캐시)를 저장함
  - Cache-Control: public 
    - public 캐시로 저장 가능
  - Cache-Control: private 
    - 특정 사용자에게만 해당, private 캐시에 저장 가능(기본값)
  - Cache-Control: s-maxage 
    - 프록시 캐시에만 적용되는 max-age
  - Age: 60 (HTTP 헤더) 오리진 서버에서 응답 후 프록시 캐시에 머문 시간(초)

#### 캐시 무효화
- Cache-Control: no-cache
  - 데이터 캐시 가능하지만, 원 서버(Origin)에 검증하고 사용 
  - 원 서버에 접근할 수 없는 경우 서버 설정에 따라 이전 데이터 or 오류 발생
- Cache-Control: no-store
  - 캐시 저장 불가, 사용 후 즉시 삭제 
- Cache-Control: must-revalidate
  - 캐시 만료 후 최초 조회 시 원서버에 검증 필요
  - 원 서버에 접근할 수 없는 경우 반드시 오류 발생(504 Gateway Timeout)
- Pragma: no-cache
<br>

>
[출처] 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한, 인프런
