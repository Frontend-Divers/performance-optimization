## 요약

Why? 웹 로딩 속도가 느리면 서비스 사용자의 이탈률이 높아진다. 웹 성능이 비즈니스 성패를 좌우한다.

How? 웹 성능 측정 방법과 웹 성능 예산 방법을 사용.

What? 웹 성능 목표를 만드는 지표(ex. YSlow)와 웹 성능 예산 지표(정량,시간,규칙)를 통해



앞으로 이 책을 통해, 프런트엔드에서 웹 성능을 최적화하는 기법을 배운다.


> 이 책에서 다루는 웹 최적화 기법도 프런트엔드에 많은 내용을 할당합니다. 24p

```
이유 : 프런트엔드가 페이지 로딩 시간 중 대부분을 차지함
- 사용자 관점에서 원하는 콘텐츠를 전달받았는지가 웹 성능의 기준이기 때문.
- 웹 서버가 콘텐츠를 생산하는 시간 < 사용자와 상호작용하여 원하는 콘텐츠를 렌더링하는 시간 
```



# 1. 웹 성능이란 무엇인가

## 1.1 웹

웹 == 인터넷일까?

동일하게 인식되기도 하지만, 웹은 인터넷이 제공하는 서비스 중 하나.

- 인터넷 서비스의 종류 : 이메일, 메신저, 텔넷(원격연결), FTP 등

### 1.1.1 웹의 역사

- 웹 등장 이전 : TCP/IP나 UDP를 이용한 클라이언트-서버간 네트워크 통신 또는 소켓 네트워크 기술을 사용하여 데이터를 교환함

- 웹의 등장 : 페이지를 기반으로 다양한 정보를 문서읽듯 제공. 브라우저를 일종의 데이터베이스로 사용하여 필요한 정보를 조회/전달할 방법을 고안함.

```
웹을 한 마디로 정의하면
" 하이퍼 텍스트를 바탕으로 관련있는 문서끼리 연결할 문서의 집합체 "
```

- 하이퍼텍스트 : 텍스트를 뛰어넘는 다양한 콘텐츠를 아우르는 형식.

---

- 서버의 역할  = 웹 서버

  TCP/IP 기술에서 고전적인 서버의 역할을 함. 문서 형식의 콘텐츠 정보를 전달

- 클라이언트의 역할 = 브라우저

  전달받은 페이지를 사용자가 볼 수 있는 화면에 출력하는 방식으로 서비스를 제공

- 사용자 : 하이퍼링크를 통해 다른 페이지로 이동하거나 사용자의 정보를 입력해서 보낼 수 있음.

---

- 최근 웹 동향 : 멀티미디어 기술이 더욱 발전, 보편화되면서 음성과 영상 콘텐츠뿐 아니라 VR, AR을 생산, 전달, 소비할 때도 사용



### 1.1.2 웹의 대표적인 요소

1. URL(Uniform Resource Locator)

2. 네트워크 프로토콜

   주로 HTTP를 사용한다. 헤더에는 클라이언트와 서버 사이에 필요한 정보를 담고, 바디(페이로드)에는 HTML이나 이미지 같은 실제 데이터를 받음

3. HTML

   웹 페이지에 실제로 나타낼 데이터를 정의하고 페이지 문서의 제목, 단락, 목록과 같은 구조를 표현하는 역할

그 외 Javascript, CSS

## 1.2 웹 성능이 중요한 이유

- #### **웹 로딩 속도가 느리면 서비스 사용자의 이탈률이 높아진다.**

  예시 : 웹사이트를 통해 수입을 만들어내는 온라인 쇼핑몰. 

  실제 사례 : 월 마트 웹사이트의 로딩 시간과 구매율의 상관관계

  웹사이트와 매출이 직접적인 연관이 없는 서비스라고 해도, 기업의 이미지와 직결됨.

- 용어 설명 : 웹 성능이란, 콘텐츠가 신속하게 전달되어 사용자가 원하는 서비스를 빠르게 전달받을 수 있도록 하는 시스템을 의미.(웹 사이트의 기능이나 내용을 의미하는 것이 아님.)

- 웹 성능(Web performance)은 웹 로딩 시간(Web loading time)

  브라우저 주소창에 도메인 주소를 입력하여 해당 사이트로 접속하고 웹 페이지가 로딩 되어 내용을 볼 수 있을 때까지 걸린 시간. 

