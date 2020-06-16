# Basic Part

## 프로토타입(Prototype)과 클래스(Class)
<br/>

### 객체생성자(Object Initializer)
- 생성자 함수의 이름은 __대문자__ 로 시작한다.(공공연한 관례)
- `new` 키워드를 통해 생성자 함수는 객체의 인스턴스를 생성한다.
- 객체 생성자 함수에서 `this`는 해당 객체를 가리킨다.
- 여러 객체가 공통으로 가지는 함수나 속성은 prototype을 통해 정의할 수 있다. `👍재사용성이 좋다`
```javascript
    //객체 생성자 함수
    function Car(make, model, year owner) {
    this.make = make;
    this.model = model;
    this.year = year;
    this.owner = owner;
    }
    //새 객체의 인스턴스
    var car1 = new Car("Eagle", "Talon TSi", 1993, "rand");
    var car2 = new Car("Nissan", "300ZX", 1992, "ken");
```

### 프로토타입(Prototype)
- 프로토타입은 개발 사이클의 초기 단계에서 제품 혹은 어플리케이션의 외형이나 동작을 보여줄 수 있는 모델을 의미한다.
- Javascript는 기존 Java, C++과 같은 클래스 기반언어가 아닌 `프로토타입 기반 언어`로 상속 개념에서는 Object가 유일한 생성자 역할을 한다. 여기서 객체는 `Prototype`이라는 __은닉속성(private)__ 을 가진다. 
- 그 객체의 프로토타입 또한 프로토타입을 가지고 있고 이것이 반복되다, 결국 null을 프로토타입으로 가지는 오브젝트에서 끝난다. null은 더 이상의 프로토타입이 없다고 정의되며, 프로토타입 체인의 종점 역할을 한다.
- 프로토타입 체인을 통해 속성과 메소드를 상속할 수 있다.
<br/>

- 프로토타입 체인
```javascript
    let Parent = function(){
        this.a = 1;
        this.b = 2;
    }
    let child = new Parent();
    Parent.prototype.c = 3;
    //prototype chain : {a:1, b:2} => __proto__ {c:3} => __proto__ Object.prototype => null
    child.a;
    //child.[[Prototype]] 속성에 존재한다 --> 1
    child.b;
    //child.[[Prototype]] 속성에 존재한다. --> 2
    child.c;
    //child.[[Prototype]]에 존재하지 않는다. --> 상위 프로토타입을 탐색한다.
    //child.[[Prototype]].[[Prototype]]에 속성이 존재한다. --> 3
    child.d;
    //child.[[Prototype]]에 존재하지 않는다. --> 상위 프로토타입을 탐색한다.
    //child.[[Prototype]].[[Prototype]]에 존재하지 않는다. --> 상위 프로토타입을 탐색한다.
    //child.[[Prototype]].[[Prototype]].[[Prototype]]에 존재하지 않는다. --> 상위 프로토타입을 탐색한다.
    //child.[[Prototype]].[[Prototype]].[[Prototype]].[[Prototype]]은 null이다. --> 탐색을 종료하고 undefined를 반환한다.
```

- 프로토타입 정의
```javascript
    //객체 생성자 함수
    function Car(make, model, year, owner) {
    this.make = make;
    this.model = model;
    this.year = year;
    this.owner = owner;
    }
    //객체 프로토타입 함수 정의
    Car.prototype.introduce = function() {
        console.log(`It's ${this.owner}'s ${this.model} made by ${this.make} in ${this.year}`)
    }

    //새 객체의 인스턴스
    var car1 = new Car("Eagle", "Talon TSi", 1993, "rand");
    var car2 = new Car("Nissan", "300ZX", 1992, "ken");

    car1.introduce();// It's rand's Talon Tsi made by Eagle in 1993
    car2.introduce();// It's ken's 300ZX made by Nissan in 1992
```

- 프로토타입 상속
```javascript
    //객체 생성자 함수
    function Car(make, model, year, owner) {
    this.make = make;
    this.model = model;
    this.year = year;
    this.owner = owner;
    }
    //객체 프로토타입 함수 정의
    Car.prototype.introduce = function() {
        console.log(`It's ${this.owner}'s ${this.model} made by ${this.make} in ${this.year}`)
    }
    //새 객체의 인스턴스
    function Car1(model, owner){
        Car.call(this, "Eagle", model, 1993, owner);
    }
    Car1.prototype = Car.prototype

    function Car2(model, owner){
        Car.call(this, "Nissan", model, 1992, owner);
    }
    Car2.prototype = Car.prototype

    car1.introduce();// It's rand's Talon Tsi made by Eagle in 1993
    car2.introduce();// It's ken's 300ZX made by Nissan in 1992
```


### 클래스(Class) since ES6
- 클래스는 `함수`다. __-> 함수처럼 표현식과 선언으로 작성할 수 있다.__
- 클래스에는 `엄격한 모드(strict)`가 적용된다.
- 클래스에서는 `호이스팅(Hoisting)`이 발생하지 않는다. __-> 클래스를 먼저 선언해야한다.__
- 상속이 매우 용이하다.
- 클래스 내부 속성과 함수는 자동으로 `prototype` 설정이 된다.
- 자식클래스는 `extends` 키워드를 통해 부모 클래스의 공통 속성과 함수를 사용할 수 있다.
- `super` 키워드를 통해 상위 생성자 함수 상속한다.
```javascript
    class Animal { 
      constructor(name) {
        this.name = name;
      }
    
      speak() {
        console.log(this.name + ' makes a noise.');
      }
    }

    class Dog extends Animal {
      speak() {
        super.speak();
        console.log(this.name + ' barks.');
      }
    }
```

>   다음장[알쓸신자: 배열내장함수](https://github.com/ss-won/Javascript/blob/master/ASSJ/assj1.md)

## Reference
- [벨로퍼트와 함께하는 모던 자바스크립트](https://learnjs.vlpt.us/)
- [MDN Web Docs - 상속과 프로토타입](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Inheritance_and_the_prototype_chain)

