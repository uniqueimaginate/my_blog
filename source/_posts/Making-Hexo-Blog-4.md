---
title: 'Making Hexo Blog #4'
date: 2020-05-04 23:35:57
tags: Blog, Hexo, Google analytics, Google search
---
# Hexo Blog 만들기 # 4

## Hexo 블로그를 Google Analytics 에 등록하기

<!-- more -->

저의 테마인 apollo 를 기준으로 설명합니다.
<br>

### Google Analytics 가입     

1. 먼저 Google Analytics 가입부터 진행합니다.
2. 설정 창으로 이동합니다. 왼쪽 아래에 톱니바퀴를 누르시면 됩니다.
3. Create Account 를 누릅니다.
4. 다음의 과정을 진행합니다{% asset_img 1.jpg %}
5. {% asset_img 2.jpg %}
6. 양식에 맞게 작성해줍니다.{% asset_img 3.png %}
7. 다 마무리 하면 다음과 같은 창이 나오게 됩니다. 검은 색 칠이 된 부분은 본인만 알고 있으면 됩니다.{% asset_img 4.jpg %} 여기서 트래킹 ID 를 복사해 두시면 됩니다.

### Google Analytics 를 Hexo에 적용
1. 각자의 테마에서 Google Analytics 를 지원해주는 경우
   1. Hexo 폴더에서 theme 폴더에 들어간 후, 자신이 사용중인 테마 폴더로 들어갑니다.
   2. _config.yml 파일을 봅니다. (Hexo 폴더에도 _config.yml 파일이 있습니다. 헷갈리면 안됩니다.)

```yml
    # Analytics
    
    ga: UA-*********-*

    # 또는 

    Google Analytics: UA-*********-*
    
    # 별 표시 된 부분을, 위에서 얻은 트래킹 ID 를 바꾸어 주면 자동으로 연동 된다.
```

2. 각자의 테마에서 Google Analytics 를 지원해주지 않는 경우



```jade
//- Google analytics
script(async src="https://www.googletagmanager.com/gtag/js?id=UA-*********-*")

script.
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());

    gtag('config', 'UA-*********-*');
```
위의 code 는 Google Analytics 에서 제공하는 gtag.js 입니다. Google Analytics 가입 6번 그림에서 나온 코드를 Jade 문법으로 살짝 바꾼 코드입니다. 이 code 를 테마 폴더 안에 partial 폴더 안에 있는 scripts.jade 파일에 붙힙니다.
<b>여기서 자신의 트래킹 코드를 별 표시 되어 있는 code 를 대체해야 합니다.</b>

이제 Google Analytics 연동은 끝났습니다. 보통 Hexo theme 은 Jade 이거나 Pub 파일일 것입니다. 크게 다르지 않을 것이나, 각자의 문법에 맞게 작성하면 연동은 무리 없이 잘 될 것입니다.

다음 포스팅은 이제 Google Search 에 등록하는 법을 알아보겠습니다. 