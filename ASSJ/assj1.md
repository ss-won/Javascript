# 알쓸신자 Part

## 배열내장함수(Array.prototype.methods)
<br/>

### 1. 배열의 앞,뒤로 값을 삽입 또는 삭제하기
- `push(elementN)`
    - 배열의 뒤쪽에 값을 삽입한다.

- `unshift(elementN)`
    - 배열의 앞쪽에 값을 삽입한다.

- `pop()`
    - 배열의 마지막 값을 반환하고 실제 배열에서 삭제한다.
    - 배열이 비어있으면 undefined를 반환한다.

- `shift()`
    - 배열의 첫번째 값을 반환하고 실제 배열에서 삭제한다.
    - 배열이 비어있으면 undefined를 반환한다.

```javascript
    let arr = [1, 2, 3, 4, 5];
    arr.push(6);//[1, 2, 3, 4, 5, 6]
    arr.unshift(0);//[0, 1, 2, 3, 4, 5, 6]
    console.log(arr.pop(), arr);//6 [0, 1, 2, 3, 4, 5]
    console.log(arr.shift(), arr);//0 [1, 2, 3, 4, 5]
```

### 2. 배열의 특정 부분만을 잘라내기
- `slice(startidx,endidx)`
    - startidx부터 endidx(불포함)까지의 요소를 shallow copy한 새로운 배열 반환
    - 함수를 적용한 array 본체에는 영향이 없다. (단, 엄격한모드가 아닐시엔 shallow copy 되므로, 내부 객체가 있을 경우에는 같은 레퍼런스 참조에 의해 array 본체에도 영향을 미친다.)
    - __swallow copy(얕은 복사)__ : 단순복사와 달리 새로운 객체를 생성하고 값을 복사하지만 내부 객체는 복사해왔던 본체와 같은 레퍼런스 참조
```javascript
    let arr = [1, 2, 3, 4, 5];
    arr.slice(2,3);//return [3]

    /* shallow copy 예제 */
    let arr2 = [1, 2, 3, [1,2], 4];
    arr.slice(3,4);//return [[1,2]]
    arr2[0].push(3);
    console.log(arr2)//[1,2,3,[1,2,3],4];
```
- `splice(startidx,제거할 요소 개수,optional[추가할 요소(s)])` 
    - startidx부터 제거할 요소의 개수만큼 요소를 삭제하고 잘라낸 요소 배열 반환
    - optional 요소들을 입력하면 제거된 후 해당 위치에 입력한 요소들을 추가한다.
```javascript
    let arr = [1, 2, 3, 4, 5];
    arr.splice(2,3);//return [3,4,5]
    console.log(arr);//[1,2]
    arr.splice(0, 1, 3, 4, 5);//return [1]
    console.log(arr)//[3,4,5,2]
```

### 3. 다수의 배열 병합하기
- `concat([value1[, value2[, ...[, valueN]]])`
    - 특정 value들을 array 뒤에 붙여 반환한다.
    - 만약 특정 value가 주어지지 않는다면, 배열 자체를 shallow copy한 배열을 반환한다.
```javascript
    var arr = [1, 2, 3];
    var arr2 = [4, 5, 6];
    var arr3 = arr.concat(arr2);
    console.log(arr3);//[1,2,3,4,5,6]
```

### 4. 특정 원소값(인덱스, 값) 찾기
-  `indexOf(searchElement[, fromIndex])`
    - 특정 값 val과 일치하는 첫번째 요소에 대한 인덱스 값을 반환, 없으면 -1을 반환한다.
    - `===`엄격한 동등성을 사용하여 배열의 요소들과 비교한다.
    - searchElement: 배열에서 찾을 요소의 값, fromIndex: 검색을 시작할 인덱스로 배열의 크기보다 큰 인덱스가 입력되는 경우 -1이 반환된다. 음수로 주어지면 배열 끝에서부터 offset값으로 사용되고, offset값이 배열의 크기보다 커지면 배열 전체를 탐색하는 기본 Case와 같다. []가 붙은 것은 Optional값이다.

