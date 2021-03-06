- - -

# BeautifulSoup

### A Short Introduction

* * *

**박 진 수** 교수  
Intelligent Data Semantics Lab  
Seoul National University

- - -

<h3>Table of Contents<span class="tocSkip"></span></h3>
<div class="toc"><ul class="toc-item"><li><span><a href="#HTML" data-toc-modified-id="HTML-1">HTML</a></span></li><li><span><a href="#기초" data-toc-modified-id="기초-2">기초</a></span></li><li><span><a href="#속성" data-toc-modified-id="속성-3">속성</a></span></li><li><span><a href="#열람" data-toc-modified-id="열람-4">열람</a></span><ul class="toc-item"><li><span><a href="#contents" data-toc-modified-id="contents-4.1">contents</a></span></li><li><span><a href="#children" data-toc-modified-id="children-4.2">children</a></span></li><li><span><a href="#descendants" data-toc-modified-id="descendants-4.3">descendants</a></span></li></ul></li><li><span><a href="#검색" data-toc-modified-id="검색-5">검색</a></span></li><li><span><a href="#텍스트-처리" data-toc-modified-id="텍스트-처리-6">텍스트 처리</a></span><ul class="toc-item"><li><span><a href="#get_text()" data-toc-modified-id="get_text()-6.1">get_text()</a></span></li><li><span><a href="#get_text(),-strings,-stripped_strings의-단순-비교" data-toc-modified-id="get_text(),-strings,-stripped_strings의-단순-비교-6.2">get_text(), strings, stripped_strings의 단순 비교</a></span></li></ul></li><li><span><a href="#웹에-접근하기" data-toc-modified-id="웹에-접근하기-7">웹에 접근하기</a></span><ul class="toc-item"><li><span><a href="#urllib" data-toc-modified-id="urllib-7.1">urllib</a></span></li><li><span><a href="#BeautifulSoup" data-toc-modified-id="BeautifulSoup-7.2">BeautifulSoup</a></span></li></ul></li></ul></div>

# HTML

**HTML(HyperText Markup Language)** 란?
- 웹 페이지 제작을 위한 마크업 언어다.
  + 마크업 언어(Markup Language): 태그, 속성 등을 이용하여 문서나 데이터의 구조를 정의하고 표현하는 언어를 말한다.
- 제목, 단락, 목록 등과 같은 본문을 위한 구조적 의미를 표현할 수 있을 뿐만 아니라, 링크나 인용 그리고 그 밖의 항목으로 구조적 문서를 만들 수 있는 방법을 제공한다.
- HTM 문서는 꺾쇠 괄호(**< >**)에 둘러싸인 '태그(tag)'를 사용하여 작성한다.

```html
<title>Welcome to HTML World!</title>
<p>Hi BeautifulSoup</p>
```

- 자세한 내용은 아래 URL을 참고한다.
  + https://en.wikipedia.org/wiki/HTML


**HTML의 기본 구성 요소**
1. **태그(tag)** : 요소를 구분할 수 있도록 하는 이름표를 말한다. 
  + 일반적으로 시작 태그(`<tag>`)와 종료 태그(`</tag>`) 한 쌍으로 구성된다.
1. **속성(attribute)=속성값(value)** : 태그들에 특성을 부여하기 위해 사용되는 요소다.
1. **내용(contents)** : 화면에 표시되는 정보(텍스트, 그림 등)다.
  + 웹 스크레이핑(크롤링)을 할 때 데이터 수집가들의 관심 대상이다.

```html
<tag attribute1='value1', attribute2='value2, ...>contents</tag>
```
```html
<태그이름 속성이름1='속성값', 속성이름2='속성값, ...>내용</태그이름>
```

**HTML 마크업 요소의 형태**
- 구조적 마크업 : 본문에 있는 내용물의 목적을 표현한다.
  + 제목(`<title>`), 문단(`<p>`), 표(`<table>`) 등
- 표현적 마크업 : 기능에 관계없이 본문의 외관(look)을 표현한다.
  + 굵게(`<b>`), 이탤릭(`<i>`) 등
- 하이퍼텍스트 마크업 : 다른 문서와 연결시켜주는 문서의 부분을 말한다.
  + 링크(`<a>`)
  
  ```html
  <a href='https://ko.Wikipedia.org/'>한국어 위키백과</a>
  ```

**자주 사용하는 HTML 태그(요소)**

 | 태그 | 기능 | 비고 |
 | - |:-  |:- |
 | `<h>` | 제목 | `<h1>`, `<h2>`, `<h3>`, ... 등으로 표현한다. |
 | `<p></p>` | 단락 | |
 | `<br/>` | 줄바꾸기 | 빈 태그(끝 태그가 없다.) |
 | `<table>` | 표 | |
 | `<tr>` | 행 | `<table>...</table>` 태그 안에 넣는다. |
 | `<td>` | 열 | `<tr>...</tr>` 태그 안에 넣는다. |
 | `<ul><li>...<li></ul>` | 순서 없는 목록 | 기본은 까만 동그라미다.|
 | `<ol><li>...<li></ol>` | 순서 있는 목록 | 기본은 숫자다.|
 | `<font`> | 폰트 지정 | |
 | `<center>` | 가운데 정렬 | |



**속성**
- 시작 태그 내에서 태그의 이름 다음에 작성한다.
- 대부분의 태그(요소) 속성들은 **속성이름='속성값'** 의 형태를 가진다.

**<center>일반적으로 자주 사용하는 속성</center>**

 | 속성 이름 | 기능 |
 | - |:-  |
 | **id** | 태그(요소)에 대한 문서 전체의 고유 식별자를 제공한다. | 
 | **class** | 유사한 태그(요소)를 분류하는 방법을 제공한다. |
 | **style** | 특정 태그(요소)에 표현적 속성을 제공한다. |
 | **title** | 태그(요소)에서 숨겨진 뜻을 설명하는 글을 첨부한다. 주로 마우스가 태그(요소) 내용 위로 이동할 때 툴팁(tooltip) 텍스트로 사용된다. |


```html
<p class='main' id='myHead'><abbr style='color:royalblue;' title='World Health Organization'>WHO</abbr> was founded in 1948.</p>
```

다음 HTML 문서와 동일한 문서를 작성하여 현재 작업 폴더의 하위 폴더인 'data'에 web_page.html'로 저장한다.


```html
%%writefile data/web_page.html
<!DOCTYPE html>
<html>
<head><title>A Simple Local Web Page</title></head>

<body>
  <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
  <h2>The second heading</h2>
    <p class='simple paragraph' id='para'>Paragraph #1 under <b>the second heading</b>.</p>
    <p class='simple paragraph'>Paragraph #2 under <u>the second heading</u>.</p>
    <div>
      <p class='div first-link' id='link'>This is a link to <a href='http://biz.snu.ac.kr' id='snubiz'>Business School at SNU</a>.</p> 
      <p class='div second-link' id='link'>We also want to visit <a href='https://www.python.org' id='python'>Python Official Web Page</a>.</p> 
    </div>
</body>
</html>
```


# 기초


```python
# 관련 모듈을 설치한다.
!python -m pip install bs4

# 또는
# !pip install bs4
```


```python
from bs4 import BeautifulSoup
```


```python
# BeautifulSoup 클래스를 사용하여 웹 페이지 객체를 생성한다.
# 이 때 파서를 'html.parser'로 설정한다.
bs = BeautifulSoup(__TODO__)

# 생성한 웹 페이지를 출력한다.
print(bs)
```

**실행 결과**
```
<!DOCTYPE html>

<html>
<head><title>A Simple Local Web Page</title></head>
<body>
<h1>The First Heading</h1>
<p>Paragraph under the first heading.</p>
<h2>The second heading</h2>
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
</body>
</html>
```


```python
# prettify() 메소드를 사용하면 웹 페이지가 태그의 깊이에 따라 들여쓰기가 되어 출력할 수 있다.
print(__TODO__)
```

**실행 결과**
```
<!DOCTYPE html>
<html>
 <head>
  <title>
   A Simple Local Web Page
  </title>
 </head>
 <body>
  <h1>
   The First Heading
  </h1>
  <p>
   Paragraph under the first heading.
  </p>
  <h2>
   The second heading
  </h2>
  <p class="simple paragraph" id="para">
   Paragraph #1 under
   <b>
    the second heading
   </b>
   .
  </p>
  <p class="simple paragraph">
   Paragraph #2 under
   <u>
    the second heading
   </u>
   .
  </p>
  <div>
   <p class="div first-link" id="link">
    This is a link to
    <a href="http://biz.snu.ac.kr" id="snubiz">
     Business School at SNU
    </a>
    .
   </p>
   <p class="div second-link" id="link">
    We also want to visit
    <a href="https://www.python.org" id="python">
     Python Official Web Page
    </a>
    .
   </p>
  </div>
 </body>
</html>
```

# 속성

태그 이름으로 HTML 문서를 탐색할 수 있다.


```python
# 태그 html의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<html>
<head><title>A Simple Local Web Page</title></head>
<body>
<h1>The First Heading</h1>
<p>Paragraph under the first heading.</p>
<h2>The second heading</h2>
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
</body>
</html>
```


```python
# 태그 head의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<head><title>A Simple Local Web Page</title></head>
```


```python
# 태그 title의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<title>A Simple Local Web Page</title>
```


```python
# 태그 body의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<body>
<h1>The First Heading</h1>
<p>Paragraph under the first heading.</p>
<h2>The second heading</h2>
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
</body>
```


```python
# 태그 h1의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<h1>The First Heading</h1>
```


```python
# 태그 h2의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<h2>The second heading</h2>
```


```python
# 태그 p의 내용을 확인한다.
__TODO__ 
```

**실행 결과**
```
<p>Paragraph under the first heading.</p>
```


```python
# find() 메소드로 태그 p가 있는 문서를 검색한다.
__TODO__
```




    <p>Paragraph under the first heading.</p>



**실행 결과**
```
<p>Paragraph under the first heading.</p>
```


```python
# 문서에서 모든 태그 p를 검색한다.
# 반환한 객체의 자료형은?
__TODO__
```

**실행 결과**
```
?
```


```python
#  url을 포함하는 태그 ???의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>
```


```python
# 문서에서 url을 포함하는 태그를 모두 검색한다.
__TODO__
```

**실행 결과**
```
[<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>,
 <a href="https://www.python.org" id="python">Python Official Web Page</a>]
```


```python
# 태그 a가 포함하고 있는 텍스트 내용을 추출한다.
__TODO__
```

**실행 결과**
<pre>
'Business School at SNU'
</pre>


```python
# 태그 div의 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
```


```python
# string 속성을 사용하여 태그 div가 포함하고 있는 텍스트 내용을 추출한다.
# <div> 내에 다른 태그가 있기 때문에 아무 것도 반환하지 않는다.
__TODO__
```

**실행 결과**
<pre>
?
</pre>

# 열람

## contents

