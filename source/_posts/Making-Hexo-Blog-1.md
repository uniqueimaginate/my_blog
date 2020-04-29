---
title: 'Making Hexo Blog #1'
date: 2020-04-29 16:40:55
tags: hexo
---

## Hexo Blog 만들기 # 1

Hexo 플랫폼을 이용해 만든 블로그입니다.

<!--more-->

1. Node.js 와 git 을 각자의 OS 에 맞게 설치를 합니다.
    - [Node.js 설치 (버전은 10.0 이상을 권장합니다.)](https://nodejs.org/en/)
    - [git 설치](https://git-scm.com/)
2. Hexo 를 설치합니다.   
    <pre><code>npm install hexo</code></pre>
3. 이제 hexo 를 사용하면 됩니다.    
    <code>npx hexo \<command> </code>    
    리눅스 유저는 다음과 같이 경로 설정을 하면 됩니다.
    <pre><code>
        echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
    </code></pre>
    경로 설정을 하면 다음과 같이 사용할 수 있습니다    
    <code>hexo \<command></code>


더 자세한 설명은 [Hexo Doc](https://hexo.io/docs/)에서 볼 수 있습니다.