- - -

# 파이썬에서의 데이터베이스 활용 : sqlite3

### Python Database: sqlite3 

* * *

**박 진 수** 교수  
Intelligent Data Semantics Lab  
Seoul National University

- - -

<div align='right'><font size='-1'>[partial credit: 이일주 연구원]</font></div>

<h3>Table of Contents<span class="tocSkip"></span></h3>
<div class="toc"><ul class="toc-item"><li><span><a href="#Python-DB-API-2.0" data-toc-modified-id="Python-DB-API-2.0-1">Python DB-API 2.0</a></span></li><li><span><a href="#sqlite3" data-toc-modified-id="sqlite3-2">sqlite3</a></span></li><li><span><a href="#sqlite3-설치-및-불러오기" data-toc-modified-id="sqlite3-설치-및-불러오기-3">sqlite3 설치 및 불러오기</a></span></li><li><span><a href="#데이터베이스-연결" data-toc-modified-id="데이터베이스-연결-4">데이터베이스 연결</a></span></li><li><span><a href="#커서-생성" data-toc-modified-id="커서-생성-5">커서 생성</a></span></li><li><span><a href="#테이블-생성" data-toc-modified-id="테이블-생성-6">테이블 생성</a></span></li><li><span><a href="#데이터-입력" data-toc-modified-id="데이터-입력-7">데이터 입력</a></span><ul class="toc-item"><li><span><a href="#execute()-메소드" data-toc-modified-id="execute()-메소드-7.1"><strong>execute()</strong> 메소드</a></span></li><li><span><a href="#executemany()-메소드" data-toc-modified-id="executemany()-메소드-7.2"><strong>executemany()</strong> 메소드</a></span></li><li><span><a href="#executescript()-메소드" data-toc-modified-id="executescript()-메소드-7.3"><strong>executescript()</strong> 메소드</a></span></li></ul></li><li><span><a href="#데이터-열람" data-toc-modified-id="데이터-열람-8">데이터 열람</a></span><ul class="toc-item"><li><span><a href="#fetchone()-메소드" data-toc-modified-id="fetchone()-메소드-8.1"><strong>fetchone()</strong> 메소드</a></span></li><li><span><a href="#fetchmany()-메소드" data-toc-modified-id="fetchmany()-메소드-8.2"><strong>fetchmany()</strong> 메소드</a></span></li><li><span><a href="#fetchall()-메소드" data-toc-modified-id="fetchall()-메소드-8.3"><strong>fetchall()</strong> 메소드</a></span></li><li><span><a href="#Cursor-클래스-속성-description" data-toc-modified-id="Cursor-클래스-속성-description-8.4"><strong>Cursor</strong> 클래스 속성 <strong>description</strong></a></span></li></ul></li><li><span><a href="#Lab:-sqlite3-활용" data-toc-modified-id="Lab:-sqlite3-활용-9">Lab: <strong>sqlite3</strong> 활용</a></span></li></ul></div>

# Python DB-API 2.0

여러 종류 데이터베이스의 파이썬 인터페이스 표준이다.
- 데이터베이스 연결, SQL 실행, 파라미터, 에러 코드 등과 같이 데이터베이스 사용에 관련된 API
- [PEP 249 -- Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/)


**Module Interface**
- **connect(*parameters...*)**: 데이터베이스에 연결하여 **Connection** 객체를 반환한다.
- **Exceptions**: Warning, Error 등을 정의한다.

**Connection Objects**
- **close()**: 데이터베이스와의 연결을 해제한다.
- **commit()**: 트랜잭션을 커밋한다.
- **rollback()**: 트랜잭션을 취소하고 롤백한다.
- **cursor()**: 커서를 생성하여 반환한다.

**Cursor Objects**
- **execute(*sql,[,parameters]*)**: 쿼리를 수행한다.
- **executemany(*sql, seq_of_param*)**: 쿼리를 수행한다.
- **fetchone()**: 결과를 가져온다.
- **fetchmany(*size = cursor.arraysize*)**: 결과를 가져온다.
- **fetchall()**: 결과를 가져온다.

