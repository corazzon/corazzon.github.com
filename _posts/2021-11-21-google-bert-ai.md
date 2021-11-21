---
layout: post
title: "[도서 리뷰] 구글 BERT의 정석"
tagline: "이 리뷰는 한빛미디어의 나는 리뷰어다 이벤트를 통해 책을 제공받아 작성했습니다. "
description: "인공지능, 자연어 처리를 위한 BERT의 모든 것"
category: 파이썬, Python, 구글, BERT, ALBERT, RoBERTa, ELECTRA, SpanBERT, KoBERT, KoGPT2, KoBART
---


<img src="https://i.imgur.com/Smeu0GO.jpg" width="500">


요즘 자연어처리에서 압도적인 인기를 끌고 있는 BERT 만을 다룬 책이 나왔다고 해서 관심이 갔는데 한빛미디어의 "나는 리뷰어다"를 통해 운 좋게 읽어보게 되었다.

자연어처리 관련된 경진대회를 보면 BERT를 사용한 모델이 종종 등장하는데 이 책은 트랜스포머 모델을 설명하며 BERT의 작동 원리 부터 BERT 모델이 사전학습 되는 방법과 BERT를 파인튜닝해 다운스트림 태스크에 활용하는 방법 등을 다루고 있다.

딥러닝, 텍스트 임베딩 등에 대한 사전 지식이 있는 상태에서 봐야하는 책이며, 초보적인 내용은 설명하고 있지 않기 때문에 자연어처리에 대한 기본 지식을 습득한 상태에서 읽어보는 것을 추천한다.

하지만 어느 책이든 요즘은 깃헙 소스코드를 친절하게 제공하고 있기 때문에 소스코드를 통해 이 책이 어떤 책인지 먼저 감을 잡을 수 있을것이다.

[PacktPublishing/Getting-Started-with-Google-BERT: Getting Started with Google BERT, published by Packt](https://github.com/PacktPublishing/Getting-Started-with-Google-BERT)

BERT만을 다룬 책도 없었고 BERT를 이렇게까지 자세하게 다룬 책도 없는데 KoBERT, KoGPT2, KoBART 모델을 개발한 역자분이 번역한 책이라 더 신뢰가 가는 책이다. 그래서 원서에는 없는 KoBERT, KoGPT2, KoBART 모델까지 다루고 있다는게 이 책의 큰 장점이기도 하다.

* BERT는 다른 임베딩 모델과 어떻게 다른가?
* BERT-base 모델과 BERT-large 모델의 차이점은 무엇인가?
* 세그먼트 임베딩은 무엇인가?
* BERT는 어떻게 사전 학습되는가?
* MLM 태스크는 어떻게 동작하는가?
* NSP 태스크는 어떻게 동작하는가?
* 마스크 언어 모델과 다음 문장 예측 태스크를 활용한 사전 학습
* BERT를 활용해 상황에 맞는 단어 및 문장 임베딩 생성
* 다운스트림 태스크를 위한 BERT 파인 튜닝


BERT를 다루며 알아야할 기본적인 내용부터 다양한 모델을 다루고 있다.

* ALBERT, RoBERTa, ELECTRA, SpanBERT 모델
* 지식 증류 기반 BERT 모델
* XLM 및 XLM-R 언어 모델
* sentence-BERT. VideoBERT, BART 모델

그리고 마지막으로 KoBERT, KoGPT2, KoBART 모델을 다룬다.

koBART에 대한 문서 요약과 관련된 소스코드와 예시를 아래 깃헙 링크에서 볼 수 있는데 사람보다도 문서요약을 더 잘 한다는 느낌이 들 정도로 엄청난 성능을 보여준다.

[SKT-AI/KoBART: Korean BART](https://github.com/SKT-AI/KoBART)

이 책은 자연어처리에 대한 기초가 없다면 읽기에 어려움이 있을지도 모른다.
하지만 이런 내용의 책을 이렇게 잘 번역된 한국어 예제로 만날 수 있어서 많은 도움이 되었다.

