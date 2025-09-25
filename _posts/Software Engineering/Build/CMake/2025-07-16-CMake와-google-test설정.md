---
title: CMake와 google test설정
description: null
date: 2025-07-16
categories:
- Software Engineering
- Build
- CMake
tags:
- CPP
- Cmake
- gtest
img: /assets/img/2025-07-16-CMake와-google-test설정/
---
## CMake와 google test설정
> [CMake 작성 방법]({% post_url 2025-07-16-CMake-기본-작성-방법 %}) 해당 프로젝트를 바탕으로 설정함
> google test는 google에서 제공하며 표준적으로 사용되는 TEST 프레임 워크이다
> 테스트 코드란 개발에 각 기능을 단위 테스트를 통해서 유지보수성을 높이고 보다 효율적이며 오류가 적은 프로그램을 개발할 수 있다
> google test는 Github에서 받아볼 수 있다. [Github Google Test](https://github.com/google/googletest)

### CMake FetchContent로 Google Test 설정
- [Google Test 문서](https://google.github.io/googletest/quickstart-cmake.html#set-up-a-project)에서도 확인할 수 있듯 CMake에서 먼저 `include(FetchContent)`를 추가한다
- 이후 Google Test를 다운받으며, `FetchContent_MakeAvailable`에 추가하여 컴파일에 등록한다
  
  ```text
	# ============================ GoogleTest 추가 =============================
	include(FetchContent)
	
	# GoogleTest v1.17.0 FetchContent 선언 (URL 방식)
	FetchContent_Declare(
	  googletest
	  URL https://github.com/google/googletest/archive/refs/tags/v1.17.0.zip
	)
	# Windows CRT 런타임 충돌 방지
	set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
	# 실제로 다운로드 및 컴파일 시 포함
	FetchContent_MakeAvailable(googletest)
  ```
- `enable_testing()` 이후 해당 설정을 통해 CTest기능을 활성화 한다
- `add_executable(TestAdd tests/Semester.test.cpp)`를 통해 실행 파일로 만들 test.cpp을 작성.
	- 이전에 설정한 내용이 있어 바로 실행파일을 설정하는 `add_executable`를 작성
	- 만일 테스트 코드에 필요한 다른 .cpp, .h이 있다면 [CMake 작성 방법]({% post_url 2025-07-16-CMake-기본-작성-방법 %})을 참고하여 테스트 실행파일의 사용할 라이브러리와 헤더 파일을 먼저 정의한다
- `target_include_directories(SemesterTest PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/inc ${CMAKE_CURRENT_SOURCE_DIR}/lib)` 실행 파일을 먼저 정의했으므로 실팽 파일에 필요한 헤더 파일의 경로를 지정한다
	- *해당 설정 내용에서는 이 부분이 없어도 되는 것을 확인함*
- 마지막으로 `target_link_libraries (SemesterTest PRIVATE GTest::gtest_main GradeManagerLib)` 해당 설정으로 테스트 코드 실행파일에서 사용될 라이브러리, 헤더 파일을 링크한다. 
  **핵심은 GTest::gtest_main를 같이 링크하여 gtest를 사용할 수 있게 만드는 것**
- `include(GoogleTest)`
  `gtest_discover_tests(SemesterTest)`
  해당 설정을 마지막으로 하여 각 테스트들이 `CTest`에 등록될 수 있도록 한다

## 전체 설정 내용
```text
# ============================ GoogleTest 추가 =============================
include(FetchContent)

# GoogleTest v1.17.0 FetchContent 선언 (URL 방식)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/v1.17.0.zip
)
# Windows CRT 런타임 충돌 방지
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
# 실제로 다운로드 및 컴파일 시 포함
FetchContent_MakeAvailable(googletest)

# CTest 기능 활성화
enable_testing()

# 테스트 실행 파일 추가
add_executable(SemesterTest tests/Semester.test.cpp)

# 테스트에서 인클루드할 헤더 경로 지정 (inc/)
target_include_directories(SemesterTest PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/inc ${CMAKE_CURRENT_SOURCE_DIR}/lib)

# 테스트용 바이너리에 GTest 및 프로젝트 라이브러리 링크
target_link_libraries(SemesterTest PRIVATE
    GTest::gtest_main
    GradeManagerLib
)

# 테스트 자동 등록
include(GoogleTest)
gtest_discover_tests(SemesterTest)
```



---
## 링크 및 참고자료

##### 링크 문서
- [CMake 기본 작성 방법]({% post_url 2025-07-16-CMake-기본-작성-방법 %})

##### 참고자료(출처)
- 



