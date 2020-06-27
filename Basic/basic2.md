# Basic Part

## 값과 타입
<bt/>

### 변수와 상수의 선언
- Variable(변수) = 변화하는 값
    - var, let 키워드
    - var은 구형브라우저에서 쓰일때만 사용 권장
- Constant(상수) = 할당된 후 변화가 없는 값
    - const 키워드
- [var vs let vs const]()

### 원시타입(Type)
- `string`(문자열)
    - [문자열내장함수](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj2.md)
```javascript
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
    - [Truthy and Falsy?](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj4.md)
- `boolean` : true 또는 false만을 가지는 값의 타입이다.
- `symbol` : ES6부터 등장한 타입으로, 보통 객체의 key값으로 쓰인다.
- `object`(객체) : 특정 속성(key)값과 메서드들을(내부함수key값) 가진다.

### Function(함수)
- 특정 로직을 재사용하기 위해 구현한 코드의 한 형태로 object이다.
```javascript
    function funName( params ) { context }
    const arrowFunction = ( params ) => { context }
    const default_params = ( params = defaultValue ) { context }
```
- return이 명시된 순간 함수가 종료된다.
- `arrow funtion`(화살표함수)는 기존의 무명함수를 단축화해서 표기할 수 있다.
    - ( param ) => param `=> return param과 같다.`
- 함수의 리턴값을 출력할때 변수명과 문장을 출력하는 방법
    - console.log("This is " + example);
    - console.log(``This is ${example}``);
- 함수의 기본값은 파라미터에 `=`표기를 통해 지정한다.

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
    - 나머지 패턴
    ```javascript
        const { name, ...others }= { name: "sswon", age: 25, alias: "wish" }
        console.log( name, others )//"sswon" { age:25, alias:"wish" } 
    ```
    - 더 자세한 비구조화 할당 👉🏻 [알쓸신자: 비구조화 할당](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj7.md)
- 객체 내부 `this` -> 현재 속해있는 object를 가리킴
    - 단, `arrow function`의 경우 속해있는 object를 가리키지 못함
    - [this 키워드 정복하기]()
- getter, setter 함수
    - getter(접근), setter(할당) 함수는 여러개가 될 수 있다.
    - getter, setter 함수는 같을 수 있고 할당과 접근이 모두 실행된다.
    - 단, 속성명(key)과는 같을 수 없다.
```javascript
    const obj = {
        _name: "abc",
        get name() {
            return this._name;
        }
        set name(str) {
            this._name = str;
        } 
    } 
```

### Array(배열)
- 여러 항목이 들어있는 리스트로 객체(object)의 일종이다.
- 배열의 선언은 `[]` 대괄호를 이용하며, 내부에는 여러가지 값이 올 수 있다.
```javascript
    //리터럴 선언(권장)
    let arr = [1,2,3,4,'5',[]];
    //네이티브 생성자 선언
    let arr2 = new Array(5);//빈 슬롯이 5개인 배열 생성
    let arr3 = new Array(1,2,3,4);//[1,2,3,4]
```
- 값의 조회는 index를 통하고, 기존언어들과 마찬가지도 할당도 가능하다.
- index값은 0부터 시작해 arr의 크기보다 1작은 수만큼을 가진다.
- 배열의 크기값은 배열 prototype 속성의 length를 이용한다.
```javascript
    let arr = [1,2,3,4,'5',[]];
    console.log(arr[3])//4
    arr[4] = 5;//1,2,3,4,5
    arr.push({name: wish});//[1,2,3,4,5,[],{name: wish}]
    arr.length;//7
```
- [배열 vs 문자열](https://blog.naver.com/PostView.nhn?blogId=j_wish_&logNo=221888000033&parentCategoryNo=&categoryNo=13&viewDate=&isShowPopularPosts=false&from=postList)
- [배열내장함수](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj1.md)
<br/>

>   이전장 [Basic: 주요특징](https://github.com/ss-won/Javascript/blob/master/Basic/basic.md)<br/>
>   다음장 [Basic: 기본문법](https://github.com/ss-won/Javascript/blob/master/Basic/basic3.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- You Don't Know JS [part 1,2] - 카일 심슨(Kyle Simpson)
- [Javascript) 비구조화 할당 알아보기](https://velog.io/@public_danuel/destructuring-assignment)