---
layout: post
title:  "Linux 터미널 명령어 정리"
date:   2017-12-20 00:00:32 +0900
categories: blog
tags:
hidden: false
---
## Linux(Ubuntu)를 공부하면서 필요한 명령어 정리
ps : 프로세스 관련 명령어
```
ps -ef | grep $PROCESS_NAME
```
dpkg : 패키지 관련 명령어
```
dpkg -l | grep $PACKAGE_NAME
```
apt(Advanced Packagin Tool) : 패키지 관리 명령어
```
apt-get install $PACKAGE_NAME   >> 패키지 설치
apt-get remove $PACKAGE_NAME    >> 패키지 제거
apt-get purge $PACKAGE_NAME     >> 패키지 설정파일까지 모두 제거
apt-cache search $PACKAGE_NAME  >> 설치할 수 있는 패키지 검색
apt update                      >> 패키지 최신 정보를 가져오기. 시스템 패키지 업데이트
apt upgrade                     >> update로 가져온 최신정보로 각 패키지 업그레이드 하기. 시스템 업그레이드
apt full-upgrade                >> 커널 버전까지 시스템 업그레이드
apt autoremove                  >> 사용하지 않는 패키지 삭제
apt autoclean                   >> 다운로드된 패키지에서 오래된 저장소 삭제
apt clean                       >> 위와 동일
apt content $PACKAGE_NAME       >> 패키지가 설치된 위치 확인. 대응 명령어 : dpkg -L
apt depends $PACKAGE_NAME       >> 패키지의 디펜던시 확인. 대응 명령어 : apt-get check, dpkg -C
apt show $PACKAGE_NAME          >> 패키지 정보 확인. 대응 명령어 : apt-cache show, dpkg -p
apt check $PACKAGE_NAME         >> 패키지의 디펜던시가 깨졌는지 확인
apt recommends $PACKAGE_NAME    >> 제공된 패키지에서 빠진 패키지에 대한 목록 보여주기
apt version $PACKAGE_NAME       >> 패키지 버전 체크
```
service : 서비스 관리
```
service $SERVICE_NAME start
service $SERVICE_NAME stop
service $SERVICE_NAME restart
service $SERVICE_NAME status
```
find : 파일이나 디렉터리 찾을 때 사용
```
find ~/ -type f -name $FILE_OR_DIR_NAME
```