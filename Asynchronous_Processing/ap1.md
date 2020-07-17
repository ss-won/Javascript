# Asynchronous Processing Part

## 동기(Synchronous)와 비동기(Asynchronous)
<br/>

### `동기적(Synchronous)`처리과 `비동기적(Asynchronous)`처리의 차이
<img src="https://media.vlpt.us/images/dek1313/post/67fcab43-5716-4d3f-bcb8-f4c8b6c91261/1.JPG" alt="동기적 비동기적의 차이점">
<br>

[이미지 출처](https://velog.io/@dek1313/JS-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC%EB%B0%A9%EC%8B%9D)
<br>

- `동기적(Synchronous)` : 들어온 순서대로 차례대로, 동시에 똑같이 처리된다.
- `비동기적(Asynchronous)` : 동기적이지 않다. 들어온 순서대로가 처리되지 않는다. 실행순서가 불명확하다. 작업들이 다르게 처리된다.
<br>

> 자바스크립트 엔진(V8)의 동작에 의해, `비동기처리문`은 `작업큐`에 `동기적 실행문`은 바로 `실행 스택`에 적재되어 비동기 적으로 함수를 처리할 수 있게 한다.
<br>

> Javascript의 callback 함수(past), Promise(es6), async/await(es8)로 비동기 처리를 구현할 수 있다.
<hr>

### 비동기처리는 왜 필요한가?
<img src="https://t1.daumcdn.net/cfile/tistory/995B743C5B3C1C672C" alt="V8엔진 실행구조">
<br>

[이미지 출처](https://marlinbar.tistory.com/30)
<br>

- Javascript 실행엔진은 Single Thread이기 때문이다. 
    - __Why ?__ `Call Stack이 하나밖에 없기 때문에, 한번에 하나의 작업만(single thread) 처리할 수 있다.`
    
- 동기적으로 작업이 끝날때까지 마냥 기다릴 수 없다.
    - __Why ?__ 
    1. 대기시간이 매우 길어길 수 있는 가능성이 있다.
    2. 시간차 작업으로 인해 의도하지 않은 값이 도출될 수 있다.

```javascript
    /*  Example1 */
    function addtotal(input){
        let total = database.query();// It takes 50ms.
        console.log(total + input);
    }
    
    addtotal(10);//error
```

```javascript
    /*  Example2 */
    let num = 0;
    function First(){
        setTimeout(() => { num = 10 }, 2000);
    }
    functuon Second(){
        First();
        console.log(num / 2);
    }
    
    Second()//0 (not 5)
```
> 따라서 비동기적인 처리가 필요하다. 

- 비동기 처리의 작업의 예시
    - `jQuery의 ajax` or `Node.js의 fetch`
    - `Web DOM Event` or `Web APIs`
    - `Alert` or `Prompt`
    - `Database query`
    - `File I/O`
    - `암호화/복호화`
    - `setTimeout()` or `setInterval()` 등을 이용한 작업예약




</br>

>   이전장 [알쓸신자: 스코프(scope)와 호이스팅(Hoisting)](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj9.md)<br/>
>   다음장 [Asynchronous Processing: Promise](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap2.md)

## Recommand
- [Async History](https://www.slideshare.net/NishchitDhanani/async-history-javascript)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [JS 비동기 처리방식 - callback](https://velog.io/@dek1313/JS-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC%EB%B0%A9%EC%8B%9D)
