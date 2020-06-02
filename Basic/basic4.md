# Basic Part

## 배열내장함수(Array.prototype.methods)
<bt/>

### 1. 배열의 앞,뒤로 값을 삽입 또는 삭제하기
- `push`, `unshift`
- `pop`, `shift`

### 2. 배열의 특정 부분만을 잘라내기
- `slice(startidx,endidx)`
    - startidx부터 endidx(불포함)까지의 요소를 shallow copy한 새로운 배열 반환
    - 함수를 적용한 array 본체에는 영향이 없다. (단, 엄격한모드가 아닐시엔 shallow copy 되므로, 내부 객체가 있을 경우에는 같은 레퍼런스 참조에 의해 array 본체에도 영향을 미친다.)
    - __swallow copy(얕은 복사)__ : 단순복사와 달리 새로운 객체를 생성하고 값을 복사하지만 내부 객체는 복사해왔던 본체와 같은 레퍼런스 참조
```javascript
    let arr = [1,2,3,4,5];
    arr.slice(2,3);//return [3]
    /* shallow copy 예제 */
    let arr2 = [1,2,3,[1,2],4];
    arr.slice(3,4);//return [[1,2]]
    arr2[0].push(3);
    console.log(arr2)//[1,2,3,[1,2,3],4];
```
- `splice(startidx,제거할 요소 개수,optional[추가할 요소(s)])` 
    - startidx부터 제거할 요소의 개수만큼 요소를 삭제하고 잘라낸 요소 배열 반환
    - optional 요소들을 입력하면 제거된 후 해당 위치에 입력한 요소들을 추가한다.
```javascript
    let arr = [1,2,3,4,5];
    arr.splice(2,3);//return [3,4,5]
    console.log(arr);//[1,2]
    arr.splice(0,1,3,4,5);//return [1]
    console.log(arr)//[3,4,5,2]
```

### 3. 다수의 배열 병합하기

### 4. 특정 원소값(인덱스, 값) 찾기
-  `indexOf(val)`
    - 특정 값 val과 일치하는 요소가 있으면 해당 인덱스 값을 반환, 없으면 -1을 반환한다.
- `findIndex(callback)`
    - 특정 조건을 만족하는 요소들의 인덱스를 반환한다.
- `find(condition)`
    - 특정 조건을 만족하는 첫번째 요소를 반환한다.
- `includes(val)`
    - 특정 값 val이 배열에 존재하면 true, 아니면 false를 반환한다.

### 5. 배열 요소에 대한 반복연산
- `forEach(callback(val,idx,thisArr))`
    - val: 현재원소값, idx: 현재 인덱스값, thisArr: 배열 본체
    - 모든 배열의 요소에 대해 callback 함수를 적용한다.
    - return 값은 undefined이다.
```javascript
    const arr = [1,2,3,4,5];
    const print = val => console.log(val);
    arr.forEach(val);//1,2,3,4,5
```
- `map(callback(val,idx,thisArr))`
    - val: 현재원소값, idx: 현재 인덱스값, thisArr: 배열 본체
    - 모든 배열의 요소에 대해 callback함수를 적용한 새로운 배열을 반환한다.
```javascript
    const arr = [1,2,3];
    const res = arr.map(x=>x*x);
    console.log(res);//[1,4,9]
```
- `filter(callback(val,idx,thisArr))`
    - val: 현재원소값, idx: 현재 인덱스값, thisArr: 배열 본체
    - 특정 조건을 만족하는 요소들의 배열을 반환한다.
```javascript
    const arr = [1,2,3];
    const res = arr.filter((v,i)=>(i%2===0&&v>2));
    console.log(res);
```

</br>

>   다음장[문자열내장함수](https://github.com/ss-won/Javascript/blob/master/Basic/basic4.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [JAVASCRIPT ARRAY METHOD 정리](http://blog.302chanwoo.com/2017/08/javascript-array-method/)
- [[Javascript] map, reduce, filter를 유용하게 활용하는 15가지 방법](https://medium.com/@Dongmin_Jang/javascript-15%EA%B0%80%EC%A7%80-%EC%9C%A0%EC%9A%A9%ED%95%9C-map-reduce-filter-bfbc74f0debd)
