# 알쓸신자 Part

## 비구조화 할당(Destructuring Assignment)
<br/>

- `비구조화 할당`__(Destructuring Assignment)__ 이란 무엇인가?
    - 구조 분해 할당 구문(비구조화 할당)은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript     표현식이다.
    - 객체 및 배열의 리터럴식 선언처럼 즉석에서 쉽게 데이터 뭉치를 만들 수 있다.
    ```javascript
    // 배열의 리터럴식 선언
    const arr = [1, 2, 3, 4, 5];
    ```
    - 비구조화 할당은 리터럴선언과 다르게 할당문의 좌변에서 사용하여, 원래 변수에서 어떤 값을 분해해 할당할지 정의한다.
    ```javascript
    // 비구조화 할당의 예시
    const x = [1, 2, 3, 4, 5];
    const [y, z] = x;
    console.log(y); // 1
    console.log(z); // 2
    ```
    - 구조 분해 할당은 Perl이나 Python 등 다른 언어가 가지고 있는 기능이다.
    - ES6 이후 자바스크립트에 적용되었다.

>   __Case__ 01: `배열[array]`의 비구조화 할당
- 기본 변수 할당
```javascript
    const [ryan, apeach, tube] = ["RYAN", "APEACH", "TUBE"];
    console.log(ryan); // RYAN
    console.log(apeach); // APEACH
    console.log(tube); // TUBE
```

- 기본값 할당 + 선언 분리한 할당
```javascript
    let a, b;
    [a=5, b=7] = [1];
    console.log(a); // 1
    console.log(b); // 7
```

- 변수값 교환
```javascript
    let a = 1, b = 5;
    [a, b] = [b, a];
    console.log(a); // 5
    console.log(b); // 1
```

- 함수 반환 배열 분석하기
```javascript
    function f() {
      return [1, 2];
    }

    let a, b;
    [a, b] = f();
    console.log(a); // 1
    console.log(b); // 2
```

- 나머지(rest) 구문 적용
```javascript
    const [ryan,...friends] = ["RYAN", "APEACH", "TUBE"];
    console.log(ryan); // RYAN
    console.log(friends);//["APEACH", "TUBE"]
```

>   __Case__ 02: `객체[Object]`의 비구조화 할당
- 기본 변수 할당
```javascript
    const k_friends = {
      ryan: "RYAN",
      apeach: "APEACH",
      tube: "TUBE"
    };
    const { ryan, apeach, tube } = k_friends;
    console.log(ryan); // RYAN
    console.log(apeach); // APEACH
    console.log(tube); // TUBE
```

- 기본값 할당 + 선언 분리 + 새로운 속성명 값 적용
```javascript
    //a : aa(새로운 속성명), = 10(기본값)
    const {a: aa = 10, b: bb = 5} = {a: 3};

    console.log(aa); // 3
    console.log(bb); // 5
```

- 중첩된 객체 + 배열의 비구조화 할당
```javascript
    const metadata = {
        title: "Scratchpad",
        translations: [
           {
            locale: "de",
            localization_tags: [ ],
            last_edit: "2014-04-14T08:43:37",
            url: "/de/docs/Tools/Scratchpad",
            title: "JavaScript-Umgebung"
           }
        ],
        url: "/en-US/docs/Tools/Scratchpad"
    };

    const { title: englishTitle, translations: [{ title: localeTitle }] } = metadata;

    console.log(englishTitle); // "Scratchpad"
    console.log(localeTitle);  // "JavaScript-Umgebung"
```

- for ... of 반복문과 구조 분해
```javascript
    const people = [
      {
        name: "Mike Smith",
        family: {
          mother: "Jane Smith",
          father: "Harry Smith",
          sister: "Samantha Smith"
        },
        age: 35
      },
      {
        name: "Tom Jones",
        family: {
          mother: "Norah Jones",
          father: "Richard Jones",
          brother: "Howard Jones"
        },
        age: 25
      }
    ];

    for (let {name: n, family: { father: f } } of people) {
      console.log("Name: " + n + ", Father: " + f);
    }

    // "Name: Mike Smith, Father: Harry Smith"
    // "Name: Tom Jones, Father: Richard Jones"
```

- 계산된 속성 이름과 구조 분해
```javascript
let key = "z";
let { [key]: foo } = { z: "bar" };

console.log(foo); // "bar"
```

- 나머지(rest) 구문 비구조화 할당
```javascript
    let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40}
    a; // 10 
    b; // 20 
    rest; // { c: 30, d: 40 }
```
</br>

>   이전장 [알쓸신자: 조건문 대체하기](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj6.md)<br/>
>   다음장 [알쓸신자: spread and rest](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj8.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [Javascript ) 비구조화 할당 알아보기](https://velog.io/@public_danuel/destructuring-assignment)
- [MDN Web Docs - 구조 분해 할당 구문](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)