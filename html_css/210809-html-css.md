# HTML_CSS 1회차

## WWW (World Wide Web)
웹의 아버지 : Tim Berners-Lee

## 웹의 분류
### BACK-END
Server, Database, Application

### FRONT-END
Client, Web Browser, Presentation Layer

## FRONT-END에서 사용하는 언어
HTML - 건강한 신체

CSS - 근사한 스타일링

Javascript - 스마트한 두뇌

## 프레임워크와 라이브러리의 차이는?
react.js는 프레임워크인가 라이브러리인가?라는 질문으로 귀결 될 수 있음.
#### 공통점 : 다른 누군가가 쓴 코드를 우리의 프로젝트를 위해 가져다 쓰는 것.


#### 차이점 : 누가 누구를 컨트롤 하는가?
내가 코드를 컨트롤 하는가 VS 누군가의 규칙을 따라 코딩하는가
* 라이브러리 (ex: jQuery) : 내가 필요 할 때 불러서 사용(제이쿼리를 부르는 것과 같이) . 자유롭게 다른 라이브러리로 대체 가능. 라이브러리를 바꿈으로써 프로젝트에 큰 문제가 생기지 않음.


* 프레임워크 (ex:django) : 내가 필요할 때 부르는 것이 아님. 프레임워크로 작업 시 프레임워크의 규칙을 따라야 함. 작업자가 컨트롤 하지 않고, 정해진 규칙을 따라 코딩 함. 

** [참고영상](https://www.youtube.com/watch?v=t9ccIykXTCM)

## 웹 표준
웹 표준은 누가 만드는가?
원래는 W3C(Word Wide Web Consortiums)에서 만들어 왔음.
W3C에서 표준을 만들면 밴더(브라우저)에서 적용하는 방식

그러나 현재는, 밴더가 표준이 아닌 것을 만들고 W3C가 표준으로 만드는 방식으로 변화 됨.

## 웹 접근성
보편성 - 누구나 접근할 수 있어야 한다. (장애인 혹은 고령자가 웹 사이트에서 제공하는 정보를 비장애인과 동등하게 접근하고 이용 할 수 있어야 한다.)

#### 장애에 대한 이해 필요
- 시각 장애 - 전맹, 저시력
- 청각 장애
- 지체 장애 - 절단 및 지체기능 장애
- 뇌병변 장애

웹 점근성 준수 고려사항
1. 시각
2. 이동성
3. 청각
4. 인지


#### 환경에 대한 이해 필요
- 다양한  Platform
- Cross Browsing
- SEO(Search Engine Optimization)
- 저사양 또는 저속회선

## HTML의 탄생
- 현재 표준: XHTML1.0, HTML4.01, HTML5(가장 최신의 표준)

### HTML4.01, XHTML1.0과 HTML5의 차이점
- 새롭게 등장한 콘텐츠 모델(Content Models) : 명확한 정보 구조 설계 및 구성을 위해 카테고리를 정의하여 각 요소별로 비슷한 성격을 가지고 있는 것끼리 그룹화
- 콘텐츠 모델의 카테고리 : Sectioning Root, Metadata Content, Flow Content, Sectioning Content, Heading Content, Phrasing Content, Embedded Content, Interactive Content, Palpable Content, Script-supporting Elements, Transparent Contnt 등..

-> 하나의 요소가 여러 그룹해 속해 있을 수도, 그러지 않을수도 있음.

### 아웃라인 알고리즘
- HTML5에서는 정보 구조를 명확히 할 수 있도록 '아웃라인 알고리즘(Outline Algorithm)' 개념 도입
- 웹 페이지의 정보 구조를 판별 할 수 있는 개념으로 책 목차와 비슷
- 직접적으로 아웃라인을 구성하는 요소에는 헤딩 콘텐츠, 섹셔닝 콘텐츠, 섹셔닝 루트 요소등이 있음.

### HTML5의 API
- HTML5의 커다란 변화 중 하나로는 다양한 API(Application Programming Interface)의 추가를 들 수 있음.
- Web Storage, Application Cache, File API 등등..

### HTML5의 서식
HTML5는 HTML4.01이나 XHTML1.0 문법을 모두 허용하기 때문에 기존에 사용하던 마크업 문법을 그대로 사용 할 수 있음.
