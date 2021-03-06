# 1. 웹 성능이란 무엇인가?

## 1.1 웹

웹은 인터넷의 대표적인 서비스

### 1.1.1 웹의 역사

- 물리학자들 간 공동으로 연구를 진행하고 그 결과를 빠르게 공유하기 위해 팀 버너스 리 등이 개발
- 기존에 이미 TCP/IP, UDP를 이용한 클라이언트-서버 간 네트워크 통신 또는 소켓 네트워크 기술이 존재했다. 그러나 웹 사이트라는 페이지를 기반으로 문자 뿐만 아니라 다양한 정보를 문서 읽듯 제공하고, 이를 읽을 수 있는 전용 프로그램인 브라우저를 일종의 데이터베이스로 사용해 필요한 정보를 조회하고 전달할 수 있는 방법 고안

### 1.1.2 웹의 대표적인 요소

1. URL
   - 웹 자원이 인터넷상 어느 위치에 존재하고 있는지 알려주는 방법
2. 네트워크 프로토콜
   - URL을 통해 알게 된 웹의 자원 위치에 접근하는 방식
3. HTML
   - 해당하는 콘텐츠를 사용자에게 쉽게 나타내기 위한 방법
   - 태그(tag)라는 명령어로 웹의 목적에 맞는 여러 기능 수행

## 1.2 웹 성능이 중요한 이유

- 웹 성능이라는 용어는 웹 사이트의 기능이나 내용을 의미하는 것이 아니라, 콘텐츠가 신속하게 전달되어 사용자가 원하는 서비스를 빠르게 전달받을 수 있도록 하는 시스템들의 성능을 의미한다.
- 웹 성능은 브라우저 주소창에 도메인 주소를 입력하여 해당 사이트에 접속하고 웹 페이지가 로딩되어 내용을 볼 수 있을 때까지 걸린 시간, 즉 웹 로딩 시간을 말한다.
- 월마트 닷컴에서 연구한 결과 로딩 시간을 1초 줄이면 구매율이 약 2% 증가한다는 사실을 밝혔다. 또한 로딩이 2초 내에 완료 됐을 때 사용자의 구매가 가장 많았다.
- 구글의 조사 자료에 따르면 페이지가 3초 안에 로딩되지 않으면 53%의 사용자가 떠나고 로딩 시간이 길어질수록 사용자 이탈률 역시 늘어난다고 한다.

## 1.3 웹 성능 측정 방법

### 1.3.1 크롬 브라우저 개발자도구

### 1.3.2 WebPageTest 서비스

- https://www.webpagetest.org/

### 1.3.3 구글 PageSpeed

- https://pagespeed.web.dev/



## 1.4 웹 성능을 만드는 지표

- 스티브 사우더스의 14가지 웹 성능 최적화 기법

| 최적화     | 내용                                                         |
| ---------- | ------------------------------------------------------------ |
| 백엔드     | 1. Expiers 헤더를 추가한다.<br />2. gzip으로 압축한다.<br />3. 페이지 재전송을 피한다.<br />4. ETag를 설정한다.<br />5. 캐시를 지원하는 AJAX를 만든다. |
| 프론트엔드 | 1. HTTP 요청을 줄인다.<br />2. 스타일 시트는 상단에 넣는다.<br />3. 스크립트는 하단에 넣는다. <br />4. CSS표현식은 피한다.<br />5. 자바스크립트와 CSS는 외부 파일에 넣는다.<br />6. 자바스크립트는 작게 한다.<br />7. 중복 스크립트는 제거한다. |
| 네트워크   | 1. CDN을 사용한다.<br />2. DNS 조회를 줄인다.                |

## 1.5 웹 성능과 프런트엔드 

- 프론트엔드가 페이지 로딩 시간 중 대부분을 차지하는 이유는 웹 서버가 아닌 '사용자 관점에서 원하는 콘텐츠를 전달받았는지'가 웹 성능의 기준.

## 1.6 웹 성능 예산

### 1.6.1 정량 기반 지표

- 이미지 파일의 최대 크기
- 최대 웹 폰트 파일 개수
- 자바스크립트 파일 크기 합
- 타사 스크립트 개수 합

### 1.6.2 시간 기반 지표

- FCP(First Contentful Paint)
- TTI(Time to Interactive)

### 1.6.3 규칙 기반 지표

- WebPageTest의 성능 점수
- 구글 Lighthouse의 성능 점수
