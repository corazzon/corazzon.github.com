---
layout: post
title: "Mac OSX python ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed" 
tagline: "Mac OSX python ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed"
description: "Mac OSX python ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed" 
category: "python, ssl, CERTIFICATE_VERIFY_FAILED"
tags: [python, ssl, CERTIFICATE_VERIFY_FAILED]
---

{% include JB/setup %}

Mac OSX python ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:749)

NLTK data를 다운로드 할 때 SSL 오류메시지가 나와서 nltk data downloader 에 문제가 있는건가 생각했었다.
결국 nltk 데이터를 깃헙에서 다운로드 받아 썼는데 


파이썬으로 크롤링을 하다보니 https 프로토콜로 통신을 하려고 하면 같은 오류가 발생해서 무슨 문제일까 고민했었다.
구글링을 해보니 https를 사용하지 않는 방법으로 해결했다는 답변들이 대부분이라 http 통신으로 우회하는 방법을 사용했다.


그런데 알고보니 너무나 간단한 방법으로 이 이슈를 해결할 수 있었다.
아래의 글을 보고 Finder로 Applications/Python 3.6 폴더를 열었다.
그리고 아래 파일을 더블클릭해서 설치했다.


`Install Certificates.command`



![9YSiPiq.png (1764×1096)](https://i.imgur.com/9YSiPiq.png)


그리고 파이썬에서 SSL 오류는 더 이상 발생하지 않았다.
이 문제를 해결하기 위해 셀프 인증서를 발급받는 방법 이라든지 여러 삽질을 했다. 


간단한 문제였는데 너무 허무하게 해결되었다.



[macos - Mac OSX python ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:749) - Stack Overflow](https://stackoverflow.com/questions/42098126/mac-osx-python-ssl-sslerror-ssl-certificate-verify-failed-certificate-verify)

