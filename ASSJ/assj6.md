# 알쓸신자 Part

## 조건문 대체하기
<br/>

> Case1 : 비교군이 많은 경우 -> `배열`을 활용한다.
```javascript
const contrast = ( param ) => {
    return ( param === 'e1' || param === 'e2' || param === 'e3' || param === 'e4' || param === 'e5' );
}

// 배열과 배열 내장함수 사용
const contrastArray = ( param ) => {
    let arr = ['e1', 'e2', 'e3', 'e4', 'e5'];
    return arr.includes(param);
}

// 더 간결한 표기 (무조건 간결한게 우수하지는 않다 -> 가독성이 좋아야 한다.)
const contrastArrayClear1 = ( param ) => ['e1', 'e2', 'e3', 'e4', 'e5'].includes(param);
const contrastArrayClear2 = ( param ) => ['e1', 'e2', 'e3', 'e4', 'e5'].some(v => v === param);
```
- Array 내장함수 includes를 사용해 인자들이 있는지 확인

> Case 2: switch, if문 등의 조건(case)에 따른 결과의 경우의 수가 많은 경우 -> `객체`를 활용한다.
```javascript
const print = ( param ) => {
    if(param === 'e1') return 'first';
    if(param === 'e2') return 'second';
    if(param === 'e3') return 'third';
    if(param === 'e4') return 'fourth';
    if(param === 'e5') return 'fifth';
    else return 0;
}

// 객체 활용하기(key-value의 형태 활용)
const printbyObject1 = ( param ) => {
    const feature = {
        'e1': 'first',
        'e2': 'second',
        'e3': 'third',
        'e4': 'fourth',
        'e5': 'fifth'
    }
    return feature[param] || 0;
}

//객체 활용하기(함수의 활용)
const printbyObject2 = ( param ) => {
    const featureName = {
        e1: () => { console.log('first') },
        e2() { console.log('second') },
        e3() { console.log('third') },
        e4: () => { console.log('fourth') },
        e5: () => { console.log('fifth') }
    }
    return featureName[param] || console.log(0);
}
```
- truthy, falsy 개념 활용해 비교 인자가 있는지 확인할 수 있다.
- 객체 내부 익명함수는 화살표 함수, 메소드 표기법을 활용하는 것이 좋다.
</br>

>   이전장 [알쓸신자: 단축평가논리계산법](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj5.md)<br/>
>   다음장 [알쓸신자: 비구조화 할당](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj7.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
