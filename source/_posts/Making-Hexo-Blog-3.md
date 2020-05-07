---
title: 'Making Hexo Blog #3'
date: 2020-05-04 11:44:39
tags: Github pages, Travis CI, deploy
---
# Hexo Blog 만들기 # 3

## Hexo 블로그를 github pages 를 통해서 배포하기

<!-- more -->

#### Github 에서 repository 만들기    

먼저 이 포스팅은 <사용자id>.github.io 를 만드는 포스팅이 아니라는 점을 명시하고 시작하고자 합니다. 이유는 저와 같은 personal 이용자들은 Github Pages 가 오직 master branch 를 통해서만 deploy 됩니다.


그러나 아래의 그림과 같이 <사용자id>.github.io 라고 이름을 짓지 않고 프로젝트 이름을 넣어준다면 master branch 가 아닌 다른 branch 를 source 로 설정하게 될 수 있게됩니다. (이 부분에서 막혀서 꽤나 헤맸습니다. ㅠ)

{% asset_img "name.png" %}
{% asset_img "source_branch.png" %}

여기까지 완성 후에 이제 local 에 만든 Hexo 폴더를 github 로 push 해줍니다.
<hr>

### Travis CI 와 연동하기

1. Github 계정과 Travis CI 를 연동합니다. 다음의 링크로 가셔서 연동하면 됩니다.
[Travis CI 연동하기](https://github.com/marketplace/travis-ci)

2. 그 다음 [Application Setting](https://github.com/settings/installations) 으로 가서 Travis CI 가 만들어 놓은 repository 와 연동되게끔 설정해 줍니다. 저와 같은 경우 다음과 같이 되어 있습니다.
{% asset_img TravisCI.png %}

3. 이제 여러분의 repository 토큰을 새로 만들어야 합니다.     
   [토큰 만들기](https://github.com/settings/tokens) <- 여기로 가셔서 Generate new token 을 누르시면 됩니다.
   {% asset_img token.png %}
    <b>위의 사진과 같이 scope 는 repo 만 선택하시면 됩니다.</b>
4. Generate token 을 하면 토큰이 번호+문자 조합으로 나옵니다. 이 것을 복사해둡시다.
5. 이제 Travis page 로 갑니다.
6. 해당 repo 의 Setting 에 가게 되면 Environment Variables 가 나옵니다. 여기서 Name에 GH_TOKEN 이라 적고, Value 값으로 복사해둔 토큰을 적고 Add 를 누릅니다.
7. 이제 local 에 있는 각자의 Hexo 폴더로 가면 _config.yml 과 package.json 이 있을 겁니다. 그 폴더에 다음의 .travis.yml 파일을 저장합니다.
```yml
sudo: false
language: node_js
node_js:
  - 10 # use nodejs v10 LTS
cache: npm
branches:
  only:
    - master # build master branch only
script:
  - hexo generate # generate static files
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GH_TOKEN
  keep-history: true
  on:
    branch: master
  local-dir: public
```
8. Travis CI 가 배포를 마무리 한다면, gh-pages branch에 만들어진 page 가 보입니다.
9. 만들어준 repo 의 setting 으로 가게 된다면 이번 포스팅의 앞부분에서 보인 이미지 처럼 source 를 gh_pages branch 로 변경해야 합니다.
10. 마지막으로 local 에 있는 _config.yml 파일에서 root: 값을 만들어둔 레포의 이름으로 만듭니다. 저의 경우 아래와 같습니다.
```yml
url: https://uniqueimaginate.github.io/my_blog
root: /my_blog
```
11. 이제 local 에 있는 모든 파일을 github로 푸시한 뒤에 약간의 시간이 흐른 후 <사용자id>.github.io/{repo name} 으로 접속해봅시다.
ex) [uniqueimaginate.github.io/my_blog](https://uniqueimaginate.github.io/my_blog)

