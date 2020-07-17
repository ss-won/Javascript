# Asynchronous Processing Part

## Promise
<br/>

### Promise가 등장한 계기
Promise가 등장하기 전(ES6 이전) 기존 비동기 작업을 처리할때는 `콜백(callback)`을 이용했다.<br>
> `콜백(callback)`은 자바스크립트에서 비동기성을 표현하는 기본 단위이다.

__그러나,__ callback은 발전하는 비동기 프로그래밍 환경을 소화하는데에 한계가 있다.<br>

- __문제점 1)__ 콜백은 비동기 흐름을 비선형적, 비순차적인 방향으로 나타낸다.
    > 보통 사람의 두뇌는 순차적, 중단적, 단일-스레드 방식을 계획하는데 익숙하므로 이는 코드를 이해하기 어렵다 따라서 유지보수가 어렵고 나쁜 코드로 이어진다.

- __문제점 2)__ `콜백지옥(Callback Hell)`을 생성한다.
    > 콜백지옥으로 인해 가독성이 매우매우 떨어진다.

- __문제점 3)__ 콜백은 프로그램을 진행하기 위해 제어를 역전시킨다(IoC).
    > 제어권을 다른 파트에 암시적으로 넘겨줘야 한다.
    > [IoC의 정의와 문제점](https://develogs.tistory.com/19)은 추후에 정리하도록 하겠다.(아직 이해가 덜되었다.)
<hr>

### Promise?
`Promise`객체는, 
    1. 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값
    2. 미랫값을 캡슐화하고 조합할 수 있게 해주는 손쉬운 반복장치

> 조금 더 쉽게 비유해서 알아보자면,

<img src="/img/promise.jpg" alt="promise1"/>
<br>

[아이콘출처](ap2.md#Reference)
<br>

 패스트푸드점에서 `햄버거`를 주문하면 우리는 햄버거 대신 대기번호가 적힌 `영수증`을 받는다.<br> 
 > 영수증은IOU(차입증서)와 같은 역할을 한다. 언젠가는 구매한 햄버거를 준다는 `프라미스(약속)`이다.<br>
 > 이제 `영수증`이 햄버거를 대신하는 `독립적인 값(Time independent)` = `미랫값(Future value)`이다.<br>
 
 영수증에 적힌 주문번호가 호출되면, __1)햄버거를 받거나__ __2)재료소진으로 제공받을 수 없거나__ 의 두가지 경우의 상황에 직면하게 될것이다.<br>
 > 이는 곧 영수증 주문번호라는 __`미랫값(Promise)`은 `성공(Fulfillment)` 아니면 `실패(Rejection)`를 의미한다는 것을 알 수 있다.__
 
 (*단, 주문전에 재고파악이 안며, 기타 경우의 수는 배제한다고 가정한다)
<hr>

### Promise의 구조
<img src="https://media.vlpt.us/images/_jouz_ryul/post/8b5708f4-366e-4527-a87e-302887e21af5/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3.png" alt="promise2" >
</br>

[이미지출처](https://velog.io/@_jouz_ryul/Promise%EB%A1%9C-%EA%B3%84%ED%9A%8D%ED%95%98%EA%B3%A0-%EA%B0%90%EC%8B%9C%EB%B0%9B%EA%B8%B0)
<br>

Promise는 비동기 연산이 종료된 이후의 결과값이나 실패 이유를 처리하기 위한 처리기를 연결해 사용한다. 프로미스를 사용하면 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있다.__(callback과 다르게 제어권이 동기적 메서드 처럼 해당 코드의 호출부에 있다.)__ 다만 최종 결과를 반환하지는 않고, 대신 프로미스를 반환해서 미래의 어떤 시점에 결과를 제공한다.
<br>

__Promise의 실행상태__
- `대기(pending)`: 이행하거나 거부되지 않은 초기 상태.
- `이행(fulfilled)`: 연산이 성공적으로 완료됨.
- `거부(rejected)`: 연산이 실패함.
<br>

__Promise의 연결__<br>
<img src="https://mdn.mozillademos.org/files/8633/promises.png" alt="promise3"/><br>
[이미지출처](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

- 이행이나 거부될 때, 프로미스에 연결한 처리기는 그 프로미스의 then 메서드에 의해 대기열에 오른다. 이미 이행했거나 거부된 프로미스에 연결한 처리기도 호출하므로, 비동기 연산과 처리기 연결 사이에 경합 조건은 없다.
- `Promise.prototype.then()`로 프라미스를 받아 이후 동작을 설정할 수 있다.
- `Promise.prototype.catch()`로 함수실행 중 나타나는 에러를 잡아낼 수 있다.
- `Promise.prototype.then()` 및 `Promise.prototype.catch()` 메서드의 반환 값은 다른 프로미스이므로, 서로 연결할 수 있다.
<br>

```javascript
    const minus = (num) => {
        return new Promise((resolve,reject)=>{
        // We call resolve(...) when what we were doing asynchronously was successful, and reject(...) when it failed.
        setTimeout(() => { 
                const val = num - 1;
                if(val<0) reject(new Error());
                resolve(val);
                console.log(val);
            }, 2000);
        })
    }

    minus(2)
    .then(n=> minus(n))
    .then(n=>minus(n))
    .catch((err)=>console.log(err));
    //1 0 -1 Error{} 
    //prints per 2 seconds
```

</br>

>   이전장 [Asynchronous Processing: 동기(Synchronous)와 비동기(Asynchronous)](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap1.md)<br/>
>   다음장 [Asynchronous Processing: aync, await](https://github.com/ss-won/Javascript/blob/master/Asynchronous_Processing/ap3.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- 도서 [You don't know JS part2(카일심슨/한빛미디어)](http://www.yes24.com/Product/Goods/44132601)
- 아이콘 출처 [Flaticon](https://www.flaticon.com/kr/)
    - hamburger [Good Ware](https://www.flaticon.com/kr/authors/good-ware")
    - recipt [Freepik](https://www.flaticon.com/kr/authors/freepik)
    - sold out [Flat-icons](https://www.flaticon.com/kr/authors/flat-icons)
    - promise [freepik](https://www.flaticon.com/kr/authors/freepik)
