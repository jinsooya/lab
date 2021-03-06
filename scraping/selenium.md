- - -

# Selenium 입문

### A Short Introduction

* * *

**박 진 수** 교수  
Intelligent Data Semantics Lab  
Seoul National University


- - -

<h3>Table of Contents<span class="tocSkip"></span></h3>
<div class="toc"><ul class="toc-item"><li><span><a href="#Selenium-설치" data-toc-modified-id="Selenium-설치-1">Selenium 설치</a></span></li><li><span><a href="#Selenium-기초" data-toc-modified-id="Selenium-기초-2">Selenium 기초</a></span><ul class="toc-item"><li><span><a href="#페이지-방문" data-toc-modified-id="페이지-방문-2.1">페이지 방문</a></span></li><li><span><a href="#옵션-사용" data-toc-modified-id="옵션-사용-2.2">옵션 사용</a></span><ul class="toc-item"><li><span><a href="#옵션을-사용하지-않고-실행" data-toc-modified-id="옵션을-사용하지-않고-실행-2.2.1">옵션을 사용하지 않고 실행</a></span></li><li><span><a href="#옵션을-설정하여-크롬-브라우저를-렌더링하지-않고-백그라운드-모드로-실행" data-toc-modified-id="옵션을-설정하여-크롬-브라우저를-렌더링하지-않고-백그라운드-모드로-실행-2.2.2">옵션을 설정하여 크롬 브라우저를 렌더링하지 않고 백그라운드 모드로 실행</a></span></li></ul></li><li><span><a href="#속성" data-toc-modified-id="속성-2.3">속성</a></span></li><li><span><a href="#웹-페이지-요소-검색" data-toc-modified-id="웹-페이지-요소-검색-2.4">웹 페이지 요소 검색</a></span></li><li><span><a href="#입력-및-실행" data-toc-modified-id="입력-및-실행-2.5">입력 및 실행</a></span></li><li><span><a href="#입력-및-실행-:-고급편" data-toc-modified-id="입력-및-실행-:-고급편-2.6">입력 및 실행 : 고급편</a></span></li></ul></li><li><span><a href="#Selenium으로-다음(Daum)-사전에-접근" data-toc-modified-id="Selenium으로-다음(Daum)-사전에-접근-3">Selenium으로 다음(Daum) 사전에 접근</a></span><ul class="toc-item"><li><span><a href="#Lab-:-한국어-사전---검색한-단어의-의미-출력" data-toc-modified-id="Lab-:-한국어-사전---검색한-단어의-의미-출력-3.1">Lab : 한국어 사전 - 검색한 단어의 의미 출력</a></span></li><li><span><a href="#Lab-:-한국어-사전---검색한-단어와-단어의-의미-출력-및-저장" data-toc-modified-id="Lab-:-한국어-사전---검색한-단어와-단어의-의미-출력-및-저장-3.2">Lab : 한국어 사전 - 검색한 단어와 단어의 의미 출력 및 저장</a></span></li><li><span><a href="#Lab-:-다른-링크-클릭" data-toc-modified-id="Lab-:-다른-링크-클릭-3.3">Lab : 다른 링크 클릭</a></span></li></ul></li><li><span><a href="#Selenium으로-Merriam-Webster-사전에-접근" data-toc-modified-id="Selenium으로-Merriam-Webster-사전에-접근-4">Selenium으로 Merriam-Webster 사전에 접근</a></span><ul class="toc-item"><li><span><a href="#Lab-:-간단한-영영사전-만들기" data-toc-modified-id="Lab-:-간단한-영영사전-만들기-4.1">Lab : 간단한 영영사전 만들기</a></span></li></ul></li></ul></div>

# Selenium 설치


```python
!python -m pip install --upgrade selenium
!python -m pip install --upgrade bs4
!python -m pip install --upgrade tqdm
```


```python
import selenium, bs4, tqdm

print('Selenium version.........:', selenium.__version__)
print('BeautifulSoup4 version...:', bs4.__version__)
print('tqdm version.............:', tqdm.__version__)
```

Selenium을 사용하려면 크롬 웹 드라이버를 내려받아 설치해야 한다.
- 'Selenium'로 구글링한다.
    + https://chromedriver.chromium.org
