---
title: Assembly-CSharp.csproj 에러
description: null
date: 2025-04-01
categories:
- Projects
- Unity
- AR-Navgation-Unity
tags:
- 지식
- Unity
- Error
img: /assets/img/2025-04-01-Assembly-CSharp.csproj-에러/
---
## Assembly-CSharp.csproj 에러

Script를 만들고 Visual Studio 2022로 코드를 작성하려고 여니 열리지 않고 
`Assembly-CSharp.csproj: 이 프로젝트 형식을 기반으로 하는 애플리케이션을 찾지 못했습니다. 추가 정보를 보려면 이 링크를 확인하십시오`
해당 에러가 발생하였다.

### 해결 방법
프로젝트 폴더로 이동한 후 **Assembly-CSharp.csproj** 파일을 연 후
아무 줄에 `<TargetFramework>net7.0</TargetFramework>` 해당 문장을 추가하고 저장---
##### 링크 문서
- 
##### 참고자료(출처)
- https://portable-paper.tistory.com/entry/%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-assembly-csharpcsproj%EC%9D%84%EB%A5%BC-%EB%A1%9C%EB%93%9C%ED%95%98%EC%A7%80-%EB%AA%BB%ED%96%88%EC%8A%B5%EB%8B%88%EB%8B%A4-one-or-more-errors-occurred-%EC%9D%B4-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EB%8A%94-c-dev-kit%EC%97%90%EC%84%9C-%EC%A7%80%EC%9B%90%EB%90%98%EC%A7%80-%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4