태그 하위항목(children)
- 태그에는 문자열과 다른 태그가 포함될 수 있으며 이러한 요소를 태그의 하위항목(children)이라고 한다.

**.contents** 
- 태그 내의 내용을 **리스트**로 반환한다.
- 문자열은 **contents**를 사용할 수 없는데 그 이유는 문자열 내에 다른 어떤 것도 담을 수 없기 때문이다.

**.children**
- 태그의 내용을 리스트로 가져오는 것이 아니라 태그의 직접적인 하위항목을 순회하는 제너레이터(generator)다.

**.descendants** 
- 태그의 모든 하위항목을 순차적으로 순회하는 제너레이터(generator)다.

참고
- **contents**와 **children** 속성은 태그의 직접적인 하위항목만을 대상으로 함
- e.g., **< head >** 태그는 **< title >** 태그 하나만 직접적인 하위항목으로 가짐  


```python
bs.head
```




    <head><title>A Simple Local Web Page</title></head>




```python
# 태그 head가 담고 있는 내용(contents)을 열람한다.
# 반환하는 객체의 자료형은?
bs.head.__TODO__
```

**실행 결과**
```
?
```


```python
# 태그 head가 담고 있는 내용 중 첫 번째 값을 열람한다.
# 반환하는 객체의 자료형은?
bs.head.__TODO__
```

**실행 결과**
```
<title>A Simple Local Web Page</title>
```


```python
bs.title # same as bs.head.contents[0]
```




    <title>A Simple Local Web Page</title>




```python
# 태그 title이 담고 있는 내용(contents)을 열람한다.
__TODO__
```

**실행 결과**
```
['A Simple Local Web Page']
```


```python
# 태그 title이 담고 있는 내용 중 첫 번째 값을 열람한다.
__TODO__
```

**실행 결과**
```
'A Simple Local Web Page'
```


```python
# 태그 title의 첫 번째 값이 담고 있는 내용(contents)을 열람한다.
__TODO__
```

**실행 결과**
<pre>
?
</pre>


```python
# 태그 body가 담고 있는 내용(contents)을 열람한다.
# 반환하는 객체의 자료형은?
bs.body.__TODO__
```

**실행 결과**
```
['\n',
 <h1>The First Heading</h1>,
 '\n',
 <p>Paragraph under the first heading.</p>,
 '\n',
 <h2>The second heading</h2>,
 '\n',
 <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
 '\n',
 <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
 '\n',
 <div>
 <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
 <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
 </div>,
 '\n']
```


```python
# 태그 body가 담고 있는 내용(contents) 중 마지막 두 값을 열람한다.
__TODO__
```

**실행 결과**
```
[<div>
 <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
 <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
 </div>,
 '\n']
```


```python
# for문을 사용하여 태그 body가 담고 있는 모든 내용(contents)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for content in __TODO__:
   print(repr(content))
```

**실행 결과**
```
'\n'
<h1>The First Heading</h1>
'\n'
<p>Paragraph under the first heading.</p>
'\n'
<h2>The second heading</h2>
'\n'
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
'\n'
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
'\n'
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
'\n'
```

## children


```python
# 태그 body가 담고 있는 하위항목(children)을 열람한다.
# 반환하는 객체의 자료형은?
__TODO__
```

**실행 결과**
```
?
```


```python
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for child in __TODO__:
     print(repr(child))
```

**실행 결과**
```
'\n'
<h1>The First Heading</h1>
'\n'
<p>Paragraph under the first heading.</p>
'\n'
<h2>The second heading</h2>
'\n'
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
'\n'
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
'\n'
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
'\n'
```


```python
# 태그 body가 담고 있는 하위항목(children)을 리스트로 가져온다.
# 즉, bs.body.contents와 같은 결과가 나도록 한다.
__TODO__
```

**실행 결과**
```
['\n',
 <h1>The First Heading</h1>,
 '\n',
 <p>Paragraph under the first heading.</p>,
 '\n',
 <h2>The second heading</h2>,
 '\n',
 <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
 '\n',
 <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
 '\n',
 <div>
 <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
 <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
 </div>,
 '\n']
```

## descendants


```python
# 태그 body의 내용을 확인한다.
bs.body
```




    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>




```python
# 태그 body가 담고 있는 내용(contents)을 열람한다.
bs.body.contents
```




    ['\n',
     <h1>The First Heading</h1>,
     '\n',
     <p>Paragraph under the first heading.</p>,
     '\n',
     <h2>The second heading</h2>,
     '\n',
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     '\n',
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     '\n',
     <div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>,
     '\n']




```python
# --- traversing .children
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for child in bs.body.children:
     print(repr(child))
```

    '\n'
    <h1>The First Heading</h1>
    '\n'
    <p>Paragraph under the first heading.</p>
    '\n'
    <h2>The second heading</h2>
    '\n'
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    '\n'
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    '\n'
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    '\n'



```python
# 태그 body가 담고 있는 하위항목(children)과 
# 그 하위항목의 모든 하위항목(descendants)을 열람한다.
# 반환하는 객체의 자료형은?
__TODO__
```

**실행 결과**
```
?
```


```python
# --- traversing .descendants
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)과 
# 그 하위항목의 모든 하위항목(descendants)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for content in __TODO__:
    print(repr(content))
```

**실행 결과**
```
'\n'
<h1>The First Heading</h1>
'The First Heading'
'\n'
<p>Paragraph under the first heading.</p>
'Paragraph under the first heading.'
'\n'
<h2>The second heading</h2>
'The second heading'
'\n'
<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
'Paragraph #1 under '
<b>the second heading</b>
'the second heading'
'.'
'\n'
<p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
'Paragraph #2 under '
<u>the second heading</u>
'the second heading'
'.'
'\n'
<div>
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
</div>
'\n'
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
'This is a link to '
<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>
'Business School at SNU'
'.'
'\n'
<p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
'We also want to visit '
<a href="https://www.python.org" id="python">Python Official Web Page</a>
'Python Official Web Page'
'.'
'\n'
'\n'
```

# 검색

아래 두 메소드는 태그를 검색한다. 태그 내 텍스트의 내용은 검색하지 않는다.

[find](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find) 
- **find**(*name, attrs, recursive, string, **kwargs*)

[find_all](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find-all)
- **find_all**(*name, attrs, recursive, string, limit, **kwargs*)


```python
# 문서에서 첫 번째 나타나는 태그 p를 검색한다.
# 찾는 태그 <p> 중 첫 번째 태그를 반환한다.
__TODO__
```

**실행 결과**
```
<p>Paragraph under the first heading.</p>
```


```python
# 문서에서 모든 태그 p를 검색한다.
# 반환한 객체의 자료형은?
__TODO__
```

**실행 결과**
```
?
```


```python
# 문서에서 찾는 태그 p 중 첫 번째 태그 내용을 확인한다.
__TODO__
```

**실행 결과**
```
<p>Paragraph under the first heading.</p>
```


```python
# 문서에서 찾는 태그 p 중에 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
bs.find_all(__TODO__)
```

**실행 결과**
```
[<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
 <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]
```


```python
# 태그 이름 없이 속성 이름만으로도 찾을 수 있다.
# 문서에서 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
bs.find_all(__TODO__)
```

**실행 결과**
```
[<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
 <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]
```


```python
# 문서에서 속성 id의 값이 'link'인 태그의 내용을 모두 검색한다.
bs.find_all(__TODO__)
```

**실행 결과**
```
[<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>,
 <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>]
```


```python
# 문서에서 속성 id의 값이 'link' 중 첫 번째 태그의 내용을 검색한다.
__TODO__
```

**실행 결과**
```
<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
```


```python
# 문서에서 모든 태그 a를 검색한다. 
bs.find_all(__TODO__)
```

**실행 결과**
```
[<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>,
 <a href="https://www.python.org" id="python">Python Official Web Page</a>]
```


```python
# 문서에서 모든 태그 div를 검색한다. 
bs.find_all(__TODO__)
```

**실행 결과**
```
[<div>
 <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
 <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
 </div>]
```

# 텍스트 처리

**get_text()** 
- 문서 또는 태그 내의 모든 텍스트를 하나의 유니코드 문자열(single Unicode string)로 반환한다.

**get_text(strip=True)** 
- 각 텍스트의 시작과 끝에서 화이트스페이스를 제거한다.

**get_text('separator')** 
- 각 텍스트를 결합하는데 사용할 문자열을 설정한다.

**strings** 
- 모든 문자열을 순회하는 제너레이터(generator)다.

**stripped_strings** 
- 전체가 화이트스페이스인 문자열이나 문자열의 처음과 끝의 화이트스페이스를 제거하는 제너레이터(generator)다.

## get_text()


```python
bs
```




    <!DOCTYPE html>
    
    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>




```python
# 문서(bs)에서 모든 태그를 제거한 텍스트만 가져온다.
# 반환한 객체의 자료형은?
__TODO__
```

**실행 결과**
```
?
```


```python
# 태그 title을 찾아 모든 태그를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'A Simple Local Web Page'
```


```python
# 태그 head을 찾아 모든 태그를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'A Simple Local Web Page'
```


```python
# 태그 h1을 찾아 모든 태그를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'The First Heading'
```


```python
# 태그 div를 찾아 모든 태그를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n'
```


```python
# 태그 body를 찾아 모든 태그를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'\nThe First Heading\nParagraph under the first heading.\nThe second heading\nParagraph #1 under the second heading.\nParagraph #2 under the second heading.\n\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n\n'
```


```python
# 태그 body를 찾아 모든 태그와 각 텍스트의 시작과 끝에 있는 화이트스페이스를 제거한 텍스트만 가져온다.
__TODO__
```

**실행 결과**
```
'The First HeadingParagraph under the first heading.The second headingParagraph #1 underthe second heading.Paragraph #2 underthe second heading.This is a link toBusiness School at SNU.We also want to visitPython Official Web Page.'
```


```python
# 태그 body를 찾아 모든 태그를 제거한 후 각 텍스트를 문자열 ':::'로 결합한 텍스트를 가져온다.
__TODO__
```

**실행 결과**
```
'\n:::The First Heading:::\n:::Paragraph under the first heading.:::\n:::The second heading:::\n:::Paragraph #1 under :::the second heading:::.:::\n:::Paragraph #2 under :::the second heading:::.:::\n:::\n:::This is a link to :::Business School at SNU:::.:::\n:::We also want to visit :::Python Official Web Page:::.:::\n:::\n'
```


```python
# 웹 페이지 전체에서 모든 태그와 각 텍스트의 시작과 끝에 있는 화이트스페이스를 제거한다.
# 각 텍스트를 문자열 콤마(',')로 결합한 텍스트를 가져온다.
__TODO__
```

**실행 결과**
```
'A Simple Local Web Page,The First Heading,Paragraph under the first heading.,The second heading,Paragraph #1 under,the second heading,.,Paragraph #2 under,the second heading,.,This is a link to,Business School at SNU,.,We also want to visit,Python Official Web Page,.'
```