- 자신의 운영체제에 맞춰 내려받으면 된다.
- 내려받은 드라이브를 사용하기 편리한 폴더에 저장한다.
    + 드라이브를 저장한 경로는 반드시 기억해야 한다.

Selenium 사용법에 대한 상세한 내용은 아래 URL을 참고한다.
- https://selenium-python.readthedocs.io/index.html
    

# Selenium 기초


```python
# Selenium에서 webdriver를 불러온다.
from selenium import webdriver
```

## 페이지 방문

`get()` 메소드를 사용하여 원하는 웹 페이지에 방문할 수 있다.
- 전달인자로 URL 주소를 문자열로 입력한다.


```python
# Selenium으로 파이썬 공식 사이트(https://www.python.org)에 접속한다.
browser = webdriver.Chrome(__TODO__)
__TODO__
```


컴퓨터 어딘가에 새로운 크롬이 실행되고 있을 것이니 확인한다.
- 화면 상단에 'Chrome이 자동화된 테스트 소프트웨어에 의해 제어되고 있습니다.'라는 문구가 있다.
- 이 브라우저는 코드로 움직이는 브라우저다.

**주의** : 크롬 드라이버로 생성하고 조작하는 브라우저는 코드를 작성할 때 혼선이 생길 수 있기 때문에 크롬 개발자 도구를 실행하는 것을 제외하고는 손으로 조작하면 안된다.


```python
# 화면을 캡처해서 저장한다.
__TODO__
```

**실행 결과**
<pre>True</pre>


```python
# 브라우저를 닫고 크롬 드라이버를 종료한다.
browser.quit()  # close & exit the chrome browser
```

## 옵션 사용

메리엄-웹스터(Merriam-Webster) 사전 웹 사이트에 접속하여 'python' 단어 뜻을 검색한다.
- https://www.merriam-webster.com/

### 옵션을 사용하지 않고 실행


```python
# --- 옵션 없이 selenium 크롬 드라이버를 실행하는 경우
from selenium import webdriver

# 크롬 드라이버를 생성한다.
browser = webdriver.Chrome(__TODO__)

# 메리엄-웹스터(Merriam-Webster) 사전 웹 사이트('https://www.merriam-webster.com')에 접속한다.
URL = 'https://www.merriam-webster.com'
__TODO__
```


```python
# 검색 창을 찾는다.
element = __TODO__

# 검색 단어인 'python'을 입력한다.
__TODO__

# 입력한 단어를 서버로 보낸다.
__TODO__
```


```python
# 단어의 뜻이 있는 부분을 찾아서 출력한다.
# 클라이언트 쪽 리다이렉트가 실행(자바스크립트) 되었기 때문에 오류가 난다.
new_element = element.find_element_by_class_name('dtText')
```

클라이언트 쪽 리다이렉트로 웹 페이지가 바뀐 경우를 처리하는 몇 가지 방법 중 대표적인 방법 두 개를 알아보자.


```python
# --- 방법 1 : BeautifulSoup의 메소드로 데이터를 추출한다.
# 클라이언트 쪽 리다이렉트가 일어나는 것을 최대 특정 시간 동안 기다린 후 웹 페이지 변화를 감지한다.
import bs4
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support    import expected_conditions as EC
from selenium.common.exceptions    import TimeoutException

try: # 리다이렉트가 일어나 패이지가 바뀔 때까지 (즉, 현재 요소가 사라질 떄까지) 최대 10초 기다란다.
    __TODO__
except TimeoutException as err:
    print('TimeoutException:', err)
    
# 리다이렉트 후 생성한 웹 페이지 소스를 가져온다.
html = __TODO__

# BeautifulSoup의 find 메소드로 단어의 뜻이 있는 부분을 찾아서 출력한다.
__TODO__
```

**실행 결과**
<pre>
: any of various large constricting snakes
</pre>


```python
# --- 방법 2 : Selenium의 메소드로 데이터를 추출한다.
# 클라이언트 쪽 리다이렉트가 일어나는 것을 최대 특정 시간 동안 기다린 후 헤당 요소가 보이면 처리한다.
from selenium.webdriver.common.by  import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support    import expected_conditions as EC
from selenium.common.exceptions    import TimeoutException

# 단어의 뜻이 있는 부분을 찾아서 출력한다.
try:  # 리다이렉트가 일어나 패이지가 바뀔 때까지 (즉, 해당 요소가 나타날 떄까지) 최대 10초 기다란다.
    new_element = __TODO__
    print(new_element.text)
except TimeoutException as err:
    print('TimeoutException:', err)
```

