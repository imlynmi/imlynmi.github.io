---
title: b_lyn.log 탄생
description: Jekyll 테마 Chirpy를 적용해 GitHub Pages가 호스트하는 블로그를 배포하는 과정 및 겪은 오류
author: braelyn
date: 2024-09-17 20:43:25 +0900
categories: [기술블로그, 놀리터기록]
tags: [GitHub, GitHub_Pages, Jekyll, Chirpy_Theme, 오답노트, playground, 기록]
render_with_liquid: false
---

> 요즘 다시 양전하지 못해 이것저것 만지고 시도하고 있다. 무엇을 찔러보고 거기서 터지는 골칫거리 하나씩 해결하는 과정을 즐기는데 다 해결하고 과정이 끝나면 잠깐 뿌듯하고 끝이었다. 그런데 나중에 거의 아무것도 기억나지 못해 후회하는 경우가 대부분이다. 그래서 이제 나도 블로그 시작해볼까 한다. 지극히 개인적인 기록이지만 나와 같이 무엇을 시도하다 막힐 때 조금이나마 도움이 됐으면 하는 마음도 있다. 
>
>첫 포스트인 만큼 이 블로그가 탄생하는 과정을 기록하는 것이 딱 적당할 것 같다. 그럼 시작해볼까?


블로그는 쉽게 시작하려면 velog와 같은 블로그 플랫폼을 사용하는 것도 괜찮은 선택이지만 자유롭게 코드를 만지면서 커스터마이징하는 것을 더 재미가 있을 것 같아 다른 선택지를 모색해 봤다. 검색해 보다가 호스팅도 데이터베이스도 아무런 비용이 안 드는 GitHub Pages에 관심이 생겼다. HTML부터 써서 사이트 만드는 것은 효율성이 떨어져 Jekyll 테마로 시작하는 것이 내 목적에 맞을 것 같아 곧바로 시작했다.

