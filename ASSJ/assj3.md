# 알쓸신자 Part

## 삼항 조건 연산자
<br/>

`condition ? exprIfTrue : exprIfFalse`
- `condition`: 조건식, `exprIfTrue`: condition이 true인 경우 실행되는 문장, `exprIfFalse`: condition이 false인 경우 실행되는 문장이다.
- 조건부 삼항 연산자는 JavaScript에서 세 개의 피연산자를 취할 수 있는 유일한 연산자이다. 보통 if 명령문의 단축 형태로 쓰인다.
- 다중 사용 가능하다. -> 가독성 안좋아서 잘 쓰지 않는다.
- 코드 개행이 가능하다.
```javascript
    let a = 0;
    a ? true : false;//false

    let stop = false; let age = 23;
    age > 18 ? (
        //1
        alert("OK, you can go."),
        location.assign("continue.html")
    ) : (
        //2
        stop = true,
        alert("Sorry, you are much too young!")
    ); //1이 실행된다.
```
</br>

>   이전장 [알쓸신자: 문자열내장함수](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj2.md)<br/>
>   다음장 [알쓸신자: Truthy Falsy?](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj4.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - 삼항 조건 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
