---
title: 공식 스레드 샘플앱 설치
description: 공식 스레드 샘플앱 설치 과정
author: braelyn
date: 2024-10-08 17:11:18 +0900
categories: [기술블로그, 놀이터기록]
tags: [정보, 기록, Threads, API, Threads API, Meta, 테스트, sample app]
render_with_liquid: false
---

> 오랜만이다. 직장을 다니고 이것저것을 챙기면서 사이드 프로젝트나 블로거를 하기는 참 쉽지 않다. 프로 블로거나 인플런서 등 매일 혹은 2, 3일마다 무엇을 작업하고 올리는 것은 너무나도 대단한 노력과 끈기라는 것을 새삼스럽게 느껴졌다. 물론 이전에도 머리로 이해하지만 이제 실제로 해보니 확실히 와 닿았다. 하지만 텀이 길어지더라도, 속도가 느려지더라도 포기하지 않게 계속 이 블로그를 이어나갈 수 있게 노력하기로 마음을 먹었다.
>
> 이번에는 지난(지지난?) 포스트에서 이야기했던 스레드 샘플앱을 설치하는 과정을 기록하려고 한다. 별거 없지만 소소하게 매 과정을 기록하다 보면 나중에 다 자산이라고 믿는다.

## 환경 세팅

### 소스코드

우선 [**공식 샘플앱**](https://github.com/fbsamples/threads_api)은 깃허브로 제공하여서 이를 포크하고 로컬로 내려받는다.

샘플앱을 구동하려면 node.js 필요한데 [**여기서**](https://nodejs.org/en/download/package-manager) 최신 버전을 다운받으면 된다.

`node -v`로 설치 상태를 확인할 수 있다.

그 다음으로 샘플앱 README에 따라 `npm install`를 실행한다. 이는 소스코드를 배포한다. `npm`{: .filepath} 설치 상태도 `npm -v`로 확인할 수 있다.

### 환경 변수

환경 변수 설정은 리포지토리에 있는 `.env.template`{: .filepath}를 사용해 `.env`{: .filepath} 파일을 만들어 하나.

`.env`{: .filepath}에 있는 `APP_ID`{: .filepath}, `API_SECRET`{: .filepath}, `SESSION_SECRET`{: .filepath}를 수정해 줘야 하고, `HOST`{: .filepath}는 그대로 두어도 되고 다른 호스트네임으로 바꿔도 되는데 바꾸면 `REDIRECT_URI`{: .filepath}도 바꿔 주어야 한다. 그냥 참고하려고 설치한 앱이니 그냥 기존 HOST 값으로 저장했다.

`APP_ID`{: .filepath}, `API_SECRET`{: .filepath}, `SESSION_SECRET`{: .filepath}는 모두 메타앱 관리자 페이지에서 찾을 수 있다.

### 호스트 맵핑

공식 샘플앱은 `localhost`{: .filepath}로 자동 맵핑시키지 않으니 환경 변수 HOST를 localhost url `127.0.0.1`로 미리 맵핑시켜야 한다.

윈도우에는 `/c/Windows/System32/drivers/etc/hosts`{: .filepath}에 아래 맵핑 코드를 추가해야 한다.

```shell
127.0.0.1       threads-sample.meta
```

> 여기서 주의! 윈도우 환경이지만 git bash 등 리눅스 기반 터미널에 익숙하다 보니 `~/etc/hosts`{: .filepath}를 잘못 수정하다가 앱을 구동할 때 오류가 난다. 호스트 맵핑은 윈도우 시스템 파일인 `/c/Windows/System32/drivers/etc/hosts`{: .filepath}에서 해야 한다. 
{: .prompt-error }

`~/etc/hosts`{: .filepath}를 잘못 수정하면 `npm start`로 앱을 구동하고 아래와 같이 'host address not found' 오류가 뜬다.

```shell
$ npm start
> threads_api_sample@1.0.0 start
> node ./src/index.js

node:events:497
    throw er; // Unhandled 'error' event
    ^

Error: getaddrinfo ENOTFOUND threads-sample.meta
    at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
Emitted 'error' event on Server instance at:
    at GetAddrInfoReqWrap.doListen [as callback] (node:net:2132:12)
    at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:17) {
errno: -3008,
code: 'ENOTFOUND',
syscall: 'getaddrinfo',
hostname: 'threads-sample.meta'
}

Node.js v20.18.0
```

### 로컬 호스트 인증서

OAuth를 통해 스레드에 로그인하려면 HTTPS 연결로 앱이 구동되어야 한다. 그래서 SSL 인증서가 필요한데 이는 `mkcert`으로 간단하게 인증서를 만들고 `.key.pem`{: .filepath}, `.pem`{: .filepath} 파일을 생성하면 된다.

`mkcert` 명령어가 없다면 `choco`로 `mkcert`를 설치하면 된다.

```shell
$ choco install mkcert
$ mkcert --version
```

인증서를 설치한다.

```shell
$ mkcert -install
```

샘플앱이 사용하는 호스트(로컬호스트)의 인증서 생성은 `mkcert $HOST`를 실행하면 된다. 

```shell
$ mkcert threads-sample.meta
```

`.key.pem`{: .filepath}, `.pem`{: .filepath} 파일은 같은 경로에 생성된다.

![img-description](/assets/img/post_241008/1.png)

## 샘플앱 실행

다시 `npm install`를 실행해 앱을 배포한다.

앱 자체 실행은 매우 간단하다. `npm start` 실행하면 끝이다. 오류가 없으면 앱은 `https://$HOST:8000(https://threads-sample.meta:8000)`{: .filepath}에 실행되고 있다. 👍

![img-description](/assets/img/post_241008/2.png)