**실행 결과**
<pre>
: any of various large constricting snakes
</pre>


```python
# 현재 브라우저를 닫는다.
browser.close()
```

### 옵션을 설정하여 크롬 브라우저를 렌더링하지 않고 백그라운드 모드로 실행


```python
# --- 방법 1
# 크롬 브라우저를 렌더링하지 않고 백그라운드 모드(headless)로 실행하는 옵선을 설정하여 사용한다.
from selenium                          import webdriver
from selenium.webdriver.chrome.options import Options

options = Options() 
options.add_argument('--headless')  

# 실행 옵션을 설정한 크롬 드라이버를 생성한다.
browser = webdriver.Chrome(__TODO__)
```



```python
# --- 방법 2
# 크롬 브라우저를 렌더링하지 않고 백그라운드 모드(headless)로 실행하는 옵선을 설정하여 사용한다.
from selenium import webdriver

options = webdriver.ChromeOptions() 
options.add_argument('--headless')

# 실행 옵션을 설정한 크롬 드라이버를 생성한다.
browser = webdriver.Chrome(__TODO__)
```


```python
import bs4
from selenium.webdriver.common.by  import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support    import expected_conditions as EC
from selenium.common.exceptions    import TimeoutException

# 메리엄-웹스터(Merriam-Webster) 사전 웹 사이트('https://www.merriam-webster.com')에 접속한다.
__TODO__

# 검색 창을 찾는다.
element = __TODO__

# 검색 단어인 'python'을 입력한다.
__TODO__

# 입력한 단어를 서버로 보낸다.
__TODO__

try: # 리다이렉트가 일어나 패이지가 바뀔 때까지 (즉, 현재 요소가 사라질 떄까지) 최대 10초 기다란다.
    __TODO__
except TimeoutException as err:
    print('TimeoutException:', err)


# 리다이렉트 후 생성한 웹 페이지를 가져온다.
html = __TODO__

# BeautifulSoup의 find 메소드로 단어의 뜻이 있는 부분을 찾아서 출력한다.
__TODO__
```

**실행 결과**
<pre>
: any of various large constricting snakes
</pre>


```python
# 현재 브라우저를 닫는다.
browser.close()
```

## 속성

브라우즈는 다음과 같은 기본 속성을 제공한다.
- `.current_url` 
- `.title`
- `.page_source`


```python
from selenium import webdriver

# 크롬 드라이버를 생성한다.
browser = webdriver.Chrome(__TODO__)

# 다음(Daum) 영화 사이트(https://movie.daum.net)에 접속한다. 
URL = 'https:/movie.daum.net'
__TODO__
```



```python
# 현재 웹 페이지의 URL을 확인힌다.
__TODO__
```

**실행 결과**
<pre>
'https://movie.daum.net/main/new#slide-1-0'
</pre>


```python
# 현재 웹 페이지의 제목(title)을 확인한다.
__TODO__
```

**실행 결과**
<pre>
'홈 | 다음영화'
</pre>


```python
# 현재 웹 페이지 소스를 가져온다.
__TODO__
```

**실행 결과**
```
'<html lang="ko" class="os_mac chrome pc version_86_0_4240_198"><head>\n<meta charset="utf-8">\n<meta property="og:site_name" content="Daum 영화">\n<meta http-equiv="X-UA-Compatible" content="IE=edge">\n <title>홈 | 다음영화</title>\n\n\t<meta property="og:title" content="">\n\t\t\t<meta property="og:url" content="">\n\t\t\t\t<meta property="og:image" content="">\n\t\t\t<meta property="og:description" content="Daum영화에서 자세한 내용을 확인하세요!">\n<meta name="viewport" content="user-scalable=no, initial-scale=1.0, maximum-scale=1.0, m...'
```

## 웹 페이지 요소 검색

Selenium는 웹 페이지의 요소를 찾을 수 있는 다양한 메소드를 제공한다.
- https://selenium-python.readthedocs.io/locating-elements.html

