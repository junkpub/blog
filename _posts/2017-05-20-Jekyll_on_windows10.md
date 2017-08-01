---
layout: post
title:  "Windows10에 Jekyll 설치하기"
date:   2017-05-20 00:00:32 +0900
categories: blog
tags: jekyll github-pages
---
Markdown viewer가 있는 에디터를 고르다 Visual Studio Code를 알게 됐다. 이런저런 리뷰를 찾아보니 윈도우를 선호하는 나에게 꽤 잘 맞는 프리웨어이지 싶어서 사용하기로 결정. 평소 Ubuntu에서 블로그를 작성했었는데 윈도우에서 VSCode를 통해서 작성하는게 낫겠다 싶어 윈도우에 Jekyll을 설치해보면서 그 과정을 정리했다. 대부분 내용은 원본 페이지의 내용을 번역해서 기록해 놓은 수준이고 내가 격은 삽질을 방지하기 위해 약간의 내용을 추가했다.

Jekyll에서 윈도우에 설치하는 방법을 설명하고 있어서 그대로 따라했는데, ruby버전 문제 등 약간의 시행착오가 있었다. 뭐, 엄청난 삽질은 아닌데 다음에 같은 삽질하기 싫어서... 

## Jekyll on Windows
역시나 윈도우에서 Jekyll용 페이지는 바로 볼 수 없다... 망할. 먼저 `Chocolatey`라는 패키지 매니저를 먼저 설치해야 한다. `Chocolatey`를 통해서 `ruby`를 설치하고 `ruby`의 gem 명령어를 통해 `Jekyll`을 설치하는 방식이다. 이 페이지를 참고하자 [Jekyll on Windows](https://jekyllrb.com/docs/windows/).

## Chocolatey 설치
먼저, `Chocolatey`를 설치하자. 설치하는 방법은 그리 어렵지 않다. 커맨드창이나 파워쉘을 열어서 명령어 입력하면 끝이다.
#### cmd.exe 에서 설치
커맨드창을 관리자모드로 먼저 실행시키고 다음 명령어를 실행하자. 커맨드창을 통해서 하지만 파워쉘을 이용하는듯 하다. 정확한 원리는 모르겠다... 파워쉘도 잘 모르고... 그냥 따라하자.
```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient
```

#### PowerShell.exe 에서 설치
파워쉘을 이용하면 몇 가지 확인이 필요하다. [Get-ExecutionPolicy](https://technet.microsoft.com/ko-KR/library/hh847748.aspx)가 Restricted가 아닌지 확인을 해야한다. `Get-ExecutionPolicy`를 실행시키면 결과를 반환하는데 결과가 `Restricted`면 `Set-ExecutionPolicy AllSigned`를 실행하자. `AllSigned`대신 `Bypass`를 사용해도 무관.
```
# Don't forget to ensure ExecutionPolicy above
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'
```

## Ruby 2.2.4설치
다음 과정은 Chocolatey를 이용해 Ruby를 설치한다. 설치시에 주의할 점이 있다면 Jekyll 구동에 필요한 nokogiri가 Ruby 2.2.4버전만 지원한다는 점이다. 때문에 `choco install ruby -y`를 사용하게 되면 자동으로 가장 최신버전(현재 2.4)을 설치해서 nokogiri를 정상적으로 설치할 수 없게 된다. 다음의 명령어를 이용해 Ruby 2.2.4버전을 설치해주도록 하자.

커맨드창으로 관리자모드로 다시 실행시키고 다음을 실행하자. (Chocolatey설치가 완료되면 커맨드창을 관리자모드로 다시 실행시켜야 Chocolatey 명령어를 사용할 수 있다.)
* `choco install ruby -version 2.2.4`
* `choco install ruby2.devkit`

위의 과정이 정상적으로 수행됐다면 `C:\tools\ruby22`에 Ruby2.2.4버전이 정상적으로 설치된 것을 확인할 수 있다.

만일 실수로 2.2.4가 아닌 다른 버전을 설치했다면 제거하고 위의 명령어를 이용해 2.2.4버전으로 다시 설치해주자. 제거하는 방법은 Ruby가 설치된 폴더로 가서 `unins000.exe`를 실행하면 된다. 2017년 5월 기준으로 최신버전을 설치했다면 폴더는 `C:\toos\ruby24`로 되어 있을 것이다.

## Ruby development kit 설정
Jekyll 공식 사이트에 나와 있는데로 그대로 따라해주면 된다. 딱히 어려울건 없다.
* `C:\tools\DevKit2`로 이동
* `ruby dk.rb init`을 실행하여 `config.yml`생성
* `config.yml`에 다음 경로를 추가 `- C:\tools\ruby22`
* `ruby dk.rb install` 실행

## Nokogiri gem installation
Nokogiri gem은 github-pages에 필요한 내용으로 Windows x64에서 사용하려면 몇 가지 작업을 수행해야 한다.
```
choco install libxml2 -Source "https://www.nuget.org/api/v2/"
choco install libxslt -Source "https://www.nuget.org/api/v2/"
choco install libiconv -Source "https://www.nuget.org/api/v2/"

gem install nokogiri --^
   --with-xml2-include=C:\Chocolatey\lib\libxml2.2.7.8.7\build\native\include^
   --with-xml2-lib=C:\Chocolatey\lib\libxml2.redist.2.7.8.7\build\native\bin\v110\x64\Release\dynamic\cdecl^
   --with-iconv-include=C:\Chocolatey\lib\libiconv.1.14.0.11\build\native\include^
   --with-iconv-lib=C:\Chocolatey\lib\libiconv.redist.1.14.0.11\build\native\bin\v110\x64\Release\dynamic\cdecl^
   --with-xslt-include=C:\Chocolatey\lib\libxslt.1.1.28.0\build\native\include^
   --with-xslt-lib=C:\Chocolatey\lib\libxslt.redist.1.1.28.0\build\native\bin\v110\x64\Release\dynamic
```

## Install github-pages
이제 윈도우10에서 github-pages를 띄워기 위한 기반작업은 끝났다. 다음 작업을 수행해 github-pages를 설치하자.
* 커맨드창을 이용해 [Bundler](http://bundler.io)를 설치
* Root폴더(블로그의 내용을 담게 될 폴더)를 생성하고 그 폴더 안에 `Gemfile`을 생성
* `Gemfile`에 다음 내용을 추가
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```
* Root폴더에서 커맨드창을 열고 `bundle install` 명령어를 실행하여 github-pages를 설치 

## 로컬에서 github-pages를 띄워보자
gihub-pages를 설치했다고 해서 바로 볼 수 있는것은 아니다. jekyll을 이용해 로컬에서 github-pages를 띄울 수 있도록 마무리 작업이 필요하다. 위의 과정에서 github-pages를 설치한 root폴더로 가서 다음 커맨드를 실행하자.

`jekyll serve`

![jekyll 구동 화면]({{ site.baseurl }}/imgs/20170520-jekyll_serve.png)

몇 가지 warning 메세지가 발생하는데 이에 대한 해결방법은 다음에 확인해보자.
브라우저를 열고 `127.0.0.1:4000`로 접근해보자. Root의 폴더구조를 볼 수 있다.
![기본 페이지]({{ site.baseurl }}/imgs/20170520-default-github-pages.png)

아무런 내용 없이 폴더구조가 뜨는 이유는 아직 `index.html`이 없기 때문이다. `Ctrl-C`로 jekyll을 종료 후에 임시로 아무 `index.html`를 생성해서 `jekyll serve`수행 한 후에 다시 접근해보면 정상적으로 페이지가 뜨는 것을 확인해볼 수 있다.
![index 추가한 임시 페이지]({{ site.baseurl }}/imgs/20170520-index-github-pages.png)

Jekyll을 구동할 때에 여러가지 옵션들을 사용할 수 있다. 이 내용은 다음에 적기로 하고 참고를 위해 링크를 남겨둔다. [Jekyll 기본 사용법](https://jekyllrb.com/docs/usage/)

## github-pages 구동 요약
여기까지해서 github-pages를 로컬에서 띄워봤다. 뭐... 별 어려움은 없었으면 좋겠다는 바램이다ㅠ. 다음 블로깅에서 스킨 및 플로그인 적용 등의 내용들을 추가적으로 설명하겠지만 기본으로 다음 순서로 진행하면 된다.
* `bundle install` (Gemfile이 수정된 상황에 수행. Gemfile이 수정되지 않았다면 넘어가도 된다.)
* `Jekyll serve`
* `127.0.0.1:4000`에서 확인

## 끝내며
Github를 이용해 자신만의 블로그를 무료로 이용할 수 있다는 점은 확실히 메리트가 있다. 나중에 따로 기술하겠지만 jekyll에서 사용가능한 여러 스킨들과 플러그인이 있기 떄문에 자신의 입맛에 맞게 꾸미는 재미도 있고. 근데... 꾸미다 보니 배보다 배꼽이 더 커져가는것처럼 보이는건 착각이겠지? -_-ㅋ

윈도우 신봉자인 나에게 윈도우10에서 jekyll을 사용할 수 있다는건 아주 좋은 일이다ㅋㅋ. Atom이랑 sublime도 사용은 해봤는데 영 맘에 안들어서 그냥 linux에서 작업했었는데 VSCode가 나와줘서 정말 다행이다ㅠㅠ.

이 글이 다른 분들에게 크게 도움이 될 지는 모르겠지만 조금이나마 도움이 되길 바라며~ 