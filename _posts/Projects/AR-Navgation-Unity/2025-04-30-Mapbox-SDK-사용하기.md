---
title: Mapbox SDK 사용하기
description: null
date: 2025-04-30
categories:
- Projects
- AR-Navgation-Unity
tags:
- 지식
- 캡스톤VR
- Unity
- MapboxSDK
img: /assets/img/2025-04-30-Mapbox-SDK-사용하기/
---
# Mapbox SDK 설치 및 API Key 발급
## Mapbox Download
- [install Mapbox](https://www.mapbox.com/install/unity)
- 사이트에서 [mapbox-unity-sdk_v2.1.1.unitypackage](https://s3.amazonaws.com/mapbox-unity-sdk/v1/mapbox-unity-sdk_v2.1.1.unitypackage) 설치
- 유니티에서 프로젝트에서 우클릭 -> `Import Package`를 눌러서 다운받은 패키지를 import해준다
- **Unity6에서 Mapbox + AR 기능을 쓰기 위해서 필수 설정**
	- [Mapbox SDK for Unity Github](https://github.com/mapbox/mapbox-unity-sdk)
	- 깃허브에 README에 있듯 AR기능을 사용 안하려면 아래의 폴더를 제거한다
		- MapboxAR
		- UnityARInterface
		- GoogleARCore
		- UnityARKitPlugin
	- 기본 Mapbox 기능에 ARFoundation + ARCore를 이용하여 AR 콘텐츠를 제작
- 정상적으로 Import하면 이와 같은 화면이 나타난다
  ![Pasted image 20250430144357]({{page.img}}Pasted image 20250430144357.webp)
## Mapbox API Key 발급
- [mapbox](https://console.mapbox.com/account/access-tokens/) 주소로 들어가서 회원가입을 해준다
- 회원가입 -> 카드정보등록 -> 이메일 인증을 해야 토큰을 발급받을 수 있다
  ![Pasted image 20250430145100]({{page.img}}Pasted image 20250430145100.webp)

## API Key 인증
- 발급받은 토큰을 넣어 Submit을 눌러준다
  ![Pasted image 20250430145013]({{page.img}}Pasted image 20250430145013.webp)
- 아래와 같이 뜨면 성공적으로 인증되었다
  ![Pasted image 20250430145142]({{page.img}}Pasted image 20250430145142.webp)

# Unity에 Mapbox 지도 띄우기
- 해당 부분을 누르면 자동으로 프리팹이 씬에 추가된다
  ![Pasted image 20250430152922]({{page.img}}Pasted image 20250430152922.webp)



---
## 링크 및 참고자료

##### 링크 문서
- 

##### 참고자료(출처)
- 



