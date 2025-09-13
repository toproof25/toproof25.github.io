---
title: chirpy 테마로 GitHub Page 구성하기
author: toproof25
date: 2025-09-11
categories: [Blogging, Tutorial]
tags: [favicon]
---

## Jekyll Thema 저장소와 로컬에 설치

### GitHub에 있는 chirpy 테마를 Fork하기
우선 Jekyll Thema를 GitHub Page로 적용하는 것은 2가지 방법이 있다
- **테마가 올라온 저장소를 Fork하는 방법**
- 테마를 zip파일로 다운로드한 후 로컬에서 설정하고, push하는 방법

뭐가 됐든 둘다 같은 방식이며 여기서는 Fork하는 방법을 사용하도록 한다


우선 [Jekyll chirpy Thema GitHub Link](https://github.com/cotes2020/jekyll-theme-chirpy.git) 해당 링크를 클릭해서 저장소를 Fork해준다
![GitHub에 있는 chirpy 테마를 Fork하기](/assets/img/GitHubPage/GitHub에 있는 chirpy 테마를 Fork하기.png)





Fork할 때 저장소 이름을 `your-username.github.io`로 변경해주고, Create fork를 누른다
*자신의 Github 아이디를 흰색 박스에 적는다*
![[Fork할 때 저장소 이름을 your-username.github.io로 변경해주고, Create fork.png|500]]

자신의 저장소 목록을 보면 정상적으로 Fork가 된 모습이 나타난다
![[저장소 목록을 보면 정상적으로 Fork가 된 모습.png|500]]

로컬에 저장소를 가져오기 위해 주소를 복사해준다
![[로컬에 저장소를 가져오기 위해 주소를 복사해준다.png|500]]
apple-touch-icon.png
이후 로컬에서 원하는 위치에 Git Bash를 연 후 다음처럼 저장소를 `clone`하여 가져온다

![[이후 로컬에서 원하는 위치에 Git Bash를 연 후 다음처럼 저장소를 clone하여 가져온다.png|500]]

정상적으로 저장소를 복사해 왔다면, 이처럼 여러 파일들이 나타날 것이다
![[정상적으로 저장소를 복사해 왔다면, 이처럼 여러 파일들이 나타날 것이다.png|500]]

---

## Ruby, Jekyll, Bundler 설치

### Ruby 설치

[[https://rubyinstaller.org/downloads/archives/|Ruby 설치 페이지]]에 접속하여 `Ruby+Devkit Installers`를 다운로드 한다. 
여기서는 `Ruby+Devkit 3.4.5-1 (x64)`를 다운로드 하였다. 각자 적절한 환경에 따라 다운로드를 하면 된다
![[ruby-Ruby+Devkit Installers를 다운로드 한다..png|300]]

설치 경로, 환경 변수, 설치할 목록 등이 나타나는데 모두 기본 설정을 유지하고 다음을 계속 눌러준다. 
![[ruby-그대로 Next를 누르다 Install을 눌러주면 된다.png|500]]

사진을 못찍어서 인터넷에서 가져왔는데 사진처럼 그대로 Next를 누르다 Install을 눌러주면 된다
![[ruby-그대로 Next를 누르다 Install을 눌러주면 된다1.png|500]]
![[ruby-그대로 Next를 누르다 Install을 눌러주면 된다2.png|500]]

다운중인 모습
![[ruby-다운중인 모습.png|500]]

완료!
![[ruby-설치완료.png|500]]

완료가 되면 콘솔창이 하나 실행되는데 여기서는 그냥 Enter를 눌러준다
![[ruby-완료가 되면 콘솔창이 하나 실행되는데 여기서는 그냥 Enter를 눌러준다.png|500]]

이것저것 설치되는데 완료되면 마지막에도 Enter를 누르면 설치가 끝이난다
![[ruby-이것저것 설치되는데 완료되면 마지막에도 Enter를 누르면 설치가 끝이난다.png|500]]

cmd창을 열고 `$ ruby -v`를 입력하면, 버전 정보가 나와야 정상적으로 설치가 완료된 것이다
![[ruby  - cmd창을 열고 `$ ruby -v`를 입력하면, 버전 정보가 나와야 정상적으로 설치가 완료된 것이다.png|500]]

이후 (안해도 되지만) `$ gem update`를 한번 해줘도 좋을 듯 하다...


### Jekyll, Bundler 설치

Ruby설치와는 다르게 Jekyll, Bundler 설치는 간단하다.
cmd창을 열고 다음 명령어를 입력한다
- `$ gem install jekyll` 
  ![[gem install jekyll.png|300]]
- `$ gem install bundler` 
  ![[gem install bundler.png|300]]

두개 모두 설치된 후에 Ruby와 마찬가지로 버전을 입력하여 설치가 됐는지 확인한다
- `$ jekyll -v`
- `$ bundler -v`
![[두개 모두 설치된 후에 Ruby와 마찬가지로 버전을 입력하여 설치가 됐는지 확인한다.png|300]]


---

## 기본적인 \_config.yml 및 기타 설정

### npm install
우선 chirpy 테마의 경우 다음 과정이 필요하다. vs code에서 설정한 로컬 폴더를 열고 터미널에 다음 명령어를 입력한다
- `$ npm install`
- `$ npm run build`
이 설정을 안하면, 홈페이지에 일부 기능이 동작하지 않는다
이유는 [[#js/dist/ *.min.js 오류로 홈페이지 기능이 동작하지 않는 경우]]에 있다

### config.yml 파일 설정
VS Code에서 로컬에 저장한 테마 폴더를 열면 **_config.yml**파일이 있다
![[VS Code에서 로컬에 저장한 테마 폴더를 열면 _config.yml파일이 있다.png|300]]

해당 파일에서 간단하게 `title`이랑 `url`부분만 수정한다
*title은 아무 제목이나 적고, url은 'https://username.github.io'으로 작성한다*
![[해당 파일에서 간단하게 `title`이랑 `url`부분만 수정한다.png|500]]

### github actions 설정
저장소에서 Setting -> Pages -> Build and deployment에서 GitHub Actions를 선택
![[저장소에서 Setting - Pages - Build and deployment에서 GitHub Actions를 선택.png|500]]
이 설정은 

---

# 로컬에서 서버를 열고 테스트하기
vs code에서 터미널을 열고 `$ bundle install`을 하고, 
성공적으로 설치가 되면 다시 터미널에서 `$ bundle exec jekyll serve`을 입력한다
![[다시 터미널에서 `$ bundle exec jekyll serve`을 입력하면.png|500]]

이렇게 무언가 실행이 되는데 여기서 마지막에 `Server address` 주소로 접속을 해보면, 다운받은 테마로 열린 페이지에 접속을 할 수 있다
![[`Server address` 주소로 접속을 해보면, 다운받은 테마로 열린 페이지에 접속을 할 수 있다.png|500]]

# 깃허브 저장소에 Push하고 테스트
최종적으로 GitHub Page에 올리려면 처음에 만든 저장소에 변경사항을 최종적으로 Push를 해야 한다
먼저 `.gitigoner`에 들어가서 다음 부분을 주석 처리한다
![[먼저 `.gitigoner`에 들어가서 다음 부분을 주석 처리한다.png|300]]



이후에는 Git에 다음과 같이 push를 해준다
```
$ git add .
$ git commit -m "chore: Jekyll 초기 설정"
$ git push origin master
```

깃허브에 가보면 Actions가 작동하는 모습이 보인다
![[깃허브에 가보면 Actions가 작동하는 모습이 보인다1.png|500]]

![[깃허브에 가보면 Actions가 작동하는 모습이 보인다2.png|500]]


정상적으로 완료가 되면 초록색 불이 들어온다
![[정상적으로 완료가 되면 초록색 불이 들어온다.png|500]]


이제 인터넷 주소창에 설정했던 url을 입력하면?
`https://설정한 URL.github.io/`
이렇게 로컬에서 본 사이트가 그대로 나타난다
![[이렇게 로컬에서 본 사이트가 그대로 나타난다.png|500]]


---

## Jekyll Thema를 설정하면서 발생한 문제
### Git Actions에서 vendors/bootstrap문제로 안되는 경우
깃허브에 Push를 했는데 Actions에서 계속 오류가 발생하는 경우
![[안되는 경우 vendors3.png|400]]
이는 `_bootstrap.scss`파일이 없어서 발생하는 문제로 간단하게 해결이 가능하다
로컬에서 



### js/dist/\*.min.js 오류로 홈페이지 기능이 동작하지 않는 경우
해당 오류는 테마에서 사용하는 기능이 일부 부족한 거로 간단하게 아래 두 명령어만 입력하면 된다
![[안되는 경우 dist.png|500]]
- `$ npm install`
- `$ npm run build`
이렇게 하면 폴더 내 `node_modules` 폴더와 문제가 발생하는 경로에 정상적으로 파일들이 생성된다
이후 `.gitigoner`에서 `assets/js/dist` 이 부분을 제거하거나 주석처리를 하여 깃허브 저장소에 올려지도록 한다
