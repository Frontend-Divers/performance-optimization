# 3장 웹 사이트 성능을 개선하는 기본적인 방법

<br>

## 3.1 HTTP 요청 수 줄이기

<br>

- 스크립트, CSS, 이미지, 폰트 등 요청하는 컨텐츠의 수가 많을수록 필연적으로 로딩 완료 시점이 뒤로 미뤄진다.
- 특히 각 컨텐츠의 도메인이 다르면 DNS 조회 수도 늘어난다.
- 따라서 좋은 웹 성능을 위해선 HTTP 요청 수를 줄여야 한다.
- 단순하게는 컨텐츠의 수를 줄이는 것이 가장 좋지만 그럴 수 없는 상황이 분명히 존재한다.
- 따라서 페이지에 나타나는 컨텐츠는 동일하게 유지하고 HTTP 요청 수를 줄이는 방법을 찾아야한다.

<br>

### 3.1.1 스크립트 파일 병합

<br>

- 기능별로 모듈화해 여러 파일을 두면 자연스레 HTTP 요청 수가 증가한다.
- 모듈화된 여러 파일을 하나로 합쳐(번들) 하나의 요청만으로 불러오게 한다면 웹 성능에 도움이 될 수 있다.
- 번들 과정에서 하나의 파일의 크기가 너무 커진다면 오히려 성능에 악영향을 주므로 적절한 크기를 유지하는 것이 중요하다.

<br>

### 3.1.2 인라인 이미지

<br>

- Data URI를 사용해 이미지를 HTML 문서에 임베드하는 방식
- HTML 파일의 용량이 증가하나 HTTP 요청을 보내지 않는다는 장점이 있다.
- HTML 문서에 임베드 되어 있기 때문에 이미지만 따로 캐싱할 수 없다.

<br>

### 3.1.3 CSS 스프라이트

<br>

- 여러 이미지(주로 아이콘)를 하나의 이미지 파일로 결함하고 필요한 이미지의 위치 좌표(background-position)를 사용하는 방식이다.
- 하나의 HTTP 요청만으로 여러 이미지를 사용할 수 있다는 장점이 있다.

<br>

## 3.2 콘텐츠 파일 크기 줄이기

<br>

- 요청의 수를 줄이는 것도 중요하지만 전송하는 컨텐츠의 크기를 줄이는 것도 성능에 영향을 준다.
- 그러나 무작정 크기를 줄이는 것은 컨텐츠 자체를 훼손 할 수 있다.
- 따라서 컨텐츠를 유지하면서 크기를 줄이는 방법을 고민해야한다.

<br>

### 3.2.1 스크립트 파일 압축 전달

<br>

- HTML, CSS, JS, XML, JSON 등은 모두 스크립트 형태의 텍스트 파일이다.
- 웹 서버가 지원하는 방식으로 해당 스크립트들을 압축해서 클라이언트에 제공할 수 있다.
- 이때, 서버는 클라이언트에서 지원하는 형식으로 압축을 해야한다.
- 이를 위해 HTTP 프로토콜에서는 Accept-Encoding, Content-Encoding 헤더를 사용해 압축 방식에 대한 정보를 공유한다.
  - 클라이언트는 컨텐츠를 요청할 때 자신이 지원하는 압축 알고리즘을 요청 헤더 Accept-Encoding에 나열해 알려준다.
  - 서버는 이 중 자신이 지원하는 방식을 선택해 컨텐츠를 압축하여 제공한다.
  - 이때, 서버는 응답 헤더 Content-Encoding에 압축 알고리즘을 담는다.
  - 클라이언트는 서버가 헤더로 전달한 방식을 보고 압축된 파일을 해제한다.

<br>

### 3.2.2 스크립트 파일 최소화

<br>

- 스크립트 파일에 포함된 주석, 공백, 개행 문자 등 실제 로직에 영향을 주지 않는 부분을 제거해 전반적인 파일의 크기를 줄일 수 있다.
- 위 방식으로 최소화 된 스크립트를 디버깅하기 쉽지 않으므로 개발 환경에서는 최소화를 하지 않거나 source map을 사용한다.

<br>

### 3.2.3 이미지 파일 압축

<br>

- 이미지 파일에 대한 정보를 담고 있는 메타데이터를 제거해 크기를 줄일 수 있다.
- 손실 압축 방식으로 이미지의 크기를 줄일 수 있다. 
- 이미지 압축에 대한 자세한 내용은 4장에서 다룬다.

<br>

### 3.2.4 브라우저가 선호하는 이미지 포맷 사용

