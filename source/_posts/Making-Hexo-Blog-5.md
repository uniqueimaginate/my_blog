---
title: 'Making Hexo Blog #5'
date: 2020-05-05 00:57:03
tags: Hexo, Blog, Google Search
---
# Heo Blog 만들기 # 5

## Hexo 블로그를 Google Search 에 등록하기

<!-- more -->
이전 포스팅에 이어서 이번에는 Google Search 에 등록을 해봅니다.

### Google Search 속성 추가    

1. 먼저 [Google search console](https://search.google.com/search-console/about) 로 가서 각자의 도메인을 등록해야 합니다.
2. 사이트에서 Start Now 버튼을 누르게 되면 속성 추가가 사이트 왼쪽 위에 보이게 될 것 입니다.
3. 속성 추가를 눌러 봅시다.
{% asset_img 1.png %}
4. Github pages 를 통해서 배포하므로 저희는 오른쪽 URL 접두어를 통해서 진행할 것 입니다.
{% asset_img 2.png %}
5. 각자의 URL 을 값으로 넣고 다음을 누릅니다.
6. 다음과 같은 화면이 보입니다. 
{% asset_img 3.png %}
7. 여기서 저의 theme 을 기준으로 보면, html file 을 다운 받는다면 어디에 놓아야 할지 잘 몰랐기 때문에, 저 같은 경우 다른 확인 방법으로 HTML 태그 를 복사하는 것을 선택했습니다.
{% asset_img 4.png %}
8. 태그를 복사합니다.
9.  이제 local 환경으로 갑니다.
10. Hexo 폴더에서 /theme/테마이름/layout/partial/head.jade 파일을 찾아 갑니다.
11. 그 파일에 복사한 태그를 붙히면 끝입니다.

저의 head.jade 파일은 다음과 같습니다.    
```jade
meta(charset="utf-8")
meta(name="X-UA-Compatible", content="IE=edge")

//-   이번에 복사한 태그 입니다.
meta(name="google-site-verification" content="제 태그")

title 
    block site_title
        = config.title
block description
    meta(name="description", content= config.description ? config.description : 'A Blog Powered By Hexo')

meta(name="viewport", content="width=device-width, initial-scale=1")
link(rel="icon", href=url_for(theme.favicon))
link(rel="stylesheet", href=url_for("css/apollo.css"))

- var xml = config.url + '/atom.xml'
    link(rel="search", type="application/opensearchdescription+xml", href=xml, title=config.title)
    

```

이상으로 포스팅을 마치겠습니다.
5번에 걸친 Hexo Blog 만드는 포스팅을 진행했네요.    
제가 블로그를 만들면서 겪은 시행착오들이 상당히 많아서 그런 것들을 이 포스팅을 보는 사람은 하지 않기를 하는 바람에서 글을 씁니다.    
다른 질문이 있다면 댓글로 남겨주시면 감사하겠습니다.