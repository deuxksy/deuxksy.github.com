---
layout: post
title:  Which DevOps solution should I choose in a non-Internet environment?
date:   2018-12-09 07:13:00
categories: [devops]
---
# 폐쇄망 에서는 어떤 DevOps 솔루션을 선택 할까

생각 하기도 싫은 거지 같은 환경 이지만 생각 보다 이런 경우가 많더라  

- ***서버 접속 권한 없음 Tomcat 만 줄테니깐 나머지는 내가 알아서***
- ***Tomcat Mananger 접속이 가능 하고 war 파일 업로드는 가능***
- 인터넷과 통신이 가능한 Nexus 3 (이후 Nexus 3) 가 있음
- 개발자 들은 Nexus 3 로 접속 불가 별도의 Nexus 를 구축
- 보안 이슈로 인해서 네트워크 폴더 안됨 메신저가 있지만 용량제한 20M 속도 느림
- 개발자들 간의 파일 전송 어떻게

기능 | 외부망 솔루션 | 폐쇄망 솔루션
:-- | :--: | --:
라이브러리 관리 | Maven Central  | [Nexus2](https://help.sonatype.com/repomanager2/download#Download-NexusRepositoryManager2OSS)
버전관리 및 코드리뷰 | GitHub  | [GitBlit](http://gitblit.com/) + [Gerrit](https://www.gerritcodereview.com/)
타스크 및 일정 관리 | Trello | [Lavagna](https://lavagna.io/)
DB Client | 니가 쓰던거 | [Tadpole DB](https://sites.google.com/site/tadpolefordb/)
파일공유 | SAMBA | [Jackrabbit](http://jackrabbit.apache.org/jcr/index.html)

Gerrit 설치시에는 추가 이슈가 있지만 이렇게 구축을 하니깐 왠만한 조건들을 만족 하면서  
프로젝트 운영에 수월 했음