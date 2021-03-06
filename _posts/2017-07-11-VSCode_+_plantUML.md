---
layout: post
title:  "VSCode과 plantUML로 UML작성하기(설치편)"
date:   2017-07-11 00:00:32 +0900
categories: blog
tags: UML VSCode plantUML
---
이번에 소개할 내용은 `VSCode`와 `plantUML`을 이용한 UML작성이다.

솔직히 UML을 자주 쓰지는 않지만(귀찮...) 간만에 UML을 작성할 일이 생겨 무료 UML툴이 어떤게 있나 검색을 해봤다. 기존에 썼었던 starUML을 다시 써볼까 고민했는데, 망할 이제 유료다.[^1] 시퀀스다이어그램 용으로 사용하던 `websequencediagram`은 텍스트로 다이어그램을 그릴 수 있어서 좋긴한데 주소명 그대로 시퀀스 다이어그램만 지원한다ㅠㅠ.

그러다 몇몇 사람들이 `plantUML`을 추천하는 것을 보고 호기심에 들어갔는데... 꽤 마음에 든다! `Websequencediagram`처럼 텍스트로 다이어그램을 그리도록 되어 있는데 시퀀스 다이어그램 뿐 만 아니라 클래스, 액티비티, 컴포넌트, 상태, 객체 등등 대부분의 다이어그램을 다룰 수 있으며 게다가 `VSCode`의 확장기능으로 쓸 수 있고 미리보기도 지원한다.

[^1]: 완전 유료는 아니다. 2.0부터 유료이긴 하지만, 예전부터 무료로 사용해오던 1.0과 1.0의 오픈소스를 이용해 새로 만든 5.0은 무료이다. 소문으로는 2.0는 원작자가 만든 버전이라는 듯...

## VSCode 설치
`VSCode`의 확장기능으로 `plantUML`을 사용하는거니까 당연히 `VSCode`를 먼저 설치해한다. 바로 [VSCode 공식페이지](https://code.visualstudio.com/)로 가서 `VSCode`를 설치하자. `VSCode`의 사용법 단축키 등은 나중에 따로 포스트할 예정.

## VSCode에 PlantUML 확장기능 설치
설치가 완료됐으면 `VSCode`를 실행한 후에 VS Code Quit Open(Ctrl+P)을 실행하자. 상단 중앙에 텍스트입력창이 뜨면 `ext install plantuml`을 입력하자. 화면 왼쪽에서 `PlantUML`을 찾아서 바로 설치하자.

## 다이어그램 렌더링을 위한 준비
텍스트로 작성한 UML을 제대로 렌더링 하기 위해선 다음의 사전작업이 필요하다.
* [Java](https://www.java.com/en/download/) : `plantUML`은 `Java`를 통해서 실행
* [Graphviz](http://www.graphviz.org/Download..php) : 모든 다이어그램을 정상적으로 렌더링 하기 위해 필요

## VSCode에서 확인
이제 모든 작업이 완료 됐으니 실제로 UML이 제대로 작성되는지 확인해 볼 차례다. `VSCode`를 열고 새로 파일을 만들어서 다음의 예제코드를 작성해보자. 작성이 끝났으면 다이어그램 미리보기 창(Alt+D)를 열어 확인해보자. 시험삼아 내용을 변경해보면 실시간으로 다이어그램이 변경되는 것을 확인해볼 수 있다! 추가적으로 파일의 확장자를 wsd로 저장할 경우 syntax hilight
```
@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml
```

## 끝내며
막상 써보니 생각보다 훌륭하다. 단점이라면 제대로된 다이어그램을 그리기 위해서는 문법들을 익혀야한다는 점. 반면, 다양한 종류의 다이어그램을 텍스트를 이용해 그릴 수 있다는 부분은 큰 장점이다.

다음 블로그에서는 `plantUML`을 제대로 사용하기 위한 문법을 알아보자. 뭐, 시퀀스 다이어그램이랑 클래스 다이어그램 정도만 짚고 넘어가면 될 듯 하다. 나머지는 나중에 필요해지면 그 때... 당장 급한 사람들은 [plantUML 공식페이지](http://plantuml.com/)로~