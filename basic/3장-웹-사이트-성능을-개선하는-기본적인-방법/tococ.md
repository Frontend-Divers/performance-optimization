# 3장 웹 사이트 성능을 개선하는 기본적인 방법
## 3.1 HTTP 요청 수 줄이기
- 웹 페이지에서 요청하는 콘텐츠의 수가 많을수록 로딩 완료 시간은 길어지고, 이미지 같은 콘텐츠가 적은 페이지는 매우 빠르게 로딩이 완료된다.
  - 따라서, 웹 성능을 더 빠르게 하기 위해서 HTTP의 요청 수를 줄여야한다.
- 웹 페이지를 단순하게 제작하는 것이 HTTP 프로토콜 요청 수를 줄이는 가장 쉬운방법이다.
  - 하지만, 웹 사이트를 통해 기업을 홍보하거나 상품 판매를 위해 많은 사용자를 끌어들여야 하는 실제 상황을 고려하면, 웹 성능을 위해 나타낼 콘텐츠를 줄이는 것이 현실적으로 적절한 방법은 아니다.

<br>

### 3.1.1 스크립트 파일 병합

- 모듈화는 HTTP 요청 수를 증가시키므로 웹 성능에 부정적인 영향을 미친다.

  > 모듈화 - 소프트웨어 개발의 손쉬운 분업화 및 편리한 유지 보수를 위해 최소 기능 단위별로 소프트웨어 모듈을 나누어 개발하는 것을 제안하는데 이를 모듈화라고 한다.

- 따라서, 기능 단위로 모듈화된 여러 파일들을 하나로 합치고 이 하나의 파일을 브라우저가 실행하는 것이 여러 파일들을 각각 호출하는 것과 동일한 결과를 만들 수 있다면, 파일 병합으로 HTTP 요청수를 줄일 수 있습니다.
- 하지만,  합쳐진 파일의 크기가 너무 크다면 해당 파일을 다운로드해 브라우저 화면에 나타내는 로딩 과정이 너무 길어질 수 있으므로 적절한 크기를 유지해야한다.

<br>

### 3.1.2 인라인 이미지

- HTML 파일의 CSS안에 해시 정보를 통해 웹 페이지 배경 이미지 파일을 삽입을 하는 방식을 사용하면 HTML 파일의 바이트 크기가 소폭 커지게 된다. 
  - 하지만, 이미지 파일을 따로 호출하여 해당 크기만큼 파일을 받아오는 전통적인 방식과 비교하면 전체 로딩시간이 단축된다.

<br>

### 3.1.3 CSS 스프라이트

- 여러 개의 이미지를 하나의 이미지 파일로 결합해 필요한 이미지가 위치하는 픽셀 좌표 정보를 사용하는 방식이다.

<br>

## 3.2 콘텐츠 파일 크기 줄이기

- 웹 사이트의 파일 수를 줄이더라도 파일 자체의 크기가 크다면 이 또한 웹 성능에 부정적인 영향을 준다.
  - 파일이 크면 인터넷 전송 시간이 길어지기 때문이다.
- 아래의 방법들은, 파일 내용은 변하지 않고 크기를 줄일 수 있는 기능들이다.

<br>

### 3.2.1 스크립트 파일 압축 전달

- 각 웹 서버가 지원하는 방식으로 스크립트 형태 콘텐츠(JS,CSS XML, JSON등)를 압축해 클라이언트에게 더 작은 크기로 내려주고, 이를 다운로드한 클라이언트가 압축을 해제하여 원래 콘텐츠를 사용한다면 인터넷 다운로드 속도가 좀 더 빨라질 수 있다.
- 다만 파일을 압축하여 내려주기 전에 웹 서버와 클라이언트는 서로가 지원하는 다양한 압축 방식 중 어떤 것을 사용할지 하나를 골라 정해야한다.
  - 압축 방식의 정보 교환은 HTTP 프로토콜에서 `Accept-Encoding`과 `Content-Encoding` 헤더를 사용하여 이루어진다.

<br>

### 3.2.2 스크립트 파일 최소화

- HTML, 자바스크립트, CSS같이 코딩된 스크립트 파일에 포함된 주석문, 공백, 개행 문자등 실제 로직에 아무런 영향을 주지 않는 부분을 제거하여 전반적인 파일 크기를 줄이는 방식이다.

<br>

### 3.2.3 이미지 파일 압축

- 이미지 파일은 웹 사이트에서 가장 많은 용량을 차지하는 콘텐츠이다.
- 이미지 파일은 해당 파일 정보를 메타 데이터에 포함해 저장한다. (어떤 카메라로 촬영했는지, 해상도가 무엇인지등)
- 메타 데이터는 사람의 눈에 실제 이미로써 보이지 않으므로 불필요한 부분을 제거하면 크기를 상당히 줄일 수 있다.

<br>

### 3.2.4 브라우저가 선호하는 이미지 포맷 사용

- 웹상의 이미지는 JPG, GIF, PNG등 다양한 포맷을 사용한다.
- 크롬이나 인터넷 익스플로러 개발팀은 자사 브라우저가 동일 품질의 이미지 크기를 더욱 줄일 수 있는 이미지 포맷을 개발했다.
  - WebP, JPEG XR