```python
# 문서에서 모든 태그 a를 검색하여 변수에 할당한 후 그 결과를 출력한다. 
tags = __TODO__
print(tags, end='\n\n')

# 태그 a의 텍스트는 변수 text에 할당하고 
# 속성 href의 속성값은 변수 link에 할당한 후 출력한다.
# [힌트] 태그 내 속성은 딕셔너리로 표현된다.
for tag in tags:
    text = __TODO__
    link = __TODO__
    print(f'{text} -> {link}')
```

**실행 결과**
```
[<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>, <a href="https://www.python.org" id="python">Python Official Web Page</a>]

Business School at SNU -> http://biz.snu.ac.kr
Python Official Web Page -> https://www.python.org
```

## get_text(), strings, stripped_strings의 단순 비교


```python
bs
```




    <!DOCTYPE html>
    
    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>




```python
bs.get_text()
```




    '\n\nA Simple Local Web Page\n\nThe First Heading\nParagraph under the first heading.\nThe second heading\nParagraph #1 under the second heading.\nParagraph #2 under the second heading.\n\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n\n\n'




```python
print(bs.get_text())
```

    
    
    A Simple Local Web Page
    
    The First Heading
    Paragraph under the first heading.
    The second heading
    Paragraph #1 under the second heading.
    Paragraph #2 under the second heading.
    
    This is a link to Business School at SNU.
    We also want to visit Python Official Web Page.
    
    
    



```python
bs.strings
```




    <generator object Tag._all_strings at 0x7fd5397a34a0>




```python
bs.stripped_strings
```




    <generator object Tag.stripped_strings at 0x7fd5397a3120>




```python
tuple(bs.strings)
```




    ('\n',
     '\n',
     'A Simple Local Web Page',
     '\n',
     '\n',
     'The First Heading',
     '\n',
     'Paragraph under the first heading.',
     '\n',
     'The second heading',
     '\n',
     'Paragraph #1 under ',
     'the second heading',
     '.',
     '\n',
     'Paragraph #2 under ',
     'the second heading',
     '.',
     '\n',
     '\n',
     'This is a link to ',
     'Business School at SNU',
     '.',
     '\n',
     'We also want to visit ',
     'Python Official Web Page',
     '.',
     '\n',
     '\n',
     '\n')




```python
tuple(bs.stripped_strings)
```




    ('A Simple Local Web Page',
     'The First Heading',
     'Paragraph under the first heading.',
     'The second heading',
     'Paragraph #1 under',
     'the second heading',
     '.',
     'Paragraph #2 under',
     'the second heading',
     '.',
     'This is a link to',
     'Business School at SNU',
     '.',
     'We also want to visit',
     'Python Official Web Page',
     '.')




```python
for content in bs.strings:
    print(repr(content))
```

    '\n'
    '\n'
    'A Simple Local Web Page'
    '\n'
    '\n'
    'The First Heading'
    '\n'
    'Paragraph under the first heading.'
    '\n'
    'The second heading'
    '\n'
    'Paragraph #1 under '
    'the second heading'
    '.'
    '\n'
    'Paragraph #2 under '
    'the second heading'
    '.'
    '\n'
    '\n'
    'This is a link to '
    'Business School at SNU'
    '.'
    '\n'
    'We also want to visit '
    'Python Official Web Page'
    '.'
    '\n'
    '\n'
    '\n'



```python
for content in bs.stripped_strings:
    print(repr(content))
```

    'A Simple Local Web Page'
    'The First Heading'
    'Paragraph under the first heading.'
    'The second heading'
    'Paragraph #1 under'
    'the second heading'
    '.'
    'Paragraph #2 under'
    'the second heading'
    '.'
    'This is a link to'
    'Business School at SNU'
    '.'
    'We also want to visit'
    'Python Official Web Page'
    '.'



```python
[text for text in bs.stripped_strings]
```




    ['A Simple Local Web Page',
     'The First Heading',
     'Paragraph under the first heading.',
     'The second heading',
     'Paragraph #1 under',
     'the second heading',
     '.',
     'Paragraph #2 under',
     'the second heading',
     '.',
     'This is a link to',
     'Business School at SNU',
     '.',
     'We also want to visit',
     'Python Official Web Page',
     '.']


# 웹에 접근하기

## urllib

**urllib.request.urlopen**()
- 웹에 있는 정보를 URL로 접근하여 가져올 수 있다.


```python
URL = 'https://www.google.com/'
```


```python
from urllib.request import urlopen

response = urlopen(URL)
response
```




    <http.client.HTTPResponse at 0x7fb8b04663d0>




```python
# --- open() 함수를 사용할 때와 비슷하게 read(), readline(), readlines() 메소드를 통해 내용을 가져올 수 있다.
# read()
html = response.read()
type(html)
```




    bytes




