### 2.5.3 네비게이션 타이밍 속성

key 속성 : API에서 정의한 웹 브라우저가 웹 페이지를 로딩 시 실행하는 각 단계

value 값 : 이 단계가 완료된 시간은 Unix Epoch Time 형식으로 변환한 값

각 performance.timing 속성은 페이지 요청 등의 탐색 이벤트 시간이나 DOM 로딩 시작 등의 페이지 로드 이벤트 시간을 1970년 1월 1일 자정부터 측정한 UTC 형식의 밀리초 단위로 나타냄.  
(이미지에서 빨간색 박스)  
![Cap 2021-12-15 21-43-05-174](https://user-images.githubusercontent.com/48556400/146189142-15915268-2a70-4a7b-98b4-a738db8ce325.jpg)  

### 2.5.4 네비게이션 타이밍 속성값 구하기

페이지 로딩에 소요된 시간을 밀리초 단위로 확인가능(이미지에서 노란색 박스)

```javascript
function onLoad() {
        var now = new Date().getTime();
        var page_load_time = now - performance.timing.navigationStart;
        console.log("User-perceived page loading time: " + page_load_time);
      }
```

HTML 문서가 실행되면 onLoad()함수가 바로 호출됨

아주 짧은 시간에 navigationStart가 실행되었음

이를 변경하여 구글 로고 이미지파일을 3번 받아오도록 수정하여 시간을 살펴보자

```javascript
function onLoad() {
                    var now = new Date().getTime();
                    document.write("<img src="https://www.google.com/images/branding/
                    googlelogo/1x/googlelogo_color_272x92dp.png"><br>");
                    document.write("<img src="https://www.google.com/images/branding/
                    googlelogo/1x/googlelogo_color_272x92dp.png"><br>");
                    document.write("<img src="https://www.google.com/images/branding/
                    googlelogo/1x/googlelogo_color_272x92dp.png"><br>");
                    var page_load_time = now - performance.timing.navigationStart;
                    console.log("User-perceived page loading time: " + page_load_time);
            }
```



#### 네비게이션 타이밍 API의 속성값 사용

```javascript
//Navigation Timing API 개체 생성
var perfData = window.performance.timing;
//navigationStart, loadEventEnd 속성을 사용하여 페이지 전체 로드 시간 구하기
var pageLoadTime = perfData.loadEventEnd - perfData.navigationStart;
console.log("pageLoadTime: " + pageLoadTime + "ms.");
//requestStart, responseEnd 속성을 사용하여 HTTP 요청에서 응답까지 걸린 시간 구하기
var connectTime = perfData.responseEnd - perfData.requestStart;
console.log("connectTime: " + connectTime + "ms.");
```

