---
layout: post
title:  "뇌를 자극 하는 TCP/IP 소켓프로그래밍"
date:   2017-03-20 00:00:32 +0900
categories: book
tags: tcp/ip socket
---
소켓 프로그래밍에 대해 기본적인 지식이 없어서 한 번 익혀보기로 했다. 흥미가 없어서 대학생 시절 수업도 대강 듣고 말았는데... 다 까먹게 되버린ㅋㅋㅋ 젠장

"뇌를 자극하는 TCP/IP 소켓 프로그래밍"이란 책을 구매하여 다시 기초부터 공부하기로 했다. 이 포스트에서는 책을 보면서 중요하다고 생각되는 부분과 이해가 되지 않는 부분 위주로 적어나갈 예정이다. 음... 책 리뷰형태가 되려나??

#### OSI 7계층과 TCP/IP 4계층

#### Blocking/Non-Blocking

#### Sync/Async I.O

#### Overlapped I.O

#### Sync/Async Notification

#### Iterative Server/Concurrent Server

#### 일반적인 socket 모델
1. Select 모델
    * Iterative Server + Non-Blocking Socket + Sync I.O + Async Notification
2. WSAAsyncSelect 모델
    * Iterative Server + Non-Blocking Socket + Sync I.O + Sync Notification
3. WSAEventSelect 모델
    * Iterative Server + Non-Blocking Socket + Sync I.O + Async Notification
4. Overlapped 모델
    * Concurrent Server + Non-Blocking Socket + Async I.O + Async Notification
    * 입출력 완료를 이벤트를 통해 알아내는 방법
    *  입출력 완료를 완료 루틴(콜백 함수)를 사용해서 알아내는 방법
5. IOCP 모델
    * Concurrent Server + Non-Blocking Socket + Async I.O + Async Notification
    * 효율적인 스레드 사용으로 가장 좋은 성능을 내도록 구현

#### Atomic
이건 아직 좀 더 찾아보고 이해가 많이 필요한 수준이다. 일단은 간단하게 참고 사이트만 적어놔야지.

>[c++ std::atomic](http://egloos.zum.com/seeper/v/3059861)
>
>[Memory Visibility(메모리 가시성)와 Memory Barrier(메모리 장벽)](http://blog.naver.com/PostView.nhn?blogId=jjoommnn&logNo=130037479493)
