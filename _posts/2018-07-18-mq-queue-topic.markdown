---
layout: post
title:  Queue 와  Topic  차이
date:   2018-07-18 22:38:39
categories: MQ
---
* Queue

Fist In First Out (FIFO) 먼저 입력한 데이터가 먼저 나오는 구조 <br>
Producer(생성자) 데이터를 생성후 Queue 에 적재를 하고 Consumer(소비자) 가 있으면 전달 없으면 <br>
Consumer 가 있을때 까지 계속 대기 Queue 에 적재된 데이터는 하나의 Consumer 만 받을 수 있다.

* Topic

Publish(발행) 와 Subscribe(구독) 이루어져 있다. 메세지를 Publish 하면 다수가 Subscribe 을 할수 있다.