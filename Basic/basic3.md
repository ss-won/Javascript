# Basic Part

## 기본문법
<bt/>

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

### 반복문
- 특정 작업을 반복적으로 할때 사용하는 구문
<img src="https://www.google.com/url?sa=i&url=http%3A%2F%2Fkocw.xcache.kinxcdn.com%2FKOCW%2Fdocument%2F2016%2Fkpu%2Fparkjeongmin0520%2F7.pdf&psig=AOvVaw3gEtRVvjqfy_4_l0aBlhTF&ust=1590848603543000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCNj1iISj2ekCFQAAAAAdAAAAABAd" width="100" height="100" alt="반복문구조"></img>
- 반복문의 종류는 크게 `for`문과 `while`문이 있고, 이외에는 객체의 prototype 내장 반복함수들이 있다.
    - `for문` : 보통 반복할 횟수가 정해져 있을때 쓴다.
        - 제한 조건이 false가 될때까지 반복자를 바꾸어 반복한다.
        - for of, for in문은 각각 객체의 key, value 반복시에 많이 사용한다.
    ```javascript
    for(let i=0;i<=10;i++){ context };
    for(let v of arr){ context };
    for(let key in obj){ context };
    ```
    - `while문(+do while)` : 정해진 횟수를 잘 모를때 많이 쓴다.(do while은 일단 먼저 실행 후 반복)
        - condition이 false일때까지 반복한다.
    ```javascript
    while(condition){ context };
    do{ context }while(condition);
    ```
- `break`와 `continue`
    - break는 반복루프를 탈출해 반복을 중단시킨다.
    - continue는 특정조건에서 반복을 건너 뛰고 다음 반복작업을 수행시킨다.
</br>

>   다음장[배열 vs 문자열](https://github.com/ss-won/Javascript/blob/master/Basic/basic4.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