검색한 첫 번째 요소를 반환하는 **8**개 메소드
- `.find_element_by_id()`
- `.find_element_by_name()`
- `.find_element_by_xpath()`
- `.find_element_by_link_text()`
- `.find_element_by_partial_link_text()`
- `.find_element_by_tag_name()`
- `.find_element_by_class_name()`
- `.find_element_by_css_selector()`

검색한 모든 요소를 리스트로 반환하는 **7**개 메소드
- `.find_elements_by_name()`
- `.find_elements_by_xpath()`
- `.find_elements_by_link_text()`
- `.find_elements_by_partial_link_text()`
- `.find_elements_by_tag_name()`
- `.find_elements_by_class_name()`
- `.find_elements_by_css_selector()`

그 외 유용한 메소드 
- `.find_element()`
- `.find_elements()`

Example usage:
```python
from selenium.webdriver.common.by import By

driver.find_element(By.XPATH, '//button[text()="Some text"]')
driver.find_elements(By.XPATH, '//button')
```

These are the attributes available for `By` class:
```python
ID = 'id'
XPATH = 'xpath'
LINK_TEXT = 'link text'
PARTIAL_LINK_TEXT = 'partial link text'
NAME = 'name'
TAG_NAME = 'tag name'
CLASS_NAME = 'class name'
CSS_SELECTOR = 'css selector'
```

**위치 지정자(locator)**
- 위치 지정자(locator)는 선택자(selector)와는 다르다. 
- 위치 지정자는 `By` 객체를 사용하는 추상 쿼리 언어다.
  + `By` 객체는 다양한 방법으로 사용할 수 있는데, 선택자를 만들 때도 쓸 수 있다.

위치 지정자와 `.find_element()` 메소드를 함께 사용하면 선택자를 만들 수 있다.

```python
driver.find_element(By.ID, 'content')
```

위 코드는 다음 코드와 같은 동작을 한다.

```python
driver.find_element_by_id('content')
```

위치 지정자가 필요하지 않으면 사용하지 않아도 된다. `import` 문도 하나 줄일 수 있다. 하지만 위치 지정자는 매우 유연하고 편리한 도구다.

**`By` 객체와 함께 사용할 수 있는 위치 지정자**
- `ID`
  + `id` 속성으로 요소를 찾는다.
- `CLASS_NAME`
  + `class` 속성으로 요소를 찾는다.
- `CSS_SELECTOR`
  + `class`, `id`, 태그 이름으로 요소를 찾는다.
  + 표기법은 각각 `.클래스이름`, `#id이름`, `#태그이름`이다.
- `LINK_TEXT`
  + 링크 텍스트로 `<a>` 태그를 찾는다.
  + 예) 링크 텍스터가 'Next'면, `(By.LINK_TEXT, 'Next')`로 선택할 수 있다.
- `PARTIAL_LINK_TEXT`
  + `LINK_TEXT` 와 비슷하지만 문자 열 일부의 일치 하는 텍스트를 찾는다.
- `NAME`
  + `name` 속성으로 요소를 찾는다. 폼을 다룰 때 편리하다.
- `TAG_NAME`
  + 태그 이름으로 요소를 찾는다.
- `XPATH`
  + XPath 표현식을 사용하여 요소를 찾는다.
  + XPath는 'XML Path'의 줄임말이다.
  + XML 문서의 일부분을 탐색하고 선택하는데 사용하는 쿼리 언어다.
  + `태그이름#id이름` 처럼 CSS 선택자와 비슷한 문법을 사용한다.
  + BeautifulSoup은 XPath를 지원하지 않는다.  

**XPath 문법**
- 루트 노드 대 루트 노드가 아닌 노드
  + `/div` 는 문서의 루트(뿌리)에 있는 `div` 노드만 선택한다.
  + `//div` 는 문서의 어디에 있든 모든 `div` 노드를 선택한다.
- 속성 선택
  + `//@href` 는 `href` 속성이 있는 모든 노드를 선택한다.
  + `//a[@href='https://google.com']`는 문서에서 구글을 가리키는 모든 링크를 선택한다.  