- WebP는 손실 압축 방식을 사용하는 이미지 형식
  - JPEG 이미지 형식을 대체하기 위해 처음부터 웹 사이트 트래픽 감소, 로딩 속도 단축을 목적으로 개발됨
  - 사진 이미지의 압축 효과가 높고화질 저하를 최소화하면서도 파일 크기를 작게 만든다.
  - 동일 품질의 JPEG보다 평균 50% 정도 파일 크기가 작아진다.

<br>

### 3.2.5 큰 파일은 작게 나누어 전송

- 인터넷 속도가 느린 곳이라면 크기가 큰 동영상을 재생할 때 버퍼링이 발생한다.
- 모든 파일을 다운로드하는 방식은 버퍼링을 유발하며 실제 보지 않는 부분까지 다운로드함으로써 인터넷 자원 낭비가 발생한다.
- 위 경우를 대비해, 큰 파일의 일부분을 순서대로 다운로드하는 부분 요청 응답 방식을 사용할 수 있다.
  - 부분 요청 응답 방식은 웹 서버에 특정 부분 파일 전달을 지원하는 기능이 있을 때만 가능하다.

<br>

## 3.3 캐시 최적화 하기
- 캐시는 자주 사용되는 콘텐츠나 특정 데이터 등을 임의의 저장소에 복제해두고 재사용하는 방식을 의미한다.
- 인터넷상에서 캐시는 ISP 회사가 지역에 분포된 특정 시스템에 사용자와 원격 시스템 사이에서 주고받은 데이터를 캐시하고 다음 사용자에게 제공하는 방식으로 널리 사용된다.
  - 콘텐츠를 캐시하는 이 시스템을 `프록시 서버`라고 부른다.
  - 해당 서버 덕분에 ISP 회사들은 네트워크 대역폭을 아낄 수 있다.
  - 또한, 소비자들은 좀 더 빠르게 콘텐츠 응답을 받을 수 있어 만족도가 증가한다.
- 인터넷에서 빠른 자원 전달을 위한 인터넷 캐시가 발달하자 해당 콘텐츠를 소모하는 브라우저도 콘텐츠를 캐시하기 시작했다.
  - 즉, 자주 바뀌지 않는 이미지나 자바스크립트, CSS파일 등을 인터넷 프록시 서버뿐만 아니라 사용자의 브라우저에도 캐시해놓습니다.

<br>

### 3.3.1 인터넷 캐시 사용

- 인터넷상에서 자주 요청되는 콘텐츠를 캐시하는 것은 속도와 인프라 보호 차원에서 중요하다.
  - 이를 주로 담당하는 시스템은 프록시 서버이다.
- 프록시 서버는 클라이언트가 처음 요청한 콘텐츠를 원본 서버에 대신 요청하여 클라이언트에게 전달해주고 이를 스스로 저장한다.
- 이후 다른 클라이언트가 동일한 콘텐츠를 요청했을 때 원본 서버에 접속할 필요 없이 자체 저장한 콘텐츠를 제공한다.
- 이 방법은 두 가지 장점을 가지고 있다.
  - 사용자 부근의 프록시 서버의 응답 속도가 원래 서버의 응답 속도보다 빠르다.
  - 원본 서버로 몰릴수 있는 인터넷 트래픽을 프록시 서버로 분산해 원본 서버의 자원을 절약한다.

<br>

### 3.3.2 브라우저 캐시 사용

- 브라우저 캐시는 클라이언트 위치의 캐시이다.
- 특정 웹 사이트에 접속하여 받아온 웹 콘텐츠들 중 브라우저가 저장할 수 있는 콘텐츠들을 클라이언트 측에 저장해 인터넷상의 요청을 아예 하지 않겠다는 개념이다.
- 특정 콘텐츠가 브라우저 캐시를 사용할지 아닐지는 일반적으로 웹 서버에서 먼저 결정해야한다.
- 웹 서버는 Catche-Control 응답 헤더를 통해 브라우저 캐시 관련 설정 내용을 클라이언트에게 전달한다.

<br>

## 3.4 CDN 사용하기

- CDN(Content Delivery Network)은 인터넷상에서 생산 소비되는 웹 콘텐츠를 사용자에게 빠르게 전달하기 우해 캐시 서버혹은 에지 서버라 불리는 대용량 인터넷 캐시 영역에 콘텐츠를 저장해 사용하는 네트워크 방식이다.

- 오늘날 인터넷 환경에서 광범위하게 사용되어 전 세계 인터넷 트래픽 성능을 개선해준다.

- CDN은 촘촘히 분산된 서버로 이루어져있고 사용자의 웹 콘텐츠 요청에 직접 응답한다.

- CDN은 주로 실제 인터넷 사용자가 가입한 ISP의 데이터 센터 내에 캐시 서버를 두고 이를 직접 사용자와 연결해 데이터를 전송한다.

  - 아래와 같은 장점들이 존재한다.
    - 네트워크 지연과 패킷 손실 현상을 줄일 수 있다.
    - 사용자는 가까운 에지 서버에 캐시된 콘텐츠를 전달받으므로 전송에 필요한 RTT(Round Trip Time)가 줄어들어 빠르게 콘텐츠를 받을 수 있다.
    - 원본 서버의 부하를 줄일 수 있다
    - etc.

  