```python
html
```




    b'<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="ko"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){window.google={kEI:\'zuBDX8LKNP-Vr7wPpr-44Ao\',kEXPI:\'0,202123,3,4,32,4,1151581,5662,730,224,5104,207,3204,10,1226,364,1499,612,205,383,246,5,304,825,225,648,371,2611,470,314,3,373,460,218,89,41,15,138,380,46,438,30,86,453,408,187,24,82,33,159,7,79,48,45,1119510,1197731,503,329033,13677,4855,32692,15247,867,28684,9188,8384,4858,1362,9290,3030,4738,6,11027,1808,4020,978,7931,5297,2054,919,2091,1085,1890,6430,14528,4517,2777,919,261,2018,6,2796,889,704,1279,2213,530,148,561,542,840,518,1522,156,4101,108,204,1137,2,2063,606,2023,546,1187,43,521,1704,243,2229,93,328,1284,16,2927,2247,1812,1787,2273,1,953,2845,8,4772,826,6755,4455,641,2449,3685,1406,337,4928,108,3407,908,2,941,2614,2397,1386,6084,2177,1098,3,576,970,865,4624,149,189,3313,1495,546,8,439,2252,3942,47,1744,4,1448,80,2304,1236,271,874,405,42,211,1607,2393,1791,52,75,4,1337,961,463,460,120,1435,4,5099,1229,699,1403,3,1264,1426,69,2419,196,2069,733,9,501,1252,690,1968,416,76,53,3023,487,188,320,198,25,887,256,308,464,218,7,377,10,44,30,1078,225,528,231,1529,178,224,151,504,659,23,1757,650,137,203,52,535,249,229,762,54,51,894,259,1391,70,1005,346,160,187,151,6,12,735,19,689,6,84,263,168,117,330,199,1011,15,69,475,2,96,665,478,32,211,1884,18,1239,356,3,369,70,552,67,90,58,4,6,258,107,779,4,19,48,81,285,62,299,60,882,1,253,346,5769960,8801916,549,333,444,1,2,80,1,900,896,1,9,2,2551,1,748,141,59,736,563,1,4265,1,1,2,1017,9,305,3299,248,548,46,60,62,1,12,4,1,4,69,3501390,20458659,54,2700387,3,4387\',kBL:\'-bmB\'};google.sn=\'webhp\';google.kHL=\'ko\';})();(function(){google.lc=[];google.li=0;google.getEI=function(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||google.kEI};google.getLEI=function(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c};google.ml=function(){return null};google.time=function(){return Date.now()};google.log=function(a,c,b,d,g){if(b=google.logUrl(a,c,b,d,g)){a=new Image;var e=google.lc,f=google.li;e[f]=a;a.onerror=a.onload=a.onabort=function(){delete e[f]};google.vel&&google.vel.lu&&google.vel.lu(b);a.src=b;google.li=f+1}};google.logUrl=function(a,c,b,d,g){var e="",f=google.ls||"";b||-1!=c.search("&ei=")||(e="&ei="+google.getEI(d),-1==c.search("&lei=")&&(d=google.getLEI(d))&&(e+="&lei="+d));d="";!b&&google.cshid&&-1==c.search("&cshid=")&&"slh"!=a&&(d="&cshid="+google.cshid);b=b||"/"+(g||"gen_204")+"?atyp=i&ct="+a+"&cad="+c+e+f+"&zx="+google.time()+d;/^http:/i.test(b)&&"https:"==window.location.protocol&&(google.ml(Error("a"),!1,{src:b,glmm:1}),b="");return b};}).call(this);(function(){google.y={};google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};}).call(this);google.f={};(function(){\ndocument.documentElement.addEventListener("submit",function(b){var a;if(a=b.target){var c=a.getAttribute("data-submitfalse");a="1"==c||"q"==c&&!a.elements.q.value?!0:!1}else a=!1;a&&(b.preventDefault(),b.stopPropagation())},!0);document.documentElement.addEventListener("click",function(b){var a;a:{for(a=b.target;a&&a!=document.documentElement;a=a.parentElement)if("A"==a.tagName){a="1"==a.getAttribute("data-nohref");break a}a=!1}a&&b.preventDefault()},!0);}).call(this);\nvar a=window.location,b=a.href.indexOf("#");if(0<=b){var c=a.href.substring(b+1);/(^|&)q=/.test(c)&&-1==c.indexOf("#")&&a.replace("/search?"+c.replace(/(^|&)fp=[^&]*/g,"")+"&cad=h")};</script><style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}\n</style><style>body,td,a,p,.h{font-family:&#44404;&#47548;,&#46027;&#50880;,arial,sans-serif}.ko{font-size:9pt}body{margin:0;overflow-y:scroll}#gog{padding:3px 8px 0}td{line-height:.8em}.gac_m td{line-height:17px}form{margin-bottom:20px}.h{color:#36c}.q{color:#00c}em{font-weight:bold;font-style:normal}.lst{height:25px;width:496px}.gsfi,.lst{font:18px arial,sans-serif}.gsfs{font:17px arial,sans-serif}.ds{display:inline-box;display:inline-block;margin:3px 0 4px;margin-left:4px}input{font-family:inherit}body{background:#fff;color:#000}a{color:#11c;text-decoration:none}a:hover,a:active{text-decoration:underline}.fl a{color:#36c}a:visited{color:#551a8b}.sblc{padding-top:5px}.sblc a{display:block;margin:2px 0;margin-left:13px;font-size:11px}.lsbb{background:#eee;border:solid 1px;border-color:#ccc #999 #999 #ccc;height:30px}.lsbb{display:block}#fll a{display:inline-block;margin:0 12px}.lsb{background:url(/images/nav_logo229.png) 0 -261px repeat-x;border:none;color:#000;cursor:pointer;height:30px;margin:0;outline:0;font:15px arial,sans-serif;vertical-align:top}.lsb:active{background:#ccc}.lst:focus{outline:none}.tiah{width:458px}</style><script nonce="OVHcL33TR+jWq5a7CIle2w=="></script></head><body bgcolor="#fff"><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){var src=\'/images/nav_logo229.png\';var iesg=false;document.body.onload = function(){window.n && window.n();if (document.images){new Image().src=src;}\nif (!iesg){document.f&&document.f.q.focus();document.gbqf&&document.gbqf.q.focus();}\n}\n})();</script><div id="mngb"><div id=gbar><nobr><b class=gb1>&#44160;&#49353;</b> <a class=gb1 href="https://www.google.co.kr/imghp?hl=ko&tab=wi">&#51060;&#48120;&#51648;</a> <a class=gb1 href="https://maps.google.co.kr/maps?hl=ko&tab=wl">&#51648;&#46020;</a> <a class=gb1 href="https://play.google.com/?hl=ko&tab=w8">Play</a> <a class=gb1 href="https://www.youtube.com/?gl=KR&tab=w1">YouTube</a> <a class=gb1 href="https://news.google.com/?tab=wn">&#45684;&#49828;</a> <a class=gb1 href="https://mail.google.com/mail/?tab=wm">Gmail</a> <a class=gb1 href="https://drive.google.com/?tab=wo">&#46300;&#46972;&#51060;&#48652;</a> <a class=gb1 style="text-decoration:none" href="https://www.google.co.kr/intl/ko/about/products?tab=wh"><u>&#45908;&#48372;&#44592;</u> &raquo;</a></nobr></div><div id=guser width=100%><nobr><span id=gbn class=gbi></span><span id=gbf class=gbf></span><span id=gbe></span><a href="http://www.google.co.kr/history/optout?hl=ko" class=gb4>&#50937; &#44592;&#47197;</a> | <a  href="/preferences?hl=ko" class=gb4>&#49444;&#51221;</a> | <a target=_top id=gb_70 href="https://accounts.google.com/ServiceLogin?hl=ko&passive=true&continue=https://www.google.com/&ec=%0000000" class=gb4>&#47196;&#44536;&#51064;</a></nobr></div><div class=gbh style=left:0></div><div class=gbh style=right:0></div></div><center><br clear="all" id="lgpd"><div id="lga"><img alt="Google" height="92" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0 14px" width="272" id="hplogo"><br><br></div><form action="/search" name="f"><table cellpadding="0" cellspacing="0"><tr valign="top"><td width="25%">&nbsp;</td><td align="center" nowrap=""><input name="ie" value="ISO-8859-1" type="hidden"><input value="ko" name="hl" type="hidden"><input name="source" type="hidden" value="hp"><input name="biw" type="hidden"><input name="bih" type="hidden"><div class="ds" style="height:32px;margin:4px 0"><div style="position:relative;zoom:1"><input class="lst tiah" style="margin:0;padding:5px 8px 0 6px;vertical-align:top;color:#000;padding-right:38px" autocomplete="off" value="" title="Google &#44160;&#49353;" maxlength="2048" name="q" size="57"><img src="/textinputassistant/tia.png" style="position:absolute;cursor:pointer;right:5px;top:4px;z-index:300" data-script-url="/textinputassistant/11/ko_tia.js" id="tsuid1" alt="" height="23" width="27"><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){var id=\'tsuid1\';document.getElementById(id).onclick = function(){var s = document.createElement(\'script\');s.src = this.getAttribute(\'data-script-url\');(document.getElementById(\'xjsc\')||document.body).appendChild(s);};})();</script></div></div><br style="line-height:0"><span class="ds"><span class="lsbb"><input class="lsb" value="Google &#44160;&#49353;" name="btnG" type="submit"></span></span><span class="ds"><span class="lsbb"><input class="lsb" id="tsuid2" value="I&#8217;m Feeling Lucky" name="btnI" type="submit"><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){var id=\'tsuid2\';document.getElementById(id).onclick = function(){if (this.form.q.value){this.checked = 1;if (this.form.iflsig)this.form.iflsig.disabled = false;}\nelse top.location=\'/doodles/\';};})();</script><input value="AINFCbYAAAAAX0Pu3rqFi65KWHkOsud8lTS9QVwmW1py" name="iflsig" type="hidden"></span></span></td><td class="fl sblc" align="left" nowrap="" width="25%"><a href="/advanced_search?hl=ko&amp;authuser=0">&#44256;&#44553;&#44160;&#49353;</a></td></tr></table><input id="gbv" name="gbv" type="hidden" value="1"><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){var a,b="1";if(document&&document.getElementById)if("undefined"!=typeof XMLHttpRequest)b="2";else if("undefined"!=typeof ActiveXObject){var c,d,e=["MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0","MSXML2.XMLHTTP","Microsoft.XMLHTTP"];for(c=0;d=e[c++];)try{new ActiveXObject(d),b="2"}catch(h){}}a=b;if("2"==a&&-1==location.search.indexOf("&gbv=2")){var f=google.gbvu,g=document.getElementById("gbv");g&&(g.value=a);f&&window.setTimeout(function(){location.href=f},0)};}).call(this);</script></form><div id="gac_scont"></div><div style="font-size:83%;min-height:3.5em"><br><div id="prm"><style>.szppmdbYutt__middle-slot-promo{font-size:small;margin-bottom:32px}.szppmdbYutt__middle-slot-promo a.ZIeIlb{display:inline-block;text-decoration:none}.szppmdbYutt__middle-slot-promo img{border:none;margin-right:5px;vertical-align:middle}</style><div class="szppmdbYutt__middle-slot-promo" data-ved="0ahUKEwjC6bHol7TrAhX_yosBHaYfDqwQnIcBCAQ"><a class="NKcBbd" href="https://www.google.com/url?q=https://about.google/stories/clean-air-for-kampala/%3Futm_source%3DGoogle%26utm_medium%3DHPP%26utm_campaign%3DEngineer_Story&amp;source=hpp&amp;id=19019758&amp;ct=3&amp;usg=AFQjCNELzKzOJb0K6uO7sQD914KHywgjDQ&amp;sa=X&amp;ved=0ahUKEwjC6bHol7TrAhX_yosBHaYfDqwQ8IcBCAU" rel="nofollow">&#50864;&#44036;&#45796;&#51032; &#45824;&#44592; &#50724;&#50684;&#51012; &#51460;&#51060;&#44592; &#50948;&#54644; AI&#47484; &#54876;&#50857;&#54616;&#45716; &#50672;&#44396;&#54016;&#51012; &#47564;&#45208;&#48372;&#49464;&#50836;</a></div></div></div><span id="footer"><div style="font-size:10pt"><div style="margin:19px auto;text-align:center" id="fll"><a href="/intl/ko/ads/">&#44305;&#44256; &#54532;&#47196;&#44536;&#47016;</a><a href="http://www.google.co.kr/intl/ko/services/">&#48708;&#51592;&#45768;&#49828; &#49556;&#47336;&#49496;</a><a href="/intl/ko/about.html">Google &#51221;&#48372;</a><a href="https://www.google.com/setprefdomain?prefdom=KR&amp;prev=https://www.google.co.kr/&amp;sig=K_UlDlkj5Ethl1ar-ecyfXegNbmQ4%3D">Google.co.kr</a></div></div><p style="font-size:8pt;color:#767676">&copy; 2020 - <a href="/intl/ko/policies/privacy/">&#44060;&#51064;&#51221;&#48372;&#52376;&#47532;&#48169;&#52840;</a> - <a href="/intl/ko/policies/terms/">&#50557;&#44288;</a></p></span></center><script nonce="OVHcL33TR+jWq5a7CIle2w==">(function(){window.google.cdo={height:0,width:0};(function(){var a=window.innerWidth,b=window.innerHeight;if(!a||!b){var c=window.document,d="CSS1Compat"==c.compatMode?c.documentElement:c.body;a=d.clientWidth;b=d.clientHeight}a&&b&&(a!=google.cdo.width||b!=google.cdo.height)&&google.log("","","/client_204?&atyp=i&biw="+a+"&bih="+b+"&ei="+google.kEI);}).call(this);})();(function(){var u=\'/xjs/_/js/k\\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\\x3dsb_he,d/am\\x3dAJ5gcw/d\\x3d1/rs\\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog\';\nsetTimeout(function(){var b=document;var a="SCRIPT";"application/xhtml+xml"===b.contentType&&(a=a.toLowerCase());a=b.createElement(a);a.src=u;google.timers&&google.timers.load&&google.tick&&google.tick("load","xjsls");document.body.appendChild(a)},0);})();(function(){window.google.xjsu=\'/xjs/_/js/k\\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\\x3dsb_he,d/am\\x3dAJ5gcw/d\\x3d1/rs\\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog\';})();function _DumpException(e){throw e;}\nfunction _F_installCss(c){}\n(function(){google.jl={dw:false,em:[],emw:false,lls:\'default\',pdt:0,snet:true,uwp:true};})();(function(){var pmc=\'{\\x22d\\x22:{},\\x22sb_he\\x22:{\\x22agen\\x22:true,\\x22cgen\\x22:true,\\x22client\\x22:\\x22heirloom-hp\\x22,\\x22dh\\x22:true,\\x22dhqt\\x22:true,\\x22ds\\x22:\\x22\\x22,\\x22ffql\\x22:\\x22ko\\x22,\\x22fl\\x22:true,\\x22host\\x22:\\x22google.com\\x22,\\x22isbh\\x22:28,\\x22jsonp\\x22:true,\\x22msgs\\x22:{\\x22cibl\\x22:\\x22&#44160;&#49353;&#50612; &#51648;&#50864;&#44592;\\x22,\\x22dym\\x22:\\x22&#51060;&#44163;&#51012; &#52286;&#51004;&#49512;&#45208;&#50836;?\\x22,\\x22lcky\\x22:\\x22I&#8217;m Feeling Lucky\\x22,\\x22lml\\x22:\\x22&#51088;&#49464;&#55176; &#50508;&#50500;&#48372;&#44592;\\x22,\\x22oskt\\x22:\\x22&#51077;&#47141; &#46020;&#44396;\\x22,\\x22psrc\\x22:\\x22&#44160;&#49353;&#50612;&#44032; \\\\u003Ca href\\x3d\\\\\\x22/history\\\\\\x22\\\\u003E&#50937; &#44592;&#47197;\\\\u003C/a\\\\u003E&#50640;&#49436; &#49325;&#51228;&#46104;&#50632;&#49845;&#45768;&#45796;.\\x22,\\x22psrl\\x22:\\x22&#49325;&#51228;\\x22,\\x22sbit\\x22:\\x22&#51060;&#48120;&#51648;&#47196; &#44160;&#49353;\\x22,\\x22srch\\x22:\\x22Google &#44160;&#49353;\\x22},\\x22ovr\\x22:{},\\x22pq\\x22:\\x22\\x22,\\x22refpd\\x22:true,\\x22refspre\\x22:true,\\x22rfs\\x22:[],\\x22sbpl\\x22:16,\\x22sbpr\\x22:16,\\x22scd\\x22:10,\\x22stok\\x22:\\x22GxFL08d95DTMAf9juZyQV_bXxt4\\x22,\\x22uhde\\x22:false}}\';google.pmc=JSON.parse(pmc);})();</script>        </body></html>'




