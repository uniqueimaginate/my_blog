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
   ```javascript
   const fs = require('fs')
   fs.writeFileSync('notes.txt', 'My name is peter')
   ```
   File System 이기 때문에 
   ```javascript
   const fs = require('fs')
   ```
   를 선언해 주어야 합니다.    

1. .appendFileSync('path', 'data')
   path : 덧붙혀 쓰기를 원하는 경로, data : 덧붙히려고 하는 데이터.
   ex)
   ```javascript
   const fs = require('fs')
   fs.appendFileSync('notes.txt', '\nI am 20 years old')
   ```
   
2. Node Module Scope!
   <code>node app.js</code> 와 같은 명령어는 app.js 만을 실행합니다.<br>
   다른 파일(util.js)을 함께 실행하기 위해서는 다음의 코드와 같습니다.
   
   ```javascript
   // util.js 코드. 
   console.log('I am utils.js')
   ```
   ```javascript
   // app.js 코드.
   require(./utils.js) 
   console.log('I am app.js')
   ```
   <pre>>> node app.js <br> I am utils.js<br> I am app.js</pre>    
   
   그렇다면 다음의 결과는 어떠할까?    
   
   ```javascript
   // util.js 코드. 
   const name = 'Peter'
   ```
   ```javascript
   // app.js 코드.
   require(./utils.js)
   console.log(name)
   ```
   
   <pre>>> node app.js<br> ERROR</pre>
   
   이 결과는 각각의 .js 파일은 각각의 변수와 스코프를 지니기 때문이다.
      
   그러나 util.js 의 변수를 app.js 에서도 사용할 수 있게 할 수 있는 방법이 있습니다.
   
   ```javascript
   // util.js 코드. 
   const name = 'Peter' 
   module.exports = name
   ```

   ```javascript
   // app.js 코드.
   const name = require(./utils.js)
   console.log(name)
   ```
   
   <pre> >> node app.js<br> Peter</pre>
   
    app.js 에서 <code>const name</code> 변수의 이름은 util.js 와 독립적이기 때문에 어떻게든 지어도 상관이 없습니다.    
   
 <b>여기서 변수만 export 할 수 있는 것이 아니라 함수도 export 할 수 있습니다!</b>
   ```javascript
   // util.js 코드. 
   const anyFunction = function(){
      return 'any Function!'
   }
   module.exports = anyFunction
   ```
   ```javascript
   // app.js 코드.
   const _function = require(./utils.js)
   console.log(_function)
   ```
   
 <pre> >> node app.js<br> any Function!</pre>
   
   
3. NPM 이용하기    
   <code>npm init</code>    
    npm package 를 이용할 수 있게 해줍니다.    
    pacakge.json 이 생성되며 프로젝트에 대한 설명을 자신이 customize 할 수 있습니다.

4. npm install \<package name>    
   ex)
   <code>npm install validator</code>    
   코드에서 사용하는 방법은 
   <code>require('validator')</code>를 코드에 추가하면 됩니다.    
   사용법은 validator 문서를 참조하면 됩니다.

   ex)
   ```javascript
   // app.js 코드
   require('validator')
   console.log(validator.isEmail('foo@bar.com'))
   ```
   <pre> >> node app.js
    true</pre>    
5. node_module 폴더가 없을 때는, <code>npm install</code> 명령어를 이용하면 다시 npm 모듈이 설치 됩니다.
6. <code>npm install \<package> -g</code>    
   -g 표기는 global 하게 설치하는 것입니다. 즉 이 프로젝트에만 적용되는 것이 아니라 OS에 설치하게 됩니다.    
   ex)    
   <code>npm install nodemon -g</code>    
   위의 명령어로 nodemon package 를 OS 에 설치했습니다. MacOS, Linux 의 경우 Sudo 명령어를 이용해야 합니다.     
   nodemon package 는 일일히 terminal 에 <code>node app.js</code> 를 칠 필요가 없습니다. <code>nodemon app.js</code> 를 터미널에 치게 된다면 app.js 파일에 변동이 생길 때 마다 자동으로 변경 사항을 적용해서 터미널에 결과를 보이게 합니다. 굉장히 편하게 만들어주는 모듈입니다.