# sqlite3

**sqlite3**란?
- 오픈소스 데이터베이스인 SQLite의 파이썬 모듈이다.
- 자세한 내용은 아래 링크를 참조하면 된다.
    - [sqlite3 — DB-API 2.0 interface for SQLite databases](https://docs.python.org/3/library/sqlite3.html)
    - [PEP 249 -- Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/)


# sqlite3 설치 및 불러오기

파이썬은 SQLite(**sqlite3**)가 내장되어 있어 따로 설치할 필요가 없다. 하지만 데이터베이스를 구축하려면 SQLite를 설치해야 한다. 아래 링크에서 최신 SQLite를 내려받는다.
- http://www.sqlite.org/download.html


```python
import sqlite3
```

# 데이터베이스 연결

데이터베이스를 사용하려면 먼저 데이터베이스와 연결을 해야한다.

<pre>sqlite3.connect('데이터베이스이름경로')</pre>

- '데이터베이스이름경로'가 기존에 있다면 경로에 있는 기존 데이터베이스를 연결하고, 기존 데이터베이스가 없다면 새로 데이터베이스를 생성한 후 연결한다. 
- '데이터베이스이름경로'에 데이터베이스 파일 이름만 설정하면 현재 작업 디렉토리의 데이터베이스를 연결한다.
- '데이터베이스이름경로'에 파일 경로와 데이터베이스 파일 이름을 같이 설정하면 해당 폴더(절대경로 또는 상대결로)의 데이터베이스를 연결한다.


```python
# 현재 작업 폴더의 하위 폴더인 'data' 폴더의 'company.db' 데이터베이스에 연결한다.
# 'company.db'가 존재하면 기존 'company.db'에 연결하고, 없다면 새로 'company.db'를 만든 후 연결한다.
# 변수 conn에 이 데이터베이스의 인스턴스를 할당한다.
# 연결에 성공하면 아무런 메시지도 출력하지 않는다.
conn = __TODO__
```

**실행 결과**


```python
# conn의 내용을 출력해본다. 
print(conn)
```

**실행 결과**

```
<sqlite3.Connection object at 0x7f9af86417b0>
```

# 커서 생성

연결한 데이터베이스를 대상으로 SQL 문을 실행하거나 실행한 결과를 돌려 받으려면 커서(cursor)를 생성해야 한다. 물론 커서 없이도 연결한 데이터베이스 객체를 통해 SQL 문을 실행할 수 있지만, 커서는 데이터베이스로부터 돌려받은 결과 데이터를 처리할 때 사용한다. 커서는 데이터를 순회할 수 있는 제어 구조로 현재 위치를 포함한다. 


```python
cursor = __TODO__
cursor
```

**실행 결과**

```
<sqlite3.Cursor at 0x7f9af8697a40>
```

# 테이블 생성

SQL 문을 실행하려면 **execute()** 메소드를 실행하면 된다. *connection*을 사용하면 따로 커서를 생성할 필요가 없다. **execute()** 메소드는 잠시 후 다시 설명하기로 한다.

- <pre>cursor.execute(sql [, optional parameters])</pre>
- <pre>connection.execute(sql [, optional parameters])</pre>


```python
# --- DDL
# Department TABLE
#   did =>    INTEGER, PRIMARY KEY, AUTOINCREMENT
#   dname =>  TEXT
#   floor =>  TEXT
#
# Employee TABLE
#   eid =>    INTEGER, PRIMARY KEY, AUTOINCREMENT
#   fname =>  TEXT
#   lname =>  TEXT
#   did =>    INTEGER, FOREIGN KEY of Department(did)
#   gender => TEXT
#   salary => INTEGER

ddl_dept = __TODO__

ddl_emp = __TODO__
```

앞서 작성한 'Department' 테이블을 정의한 SQL 문을 **Connection** 객체를 사용하여 실행해보자.


```python
# --- Department 테이블을 생성하다.
# 데이터베이스 연결 객체로 Department 테이블을 생성한다.
conn.__TODO__

# commit()을 하지 않아도 테이블은 저장되지만 항상 commit을 하는 습관을 가지는 것이 좋다.
conn.__TODO__ 

# 연결을 종료한다.
conn.__TODO__
```

이번에는 'Employee' 테이블을 **Cursor** 객체를 사용하여 실행해보자. 그리고 보다 안전한 방법으로 SQL 문을 실행하기 위해 **try-except-finally** 문을 사용하여 코드를 작성한다.


```python
# --- Employee 테이블을 생성하다.
# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    cursor = conn.__TODO__
    
    # 커서로 Employee 테이블을 생성한다.
    cursor.__TODO__
    
    # commit()을 하지 않아도 테이블은 저장되지만 
    # 항상 commit을 하는 습관을 가지는 것이 좋다.
    # [주의] commit()은 Connection 메소드다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

# 데이터 입력

## **execute()** 메소드

**execute**(*sql [, optional parameters]*) : **하나**의 SQL 문을 실행한다. *connection*을 사용하면 따로 커서를 생성할 필요가 없다.
- <pre>cursor.execute(sql [, optional parameters])</pre>
- <pre>connection.execute(sql [, optional parameters])</pre>

데이터를 입력하는 방법으로 여러 가지가 있다. 먼저 SQL 문을 직접 입력해서 실행해보자. **Cursor**를 통해 실행할 수도 있지만 여기서는 우선 **Connection** 객체를 통해 실행해본다.


```python
# 먼저 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)
```


```python
# --- SQL문을 직접 입력한다.
# Department 테이블에 부서 이름을 'Finance'로 부서 위치를 '10F'로 입력한다.
conn.__TODO__
```

바로 앞의 SQL 문을 실행한 후 SQLite를 열어 'company.db'의 'Department' 테이블을 조회하면 아직 데이터가 입력되지 않았음을 알 수 있다. 이는 지금까지 입력한 데이터는 아직 데이터베이스에 완전히 저장한 것이 아니라 임시로 저장한 상태인 것이다. 데이터베이스에 확실히 저장을 하려면 **Connection.commit()** 을 실행해야한다. 참고로 **Connection.rollback()** 은 **Connection.commit()** 이후의 모든 트랜잭션을 취소하고 **Connection.commit()** 했을 때의 상태로 되돌아간다.

**[주의]**   
**CREATE TABLE**의 경우는 **commit()** 을 하지 않아도 테이블이 생성되지만 테이블이 담고 있는 데이터를 추가/삭제/수정 할 때는 반드시 **commit()** 을 해야한다.


```python
# 실행한 SQL 결과를 데이터베이스에 반영한다.
conn.commit()
```


```python
# 데이터베이스 연결을 종료한다.
conn.close()
```

지금부터는 **Connection** 대신 **Cursor** 객체를 사용해서 SQL 문을 실행하도록 한다. [PEP 249 -- Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/#cursor-methods)에서도 **Cursor**의 메소드를 사용해서 SQL 문을 실행할 것을 권장하고 있다.

이번에는 placeholder를 사용하여 SQL 문을 실행해보자. placeholder는 두 종류가 있다.
- ? placeholder
- Named placeholder


```python
# --- Department 테이블에 다음 내용을 각각 부서 이름과 부서 위치로 입력한다.
# > 'Sales', '9F'
# > 'Research', '9F'
# > 'HR', '10F'
# > 11, 'Marketing', '10F'

# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    # 커서는 SQL문을 실행하고 결과의 현재 위치를 알고 있다.
    cursor = conn.cursor()
    
    # --- '? placeholder'를 사용하여 SQL문을 실행한다.
    # > 'Sales', '9F'
    # > 'Research', '9F'
    cursor.execute(__TODO__)
    cursor.execute(__TODO__)

    # --- 'named placeholder' 를 사용하여 SQL문을 실행한다.
    # 전달인자로 딕셔너리가 온다.
    # > 'HR', '10F'
    cursor.execute(__TODO__)

    # %%% 커밋을 하여 지금까지의 업데이트를 데이터베이스에 반영한다. %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    # [주의] commit()은 Connection 메소드다.
    conn.commit()
    
    # 다섯 번째 데이터는 SQL문을 직접 입력하여 추가한다. 이 때 did는 11로 한다.
    # > 11, 'Marketing', '10F'
    cursor.execute(__TODO__)
                    
    # %%% 롤백을 하여 가장 최근 커밋 이후의 모든 작업을 취소한다. %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
    # [주의] rollback()은 Connection 메소드다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

바로 앞의 SQL 문을 실행한 후 SQLite를 열어 'company.db'의 'Department' 테이블을 조회하면 마지막에 입력한 데이터인 **(11, 'Marketing', '10F')** 를 저장하지 않았음을 알 수 있다. 이는 첫 번째 커밋 이후 작업을 롤백 했기 때문에 마지막 데이터 입력은 취소하고 첫 번째 커밋을 한 상태로 돌아 갔기 때문이다.

***만약 기존에 있는 테이블과 동일한 이름의 테이블을 만들면 어떻게 될까?***


```python
# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    # 커서는 SQL문을 실행하고 결과의 현재 위치를 알고 있다.
    cursor = __TODO__
    
    # 기존에 있는 테이블과 동일한 이름의 테이블을 생성한다.
    cursor.execute(__TODO__)

    # [주의] commit()은 Connection 메소드다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

**실행 결과**

<pre>
SQLite ERROR: table Department already exists
</pre>

***만약 주키가 같은 데이터를 입력하면 어떻게 될까?***


```python
# 데이터베이스에 연결한다.
# 주키가 1인 데이터를 입력한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    # 커서는 SQL문을 실행하고 결과의 현재 위치를 알고 있다.
    cursor = __TODO__
    
    # 기존에 있는 테이블과 동일한 이름의 테이블을 생성한다.
    # > 1, 'HR', '10F'
    cursor.execute(__TODO__)

    # [주의] commit()은 Connection 메소드다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

**실행 결과**

<pre>
SQLite ERROR: UNIQUE constraint failed: Department.did
</pre>

## **executemany()** 메소드

**executemany**(*sql, seq_of_parameters*) : *seq_of_param*에 있는 모든 매개변수 시퀀스나 매핑에 대하여 SQL문을 실행한다. *connection*을 사용하면 따로 커서를 생성할 필요가 없다.
- <pre>cursor.executemany(sql, seq_of_parameters)</pre>
- <pre>connection.executemany(sql[, parameters])</pre>


```python
# --- Department 테이블에 다음 내용을 각각 부서 이름과 부서 위치로 입력한다.
# > 'Finance', '10F'
# > 'Sales', '9F'
# > 'Research', '9F'
# > 'HR', '10F'

# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    # 커서는 SQL문을 실행하고 결과의 현재 위치를 알고 있다.
    cursor = __TODO__
    
    # --- 실습을 위해 테이블을 새로 생성한다.
    cursor.execute('''DROP TABLE IF EXISTS Department;''')
    cursor.execute(ddl_dept)
    
    # --- executemany()로 데이터를 입력한다.
    # > 'Finance', '10F'
    # > 'Sales', '9F'
    # > 'Research', '9F'
    # > 'HR', '10F'
    stmt = '''INSERT INTO Department(dname, floor) VALUES(?, ?);'''
    seq_of_params = [__TODO__]
    cursor.executemany(__TODO__)

    # 트랜잭션(작업)을 커밋한다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

## **executescript()** 메소드

**executescript**(*sql_script*) : 스크립트 형식으로 제공된 여러 SQL 문인 *sql_script*를 한 번에 실행한다. *connection*을 사용하면 따로 커서를 생성할 필요가 없다.
- <pre>cursor.executescript(sql_script)</pre>
- <pre>connection.executescript(sql_script)</pre>


```python
# --- Department 테이블에 다음 내용을 각각 부서 이름과 부서 위치로 입력한다.
# > 'Finance', '10F'
# > 'Sales', '9F'
# > 'Research', '9F'
# > 'HR', '10F'

# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

# 각 SQL문은 ; 문자로 구분해야 한다.
stmts = '''DROP TABLE IF EXISTS Department;
CREATE TABLE Department(__TODO_);
INSERT INTO Department(dname, floor) VALUES __TODO__;
'''

try:
    # 커서를 생성한다.
    # 커서는 SQL문을 실행하고 결과의 현재 위치를 알고 있다.
    cursor = __TODO__
    
    # --- executescript()로 SQL문 script를 실행한다.
    # 각 SQL문은 ; 문자로 구분해야 한다.
    cursor.executescript(stmts)
    
    # 트랜잭션(작업)을 커밋한다.
    __TODO__
except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

# 데이터 열람

## **fetchone()** 메소드

**fetchone**() : 질의 결과 세트의 다음 행(row)을 튜플 자료형으로 하나씩 반환한다. 반환할 데이터가 (더 이상) 없으면 **None**을 반환한다.
- <pre>cursor.fetchone()</pre>


```python
# --- Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    cursor = __TODO__
    
    # Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
    cursor.execute(__TODO__)
    
    row = cursor.fetchone()
    print('fetchone()이 번환한 객체의 자료형:', type(row))
    # while문을 사용하여 데이터를 하나씩 출력한다.
    __TODO__

except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

**실행 결과**

```
fetchone()이 번환한 객체의 자료형: <class 'tuple'>
(2, 'Sales', '9F')
(3, 'Research', '9F')
```

데이터 열람을 할 경우에는 입력이나 변경이 아니므로 굳이 커밋을 할 필요는 없다

## **fetchmany()** 메소드

**fetchmany**([*size=cursor.arraysize*]) : 질의 결과 세트의 다음 행(row) 세트를 ***size*** 개수만큼 튜플을 담고 있는 리스트 자료형으로 반환한다. 반환할 데이터가 (더 이상) 없으면 빈 리스트를 반환한다. ***size*** 를 설정하지 않으면 **fetchone()** 처럼 다음 행(row) 하나를 반환하는데 튜플이 아니라 튜플 하나를 담은 리스트를 반환한다.
- <pre>cursor.fetchmany([size = cursor.arraysize]))</pre>


```python
# --- Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    cursor = __TODO__
    
    # Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
    cursor.execute(__TODO__)
    
    rows = cursor.fetchmany(5)
    
    # for문을 사용하여 데이터를 하나씩 출력한다.
    __TODO__
    
    
    print('--- Fetch completed! -------')

    rows = cursor.fetchmany(1)   # 데이터가 남아있는지 확인한다.
    print(rows)

except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

**실행 결과**

<pre>
(2, 'Sales', '9F')
(3, 'Research', '9F')
--- Fetch completed! -------
[]
</pre>

## **fetchall()** 메소드

**cursor.fetchall()** : 
질의 결과 세트의 (남은) 모든 행(row) 세트를 튜플을 담고 있는 리스트 자료형으로 반환한다. 사용 가능한 행이 없으면 빈 리스트를 반환한다.
- <pre>cursor.fetchall()</pre>


```python
# --- Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
# 데이터베이스에 연결한다.
conn = sqlite3.connect(__TODO__)

try:
    # 커서를 생성한다.
    cursor = __TODO__
    
    # Department 테이블에서 9층에 위치한 모든 부서를 조회한다.
    cursor.execute(__TODO__)
    
    rows = cursor.fetchall()
    
    # for문을 사용하여 데이터를 하나씩 출력한다.
    __TODO__
    
    
    print('--- Fetch completed! -------')

    rows = cursor.fetchall()
    print(rows)

except sqlite3.Error as err:
    print('SQLite ERROR:', err)
finally:  
    conn.close()  
```

**실행 결과**

<pre>
(2, 'Sales', '9F')
(3, 'Research', '9F')
--- Fetch completed! -------
[]
</pre>

## **Cursor** 클래스 속성 **description**

**Cursor** 클래스의 속성 중 **description**는 실행 결과 각 필드(컬럼)에 대한 **7**개의 정보를 담고 있다.
- <pre>name, type_code, display_size, internal_size, precision, scale, null_ok</pre>    


```python
conn = sqlite3.connect('data/company.db')
cursor = conn.cursor()
cursor.execute('''SELECT * FROM Department WHERE floor = '9F';''')
rows = cursor.fetchall()
```




    <sqlite3.Cursor at 0x7fb040140c00>




```python
# Cursor 클래스의 description 속성은 마지막 SQL문을 실행하고 가져온 데이터의 각 필드(컬럼)에 대한 정보를 담고 있다. 
# 이 중 각 튜플의 첫 번째 객체가 필드명이다.
__TODO__
```

**실행 결과**

<pre>
(('did', None, None, None, None, None, None),
 ('dname', None, None, None, None, None, None),
 ('floor', None, None, None, None, None, None))
</pre>


```python
# Cursor.description에서 테이블의 필드명만 추출한다.
__TODO__
```

**실행 결과**

<pre>
('did', 'dname', 'floor')
</pre>

# Lab: **sqlite3** 활용

다음 조건을 만족하는 코드를 작성한다.
- SQL **INSERT** 문은 **executemany()** 메소드를 사용한다.
- SQL **SELECT** 문을 실행한 결과는 **fetchall()** 을 사용하여 출력한다.

**STEP 1**: **CREATE** 문을 사용하여 아래 테이블 'Employee'를 생성한다.
- eid: INTEGER
- fname: TEXT
- lname: TEXT
- did: INTEGER
- gender: TEXT
- salary: INTEGER

이 때 'eid'를 주키로 하고 필드값을 AUTOINCREMENT로 설정한다. 'did'는 외래키이며 'Department'의 주키를 참조하도록 한다.

**STEP 2**: **INSERT** 문을 사용하여 아래 표에 나타난 8개의 레코드를 입력한다.

|eid|fname|lname|did|gender|salary|
|-|-----|-----|-----|-----|-----|
|1 | Brad | Nash | 3 | M | 30000|
|2 | Franklin | Smith | 2 | M | 40000|
|3 | Nicole | Kim | 1 | F | 25000|
|4 | Anna | Mills | 3 | F | 43000 |
|5 | Tim | Allen | 3 | M | 38000 |
|6 | Jennifer |Grey | 4 | F | 35000 |
|7 | Tony | Parker | 2 | M | 25000 |
|8 | James | Wong | 1 | M | 45000 |

**STEP 3**: 다음을 질의하는 SQL을 작성하여 실행하고 결과를 출력한다.
- 연봉이 30,000불 이상인 직원들의 fname, lname, salary를 열람한다.

| fname | lname | salary |
|-----|-----|-----|
| Brad | Nash | 30000 |
| Franklin | Smith | 40000 |
| Anna | Mills |43000 |
| Tim | Allen | 38000 |
| Jennifer | Grey | 35000 |
| James | Wong | 45000 |

**실행 예**

<pre>> python employee_over_30000.py
('Brad', 'Nash', 30000)
('Franklin', 'Smith', 40000)
('Anna', 'Mills', 43000)
('Tim', 'Allen', 38000)
('Jennifer', 'Grey', 35000)
('James', 'Wong', 45000)
--- Fetch completed! -------</pre>

**답**


```python
# Your answer here
```

- - -

# THE END
