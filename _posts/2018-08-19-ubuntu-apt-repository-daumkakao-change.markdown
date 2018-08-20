---
layout: post
title:  Ubuntu APT Repository DaumKaKao 로 변경하기
date:   2018-08-19 00:53:39 +0900
categories: [Ubuntu, APT]
---
    #!/bin/sh
    SL=/etc/apt/sources.list
    cp ${SL} ${SL}.org
    ## 
    sed -e 's/\(us.\)\?archive.ubuntu.com/ftp.daumkakao.com/g' -e 's/security.ubuntu.com/ftp.daumkakao.com/g' < ${SL}.org > ${SL}
    ## check
    apt update

* [우분투의 apt 기본 미러를 다음 카카오로 변경][req-1]
 
[req-1]: https://gist.github.com/lesstif/8185f143ba7b8881e767900b1c8e98ad