---
date: 2021-04-15 23:00
layout: post
title: Jekyll LiveReload 적용하기
subtitle:
description:
image: 
category: blog
tags:
 - jekyll
author: chanoyoung
---

Jekyll 테마를 수정하거나 새로운 글을 작성할 때 확인을 위해 매번 새로고침을 하는 것은 여간 번거로운게 아니다.

이를 해결하기 위해 [Jekyll 3.7.0](https://jekyllrb.com/news/2018/01/02/jekyll-3-7-0-released/)부터 수정사항이 생길시 자동으로 새로고침이 되는 LiveReload 기능이 포함되었다. (현재 페이지와 상관 없는 파일이 수정되어도 새로고침이 되는 단점은 있다.)

다음과 같이 실행 명령어 뒤에 -\-livereload 만 붙이면 간단하게 적용된다.

```
jekyll serve --livereload  
```
또는
```
bundle exec jekyll serve --livereload
```


---

위 방법만으로 간단한게 적용이 되면 좋겠지만, 다음은 내가 겪은 에러와 해결방안이다.

일반 실행에는 문제가 없는데, -\-livereload를 붙이자 다음과 같은 에러가 나면서 Jekyll 이 실행이 되지 않았다.
![capture_1](/assets/img/uploads/jekyll_livereload_1.jpg)

검색해 보았을 때 Stack Overflow 등에서 중복되어 나오는 답변은 다음 명령어로 eventmachine을 삭제하고 새로 설치하라는 것이었는데, 내 경우에는 도움이 되지 않았다.

```
gem uninstall eventmachine  
gem install eventmachine –platform ruby
```

이후에 혹시나 하는 마음에 Ruby 2.5, 2.6, 2.7 를 버전별로 설치해보는 등 여러 방법들을 시도해 보았지만, 해결이 되지 않았다.

그리고 며칠 뒤 마지막으로 한번만 더 시도해보자는 심정으로 검색을 하다가 해결책을 찾았다.

Gemfile에 다음 한 줄을 추가하는 것으로 해결이 되었다. 결국 eventmachine 문제가 맞았다.
```
gem 'eventmachine', '1.2.7', git: 'https://github.com/eventmachine/eventmachine', tag: 'v1.2.7'
```

참고 : [Jekyll - Unable to load the EventMachine C extension](https://robbinespu.gitlab.io/blog/2020/10/16/jekyll-unable-to-load-the-eventmachine-c-extension/)


bundle install 을 통해 eventmachine 을 새로 받은 뒤 정상적으로 실행이 되었다.
![capture_2](/assets/img/uploads/jekyll_livereload_2.jpg)