---
title: Threads API 둘러보기
description: 
author: braelyn
date: 2024-09-23 17:58:22 +0900
categories: [기술블로그, 놀이터기록]
tags: [정보, 기록, Threads, API, Threads API, 소개]
render_with_liquid: false
---

> 저만 느끼는지 모르겠지만 요즘 스레드(Thread)가 인기 많더라고요. 개인적으로 X보다 분위기가 조금 더 친절하고 더 따뜻해요. 대체로 긍정적인 바이브가 있어 SNS를 잘 안 하는 저도 틈틈이 스크롤링하고 있어요.
> 스레드도 API가 있겠지?라는 생각이 어느 날 문득 들었어요. 찾아보니까 올해 4월에 공개되었다 하니 괜히 신이 났죠.
> 거창한 것이 아니더라도 소소하게 무엇을 만들까 해요.

## Threads API 첫인상

[**Threads API 홈페이지**](https://developers.facebook.com/docs/threads)를 딱 봤을 때 생각보다 많은 기능을 지원하고 있다는 느낌을 받았다. 

댓글/답글 관리, 태그라고 링크, 미디어 삽입 등 스레드 포스트에 관련 기능은 물론이고, 미디어 관리, 프로필도 다룰 수 있다. 그리고 Insights도 지원하니 꽤 유용한 API다.

각 세션도 잘 설명되어 있고, 기본적인 트러블슈팅도 안내가 있으니 이 API를 어떻게 응용할까?머리를 굴리기 시작했다.

## API 샘플 앱

[**공식 샘플 앱**](https://github.com/fbsamples/threads_api)이 있어서 API가 어떻게 활용할 수 있을지 더욱 직관적으로 확인할 수 있다.

`README.md`{: .filepath} 설치 설명에 따르면 앰플 앱을 쉽게 설치하고 실행할 수 있을 것 같다. 

이에 대해 실제로 스레드 API 활용 환경을 준비하면서 따로 기록하겠다.

> 이제 본격적으로 API를 작동시키는 일만 남았네요. 또 돌아올게요!