- 3초의 법칙 : 3초 안에 웹 사이트에 접속한 사용자의 관심을 끌어야한다. (구글의 조사자료에 따르면 페이지가 3초 안에 로딩되지 않으면 53% 의 사용자가 떠난다.)
  1. 웹사이트의 로딩이 빨라야한다. (웹 성능과 연관된 부분)
  2. 웹사이트의 머리말이 주목받을 수 있어야한다.
  3. 웹 페이지의 글이 눈에 띄어야한다.
  4. 웹 페이지 내 사용자 행동이 필요한 부분은 명확이 전달해야한다. 
- 한국처럼 인터넷 전송속도가 빠른 나라에선 웹 성능 최적화(WPO, Web Performance Optimization)가 큰 관심을 받지 못했다. 그러나 **글로벌 서비스를 지향하며 많은 국가를 대상으로 프로젝트를 진행하는 경우 상대적으로 느린 인터넷 환경에 대비해야하기에**, WPO가 중요하다.



## 1.3 웹 성능 측정 방법

1. 웹 성능에 **영향을 주는 요소를 파악**해야한다. (사용자 환경, 공급자 환경, 전달 환경 등)
   - 사용자 입장 : 거주지역, 네트워크 장비(4G, 5G, Wi-fi 등), 브라우저 등
   - 공급자 입장 : DNS 네임 서버 응답 속도, 웹 서버 응답 속도, 웹 사이트의 백엔드 처리 속도, **프런트엔드 최적화 여부**
   - 전달 환경 : 웹 서버가 위치한 데이터 센터가 자체 전용선을 보유했는지, 유선망과 모바일망에 각각의 서버를 배포했는지
2. 이를 측정할 수 있는 **적절한 도구를 선택**해야한다.

### 1.3.1 크롬 브라우저의 개발자 도구

크롬 브라우저에서 F12로 실행

Network 탭에서 **전체 HTTP 요청 수와 응답수**, 전달받은 콘텐츠 파일들의 크기, **DOMContentLoaded** 시간, **Load시간**, **로딩 완료 시간(Finish)**을 확인할 수 있음

Waterfall차트는 어떤 콘텐츠 파일이 로딩 시간을 얼마나 소모했는지 시각적으로 나타낸다.

### 1.3.2 WebPageTest 서비스

WPT는 세계 여러 위치에서 웹 사이트 로딩 속도를 테스트할 수 있는 무료 서비스.

실제 유선망이나 모바일 망의 네트워크, 다양한 기기, 브라우저를 세계 곳곳에 설치하여 실제 사용자 환경에서 테스트할 수 있게 함.

웹 성능에 영향을 주는 6개 항목이 잘 지켜지고 있는지 A~F점수로 알려줌.

1. First Byte Time : 웹 서버에서 받은 콘텐츠의 첫 번째 바이트가 얼마 만에 도착했는가?
2. Keep-Alive Enabled : TCP 연결을 재사용하기 위한 Keep-Alive가 설정되어 있었는가?
3. Compress Tranfer : 스크립트 파일이 Content-Encoding으로 압축되어 있었는가?
4. Compress Image : 이미지를 압축해 최적화했는가?
5. Cache Static content : 정적 파일에 브라우저 캐시가 설정되어 있었는가?
6. Effective use of CDN : CDN을 효과적으로 적용했는가?

### 1.3.3 구글 PageSpeed

웹 사이트 성능 개선을 돕기 위해 구글에서 개발한 서비스.

- 모듈 **Mod_pagespeed** : Apache나 Nginx 웹 서버에 추가할수 있는 오픈소스 모듈.

  웹 서버에 연동하여 CSS, JavaScript, HTML, 이미지 등의 성능 최적화를 수행함.

  장점 : 원본 콘텐츠를 별도로 가공하여 저장할 필요없이 최적화된 모듈을 웹상에서 클라이언트에게 실시간으로 제공함. 설치 이후 자동으로 최적화 실행

- 모듈 **PSI**(PageSpeed Insights) : 웹 사이트의 성능 최적화 요소를 평가하는 서비스를 제공.

  1.3.2의 WebPageTest처럼 별도의 테스트지역이나 세세한 옵션을 선택할 순 없으나 PC와 모바일 환경의 웹 성능 테스트 결과를 심플하게 제공함.

- **FCP**(First Contentful Paint) : 웹 페이지가 사용자에게 시각적 응답을 보인 시간
- **DCL**(DOM Content Loaded) : 브라우저가 HTML 문서를 로딩 및 해석하는 시간을 측정한 값
- FCP와 DCL메트릭스로 특정 웹 페이지의 성능을 알림. 두 메트릭스로 측정된 데이터들의 중간값으로 빠른 영역, 중간 영역, 느린 영역이 전체 콘텐츠 대비 몇 %인지 비교가능.  