<br>

- 이미지 포맷에는 일반적으로 무손실 이미지 형식인 png, gif, 손실 이미지 형식인 jpeg 등 다양한 형식이 있다.
- 브라우저 개발팀에 의해 더욱 압축 효율이 좋은 포맷이 개발되기도 한다.
- WebP와 JPEG XR이 대표적이다.
  - WebP는 구글에서 개발된 손실 압축 방식의 이미지 포맷이다.
  - WebP는 동일 품질의 JPEG 보다 10% ~ 80% 정도 작게 압축할 수 있다.
  - JPEG XR은 MS에 의해 개발된 이미지 포맷으로 손실 압축과 비손실 압축을 모두 지원한다.
  - JPEG XR은 동일 품질 JPEG의 약 30% 정도 크기로 압축할 수 있다.
  - 각 형식을 개발사의 브라우저를 우선적으로 지원한다.

<br>

### 3.2.5 큰 파일은 작게 나누어 전송

<br>

- 동영상이나 패치 파일 등 크기가 매우 큰 컨텐츠의 경우 파일의 일부분을 순서대로 다운로드하는 부분 요청 응답 방식을 사용할 수 있다.
- 또한 크기를 가늠할 수 없는 컨텐츠 전송에도 유용하다.
- 이 방식은 웹서버가 지원할 때만 사용할 수 있다.
  - 지원 여부는 응답 헤더를 통해 확인할 수 있다.
  - 응답헤더에 "Accept-Ranges: bytes"가 포함되어 있으면 부분 지원 기능을 수락한다는 의미이다.
- 부분 지원이 가능한 컨텐츠에 경우 Range 헤더를 통해 특정 부분만 요청할 수 있다.
  - 이 경우 서버는 206 Partial Content로 응답한다.
  - 이때, 응답 헤더에 Content-Range 가 포함되면 전체 영역중 어느 부분을 전송했는지 명시한다.
  - "Range: bytes=0-50, 100-150" 과 같이 쉼표로 구분해 여러 범위를 동시에 요청할 수도 있다.

<br>

## 3.3 캐시 최적화 하기

<br>

- 컴퓨터 자원의 활용을 위해 캐시가 사용되듯 인터넷 상에서도 캐시를 사용한다.
- ISP가 제공하는 Proxy를 통해 캐시를 하면 로딩 속도를 개선할 수 있을 뿐만 아니라 네트워크 대역폭도 아낄 수 있다.
  - Proxy는 인터넷 구간에서 서버 대신 클리이언트 자우너 요청에 응답해주는 기능을 의미한다.
  - 서버와 클라이언트 사이에서 통신을 대신하는 기능 자체를 proxy, 이 중계 기능을 수행하는 서버를 Proxy server라고 한다.
- 인터넷 캐시는 PUSH 방식과 PULL 방식으로 구분할 수 있다.
  - PUSH
    - 캐시 영역에 미리 데이터를 복사해 두는 방식이다.
    - 특정 시간, 특정 지역에 사용자 요청이 과하게 몰릴 것을 대비할 수 있다.
  - PULL
    - 실제 요청이 있을 때만 캐시에 저장하는 방식이다.
- 브라우저에서도 캐시를 할 수 있다.
  - 특정 웹 사이트에서 받아온 컨텐츠들 중 브라우저가 저장할 수 있는 컨텐트 들은 클라이언트 측에 저장해 불필요한 요청 자체를 줄일 수 있다.
  - 서버는 Cache-Control 헤더를 통해 브라우저 캐시 여부와 어떤 방식으로 캐시를 할 것인지 명시한다.

<br>

## 3.4 CDN 사용하기

<br>

- CDN은 에지 서버(or 캐시 서버)라 불리는 대용량 인터넷 캐시 영역에 컨텐츠를 저장해 사용하는 네트워크 방식이다.
- 여러 엔드 포인트를 사용하는 일종의 proxy이다.
- CDN의 장점
  - 원거리 origin에서 컨텐트를 전달 받을 때 생길 수 있는 네트워크 지연, 패킷 손실 등의 현상을 줄일 수 있다.
  - 사용자는 가까운 에지에서 컨텐츠를 제공받으므로 로딩시간을 단축할 수 있다.
  - 원본서버의 부하를 줄일 수 있다.
  - 에지 서버와 에지 서버 간 ICP(Internet Cache Protocol)를 사용한 서버 전파를 할 수 있어 캐시 컨텐츠의 재사용률이 높다.

<br>
