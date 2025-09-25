---
title: System Call
description: null
date: 2025-09-18
categories:
- Computer Science
- 운영체제
tags:
- 운영체제
- 컴퓨터공학
img: /assets/img/2025-09-18-System-Call/
---
## System Call
>사용자가 커널에서 제공하는 기능을 사용하기 위해서는 System Call Interface를 통해서 요청을 해야 하는데 이를 System Call이라 부른다

사용자가 응용프로그램을 마우스 더블 클릭으로 오픈할 때는 아래와 같은 과정이 발생한다
- 유저 모드에서 사용자가 더블클릭으로 Open한다
- 시스템 콜 인터페이스에 이벤트가 발생하고, 커널에서는 응용프로그램을 Open하는 기능을 수행한다
- 이후 커널은 작업을 마친 후 시스템 콜 인터페이스에 알린다
- 이후 응용프로그램이 오븐이 되며 이때 fd라는 개념이 발생



---
## 링크 및 참고자료

##### 링크 문서
- [Shell]({% post_url 2025-09-25-Shell %})

##### 참고자료(출처)
- 