- `findIndex(callback(element[, index[, array]])[, thisArg])`
    - 특정 조건을 만족하는 배열의 첫번째 요소에 대한 인덱스를 반환한다. 만족하는 요소가 없으면 -1을 반환한다.
    - element: 배열의 요소값, index: 배열의 인덱스값, array: find를 call한 배열본체, thisArg : callback이 호출될때 this로 사용할 객체이고 []가 붙은 것은 Optional값이다.
```javascript
    const arr = [5, 12, 8, 130, 44];
    const found = arr.findIndex(val => val > 10);
    console.log(found);//1
```

- `find(callback(element[, index[, array]])[, thisArg])`
    - 특정 조건을 만족하는 첫번째 요소를 반환한다.
    - element: 배열의 요소값, index: 배열의 인덱스값, array: find를 call한 배열본체, thisArg: callback이 호출될때 this로 사용할 객체이고 []가 붙은 것은 Optional값이다.
```javascript
    const arr = [5, 12, 8, 130, 44];
    const found = arr.find(val => val > 10);
    console.log(found);//12
```

- `includes(valueToFind[, fromIndex])`
    - 특정 값이 배열에 존재하면 true, 아니면 false를 반환한다.
    - valueToFind : 배열에서 찾을 요소값(대소문자를 구별한다), fromIndex: 검색을 시작할 인덱스로 배열의 크기보다 큰 인덱스가 입력되는 경우 -1이 반환된다. 음수로 주어지면 배열 끝에서부터 offset값으로 사용되고, offset값이 배열의 크기보다 커지면 배열 전체를 탐색하는 기본 Case와 같다. []가 붙은 것은 Optional값이다.
    - [제네릭 메소드로 사용된다.]()
```javascript
    [1, 2, 3].includes(2);     // true
    [1, 2, 3].includes(4);     // false
    [1, 2, 3].includes(3, 3);  // false
    [1, 2, 3].includes(3, -1); // true
    [1, 2, NaN].includes(NaN); // true
```

### 5. 배열 요소에 대한 반복연산
- `forEach(callback(currentvalue[, index[, array]])[, thisArg])`
    - 모든 배열의 요소에 대해 callback 함수를 적용한다.
    - currentvalue: 처리할 현재 요소, index: 처리할 현재 인덱스, array: forEach를 호출한 배열 본체, thisArg: callback이 호출될때 this로 사용할 객체이고 []가 붙은 것은 Optional값이다.
    - return 값은 undefined이다.
```javascript
    const arr = [1, 2, 3, 4, 5];
    const print = val => console.log(val);
    arr.forEach(val);//1,2,3,4,5
```

- `map(callback(currentValue[, index[, array]])[, thisArg])`
    - 모든 배열의 요소에 대해 callback함수를 적용한 새로운 배열을 반환한다.
    - currentvalue: 처리할 현재 요소, index: 처리할 현재 인덱스, array: forEach를 호출한 배열 본체, thisArg: callback이 호출될때 this로 사용할 객체이고 []가 붙은 것은 Optional값이다.
```javascript
    const arr = [1, 2, 3];
    const res = arr.map(x=>x*x);
    console.log(res);//[1,4,9]
```

- `filter(callback(element[, index[, array]])[, thisArg])`
    - 특정 조건을 만족하는 요소들의 배열을 반환한다.
    - currentvalue: 처리할 현재 요소, index: 처리할 현재 인덱스, array: forEach를 호출한 배열 본체, thisArg: callback이 호출될때 this로 사용할 객체이고 []가 붙은 것은 Optional값이다.
```javascript
    const arr = [1, 2, 3];
    const res = arr.filter((v,i)=>(i%2===0&&v>2));
    console.log(res);
```

