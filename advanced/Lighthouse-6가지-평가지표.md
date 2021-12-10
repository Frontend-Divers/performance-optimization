### 1. FCP(First Contentful Paint) - 15%

- FCP는 사용자가 페이지를 탐색 한 후 브라우저가 DOM 콘텐츠의 첫 번째 부분을 렌더링하는 데 걸리는 시간을 측정합니다. 페이지의 이미지, 흰색이 아닌 `<canvas>` 요소 및 SVG는 DOM 콘텐츠로 간주됩니다. iframe 내부의 내용은 포함되지 않는다.
  ![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/569069b6-b433-4deb-93f6-a080c066220e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5/20210822/us-west-2/s3/aws4_request&X-Amz-Date=20210822T053938Z&X-Amz-Expires=86400&X-Amz-Signature=4c14764633cf7e09b371fe58904ee19ff0fa3660920c00aadd813fe68f598a7c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20="Untitled.png")
- https://web.dev/first-contentful-paint/

### 2. Speed Index - 15%

- Speed Index는 페이지로드 중 콘텐츠가 시각적으로 표시되는 속도를 측정한다.
- Lighthouse는 먼저 브라우저에서로드되는 페이지의 비디오를 캡처하고 프레임 간의 시각적 진행을 계산합니다. Lighthouse는 Speedline Node.js 모듈 을 사용하여 Speed Index 점수를 생성한다.

![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0c403c7d-2b94-417f-8244-87c34c4190bd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5/20210822/us-west-2/s3/aws4_request&X-Amz-Date=20210822T054235Z&X-Amz-Expires=86400&X-Amz-Signature=a3d7097f65c4628a231946e48ef3f9f29c6565ec5eeeb229492884668b5a8be0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20="Untitled.png")

- https://web.dev/speed-index

### 3. LCP(Largest Contentful Paint) - 25%

- LCP는 페이지가 처음 로드 되기 시작한 시점을 기준으로 뷰포트 내에 표시되는 가장 큰 이미지 또는 텍스트 블록의 렌더링 시간을 측정한다.
- https://web.dev/lcp/

### 4. TTI(Time to Interactive) - 15%

- TTI는 페이지가 완전히 상호 작용하는 데 걸리는 시간을 측정한다.
- 페이지는 다음과 같은 경우 완전한 대화 형으로 간주됩니다.
- https://web.dev/interactive/

### 5. TBT(Total Blocking Time) - 25%

- TBT는 페이지가 마우스 클릭, 화면 탭 또는 키보드 누름과 같은 사용자 입력에 응답하지 못하도록 차단 된 총 시간을 측정한다.
- 합계는 First Contentful Paint와 Time to Interactive 사이의 모든 긴 작업의 차단 부분을 추가하여 계산된다.
- 50ms 이상 실행되는 모든 작업은 긴 작업으로 간주 된다. 50ms 이후의 시간이 차단 부분이다.
- 예를 들어 Lighthouse가 70ms의 긴 작업을 감지하면 차단 부분은 20ms가 된다.
- https://web.dev/lighthouse-total-blocking-time/

### 6. CLS(Cumulative Layout Shift) - 5%

- CLS는 페이지의 전체 수명 동안 발생하는 모든 예기치 않은 레이아웃 이동에 대한 모든 개별 레이아웃 이동 점수의 합계를 측정한다.
- 레이아웃 이동은 표시되는 요소가 렌더링 된 프레임에서 다음 프레임으로 위치를 변경할 때마다 발생한다.

- https://web.dev/cls/
