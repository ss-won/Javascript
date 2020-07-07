# Asynchronous Processing Part

## Promise
<br/>

- 기존 비동기로 작업을 처리할 당시 callback을 이용했다. => 콜백 지옥 탄생!
- new Promise((resolve, reject) => { });
=> resolve 성공했을때의 실행 함수, reject 실패했을때의 실행 함수
=> then 함수로 함수 실행 후 실행할 구문을 작동시킬 수 있다.
=> catch 함수로 함수실행 중 나타나는 에러를 잡아낼 수 있다.

</br>

>   이전장 [Asynchronous Processing: 동기(Synchronous)와 비동기(Asynchronous)](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap1.md)<br/>
>   다음장 [Asynchronous Processing: aync, await](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap3.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)