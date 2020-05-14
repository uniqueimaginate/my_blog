---
title: 'NodeJS#2'
date: 2020-05-13 22:30:38
tags: Node.js, Node.js File system, yargs
---
# Node.js File System (Notes App # 2)

## Node.js 파일 시스템과 커맨드라인 Argv 에 대한 글입니다.

<!-- more -->

1. argv 이용하기    
   직접 해보세요
   ```javascript
   console.log(process.argv)
   ```
   ```javascript
   console.log(process.argv[2])
   ```
   <pre> >> node app.js peter</pre>
   <pre>// 저의 결과 입니다.
   // 각자의 local 환경에 따라 다릅니다.
   <code>console.log(process.argv)</code> 의 경우에는 아래의 3개의 줄이 나오겠지만
   <code>console.log(process.argv[2])</code> 의 경우에는 직접 입력한 peter 만 나올 것입니다.    

    [
    '/usr/local/bin/node',
    '/Users/peter/Desktop/Study/NodeJS/Learn_NodeJS/notes-app/app.js',
    'peter'
    ]
   </pre>
2. yargs package 이용하기
   이 패키지는 args 를 더 편하게 이용 할 수 있게 하는 패키지 입니다.    
    아래의 코드 결과를 비교해봅시다.
   ```javascript
    console.log(process.argv)
    console.log(yargs.argv)
   ```
   <pre> >> node app.js
    [
    '/usr/local/bin/node',
    '/Users/peter/Desktop/Study/NodeJS/Learn_NodeJS/notes-app/app.js'
    ]
    { _: [], '$0': 'app.js' }
   </pre>
   <code>console.log(process.argv)</code> 와는 다르게
   <code>console.log(yargs.argv)</code> 는 불필요한 것들을 보이지 않습니다.

   추가적인 기능도 있습니다.
   ```javascript
    yargs.command({
        command: 'add',
        describe: 'Add a new note',
        handler: function(){
            console.log('Adding a new note')
        }
    })
   ```
   위의 코드를 app.js 에 적습니다.    
   그 다음 실행해 봅니다.  
   <pre> >> node app.js add
    Adding a new note
    { _: [ 'add' ], '$0': 'app.js' }
    </pre>
    이러한 결과를 보일 수 있습니다. 즉, handler 에 자신이 원하는 함수를 넣어서 특정 기능을 수행 할 수 있습니다.

    아래와 같은 기능도 있습니다.    

    ```javascript
    yargs.command({
        command: 'add',
        describe: 'Add a new note',
        builders: {
            title:{
                describe: 'Note title',
                demandOption: true,
                type: 'string'
            },
            body:{
                describe: 'Note body',
                demandOption: true,
                type: 'string'
            }
        },
        handler: function(argv){
            console.log('Title: ' + argv.title)
            console.log('Body: ' + argv.body)
        }
    })
    ```
    위의 코드를 실행해 봅니다.
    <pre> >> node app.js add --title="This title" --body="This Body"
     Title : This title
     Body : This Body
    </pre>
    위와 같이 yargs 를 사용해서 데이터를 저장할 수 있습니다.
    단지 위의 예시는 handler 에서 console 출력만을 진행한 예시입니다.

3. JSON 이용하기    
   JSON 을 공식문서를 통해 알아보자면 다음과 같습니다.    
   <b>JSON (JavaScript Object Notation) is a lightweight data-interchange format.</b>    
   굉장히 직관적이고 단순한 설명입니다.    
   바로 JSON 을 어떻게 사용하는지에 대해서 설명하겠습니다.    
   [자세한 설명은 공식 홈페이지에 있습니다.](https://www.json.org/json-en.html)

    ```javascript
    // 1-json.js 파일입니다.
    
    // 먼저 filesystem 사용을 선언합니다.
    const fs = require('fs')

    // 같은 폴더에 있는 1-json.json 파일을 읽어옵니다.
    const dataBuffer = fs.readFileSync('1-json.json')
    
    // buffer 로 읽어오기 때문에 hex 로 표기 됩니다.
    // 따라서 toString() 함수를 통해서 string 으로 변경합니다.
    const dataJSON = dataBuffer.toString()

    // JSON 을 parsing 하는 단계를 거칩니다.
    const user = JSON.parse(dataJSON)

    // JSON 을 parsing 한 후에는 이렇게 수정할 수 있습니다.
    user.name = "Cali"
    user.age = 50

    // 수정이 끝난 후, 다시 JSON 으로 만들어줍니다.
    userJSON = JSON.stringify(user)
    // 수정 된 문자들이 1-json.json 으로 저장됩니다.
    fs.writeFileSync('1-json.json', userJSON)
    ```

    ```json
    // 1-json.json 파일입니다.
    // 설명을 위해서 JSON 파일에 주석이 있다고 가정합니다.
    // JSON 파일에는 주석을 사용하지 않는 것이 좋습니다.
    {"name":"peter","planet":"Earth","age":27}
    ```

    <pre>
    // 결과 1-json.json    
    {"name":"Cali","planet":"Earth","age":50}
    </pre>