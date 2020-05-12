---
title: 'Node.js #1'
date: 2020-05-12 21:50:08
tags: Node.js, Node.js Core Modules
---

# Node.js Core Modules (Notes App # 1)

## Node.js 핵심 모듈에 대한 글입니다.

#### Udemy 의 수업 The Complete Node.js Developer Course(3rd Edition) - Andrew Mead 을 공부하면서.

<!-- more -->
배운 것 들을 순서 대로 정리할 뿐입니다.    
[Node.js 공식 문서](https://nodejs.org/en/docs/)를 보면서 참고하시면 좋을 것 같습니다.

1. .writeFileSync('file','data')    
   file : 파일명, data : 쓰려고 하는 데이터.    
   ex)
   <pre><code>const fs = require('fs')<br>fs.writeFileSync('notes.txt', 'My name is peter')</code></pre>
    File System 이기 때문에 <code>const fs = require('fs')</code> 를 선언해 주어야 합니다.    

2. .appendFileSync('path', 'data')
   path : 덧붙혀 쓰기를 원하는 경로, data : 덧붙히려고 하는 데이터.
   ex)
<pre><code>const fs = require('fs')<br>fs.appendFileSync('notes.txt', '\nI am 20 years old')</code></pre>
   
3. Node Module Scope!
   <code>node app.js</code> 와 같은 명령어는 app.js 만을 실행합니다.<br>
   다른 파일(util.js)을 함께 실행하기 위해서는 다음의 코드와 같습니다.
   
   <pre><code>// util.js 코드. <br>console.log('I am utils.js')</code></pre>
   <pre><code>// app.js 코드.<br>require(./utils.js) <br>console.log('I am app.js')</code></pre>
    <pre>>> node app.js <br>I am utils.js<br>I am app.js</pre>    
   
    그렇다면 다음의 결과는 어떠할까?    
   
    <pre><code>// util.js 코드. <br>const name = 'Peter'</code></pre>
 <pre><code>// app.js 코드.<br>require(./utils.js) <br>console.log(name)</code></pre>
   
 <pre>>> node app.js<br>ERROR</pre>
   
 이 결과는 각각의 .js 파일은 각각의 변수와 스코프를 지니기 때문이다.
   
 그러나 util.js 의 변수를 app.js 에서도 사용할 수 있게 할 수 있는 방법이 있습니다.
   
    <pre><code>// util.js 코드. <br>const name = 'Peter' <br>module.exports = name</code></pre>
 <pre><code>// app.js 코드.<br>const name = require(./utils.js) <br>console.log(name)</code></pre>
   
 <pre>>> node app.js<br>Peter</pre>
   
    app.js 에서 <code>const name</code> 변수의 이름은 util.js 와 독립적이기 때문에 어떻게든 지어도 상관이 없습니다.    
   
 <b>여기서 변수만 export 할 수 있는 것이 아니라 함수도 export 할 수 있습니다!</b>
   
    <pre><code>// util.js 코드. <br>const anyFunction = function(){
        return 'any Function!'
    }
    module.exports = anyFunction</code></pre>
 <pre><code>// app.js 코드.<br>const _function = require(./utils.js) <br>console.log(_function)</code></pre>
   
 <pre>>> node app.js<br>any Function!</pre>
   
4. npm init
    npm package 를 이용할 수 있게 해줍니다.    
    pacakge.json 이 생성되며 프로젝트에 대한 설명을 자신이 customize 할 수 있습니다.

5. npm install \<package name>    
   ex)
   <code>npm install validator</code>    
   코드에서 사용하는 방법은 
   <code>require('validator')</code>를 코드에 추가하면 됩니다.    
   사용법은 validator 문서를 참조하면 됩니다.

   ex)
   <pre><code>// app.js 코드
   require('validator')
   console.log(validator.isEmail('foo@bar.com'))</code></pre>
   <pre>>> node app.js
   true</pre>