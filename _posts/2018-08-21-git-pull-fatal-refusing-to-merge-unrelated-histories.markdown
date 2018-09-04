---
layout: post
title:  git pull fatal refusing to merge unrelated historiess
date:   2018-08-21 01:49:00
categories: [Git]
tags: [Git, pull]
---
github 에서 repository 만들고 local 에 있는 Source 에 git remote add orign ${GIT_URL} 하고 git pull

    D:\ZZiZiLY\Version\Git\spring-boot-skeleton-multi-module>git pull
    fatal: refusing to merge unrelated histories

    D:\ZZiZiLY\Version\Git\spring-boot-skeleton-multi-module>git pull --allow-unrelated-histories
    Merge made by the 'recursive' strategy.
    .gitignore | 23 +++++++++++++++++++++++
    1 file changed, 23 insertions(+)
    create mode 100644 .gitignore

오류가 발생 하냉 머징???

    git pull --allow-unrelated-histories**

문재는 해결 되었다

## 참조
* [Git refusing to merge unrelated histories on rebase](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase)