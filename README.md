# CoffeeScript 정리

## 서문
* 2009년 크리스마스 제레미 애쉬키나스가 릴리즈를 함.
* 2010년 크리스마스에 1.0 릴리즈.
* javascript의 장점을 그대로 가지고 왔고 손쉽게 사용할 수 있는 문법을 채용.
* coffeescript 컴파일러는 javascript Lim을 준수하는 결과물을 만들려고 최선을 다한다.
* coffeescript 컴파일러는 오류코드에 대하여 리포트를 해준다.
* coffeescript는 간결하다.

## 설치
* node를 설치.
* npm 설치
* ``` npm install -g coffee-script ``` 명령어를 실행하여 최신버전의 coffeescript 를 설치한다.
* ``` coffee -v ``` 를 이용하여 설치된 버전을 확인.
* ``` export NODE_PATH=/usr/local/lib/node_modules ``` 을 이용하여 NODE_PATH를 설정힌디.
* console 에서 node명령어를 실행하여 node REPL에서 ``` require('coffee-script') ``` 를 실행하여 확인한다.
* Error : Cannot find module 'coffee-script'가 발생하면 NODE_PATH가 제대로 설정되어 있지 않아서이다.

## coffeescript 기본

### coffeescript 명령어
* ``` coffee hello.coffee ``` 명령어를 이용하여 실행.
* coffee -h
```
    -b, --bare         compile without a top-level function wrapper (컴파일된 javascript를 함수로 감싸지 않는다.)
	-c, --compile      compile to JavaScript and save as .js files
	-e, --eval         pass a string from the command line as input
	-h, --help         display this help message
	-i, --interactive  run an interactive CoffeeScript REPL
	-j, --join         concatenate the source CoffeeScript before compiling (컴파일전에 스크힙트들을 합친다.)
	-m, --map          generate source map and save as .js.map files
	-n, --nodes        print out the parse tree that the parser produces
      --nodejs       pass options directly to the "node" binary
      --no-header    suppress the "Generated by" header
	-o, --output       set the output directory for compiled JavaScript
	-p, --print        print out the compiled JavaScript
	-s, --stdio        listen for and compile scripts over stdio (표준 입출력을 통해 스크립트들을 컴파일한다.)
	-l, --literate     treat stdio as literate style coffee-script
	-t, --tokens       print out the tokens that the lexer/rewriter produce
	-v, --version      display the version number
	-w, --watch        watch scripts for changes and rerun commands (변경사항을 나타내고 재컴파일한다.)
```

## 함수

### 함수의 정의
* coffeescript는 함수의 마지막 표현을 자동으로 반환하게 되어 있다.
* 명시적으로 return을 사용할 수 있지만 옵션
* 프로그램의 흐름을 크게 벗어나지 않는다면 return 키워드 없이 사용하는 것이 일반적이다.
* 아무것도 반활할 값이 없으면 return 만 사용.
* 함수 인자가 없을 때를 제외하고는 보통 함수 호출 시에 괄호를 생략한다.
* coffeescript의 삽입문법을 사용하는 방법
	* "" 안에 삽입문법을 작성
	* "#{subject}"
* + 연산자는 공백을 분명히 구분한다.
* 함수정의 시 함수로 전달되는 인자에 대한 특별한 정의 또는 선언 없이도 arguments객체를 사용해서 함수로 전달되는 모든 인자들에 접근할 수 있다.

### 조건과 예외
* is
	* javascript === 연산자와 같음.
* 함수와 조건문의 분기를 구분하기 위해 중괄호 대신 들여쓰기를 사용한다.
* coffeescript의 중괄호는 JSON 객체선언에만 사용된다.

### 범위: 참조시 고려사항
* 변수의 범위
	* 변수는 참조할 수 있는 영역이 있다.
	* 모든 함수는 범위를 만들고, 범위를 생성하는 유일한 방법은 함수 정의를 통해서다.
	* 변수는 함수가 정의된(할당이 이루어짐)그 범위 내에서만 존재한다.
	* 범위 밖에서는 변수를 참조할 수 없다.
* coffeescript 범위 접근 방식 : 어휘 범위 방식
	* 프로그램 작성시 선언 된 변수의 위치에 따라 그 변수가 사용될 수 있는 범위가 결정됨.
	* 타이핑의 수고를 덜어준다.
	* 동일한 변수명이 중첩된 하위 범위에 존재하였을 때 상위 변수가 하위 범위에서 가려지는 문제를 방지한다.
* 함수도 단지 변수다
* 함수가 만들어 낸 범위 안에서 또 다른 중첩된 함수 범위가 존재할 수 있다.
* coffeescript는 변수 할당을 통해서만 변수 생성이 가능.

### 컨텍스트 ( 또는 this는 무엇일까?)
* this는 이 컨텍스트라고 생각해야한다.
* 컨텍스트(this 또는 @로 표현)는 함수가 호출될 때마다 다른 어떤 것이 될 수 있다.
* 컨텍스트의 주목적은 객체에 메소드(객체 속성으로 함수가 지정됨)를 만드는것.
* 생성된 메소드는 객체 참조 방식으로 호출될 수 있다.
* call또는 apply메소드를 사용하여 특정 컨텍스트에 함수를 지정하고 호출할 수 있다.
	* call 또는 apply 메소드 호출시 해당 인자로 컨텍스트와 배열 리스트(혹은 개별요소)를 넘겨줌
* new 키워드를 사용하여 컨텍스트에 함수를 지정할 수 있다.
* new 키워드는 해당 함수를 생성자로 사용해서 객체를 만든다.
* new 키워드를 사용한다는 것은 "함수 결과를 반환하지 말고 새로운 객체를 생성하여 그 객체 컨텍스트에서 함수를 실행한 뒤 해당 객체를 반환한다"는 것.
* 만약 함수가 객체의 메소드로 사용되지 않고, new 키워드 또는 call/apply에서도 사용되지 않으면 해당 함수의 컨텍스트는 전역 객체로 지정된다.

#### 바운드(Bound)함수: this는 this를 의미한다.
* 함수가 어떻게 호출되든지 간에 현재 컨텍스트에서 해당 함수가 실행되길 원할 때.
* 이벤트 콜백함수
* =>
	* 현재 컨텍스트에 함수를 바인딩
	* 바운드 함수 연산자

### 속성 인자 (@arg)
* 함수 정의시 인자명 앞에 @을 붙이면 자동으로 컨텍스트 객체(this)에 해당 인자명을 가진 속성을 만들고, 해당 속성에 그 인자값을 설정한다.
* setName = (@name) ->
* 클레스의 생성자를 만들때 매우 유용하게 사용

### 기본인자(arg =)
* 샘플예제로 대체








