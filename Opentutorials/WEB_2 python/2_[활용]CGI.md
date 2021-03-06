## CGI

### 홈페이지를 CGI로 구현

#### 1. 파일 생성

- 파일 생성 후 권한을 줘야 한다. (linux or mac)

```bash
# 리눅스 환경
ls -al # 권한 보기
sudo chmod a+x index.py
```



#### 2. shebang

- https://stackoverflow.com/questions/41082302/ah01215-8-exec-format-error-exec-of-var-www-python-hello-py-failed-var
- python 파일을 python application으로 실행하기 위한 작업

```
#!python
```



#### 3. CGI

- https://docs.python.org/3/library/cgi.html

```python
print("Content-Type: text/html") # HTML header
print()
```



- HTML 내용 입력

```python
print('''
<!doctype html>
<html>
    <head>
      <title>WEB1 - Welcome</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="index.html">WEB</a></h1>
      <ol>
        <li><a href="1.html">HTML</a></li>
        <li><a href="2.html">CSS</a></li>
        <li><a href="3.html">JavaScript</a></li>
      </ol>
      <h2>WEB</h2>
      <p>The World Wide Web (abbreviated WWW or the Web) is an information space where documents and other web resources are identified by Uniform Resource Locators (URLs), interlinked by hypertext links, and can be accessed via the Internet.[1] English scientist Tim Berners-Lee invented the World Wide Web in 1989. He wrote the first web browser computer program in 1990 while employed at CERN in Switzerland.[2][3] The Web browser was released outside of CERN in 1991, first to other research institutions starting in January 1991 and to the general public on the Internet in August 1991.
      </p>
    </body>
</html>
''')
```



### URL query string을 가져오는 방법

#### 1. URL 변경

```python
# index.py

print('''
<!doctype html>
<html>
    <head>
      <title>WEB1 - Welcome</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="index.html">WEB</a></h1>
      <ol>
        <li><a href="index.py?id=HTML">HTML</a></li>
        <li><a href="index.py?id=CSS">CSS</a></li>
        <li><a href="index.py?id=JavaScript">JavaScript</a></li>
      </ol>
      <h2>{title}</h2>
        <p>The World Wide Web (abbreviated WWW or the Web) is an information space where documents and other web resources are identified by Uniform Resource Locators (URLs), interlinked by hypertext links, and can be accessed via the Internet.[1] English scientist Tim Berners-Lee invented the World Wide Web in 1989. He wrote the first web browser computer program in 1990 while employed at CERN in Switzerland.[2][3] The Web browser was released outside of CERN in 1991, first to other research institutions starting in January 1991 and to the general public on the Internet in August 1991.
        </p>
    </body>
</html>
'''.format(title='pageId'))
```


#### 2. URL query string 가져오기

- https://docs.python.org/3/library/cgi.html#using-the-cgi-module

```python
# index.py

import cgi

form = cgi.FieldStorage()
pageId = form["id"].value

print('''
<!doctype html>
<html>
    <head>
      <title>WEB1 - Welcome</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="index.py">WEB</a></h1>
      <ol>
        <li><a href="index.py?id=HTML">HTML</a></li>
        <li><a href="index.py?id=CSS">CSS</a></li>
        <li><a href="index.py?id=JavaScript">JavaScript</a></li>
      </ol>
      <h2>{title}</h2>
        <p>The World Wide Web (abbreviated WWW or the Web) is an information space where documents and other web resources are identified by Uniform Resource Locators (URLs), interlinked by hypertext links, and can be accessed via the Internet.[1] English scientist Tim Berners-Lee invented the World Wide Web in 1989. He wrote the first web browser computer program in 1990 while employed at CERN in Switzerland.[2][3] The Web browser was released outside of CERN in 1991, first to other research institutions starting in January 1991 and to the general public on the Internet in August 1991.
        </p>
    </body>
</html>
'''.format(title=pageId))
```

- 이 경우 ID값이 없는 경우 에러 발생



### CGI 소개

- 웹서버와 언어들이 상호간에 쉽게 연결될 수 있도록 만든 규약

![CGI](http://www.sergey.com/web_course/images/cgi.jpg)



- 웹서버가 사용자의 요청에 따라서 `cgi_env` app 에 전달하는 데이터들이 출력

```python
# cgi_env.py 

#!/usr/local/bin/python3
print("Content-Type: text/html")
print()
import cgi
cgi.test()
```



```php
# cgi_env.php

<?php
print_r($_SERVER);
?>
```