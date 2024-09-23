---
title: 블로그에 댓글 기능을 추가하기
description: GitHub Discussions를 기반을 둔 Giscus를 사용해 무료로 간단하게 블로그에 댓글 기능을 추가하기
author: braelyn
date: 2024-09-20 00:23:47 +0900
categories: [기술블로그, 놀이터기록]
tags: [GitHub, GitHub_Discussions, Chirpy_Theme, Jekyll 테마, playground, 기록, Giscus]
render_with_liquid: false
---

오늘은 자기 전에 짧게 Giscus를 연동하는 것에 대해 끄적끄적할까 한다.
아마 내 포스트에 댓글을 남겨주는 사람 없을 것 같긴 하지만 그래도 나름 블로그답게 만들려면 댓글 섹션이 빠지면 섭섭하지.

## 가능한 댓글 구동 서비스

Chirpy 테마는 [**Giscus**](https://giscus.app/ko), [**Utterances**](https://utteranc.es/), [**Disqus**](https://disqus.com/) 이 3가지 댓글 기능을 제공하는 서비스를 지원한다.

- Disqus는 무료 및 유료 계정으로 사용할 수 있는데 무료 계정일 때 광고가 노출된다. 그러나 GitHub 계정이 없어도 댓글 할 수 있는 장점이 있다.
- Utterances는 완전 무료고 GitHub Issues를 사용한다. 그래서 댓글 하려면 무조건 GitHub 계정이 있어야 한다.
- Giscus는 Utterance와 비슷하게 GitHub Discussions를 사용한 무료 서비스다. 물론 똑같이 댓글 하는 데 GitHub 계정이 필요하다.

나는 댓글을 Discussions로 관리하는 것이 더 직관적으로 다가오니 Giscus를 선택했다.

## GitHub에서 Giscus 앱 설치

[**여기**](https://github.com/apps/giscus)에 들어가서 GitHub에 로그인 상태에서 '설치'를 눌러 앱을 설치했다.

바로 설치 설정에 진입했다. 나는 Giscus만 사용하려고 미리 리포지토리(`/giscus_comments`{: .filepath}) 하나 새로 만들었고 설정 페이지에서 이 리포지토리만 지정했다.

![img-description](/assets/img/post_240920/1.png)

## GitHub Discussions 설정

Discussions는 직접 활성화해야 했다.
리포지토리 Settings 탭 > General > Features 섹션--
title: 블로그에 댓글 기능을 추가하기
description: GitHub Discussions를 기반을 둔 Giscus를 사용해 무료로 간단하게 블로그에 댓글 기능을 추가하기
author: braelyn
date: 2024-09-20 00:23:47 +0900
categories: [기술블로그, 놀리터기록]
tags: [GitHub, GitHub_Discussions, Chirpy_Theme, Jekyll 테마, playground, 기록, Giscus]
render_with_liquid: false
---

오늘은 자기 전에 짧게 Giscus를 연동하는 것에 대해 끄적끄적할까 한다.
아마 내 포스트에 댓글을 남겨주는 사람 없을 것 같긴 하지만 그래도 나름 블로그답게 만들려면 댓글 섹션이 빠지면 섭섭하지.

## 가능한 댓글 구동 서비스

Chirpy 테마는 [**Giscus**](https://giscus.app/ko), [**Utterances**](https://utteranc.es/), [**Disqus**](https://disqus.com/) 이 3가지 댓글 기능을 제공하는 서비스를 지원한다.

- Disqus는 무료 및 유료 계정으로 사용할 수 있는데 무료 계정일 때 광고가 노출된다. 그러나 GitHub 계정이 없어도 댓글 할 수 있는 장점이 있다.
- Utterances는 완전 무료고 GitHub Issues를 사용한다. 그래서 댓글 하려면 무조건 GitHub 계정이 있어야 한다.
- Giscus는 Utterance와 비슷하게 GitHub Discussions를 사용한 무료 서비스다. 물론 똑같이 댓글 하는 데 GitHub 계정이 필요하다.

나는 댓글을 Discussions로 관리하는 것이 더 직관적으로 다가오니 Giscus를 선택했다.

## GitHub에서 Giscus 앱 설치

[**여기**](https://github.com/apps/giscus)에 들어가서 GitHub에 로그인 상태에서 '설치'를 눌러 앱을 설치했다.

바로 설치 설정에 진입했다. 나는 Giscus만 사용하려고 미리 리포지토리(`/giscus_comments`{: .filepath}) 하나 새로 만들었고 설정 페이지에서 이 리포지토리만 지정했다.

![img-description](/assets/img/post_240920/1.png)

## GitHub Discussions 설정

Discussions는 직접 활성화해야 했다.

> 리포지토리 Settings 탭 > General > Features 섹션
{: .prompt-info }

여기서 Discussions 선택하고 "Set up discussions"로 Discussions 활성화했다. 

![img-description](/assets/img/post_240920/2.png)

## 댓글 내용이 분류된 카테고리

이제 같은 페이지에서 Categories 옆에 연필 아이콘을 눌러 미래 있을지도 모른 댓글을 어디(어느 카테고리)로 저장하고 관리하기를 설정해야 했다.

![img-description](/assets/img/post_240920/3.png)

기존 카테고리를 선택해도 되고 새로운 카테고리를 만들어도 되는데 나는 새로 만들었다.
기존 카테고리는 연필 아이콘을 누르면 되고 새로운 카테고리는 오른쪽 위 New Category를 누르면 된다.

![img-description](/assets/img/post_240920/4.png)

새로운 카테고리의 이름, 설명을 작성해주고 Discussions 형식은 권장하는 Announcement로 설정했다.

![img-description](/assets/img/post_240920/5.png)

여기까지는 GitHub 쪽 설정이 완료됐다. Giscus로 넘어가야지.

## Giscus 코드 스니펫 생성

[**Giscus 사이트**](https://giscus.app/ko)에 가서 코드 스니펫 생성을 위해 설정을 입력해줬다.

- 언어: 한국어/English
- 저장소: `git_username/repo_name` (이는 Giscus앱이 설치되는 저장소다. 나는 아까 새로 만든 리포지토리 주소를 입력했다.)
- 페이지 <-> Disscussions 연결: 이건 나중에 Discussions에서 댓글 내용을 확인할 때 댓글의 제목이 어떤 것을 포함하냐는 옵션이다. 나는 어떤 포스트에 달린 댓글을 확인하고 싶어서 '경로'를 선택했다.
- Discussions 카테고리: 아까 설정해 놓은 카테고리 선택했다.
- 기능: 개인 취향인 것 같다. 나는 1, 3, 4번 박스를 체크했다.
- 테마: 나는 그냥 Preferred color scheme으로 그대로 두었다.

![img-description](/assets/img/post_240920/6.JPG)

후후 이제 드디어 코드 스니펫 아래처럼 생성됐다!

```html
<script
  src="https://giscus.app/client.js"
  data-repo="imlynmi/giscus_comments"
  data-repo-id="xxxxxxxxxxxxx"
  data-category="Comments (b_lyn.log)"
  data-category-id="xxxxxxxxxx"
  data-mapping="pathname"
  data-strict="0"
  data-reactions-enabled="1"
  data-emit-metadata="0"
  data-input-position="top"
  data-theme="preferred_color_scheme"
  data-lang="en"
  data-loading="lazy"
  crossorigin="anonymous"
  async
></script>
```

## Giscus 코드를 테마 코드에 삽입

마지막으로 필요한 정보만 `_config.yml`{: .filepath}에 입력하면 끝!!!

```yaml
comments:
  # Global switch for the post-comment system. Keeping it empty means disabled.
  provider: giscus # [disqus | utterances | giscus]
  giscus:
    repo: imlynmi/giscus_comments # <gh-username>/<repo>
    repo_id: 
    category: Comments (b_lyn.log)
    category_id: 
    input_position: top # optional, default to 'bottom'
```
{: file='/_config.yml'}

짜짠~

![img-description](/assets/img/post_240920/7.png)
