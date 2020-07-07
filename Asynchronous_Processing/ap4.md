# Asynchronous Processing Part

## Promise all, Promise race
<br/>

- 여러개의 promise를 async, await으로 이용할 때는 Promise.all() 함수를 이용해 promise를 배열로 등록한다.
- Promise all은 모두 함께 시작해서 모든 promise가 끝날때까지 실행한다. => 반환물을 배열요소로 각각 담아 반환한다.
- 하나의 promise라도 error가 발생하면 모든 값을 error라고 간주한다.

- 여러개의 promise를 async, await으로 이용할 때는 Promise.race() 함수를 이용해 promise를 배열로 등록한다.
- promise 중 가장 빨리 끝난 promise 결과값을 반환한다.
- 가장 빨리 끝난 promise가 error일때만, error로 간주하고 나머지 값은 error라고 간주하지 않는다.

</br>

>   이전장 [Asynchronous Processing: aync, await](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap3.md)<br/>
>   다음장 [Driving_Principle: Javascript 구동원리](https://github.com/ss-won/Javascript/blob/master/Driving_Principle/dp1.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)