```python
# readline()
urlopen(URL).readline()
```




    b'<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="ko"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="L54iYMUORAWLSyaxE+9tKg==">(function(){window.google={kEI:\'z-BDX5_KHbCxmAXHub4w\',kEXPI:\'0,55814,146309,3,4,32,4,1151581,5662,730,224,5104,207,3204,10,1226,364,1499,611,206,383,246,5,1354,648,370,282,2330,469,50,265,3,373,677,91,41,7,145,110,755,29,86,452,409,327,11,139,91,3,94,1119509,1197731,545,328991,13677,4855,32692,15247,867,17444,11240,9188,8384,4859,1361,283,9007,3030,2815,1923,7,2640,8386,1808,4020,978,7931,5297,2974,873,37,1180,2975,6430,14528,4516,2778,919,910,1367,8,2796,887,706,1165,114,2212,530,149,1103,840,517,513,624,279,106,4258,312,1137,2,2063,606,2023,1777,520,1947,244,1985,95,326,1284,24,2919,2247,1812,1787,3227,2845,8,6067,6286,4455,641,2449,3685,1742,3748,1181,108,2855,552,908,2,941,2614,2397,7468,2179,1098,3,346,230,970,865,4625,148,189,3312,744,1745,2252,1798,194,1997,1744,4,1528,278,2,1418,606,1236,271,874,405,1860,2393,537,43,1211,52,1416,961,463,460,118,1437,3791,276,1036,1229,86,3,2283,997,1426,69,642,1,1776,196,2811,1753,690,1968,416,129,860,2498,151,189,320,198,25,887,254,310,299,165,597,3,4,52,30,894,409,445,314,645,883,180,223,151,504,659,23,318,1439,340,310,340,52,535,249,990,509,491,257,255,1221,992,346,158,346,12,732,22,561,128,6,481,35,116,330,338,956,475,2,93,3,497,362,527,126,1760,2,1077,532,372,70,552,68,522,140,496,166,49,340,1328,1,253,346,54,5769906,8801916,549,333,444,1,2,80,1,900,896,1,9,2,2551,1,748,200,736,4,559,1,4265,1,1,2,1017,9,305,3299,248,548,46,60,62,1,12,4,1,4,69,3501390,20458659,54,2704777\',kBL:\'-bmB\'};google.sn=\'webhp\';google.kHL=\'ko\';})();(function(){google.lc=[];google.li=0;google.getEI=function(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||google.kEI};google.getLEI=function(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c};google.ml=function(){return null};google.time=function(){return Date.now()};google.log=function(a,c,b,d,g){if(b=google.logUrl(a,c,b,d,g)){a=new Image;var e=google.lc,f=google.li;e[f]=a;a.onerror=a.onload=a.onabort=function(){delete e[f]};google.vel&&google.vel.lu&&google.vel.lu(b);a.src=b;google.li=f+1}};google.logUrl=function(a,c,b,d,g){var e="",f=google.ls||"";b||-1!=c.search("&ei=")||(e="&ei="+google.getEI(d),-1==c.search("&lei=")&&(d=google.getLEI(d))&&(e+="&lei="+d));d="";!b&&google.cshid&&-1==c.search("&cshid=")&&"slh"!=a&&(d="&cshid="+google.cshid);b=b||"/"+(g||"gen_204")+"?atyp=i&ct="+a+"&cad="+c+e+f+"&zx="+google.time()+d;/^http:/i.test(b)&&"https:"==window.location.protocol&&(google.ml(Error("a"),!1,{src:b,glmm:1}),b="");return b};}).call(this);(function(){google.y={};google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};}).call(this);google.f={};(function(){\n'




```python
# readlines()
lines = urlopen(URL).readlines()
type(lines), len(lines)
```




    (list, 11)