## 1.4 웹 성능을 만드는 지표

스티브 사우더스 <High Performance Web Sites>(ITC, 2008)

사우더스는 14가지 웹 성능 최적화 기법을 백엔드, 프런트엔드, 네트워크 기술로 나누었다. 

이후 야후는 이 항목들을 바탕으로 YSlow 서비스를 개발하여, 각 웹 성능 최적화 항목이 얼마나 잘 지켜지고 있는지 온라인에서 확인할 수 있도록 했다. (http://yslow.org/)

## Web Performance Best Practices and Rules

1. [Minimize HTTP Requests](http://developer.yahoo.com/performance/rules.html#num_http)
2. [Use a Content Delivery Network](http://developer.yahoo.com/performance/rules.html#cdn)
3. [Avoid empty src or href](http://developer.yahoo.com/performance/rules.html#emptysrc)
4. [Add an Expires or a Cache-Control Header](http://developer.yahoo.com/performance/rules.html#expires)
5. [Gzip Components](http://developer.yahoo.com/performance/rules.html#gzip)
6. [Put StyleSheets at the Top](http://developer.yahoo.com/performance/rules.html#css_top)
7. [Put Scripts at the Bottom](http://developer.yahoo.com/performance/rules.html#js_bottom)
8. [Avoid CSS Expressions](http://developer.yahoo.com/performance/rules.html#css_expressions)
9. [Make JavaScript and CSS External](http://developer.yahoo.com/performance/rules.html#external)
10. [Reduce DNS Lookups](http://developer.yahoo.com/performance/rules.html#dns_lookups)
11. [Minify JavaScript and CSS](http://developer.yahoo.com/performance/rules.html#minify)
12. [Avoid Redirects](http://developer.yahoo.com/performance/rules.html#redirects)
13. [Remove Duplicate Scripts](http://developer.yahoo.com/performance/rules.html#js_dupes)
14. [Configure ETags](http://developer.yahoo.com/performance/rules.html#etags)
15. [Make AJAX Cacheable](http://developer.yahoo.com/performance/rules.html#cacheajax)
16. [Use GET for AJAX Requests](http://developer.yahoo.com/performance/rules.html#ajax_get)
17. [Reduce the Number of DOM Elements](http://developer.yahoo.com/performance/rules.html#min_dom)
18. [No 404s](http://developer.yahoo.com/performance/rules.html#no404)
19. [Reduce Cookie Size](http://developer.yahoo.com/performance/rules.html#cookie_size)
20. [Use Cookie-Free Domains for Components](http://developer.yahoo.com/performance/rules.html#cookie_free)
21. [Avoid Filters](http://developer.yahoo.com/performance/rules.html#no_filters)
22. [Do Not Scale Images in HTML](http://developer.yahoo.com/performance/rules.html#no_scale)
23. [Make favicon.ico Small and Cacheable](http://developer.yahoo.com/performance/rules.html#favicon)

### 1.4.1 사용자 환경 - 프런트엔드

목적 : 빠르고 보기 쉽게 콘텐츠를 전달

역할 : 감각적인 디자인으로 더 많은 사용자들이 웹 사이트로 유입될 수 있도록 끌어들임,  콘텐츠를 보기 편하게 전달

### 1.4.2 공급자 환경 - 백엔드

백엔드는 사용자에게 보이는 프런트엔드 콘텐츠를 실제 생산하고 저장하여 네트워크를 통해 전달.

백엔드의 성능을 빠르게 알 수 있는 방법 : 구글 애널리틱스의 웹 성능과 속도 관련 서비스인 Speed 기능을 사용

### 1.4.1 전달 환경 - 네트워크

네트워크는 장소와 시간에 따라 속도가 변하기에 성능 측정이 어렵다.

네트워크 성능을 제약하는 두 가지 요소 : 대역폭(bandwidth), 지연시간(latency)

- 대역폭 : 일정 시간에 처리할 수 있는 트래픽 양. 사용자가 갑작스레 증가하면 이에 영향을 받아 웹 콘텐츠의 전달 속도를 느리게 만들 수도 있다.
- 지연시간 : 기술적 이유로 사용자에게 콘텐츠를 전달하지 못하고 지연되는 시간을 의미함. 인터넷상 다양한 환경에 영향을 받음

네트워크는 각 국가의 인터넷 서비스 사업자(ISP)가 제공하는 서비스를 사용한다. ISP 품질에 따라 대역폭과 지연 시간도 달라질 수 있다. 회사마다 유/무선망을 이용하는 사용자와 트래픽 증가에 따라 네트워크 장비 시스템 증설 투자 여부를 결정한다. 그러므로 보통 분기나 연도별로 평균값을 구하여 네트워크의 성능을 판단한다. 

## 1.5 웹 성능과 프런트엔드

소프트웨어 공학에서의 백엔드(데이터 접근 영역), 프런트엔드(소프트웨어의 표시영역), 

웹에서의 백엔드(사용자에게 제공하는 데이터를 생성,저장,전달), 프런트엔드(그 데이터를 요청하고 받아서 표현)

- 프런트엔드가 페이지 로딩 시간 중 대부분을 차지함
  - 이유 : 사용자 관점에서 원하는 콘텐츠를 전달받았는지가 웹 성능의 기준이기 때문.
  - 웹 서버가 콘텐츠를 생산하는 시간 < 사용자와 상호작용하여 원하는 콘텐츠를 렌더링하는 시간

### 1.5.1 브라우저 렌더링

방법1 : 브라우저 렌더링 시 성능 지표를 PageSpeed로 살펴본다.

방법2 : 크롬 개발자 도구-Lighthouse 기능을 사용한다. 



## 1.6 웹 성능 예산

웹 성능이 비즈니스 성패를 좌우하는 경우가 많다. 전자상거래와 같은 산업에서는 웹 성능 목표를 명확한 지표로 만들고 관리하는 것이 중요하다. 웹 성능을 계량할 수 있도록 수치화하여 기업의 목표로 삼을 때 '**웹 성능 예산**' 방법을 많이 사용한다. 

- **성능 예산**이란 : 웹 성능에 영향을 미치는 다양한 요소를 제어하는 한곗값을 의미. 웹 페이지의 파일 크기, 페이지 로딩시간, 페이지에 포함된 이미지 파일 수 등 다양한 값이 존재함.

### 1.6.1 정량 기반 지표

- 정량 기반 지표 : 이미지, 스크립트, 폰트 등 웹 페이지 제작에 필요한 요소들에 대한 한곗값

- 정량 기반 지표의 대표적 예시
  - 이미지 파일의 최대 크기
  - 최대 웹 폰트 파일 개수
  -  자바스크립트 파일 크기 합
  - 타사 스크립트 개수 합

### 1.6.2 시간 기반 지표

시간 기반 지표(timing based metrics)는 milestone timing이라고도 함.

정량 기반 지표의 단점을 보완하는 성능 예산이다.

DOMContentLoaded, Load와 같이 브라우저에서 실제로 발생하는 다양한 웹 성능 이벤트 값을 측정하여 사용주가 느끼는 웹 성능에 대한 목표치를 설정하는 방식

- 시간 기반 지표의 대표적 예시
  - **FCP**(First Contentful Paint) : 텍스트 또는 이미지와 같이 DOM의 첫 번째 비트를 표시하는 시점
  - **TTI**(Time to Interactive) : 페이지가 사용자 입력에 안정적으로 응답하는 데 걸리는 시간

### 1.6.3 규칙 기반 지표

- 규칙 기반 지표의 대표적 예시
  - **WebPageTest**의 성능 점수
  - 구글 **Lighthouse**의 성능 점수
- PageSpeed, WebPageTest, 구글의 Lighthouse 등이 제공하는 웹 성능 점수는 공신력있는 표준 점수이기 때문에 규칙 기반 지표에서 자주 사용됨. 
- 또는 사내에 자체적인 웹 성능 지표에 대한 테스트케이스를 만들고, 자동화 테스트 시스템을 통해 웹 사이트의 성능을 지표화하는 방식을 이용하기도 한다. 
- 정량 기반 지표와 시간 기반 지표를 개선할수록 규칙 기반 지표 점수는 높아진다.

### 1.6.4 성능 예산 활용

웹 기획자들이 사이트에 적합한 성능 예산이 어느정도 되는지 초기에 가늠하긴 어렵다. 따라서 일반적으로 **경쟁사 사이트나 비슷한 산업군의 대표적인 웹 사이트를 참고**함

가장 쉬운 접근 방법은 **아주 직관적이고 단순하게 성능 예산 목표치를 설정**하고 웹 사이트 설계와 개발을 시작하는 것이다. 

웹 사이트는 업데이트가 잦기 때문에, 최근에는 **형상 관리 및 새로운 버전을 빌드한 후 배포 이전에 최종 성능 예산을 측정하고 관리하는 방법**도 사용한다. 구글 Lighthouse의 측정값을 빌드의 CI 단계의 테스트 케이스로 사용하는 것이 대표적인 예이다.

