# html/css 실습

## 숨김콘텐츠

화면에서는 보이지 않으나, 보조기기는 해당 내용을 읽어주어야 할 때 사용하는 기법.

예전에는 `positon:absolute; top:-1000px`등과 같이 화면에서 안보이게 작업하기도 했으나,
`top`값이 음수값으로 설정되어있어 포커싱 될 경우 스크롤리 화면 상단으로 튀는 현상이 발생했음.

접근성에 위배되지 않으면서 숨김콘텐츠를 적용할 수 있는 코드는 다음과 같다.

```css
.a11y-hidden { /* a11y-hidden는 숨김콘텐츠를 위한 utility class 많이 사용 됨 */
    position: absolute;
    width: 1px; /* 최소한의 가로, 세로값이 있어야 요소가 있는 것으로 판단. */
    height: 1px;
    margin: -1px;
    /* clip 속성은 clip-path가 적용되지 않는 구형 브라우저(ie)를 커버하기 위해 넣음.*/
    /* clip 속성은 position:absolute; 일 경우에만 적용 됨 */
    clip: rect(0 0 0 0);
    clip: rect(0,0,0,0);
    clip-path: inset(50%);
    /* overflow는 넘치는 텍스트를 없애기 위해 사용 */
    overflow: hidden;
}
```
* 참고 : [숨김 콘첸트 관련 참고 글](https://mulder21c.github.io/2019/03/22/screen-hide-text/)

## float 된 요소의 더블마진
ie6에서는 `float`의 방향과 `margin`의 방향이 같을때 `margin`이 2배로 생겨나는 버그가 있었음.

ie6까지 크로스브라우징 해야 할 경우 유의해야 함.

## 점진적 향상(Progressive Enhancement)과 우아한 성능 저하(Graceful Degradation)
점진적 향상 기법과 우아한 성능 저하 기법은 모두 최신 브라우저와 구형 브라우저에 대응하기 위한 방법을 의미한다.

1. 점진적 향상
    - 기본적인 기능부터 모던한 기능으로 쌓아가는 것.
    - 최신 브라우저에서 더 나은 화면과 추가된 부가기능을 사용할 수 있게 하면서도, 구형 브라우저에서도 콘텐츠 가독이 가능하게 하는 방법

2. 우아한 성능 저하
    - 최신 기술을 기반으로 기능을 구현하고, 구형 기술을 기반한 환경에서도 유사하게 동작하도록 만드는 방법
    - 즉, 최신 기능을 제공한 상태에서 대안을 만들어 제공한다. (예. 현재 페이지는 javascript를 활성화 한 후 확인해주세요! 같은 알림멘트)

## background-position 동작 방식
`background-position`을 px로 정의내릴 경우, 좌상단 꼭지점을 기준으로 위치가 설정 됨.
백분율로 설정 할 경우, 백그라운드로 설정되는 영역의 백분율 뿐만 아니라 background로 사용되는 이미지 또한 해당 비율에 맞는 위치가 기준으로 설정 됨.

## 브라우저의 reflow, repaint
`padding`, `margin`, `width`, `height`, `position`과 같이 레이아웃에 관여하는 속성들은 reflow, repaint가 일어나기 때문에 성능저하를 야기 할 수 있음.

`transform`, `opacity`의 경우 일반적으로 reflow, repaint가 일어나지 않기때문에, 성능을 고려할 경우 이런 속성을 사용해야 함.
(단, opacity의 경우 레이아웃에 영향을 주지 않기때문에 reflow, repaint가 일어나지 않는다는 것이 일반적인 견해이나 webkit 엔진에서는 feflow한다고 하니 유의 할 것.)

* 참고자료 : [배영 - CSS Animation 성능 이론과 실제 적용 사례 (WSConf.Seoul.2017. Vol.2)](https://www.slideshare.net/wsconf/css-animation-wsconfseoul2017-vol2?qid=d1c12dab-f8b0-4b4c-a5af-964e5cae15e0&v=&b=&from_search=15)

## CSS : will-change 속성
`will-change`속성은 요소의 예상되는 변화의 종류에 관한 힌트를 부라우저에게 제공한다. 
하여 실제 요소가 변화되기 전에 미리 브라우저는 적절하게 최적화 할 수 있다.
이런 최적화는 잠재적으로 성능 비용이 큰 작업이 실제로 요구되기 전에 미리 실행함으로써 페이지의 반응성을 증가시킬 수 있다.

단, 너무 많은 요소에 이 속성을 사용 할 경우 오히려 성능 저하를 야기시킬 수 있다. 