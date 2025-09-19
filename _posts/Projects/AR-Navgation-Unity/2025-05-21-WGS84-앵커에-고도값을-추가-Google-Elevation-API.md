---
title: WGS84 앵커에 고도값을 추가 (Google Elevation API)
description: null
date: 2025-05-21
categories:
- Projects
- AR-Navgation-Unity
tags:
- 캡스톤VR
- Unity
- ARCore
- 고도
img: /assets/img/2025-05-21-WGS84-앵커에-고도값을-추가/
---
## 고도
- ### Google Elevation API
	- Google에서 경위도값을 바탕으로 고도 값을 응답해주는 API
	- 이를 통해 보행자 경위도값을 바탕으로 해당 위치의 고도를 가져와 앵커를 생성하고자 함
	- API 요청 형식은 아래와 같다 (경도, 위도, API Key)
	  `string elevUrl = $"https://maps.googleapis.com/maps/api/elevation/json?locations={latitude},{longitude}&key={Google_API_Key}";`
	  　
	- 이후 요청한 후 응답받고 고도 정보를 가져오는 코드
	  ```cpp
	using (UnityWebRequest elevReq = UnityWebRequest.Get(elevUrl))
	{
	    // 응답 처리
	    yield return elevReq.SendWebRequest();
	    if (elevReq.result != UnityWebRequest.Result.Success)
	    {
	        valueLog.text += $"[{DateTime.Now:HH:mm:ss}] [오류] 고도 요청 실패: {elevReq.error}\n";
	        continue;
	    }
	
	    // 직렬화 클래스로 JSON 매핑
	    var elevJson = JsonUtility.FromJson<ElevationResponse>(elevReq.downloadHandler.text);
	    if (elevJson.results == null || elevJson.results.Length == 0)
	    {
	        valueLog.text += $"[{DateTime.Now:HH:mm:ss}] [오류] 고도 파싱 실패\n";
	        continue;
	    }
	
	    // 최종 해수면 기준 고도값 추출
	    double altitude = elevJson.results[0].elevation;
	}
    ```
	- 해당 고도값을 바탕으로 [Google AR Core API WGS84앵커 생성]({% post_url 2025-05-21-Google-AR-Core-API-WGS84앵커-생성 %}#WGS84-앵커) WGS84 고도를 설정하니 임의로 설정한 것 보다는 확실히 가까워졌다는 것이 느껴진다
	- 하지만 아직도 고도가 낮게 잡히는 것으로 느껴진다
	  ![하지만 아직도 고도가 낮게 잡히는 것으로 느껴진다]({{page.img}}하지만 아직도 고도가 낮게 잡히는 것으로 느껴진다.webp)
- ### 고도의 기준 (해수면, 타원체)
	  ![Pasted image 20250521164300]({{page.img}}Pasted image 20250521164300.webp)
	- GPT에게 문제 설명 후 확인한 결과 Google Elevation API는 해수면 기준 고도를 알려준다
	- AR Core의 경우 타원체 기준 고도를 사용하므로 여기서 발생하는 오차가 위와 같은 현상으로 나타난다 (즉 고도가 맞지 않음)
	- ### 정표고(해수면 기준)
		- 해수면을 기준으로 현재 내 위치 고도가 평균 해수면에서 몇 m 있는지 체크
	- ### 타원체
		- 타원체는 지구 표면을 평평한 구로 본다
		- 매끈한 구에서 현재 내 위치 고도가 몇 m 떨어져 있는지 체크
	- 위 사진을 보면 파란선인 해수면 기준에서 지표면의 차이와 타원체인 빨간선에서 지표면의 고도 차이가 N만큼 발생하는 것을 확인할 수 있다
	- **결론적으로 타원체 고도를 구하기 위해서는 `타원체 고도 = 해수면 고도 + 지오이드 분리` 공식이 필요하다**
- ### 고도 보정
	- 기존에는 해당 지오이드 분리값을 받아올 수 있는 API를 사용하고자 했으나, 진행아 안되어 고정값을 구하
	- 지오이드 분리 고도값을 알기 위해  [지오이드 변환 사이트](https://geographiclib.sourceforge.io/cgi-bin/GeoidEval)에서 중앙도서관 해수면 고를 기준으로 확인해본 결과 대략적으로 학교 기준에서 23.5m 정도로 설정하기로 함
	  ![해수면 변환]({{page.img}}해수면 변환.webp)
	- `double geoidSeparation = 23.5;` 보정 고도 값을 설정한 후 
	  `double ellipsoidalHeight = altitude + geoidSeparation;` 최종 고도값을 계산하여 적용
- ### 빌드 및 테스트
	- 테스트 결과 아래에 위치하면 앵커 AR 오브젝트가 옆면이 보이면서 고도가 맞춰진 것을 확인
	- 아직 제대로 테스트는 안해봤으나 지속적으로 이공관, 도서관, 샬롬관, 사거리쪽 고도 테스트를 통해서 진행하고자 함
	  ![아직 제대로 테스트는 안해봤으나 지속적으로 이공관, 도서관, 샬롬관, 사거리쪽 고도 테스트를 통해서 진행하고자 함]({{page.img}}아직 제대로 테스트는 안해봤으나 지속적으로 이공관, 도서관, 샬롬관, 사거리쪽 고도 테스트를 통해서 진행하고자 함.webp)

## Google API의 지형 앵커
- 위 방법 말고 Google API에서 제공하는 지형 앵커를 사용하는 알아서 고도에 맞게 앵커를 배치할 수 있다
- 어떤 이유에서인지는 모르겠으나 Google API를 이용하여 길찾기 등 API 사용이 금지된 것인지 아직 모든 지역에서 사용하지 못하는 것인지 *지원되지 않는 지역*오류로 사용하지 못했다
  ![어떤 이유에서인지는 모르겠으나 Google API를 이용하여 길찾기 등 API 사용이 금지된 것인지]({{page.img}}어떤 이유에서인지는 모르겠으나 Google API를 이용하여 길찾기 등 API 사용이 금지된 것인지.webp)

---
## 링크 및 참고자료

##### 링크 문서
- [Google AR Core API WGS84앵커 생성]({% post_url 2025-05-21-Google-AR-Core-API-WGS84앵커-생성 %})



##### 참고자료(출처)
- [지오이드 변환](https://geographiclib.sourceforge.io/cgi-bin/GeoidEval)
- [고도 종류 설명](https://clouds-daily.tistory.com/124)



