---
date: 2021-04-12 19:10:00
layout: post
title: Jekyll에서 방금 업로드한 post가 보이지 않는 경우
subtitle:
description:
image: /assets/img/uploads/new-post.png
category: blog
tags:
 - jekyll
author: chanoyoung
---

로컬에서는 포스트가 잘 보였는데, 깃헙 페이지에서는 포스트가 보이지 않는 경우가 있다.

Jekyll 은 기본적으로 설정된 date가 미래이면 포스트를 보여주지 않는데, 로컬에서는 운영체제의 시간대를 따라가지만 깃헙 페이지는 시간대가 달라서 생기는 문제인 것 같다.

이를 해결하기 위해서 한국 시간대인 UTC+0900을 다음과 같이 명시해주면 된다.
```
date: 2021-04-11 16:00:00+0900
```

매 포스트마다 이를 작성하기 번거로운 경우 _config.yml 파일에 다음과 같이 추가하면 모든 포스트에 대해서 적용이 된다.

```yml
timezone: Asia/Seoul
```


참고 : [Posting Jekyll Content on Time](https://mehmandarov.com/jekyll-content-on-time/)