---
layout: post
title: Checking pip list while running Python
date: 2018-08-26 14:59:00
categories: [Python]
tags: [Python, pip]
---
Python Package 검색인 pip list 기능을 Source Code 에서 확인 할수 있는 방법

    import pkg_resources
    from pip._internal.utils import misc

    for d in misc.get_installed_distributions():
        print(d)

    for d in pkg_resources.working_set:
        print(d)