```python
lines
```




    [b'<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="ko"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){window.google={kEI:\'z-BDX7flKpKWr7wP95uc2AY\',kEXPI:\'0,202123,3,4,32,4,1151581,5662,730,224,5105,206,2415,789,10,1226,364,1499,611,93,113,383,246,5,1129,225,648,371,282,2799,314,3,1050,90,172,22,110,783,86,454,408,188,23,82,34,244,53,1119550,1197694,582,328991,13677,4855,32691,15248,867,17444,1953,9287,9188,8384,4859,1361,9291,3020,2824,1923,11033,1816,4012,978,7933,5295,2054,920,873,1217,2975,6430,14527,4517,2778,919,2277,9,2795,887,706,1165,114,2212,530,149,1103,840,517,1137,279,53,53,157,4101,109,203,1137,2,2063,606,2023,1733,43,521,1947,2229,93,328,1284,16,447,2480,2246,1813,1787,3227,2845,7,6068,6286,4455,641,2449,3685,1742,3748,1181,108,3407,908,2,941,2614,2397,1386,6082,2179,1098,3,576,970,865,4625,149,188,3312,743,1300,47,401,2250,1991,1998,1744,4,1528,701,1603,1236,271,874,405,1860,2393,1791,52,1416,961,464,459,117,1438,2563,1504,1035,717,512,87,2019,390,874,1426,69,2615,2811,1753,690,1968,416,129,3358,152,188,320,198,25,887,254,310,464,218,7,376,7,48,30,470,833,759,1527,181,222,152,504,659,23,1102,655,650,225,53,62,52,535,249,989,52,950,255,256,1140,68,1005,345,161,343,13,141,576,726,6,483,32,117,330,338,956,406,69,2,93,2,493,2885,3,108,1395,38,335,619,70,224,298,850,81,347,359,511,371,1,269,330,5769960,8800593,1323,549,333,444,1,2,80,1,900,897,2,7,2,2551,1,748,141,795,10,553,1,4265,1,1,2,1017,9,305,3299,248,548,46,60,62,1,12,4,1,4,69,3501390,20458659,53,2704778\',kBL:\'-bmB\'};google.sn=\'webhp\';google.kHL=\'ko\';})();(function(){google.lc=[];google.li=0;google.getEI=function(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||google.kEI};google.getLEI=function(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c};google.ml=function(){return null};google.time=function(){return Date.now()};google.log=function(a,c,b,d,g){if(b=google.logUrl(a,c,b,d,g)){a=new Image;var e=google.lc,f=google.li;e[f]=a;a.onerror=a.onload=a.onabort=function(){delete e[f]};google.vel&&google.vel.lu&&google.vel.lu(b);a.src=b;google.li=f+1}};google.logUrl=function(a,c,b,d,g){var e="",f=google.ls||"";b||-1!=c.search("&ei=")||(e="&ei="+google.getEI(d),-1==c.search("&lei=")&&(d=google.getLEI(d))&&(e+="&lei="+d));d="";!b&&google.cshid&&-1==c.search("&cshid=")&&"slh"!=a&&(d="&cshid="+google.cshid);b=b||"/"+(g||"gen_204")+"?atyp=i&ct="+a+"&cad="+c+e+f+"&zx="+google.time()+d;/^http:/i.test(b)&&"https:"==window.location.protocol&&(google.ml(Error("a"),!1,{src:b,glmm:1}),b="");return b};}).call(this);(function(){google.y={};google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};}).call(this);google.f={};(function(){\n',
     b'document.documentElement.addEventListener("submit",function(b){var a;if(a=b.target){var c=a.getAttribute("data-submitfalse");a="1"==c||"q"==c&&!a.elements.q.value?!0:!1}else a=!1;a&&(b.preventDefault(),b.stopPropagation())},!0);document.documentElement.addEventListener("click",function(b){var a;a:{for(a=b.target;a&&a!=document.documentElement;a=a.parentElement)if("A"==a.tagName){a="1"==a.getAttribute("data-nohref");break a}a=!1}a&&b.preventDefault()},!0);}).call(this);\n',
     b'var a=window.location,b=a.href.indexOf("#");if(0<=b){var c=a.href.substring(b+1);/(^|&)q=/.test(c)&&-1==c.indexOf("#")&&a.replace("/search?"+c.replace(/(^|&)fp=[^&]*/g,"")+"&cad=h")};</script><style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}\n',
     b'</style><style>body,td,a,p,.h{font-family:&#44404;&#47548;,&#46027;&#50880;,arial,sans-serif}.ko{font-size:9pt}body{margin:0;overflow-y:scroll}#gog{padding:3px 8px 0}td{line-height:.8em}.gac_m td{line-height:17px}form{margin-bottom:20px}.h{color:#36c}.q{color:#00c}em{font-weight:bold;font-style:normal}.lst{height:25px;width:496px}.gsfi,.lst{font:18px arial,sans-serif}.gsfs{font:17px arial,sans-serif}.ds{display:inline-box;display:inline-block;margin:3px 0 4px;margin-left:4px}input{font-family:inherit}body{background:#fff;color:#000}a{color:#11c;text-decoration:none}a:hover,a:active{text-decoration:underline}.fl a{color:#36c}a:visited{color:#551a8b}.sblc{padding-top:5px}.sblc a{display:block;margin:2px 0;margin-left:13px;font-size:11px}.lsbb{background:#eee;border:solid 1px;border-color:#ccc #999 #999 #ccc;height:30px}.lsbb{display:block}#fll a{display:inline-block;margin:0 12px}.lsb{background:url(/images/nav_logo229.png) 0 -261px repeat-x;border:none;color:#000;cursor:pointer;height:30px;margin:0;outline:0;font:15px arial,sans-serif;vertical-align:top}.lsb:active{background:#ccc}.lst:focus{outline:none}.tiah{width:458px}</style><script nonce="Jy4BXkzCI9KcfIrdtyLbPw=="></script></head><body bgcolor="#fff"><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){var src=\'/images/nav_logo229.png\';var iesg=false;document.body.onload = function(){window.n && window.n();if (document.images){new Image().src=src;}\n',
     b'if (!iesg){document.f&&document.f.q.focus();document.gbqf&&document.gbqf.q.focus();}\n',
     b'}\n',
     b'})();</script><div id="mngb"><div id=gbar><nobr><b class=gb1>&#44160;&#49353;</b> <a class=gb1 href="https://www.google.co.kr/imghp?hl=ko&tab=wi">&#51060;&#48120;&#51648;</a> <a class=gb1 href="https://maps.google.co.kr/maps?hl=ko&tab=wl">&#51648;&#46020;</a> <a class=gb1 href="https://play.google.com/?hl=ko&tab=w8">Play</a> <a class=gb1 href="https://www.youtube.com/?gl=KR&tab=w1">YouTube</a> <a class=gb1 href="https://news.google.com/?tab=wn">&#45684;&#49828;</a> <a class=gb1 href="https://mail.google.com/mail/?tab=wm">Gmail</a> <a class=gb1 href="https://drive.google.com/?tab=wo">&#46300;&#46972;&#51060;&#48652;</a> <a class=gb1 style="text-decoration:none" href="https://www.google.co.kr/intl/ko/about/products?tab=wh"><u>&#45908;&#48372;&#44592;</u> &raquo;</a></nobr></div><div id=guser width=100%><nobr><span id=gbn class=gbi></span><span id=gbf class=gbf></span><span id=gbe></span><a href="http://www.google.co.kr/history/optout?hl=ko" class=gb4>&#50937; &#44592;&#47197;</a> | <a  href="/preferences?hl=ko" class=gb4>&#49444;&#51221;</a> | <a target=_top id=gb_70 href="https://accounts.google.com/ServiceLogin?hl=ko&passive=true&continue=https://www.google.com/&ec=%0000000" class=gb4>&#47196;&#44536;&#51064;</a></nobr></div><div class=gbh style=left:0></div><div class=gbh style=right:0></div></div><center><br clear="all" id="lgpd"><div id="lga"><img alt="Google" height="92" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0 14px" width="272" id="hplogo"><br><br></div><form action="/search" name="f"><table cellpadding="0" cellspacing="0"><tr valign="top"><td width="25%">&nbsp;</td><td align="center" nowrap=""><input name="ie" value="ISO-8859-1" type="hidden"><input value="ko" name="hl" type="hidden"><input name="source" type="hidden" value="hp"><input name="biw" type="hidden"><input name="bih" type="hidden"><div class="ds" style="height:32px;margin:4px 0"><div style="position:relative;zoom:1"><input class="lst tiah" style="margin:0;padding:5px 8px 0 6px;vertical-align:top;color:#000;padding-right:38px" autocomplete="off" value="" title="Google &#44160;&#49353;" maxlength="2048" name="q" size="57"><img src="/textinputassistant/tia.png" style="position:absolute;cursor:pointer;right:5px;top:4px;z-index:300" data-script-url="/textinputassistant/11/ko_tia.js" id="tsuid1" alt="" height="23" width="27"><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){var id=\'tsuid1\';document.getElementById(id).onclick = function(){var s = document.createElement(\'script\');s.src = this.getAttribute(\'data-script-url\');(document.getElementById(\'xjsc\')||document.body).appendChild(s);};})();</script></div></div><br style="line-height:0"><span class="ds"><span class="lsbb"><input class="lsb" value="Google &#44160;&#49353;" name="btnG" type="submit"></span></span><span class="ds"><span class="lsbb"><input class="lsb" id="tsuid2" value="I&#8217;m Feeling Lucky" name="btnI" type="submit"><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){var id=\'tsuid2\';document.getElementById(id).onclick = function(){if (this.form.q.value){this.checked = 1;if (this.form.iflsig)this.form.iflsig.disabled = false;}\n',
     b'else top.location=\'/doodles/\';};})();</script><input value="AINFCbYAAAAAX0Pu39j5Nd4gL8EsVFb9ZvGIRLxGSOD9" name="iflsig" type="hidden"></span></span></td><td class="fl sblc" align="left" nowrap="" width="25%"><a href="/advanced_search?hl=ko&amp;authuser=0">&#44256;&#44553;&#44160;&#49353;</a></td></tr></table><input id="gbv" name="gbv" type="hidden" value="1"><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){var a,b="1";if(document&&document.getElementById)if("undefined"!=typeof XMLHttpRequest)b="2";else if("undefined"!=typeof ActiveXObject){var c,d,e=["MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0","MSXML2.XMLHTTP","Microsoft.XMLHTTP"];for(c=0;d=e[c++];)try{new ActiveXObject(d),b="2"}catch(h){}}a=b;if("2"==a&&-1==location.search.indexOf("&gbv=2")){var f=google.gbvu,g=document.getElementById("gbv");g&&(g.value=a);f&&window.setTimeout(function(){location.href=f},0)};}).call(this);</script></form><div id="gac_scont"></div><div style="font-size:83%;min-height:3.5em"><br><div id="prm"><style>.szppmdbYutt__middle-slot-promo{font-size:small;margin-bottom:32px}.szppmdbYutt__middle-slot-promo a.ZIeIlb{display:inline-block;text-decoration:none}.szppmdbYutt__middle-slot-promo img{border:none;margin-right:5px;vertical-align:middle}</style><div class="szppmdbYutt__middle-slot-promo" data-ved="0ahUKEwj3iOXol7TrAhUSy4sBHfcNB2sQnIcBCAQ"><a class="NKcBbd" href="https://www.google.com/url?q=https://about.google/stories/clean-air-for-kampala/%3Futm_source%3DGoogle%26utm_medium%3DHPP%26utm_campaign%3DEngineer_Story&amp;source=hpp&amp;id=19019758&amp;ct=3&amp;usg=AFQjCNELzKzOJb0K6uO7sQD914KHywgjDQ&amp;sa=X&amp;ved=0ahUKEwj3iOXol7TrAhUSy4sBHfcNB2sQ8IcBCAU" rel="nofollow">&#50864;&#44036;&#45796;&#51032; &#45824;&#44592; &#50724;&#50684;&#51012; &#51460;&#51060;&#44592; &#50948;&#54644; AI&#47484; &#54876;&#50857;&#54616;&#45716; &#50672;&#44396;&#54016;&#51012; &#47564;&#45208;&#48372;&#49464;&#50836;</a></div></div></div><span id="footer"><div style="font-size:10pt"><div style="margin:19px auto;text-align:center" id="fll"><a href="/intl/ko/ads/">&#44305;&#44256; &#54532;&#47196;&#44536;&#47016;</a><a href="http://www.google.co.kr/intl/ko/services/">&#48708;&#51592;&#45768;&#49828; &#49556;&#47336;&#49496;</a><a href="/intl/ko/about.html">Google &#51221;&#48372;</a><a href="https://www.google.com/setprefdomain?prefdom=KR&amp;prev=https://www.google.co.kr/&amp;sig=K_ex9lXzXTbiVuHhQUsz-_an7gpLA%3D">Google.co.kr</a></div></div><p style="font-size:8pt;color:#767676">&copy; 2020 - <a href="/intl/ko/policies/privacy/">&#44060;&#51064;&#51221;&#48372;&#52376;&#47532;&#48169;&#52840;</a> - <a href="/intl/ko/policies/terms/">&#50557;&#44288;</a></p></span></center><script nonce="Jy4BXkzCI9KcfIrdtyLbPw==">(function(){window.google.cdo={height:0,width:0};(function(){var a=window.innerWidth,b=window.innerHeight;if(!a||!b){var c=window.document,d="CSS1Compat"==c.compatMode?c.documentElement:c.body;a=d.clientWidth;b=d.clientHeight}a&&b&&(a!=google.cdo.width||b!=google.cdo.height)&&google.log("","","/client_204?&atyp=i&biw="+a+"&bih="+b+"&ei="+google.kEI);}).call(this);})();(function(){var u=\'/xjs/_/js/k\\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\\x3dsb_he,d/am\\x3dAJ5gcw/d\\x3d1/rs\\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog\';\n',
     b'setTimeout(function(){var b=document;var a="SCRIPT";"application/xhtml+xml"===b.contentType&&(a=a.toLowerCase());a=b.createElement(a);a.src=u;google.timers&&google.timers.load&&google.tick&&google.tick("load","xjsls");document.body.appendChild(a)},0);})();(function(){window.google.xjsu=\'/xjs/_/js/k\\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\\x3dsb_he,d/am\\x3dAJ5gcw/d\\x3d1/rs\\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog\';})();function _DumpException(e){throw e;}\n',
     b'function _F_installCss(c){}\n',
     b"(function(){google.jl={dw:false,em:[],emw:false,lls:'default',pdt:0,snet:true,uwp:true};})();(function(){var pmc='{\\x22d\\x22:{},\\x22sb_he\\x22:{\\x22agen\\x22:true,\\x22cgen\\x22:true,\\x22client\\x22:\\x22heirloom-hp\\x22,\\x22dh\\x22:true,\\x22dhqt\\x22:true,\\x22ds\\x22:\\x22\\x22,\\x22ffql\\x22:\\x22ko\\x22,\\x22fl\\x22:true,\\x22host\\x22:\\x22google.com\\x22,\\x22isbh\\x22:28,\\x22jsonp\\x22:true,\\x22msgs\\x22:{\\x22cibl\\x22:\\x22&#44160;&#49353;&#50612; &#51648;&#50864;&#44592;\\x22,\\x22dym\\x22:\\x22&#51060;&#44163;&#51012; &#52286;&#51004;&#49512;&#45208;&#50836;?\\x22,\\x22lcky\\x22:\\x22I&#8217;m Feeling Lucky\\x22,\\x22lml\\x22:\\x22&#51088;&#49464;&#55176; &#50508;&#50500;&#48372;&#44592;\\x22,\\x22oskt\\x22:\\x22&#51077;&#47141; &#46020;&#44396;\\x22,\\x22psrc\\x22:\\x22&#44160;&#49353;&#50612;&#44032; \\\\u003Ca href\\x3d\\\\\\x22/history\\\\\\x22\\\\u003E&#50937; &#44592;&#47197;\\\\u003C/a\\\\u003E&#50640;&#49436; &#49325;&#51228;&#46104;&#50632;&#49845;&#45768;&#45796;.\\x22,\\x22psrl\\x22:\\x22&#49325;&#51228;\\x22,\\x22sbit\\x22:\\x22&#51060;&#48120;&#51648;&#47196; &#44160;&#49353;\\x22,\\x22srch\\x22:\\x22Google &#44160;&#49353;\\x22},\\x22ovr\\x22:{},\\x22pq\\x22:\\x22\\x22,\\x22refpd\\x22:true,\\x22refspre\\x22:true,\\x22rfs\\x22:[],\\x22sbpl\\x22:16,\\x22sbpr\\x22:16,\\x22scd\\x22:10,\\x22stok\\x22:\\x22663cgNbzB9QgCxCsiFZGgrWSkr8\\x22,\\x22uhde\\x22:false}}';google.pmc=JSON.parse(pmc);})();</script>        </body></html>"]



## BeautifulSoup


```python
URL = 'https://www.google.com/'
```


```python
from urllib.request import urlopen

response = urlopen(URL)
response
```




    <http.client.HTTPResponse at 0x7fb8d0775e50>




```python
from bs4 import BeautifulSoup

bs = BeautifulSoup(response, 'html.parser')
type(bs)
```




    bs4.BeautifulSoup