- 위치에 따른 노드 선택  
  + `(//a)[3]` 는 문서의 세 번째 링크를 선택한다.
    - XPath에서 노드의 인덱스는 **0** 이 아니라 **1** 부터 시작한다.
    - 노드 인덱스를 지정하는 `[]`sms `//` 보다 우선 순위가 높다.
  + `(//table)[last()]` 는 문서의 마지막 테이블을 선택한다.
  + `(//a)[position() < 3]` 는 문서의 처음 두 링크를 선택한다.
- 아스테리크(*)는 어떤 문자나 노드의 집합이든 선택하기 때문에 다양한 상황에서 사용할 수 있다.
  + `//table/tr/*` 는 모든 테이블에서 자기 자식 `tr` 태그를 선택한다.
    + `th` 와 `td` 를 같이 사용하는 테이블에서 모든 셀을 선택할 때 유용하다.
  + `//div[@*]` 는 속성이 하나라도 있는 모든 `div` 태그를 선택한다.


```python
# 검색창을 찾는다.
element = __TODO__
element
```

**실행 결과**
```
<selenium.webdriver.remote.webelement.WebElement (session="...", element="...")>
```

## 입력 및 실행

`send_keys()` 메소드를 활용하면 키보드로 내용을 입력하듯이 원하는 문자열이나 숫자를 창에 입력할 수 있다.
- *element*`.send_keys`(_*value_)
  + https://selenium-python.readthedocs.io/api.html?highlight=send_key#selenium.webdriver.remote.webelement.WebElement.send_keys

참고
- https://selenium-python.readthedocs.io/api.html?highlight=send_key#module-selenium.webdriver.remote.webelement


```python
# 검색창에 검색어를 입력한다.
__TODO__
```


```python
# 검색창을 실행한다.
__TODO__
```



```python
# 현재 웹 페이지의 제목(title)을 확인한다.
__TODO__
```

**실행 결과**
<pre>
'비긴어게인 – Daum 검색'
</pre>


```python
# 현재 웹 페이지 소스를 가져온다.
__TODO__
```

**실행 결과**
```
'<html xmlns="http://www.w3.org/1999/xhtml" lang="ko" class="mac chrome "><head profile="http://a9.com/-/spec/opensearch/1.1/">\n<meta http-equiv="content-Type" content="text/html;charset=utf-8">\n<meta http-equiv="X-UA-Compatible" content="IE=edge">\n<meta name="autocomplete" content="off">\n\n<meta name="referrer" content="always">\n\n<meta name="format-detection" content="telephone=no">\n<meta property="og:title" content="비긴어게인 – Daum 검색">\n<meta property="og:url" content="https://search.daum.net/searc...'
```


```python
# 검색한 영화의 다음 영화 링크 요소를 가져온다.
element = __TODO__
```



```python
type(element)
```


```python
element
```


```python
# 가져온 요소의 속성 중 'href'의 내용을 확인한다.
__TODO__
```

**실행 결과**
<pre>
'http://movie.daum.net/moviedb/main?movieId=80780'
</pre>


```python
# 해당 링크로 접속한다.
__TODO__
```



```python
# '평점'을 클릭하여 평점 화면으로 넘어간다.
__TODO__
```


## 입력 및 실행 : 고급편

영화 평점과 리뷰 코멘트를 수집한다.


```python
# --- 방법 1 : BeautifulSoup이 제공하는 메소드를 사용하는 방법
# 해당 페이지의 네티즌 평점과 리뷰를 출력한다. 
import bs4

bs = bs4.BeautifulSoup(__TODO__)
scores = bs.find_all(__TODO__)
reviews = bs.find_all(__TODO__)
```



```python
type(scores), type(reviews)
```


```python
scores
```


```python
for score in scores:
    print(score.text)
```


```python
reviews
```


```python
for review in reviews:
    print(review.get_text(strip=True))
```


```python
len(scores), len(reviews)
```

두 데이터의 길이가 다르다.

***해결할 빙법은?***


```python
review_tags = bs.find_all(__TODO__)
len(review_tags)
```

**실행 결과**
<pre>10</pre>


