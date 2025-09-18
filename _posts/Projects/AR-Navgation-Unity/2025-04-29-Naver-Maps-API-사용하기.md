---
title: Naver Maps API 사용하기
description: null
date: 2025-04-29
categories:
- Projects
- AR Navgation Unity
tags:
- 캡스톤VR
- Unity
- API
img: /assets/img/2025-04-29-Naver-Maps-API-사용하기/
---
## Naver Maps API
- ### Naver Cloud API Key 발급
	- [네이버 cloud 홈페이지](https://www.ncloud.com/) 에서 로그인
	- 콘솔을 누르면 API 키를 발급할 수 있는데 만약 결제 정보(카드)가 등록이 안됐다면 먼저 결제 정보를 등록해야 API를 사용할 수 있다
	  ![먼저 결제 정보를 등록해야 API를 사용할 수 있다]({{page.img}}먼저 결제 정보를 등록해야 API를 사용할 수 있다.webp)
	- 이후 콘솔 확면에서 서비스를 누른 후 *Maps*로 API 서비스를 찾는다
	  ![이후 콘솔 확면에서 서비스를 누른 후 Maps로 API 서비스를 찾는다]({{page.img}}이후 콘솔 확면에서 서비스를 누른 후 Maps로 API 서비스를 찾는다.webp)
	- 애플리케이션을 등록해야 하는데 
		- 애플리케이션 이름
		- 사용할 API 선택 (Static Map과 Directions 5를 선택)
		- 안드로이드 앱 환경이니 패키지 이름을 추가
			- 이는 Unity -> Project Settings -> Player -> Other Settings 아래쪽에 해당 부분이 있다. (만약 아무것도 없거나 하면 체크박스 클릭해보기)
			  ![Other Settings 아래쪽에 해당 부분이 있다]({{page.img}}Other Settings 아래쪽에 해당 부분이 있다.webp)
			- 그대로 똑같이 복사하여 붙여넣고 추가를 누른다
	- 이후 사진처럼 선택한 API가 나타나며, 일/월별 제한이 있는 것을 볼 수 있다
	  ![이후 사진처럼 선택한 API가 나타나며, 일월별 제한이 있는 것을 볼 수 있다]({{page.img}}이후 사진처럼 선택한 API가 나타나며, 일월별 제한이 있는 것을 볼 수 있다.webp)
	- 인증 정보를 누르면 네이버 API Key를 볼 수 있다. ID와 Secret을 이용하여 API 요청을 한다
	  ![인증 정보를 누르면 네이버 API Key를 볼 수 있다]({{page.img}}인증 정보를 누르면 네이버 API Key를 볼 수 있다.webp)


## Unity Naver API 사용하여 지도/마커 띄우기
- ### NaverStaticMapLoad.cs 스크립트 생성
	- 먼저 이전에 Google API로 사용하고자 했던 UI와 스크립트를 참고하여 사용
	- 변수는 API 요청을 위한 ID, Secret 키를 입력하고 옵션을 추가해준다
	  ![변수는 API 요청을 위한 ID, Secret 키를 입력하고 옵션을 추가해준다]({{page.img}}변수는 API 요청을 위한 ID, Secret 키를 입력하고 옵션을 추가해준다.webp)
	- 이후 네이버 API 형식에 맞게 지도를 불러온다
		```cpp
		IEnumerator GetStaticMap(string encodedPath, float centerX, float centerY, int zoomLevel)
		{
			// 1) 기본 파라미터 설정
			string url = $"{staticBaseUrl}?w={mapWidth}&h={mapHeight}&center={centerX},{centerY}&level={zoomLevel}";
			valueLog.text += $"[{System.DateTime.Now:HH:mm:ss}] [정보] 기본 지도 요청 URL 구성 완료.\n";
		
			// 2) 현재 위치 마커 추가 (공식 문서 형식 준수)
			// markers=type:d|size:mid|pos:{longitude} {latitude}
			string marker = $"&markers=type:d|size:mid|pos:{centerX} {centerY}";
			url += marker;
			valueLog.text += $"[{System.DateTime.Now:HH:mm:ss}] [정보] 현재 위치 마커 추가 완료. 위치: ({centerX}, {centerY})\n";
		
			// 3) 최종 URL 출력
			valueLog.text += $"[{System.DateTime.Now:HH:mm:ss}] [정보] 최종 Static Map 요청 URL:\n{url}\n";
		
			// 4) API 요청
			UnityWebRequest mapReq = UnityWebRequestTexture.GetTexture(url);
			mapReq.SetRequestHeader("x-ncp-apigw-api-key-id", apiKeyId);
			mapReq.SetRequestHeader("x-ncp-apigw-api-key", apiKey);
		
			yield return mapReq.SendWebRequest();
		
			// 5) 요청 결과 처리
			if (mapReq.result == UnityWebRequest.Result.Success)
			{
				Destroy(GetComponent<RawImage>().texture);
				GetComponent<RawImage>().texture = ((DownloadHandlerTexture)mapReq.downloadHandler).texture;
				valueLog.text += $"[{System.DateTime.Now:HH:mm:ss}] [완료] Static Map 이미지 로드 성공\n";
			}
			else
			{
				valueLog.text += $"[{System.DateTime.Now:HH:mm:ss}] [오류] Static Map 요청 실패: {mapReq.error}\n";
			}
		}
		```
	- 네이버 지도와 마커가 정상적으로 불러와진 것을 확인
	  ![네이버 지도와 마커가 정상적으로 불러와진 것을 확인]({{page.img}}네이버 지도와 마커가 정상적으로 불러와진 것을 확인.webp)	


## 네이버 Maps 길찾기 API
- 테스트를 위해 강남대 앞 다이소의 GPS를 목적지로 설정
  ![변수는 API 요청을 위한 ID, Secret 키를 입력하고 옵션을 추가해준다]({{page.img}}변수는 API 요청을 위한 ID, Secret 키를 입력하고 옵션을 추가해준다.webp)
- 지도를 띄운 후 길찾기 테스트를 위해 기존 스크립트에 길찾기 함수를 작성
- 네이버 길찾기 API의 경우 보행자가 아닌 자동차만 지원하는 것을 알게됨
- **결론은 네이버 API에서 길찾기는 안되니 다른 API를 사용해야함. 그 중 Mapbox API는 한궁에서 보행자 길찾기가 가능하다는 것을 알게되고 한국 특화 지도인 Naver Map에 길찾기는 Mapbox를 사용하여 네이버 지도 위에 오버레이 하는 방식으로 진행하고자 함**
- **혹은 Tmap은 도보 길찾기와 한국 특화 지도가 가능해보이니 먼저 Tmap API를 사용해보고자 함**
- ... 초반에 API를 찾아보고 정리했으면 이런 일이 없었을 건데 준비가 미흡했다



---
## 링크 및 참고자료

##### 링크 문서
- 

##### 참고자료(출처)
- [Unity에서 naver map api 이용](https://velog.io/@disco9612/Unity%EC%97%90%EC%84%9C-naver-map-api-%EC%9D%B4%EC%9A%A9)
- [[Unity] Naver StaticMap API 연동](https://tkablog.tistory.com/entry/Unity-Naver-StaticMap-API-%EC%97%B0%EB%8F%99)
- [네이버 cloud 홈페이지](https://www.ncloud.com/)



