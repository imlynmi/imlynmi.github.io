---
title: Threads API 간단하게 시작
description: Threads API를 사용하기 위해 기본적인 설정 및 간단한 접근 테스트
author: braelyn
date: 2024-09-30 14:45:34 +0900
categories: [기술블로그, 놀이터기록]
tags: [정보, 기록, Threads, API, Threads API, Meta, 테스트]
render_with_liquid: false
---

> Threads API에 접근하여 활용할 수 있도록 기초 세팅해봤다. 아직 앱을 만들지 않아 단순히 API를 써보고 싶은 처음에 `Meta App`이 필요하다고 난감했다. 하지만 알고 보니 이 Meta App은 메타에서 개발자/제3자 앱이 스레드와 같은 메타 애플리케이션 데이터 사용을 관리하는 매체라고 생각하면 된다.
>
> 메타 개발자 계정을 생성하고, 메타 앱을 만들면 API 접근 권한이 부여되는 토큰을 생성할 수 있다. 공식 가이드를 따라서 하면 어렵지 않다.

API를 활용하는 데 필요한 설정이나 준비 내용은 [**Get Started**](https://developers.facebook.com/docs/threads/get-started?locale=en_US)에서 찾을 수 있다. 한 섹션 한 섹션을 따라 설정을 진행한다.

## 메타앱 만들기

> 먼저 `Meta App`{. :filepath}를 `Threads use case`{. :filepath}로 만들어야 한다.
{: .prompt-warning }

개발자 페이지에 가서 오른쪽 첫 번째 메뉴 `시작하기`{. :filepath}를 선택한다.

![img-description](/assets/img/post_240930/1.png)

안내에 따라 `Meta for Developers`{. :filepath} 개발자 계정을 생성한다. 기존 페이스북 계정으로 생성해도 좋고, 새로 생성해도 상관없다.

![img-description](/assets/img/post_240930/2.png)

그다음 '앱 만들기' 누르고 메타앱을 만든다. 안내에 따라 하면 되는데 여기서 두 번째 메뉴인 '이용 사례'는 `Threads API 액세스`{. :filepath}를 선택해 준다.

![img-description](/assets/img/post_240930/3.png)

앱을 만들면 화면이 메타앱 대시보드로 전환된다. 🙌

![img-description](/assets/img/post_240930/4.png)

## 스레드에 관련 권한 부여하기

스레드 사용자 데이터에 접근하고 그 데이터로 다양한 작업을 하기 위해 앱에 아래 권한을 부여해 줘야 한다.
`앱 맞춤 설정 및 요건`{. :filepath} 1번을 선택하고 권한을 추가한다.
    - threads_content_publish
    - threads_manage_insights
    - threads_manage_replies
    - threads_read_replies

![img-description](/assets/img/post_240930/5.png)

## 스레드 테스터 계정 및 액세스 토큰

### 테스터 계정 추가하기

앱을 테스트할 Threads 테스터 계정을 추가해야 한다. 우선 개인 스레드 계정을 쓰겠다.

아래 캡처처럼 `사용자 토큰 생성기`{. :filepath}에서 `Threads 테스터 추가 또는 삭제`{. :filepath}를 선택한다.

![img-description](/assets/img/post_240930/6.png)

'Threads 테스터'를 선택하고 스레드 아이디를 입력하면 테스터 계정 추가가 완료된다. 

![img-description](/assets/img/post_240930/7.png)

하지만 스레드 계정에 들어가서 테스터 추가 초대를 수락해야 마무리할 수 있다.
`스레드 설정 > 웹사이트 권한 > 초대`로 초대 건을 찾고 초대를 수락한다.

![img-description](/assets/img/post_240930/8.png)

### 액세스 토큰 생성하기

마지막으로 API를 호출할 때 필요한 액세스 토큰을 생성해야 한다.

다시 `이용 사례 > Threads API 액세스 편집 > 설정 > 사용자 토큰 생성기 > 액세스 토큰 생성하기`에 돌아가서 테스터 액세스 토큰 생성하면 된다.
'이해합니다'를 선택하면 토큰을 보이게 된다. 생성한 토큰은 복사하여 안전하게 보관한다.

![img-description](/assets/img/post_240930/9.png)

## API 호출 테스트

간단하게 cURL로 API 호출해 본다.

```shell
curl -i -X GET \
 "https://graph.threads.net/v1.0/me?fields=id,username&access_token=$THREADS_ACCESS_TOKEN"
```

> `$THREADS_ACCESS_TOKEN`은 아까 생성한 액세스 토큰이다.
{: .prompt-info }

아웃풋은 이렇게 나오는 것을 확인하고 드디어 잠을 자러 갈 수 있다. 👍🛌😪

![img-description](/assets/img/post_240930/10.png)