```python
# 영화 리뷰 평가 점수와 코멘트를 담을 리스트를 초기화 한다.
scores = []     # 네티즌 평가 점수
comments = []   # 네티즌 리뷰 코멘트

# 영화 리뷰 관련 모든 정보를 가져와서 리스트에 담는다.
for review_tag in review_tags:
    scores.append(__TODO__)
    review = __TODO__
    if review:  
        comments.append(__TODO__)
    else:  # 리뷰 코멘트가 없으면 빈 문자열을 추가한다.
        comments.append('')
else:
    print(len(scores), len(comments))        
    print(scores)
    print(comments)
```

**실행 결과** (실시간 정보를 가져오기 때문에 현재 결과는 다를 수 있다.)
<pre>
10 10
['9', '10', '1', '9', '10', '10', '9', '8', '9', '9']
['음악영화이면서 성장영화 여주인공이 자신의 삶을 쿨하게 선택해나가는 모습, 음악하는 친구들의 모습이 좋았다 루저는 없다 행복하게 내 삶을 선택하자', '감동그자체 .인생영화에 추가합니다.', '', '어쩌다 단체 관람한 상큼한 음악영화.\n상상속에서 악기편성하는게 재밌다. 뭔가 이루어질 듯 하다가 그냥 헤어지는 여운이 있다.', '좋아요...', '맘이 ..', '', '', '', '']
</pre>


```python
# --- 방법 2 : selenium이 제공하는 메소드를 사용하는 방법
from selenium.common.exceptions import NoSuchElementException

# 영화 리뷰 평가 점수와 코멘트를 담을 리스트를 초기화 한다.
scores = []    # 네티즌 평가 점수
comments = []   # 네티즌 리뷰 코멘트

# 영화 리뷰 관련 모든 정보를 가져와서 리스트에 담는다.
review_elems = __TODO__
for review_elem in review_elems:
    # --- 아래 방법은 결측치를 하나 하나 예외 처리를 하기 때문에 시간은 상대적으로 상당히 오래 걸릴 수 있다.
    scores.append(__TODO__)
    try:
        comments.append(__TODO__)
    except NoSuchElementException:
        comments.append('')
else:
    print(len(scores), len(comments))
    print(scores)
    print(comments)
```

**실행 결과** (실시간 정보를 가져오기 때문에 현재 결과는 다를 수 있다.)
<pre>
10 10
['9', '10', '1', '9', '10', '10', '9', '8', '9', '9']
['음악영화이면서 성장영화 여주인공이 자신의 삶을 쿨하게 선택해나가는 모습, 음악하는 친구들의 모습이 좋았다 루저는 없다 행복하게 내 삶을 선택하자', '감동그자체 .인생영화에 추가합니다.', '', '어쩌다 단체 관람한 상큼한 음악영화.\n상상속에서 악기편성하는게 재밌다. 뭔가 이루어질 듯 하다가 그냥 헤어지는 여운이 있다.', '좋아요...', '맘이 ..', '', '', '', '']
</pre>


```python
for i, score in enumerate(scores):
    print(f'{score}|{comments[i]}')    
```

***전체 리뷰 데이터를 다 가져오려면 어떻게 해야할까?***

**selenium**으로 하여금 리뷰 페이지 맨 아래에 있는 '평점 더보기' 버튼을 계속 눌러서 모든 내용을 펼친 후 데이터를 수집하면 된다.


```python
# --- Explicit Wait
from selenium.webdriver.common.by  import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support    import expected_conditions as EC
from selenium.common.exceptions    import TimeoutException

print('unfolding...')
print('click count:')
click = 0  # '평점 더보기' 버튼을 누른 횟수를 계산하기 위한 변수를 초기화한다.

# 리뷰 페이지 맨 아래에 있는 '평점 더보기' 버튼을 누른다,
# 첫 페이지는 10개의 리뷰를 보여준다.
# 버튼 한 개 누를 때마다 5개의 추가 리뷰를 보여준다.
XPATH = __TODO__
while True:
    try:  # 페이지가 너무 길어 필요하다면 충분히 30초 이상 대기 시간을 주는게 좋다.
        WebDriverWait(browser, 10).until(EC.presence_of_element_located(
            (By.XPATH, XPATH))).click()
        # --- 진행 상태를 보여준다.
        click += 1
        print(click) if click % 20 == 0 else print(click, end='|')
    except TimeoutException:  # '평점 더보기' 버튼이 없으면 중단한다.
        print('Done!')
        break
```

