#### 19 프로토타입
- 자바스크립트는 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어다.
- 자바스크립트는 객체 기반의 프로그래밍 언어이며 원시 타입 값을 제외한 나머지 값들(함수, 배열, 정규 표현식 등)은 모두 객체다.

<br />

#### 19.1 객체지향 프로그래밍
- 객체지향 프로그래밍은 명령형 프로그래밍의 절차지향적 관점에서 벗어나 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임을 말한다.
- 객체지향 프로그래밍은 객체의 **상태**를 나타내는 데이터와 상태 데이터를 조작할 수 있는 **동작**을 하나의 논리적인 단위로 묶는 복합적인 자료구조라고 할 수 있다.

<br />

#### 19.2 상속과 프로토타입
- 상속은 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다.
- 자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거해 기존의 코드를 재사용한다.

<br />

```js
function Circle(radius) {
  this.radius = radius;
  this.getArea = function () {
    return Math.PI * this.radius ** 2; 
  };
}

const circle1 = new Circle(1);
const circle2 = new Circle(2);
```
- [17.2절 "생성자 함수"](https://github.com/darkmyu/note/tree/main/01_%EB%AA%A8%EB%8D%98_%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8_Deep_Dive/CH_17_%EC%83%9D%EC%84%B1%EC%9E%90_%ED%95%A8%EC%88%98%EC%97%90_%EC%9D%98%ED%95%9C_%EA%B0%9D%EC%B2%B4_%EC%83%9D%EC%84%B1#1722-%EC%83%9D%EC%84%B1%EC%9E%90-%ED%95%A8%EC%88%98%EC%97%90-%EC%9D%98%ED%95%9C-%EA%B0%9D%EC%B2%B4-%EC%83%9D%EC%84%B1-%EB%B0%A9%EC%8B%9D%EC%9D%98-%EC%9E%A5%EC%A0%90) 는 동일한 프로퍼티 구조를 갖는 객체를 여러 개 생성할 때 유용하지만 위 예제의 생성자 함수는 문제가 있다.
- Circle 생성자 함수는 인스턴스를 생성할 때마다 getArea 동일한 내용의 메서드를 중복 생성하고 모든 인스턴스가 중복 소유하는 문제가 있다.
- 이처럼 동일한 생성자 함수에 의해 생성된 모든 인스턴스가 동일한 메서드를 중복 소유하는 것은 메모리를 불필요하게 낭비하게 되며, 인스턴스를 생성할 때마다 메서드를 생성하므로 퍼포먼스에도 악영향을 줄 수 있다.

![19-1](https://github.com/user-attachments/assets/14f08eed-4cf8-4a47-b519-d7e54dfa51e3)

<br />

```js
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getArea = function() {
  return Math.PI * this.radius ** 2;
}
```
- 자바스크립트는 위와 같은 문제를 프로토타입을 기반으로 한 상속을 통해 중복을 제거할 수 있다.
- Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위 객체 역할을 하는 Circle.prototype 의 모든 프로퍼티와 메서드를 상속받는다.
- 즉, 자신의 상태를 나타내는 radius 프로퍼티만 개별적으로 소유하고 내용이 동일한 메서드는 상속을 통해 공유하여 사용하는 것이다.

![19-2](https://github.com/user-attachments/assets/e85827b7-f858-406d-80b8-8e23a67b145e)

<br />

#### 19.3 프로토타입 객체
- 프로토타입 객체는 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용된다.
- 모든 객체는 [[Prototype]]  이라는 내부 슬롯을 가지며, 저장되는 프로토타입은 객체 생성 방식에 의해 결정된다.
- 모든 객체는 하나의 프로토타입을 가지며, 모든 프로토타입은 생성자 함수와 연결되어 있다.
  - \_\_proto\_\_ 접근자 프로퍼티를 통해 자신의 [[Prototype]] 내부 슬롯이 가리키는 프로토타입에 간접적으로 접근할 수 있다.
  - constructor 프로퍼티를 통해 생성자 함수에 접근할 수 있고, 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근할 수 있다.

![19-3](https://github.com/user-attachments/assets/aea50e3c-7e67-4af8-b36d-94f2e386b50b)

<br />

#### 19.3.1 \_\_proto\_\_ 접근자 프로퍼티
- 모든 객체는 \_\_proto\_\_ 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.
- \_\_proto\_\_ 는 getter/setter 함수라고 부르는 접근자 함수([[Get]], [[Set]] 프로퍼티 어트리뷰트에 할당된 함수)를 통해 [[Prototype]] 내부 슬롯의 값, 즉 프로토타입을 취득하거나 할당한다.

```js
const obj = {};
const parent = { x: 1 };

// getter 함수인 get __proto__ 가 호출되어 obj 객체의 프로토타입을 취득
obj.__proto__;

// setter 함수인 set __proto__ 가 호출되어 obj 객체의 프로토타입을 교체
obj.__proto__ = parent;
```

<br />

- 모든 객체는 상속을 통해 Object.prototype.\_\_proto\_\_ 접근자 프로퍼티를 사용, 즉 \_\_proto\_\_ 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype 의 프로퍼티다.

```js
const person = { name: 'Lee' };

// person 객체는 __proto__ 프로퍼티를 소유하지 않는다.
console.log(person.hasOwnProperty('__proto__'));

// __proto__ 프로퍼티는 모든 객체의 프로토타입 객체인 Object.prototype 의 접근자 프로퍼티다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));

// 모든 객체는 Object.prototype 의 접근자 프로퍼티 __proto__ 를 상속받아 사용할 수 있다.
console.log({}.__proto__ === Object.prototype); // true
```

<br />

- 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서다.

```js
const parent = {};
const child = {};

// child 의 프로토타입을 parent 로 설정
child.__proto__ = parent;

// parent 의 프로토타입을 child 로 설정
parent.__proto__ = child; // TypeError: Cyclic __proto__ value
```

![19-6](https://github.com/user-attachments/assets/35e36e4c-f2ee-44e5-8293-195379970b96)

<br />

- \_\_proto\_\_ 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.
- [19.11절 "직접 상속"](URL) 을 통해 Object.prototype 을 상속받지 않는 객체를 생성할 수도 있기 때문에 \_\_proto\_\_ 접근자 프로퍼티를 사용할 수 없는 경우가 있다.
- 따라서 프로토타입의 참조를 취득하고 싶은 경우에는 Object.getprototypeOf 메서드를 사용하고, 프로토타입을 교체하고 싶은 경우에는 Object.setPrototypeOf 메서드를 사용할 것을 권장한다.

```js
// obj 는 프로토타입 체인의 종접으로 Object.__proto__ 를 상속받을 수 없다.
const obj = Object.create(null);

console.log(obj.__proto__); // undefined
console.log(Object.getPrototypeOf(obj)); // null
```

<br />

#### 19.3.2 함수 객체의 prototype 프로퍼티
- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.
- 생성자 함수로서 호출할 수 없는, 즉 non-constructor([17.2.5절 "constructor 와 non-constructor 의 구분](https://github.com/darkmyu/note/tree/main/01_%EB%AA%A8%EB%8D%98_%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8_Deep_Dive/CH_17_%EC%83%9D%EC%84%B1%EC%9E%90_%ED%95%A8%EC%88%98%EC%97%90_%EC%9D%98%ED%95%9C_%EA%B0%9D%EC%B2%B4_%EC%83%9D%EC%84%B1#1725-constructor-%EC%99%80-non-constructor-%EC%9D%98-%EA%B5%AC%EB%B6%84)) 인 화살표 함수와 ES6 메서드 축약 표현으로 정의한 메서드는 prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않는다.
- Object.prototype 으로부터 상속받은 \_\_proto\_\_ 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.

```js
function Person(name) {
  this.name = name;
}

const person = new Person('Min');
console.log(Person.prototype === person.__proto__); // true
```

| 구분                          | 소유          | 값         | 사용 주체  | 사용 목적                                       |
|-----------------------------|-------------|-----------|--------|---------------------------------------------|
| \_\_proto\_\_<br />접근자 프로퍼티 | 모든 객체       | 프로토타입의 참조 | 모든 객체  | 객체가 자신의 프로토타입에 접근 또는 교체하기 위해 사용             |
| prototype<br />프로퍼티         | constructor | 프로토타입의 참조 | 생성자 함수 | 생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용 |

![19-7](https://github.com/user-attachments/assets/fd9c6a3a-bab1-4ca4-8571-f4234ec365b4)

<br />

#### 19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수
- 모든 프로토타입은 constructor 프로퍼티를 가지며, prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다.

```js
function Person(name) {
  this.name = name;
}

const person = new Person('Min');
console.log(person.constructor === Person); // true
```

![19-8](https://github.com/user-attachments/assets/4eb812ff-4be2-4b39-b632-5e15e1c721ff)

<br />

#### 19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
- 리터럴 표기법에 의한 객체 생성 방식과 같이 명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않는 객체 생성 방식도 있다.
- 리터럴 표기법에 의해 생성된 객체의 경우 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성한 생성자 함수라고 단정할 수는 없다.

<br />

```js
// obj 객체는 객체 리터럴로 생성했다.
const obj = {};

// 하지만 obj 객체는 Object 생성자 함수와 constructor 프로퍼티로 연결되어 있다.
console.log(obj.constructor === Object); // true
```

- 하지만 위 예제의 obj 는 객체 리터럴에 의해 생성된 객체이지만 Object 생성자 함수와 constructor 프로퍼티로 연결되어 있는 이유는 뭘까?
  - ECMAScript 사양에서는 아래와 같이 정의하고 있다.
  - 객체 리터럴이 평가될 때는 추상 연산 [OrdinaryObjectCreate](https://tc39.es/ecma262/#sec-object-initializer-runtime-semantics-evaluation) 을 호출하여 빈 객체를 생성하고 프로퍼티를 추가한다.
  - Object 생성자 함수에 인수를 전달하지 않거나 undefined, null 을 인수로 전달하면서 호출하면 내부적으로는 추상 연산 [OrdinaryObjectCreate](https://tc39.es/ecma262/#sec-object-value) 를 호출하여 Object.prototype 을 프로토타입으로 갖는 빈 객체를 생성한다.

<br />

- 이처럼 Object 생성자 함수 호출과 객체 리터럴의 평가는 추상 연산 OrdinaryObjectCreate 를 호출하여 빈 객체를 생성하는 점은 동일하다.
- 하지만 new.target 의 확인이나 프로퍼티를 추가하는 처리 등 세부 내용은 달라 객체 리터럴에 의해 생성된 객체는 Object 생성자 함수가 생성한 객체가 아니다.

<br />

- 즉, 리터럴 표기법에 의해 생성된 객체도 상속을 위해 프로토타입이 필요하여 가상적인 생성자 함수를 갖는다.
- 프로토타입은 생성자 함수와 더불어 생성되며 prototype, constructor 프로퍼티에 의해 연결되어 있기 때문이다.

<br />
