# 알쓸신자 Part

## 단축평가논리계산법
<br/>

### `단축 평가 논리 계산법?`
```javascript 
    if(condition) return a else return b
``` 
- 다음과 같은 조건식과 문장이 존재할때, 이 문장을 `return a 논리 연산자 b`의 형태로 단축할 수 있다. 
- 논리연산자를 이용해 코드를 단축하는 이러한 형태를 단축 평가 논리 계산법이라고 한다.
- React의 조건부 렌더링, 함수의 조건문에 따른 변수 할당, 함수의 기본값 할당 등에 응용할 수 있는 개념이다.

>   Case1 : 논리계산자가 `&&`인 경우
```javascript 
    const example = () => {
        return a && b;
    }
``` 
- a가 __Truthy__ 하다면 => `return b` (식의 결과과 true인지 뒤에 값도 체크해야하기 때문)
- a가 __Falsy__ 하다면 => `return a` (b의 값과 상관없이 결과값이 false로 결정되었기 때문)

>   Case2 : 논리계산자가 `||`인 경우
```javascript 
    const example = () => {
        return a && b;
    }
``` 
- a가 __Falsy__ 하다면 => `return b` (뒤에 값의 여부에 따라 결정되기 때문)
- a가 __Truthy__ => `return a` (어차피 식이 true인게 결정되었기 때문)
</br>

>   이전장 [알쓸신자: Truthy Falsy?](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj4.md)<br/>
>   다음장 [알쓸신자: 조건문 대체하기](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj6.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
