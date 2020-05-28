# Basic Part

<br/>

## 주요특징
<br/>

### What is Javascript?
- Web 브라우저에서 사용하기 위해 만들어진 언어 중 하나.
- Web상의 UI 동적 변환에 쓰인다.

### 만능언어 Javascript
- ☝🏻`Web`의 UI 동적 변환
- ☝🏻`Node.js`로 JS컴파일, 런타임영역을(서버) 동작 및 실행
- ☝🏻`ELECTRON`으로 데스크탑 Application 제작
- ☝🏻`React-Native`, `Nativescript`으로 모바일 네이티브앱 제작
    - 단순한 웹앱의 웹뷰(Webview)를 보여주는 것이 아닌, 네이티브 UI를 Javscript로 구현 가능

### IDE
- 브라우저 개발자 콘솔, Codesendbox, VSCODE+Nodejs, etc...

## 기본문법
<bt/>

### Variable vs Constant
- Variable(변수) = 변화하는 값
    - var, let 키워드
    - var은 구형브라우저에서 쓰일때만 사용 권장
- Constant(상수) = 할당된 후 변화가 없는 값
    - const 키워드
- [var vs let vs const]()

### 원시타입(Type)
- `string`(문자열)
```
let str = 'string';
let str2 = "string";
let str3 = `This is
            string`;
```
- `number`(숫자)
    - 특수숫자로는 `NaN`(Not a Number), `Infinity`(무한대), `NegZero`(-0)가 있다.
- `null`, `undefined` : 없음을 의미하지만 역할이 다르다.
    - `null`은 Empty의 개념(falsy한 값이지만, type은 object의 일종이다.)
    - `undefined`는 '할당되지 않은'의 개념
- `boolean` : true 또는 false만을 가지는 값의 타입이다.
- `symbol` : ES6부터 등장한 타입으로, 보통 객체의 key값으로 쓰인다.
- `object`(객체) : 특정 속성(key)값과 메서드들을(내부함수key값) 가진다.

### 네이티브(Native)
- 작성예정

### 연산자
- 연산할 때 사용하는 문자
- __산술연산자__
    - number형 값 사칙연산에 쓰이는 연산자
    - `+`(덧셈), `-`(뺄셈), `*`(곱셈), `/`(나눗셈), `%`(나머지연산)
    - `++`, `--`는 +1, -1을 의미하고 전위, 후위 표기에 따라 뜻이 다름
        - `++a` : 기존 a에 1을 미리 더하고 더해진 값을 보여준다.
        - `a++` : 기존 a를 먼저 보여주고, 1을 더한다.
    - 우선순위 : `*,/,%` -> `+,-,++,--``
    - `+`연산자의 경우 string형에 이용하면 이어붙이는 작업을 한다. => 이미 오버로딩 되어있음
- __논리연산자__
    - `!`(Not) : true->false, false->true 반환
    - `&&`(And) : 모든 값이(All, Every) True일때만 True를 반환
    - `||`(Or) : 특정 값이(Any, Some) True면 True 반환
    - 우선순위 : `!` -> `&&` -> `||`
- __비교연산자__
    - `==`, `===` Equal
        - `==`은 스칼라값만 비교 `===`은 스칼라값과 타입형 모두 비교
        - Javascript의 선언형태는 any가 기본이므로 개발시 `===`를 사용하는 것이 좋다.
    - `!=`, `!==` Not Equal
    - `>`,`<`,`>=`,`<=` 부등호(크기비교)

### 조건문
- 어떤 조건에 따라 결과를 다르게 하는 경우를 위해 쓰이는 문장
- ☝🏻`if`, `else`, `else if`
    - if(condition) { sentences } condition이 true면 실행된다.
    - else if는 if이외에 다른 조건을 넣을 때, else는 모든 조건을 만족하지 않은 나머지의 경우 실행된다.
- ✌🏻`switch case`
    - switch(case) case x: { sentences break;} ... 형태로 case 값마다 다른 행위를 구현할 수 있다.
    - `default:`를 통해 어떠한 case에도 속하지 않을때 기본형으로 실행될 sentence를 설정할 수 있다.
    - case문이 끝날때마다 break를 통해 끝났음을 명시해 주어야 한다.

### Function(함수)
- 특정 로직을 재사용하기 위해 구현한 코드의 한 형태로 type은 object이다.
```javascript
function funName(params) { context }
```
- return이 명시된 순간 함수가 종료된다.
- `arrow funtion`(화살표함수)는 기존의 무명함수를 단축화해서 표기할 수 있다.
    - (params) => { context }, (param) => example `=> example이 return 된다.`
- 함수의 리턴값을 출력할때 변수명과 문장을 출력하는 방법
    - console.log("This is " + example);
    - console.log(``This is ${example}``);

### Object(객체)
- 특정 속성과 메서드를 정의한 형태로 key속성으로 value에 접근 및 실행 할 수 있다.
```javascript
const obj = { key1: val1, key2:val2, ... } 
console.log(obj.key1)//val1
```
- __객체의 비구조화 할당(destructuring assignment)__
    - 할당 및 기본형
     ```javascript
     const { name, alias, age, job="student" }= { name:"sswon", age:25, alias:"wish" }
     console.log(name, alias, age, job)//"sswon" "wish" 25 "student"
     ```
    - 나머지패턴
    ```javascript
    const { name, ...others }= { name:"sswon", age:25, alias:"wish" }
    console.log(name, others)//"sswon" { age:25, alias:"wish" } 
    ```
- 객체 내부 `this` -> 현재 속해있는 object를 가리킴
    - 단, `arrow function`의 경우 속해있는 object를 가리키지 못함
- getter, setter 함수
```javascript
const obj = {
    _name: "abc",
    get name(){
        return this._name;
    }
    set name(str){
        this._name = str;
    } 
} 
```
    - getter(접근), setter(할당) 함수는 여러개가 될 수 있다.
    - getter, setter 함수는 같을 수 있고 할당과 접근이 모두 실행된다.
    - 단, 속성명(key)과는 같을 수 없다.


## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- You Don't Know JS [part 1,2] - 카일 심슨(Kyle Simpson)
- [Javascript) 비구조화 할당 알아보기](https://velog.io/@public_danuel/destructuring-assignment)

