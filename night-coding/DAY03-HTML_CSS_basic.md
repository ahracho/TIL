# 코딩야학 3일차 : HTML과 CSS 기본

## HTML 이론
### HTML은 무엇인가?
- __HyperText__ : 문서와 문서가 링크로 연결되어 있는 시스템 - HTML에서 가장 중요한 특성(본질)은 링크라는 것, 결국 HTML 문서들이 링크처럼 얽히고 설켜 거대한 웹을 구성하게 되는 것.
- __Markup Language__ : HTML은 사람도 이해하고 웹브라우저도 이해하는 언어이다. 그럼 마크업은 무엇인가? 태그를 통해서 속성을 표시하는 형식

~~~html
<!--  strong은 강조 표시를 나타내는 TAG -->
안녕하세요, <strong> 생활코딩 </strong> 입니다.
~~~

### HTML의 속성
- __a 태그__ : 링크를 나타내는 태그
1. href 속성 : a만으로는 설명이 부족해 그냥 링크라는 것만 알려줄 뿐, 어디에 어떻게 가리켜야 하는지는 알려주지 않아. href 속성이 필요함.  
~~~ html
<!-- 생활코딩를 링크로 표시해야 한다는 것을 a 태그가 알려주고, 링크가 어디를 가리켜야 하는지는 href 속성이 알려준다-->
<a href="https://opentutorials.org/course/1"> 생활코딩 </a>
~~~  

2. target 속성 : 링크를 열 때 새로운 창에 열리도록 하고 싶어. _blank(새창), _parent, _self(현재 창), _top 등이 있음. 
~~~ html
<a href="https://opentutorials.org/course/1" target="_blank"> 생활코딩 </a>
~~~

### 태그의 중첩
- li 태그 : 리스트. 리스트로 나타낼 내용 각각 앞에 li 태그 붙이면 된다.
~~~html
<li> html </li>
<li> css </li>
<li> JaveScript </li>
~~~ 

- ul 태그 : Unordered List. 리스트 간의 구분을 하고 싶을 때 각 그룹을 감싸는 태그.
~~~html
<!-- ul 태그는 점으로 표시 -->
<ul>
  <li> html </li>
  <li> css </li>
  <li> JaveScript </li>
</ul>

<!-- ol 태그는 숫자로 표시-->
<ol>
  <li> 사과 </li>
  <li> 딸기 </li>
  <li> 참외 </li>
</ol>
~~~ 

ul / ol - li 태그처럼 태그 간에도 포함관계가 있어서 누가 누굴 감싸면 특정 기능을 하게 할 수 있어. body, head 태그 등과도 마찬가지.

~~~<!DOCTYPE html>
<html> <!-- 이 태그 아래에 있는 것들이 HTML 문서임을 알려주는 역할-->
  <head>
    <meta charset="utf-8">
    <title>생활코딩</title> <!-- 창에 보이는 제목 -->
  </head>
  <body>
    <!-- 필요한 문서 내용은 여기에 작성하는 것--> 
  </body>
</html>
~~~

### HTML 정리
~~~html 
<!DOCTYPE html>
<html>

</html>
~~~

__DOCTYPE__은 해당 문서를 어떤 표준에 따라서 해석할지를 웹브라우저에 알려주는 역할을 한다. 위의 DOCTYPE은 HTML5 표준을 따른다는 의미.

주로 사용하는 태그는 종류가 많지 않지만 상황에 따라서 어떤 태그를 사용해야 할지 모르겠으면 검색하면서 사용하면 돼! 처음부터 모든 태그를 알 수도 없고, 알 필요도 없다.

__끝으로, HTML의 본질은 표시할 정보를 전달한다는 것이다__

### Semantic Web : 의미가 잘 드러나는 웹
정보의 의미가 잘 드러날 수 있도록 하는 태그로 작성된 웹페이지  
사람에게도 의미가 전달되고, 브라우저에게도 의미가 전달되도록 태그를 잘 설정하는 것이 필요

- 실습에서 작성된 기존 코드
~~~<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <header> <!-- 전체 페이지의 제목이라는 걸 나타냄 -->
    <h1>Java Script</h1>
  </header>
  <nav> <!-- 이 안에 있는 내용이 내비게이트 역할을 한다는 것을 나타내, 기능은 없고, 의미만 드러내는 역할을 한다 -->
    <ol>
      <li> Java Script란? </li>
      <li> 변수와 상수 </li>
      <li> 연산자 </li>
    </ol>
  </nav>
  <article> <!-- 페이지의 본문을 나타냄 -->
    <h2> 변수와 상수 </h2> 
    변수란
    <ul>
      <li> 변하는 값 </li>
    </ul>
  </article>
</body>
</html>
~~~ 

### 사이트 완성
- 대문 페이지 : 보통 index.html이라는 파일이 대문 페이지로 사용된다. 암묵적 약속으로, 홈페이지 주소를 치면 웹서버는 가장 먼저 index.html 파일을 찾게 된다.

~~~<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <header> <!-- 전체 페이지의 제목이라는 걸 나타냄 -->
    <h1> <a href="http://localhost/"> Java Script </a> </h1> <!-- 제목을 누르면 첫 페이지로 돌아가도록 링크 삽입-->
  </header>
  <nav> <!-- 이 안에 있는 내용이 내비게이트 역할을 한다는 것을 나타내, 기능은 없고, 의미만 드러내는 역할을 한다 -->
    <ol>
      <li> <a href="http://localhost/page_html.html"> Java Script란? </a> </li>
      <li> <a href="http://localhost/page_vc.html"> 변수와 상수 </a> </li>
      <li> <a href="http://localhost/page_op.html"> 연산자 </a> </li>
    </ol>
  </nav>
  <article>
    여기에 각 페이지마다 달라야 하는 내용을 작성하면 링크를 눌렀을 때 내용이 변하게 된다.
  </article>
</body>
</html>
~~~ 

만약에 목록에 페이지가 하나 추가되면 각 페이지에 모든 소스를 고쳐야해. 너무 비효율적인데, 어떻게 해야할까? 초기 웹에서 이런 문제에 맞닥뜨리고 해결하면서 웹기술이 발전하게 되었다.  
- 클라이언트 : HTML, CSS(디자인 측면), JS
- 서버 : PHP, MySQL