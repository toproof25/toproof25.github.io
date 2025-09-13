---
title: chirpy 테마로 GitHub Page 구성하기
description: 
date: 2025-09-11
last_modified_at: 2025-09-13
categories: 
  - GitHub Page
  - 환경설정
tags: 
  - GitHubPage
  - Jekyll
img: /assets/img/2025-09-11-chirpy-테마로-GitHub Page-구성하기/
---



## Jekyll Thema 저장소와 로컬에 설치

### GitHub에 있는 chirpy 테마를 Fork하기
우선 Jekyll Thema를 GitHub Page로 적용하는 것은 2가지 방법이 있다
- **테마가 올라온 저장소를 Fork하는 방법**
- 테마를 zip파일로 다운로드한 후 로컬에서 설정하고, push하는 방법

뭐가 됐든 둘다 같은 방식이며 여기서는 Fork하는 방법을 사용하도록 한다


우선 [Jekyll chirpy Thema GitHub Link](https://github.com/cotes2020/jekyll-theme-chirpy.git) 해당 링크를 클릭해서 저장소를 Fork해준다

![GitHub에 있는 chirpy 테마를 Fork하기]({{page.img}}GitHub에%20있는%20chirpy%20테마를%20Fork하기.png)




Fork할 때 저장소 이름을 `your-username.github.io`로 변경해주고, Create fork를 누른다
*자신의 Github 아이디를 흰색 박스에 적는다*

![Fork할 때 저장소 이름을 your-username.github.io로 변경해주고, Create fork]({{page.img}}Fork할%20때%20저장소%20이름을%20your-username.github.io로%20변경해주고,%20Create%20fork.png)

자신의 저장소 목록을 보면 정상적으로 Fork가 된 모습이 나타난다

![저장소 목록을 보면 정상적으로 Fork가 된 모습]({{page.img}}저장소%20목록을%20보면%20정상적으로%20Fork가%20된%20모습.png)


로컬에 저장소를 가져오기 위해 주소를 복사해준다

![로컬에 저장소를 가져오기 위해 주소를 복사해준다]({{page.img}}로컬에%20저장소를%20가져오기%20위해%20주소를%20복사해준다.png)

이후 로컬에서 원하는 위치에 Git Bash를 연 후 다음처럼 저장소를 `clone`하여 가져온다
`$ git clone "복사한 주소"`

![이후 로컬에서 원하는 위치에 Git Bash를 연 후 다음처럼 저장소를 clone하여 가져온다]({{page.img}}이후%20로컬에서%20원하는%20위치에%20Git%20Bash를%20연%20후%20다음처럼%20저장소를%20clone하여%20가져온다.png)

정상적으로 저장소를 복사해 왔다면, 이처럼 여러 파일들이 나타날 것이다

![정상적으로 저장소를 복사해 왔다면, 이처럼 여러 파일들이 나타날 것이다]({{page.img}}정상적으로%20저장소를%20복사해%20왔다면,%20이처럼%20여러%20파일들이%20나타날%20것이다.png)

---

## Ruby, Jekyll, Bundler 설치

### Ruby 설치

[Ruby 설치 페이지](https://rubyinstaller.org/downloads/archives/)에 접속하여 `Ruby+Devkit Installers`를 다운로드 한다. 
여기서는 `Ruby+Devkit 3.4.5-1 (x64)`를 다운로드 하였다. 각자 적절한 환경에 따라 다운로드를 하면 된다

![ruby-Ruby+Devkit Installers를 다운로드 한다.]({{page.img}}ruby-Ruby+Devkit%20Installers를%20다운로드%20한다.png)

설치 경로, 환경 변수, 설치할 목록 등이 나타나는데 모두 기본 설정을 유지하고 다음을 계속 눌러준다. 

![ruby-그대로 Next를 누르다 Install을 눌러주면 된다]({{page.img}}ruby-그대로%20Next를%20누르다%20Install을%20눌러주면%20된다.png)

사진을 못찍어서 인터넷에서 가져왔는데 사진처럼 그대로 Next를 누르다 Install을 눌러주면 된다

![ruby-그대로 Next를 누르다 Install을 눌러주면 된다1]({{page.img}}ruby-그대로%20Next를%20누르다%20Install을%20눌러주면%20된다1.png)

![ruby-그대로 Next를 누르다 Install을 눌러주면 된다2]({{page.img}}ruby-그대로%20Next를%20누르다%20Install을%20눌러주면%20된다2.png)

다운중인 모습

![ruby-다운중인 모습]({{page.img}}ruby-다운중인%20모습.png)

완료!

![ruby-설치완료]({{page.img}}ruby-설치완료.png)

완료가 되면 콘솔창이 하나 실행되는데 여기서는 그냥 Enter를 눌러준다
*그냥 Enter를 누르면 1, 3번이 설치된다*

![ruby-완료가 되면 콘솔창이 하나 실행되는데 여기서는 그냥 Enter를 눌러준다]({{page.img}}ruby-완료가%20되면%20콘솔창이%20하나%20실행되는데%20여기서는%20그냥%20Enter를%20눌러준다.png)

이것저것 설치되는데 완료되면 마지막에도 Enter를 누르면 설치가 끝이난다

![ruby-이것저것 설치되는데 완료되면 마지막에도 Enter를 누르면 설치가 끝이난다]({{page.img}}ruby-이것저것%20설치되는데%20완료되면%20마지막에도%20Enter를%20누르면%20설치가%20끝이난다.png)

cmd창을 열고 `$ ruby -v`를 입력하면, 버전 정보가 나와야 정상적으로 설치가 완료된 것이다

![ruby  - cmd창을 열고 `$ ruby -v`를 입력하면, 버전 정보가 나와야 정상적으로 설치가 완료된 것이다]({{page.img}}ruby%20%20-%20cmd창을%20열고%20`$%20ruby%20-v`를%20입력하면,%20버전%20정보가%20나와야%20정상적으로%20설치가%20완료된%20것이다.png)

이후 (안해도 되지만) `$ gem update`를 한번 해줘도 좋을 듯 하다...


### Jekyll, Bundler 설치

Ruby설치와는 다르게 Jekyll, Bundler 설치는 간단하다.
cmd창을 열고 다음 명령어를 입력한다
- `$ gem install jekyll` 
- `$ gem install bundler` 

![gem install jekyll]({{page.img}}gem%20install%20jekyll.png)

![gem install bundler]({{page.img}}gem%20install%20bundler.png)

두개 모두 설치된 후에 Ruby와 마찬가지로 버전을 입력하여 설치가 됐는지 확인한다
- `$ jekyll -v`
- `$ bundler -v`

![두개 모두 설치된 후에 Ruby와 마찬가지로 버전을 입력하여 설치가 됐는지 확인한다]({{page.img}}두개%20모두%20설치된%20후에%20Ruby와%20마찬가지로%20버전을%20입력하여%20설치가%20됐는지%20확인한다.png)

---

## 기본적인 \_config.yml 및 기타 설정

### npm install
우선 chirpy 테마의 경우 다음 과정이 필요하다. vs code에서 설정한 로컬 폴더를 열고 터미널에 다음 명령어를 입력한다
- `$ npm install`
- `$ npm run build`
이 설정을 안하면, 홈페이지에 일부 기능이 동작하지 않는다

### config.yml 파일 설정
VS Code에서 로컬에 저장한 테마 폴더를 열면 **_config.yml**파일이 있다

![VS Code에서 로컬에 저장한 테마 폴더를 열면 _config.yml파일이 있다]({{page.img}}VS%20Code에서%20로컬에%20저장한%20테마%20폴더를%20열면%20_config.yml파일이%20있다.png)

해당 파일에서 간단하게 `title`이랑 `url`부분만 수정한다
*title은 아무 제목이나 적고, url은 'https://username.github.io'으로 작성한다*

![해당 파일에서 간단하게 `title`이랑 `url`부분만 수정한다]({{page.img}}해당%20파일에서%20간단하게%20`title`이랑%20`url`부분만%20수정한다.png)

### github actions 설정
저장소에서 Setting -> Pages -> Build and deployment에서 GitHub Actions를 선택

![저장소에서 Setting - Pages - Build and deployment에서 GitHub Actions를 선택]({{page.img}}저장소에서%20Setting%20-%20Pages%20-%20Build%20and%20deployment에서%20GitHub%20Actions를%20선택.png)
이 설정은 

---

## 로컬에서 서버를 열고 테스트하기
vs code에서 터미널을 열고 `$ bundle install`을 하고, 
성공적으로 설치가 되면 다시 터미널에서 `$ bundle exec jekyll serve`을 입력한다

![다시 터미널에서 `$ bundle exec jekyll serve`을 입력하면]({{page.img}}다시%20터미널에서%20`$%20bundle%20exec%20jekyll%20serve`을%20입력하면.png)

이렇게 무언가 실행이 되는데 여기서 마지막에 `Server address` 주소로 접속을 해보면, 다운받은 테마로 열린 페이지에 접속을 할 수 있다

![`Server address` 주소로 접속을 해보면, 다운받은 테마로 열린 페이지에 접속을 할 수 있다]({{page.img}}`Server%20address`%20주소로%20접속을%20해보면,%20다운받은%20테마로%20열린%20페이지에%20접속을%20할%20수%20있다.png)

## 깃허브 저장소에 Push하고 테스트
최종적으로 GitHub Page에 올리려면 처음에 만든 저장소에 변경사항을 최종적으로 Push를 해야 한다
먼저 `.gitigoner`에 들어가서 다음 부분을 주석 처리한다

![먼저 `.gitigoner`에 들어가서 다음 부분을 주석 처리한다]({{page.img}}먼저%20`.gitigoner`에%20들어가서%20다음%20부분을%20주석%20처리한다.png)



이후에는 Git에 다음과 같이 push를 해준다
```
$ git add .
$ git commit -m "chore: Jekyll 초기 설정"
$ git push origin master
```

깃허브에 가보면 Actions가 작동하는 모습이 보인다

![깃허브에 가보면 Actions가 작동하는 모습이 보인다1]({{page.img}}깃허브에%20가보면%20Actions가%20작동하는%20모습이%20보인다1.png)

![깃허브에 가보면 Actions가 작동하는 모습이 보인다2]({{page.img}}깃허브에%20가보면%20Actions가%20작동하는%20모습이%20보인다2.png)


정상적으로 완료가 되면 초록색 불이 들어온다

![정상적으로 완료가 되면 초록색 불이 들어온다]({{page.img}}정상적으로%20완료가%20되면%20초록색%20불이%20들어온다.png)


이제 인터넷 주소창에 설정했던 url을 입력하면?
`https://설정한 URL.github.io/`
이렇게 로컬에서 본 사이트가 그대로 나타난다

![이렇게 로컬에서 본 사이트가 그대로 나타난다]({{page.img}}이렇게%20로컬에서%20본%20사이트가%20그대로%20나타난다.png)




## Jekyll Thema를 설정하면서 발생한 문제

### Git Actions에서 vendors/bootstrap문제로 안되는 경우
깃허브에 Push를 했는데 Actions에서 계속 오류가 발생하는 경우

![안되는 경우 vendors3]({{page.img}}안되는%20경우%20vendors3.png)

이는 `_bootstrap.scss`파일이 없어서 발생하는 문제로 간단하게 해결이 가능하다
로컬에서 



### js/dist/\*.min.js 오류로 홈페이지 기능이 동작하지 않는 경우
해당 오류는 테마에서 사용하는 기능이 일부 부족한 거로 간단하게 아래 두 명령어만 입력하면 된다

![안되는 경우 dist]({{page.img}}안되는%20경우%20dist.png)

- `$ npm install`
- `$ npm run build`
이렇게 하면 폴더 내 `node_modules` 폴더와 문제가 발생하는 경로에 정상적으로 파일들이 생성된다
이후 `.gitigoner`에서 `assets/js/dist` 이 부분을 제거하거나 주석처리를 하여 깃허브 저장소에 올려지도록 한다

