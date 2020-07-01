# 알쓸신자 Part

## 전개(spread) and 나머지(rest)
<br/>

전개구문(spread syntax)은 어떤 배열이나 객체의 엘리먼트들을 __확장__ 하고 나머지 구문은 엘리컨트들을 수집하여 __압축__ 한다.

1. 전개구문(spread syntax)
    - 배열과 같이 반복이 가능한(iterable) 문자를 0개 이상의 인수(함수) 또는 요소(배열)로 확장하여 0개 이상의 key-value의 쌍인 객체로 __확장__ 시킬 수 있다.

>   __CASE__ 01: 함수 호출
- apply 메소드의 대체로 사용가능하다. (* apply는 일반적으로 배열의 elements를 함수의 인수로 사용하려 할때 사용)
```javascript
    function example(x,y,z){
        return x + y + z;
    }
    let args = [1, 2, 3, 4];
    example.apply(null, args);//10
    example(...args);//10
```
- new 연산자와 함께 사용할 수 있다.
```javascript
    const args = [1, 1, 2, 3, 4, 9, 5, 3, 4];
    let duplication = new Set[...args];//[1, 2, 3, 4, 9, 5]
```

>   __CASE__ 02: 배열리터럴과 문자열
- 어떤 배열을 일부로 가지는 배열을 리터럴 선언할 수 있다.
    - `splice(), push(), concat() 등의 메소드를 대신할 수 있다.` 
    ```javascript
        const parts = ['shoulders', 'knees'];
        const lyrics = ['head', ...parts, 'and', 'toes'];
        // [ head, shoulders, knees, and, toes ] 
    ``` 
- 배열 복사가 가능하다.
    - `shallow copy`로 동작한다. 
    - 다차원 배열에서는 내부 객체가 원 배열을 참조하기 때문에 사용에 부적합하다.
    ```javascript
       let arr1 = [1, 2, 3];
       let arr2 = [[1], [2], [3]];//다차원배열
       let arr3 = [...arr1];
       arr3.push(4);
       console.log(arr1, arr3)//[1, 2, 3] [1, 2, 3, 4];

       arr3 = [...arr2];
       arr3.shift().shift();
       console.log(arr2, arr3)//[[], [2], [3]] [[2], [3]];
    ```
- 배열 연결을 더 쉽게 할 수 있다.
    - `concat()` 대체
     ```javascript
        let arr1 = [0, 1, 2];
        let arr2 = [3, 4, 5];
        /* arr1.concat(arr2)와 같다. */
        arr1 = [...arr1, ...arr2];//[0, 1, 2, 3, 4, 5]
    ```
    - `shift()`를 대신해 배열 시작지점에 배열의 값을 삽입한다.
    ```javascript
        let arr1 = [0, 1, 2];
        let arr2 = [3, 4, 5];
        /* arr1.unshift.apply(arr1,arr2)와 같다. */
        arr1 = [...arr2, ...arr1];//[3, 4, 5, 0, 1, 2]
    ```

>   __CASE__ 03: 객체리터럴(ES8)
- 객체 속성 전개를 할 수 있다.
- 얕은 복사 또는 객체의 병합을 할때 Object.assign보다 더 짧은 문법을 이용해 만들 수 있다.
```javascript
    const obj1 = { foo: 'bar', x: 42 };
    const obj2 = { foo: 'bax', x: 13 };
    const cloneObj = { ...obj1 };
    //Object{ foo: 'bar', x: 42 }
    const mergeObj = { ...obj1, ...obj2 }
    //Object{ foo: 'baz', x: 42, y: 13} -> 공통분모인 foo의 경우 마지막 객체의 속성을 따른다.
```
- Obejct.assign 메소드는 setters를 트리거하지만 전개구문은 그렇지 않다.(엄연히 둘은 다르다!) 
    - 같이 읽어보면 좋을 것 같은 게시물<br>
    (1) [Javascript - 접근자 프로퍼티(setter, getter)](https://velog.io/@bigbrothershin/JavaScript-%EC%A0%91%EA%B7%BC%EC%9E%90-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0-getter-setter)<br>
    2. [객체를 쉽게 병합하는 assign 메서드](https://velog.io/@bathingape/%EA%B0%9D%EC%B2%B4%EB%A5%BC-%EC%89%BD%EA%B2%8C-%EB%B3%91%ED%95%A9%ED%95%98%EB%8A%94-%EB%A9%94%EC%84%9C%EB%93%9C-Object.assign)

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
>   파라미터(parameter) = 함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 있게 해주는 변수
>   인수(argument) = 함수가 호출될 때 함수로 값을 전달해주는 변수
- rest 파라미터와 인수(arguments)객체의 차이
        - rest 파라미터는 함수 표현에 정식으로 정의된 이름이 주어지지 않은 `유일한 대상`인 반면, 인수 객체는 함수로 전달된 모든 인수를 포함한다.
        - 인수 객체는 실제 배열이 아니지만, rest 파라미터는 Array 객체의 인스턴스값으로 Array의 내장 함수를 이용할 수 있다.
        - 인수 객체에는 독립된 하나의 객체로, 특정 추가 기능(함수)을 가지고 있다.
- arguments에 의해 유발된 상용구(boilerplate) 코드를 줄이기 위해 도입되었다.
    
</br>

>   이전장 [알쓸신자: 비구조화 할당](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj7.md)<br/>
>   다음장 [알쓸신자: 스코프(scope)와 호이스팅(Hoisting)](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj9.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - Spread Syntax](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [MDN Web Docs - Rest 파라미터](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)