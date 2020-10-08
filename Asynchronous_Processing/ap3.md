# Asynchronous Processing Part

## async, await
<br>

> __async, await이란?__

- JavaScript의 비동기 처리 구문 중 가장 최신의 문법이다. (`ES8`, `ECMAScript2017`)
- `async 함수`는 async function 객체이다. (JavaScript의 비동기 함수는 사실상 async function 객체이다.)
- `async 함수`는 `Promise`를 반환한다.
- async 함수는 function 앞에 async 키워드가 있고, 내부 비동기 함수(thenable 객체) 앞에는 await을 붙여준다.
    - `Async` : keyword defines an asynchronous function
    - `Await` : indicates that you want to resolve the Promise
- await 함수는 async 함수 내에서만 작동한다. (이외의 다른 곳에서 호출되면 Syntax Error가 발생한다.)
```javascript
async function name([param[, param[, ... param]]]) { 
    /* ============ statement ============ */
    // fetchAPI 함수가 이행될때까지 기다린다.
    const ex = await fetchAPI("something").json();
    return ex.json().id;
    // Promise<type> 이 반환된다.
    // 만약 string형이라면, Promise<string>이 반환된다.
}
```
<br>

> __async/await의 장점__
- async/await 함수를 이용하면, 동기 코드처럼 비동기 코드를 작성할 수 있다.
- Promise.then을 사용하지 않아도 된다.
    - then문이 지나치게 많아지면 가독성이 감소한다.
    - Promise.then은 연속적으로 호출되므로, 오류 위치가 어디에 있는지 알기 힘들다.
- `try ~ catch 구문`으로 에러 핸들링을 할 수 있다.
    - Promise.then과 다르게, 에러가 발생한 위치에서 `throw error`를 호출한 것과 동일하게 처리된다.

> __EXAMPLE__ <br>
> 아래 예시는 <https://ko.javascript.info/async-await> <- 이곳에서 가져왔습니다.
```javascript
// Promise 구문
class HttpError extends Error {
  constructor(response) {
    super(`${response.status} for ${response.url}`);
    this.name = 'HttpError';
    this.response = response;
  }
}

function loadJson(url) {
  return fetch(url)
    .then(response => {
      if (response.status == 200) {
        return response.json();
      } else {
        throw new Error(response.status);
      }
    })
}

// 유효한 사용자를 찾을 때까지 반복해서 username을 물어봄
function demoGithubUser() {
  let name = prompt("GitHub username을 입력하세요.", "iliakan");

  return loadJson(`https://api.github.com/users/${name}`)
    .then(user => {
      alert(`이름: ${user.name}.`);
      return user;
    })
    .catch(err => {
      if (err instanceof HttpError && err.response.status == 404) {
        alert("일치하는 사용자가 없습니다. 다시 입력해 주세요.");
        return demoGithubUser();
      } else {
        throw err;
      }
    });
}

demoGithubUser();
```

```javascript
// Async/Await 적용 구문
class HttpError extends Error {
  constructor(response) {
    super(`${response.status} for ${response.url}`);
    this.name = 'HttpError';
    this.response = response;
  }
}

async function loadJson(url) {
    let res = await fetch(url)
    if(res.status == 200){
        return res.json();
    }
    else{
        throw new Error(res.status);
    }
}

async function demoGithubUser() {
  let user;
  // 유효한 사용자를 찾을i 때까지 반복해서 username을 물어봄
  while(true){
    let name = prompt("GitHub username을 입력하세요.", "iliakan");
    try{
        user = await loadJson(`https://api.github.com/users/${name}`);
        break;
    }
    catch(err){
        if (err instanceof HttpError && err.response.status == 404) {
            alert("일치하는 사용자가 없습니다. 다시 입력해 주세요.");
        }
        else{
            throw err;
        }
    }
  }
    alert(`이름: ${user.name}.`);
    return user;
}

demoGithubUser();
```
</br>

>   이전장 [Asynchronous Processing: Promise](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap2.md)<br/>
>   다음장 [Asynchronous Processing: Promise all, Promise race](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap4.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [Javascript info - 프라미스와 async, await](https://ko.javascript.info/async-await)
- [Async History - javascript](https://www.slideshare.net/NishchitDhanani/async-history-javascript)
- [MDN - async function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function)