**실행 결과** (실시간 정보를 가져오기 때문에 현재 결과는 다를 수 있다.)
<pre>
unfolding...
click count:
1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20
21|22|23|24|25|26|27|28|29|30|31|32|33|34|35|36|37|38|39|40
41|42|43|44|45|46|47|48|49|50|51|52|53|54|55|56|57|58|59|60
61|62|63|64|65|66|67|68|69|70|71|72|73|74|75|76|77|78|79|80
81|82|83|84|85|86|87|88|89|90|91|92|93|94|95|96|97|98|99|100
101|102|103|104|105|106|107|108|109|110|111|112|113|114|115|116|117|118|119|120
121|122|123|124|125|126|127|128|129|130|131|132|133|134|135|136|137|138|139|140
141|142|143|144|145|146|147|148|149|150|151|152|153|154|155|156|157|158|159|160
161|162|163|164|165|166|167|168|169|170|171|172|173|174|175|176|177|178|179|180
181|182|183|184|185|186|187|188|189|190|191|192|193|194|195|196|197|198|199|200
201|202|203|204|205|206|207|208|209|210|211|212|213|214|215|216|217|218|219|220
221|222|223|224|225|226|227|228|229|230|231|232|233|234|235|236|237|238|239|240
241|242|243|244|245|246|247|248|249|250|251|252|253|254|255|256|257|258|259|260
261|262|263|264|265|266|267|268|269|270|271|272|273|274|275|276|277|278|279|280
281|282|283|284|285|286|287|288|289|290|291|292|293|294|295|296|297|298|299|300
301|302|303|304|305|306|307|308|309|310|311|312|313|314|315|316|317|318|319|320
321|322|323|324|325|326|327|328|329|330|331|332|333|334|335|336|337|338|339|Done!
</pre>


```python
# --- 방법 1 : BeautifulSoup이 제공하는 메소드를 사용하는 방법
import bs4
from tqdm import tqdm

bs = bs4.BeautifulSoup(__TODO__)

# 영화 리뷰 평가 점수와 코멘트를 담을 리스트를 초기화 한다.
scores = []     # 네티즌 평가 점수
comments = []   # 네티즌 리뷰 코멘트

# 영화 리뷰 관련 모든 정보를 가져와서 리스트에 담는다.
review_tags = __TODO__
for review_tag in tqdm(review_tags):
    scores.append(__TODO__)
    review = __TODO__
    if review:  
        comments.append(__TODO__)
    else:  # 리뷰 코멘트가 없으면 민 문자열을 추가한다.
        comments.append('')
else:
    browser.quit()
    print('\n--- Job completed!', f'총 {len(review_tags):,}개의 리뷰 데이터를 수집했습니다.', '-' * 11, '\n')     
```

**실행 결과** (실시간 정보를 가져오기 때문에 현재 결과는 다를 수 있다.)
```
100%|██████████| 1701/1701 [00:00<00:00, 14027.25it/s]

--- Job completed! 총 1,701개의 리뷰 데이터를 수집했습니다. ----------- 
```


```python
for i, score in enumerate(scores[:10]):
    print(f'{score}|{comments[i]}')    
```


```python
# --- 방법 2 : selenium이 제공하는 메소드를 사용하는 방법
from tqdm import tqdm
from selenium.common.exceptions import NoSuchElementException

# 영화 리뷰 데이터를 담을 리스트를 모두 초기화 한다.
scores = []     # 네티즌 평가 점수
comments = []   # 네티즌 리뷰 코멘트

# 영화 리뷰 관련 모든 정보를 가져와서 리스트에 담는다.
review_elems = __TODO__
for review_elem in tqdm(review_elems):
    # --- 아래 방법은 결측치를 하나 하나 예외 처리를 하기 때문에 시간은 상대적으로 상당히 오래 걸릴 수 있다.
    scores.append(__TODO__)
    try:
        comments.append(__TODO__)
    except NoSuchElementException:
        comments.append('')
else:
    browser.quit()
    print('\n--- Job completed!', f'총 {len(review_elems):,}개의 리뷰 데이터를 수집했습니다.', '-' * 11, '\n')     
```

**실행 결과** (실시간 정보를 가져오기 때문에 현재 결과는 다를 수 있다.)
```
100%|██████████| 1701/1701 [01:35<00:00, 17.84it/s]

--- Job completed! 총 1,701개의 리뷰 데이터를 수집했습니다. ----------- 
```