내가 선택한 테마는 깔끔한 [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy) 테마다. 별도 환경 설정이나 코딩 필요없이 바로 시작하는 [**chirpy-starter**](https://github.com/cotes2020/chirpy-starter)도 있지만 나는 나름 재미를 위해 본래 Chirpy를 그대로 fork했다.

## Chirpy 테마 fork하기

새로운 리포지토리로 포크한 다음에 리포지토리 이름을 지어줘야 한다. GitHub Pages의 URL로 써야 하기 때문에 `username.github.io`{: .filepath}로 지정해야 한다. 여기서 `username`{: .filepath}는 GitHub 사용자 이름이다.

![img-description](/assets/img/post_240917/1.png)

이제 리포지토리를 로컬로 clone하면 된다.

```bash
git clone git@github.com:imlynmi/imlynmi.github.io.git
```

## 기본적인 설정 수정

기본이라고 하지만 어떻게 보면 주요 사이트 설정은 전부 다 `_config.yml`{: .filepath}에 있다. 그러면 배포하기 전에 설정 몇 개를 건드려볼까?

> 사이트 url는 가장 중요하니 꼭 나의 url로 수정해 줘야 함
{: .prompt-warning }

```yaml
timezone: Asia/Seoul    #서울로 시간대를 바꿈
title: b_lyn.log    #사이트 제목을 수정함
tagline: 기억에서 사라지기 전에 소소하게 끄적끄적   #사이트 소제목을 수정함
url: "https://imlynmi.github.io" #제일 중요한 사이트 url를 수정함
```

수정한 `_config.yml`{: .filepath}를 로컬 테스팅을 위해 아직 commit하지 않다.

## 배포 전 환경 설정

전체 테마는 Jekyll로 구동되니까 Jekyll을 설치해 줘야 한다. 하지만 Jekyll 설치하기 전에 Ruby가 깔렸는지도 확인해야 한다. 나는 얼마 전에 윈도우 시스템을 재설치하는 바람에 거의 모든 것을 재설치해야 하는 상황이었다. Ruby부터 설치해 볼까?

### Ruby 설치

[**여기**](https://rubyinstaller.org/downloads/)에 들어가서 DEVKIT 탑재된 윈도우 버전을 다운받았다. 그다음은 `rubyinstaller-devkit-3.3.5-1-x64.exe`{: .filepath} 파일을 실행해 준다.

설치 파일이 실행되면서 아래 두 가지를 선택해야 한다.
- MSYS2 and MINGW development toolchain
- ridk install

마지막 단계에 terminal 창이 자동으로 떠 `3`{: .filepath}번을 입력하면 설치가 완료된다.

![img-description](/assets/img/post_240917/2.png)

> 윈도우 Command Prompt 이외 shell(ex. git bash)에서도 Ruby를 사용하고 싶다면 global PATH를 설정해야 하는데 이는 `ridk enable` 실행해 주면 된다.
{: .prompt-tip }

자, 그럼 이제 Ruby가 제대로 설치되어 있는지 확인해볼까? `ruby -v` 실행하고...

![img-description](/assets/img/post_240917/3.png)

굿! 👍	

### Jekyll 설치

Ruby 준비 완료됐으니 대망의 Jekyll을 설치 시작!
근데 Ruby가 있어 너무나도 쉽다.

```bash
gem install jekyll bundle   #Jekyll 설치
jekyll -v   #Jekyll 설치 확인
```

![img-description](/assets/img/post_240917/4.png)

## 로컬 배포

Production으로 가기 전에 당연히 로컬 환경에서 먼저 배포해 준다.

```bash
bundle insall   #로컬 환경에 배포한다
```

내가 재미 없을까봐 이렇게 딱 에러를 던저 주는구나!

### 오류 1

```bash
An error occurred while installing wdm (0.1.1), and Bundler cannot continue.

In Gemfile:
  wdm
```

우선 `Gemfile`{: .filepath}을 확인한다. 14행 `gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]`가 문제이군...하지만 뭐가 문제일까?

wdm은 윈도우 환경에서 수정 사항을 실시간으로 반영하게 하는 Ruby 플러그인이다. 그래서 위 오류를 처리하기 위해 사실 14행이 없어도 큰 문제가 발생하지는 않다. 하지만 그냥 comment out하는 것은 뭔가 문제를 외면하는 느낌이 들어서 곰곰이 생각해 보았다.

검색하다 보니 내가 설치한 Ruby는 최신 버전이라 wdm도 최신 버전만 지원하는 것을 알겠 되었다. 따라서 최신 wdm을 설치해 주고 Gemfile 14행을 최신 wdm 버전으로 수정했다.

```bash
gem install wdm
```

```ruby
이전:
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

수정:
gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]
```
{: file='/Gemfile'}

### 오류 2

다 된 줄 알았지만 아니었다...

사이트는 로컬 URL `http://127.0.0.1:4000/`{: .filepath}로 잘 구동된 것처럼 보이지만 terminal 창에서 이런 에러들이 올라오고 있었다.

```shell
 Auto-regeneration: enabled for 'B:/GitHub_Pages/imlynmi.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
[2024-09-16 14:00:13] ERROR `/assets/js/dist/home.min.js' not found.
[2024-09-16 14:00:56] ERROR `/assets/js/dist/page.min.js' not found.
[2024-09-16 14:42:45] ERROR `/assets/js/dist/categories.min.js' not found.
[2024-09-16 14:42:47] ERROR `/assets/js/dist/commons.min.js' not found.
[2024-09-16 14:42:48] ERROR `/assets/js/dist/misc.min.js' not found.
[2024-09-16 14:42:50] ERROR `/assets/js/dist/page.min.js' not found.
[2024-09-16 14:42:54] ERROR `/assets/js/dist/home.min.js' not found.
[2024-09-16 14:42:56] ERROR `/assets/js/dist/post.min.js' not found.
```

다시 고민에 빠졌다. `/assets/js/dist/`{: .filepath} 아예 없단다...뭘까...알고 보니까 그 파일들은 npm로 사이트를 구동하는 과정에서 생긴 것이고 `.gitignore`{: .filepath}에 그 파일들을 무시한다. 내가 리포지토리를 fork했으니 당연히 나의 리포지토리에서 그 파일들은 못찾을 것이다.

5.6.0 버전 이상부터 JS는 스스로 컴파일해야 한다는 지침도 마침 찾았다.

![img-description](/assets/img/post_240917/5.png)

그래서 곧바로 npm으로 구동하고 해당 파일들을 생성했습니다.

![img-description](/assets/img/post_240917/6.png)

마지막으로 `git add` 해서 해당 .js 파일들을 stage했다.

```shell
git add assets/js/dist _sass/dist -f
```
'~.js not found' 에러들은 더이상 안 뜬다. 😀

## 라이브 배포

로컬 환경에서 사이트가 제대로 구동되어 있다는 것을 확인하게 되면 라이브 배포는 사실 생각보다 어렵지 않다.

지금까지 모든 staged 파일을 commit하고 push한다.

리포지토리 `Settings`{: .filepath} 탭에 `Pages`{: .filepath}에 들어가면 `Build and deployment`{: .filepath}의 `Source`{: .filepath}를 `GitHub Actions`{: .filepath}로 바꿔주면 끝!

![img-description](/assets/img/post_240917/7.png)

이제 `Actions`{: .filepath} 탭에서 배포가 성공적인 것을 확인할 수 있다.

![img-description](/assets/img/post_240917/8.png)

## Production 환경의 블로그

드디어 완성!
아직 포스트는 없어서(물론 이 포스트를 쓰고 있지만) 아무것도 없지만 그래도 이렇게 라이브 페이지를 보면서 참 뿌듯하다.

![img-description](/assets/img/post_240917/9.png)