```python
bs
```




    <!DOCTYPE doctype html>
    <html itemscope="" itemtype="http://schema.org/WebPage" lang="ko"><head><meta content="text/html; charset=utf-8" http-equiv="Content-Type"/><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"/><title>Google</title><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){window.google={kEI:'0OBDX7PsEpHemAWl-rawCQ',kEXPI:'0,202123,3,4,32,4,1151581,5662,731,223,5105,206,3204,10,1226,364,1499,611,206,383,246,5,1354,648,370,2612,470,50,264,3,374,286,391,89,42,7,144,380,48,307,159,84,456,408,211,3,113,134,7,104,1119602,1197765,308,203,328991,13677,4855,32691,15248,867,17444,11240,9188,8384,4859,1361,284,9007,3024,2819,1924,2646,5354,3033,1808,4020,978,7931,5297,2054,920,873,1217,2975,6431,14526,4517,1397,1381,919,2277,10,83,2711,1593,1165,114,2212,530,149,1103,842,515,513,624,279,106,4258,312,1137,2,2669,2023,1777,521,1703,243,2229,93,328,1284,16,2927,2247,1812,1787,3227,2845,7,6068,6286,4455,641,2450,3684,1405,338,3748,1180,108,1456,1951,908,2,941,2614,2397,7468,2179,1098,3,346,230,970,865,4625,148,189,3313,743,1298,8,439,2252,1991,1998,1744,4,1448,80,701,997,606,1236,271,874,405,1861,2392,1791,52,1416,961,463,460,120,1435,4067,154,881,1230,86,3,2406,874,1426,69,644,1,1774,196,2811,935,818,690,1968,416,129,164,504,2355,486,189,320,198,25,887,256,308,464,217,8,377,10,44,30,1303,759,1528,180,222,152,504,659,23,334,147,17,1259,650,278,62,52,535,249,989,56,945,256,255,738,471,1005,346,160,344,12,139,616,688,6,515,117,330,337,873,84,475,2,96,1137,38,211,141,1468,1389,154,26,320,371,622,588,27,114,663,48,81,1588,1,253,346,458,5769502,3522,8798394,549,333,444,1,2,80,1,900,896,1,9,2,2551,1,748,141,59,736,563,1,4265,1,1,2,1017,9,305,3299,248,548,46,60,62,1,12,4,1,4,69,3501390,20458659,53,2701839',kBL:'-bmB'};google.sn='webhp';google.kHL='ko';})();(function(){google.lc=[];google.li=0;google.getEI=function(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||google.kEI};google.getLEI=function(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c};google.ml=function(){return null};google.time=function(){return Date.now()};google.log=function(a,c,b,d,g){if(b=google.logUrl(a,c,b,d,g)){a=new Image;var e=google.lc,f=google.li;e[f]=a;a.onerror=a.onload=a.onabort=function(){delete e[f]};google.vel&&google.vel.lu&&google.vel.lu(b);a.src=b;google.li=f+1}};google.logUrl=function(a,c,b,d,g){var e="",f=google.ls||"";b||-1!=c.search("&ei=")||(e="&ei="+google.getEI(d),-1==c.search("&lei=")&&(d=google.getLEI(d))&&(e+="&lei="+d));d="";!b&&google.cshid&&-1==c.search("&cshid=")&&"slh"!=a&&(d="&cshid="+google.cshid);b=b||"/"+(g||"gen_204")+"?atyp=i&ct="+a+"&cad="+c+e+f+"&zx="+google.time()+d;/^http:/i.test(b)&&"https:"==window.location.protocol&&(google.ml(Error("a"),!1,{src:b,glmm:1}),b="");return b};}).call(this);(function(){google.y={};google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};}).call(this);google.f={};(function(){
    document.documentElement.addEventListener("submit",function(b){var a;if(a=b.target){var c=a.getAttribute("data-submitfalse");a="1"==c||"q"==c&&!a.elements.q.value?!0:!1}else a=!1;a&&(b.preventDefault(),b.stopPropagation())},!0);document.documentElement.addEventListener("click",function(b){var a;a:{for(a=b.target;a&&a!=document.documentElement;a=a.parentElement)if("A"==a.tagName){a="1"==a.getAttribute("data-nohref");break a}a=!1}a&&b.preventDefault()},!0);}).call(this);
    var a=window.location,b=a.href.indexOf("#");if(0<=b){var c=a.href.substring(b+1);/(^|&)q=/.test(c)&&-1==c.indexOf("#")&&a.replace("/search?"+c.replace(/(^|&)fp=[^&]*/g,"")+"&cad=h")};</script><style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}
    </style><style>body,td,a,p,.h{font-family:&#44404;&#47548;,&#46027;&#50880;,arial,sans-serif}.ko{font-size:9pt}body{margin:0;overflow-y:scroll}#gog{padding:3px 8px 0}td{line-height:.8em}.gac_m td{line-height:17px}form{margin-bottom:20px}.h{color:#36c}.q{color:#00c}em{font-weight:bold;font-style:normal}.lst{height:25px;width:496px}.gsfi,.lst{font:18px arial,sans-serif}.gsfs{font:17px arial,sans-serif}.ds{display:inline-box;display:inline-block;margin:3px 0 4px;margin-left:4px}input{font-family:inherit}body{background:#fff;color:#000}a{color:#11c;text-decoration:none}a:hover,a:active{text-decoration:underline}.fl a{color:#36c}a:visited{color:#551a8b}.sblc{padding-top:5px}.sblc a{display:block;margin:2px 0;margin-left:13px;font-size:11px}.lsbb{background:#eee;border:solid 1px;border-color:#ccc #999 #999 #ccc;height:30px}.lsbb{display:block}#fll a{display:inline-block;margin:0 12px}.lsb{background:url(/images/nav_logo229.png) 0 -261px repeat-x;border:none;color:#000;cursor:pointer;height:30px;margin:0;outline:0;font:15px arial,sans-serif;vertical-align:top}.lsb:active{background:#ccc}.lst:focus{outline:none}.tiah{width:458px}</style><script nonce="//IKsItD0wzouSzhdZULxA=="></script></head><body bgcolor="#fff"><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){var src='/images/nav_logo229.png';var iesg=false;document.body.onload = function(){window.n && window.n();if (document.images){new Image().src=src;}
    if (!iesg){document.f&&document.f.q.focus();document.gbqf&&document.gbqf.q.focus();}
    }
    })();</script><div id="mngb"><div id="gbar"><nobr><b class="gb1">검색</b> <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a> <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a> <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a> <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a> <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a> <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a> <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a> <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a></nobr></div><div id="guser" width="100%"><nobr><span class="gbi" id="gbn"></span><span class="gbf" id="gbf"></span><span id="gbe"></span><a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a> | <a class="gb4" href="/preferences?hl=ko">설정</a> | <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a></nobr></div><div class="gbh" style="left:0"></div><div class="gbh" style="right:0"></div></div><center><br clear="all" id="lgpd"/><div id="lga"><img alt="Google" height="92" id="hplogo" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0 14px" width="272"/><br/><br/></div><form action="/search" name="f"><table cellpadding="0" cellspacing="0"><tr valign="top"><td width="25%"> </td><td align="center" nowrap=""><input name="ie" type="hidden" value="ISO-8859-1"/><input name="hl" type="hidden" value="ko"/><input name="source" type="hidden" value="hp"/><input name="biw" type="hidden"/><input name="bih" type="hidden"/><div class="ds" style="height:32px;margin:4px 0"><div style="position:relative;zoom:1"><input autocomplete="off" class="lst tiah" maxlength="2048" name="q" size="57" style="margin:0;padding:5px 8px 0 6px;vertical-align:top;color:#000;padding-right:38px" title="Google 검색" value=""/><img alt="" data-script-url="/textinputassistant/11/ko_tia.js" height="23" id="tsuid1" src="/textinputassistant/tia.png" style="position:absolute;cursor:pointer;right:5px;top:4px;z-index:300" width="27"/><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){var id='tsuid1';document.getElementById(id).onclick = function(){var s = document.createElement('script');s.src = this.getAttribute('data-script-url');(document.getElementById('xjsc')||document.body).appendChild(s);};})();</script></div></div><br style="line-height:0"/><span class="ds"><span class="lsbb"><input class="lsb" name="btnG" type="submit" value="Google 검색"/></span></span><span class="ds"><span class="lsbb"><input class="lsb" id="tsuid2" name="btnI" type="submit" value="I’m Feeling Lucky"/><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){var id='tsuid2';document.getElementById(id).onclick = function(){if (this.form.q.value){this.checked = 1;if (this.form.iflsig)this.form.iflsig.disabled = false;}
    else top.location='/doodles/';};})();</script><input name="iflsig" type="hidden" value="AINFCbYAAAAAX0Pu4O9wbf8oP4_XQNCrTly3QBa3OXVP"/></span></span></td><td align="left" class="fl sblc" nowrap="" width="25%"><a href="/advanced_search?hl=ko&amp;authuser=0">고급검색</a></td></tr></table><input id="gbv" name="gbv" type="hidden" value="1"/><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){var a,b="1";if(document&&document.getElementById)if("undefined"!=typeof XMLHttpRequest)b="2";else if("undefined"!=typeof ActiveXObject){var c,d,e=["MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0","MSXML2.XMLHTTP","Microsoft.XMLHTTP"];for(c=0;d=e[c++];)try{new ActiveXObject(d),b="2"}catch(h){}}a=b;if("2"==a&&-1==location.search.indexOf("&gbv=2")){var f=google.gbvu,g=document.getElementById("gbv");g&&(g.value=a);f&&window.setTimeout(function(){location.href=f},0)};}).call(this);</script></form><div id="gac_scont"></div><div style="font-size:83%;min-height:3.5em"><br/><div id="prm"><style>.szppmdbYutt__middle-slot-promo{font-size:small;margin-bottom:32px}.szppmdbYutt__middle-slot-promo a.ZIeIlb{display:inline-block;text-decoration:none}.szppmdbYutt__middle-slot-promo img{border:none;margin-right:5px;vertical-align:middle}</style><div class="szppmdbYutt__middle-slot-promo" data-ved="0ahUKEwizlIrpl7TrAhURL6YKHSW9DZYQnIcBCAQ"><a class="NKcBbd" href="https://www.google.com/url?q=https://about.google/stories/clean-air-for-kampala/%3Futm_source%3DGoogle%26utm_medium%3DHPP%26utm_campaign%3DEngineer_Story&amp;source=hpp&amp;id=19019758&amp;ct=3&amp;usg=AFQjCNELzKzOJb0K6uO7sQD914KHywgjDQ&amp;sa=X&amp;ved=0ahUKEwizlIrpl7TrAhURL6YKHSW9DZYQ8IcBCAU" rel="nofollow">우간다의 대기 오염을 줄이기 위해 AI를 활용하는 연구팀을 만나보세요</a></div></div></div><span id="footer"><div style="font-size:10pt"><div id="fll" style="margin:19px auto;text-align:center"><a href="/intl/ko/ads/">광고 프로그램</a><a href="http://www.google.co.kr/intl/ko/services/">비즈니스 솔루션</a><a href="/intl/ko/about.html">Google 정보</a><a href="https://www.google.com/setprefdomain?prefdom=KR&amp;prev=https://www.google.co.kr/&amp;sig=K_mU3ypo-7wCbCBi5ZAHZnf8iHSTc%3D">Google.co.kr</a></div></div><p style="font-size:8pt;color:#767676">© 2020 - <a href="/intl/ko/policies/privacy/">개인정보처리방침</a> - <a href="/intl/ko/policies/terms/">약관</a></p></span></center><script nonce="//IKsItD0wzouSzhdZULxA==">(function(){window.google.cdo={height:0,width:0};(function(){var a=window.innerWidth,b=window.innerHeight;if(!a||!b){var c=window.document,d="CSS1Compat"==c.compatMode?c.documentElement:c.body;a=d.clientWidth;b=d.clientHeight}a&&b&&(a!=google.cdo.width||b!=google.cdo.height)&&google.log("","","/client_204?&atyp=i&biw="+a+"&bih="+b+"&ei="+google.kEI);}).call(this);})();(function(){var u='/xjs/_/js/k\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\x3dsb_he,d/am\x3dAJ5gcw/d\x3d1/rs\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog';
    setTimeout(function(){var b=document;var a="SCRIPT";"application/xhtml+xml"===b.contentType&&(a=a.toLowerCase());a=b.createElement(a);a.src=u;google.timers&&google.timers.load&&google.tick&&google.tick("load","xjsls");document.body.appendChild(a)},0);})();(function(){window.google.xjsu='/xjs/_/js/k\x3dxjs.hp.en.JEBLbdHGMZ4.O/m\x3dsb_he,d/am\x3dAJ5gcw/d\x3d1/rs\x3dACT90oE5v_LRqw1GtjavBuThAC7uj1vhog';})();function _DumpException(e){throw e;}
    function _F_installCss(c){}
    (function(){google.jl={dw:false,em:[],emw:false,lls:'default',pdt:0,snet:true,uwp:true};})();(function(){var pmc='{\x22d\x22:{},\x22sb_he\x22:{\x22agen\x22:true,\x22cgen\x22:true,\x22client\x22:\x22heirloom-hp\x22,\x22dh\x22:true,\x22dhqt\x22:true,\x22ds\x22:\x22\x22,\x22ffql\x22:\x22ko\x22,\x22fl\x22:true,\x22host\x22:\x22google.com\x22,\x22isbh\x22:28,\x22jsonp\x22:true,\x22msgs\x22:{\x22cibl\x22:\x22&#44160;&#49353;&#50612; &#51648;&#50864;&#44592;\x22,\x22dym\x22:\x22&#51060;&#44163;&#51012; &#52286;&#51004;&#49512;&#45208;&#50836;?\x22,\x22lcky\x22:\x22I&#8217;m Feeling Lucky\x22,\x22lml\x22:\x22&#51088;&#49464;&#55176; &#50508;&#50500;&#48372;&#44592;\x22,\x22oskt\x22:\x22&#51077;&#47141; &#46020;&#44396;\x22,\x22psrc\x22:\x22&#44160;&#49353;&#50612;&#44032; \\u003Ca href\x3d\\\x22/history\\\x22\\u003E&#50937; &#44592;&#47197;\\u003C/a\\u003E&#50640;&#49436; &#49325;&#51228;&#46104;&#50632;&#49845;&#45768;&#45796;.\x22,\x22psrl\x22:\x22&#49325;&#51228;\x22,\x22sbit\x22:\x22&#51060;&#48120;&#51648;&#47196; &#44160;&#49353;\x22,\x22srch\x22:\x22Google &#44160;&#49353;\x22},\x22ovr\x22:{},\x22pq\x22:\x22\x22,\x22refpd\x22:true,\x22refspre\x22:true,\x22rfs\x22:[],\x22sbpl\x22:16,\x22sbpr\x22:16,\x22scd\x22:10,\x22stok\x22:\x22YIkq4yCMKDPCxshBIUwNQUPmMRo\x22,\x22uhde\x22:false}}';google.pmc=JSON.parse(pmc);})();</script> </body></html>




