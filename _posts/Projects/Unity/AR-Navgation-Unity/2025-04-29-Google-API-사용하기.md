---
title: Google API 사용하기
description: null
date: 2025-04-29
categories:
- Projects
- Unity
- AR-Navgation-Unity
tags:
- 캡스톤VR
- Unity
- API
img: /assets/img/2025-04-29-Google-API-사용하기/
---
## Google API 키 발급받기
- ### [Google Maps Platform](https://developers.google.com/maps?hl=ko)
	- Google 로그인 후 시작하기 
	- 누른 후 결제 정보 등록 (등록해야 API 사용 가능)
	- API키를 발급하고 두가지 API를 주로 사용
	  ![API키를 발급하고 두가지 API를 주로 사용]({{page.img}}API키를 발급하고 두가지 API를 주로 사용.webp)
		- Maps Static API (정적 지도를 받아오는 API)
		- Directions API (길찾기를 수행하는 API)
- ### Unity Maps Static 구현
	- 내 디바이드 GPS를 가져와서, static map 센터에 요청하여 지도를 받아오기 위해 Image UI를 생성
	  ![static map 센터에 요청하여 지도를 받아오기 위해 Image UI를 생성]({{page.img}}static map 센터에 요청하여 지도를 받아오기 위해 Image UI를 생성.webp)
	- #### **GoogleStaticMapRoad.cs** 스크립트 작성
		- ![GoogleStaticMapRoad.cs 스크립트 작성]({{page.img}}GoogleStaticMapRoad.cs 스크립트 작성.webp)
		- API key, 요청값 기본값을 설정
		  > ```cpp
		  > [Header("API 키 설정")]
		  > public string apiKey = "";                         // Google Maps API Key
		  > 	
		  > [Header("Static Map 설정")]
		  > public int zoom = 20;                              // 초기 확대 레벨
		  > public enum resolution { low = 1, high = 2 };
		  > public resolution mapResolution = resolution.low;  // 해상도
		  > public enum type { roadmap, satellite, hybrid, terrain };
		  > public type mapType = type.roadmap;                // 지도 종류
		  > ```
		- Start시 크기 조정 후 최초 지도 갱신
		  > ```cpp
		  > void Start()
		  > {
		  > 	// 1) RawImage 크기에 맞춰 요청 사이즈 설정
		  > 	rect = GetComponent<RawImage>().rectTransform.rect;
		  > 	mapWidth = Mathf.RoundToInt(rect.width);
		  > 	mapHeight = Mathf.RoundToInt(rect.height);
		  > 
		  > 	// 2) 길찾기 버튼에 리스너 연결
		  > 	routeButton.onClick.AddListener(() => StartCoroutine(RequestRouteAndMap()));
		  > 
		  > 	// 3) 앱 시작 시 현재 위치 맵만 먼저 로드
		  > 	StartCoroutine(getStaticMap(null, Input.location.lastData.latitude, Input.location.lastData.longitude, zoom));
		  > }
		  > ```
		- 100 프레임마다 새로운 지도 갱신 요청
		- 요청 성공 시 지도 갱신
		  > ```cpp
		  > IEnumerator getStaticMap()
		  >{
		  >     url = "https://maps.googleapis.com/maps/api/staticmap?" + "&zoom=" + zoom + "&size=" + mapWidth + "x" + mapHeight + "&scale=" + mapResolution + "&maptype=" + mapType + "&key=" + apiKey;
		  > 
		  >     var query = "";
		  >     query += "&center=" + UnityWebRequest.UnEscapeURL(string.Format("{0}, {1}", Input.location.lastData.latitude, Input.location.lastData.longitude));
		  >     query += "&markers=" + UnityWebRequest.UnEscapeURL(string.Format("{0}, {1}", Input.location.lastData.latitude, Input.location.lastData.longitude));
		  > 
		  >     UnityWebRequest www = UnityWebRequestTexture.GetTexture(url + query);
		  >     
		  >     yield return www.SendWebRequest();
		  > 
		  >     if (www.error == null)
		  >     {
		  >         Destroy(GetComponent<RawImage>().texture);
		  >         GetComponent<RawImage>().texture = ((DownloadHandlerTexture)www.downloadHandler).texture;
		  >         mapLog.text = "택스쳐 불러오기 성공";
		  >     }
		  >     else
		  >     {
		  >         mapLog.text = "error. 맵 불러오기 실패";
		  >     }
		  > }
		  > ```
		- #### 간단한 플로우 차트
		  ![GOOGLE API 간단한 플로우 차트]({{page.img}}GOOGLE API 간단한 플로우 차트.webp)
		- #### 결과
			- 정상적으로 지도와 마커가 표시되는 것을 확인
			  ![정상적으로 지도와 마커가 표시되는 것을 확인]({{page.img}}정상적으로 지도와 마커가 표시되는 것을 확인.webp)
- ## Unity Google API Directions 구현
	- 임시 목적지 이공관, 다이소로 설정하며 길찾기 구현 시 안되는 현상 발생
	  ![임시 목적지 이공관, 다이소로 설정하며 길찾기 구현 시 안되는 현상 발생]({{page.img}}임시 목적지 이공관, 다이소로 설정하며 길찾기 구현 시 안되는 현상 발생.webp)
	- 간단하게 한국에서는 국가 안보 문제로 지도 데이터 해외 반출 규정이 있다
	  >[!note] AI-Perplexity
	  >**구글 API(특히 구글 맵스)**가 한국에서 정상적으로 동작하지 않는 핵심 원인은 **한국 정부의 지도 데이터 해외 반출 제한**입니다. 이로 인해 구글은 **고정밀 지도 데이터(1:5,000 축척 등)**를 해외 서버에 저장하지 못하고, 도보·자동차 내비게이션, 실시간 교통정보 등 주요 기능을 한국 내에서 제공하지 못합니다[1](https://sphinfo.com/blog/read/583)[3](https://www.newsis.com/view/NISX20250314_0003099281)[5](https://byline.network/2016/05/1-160/). 이는 국가 안보를 이유로 한 법적 규제에 따른 것으로, 외국인 관광객과 개발자 모두에게 큰 불편을 초래하고 있습니다.
- ## Google API
	- 처음에는 신경안쓰고 구글 API를 사용하려 했으나, 이러한 정보를 간과하고 접근하여 알게되었다. 
	- 물론 진행 완전 초반이라 문제는 없이 한국 지도에 특화된 네이버 API를 사용하기로 결정



---
##### 링크 문서
- 

##### 참고자료(출처)
- [[Unity] Google static map 현재위치 받기](https://velog.io/@jjarseag_kim/Unity-Google-static-map-%ED%98%84%EC%9E%AC%EC%9C%84%EC%B9%98-%EB%B0%9B%EA%B8%B0)
- [유니티(Unity) 구글 지도 api 사용하기](https://ljhyunstory.tistory.com/265)



