---
layout: post
title:  Git Tag Rename
date:   2018-12-26 05:03:00
categories: [git]
---

# Git Tag Rename

git tag 를 남기다가 오타로 인해서 다시 남겨야 할때

```bash
git tag new old
git tag -d old
git push origin :refs/tags/old
git push --tags
```

## 참조
[How do you rename a Git tag?](https://stackoverflow.com/questions/1028649/how-do-you-rename-a-git-tag)
