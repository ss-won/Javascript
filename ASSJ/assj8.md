# 알쓸신자 Part

## 전개구문(spread syntax) and 나머지(rest)
<br/>

전개구문은 어떤 배열이나 객체의 엘리먼트들을 __확장__ 하고 나머지 구문은 엘리컨트들을 수집하여 __압축__ 한다.

1. 전개구문(spread syntax)
    - 배열과 같이 반복이 가능한(iterable) 문자를 0개 이상의 인수(함수) 또는 요소(배열)로 확장하여 0개 이상의 key-value의 쌍인 객체로 __확장__ 시킬 수 있다.

>   __CASE__ 01: 함수 호출
    - apply 메소드의 대체로 사용가능하다. (* apply는 일반적으로 배열의 elements를 함수의 인수로 사용하려 할때 사용)
    - new 연산자와 함께 사용할 수 있다.

>   __CASE__ 02: 배열리터럴과 문자열
    - 더 강력한 배열 리터럴로 사용할 수 있다.
    - 배열 복사가 가능하다
    - 배열 연결을 더 쉽게 할 수 있다.

>   __CASE__ 03: 객체리터럴(ES8)
    - 객체 속성 전개를 할 수 있다.
    - 얕은 복사 또는 객체의 병합을 할때 Object.assign보다 더 짧은 문법을 이용해 만들 수 있다.
    - Obejct.assign 메소드는 setters를 트리거하지만 전개구문은 그렇지 않다.(엄연히 둘은 다르다!) 

2. 나머지구문(rest)
    - 정해지지 않은 수(an indefinite number, 부정수) 인수들을 수집 후 __압축__ 하여 배열로 나타낼 수 있게 한다.
    - 함수의 파라미터 또는 비구조화 할당에 이용한다.
    ```javascript
        function sum(...theArgs) {
            return theArgs.reduce((acc, cur) => acc + cur, 0);
        }
        console.log(sum(1, 2, 3));//6
        console.log(sum(1, 2, 3, 4));//10
    ```
>   __CASE__ : 파라미터와 인수
    - 파라미터(parameter)와 인수(argument)의 차이?
    - rest 파라미터와 인수(arguments)객체의 차이는 ?
    - arguments에서 배열까지
    
</br>

>   이전장 [알쓸신자: 비구조화 할당](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj7.md)<br/>
>   다음장 [알쓸신자: 스코프(scope)와 호이스팅(Hoisting)](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj9.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - Spread Syntax](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [MDN Web Docs - Rest 파라미터](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)