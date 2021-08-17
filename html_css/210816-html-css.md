# html/css 실습

## 네이티브로 초점 받을 수 있는 요소

- href값을 가지고 있는 a, button, input 같은 폼 요소
- img -> map, area 태그를 활용하여 링크 적용 할 수 있음. (즉, 초점 받을 수 있음)
- 혹은 `tabindex` 속성을 사용하여 초점 가져올 수 있음. (`tabindex="0"`)
- 단, `tabindex`는 초점만 가져올뿐, 키보드 이벤트 발생하지 않으므로 자바스크립트로 동적 처리를 해주어야 함.

## 탭 콘텐츠에서, 탭 메뉴명을 어떻게 처리 할 것인가?

1. heading의미를 가진 `h2`를 마크업한 후 숨김콘텐츠 처리하고, `h2` 하단에 `button` 삽입하여 기능적이 부분 추가.
2. `h2`에 포커싱 될 수 있도록 `tabindex = "0"` 처리 가능. 단, `tabindex` 속성을 적용하면 포커싱은 되지만, 키보드 이벤트는 발생하지 않으므로 js로 키 이벤트 발생시켜주어야 함.
3. 혹은, `h2` 태그에 자식으로 `a`태그를 넣고, WAI-ARIA를 활용하여 속성으로 `role="button"` 적용하여 처리 할 수도 있음.
4. 단, heading 태그에 버튼을 포함하는건 추천하는 방향은 아님. heading 태그는 의미적, 버튼은 기능적이므로 의미적인 요소 안에 기능적인 요소가 들어가는 것이 적합하지 않기 때문.

## `time` 태그에 관하여.

`time` 태그로 날짜와 시간 처리가 가능하다.

만약, 날짜가 들어가는 영역에 `span`을 사용하여 작성하면, 기계는 해당 내용을 string으로 받아들인다.

즉, 기계는 해당 텍스트를 날짜 데이터로 인식하지 못하므로 스크립트 단에서 추가 작업 진행해 주어야 함.

`datetime` 속성 : 기계가 인식 할 수 있는 날짜 데이터를 넣어줄 수 있음.

(datetime="year-month-dayThour:minute:seconds")

``` css
datetime="2021-08-16T21:40:50"
```

- 이러한 속성 처리는 스트립트연산에도 유리하다. new Date로 현재시간 받아올 필요 없이 datetime의 값만 읽어오면 되기 때문.

## 더보기 링크 생성시 링크 텍스트는 어떻게 처리?

- 모든 더보기 링크에 단순하게 "더보기"만 넣어주면, 어떤 것을 더 볼 수 있는 링크인지 알 수 없음.
- 연결하고자 하는 콘텐츠에 `id` 생성 후, `a` 태그에 `aria-labelledby` 속성 추가 후 , 속성 값으로 `id` 값을 넣어주면, 해당 `id`가 선언된 콘텐츠와 연결된 링크라는 것을 알려 줄 수
  있음.

## css에서의 !important 사용.

강제적으로 순위를 끌어올려야 할 때 important 사용 가능. (단, 모든 가중치보다 우선되므로 남용 절대 불가)

## 탭 메뉴와 탭 콘텐츠

### 탭 UI 마크업은 어떻게 해야할까?

1. 디자인 중심으로 마크업 할 경우
    - 탭메뉴 1 -> 탭메뉴 2 -> 더보기 링크 -> 목록(탭 콘텐츠)
    - 이런 순서로 마크업 할 경우, 해당 목록이 탭메뉴1에 대한 목록인지, 탭메뉴2에 대한 목록인지 파악이 어려움.

``` html
<ul class="tab-list">
  <li><a href="/">공지사항</a></li>
  <li><a href="/">자료실</a></li>
</ul>
<div class="tab-content">
    <ul class="notice-list">
      <li><a href="#">목록 1</a></li>
      <li><a href="#">목록 2</a></li>
    </ul>
    <ul class="pds-list">
      <li><a href="#">목록 1</a></li>
      <li><a href="#">목록 2</a></li>
    </ul>
    <a href="#" class="more">더보기</a>
</div>
```

