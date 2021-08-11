#CSS
## CSS란?
* CSS(Cascading Style Sheet) : 마크업 언어가 실제로 표시되는 방법을 기술하는 언어로 HTML과 XHTML에 주로 ML에 쓰이며 XML에서도 사용 가능.
* CSS는 W3C의 표준.

## CSS의 과거와 현재
1. 1996년 W3C이 주도하에 CSS Level 1 발표.
2. 1998년 CSS Level 2가 등장하면서 대부분의 웹 브라우저가 CSS Level 2를 지원
3. 2006년 CSS Level 2의 버그를 수정한 CSS Level 2.1이 발표되면서 현재까지 표준으로 사용되고 있음.
4. CSS Level 3는 CSS Level 2.1과 달리 모든 명세가 포함된 버전이 아닌 모듈 단위로 개발되고 있으며, 표준화가 모듈단위로 진행되고 있음.


## 웹표준 개발단계
1. Draft(초안, FPWD) -> Working Draft(작업 초안, WD) -> Candidate Recommendation(권고 후보, CR) -> Proposed Recommendation(최종 권고안, PR) -> Recommendation(권고안, REC)
* [참고링크:W3C](https://www.w3.org/Style/CSS/current-work)
* [웹 브라우저별 CSS3 지원 TEST](https://css3test.com)

## CSS 사용 의의
과거에는 사이트는 구조, 표현, 동작의 분리가 제일 좋은 방법론이었음.

현재는 아주 작은 단위로 쪼개, markup, css, javascript를 컴포넌트화 하여 사용하는 방식으로 변화하고 있음. 각 단위별로 완성되어있고, 이것들을 부품화하여 조립하여 사용하는 방향으로 진행되고 있음

----

### 브라우저 렌더링 엔진

요청한 콘텐츠를 화면에 출력하는 역할. HTML, CSS 등을 파싱하여 최종적으로 화면에 그림.

- 브라우저 렌더링 엔진 종류
    - 게코(Gecko) : 모질라 재단에서 만든 레이아웃 엔진으로 파이어폭스, 모질라 선더버드, 시몽키 등이 이를 탑재하고 있다.
    - 블링크(Blink) : 웹키트에서 파생된 레이아웃 엔진으로 크롬, 오페라 등이 이를 탑재하고 있다.
    - 트라이던트(Trident) : 마이크로소프트의 레이아웃 엔진으로 인터넷 익스플로러, 아웃룩 익스프레스, 마이크로소프트 아웃룩, 그리고 윈앰프, 리얼플레이어의 미니 브라우저 등이 이를 탑재하고 있다.
    - 프레스토(Presto) : 오페라 소프트웨어의 사유 엔진으로 오페라가 탑재하고 있었으나, 오페라 15부터는 블링크로 교체되었다.
    - KHTML : KDE의 컨커러가 탑재하고 있다.
    - 웹키트(Webkit) : KHTML에서 파생된 레이아웃 엔진으로 사파리 등이 탑재하고 있다.
    - 태즈먼(Tasman) : 마이크로소프트의 레이아웃 엔진으로 맥용 인터넷 익스플로러가 탑재하고 있다.
    - EdgeHTML : 트라이던트에서 파생된 마이크로소프트의 레이아웃 엔진으로 마이크로소프트 엣지 스파르탄(~2019) 버전에 탑재하고 있었으나, 마이크로소프트 엣지 애너하임(2019~)부터는 블링크로 교체되었다.

#### 참고 링크
> [브라우저 엔진 (위키백과)](https://ko.wikipedia.org/wiki/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80_%EC%97%94%EC%A7%84)

> [브라우저 엔진 동작 원리 (블로그)](https://all-young.tistory.com/22)

### css 방법론
1. 아토믹 CSS : 모든 CSS 클래스는 하나의 고유한 CSS 규칙을 가지고 있음.
2. utility-first CSS (tailwind) : 미리 세팅된 유틸리티 클래스를 활용하는 방식으로 HTML 코드 내에서 스타일링 할 수 있음.
* [참고링크 (블로그)](https://velog.io/@gtah2yk/Atomic-CSS-in-JS-%EA%B8%80-%EC%A0%95%EB%A6%AC)
* [tailwind (공식 홈페이지)](https://tailwindcss.com/)
* [tailwind 설명 블로그](https://wonny.space/writing/dev/hello-tailwind-css)

### em과 rem의 차이, 왜 em이 더 다루기 까다로운가?

em과 rem 모두 폰트 사이즈를 기준으로 두나, 기준으로 삼는 대상이 다름.
em은 해당 요소의 부모 요소의 폰트 사이즈를 기준으로 하고, rem의 루트(html)의 폰트 사이즈를 기준으로 함.

기본적으로 폰트 사이즈는 부모로부터 상속받는 속성.

em을 사용 할 경우 해당 부모 요소의 폰트사이즈 변경에 영향을 받게 됨. 부모 요소의 폰트 사이즈가 변할 경우 원하지 않는 방향으로 사이즈가 변경 될 수 있음.

rem은 오로지 루트(html)의 폰트 사이즈만을 바라보기 때문에, 부모나 나의 폰트사이즈의 영향을 받지 않음. 그렇게 때문에 부모나 해당 요소의 폰트사이즈의 영향을 받지 않고 사용 가능.


### px은 Absolut unit인가 아닌가?

[CSS unit - MDN](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units)

[CSS unit 관련 블로그](https://velog.io/@3juhwan/CSS-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9-CSS-Unit)

### containing block이란?
[컨테이닝 블러의 모든 것 (MDN)](https://developer.mozilla.org/ko/docs/Web/CSS/Containing_block)

### BFC

BFC는 Block Formatting Context의 약자

[참고 블로그](https://blueshw.github.io/2020/05/17/know-css-block-formatting-context/)

### float의 문제점을 해결하는 방법
1. 부모 요소도 float으로 띄우기 : 부모까지 float을 적용 할 경우 ㅇ 
2. 마지막 형제로 빈 요소 넣고 clear 속성 적용하기
3. 가상요소선택자(::after)로 clear 속성 적용하기
4. 부모에게 display:flow-root 속성 적용하기

### 접근성을 위한 숨김 콘텐츠 만들기
화면에는 보이지 않지만, 문서의 맥락에 필요한 내용들을 처리. (스크린 리더는 읽을 수 있음)
* 많이 사용하는 클래스 : a11y-hidden(a11y => accessibility 약자), sr-hidden, blind 등

### WAI-ARIA의 사용
aria-hidden="true" : 화면에서는 보여주지만, 스크린리더가 읽어주지 않음

*[상세 내용은 ARIA 문서 참조](https://github.com/frontend-2nd/BareumPark/blob/main/HTML_CSS/ARIA/WAI-ARIA.md)*

---
### 참고링크
> [HTML 공식 명세](https://html.spec.whatwg.org/)

> [CSS ZEN GARDEN](http://www.csszengarden.com/214/)

> [널리(NULI)](https://nuli.navercorp.com/)

> [김원준의 웹폰트 파헤치기](https://www.slideshare.net/wsconf/web-font-wsconfseoul2017-vol2?qid=322a6df5-be93-41ab-ae86-816e01cec9f6&v=&b=&from_search=2)

> [CSS 변수 합성 (Toast UI)](https://ui.toast.com/weekly-pick/ko_20210402)

> [CSS 논리적 속성과 값(블로그, margin-inline, margin-block 관련)](https://wit.nts-corp.com/2019/08/05/5621)