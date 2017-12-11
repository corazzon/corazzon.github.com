---
layout: post
title: "Mac OSX에서 NLTK Data 설치하기" 
tagline: "아나콘다가 아닌 가상환경에서 직접 설치해서 사용할 때 nltk_download() 오류 해결하기"
description: " 파이썬을 이용한 자연어 처리 툴깃 분류, 토큰 화, 형태소 분석, 태깅, 구문 분석 및 의미 추론을 위한 텍스트 처리 라이브러리, WordNet을 제공 아나콘다를 사용하면 한 번에 다운로드를 받을 수 있으나, 아나콘다 환경이 아닐 때 직접 설치하려고 하면 CERTIFICATE_VERIFY_FAILED 로 설치가 되지 않는다.  nltk.download() 에서 SSL오류가 발생해 설치를 못하고 고생하다 결국 nltk_data 를 일일이 내려받았다.  한 번에 받는 방법도 있다. 하지만 그 방법도 SSL 오류가 발생한다."
category: "자연어처리, NLTK,  python, 머신러닝"
tags: [python, ml, 머신러닝, machine learning, 기계학습, NLP, NLTK, 자연어처리]
---

{% include JB/setup %}

<iframe width="560" height="315" src="https://www.youtube.com/embed/kjInASI9GGE" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>


# Mac OSX에서 [NLTK Data](http://www.nltk.org/nltk_data/) 설치하기