```python
for i, score in enumerate(scores[:10]):
    print(f'{score}|{comments[i]}')    
```

# Selenium으로 다음(Daum) 사전에 접근

- https://dic.daum.net/


```python
# Selenium에서 webdriver를 불러온다.
from selenium import webdriver

# 크롬 드라이브를 불러온다. 
browser = webdriver.Chrome(__TODO__)

# Selenium으로 다음 사전 웹사이트에 접속한다.
browser.get('https://dic.daum.net/')
```


```python
# 검색창을 찾는다.
element = browser.find_element_by_name('q')

# 검색창에 'python'을 입력한다.
element.send_keys('python')

# 검색창을 실행한다.
element.submit()
```


```python
# 현재 브라우저를 닫는다.
browser.close()
```

## Lab : 한국어 사전 - 검색한 단어의 의미 출력

- - -

다음 한국어 사전에 접속하여 '온톨로지' 단어를 검색한 결과 화면의 가장 상단에 나타나는 단어의 의미(meaning)을 출력한다.
- https://dic.daum.net/index.do?dic=kor

- - -

**실행 결과**
<pre>> python dict_daum_KOR_word_meaning.py
존재 또는 존재의 근본적ㆍ보편적인 모든 규정을 연구하는 학문.
</pre>


```python
# Your answer here
```

## Lab : 한국어 사전 - 검색한 단어와 단어의 의미 출력 및 저장

- - -

다음 어학 사전('전체')에 접속하여 '인공지능', '온톨로지', '기계학습'  단어를 검색한 결과 해당 단어와 함께 화면의 가장 상단에 나타나는 단어의 의미(meaning)를 화면으로 출력하고 텍스트 파일로 저장한다.
- https://dic.daum.net

- - -

**실행 결과**
<pre>> python dict_daum_KOR_word_meaning_file.py
인공지능 : 판단, 추론, 학습 등 인간의 지능이 가지는 기능을 갖춘 컴퓨터 시스템
온톨로지 : 존재 또는 존재의 근본적ㆍ보편적인 모든 규정을 연구하는 학문.
기계학습 : 인간이 자연적으로 수행하는 학습 능력과 같은 기능을 컴퓨터에서 실현하려는 기술이나 방법. 인공 지능 분야의 연구 과제 가운데 하나이다.

위 내용을 'daum-dict-KOR.txt'로 저장하였습니다.
</pre>


```python
# Your answer here
```

## Lab : 다른 링크 클릭

- - -

다음 어학 사전('전체')에 접속한 후 화면의 상단에 있는 **[단어장]**을 클릭하여 '공개단어장' 화면이 나오도록 한다.
- https://dic.daum.net

- - -


```python
# Your answer here
```

# Selenium으로 Merriam-Webster 사전에 접근

- https://www.merriam-webster.com


```python
# Selenium에서 webdriver를 불러온다.
from selenium import webdriver

# Selenium으로 Merriam-Webster 사전 웹사이트에 접속한다.
browser = webdriver.Chrome(__TODO__)
browser.get('https://www.merriam-webster.com')
```


```python
# 검색 창의 속성 'name'의 값을 확인한다.
search_box = browser.find_element_by_name('s')

# 검색 창에 'python'을 입력한다.
search_box.send_keys('python')

# Selenium으로 검색 창 버튼을 누르는 동작을 지시한다.
search_box.submit()
```


```python
# 현재 브라우저를 닫고 크롬 드라이버를 종료한다.
browser.quit()
```

## Lab : 간단한 영영사전 만들기

- - -

메리엄-웹스터(Merriam-Webster) 사전 웹 사이트에 접속하여 'python', 'anaconda', 'cobra', 'rattlesnake'이란 단어를 검색한 결과 해당 단어와 함께 화면의 가장 상단에 나타나는 단어의 의미(meaning)를 텍스트 파일로 저장한다.
- https://www.merriam-webster.com

- - -

**실행 결과**
<pre>> python mwdictionary_file.py
수집한 데이터를 'dictionary-selenium.txt'로 저장하였습니다.
</pre>


```python
# Your answer here
```

- - -

# THE END
