# 알쓸신자 Part

## 문자열 내장함수(String.prototype.methods)
<br/>

### 1.문자열 데이터 변수 초기화 
- `리터럴 형식`과 `네이티브 형식`이 있다.
- 문자열 데이터는 불변형이고 배열은 가변형 데이터이다.
- 데이터 변수는 '', "", `` 등을 사용할 수 있다.
- ``문자는 개행이 가능하고, __${ }__ 를 통해 변수와 문자열값을 함께 넣을 수 있다.
```javascript
    //네이티브형 선언 => 변수가 많아 사용 지양
    let ex1 = new String("ex1");
    //리터럴 형식으로만 선언할것
    let ex2 = "ex2";
```

### 2. 문자열의 길이(속성값)
- `string.length`
    - 내장 함수가 아닌 속성값이지만, 매우 자주 사용.
    - 문자열의 길이(속성)값을 return 한다.
```javascript
    let ex = 'abc';
    console.log(ex.length);//3
```
 
### 3-1. 문자열에서 특정 문자 값 찾기
1. `string.charAt(index)`
    - index는 0 - (string.length-1)의 사이의 정수값이다.
    - 문자열에서 지정된 index에 해당하는 유니코드 단일문자를 반환한다.
    - 인자가 생략되면 기본적으로 첫번째 값을 반환한다.
    - index가 문자열의 길이보다 큰 경우 ""(공백)문자를 반환한다.
2. `string[index]`
    - index는 0 - (string.length-1)의 사이의 정수값이다.
    - 문자열에서 지정된 index에 해당하는 유니코드 단일문자를 반환한다.
    - 일반적으로 가장 많이 사용한다.
```javascript
    let ex1 = "example";
    console.log(ex1.charAt(1));//x
    console.log(ex1[1]);//x
```

### 3-2. 특정 문자열의 위치 찾기
- `string.search(regexp)`
    - regexp는 정규표현식 객체로 어떤 원시 문자열 값이 주어져도 암묵적으로 RegExp 객체로 암묵적 변환된다.
    - 정규표현식과 주어진 문자열간에 첫번째로 일치하는 인덱스를 반환하고, 일치하는 값이 없으면 -1을 반환한다.
```javascript
    let ex1 = "exam";
    let ex2 = "ple"
    console.log(ex1.concat(ex2).search("ex"));//0
```
 
### 4. 문자열에서 특정 하위문자열의 존재여부 찾기 
1. `string.indexOf(searchValue[, fromIndex])` 
    - 처음부터-인덱스끝까지 searchValue와 일치하는 값이 있는지 탐색한다.
    - fromIndex는 탐색 지점을 기준으로 탐색을 시작할 값을 offset으로 표현할 수 있다.
2. `string.lastIndexOf(searchValue[, fromIndex])`
    - 인덱스끝부터-처음값까지 searchValue와 일치하는 값이 있는지 탐색한다.
    - fromIndex는 탐색 지점을 기준으로 탐색을 시작할 값을 offset으로 표현할 수 있다.
```javascript
    let ex1 = "ex1";
    console.log(ex1.indexOf("exam"));//-1
    console.log(ex1.lastIndexOf("x"));//1
```
 
### 5. 특정문자열 찾아 치환하기
- `string.replace(regexp|substr, newSubstr|function)` 
    - 어떤 패턴에 일치하는 일부 또는 모든 부분이 교체된 새로운 문자열을 반환한다.
    - regexp or substr (pattern) => replacement 문자열로 치환된다. 단, 치환할 특정 문자열이 여러번 나타나는 경우 최초에 발견된 변수만 적용한다.
    - newSubstr or function (replacement) => 해당 치환될 문자열을 적용한 새로운 문자열을 반환한다.
```javascript
    console.log(ex1.replace("ex","example"))//example1;
    /*문자열은 불변값이기 때문에 변환값은 특정 변수에 옮겨서 result로 출력해야 함*/
    console.log(ex1.valueOf());//ex1
```

### 6. 문자열 내부의 특정 구간 출력하기 
1. string.substring(indexStart[, indexEnd]);
    - indexStart이상 indexEnd(Optional)미만의 문자열을 출력한다.
    - indexEnd가 주어지지 않으면, indexStart부터 문자열 끝까지 출력한다.
2. string.substr(indexStart[, length]);
    - indexStart부터 length만큼 출력한다.
    - length가 주어지지 않으면 indexStart부터 문자열 크기만큼 출력한다.
    - length가 0 또는 음수일경우 빈 문자열이 출력된다.
    - __ECMA-262 표준 부록에서는 바람직하지 않은 표현이라 사라질 것이기 때문에 사용을 지양하라고 명시되어있다.__
```javascript
    console.log(ex1.substring(1,2));//x
    console.log(ex1.substr(0,3));//ex1
```

### 7. 특정 문자를 기준으로 잘라서 배열화하기
`string.split([separator[, limit]])` 
    - separator를 기준으로 잘라 배열의 원소로 만든다.
    - separator가 없으면 해당 문자열 전체를 하나로 갖는 배열 출력, separator가 ""(공백문자)면 해당 문자열의 문자 하나하가 배열의 원소가 되어 출력
    - limit는 배열의 원소 최대값(===배열의 최대 길이)
    - Array.join()이랑 같이 기억하기
    - 문자열에 변화값이 많을 경우 배열로 처리한 후 join으로 다시 문자열로 만들어주는게 정석!
```javascript
    let res = ex1.split("");
    log(res[0]);
    res = res.reverse().join("");
    log(res);
```

### 8. 소문자/대문자 변경 
1. `string.toLowerCase()`
    - 대문자 -> 소문자로 변환한다.
2. `string.toUpperCase()`
    - 소문자 -> 대문자로 변환한다.
```javascript
    console.log(ex1.toLowerCase());//ex1
    console.log(ex1.toUpperCase());//EX1
```

### 9. 문자열 합치기 
- `string.concat(string2, string3[, ..., stringN])`
    - 합칠문자열이 뒤에 붙은 새로운 문자열이 반환된다.
```javascript
    let ex1 = "exam"
    let ex2 = "ple"
    console.log(ex1.concat(ex2));//example
```

### 10. 공백 제거하기
- `string.trim()` 
    - 양쪽 끝의 공백을 없애줌
```javascript
    var ex3 = " " + ex1.concat(" ");
    log(ex3);
    log(ex3.trim());
```

</br>

>   이전장 [알쓸신자: 배열내장함수](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj1.md)<br/>
>   다음장 [알쓸신자: 삼항연산자](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj3.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - String](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)