* 파이썬을 이용한 자연어 처리 툴깃
* 분류, 토큰 화, 형태소 분석, 태깅, 구문 분석 및 의미 추론을 위한 텍스트 처리 라이브러리, WordNet을 제공
* 아나콘다를 사용하면 한 번에 다운로드를 받을 수 있으나, 아나콘다 환경이 아닐 때 직접 설치하려고 하면 CERTIFICATE_VERIFY_FAILED 로 설치가 되지 않는다.
* nltk.download() 에서 SSL오류가 발생해 설치를 못하고 고생하다 결국 nltk_data 를 일일이 내려받았다.
* 한 번에 받는 방법도 있다. 하지만 그 방법도 SSL 오류가 발생한다.
* [nltk/nltk_data: NLTK Data](https://github.com/nltk/nltk_data)
* 일일이 다운받는 게 귀찮다면 위의 깃헙 패키지 폴더를 nltk_data에 한번에 옮겨놓고 필요한 패키지들의 압축을 해당 위치에서 풀어 사용해도 된다.
* 일단 nltk부터 설치한다.


```python
import nltk
!pip3 show nltk
```

    Name: nltk
    Version: 3.2.5
    Summary: Natural Language Toolkit
    Home-page: http://nltk.org/
    Author: Steven Bird
    Author-email: stevenbird1@gmail.com
    License: Apache License, Version 2.0
    Location: /Users/corazzon/codes/jupyter/lib/python3.6/site-packages
    Requires: six



```python
sentence = """At eight o'clock on Thursday morning Arthur didn't feel very good."""
```


```python
tokens = nltk.word_tokenize(sentence)
tokens 
# nltk.download('punkt')
```




    ['At',
     'eight',
     "o'clock",
     'on',
     'Thursday',
     'morning',
     'Arthur',
     'did',
     "n't",
     'feel',
     'very',
     'good',
     '.']




```python
tagged = nltk.pos_tag(tokens)
tagged
```




    [('At', 'IN'),
     ('eight', 'CD'),
     ("o'clock", 'NN'),
     ('on', 'IN'),
     ('Thursday', 'NNP'),
     ('morning', 'NN'),
     ('Arthur', 'NNP'),
     ('did', 'VBD'),
     ("n't", 'RB'),
     ('feel', 'VB'),
     ('very', 'RB'),
     ('good', 'JJ'),
     ('.', '.')]




```python
# nltk.download('averaged_perceptron_tagger')
```


```python
# [nltk_data] Error loading wordnet: <urlopen error [SSL:
# [nltk_data]     CERTIFICATE_VERIFY_FAILED] certificate verify failed
# [nltk_data]     (_ssl.c:749)>
# 위와 같은 오류가 나서 스택오버플로우를 검색해 봤더니 SSL 링크가 깨져서 직접 다운로드 받아야 한다고 한다.
# 다음의 폴더에 넣어주면 작동을 한다. 첫줄에 있는 Resource에 있는 하위 경로도 같이 맞춰주어야 한다.
# **********************************************************************
#   Resource 'corpora/wordnet.zip/wordnet/' not found.  Please use
#   the NLTK Downloader to obtain the resource:  >>> nltk.download()
#   Searched in:
#     - '/usr/share/nltk_data'
#     - '/usr/local/share/nltk_data'
#     - '/usr/lib/nltk_data'
#     - '/usr/local/lib/nltk_data'
# **********************************************************************
#   >>> import nltk
#   >>> nltk.download('averaged_perceptron_tagger')
# 오류 내용을 보니 다음의 경로에서 파일을 찾을 수 없는 것으로 보인다.
# 위의 nltk_data폴더에 아래 경로의 폴더를 만들어 넣어주어야지 읽어올 수 있다.
# 오류 로그에 나오는 아래의 경로를 확인해서 다운로드 받은 averaged_perceptron_tagger를 nltk_data/taggers 경로에 넣어준다.
#  AP_MODEL_LOC = 'file:'+str(find('taggers/averaged_perceptron_tagger/'+PICKLE))
```


```python
# 다음의 항목을 추가로 설치해야 했으나 링크가 깨져 직접 다운로드 받음
# from nltk.corpus import brown
# brown.words()
# nltk.download('punkt')
# nltk.download('averaged_perceptron_tagger')

# nltk.download('treebank')
# nltk.download('wordnet')
```

nltk.download()를 하면 다음과 같은 창과 함께 오류메시지가 출력되고 다운로드가 되지 않는다.
!['image'](nltk_download.png)
터미널로 다운로드를 시도해도 같은 오류가 발생한다.

`$ sudo python -m nltk.downloader -d /usr/local/share/nltk_data all`

```
/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py:125: RuntimeWarning: 'nltk.downloader' found in sys.modules after import of package 'nltk', but prior to execution of 'nltk.downloader'; this may result in unpredictable behaviour
  warn(RuntimeWarning(msg))
[nltk_data] Error loading all: <urlopen error [SSL:
[nltk_data]     CERTIFICATE_VERIFY_FAILED] certificate verify failed
[nltk_data]     (_ssl.c:749)>
```

* 링크가 깨져서 http://www.nltk.org/nltk_data/ 에서 직접 다운로드 후 다음의 링크에 넣어 둠
* nltk_data 경로에 punkt 폴더를 추가해도 읽어오지 못해서 무슨 문제인지 찾아보았더니 tokenizers 폴더를 생성하고 그 안에 punkt를 넣어주어야 로드해 올 수 있다.
* /usr/local/share/nltk_data/tokenizers/punkt
[NLTK download SSL: Certificate verify failed - Stack Overflow](https://stackoverflow.com/questions/38916452/nltk-download-ssl-certificate-verify-failed)


```python
# nltk.download()
```

## 결론 
1. 다음의 경로에 nltk_data 폴더를 만든다. `/usr/local/share/nltk_data/`
* 필요한 패키지를 nltk_data에 직접 다운로드 받아 옮겨놔도 동작하는 패키지도 있지만, 위치정보에 맞게 새로운 폴더를 생성하고 다운로드 받은 패키지를 옮겨야 하기도 한다.
* nltk_data에 패키지를 옮겨도 동작하지 않으면 다음의 github 경로를 참고하여 폴더를 만들어 준다. https://github.com/nltk/nltk_data/tree/gh-pages/packages
* 아니면 위의 깃헙 패키지 폴더를 nltk_data에 한번에 옮겨놓고 필요한 패키지들의 압축을 해당 위치에서 풀어 사용해도 된다.
