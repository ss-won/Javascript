# 알쓸신자 Part

## 스코프(Scope)와 호이스팅(Hoisting)
<br/>

### 1. 스코프(Scope) : 유효범위
(1) 스코프의 정의
- 스코프는 영역, 범위라는 뜻으로 `변수`와 `파라미터`의 __접근성__ 과 __생존기간__ 을 뜻한다.
- 크게 전역 유효범위(Global Scope), 지역 유효범위(Local Scope)로 나누어진다.
> 전역 유효범위는 스크립트 전체에서 참조할 수 있고, 지역 유효범위에서는 함수 내부와 하위 함수에서만 참조할 수 있다.
<br/>

(2) __Javascript__ 에서의 `Scope`
- 전역 스코프(Global Scope), 함수 레벨 스코프(Function-level Scope), 블록 레벨 스코프(Block-level Scope)로 나누어진다.

>   함수와 블록 스코프를 일반적인 지역 스코프라고 보면 된다.

- 자바스크립트에는 시작점이 따로 정해져 있지 않아서, 함수 밖에서 선언하면 전역 객체(웹상에서 window)의 프로퍼티가 된다.
- 전역 변수의 사용은 변수 이름이 중복될 수 있고, 의도치 않은 재할당에 의한 상태 변화로 코드를 예측하기 어렵게 만드므로 사용을 억제하여야 한다.

```javascript
    var a = 10;
    function globalScope() {
       console.log(a);// 10
    }
    function functionScope() {
        var a = 11;
        console.log(a);// 11
        function inner(){
            console.log(a);
        }
        inner();//11
    }
    function blockScope(){
        const a = 12;
        console.log(a);// 12
        if(a > 10){ 
            let b = a+1;
            console.log(b);// 13
        }
        console.log(b);// Uncaught ReferenceError: b is not defined
    }
    console.log(a);// 10
```

- Javascript는 기본적으로 `함수 레벨 스코프`를 따르고 있다.
>   기존 언어들은 블록 단위 스코프를 따른다. 
>   단, ES6부터 적용된 문법인 let, const는 블록 단위 스코프를 따른다.

- `변수명 중복선언`을 허용한다.(단, var 한정이다.)
> 기존 언어에서는 중복되는 변수를 사용할 수 없는 것에 비해 독특한 특징이라 볼 수 있다.

- `var 키워드의 생략`할 수 있다. => __키워드가 설정되지 않은 변수__ 는 모두 `var`로 취급한다.
```javascript 
    a = 3;
    console.log(a);//3
```

- `렉시컬 스코프`를 따른다.
    - 함수 실행 시 유효범위를 함수 실행 환경이 아닌 함수 정의 환경으로 참조하는 특성이다.
> __EXAMPLE__ 01
```javascript
    function f1(){  
        var a= 10;
        f2();
    }
    function f2(){  
        return a;
    }
    f1();//Uncaught Reference Error : a is not defined
```

- f2()가 f1()내부에서 실행되지만, 렉시컬 특성에 의해 f1()의 실행환경을 따르지 않고 f2()가 정의된 환경을 보기 때문에 a가 선언되지 않아 참조 에러가 발생한다.

> __EXAMPLE__ 02
```javascript
    var x = 'global';
    function outer() {
        var x = 'local';
        inner();
    }
    function inner() {
        console.log(x);
    }
    foo();//global
    inner();//global
```
- 위의 코드에서는 outer()의 내부 변수 x가 있지만, 렉시컬 특서에 의해 호출 스택과 관계없이 각각(this 제외)의대응표를 정의된 환경의 소스코드 기준으로 정의하고 런타임에 그 대응표를 변경시키지 않는다.

- 변수 x의 값을 출력하는 실행문에서, 변수 x를 찾을때까지 상위 환경을 반복 탐색한다. 
> inner의내부에는 x값이 undefined이므로 `-> 상위환경에서 선언된 x의 값을 참조하여 출력한다.`   

- `var`는 __function scope__ 이고 `let, const`는 __block scope__ 이다.
<hr>

### 2. 호이스팅(Hoisting)
- `hoist = 끌어올린다`라는 의미로 변수가 선언되었을때(var) 선언이 함수(또는 각 scope)의 최상위, 함수 밖에서는 전역 컨텍스트의 최상으로 변경된다.
- 선언문이 항상 자바스크립트 엔진 구동 시 가장 최우선적으로 해석되어 호이스팅 현상이 발생한다.
- 할당문은 런타임 과정에서 이루어지기 때문에 호이스팅 되지 않는다. 
    - 따라서 `함수선언`, `변수 선언` 등을 끌어올리지만 __변수 값을 끌어올리지 않는다.__

> ** `런타임(runtime)`이란, 프로그램이 실행되고 있을때 존재하고 있는 곳으로 자바스크립트에서는 web browser, Nodejs 등에서 실행되는 측면 등을 말한다. 

- const, let은 호이스팅이 되지 않는다.
>   `babel`과 같은 `트랜스파일러`에 의해 let, const가 var로 바뀌는 환경에서는 호이스팅이 발생할 수 있음에 주의하고 코딩해야한다. 
- 코드를 이해하기 어렵고, 유지보수가 어렵기 때문에 피하는 것이 좋다.
> 따라서, 이를 해결하기 위해

    - 함수를 선언 후 함수 내용을 실행한다.
    - eslint같은 도구에서 검열을 해서 수정한다.
</br>

>   이전장 [알쓸신자: spread and rest](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj8.md)<br/>
>   다음장 [Asynchronous Processing: 동기(Synchronous)와 비동기(Asynchronous)](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap1.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [Javscript : Scope의 이해](http://www.nextree.co.kr/p7363/)
- [스코프(scope)](https://poiemaweb.com/js-scope)