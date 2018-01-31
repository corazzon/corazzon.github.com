---
layout: post
title: "Mac OSX에서 XGBoost 설치하기" 
tagline: "XGBoost: A Scalable Tree Boosting System"
description: " 분산형 그래디언트 부스팅 알고리즘 , 결정트리(Decision Tree) 알고리즘의 연장선에 있음 , 여러 개의 결정트리를 묶어 강력한 모델을 만드는 앙상블 방법 , 분류와 회귀에 사용할 수 있음 , 랜덤포레스트와는 다르게 이전 트리의 오차를 보완하는 방식으로 순차적으로 트리를 만듦 , 무작위성이 없으며 강력한 사전 가지치기를 사용 , 캐글 상위 랭커들이 많이 사용하고 있음"
category: "자연어처리, NLTK,  python, 머신러닝"
tags: [python, ml, 머신러닝, machine learning, 기계학습, GBM, XGBM, XGBoost, 부스팅, 배깅]
---

{% include JB/setup %}

* 2016년 논문에서 소개 됨 : [XGBoostArxiv.pdf](http://dmlc.cs.washington.edu/data/pdf/XGBoostArxiv.pdf)
* 분산형 그래디언트 부스팅 알고리즘
* 결정트리(Decision Tree) 알고리즘의 연장선에 있음
* 여러 개의 결정트리를 묶어 강력한 모델을 만드는 앙상블 방법
* 분류와 회귀에 사용할 수 있음
* 랜덤포레스트와는 다르게 이전 트리의 오차를 보완하는 방식으로 순차적으로 트리를 만듦
* 무작위성이 없으며 강력한 사전 가지치기를 사용
* 캐글 상위 랭커들이 많이 사용하고 있음
* 타이타닉 경진대회에 사용 예제가 있음 : [XGBoost example (Python) Kaggle](https://www.kaggle.com/datacanary/xgboost-example-python/)


## 공식문서대로 설치하기

`
pip로는 잘 설치되지 않을 수 있다.
`

`일단 github에서 해당 프로젝트를 다운로드 혹은 클론 받아 놓는다.`

<pre>
git clone --recursive https://github.com/dmlc/xgboost.git  
</pre>

1. 일단 설치하려고 보니 clang, make가 필요했다. 이건 xcode설치로 대체했다.
2. 그리고 다시 공식문서로 돌아갔다. => [Installation Guide — xgboost 0.6 documentation](https://xgboost.readthedocs.io/en/latest/build.html)
3. brew install gcc --without-multilib 을 설치했다.
4. cd xgboost; cp make/minimum.mk ./config.mk; make -j4 `이 방법으로 설치하게 되면 멀티스레드를 지원하지 않는다.` 시행착오로 겪은 것을 적은 것이기 때문에 이 글을 보고 설치하는 분은 6번을 참고해 주시면 된다.
5. 이렇게 해주었는데도 아래의 오류가 발생했다.

	```
	XGBoostLibraryNotFound: Cannot find XGBoost Library in the candidate path, did you install compilers and run build.sh in root path?
	List of candidates:
	mypath/xgboost/python-package/xgboost/libxgboost.dylib
	```

6. 그래서 공식 문서로 다시 돌아가서 보니 최신버전의 gcc를 사용하고 있다면 make 파일을 변경해 주어야 한단다.
`아래 방법으로 설치해야 멀티스레드를 지원한다. GPU Support는 공식 문서의 하단을 참고한다.`

	`cd xgboost; cp make/config.mk ./config.mk; make -j4`

7. 그리고 다시 빌드 했더니 성공했다.
```
./build.sh
Makefile:31: MAKE [/Applications/Xcode.app/Contents/Developer/usr/bin/make] - checked OK
make: Nothing to be done for `all'.
Successfully build multi-thread xgboost
```

8. 마지막으로 `pip3 install -e python-package`로 설치했다.
```
Obtaining file:///Users/corazzon/codes/xgboost/python-package
Requirement already satisfied: numpy in /my_venv_path/lib/python3.6/site-packages (from xgboost==0.6)
Requirement already satisfied: scipy in /my_venv_path/lib/python3.6/site-packages (from xgboost==0.6)
Installing collected packages: xgboost
  Running setup.py develop for xgboost
Successfully installed xgboost
```

## pip로 겪은 시행착오
* pip로 설치가 되지 않아 다음의 방법으로 설치했다.
* 하지만 아래 방법으로도 설치가 안 될때가 있으니 공식 문서를 참고하는것을 추천한다.
* 장비를 바꾸고 이 방법대로 되지 않아 이 블로그글 앞의 공식문서대로 설치하기로 설치했다.  
* 아래 내용은 설치하며 겪은 시행착오로 참고삼아 적어둔다.
* [pip install failure · Issue #463 · dmlc/xgboost](https://github.com/dmlc/xgboost/issues/463)

<pre>
git clone --recursive https://github.com/dmlc/xgboost.git  
cd xgboost  
./build.sh
pip3 install -e python-package  
</pre>


```python
!pip3 show xgboost
```

    Name: xgboost
    Version: 0.6
    Summary: XGBoost Python Package
    Home-page: https://github.com/dmlc/xgboost
    Author: Hongliang Liu
    Author-email: phunter.lau@gmail.com
    License: Apache-2.0
    Location: /data/xgboost/python-package
    Requires: numpy, scipy


설치는 되었지만 Jupyter Notebook에서 실행되지 않는 문제가 있었다.

다음 글을 참고하여 노트북에서 불러오기에 성공했다.

* [python - Jupyter notebook xgboost import - Stack Overflow](https://stackoverflow.com/questions/44856105/jupyter-notebook-xgboost-import)



## 설치 및 동작확인

`jupyter notebook에서 제대로 설치되었는지 확인해 본다.`

```python
import pip
pip.main(['install', 'xgboost'])
```

    Requirement already satisfied: xgboost in /data/xgboost/python-package
    Requirement already satisfied: numpy in /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages (from xgboost)
    Requirement already satisfied: scipy in /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages (from xgboost)


`jupyter notebook에서 xgboost를 실행해 본다.`

```python
import xgboost as xgb
model = xgb.XGBClassifier(n_estimators=15, nthread=-1, seed=1111)
model
```

```
    XGBClassifier(base_score=0.5, booster='gbtree', colsample_bylevel=1,
           colsample_bytree=1, gamma=0, learning_rate=0.1, max_delta_step=0,
           max_depth=3, min_child_weight=1, missing=None, n_estimators=15,
           n_jobs=1, nthread=-1, objective='binary:logistic', random_state=0,
           reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=1111,
           silent=True, subsample=1)
```