```python
tag = bs.find('a')
tag
```




    <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>




```python
link = tag['href']
link
```




    'https://www.google.co.kr/imghp?hl=ko&tab=wi'



[urllib.parse.urlparse](https://docs.python.org/3/library/urllib.parse.html?highlight=urlparse#urllib.parse.urlparse)
- Parse a URL into six components, returning a 6-item named tuple.
    + This corresponds to the general structure of a URL: **scheme://netloc/path;parameters?query#fragment.**
- urllib.parse.**urlparse**(*urlstring, scheme='', allow_fragments=True*)

<pre>
>>> from urllib.parse import urlparse
>>> o = urlparse('http://www.cwi.nl:80/%7Eguido/Python.html')
>>> o   
ParseResult(scheme='http', netloc='www.cwi.nl:80', path='/%7Eguido/Python.html',
            params='', query='', fragment='')
>>> o.scheme
'http'
>>> o.port
80
>>> o.geturl()
'http://www.cwi.nl:80/%7Eguido/Python.html'
</pre>


```python
import urllib

result = urllib.parse.urlparse(link)
result
```




    ParseResult(scheme='https', netloc='www.google.co.kr', path='/imghp', params='', query='hl=ko&tab=wi', fragment='')




```python
result.scheme
```




    'https'




```python
result.netloc
```




    'www.google.co.kr'




```python
result.path
```




    '/imghp'




```python
result.params
```




    ''




```python
result.query
```




    'hl=ko&tab=wi'




```python
result.fragment
```




    ''




```python
bs.find('a')
```




    <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>




```python
bs.find('a', 'gb4')
```




    <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>




```python
bs.find('a', href='http://www.google.co.kr/history/optout?hl=ko')
```




    <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>




```python
bs.find({'class': 'gbh', 'style': 'left:0'})
```




    <style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}
    </style>




```python
bs.find_all('a')
```




    [<a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>,
     <a href="/advanced_search?hl=ko&amp;authuser=0">고급검색</a>,
     <a class="NKcBbd" href="https://www.google.com/url?q=https://about.google/stories/clean-air-for-kampala/%3Futm_source%3DGoogle%26utm_medium%3DHPP%26utm_campaign%3DEngineer_Story&amp;source=hpp&amp;id=19019758&amp;ct=3&amp;usg=AFQjCNELzKzOJb0K6uO7sQD914KHywgjDQ&amp;sa=X&amp;ved=0ahUKEwizlIrpl7TrAhURL6YKHSW9DZYQ8IcBCAU" rel="nofollow">우간다의 대기 오염을 줄이기 위해 AI를 활용하는 연구팀을 만나보세요</a>,
     <a href="/intl/ko/ads/">광고 프로그램</a>,
     <a href="http://www.google.co.kr/intl/ko/services/">비즈니스 솔루션</a>,
     <a href="/intl/ko/about.html">Google 정보</a>,
     <a href="https://www.google.com/setprefdomain?prefdom=KR&amp;prev=https://www.google.co.kr/&amp;sig=K_mU3ypo-7wCbCBi5ZAHZnf8iHSTc%3D">Google.co.kr</a>,
     <a href="/intl/ko/policies/privacy/">개인정보처리방침</a>,
     <a href="/intl/ko/policies/terms/">약관</a>]




```python
# 여러 속성을 한번에 검색한다. (방법 1: [], (), {} 모두 가능)
bs.find_all('a', {'class': ['gb1', 'gb4']})
```




    [<a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>]




```python
# 여러 속성을 한번에 검색한다. (방법 2: [], (), {} 모두 가능)
bs.find_all('a', class_=('gb1', 'gb4'))
```




    [<a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>]




```python
# 여러 속성을 한번에 검색한다. (방법 3: [], (), {} 모두 가능)
bs.find_all('a', {'gb1', 'gb4'})
```




    [<a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>]




```python
# 여러 속성을 한번에 검색한다. (방법 3: [], (), {} 모두 가능)
bs.find_all('', {'gb4', 'gb1'})
```




    [<b class="gb1">검색</b>,
     <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>]




```python
# 여러 태그를 검색한다. ([], (), {} 모두 가능)
bs.find_all({'title', 'a'})
```




    [<title>Google</title>,
     <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>,
     <a class="gb1" href="https://maps.google.co.kr/maps?hl=ko&amp;tab=wl">지도</a>,
     <a class="gb1" href="https://play.google.com/?hl=ko&amp;tab=w8">Play</a>,
     <a class="gb1" href="https://www.youtube.com/?gl=KR&amp;tab=w1">YouTube</a>,
     <a class="gb1" href="https://news.google.com/?tab=wn">뉴스</a>,
     <a class="gb1" href="https://mail.google.com/mail/?tab=wm">Gmail</a>,
     <a class="gb1" href="https://drive.google.com/?tab=wo">드라이브</a>,
     <a class="gb1" href="https://www.google.co.kr/intl/ko/about/products?tab=wh" style="text-decoration:none"><u>더보기</u> »</a>,
     <a class="gb4" href="http://www.google.co.kr/history/optout?hl=ko">웹 기록</a>,
     <a class="gb4" href="/preferences?hl=ko">설정</a>,
     <a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>,
     <a href="/advanced_search?hl=ko&amp;authuser=0">고급검색</a>,
     <a class="NKcBbd" href="https://www.google.com/url?q=https://about.google/stories/clean-air-for-kampala/%3Futm_source%3DGoogle%26utm_medium%3DHPP%26utm_campaign%3DEngineer_Story&amp;source=hpp&amp;id=19019758&amp;ct=3&amp;usg=AFQjCNELzKzOJb0K6uO7sQD914KHywgjDQ&amp;sa=X&amp;ved=0ahUKEwizlIrpl7TrAhURL6YKHSW9DZYQ8IcBCAU" rel="nofollow">우간다의 대기 오염을 줄이기 위해 AI를 활용하는 연구팀을 만나보세요</a>,
     <a href="/intl/ko/ads/">광고 프로그램</a>,
     <a href="http://www.google.co.kr/intl/ko/services/">비즈니스 솔루션</a>,
     <a href="/intl/ko/about.html">Google 정보</a>,
     <a href="https://www.google.com/setprefdomain?prefdom=KR&amp;prev=https://www.google.co.kr/&amp;sig=K_mU3ypo-7wCbCBi5ZAHZnf8iHSTc%3D">Google.co.kr</a>,
     <a href="/intl/ko/policies/privacy/">개인정보처리방침</a>,
     <a href="/intl/ko/policies/terms/">약관</a>]




```python
# 키워드 매개변수를 사용하면 AND 필터가 된다.
bs.find_all(class_='gb4', target='_top')
```




    [<a class="gb4" href="https://accounts.google.com/ServiceLogin?hl=ko&amp;passive=true&amp;continue=https://www.google.com/&amp;ec=%0000000" id="gb_70" target="_top">로그인</a>]




```python
bs.find('a')
```




    <a class="gb1" href="https://www.google.co.kr/imghp?hl=ko&amp;tab=wi">이미지</a>




```python
bs.find('a').text
```




    '이미지'




```python
bs.find('a').string
```




    '이미지'




```python
bs.find('a').get_text()
```




    '이미지'




```python
# 화이트스페이스를 제거한다.
bs.find('a').get_text(strip=True)
```




    '이미지'


- - -

# THE END
