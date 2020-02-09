---
layout: post
title: "MAC OSX에서 konlpy 설치 시 ImportError: No module named 'jpype' 오류 해결"
tagline: "MAC OSX에서 파이썬 한국어 자연어 처리 도구인 KoNLPy 설치하기" 
description: "파이썬 자연어처리 도구인 KoNLPy(코엔엘파이) 를 사용하려면 파이썬에서 자바라이브러리를 사용할 수 있는 도구인 JPype 가 설치되어 있어야 합니다. JPype 설치 시 자바버전과 Xcode 커맨드라인툴 의존성을 해결해 주고 설치에 성공했습니다. 별것 아닌 문제인데 몇 시간동안 삽질을 해서 그 과정을 공유합니다."
category: "konlpy, jpype, xcode, java, mac, osx"
tags: [konlpy, jpype, xcode, java, mac, osx]
---
{% include JB/setup %}

<iframe width="560" height="315" src="https://www.youtube.com/embed/yUImPXmYO7M" frameborder="0" allowfullscreen></iframe>

* [설치하기 — KoNLPy 0.4.3 documentation](http://konlpy.org/ko/v0.4.3/install/)


```python
# 일단, 내 MAC OSX 버전은 다음과 같다.
import platform
import sys

print("""
system: %s
mac_ver: %s
""" % (
platform.system(),
platform.mac_ver(),
))
```

    
    system: Darwin
    mac_ver: ('10.13.1', ('', '', ''), 'x86_64')
    




konlpy를 `pip install konlpy`로 설치하고 노트북에서 import 했더니 다음과 같은 오류가 나서 몇 시간을 헤멨다.

## JPype
JPype는 Python 프로그램이 Java 클래스 라이브러리에 접근하고자 할 때 필요하다고 한다.

## 1. pip install konlpy 로 깔끔하게 설치가 완료된 듯 하여, 노트북에서 konlpy 를 불러왔다.

import konlpy

```python
ImportError: No module named 'jpype' 
```


## 2. jpype 가 필요한 듯 하여, 이 때부터 설치 삽질이 시작 되었다.

pip install jpype를 하니 오류가 나서 찾아보니 공식문서에 소스코드를 받아 직접 설치하는 방법이 나와서 깃헙에서 해당 소스를 다운로드 받았다.<br/>
처음에는 깃헙에 있는 소스코드를 다운로드 받아 설치했는데, 설치가 잘 되지 않아 최신소스 보다는 배포판이 좀 더 안정적이지 않을까 하여, 배포판을 다시 다운로드 받았다.


* [JPype1 0.6.2 : Python Package Index](https://pypi.python.org/pypi/JPype1)
* github : [originell/jpype: Friendly jpype fork with focus on easy installation.](https://github.com/originell/jpype)
* 공식 문서 : [JPype documentation — JPype 0.6.2 documentation](http://jpype.readthedocs.io/en/latest/index.html)


## 3. 자바 설치 및 환경변수 설정
여러 문서를 뒤적거리다가 자바 jdk 버전문제인가 생각이 되어 설치 된 버전을 삭제하고 예전 버전을 설치해 주고 환경변수까지 설정해 주었다.<br/>
그리고 맥에서 레거시용 자바를 다운로드 받을 수 있는 페이지가 있어서 해당 페이지에 가서 해당 자바를 다운로드 받아 설치했다.

* [다운로드 - OS X용 Java 2015-001](https://support.apple.com/kb/dl1572?locale=ko_KR)
* 터미널에서 java -version 으로 설치 정보를 봤다.
```
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```


## 4. 그런데도 `python setup.py build`를 해주었더니 다음과 같은 오류가 나왔다.

```c
cc1plus: warning: command line option '-Wstrict-prototypes' is valid for C/ObjC but not for C++
In file included from src/native/common/include/jpype.h:45:0,
                 from src/native/common/jp_method.cpp:17:
/Library/Java/JavaVirtualMachines/jdk1.8.0_151.jdk/Contents/Home/include/jni.h:39:10: fatal error: stdio.h: No such file or directory
 #include <stdio.h>
          ^~~~~~~~~
```

## 5. c나 c++과 관련 된 문제는 Xcode 관련 문제일거 같아 다음의 명령어로 다시 설치를 해주었다.
```
$ xcode-select --install
```

다시 다운로드 받은 프로젝트 폴더로 갔다.
```sh
$ python setup.py build
$ python setup.py install
```
## 설치 성공!

pip install JPype1-py3 로 설치해도 잘 된다.


```python
from konlpy.tag import Kkma
from konlpy.utils import pprint
kkma = Kkma()
print(kkma.sentences(u'JPype 설치 너무 까다롭습니다. 몇 시간을 날렸어요.'))
```

    ['JPype 설치 너무 까다롭습니다.', '몇 시간을 날렸어요.']



```python
print(kkma.nouns(u'JPype 설치 너무 까다롭습니다. 몇 시간을 날렸어요.'))
```

    ['설치', '시간']



```python
print(kkma.pos(u'JPype 설치 너무 까다롭습니다. 몇 시간을 날렸어요.'))
```

    [('JPype', 'OL'), ('설치', 'NNG'), ('너무', 'MAG'), ('까다롭', 'VA'), ('습니다', 'EFN'), ('.', 'SF'), ('몇', 'MDT'), ('시간', 'NNG'), ('을', 'JKO'), ('날리', 'VV'), ('었', 'EPT'), ('어요', 'EFN'), ('.', 'SF')]

## Colab에서 설치

```
# colab에서 konlpy 설치
!apt-get update
!apt-get install g++ openjdk-8-jdk 
!pip install konlpy
```