- `reduce(callback( accumulator, currentValue[, index[, array]] )[, initialValue])`
    - 배열값에 대해 누산된 값을 반환한다.
    - accumulator: 누산기(누산값반환), currentValue: 현재 배열 값, index: 현재 인덱스, array: 현재 배열, initialValue: 누산기의 초기값(default)
```javascript
    const array1 = [1, 2, 3, 4];
    const reducer = (accumulator, currentValue) => accumulator + currentValue;
    // 1 + 2 + 3 + 4
    console.log(array1.reduce(reducer));//10
    // 5 + 1 + 2 + 3 + 4
    console.log(array1.reduce(reducer,5));//15
```

- `every(callback(element[, index[, array]])[, thisArg])`
    - (AND개념) 특정 조건에 대해 모든 배열 요소가 만족하면 true를, 그렇지 않으면 false를 반환한다.
    - element: 현재 요소, index: 현재 인덱스, array: 현재 배열, thisArg: callback이 호출될때 this로 사용할 객체
```javascript
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    function ismulti(i){
       return (i % 2 === 0);
    }
    console.log(arr.every(ismulti));//false
```

- `some(callback(element[, index[, array]])[, thisArg])`
    - (OR개념) 특정 조건에 대해 true값이 나올때까지 배열 요소에 대해 callback 함수를 실행한다. 적어도 한개 이상의 truthy값이 존재하면 true, 그렇지 않으면 false를 반환한다.
    - element: 현재 요소, index: 현재 인덱스, array: 현재 배열, thisArg: callback이 호출될때 this로 사용할 객체
```javascript
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    function ismulti(i) {
       return (i % 2 === 0);
    }
    console.log(arr.some(ismulti)); //true
```   

### 6. 배열값 정렬
- `reverse()`
    - 배열의 순서를 뒤집은 배열을 반환한다. -> shallow copy개념이 아니기 때문에 실제 함수를 실행하는 배열에 영향을 준다.
```javascript
    let arr = [1, 2, 3];
    arr.reverse();
    console.log(arr);//[3, 2, 1]
```

- `sort([compareFunction])`
    - 배열 순서를 결정하는 비교함수를 만족하는 형태로 정렬한 배열을 반환한다. -> 실제 함수를 실행하는 배열에 영향은 준다.
    - compareFunction이 생략될 경우, 배열의 모든 값을 string 형태로 취급해 유니코드 순서로 정렬한다.
```javascript
    let arr = [13, 12, 11, 10, 5, 3, 2, 1];
    arr.sort(function (a, b) {
       return a - b;//오름차순
    })
    console.log(arr); // [ 1, 2, 3, 5, 10, 11, 12, 13 ]
```

### 7. 문자열로 반환
- `toString()`
    - 배열 원소의 값을 string 형태로 반환한다.

- `join([separator])`
    - 배열 원소들을 separator 기준으로 병합해 string 형태로 반환한다.
    - separator가 생략되면 기본적으로 ','를 기준으로 병합한다.

```javascript
    let arr = [1, 2, 3];
    arr.toString();//return "1,2,3"
    arr.join();//return "1,2,3"
    arr.join("");//return "123"
```
</br>

>   이전장 [Basic: 기본문법](https://github.com/ss-won/Javascript/blob/master/Basic/basic3.md)<br/>
>   다음장 [알쓸신자: 문자열내장함수](https://github.com/ss-won/Javascript/blob/master/ASJS/assj2.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [JAVASCRIPT ARRAY METHOD 정리](http://blog.302chanwoo.com/2017/08/javascript-array-method/)
- [MDN Web Docs - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

## Recommand
- [[Javascript] map, reduce, filter를 유용하게 활용하는 15가지 방법](https://medium.com/@Dongmin_Jang/javascript-15%EA%B0%80%EC%A7%80-%EC%9C%A0%EC%9A%A9%ED%95%9C-map-reduce-filter-bfbc74f0debd)
