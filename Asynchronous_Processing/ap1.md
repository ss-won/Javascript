# Asynchronous Processing Part

## 동기(Synchronous)와 비동기(Asynchronous)
<br/>

### `동기적(Synchronous)`처리과 `비동기적(Asynchronous)`처리의 차이
<img src="https://media.vlpt.us/images/dek1313/post/67fcab43-5716-4d3f-bcb8-f4c8b6c91261/1.JPG" alt="동기적 비동기적의 차이점"><br>

- `동기적(Synchronous)` : 들어온 순서대로 차례대로, 동시에 똑같이 처리된다.
- `비동기적(Asynchronous)` : 동기적이지 않다. 들어온 순서대로가 아닌 동시다발적으로 처리된다. 작업들이 다르게 처리된다.

자바스크립트 엔진(V8)의 동작에 의해, `비동기처리문`은 `작업큐`에 `동기적 실행문`은 바로 `실행 스택`에 적재되어 비동기 적으로 함수를 처리할 수 있게 한다.
<hr>

### 비동기처리는 왜 필요한가?

- `jQuery의 ajax`, `fetch`, `Web api 요청`, `파일읽기(File I/O)`, `암호화/복호화`, 작업예약 등의 경우에는 비동기적으로 처리해야 한다.

</br>

>   이전장 [알쓸신자: 스코프(scope)와 호이스팅(Hoisting)](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj9.md)<br/>
>   다음장 [Asynchronous Processing: Promise](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap2.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)