2. 순서에 맞게 마크업
    - 탭메뉴 1 -> 탭메뉴 1 목록 -> 탭메뉴 1 더보기 링크 -> 탭메뉴 2 -> 탭메뉴 2 목록 -> 탭메뉴 2 더보기 링크
    - 이때 탭 메뉴를 해당 콘텐츠 블록의 제목으로 제공한다면 콘텐츠 블록에 대한 명확한 범위를 지정할 수 있고 스크린리더 등의 사용자가 헤딩 간 이동 기능을 사용하여 필요한 정보로 건너뛰 기 할 수 있다.

``` html
<div class=“tab-contents”>
     <div id=“notice” class=“on”>
        <h1><a href=“/”>공지사항</a></h1>
         <ul class=“notice-list”>
             <li><a href=“/”>목록 1</li>
             <li><a href=“/”>목록 2</li>
         </ul>
         <a href=“/” class=“more” title=“공지사항”>더보기</a>
     </div>
     <div id=“pds”>
         <h1><a href=“/”>자료실</a></h1>
         <ul class=“pds-list”>
             <li><a href=“/”>목록 1</li>
             <li><a href=“/”>목록 2</li>
         </ul>
         <a href=“/” class=“more” title=“자료실”>더보기</a>
     </div>
 </div>
```

### WAI-ARIA를 사용하여 해결해보자!

탭과 많은 양의 본문으로 구성된 형식의 탭 UI라면 마크업 순서를 조정하는 것이 오히려 접근성과 사용성을 해치는 경우가 될 수도 있다.

이런 문제점을 해결하기 위해서는 마크업 순서의 조정보다 WAI-ARIA에서 제공되는 role(역할)을 활용하는 것이 바람직하다.

- 적용방법
  - 탭 메뉴를 그룹핑 하는 요소에 tablist role 부여
  - 각각의 탭 메뉴 요소에 tab role 부여
  - 각 탭이 컨트롤 하는 탭 섹션의 id 값을 aria-controls 속성 값으로 설정
  - 각 탭 섹션에 tabpanel role 부여
  - 선택된 탭 메뉴에 aria-selected 속성의 값을 true로 설정
  - 나머지 탭 메뉴들은 aria-selected 속성의 값을 false로 설정하거나 aria-selected 속성을 제거

``` html
<div class="tab-interface">
    <!-- 탭 인덱스 -->
    <ul class="tab-list" role="tablist">
        <li id="tab1" role="tab" aria-controls="section1" aria-selected="true" tabindex="0">HTML</li>
        <li id="tab2" role="tab" aria-controls="section2" aria-selected="false" tabindex="0">CSS</li>
        <li id="tab3" role="tab" aria-controls="section3" aria-selected="false" tabindex="0">Javascrip</li>
    </ul>
    <!-- 탭 콘텐츠 -->
    <div class="tab-contents">
        <section id="section1" role="tabpanel" aria-labelledby="tab1">
            <p>
                HTML은 하이퍼텍스트 마크업 언어(HyperText Markup Language)
              라는 의미의 웹 페이지를 위한 마크업 언어이다.
            </p>
            <a href="#">상세 보기</a>
        </section>
        <section id="section2" class="unvisual" role="tabpanel" aria-labelledby="tab2">
            <p>
                캐스케이딩 스타일 시트(Cascading Style Sheets, CSS)는 마크업 언어가
                실제 표시되는 방법을 기술하는 언어로, HTML과 XHTML에 주로 쓰이며,
                XML에서도 사용할 수 있다.
            </p>
            <a href="#">상세 보기</a>
        </section>
        <section id="section3" class="unvisual" role="tabpanel" aria-labelledby="tab3">
            <p>
                자바스크립트(JavaScript)는 객체 기반의 스크립트 프로그래밍 언어이다.
                이 언어는 웹브라우저 내에서 주로 사용하며,
                다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다.
            </p>
            <a href="#">상세 보기</a>
        </section>
    </div>
</div>
<a href="#">copyright</a>
```

#### 참고자료
- [WAI-ARIA 사례집](https://www.wah.or.kr:444/_Upload/pds2/WAI-ARIA%20%EC%82%AC%EB%A1%80%EC%A7%91(%EC%98%A8%EB%9D%BC%EC%9D%B8%ED%8C%90).pdf)
- [사례집 구현 코드(github)](https://github.com/niawa/ARIA)