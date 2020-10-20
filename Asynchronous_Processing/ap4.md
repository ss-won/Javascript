# Asynchronous Processing Part

## Promise all, Promise race

<br/>

> **Promise.all()**

```javascript
Promise.all(iterable);
```

- Array같은 iterable 객체를 인수로 받아, 여러개의 이행된(fulfilled) Promise 값을 주어진 순서대로 객체에 담아 반환한다.
  <br>

  1. 주어지는 객체가 빈 배열(객체)일 경우 **👉🏻 즉시 이행된(fulfilled) Promise 값을 반환한다.**
  2. 주어지는 객체에 Promise가 없을 경우 **👉🏻 비동기적으로 Promise를 반환한다. (단, 크롬에서는 이행된 Promise)**
  3. 1,2가 아닌 나머지 경우 **👉🏻 pending 상태의 Promise 반환, fulfilled/rejected 된다면 해당 Promise 값을 주어진 객체의 순서대로 담아 반환한다.**

- 일반적인 경우(Promise는 객체가 비어있을 때를 제외) Promise all은 모두 함께 시작해서 모든 promise가 끝날때까지 실행한다. **👉🏻 모든 객체 원소가 비동기적으로 이행된다.**

```javascript
const mixedPromisesArray = [Promise.resolve(33), Promise.reject(44), 55];
const haveNotPromisesArray = [33, 44, 55];
const emptyPromiseArray = [];
const p1 = Promise.all(mixedPromisesArray);
const p2 = Promise.all(haveNotPromisesArray);
const p3 = Promise.all(emptyPromiseArray);
console.log(p1);
console.log(p2);
console.log(p3);
setTimeout(function () {
  console.log("the stack is now empty");
  console.log(p1);
  console.log(p2);
});

// 출력
// Promise { <state>: "pending" }
// Promise { <state>: "pending" }
// Promise { <state>: "fulfilled", <value>: Array[0] }
// the stack is now empty
// Promise { <state>: "rejected", <reason>: 44 }
// Promise { <state>: "fulfilled", <value>: Array[3] }
```

- 하나의 promise라도 rejected가 발생하면 다른 Promise의 이행 결과와 상관없이 모든 값이 해당 이유에 따라 rejected되고 해당 객체를 반환한다. <br> **👉🏻 Promise.all()의 실패 우선성**

  - 각 Promise에 대해 발생할 수 있는 거부를 사전에 처리해 주면 동작방식을 바꿀 수 있다. <br>

  ```javascript
  const p1 = new Promise((resolve, reject) => {
    setTimeout(() => resolve("p1_지연_이행"), 1000);
  });
  const p2 = new Promise((resolve, reject) => {
    reject(new Error("p2*즉시*거부"));
  });
  Promise.all([
    p1.catch((error) => {
      return error;
    }),
    p2.catch((error) => {
      return error;
    }),
  ]).then((values) => {
    console.log(values[0]); // "p1*지연*이행"
    console.log(values[1]); // "Error: p2*즉시*거부"
  });
  ```

- 여러개의 promise를 async, await으로 이용할 때는 Promise.all() 함수를 이용해 promise를 배열로 등록하면 결과를 집계할 때 유용하게 사용할 수 있다.

<br>

> **Promise.race()**

```javascript
Promise.race(iterable);
```

- Array같은 iterable 객체를 입력 받아, 가장 먼저 이행(fulfilled)되거나 거부된(rejected) 프로미스 값을 비동적으로 전달받는 대기중인(pending) Promise 객체를 반환한다.

  - 비어있는 iterable 객체를 입력하면 **👉🏻 영원히 pending 상태가 된다.**
  - 객체에 Promise가 아닌 값이나, 이미 이행된 Promise 객체가 포함된 경우 **👉🏻 처음으로 등장하는 해당 값을 반환한다.** <br>

  ```javascript
  const foreverPendingPromise = Promise.race([]);
  const alreadyFulfilledProm = Promise.resolve(666);

  const arr = [foreverPendingPromise, alreadyFulfilledProm, "프로미스 아님"];
  const arr2 = [foreverPendingPromise, "프로미스 아님", Promise.resolve(666)];
  const p = Promise.race(arr);
  const p2 = Promise.race(arr2);

  console.log(p);
  console.log(p2);
  setTimeout(function () {
    console.log("the stack is now empty");
    console.log(p);
    console.log(p2);
    console.log(foreverPendingPromise);
  });

  // 로그 출력 결과 (순서대로):
  // Promise { <state>: "pending" }
  // Promise { <state>: "pending" }
  // the stack is now empty
  // Promise { <state>: "fulfilled", <value>: 666 }
  // Promise { <state>: "fulfilled", <value>: "프로미스 아님" }
  // Promise { <state>: "pending" }
  ```

- 가장 빠르게 수행된 Promise가 rejected되었다면, rejected를 반환한다. 그러나 다른 값을 모두 rejected되었다고 취급하지는 않는다.

```javascript
const p1 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("하나"), 500);
});
const p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("둘"), 100);
});

Promise.race([p1, p2]).then(function (value) {
  console.log(value); // "둘"
  // 둘 다 이행하지만 p2가 더 빠르므로
});

const p3 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("셋"), 100);
});
const p4 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error("넷")), 500);
});

Promise.race([p3, p4]).then(
  function (value) {
    console.log(value); // "셋"
    // p3이 더 빠르므로 이행함
  },
  function (reason) {
    // 실행되지 않음
  }
);

const p5 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("다섯"), 500);
});
const p6 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error("여섯")), 100);
});

Promise.race([p5, p6]).then(
  function (value) {
    // 실행되지 않음
  },
  function (error) {
    console.log(error.message); // "여섯"
    // p6이 더 빠르므로 거부함
  }
);
```

- 여러개의 promise를 async, await으로 이용할 때는 Promise.race() 함수를 이용해 promise를 배열로 등록하면 먼저 끝나는 promise 객체의 값을 이용할 때 유용하다.

</br>

> 이전장 [Asynchronous Processing: aync, await](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap3.md)<br/>
> 다음장 [Driving_Principle: Javascript 구동원리](https://github.com/ss-won/Javascript/blob/master/Driving_Principle/dp1.md)

## Reference

- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN - Promise.all()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
- [MDN - Promise.race()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)
