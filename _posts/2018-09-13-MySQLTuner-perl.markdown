---
layout: post
title:  MySQLTuner-perl
date:   2018-09-13 22:52:00
categories: [mysql, tuner]
---
DB 대한 경험이 별로 없다 보니 튜닝을 해야 할때 어려움이 많은되 [MySQLTuner-perl](https://github.com/major/MySQLTuner-perl) 도움을 받는다면?<br>
perl 만 있다고 동작 하지는 않음 mysqladmin 이 있어야 동작함 검사 결과 중간에 [!!] 문재가 있는 부분 수정해야 하는 부분<br>
그리고 마지막에 나오는 부분이 my.cnf 또는 server.cnf 가서 옵션을 조정 해야함<br>
---------- Recommendations ------------------------------