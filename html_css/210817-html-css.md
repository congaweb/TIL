# html/css 실습

## accordion을 WAI-ARIA로 하면?

accordion header와 accordion panel로 마크업 후 aria 속성 사용하여 각 영역에 의미 부여.

``` html
<div id="accordionGroup" class="Accordion">
    <h3>
      <button aria-expanded="true" class="Accordion-trigger"aria-controls="sect1" id="accordion1id">
        <span class="Accordion-title">
          Perso:nal Information
          <span class="Accordion-icon"></span>
        </span>
      </button>
    </h3>
    <div id="sect1" role="region" aria-labelledby="accordion1id"class="Accordion-panel">
      <div>
        <!-- Variable content within section, may include any type of markup or interactive widgets. -->
        contents
      </div>
    </div>
    <h3>
      <button aria-expanded="true" class="Accordion-trigger"aria-controls="sect2" id="accordion2id">
        <span class="Accordion-title">
          Personal Information
          <span class="Accordion-icon"></span>
        </span>
      </button>
    </h3>
    <div id="sect2" role="region" aria-labelledby="accordion2id"class="Accordion-panel">
      <div>
        <!-- Variable content within section, may include any type of markup or interactive widgets. -->
        contents
      </div>
    </div>
  </div>
</div>
```
* 참고 : [WAI-ARIA practice](https://www.w3.org/TR/wai-aria-practices-1.1/#accordion)
* WAI-ARIA practice 사이트에 툴팁 사용 방법등도 나와있으니 시간날 때 찾아볼 것!

## 시맨틱 태그 != 웹 접근성
웹 접근성을 지킨다는 것이 곧 시맨틱 태그를 사용한다는 뜻은 아님!

둘을 같은 의미로 받아들이면 안됨!

## `figure` 태그

`figure`태그는 자식으로 `img`, `video`, `audio`, `table`과 같은 요소를 가질 수 있다.

또한 `figcaption`을 자식으로 가질 수 있는데, 이 태그는 부모 `figure`요소가 포함하는 다른 콘텐츠에 대한 설명 혹은 범례를 나타낸다.

만약, `figcaption`이 대체 텍스트의 역할을 한다고 생각 될 경우, `alt` 값을 비워놓고, `img`와 `figcaption`을 `id`와 `aria-labelledby`로 연결해도 됨.

단, 이렇게 처리 할 경우 의미적, 웹 접근성적으로는 맞을 수 있으나 seo 측면에서는 적합하지 않을 수 있다. (`alt` 값이 없어 검색되지 않음)

그러므로 `alt`를 쓸 것인지 `ARIA`를 쓸 것인지는 상황에 맞게 판단하여 작업 할 것.

## 인라인 요소는 블럭 요소를 자식으로 가질 수 있다? 없다?

XHTML 1.0과 HTML4.1에서는 인라인 요소의 자식으로 블럭 요소가 올 수 없었다.

하지만 HTML5로 넘어오고 `a`태그가 transparent 모델이 되면서, `a`태그는 인라인 요소임에도 불구하고 블럭 요소를 자식으로 가질 수 있게 됨.

다른 브라우저와 달리 과거 파이어폭스에서 `a`의 자손으로 블럭 요소가 올 경우 포커싱 아웃라인이 이상하게 잡히는 경우가 있었음. 
이처럼 아웃라인이 이상하게 잡혔던 것은 `a`가 인라인 요소였기 때문이므로, `display:block;` 을 통해 해결 가능하다.

## WAI-ARIA 참고용 사이트
항공사 ARIA 적용 사례(대한항공) -> 사이트 들어가서 사례 확인 해 볼 것.
[링크](https://aoa.gitbook.io/skymimo/)

## 라인을 1px보다 얇게 만드는 방법
일단, 파이어폭스를 제외한 대부분의 웹 브러우저 환경에서 1px보다 얇은 디자인을 그리는 것은 현재 불가능함.

왜냐? 픽셀 밀도 때문!

### 픽셀 밀도란?
1인치 영역에 물리적으로 표현 가능한 픽셀 수. 모니터, 스마트폰, 태블릿과 같은 디지털 기기의 화면의 픽셀 밀도는 PPI(인치당 픽셀 수) 단위로 측정.
기기가 지원하는 식펠 농도에 따라 최소 표현 가능한 픽셀 개수가 변경되는데, 1PPI 밀도를 가진 화면에서는 최소 픽셀 개수가 1개.

1px 보다 얇은 선을 화면에서 표현하려면 최소 2PPI 픽셀 농도를 지원하는 디지털 기기여야 함. 즉, 고해상도 디스플레이로 불리는 화면에서나 가능하다는 뜻.

**그럼 0.5px 표현 할 수 있는 방법은??**

### 1. `transform:scale()`의 사용

``` css
.thin-border{
    transform:scaleY(0.5) /* 1px * 0.5 = 0.5px */
}
```

화면의 실제 픽셀은 1px이지만, 스케일을 사용해 가늘게 표시하는 일종의 트릭.

**장점**은 쉽다!

**단점**은 라인을 표시하기 위하여 불필요한 요소를 추가해야 한다는 것! (라인용 마크업이 추가 됨)

이를 **보완**하기 위해, 표현(presentation)임을 `role="presentation"` 사용하여 명시. 혹은 의미를 가지지 않는 가상 요소를 사용하여 표현할 것.

### 2. Opacity(불투명도)의 활용

``` css
.this-border{
    opacity:0.5;
}
```

css의 불투명도를 활용한 방법으로, "색체 원근법"으로 착시 현상을 일으키는 것.

화면의 실제 픽셀은 1px이지만, 스케일을 사용해 가늘게 표시하는 일종의 트릭.

**장점**은 쉽다!

**단점**은 라인을 표시하기 위하여 불필요한 요소를 추가해야 한다는 것! (라인용 마크업이 추가 됨) 실제 크기는 변하지 않고, 단지 반투명하게 해서 착시를 이용 할 뿐!

이를 **보완**하기 위해, 표현(presentation)임을 `role="presentation"` 사용하여 명시. 혹은 의미를 가지지 않는 가상 요소를 사용하여 표현할 것.


### 3. 선형 그레디언트(Linear Gradients)

css 선형 그레디언트를 배경 이미지로 활용 한 방법.

``` css
.thin-border {
  border-bottom: 0;
  height: 1px;
  background: linear-gradient(to bottom, transparent 50%, currentColor 50%);
}
```

**장점**은 화면에 그려진 실제 결과가 0.5px!

**단점**은 라인을 표시하기 위하여 불필요한 요소를 추가해야 한다는 것! 비교적 문법이 복잡하여 사용이 쉽지 않음!

이를 **보완**하기 위해, 표현(presentation)임을 `role="presentation"` 사용하여 명시. 혹은 의미를 가지지 않는 가상 요소를 사용하여 표현할 것.

### 4. 박스 그림자(Box Shadow)

css `box-shadow` 속성을 사용한 방법. 그림자의 위치, 블러, 확상, 색상 등의 속성을 조절하여 1px 보다 얇은 선을 화면에 그려 낼 수 있음.

``` css
.thin-border-box {
  box-shadow: 0 0.5px #000;
}
```

**장점**은 사용법이 쉽고, 화면에 그려진 실제 결과가 0.5px!

**단점**은 박스 크기 만큼 라인이 그려지므로 박스 크기와 다른 크기로 조정이 어려움!(단, 박스 자체에 그림자를 적용했을 경우에만 해당)


### 5. 보더 이미지(Border Image)
실제 디자이너가 그린 가는 선을 svg 포맷으로 이미지 저장하여 사용.

``` css
.thin-border{
    border-bottom-color:transparent;
    border-image:url("이미지 경로") 0.5;
}
```

**장점**은 화면에 그려진 실제 결과물이 0.5px!

**단점**은 코드와 별개로 이미지 필요, 보더 이미지 분법이 복잡, 선을 그리기위한 불필요한 마크업의 추가

이를 **보완**하기 위해, 표현(presentation)임을 `role="presentation"` 사용하여 명시. 혹은 의미를 가지지 않는 가상 요소를 사용하여 표현할 것. 

* 출처 : [이듬 브런치](https://brunch.co.kr/@euid/6)


## 라인을 그리기 위해 `hr` 태그를 사용한다?
`<hr>` 요소는 이야기 장면 전환, 구획 내 주제 변경 등, 문단 레벨 요소에서 주제의 분리를 나타냄.

즉, 의미를 가지고 있는 태그임!

그러므로, `hr` 태그를 단순히 장식용 라인으로 사용하면 안 됨.

장식용 라인은 `border` 속성 혹은 가상 요소를 사용하여 작업 할 것.

## `display:flex; flex-direction:column`을 사용하여 콘텐츠 수평 배치?
flex-box에 `height`를 강제 지정하여 수평 배치는 가능하나, 콘텐츠가 지정한 `heigth` 보다 많아질 경우 레이아웃이 틀어짐

다양한 접근 방식의 하나로 참고 할 것!

## 이전, 다음 버튼 디자인은 어떻게 구현?

흔히, 캐러셀 혹은 슬라이드에 많이 사용하는 텍스트는 없고 화살표 이미지만 있는 좌,우 이동 버튼은 어떻게 구현할까?

### 1. 제일 쉬운건 `aria-label`을 사용하는 것!

콘텐츠를 숨김처리 하지 않아도 되고, 보조기기도 읽을 수 있어 접근성도 보장되는 가장 간단한 방법!

단, 배경이미지를 불러오지 못하는 상황에서 화면에 버튼이 제대로 표현되지 않는다는 단점이 있음.

### 2. `button`안에 텍스트 노드를 넣고, 이 텍스트를 안보이게 해보자.
`button`의 높이 값 만큼 `padding-top`을 주어 텍스트를 바깥으로 밀고 `overflow:hidden`처리하면 됨.

단, `button`의 경우 `button`에 직접 `height`도 주고 `padding-top`도 주면 브라우저가 생각하지 못한 방향으로 렌더링해줌.

브라우저 마음대로 `button`의 높이값을 보존하기 때문!

이를 **해결**하기 위해서는, `button`을 감싸는 부모를 만들어서 부모에게 `height`를 주고 `overflow:hidden;` 속성을 주면 됨. **이때 button은 높이값은 0!**

### button 텍스트를 숨기는 다른 트릭은? `text-indent`를 사용해보자!

``` css
button{
    text-indent: -999px;
    white-space: nowrap;
    overflow: hidden;
}
```
### button 텍스트를 숨기는 다른 트릭은? `absolute`를 사용해보자!

``` html
<a href="#">
    <span class="bg"></span>
    <span class="text"></span>
</a>
```
이렇게 마크업 하고,

``` css
a{
    position:relative;
}
.bg{
    position:absolute;
    top:0;
    left:0;
    background-image:url(이미지 경로);
}
```
이런식으로, `span.bg`를 띄워서 `span.text`를 덮어 놓을 수 있음.
이렇게 할 경우, `background-image`를 못 불러오는 경우에는 하단에 있던 text가 노출 됨!

단, 좌,우 버튼과 같이 버튼 크기가 너무 작을 경우는 이런식으로 대체 텍스트를 노출하기 어려움! (텍스트가 들어갈만한 너비가 안나오니까..)

## `background-image`를 sprite 이미지로 만드는 이유는?

백그라운드에 사용되는 이미지를 모두 조각 낼 경우, 서버에 이미지 요청하는 횟수가 그만큼 늘어나기 때문에 성능저하가 올 수 있음.

하여, 아이콘과 같이 백그라운드로 사용되는 이미지를 하나의 이미지로 만드는 sprite 이미지 기법이 사용 됨.

[참고링크](https://eh-together.tistory.com/1)


### css layout pattern 참고용 링크는 아래 링크 확인! 
[css layout pattern](https://csslayout.io/patterns/)