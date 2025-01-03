- [10장 "객체 리터럴"](https://github.com/darkmyu/note/tree/main/01_%EB%AA%A8%EB%8D%98_%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8_Deep_Dive/CH_10_%EA%B0%9D%EC%B2%B4_%EB%A6%AC%ED%84%B0%EB%9F%B4#102-%EA%B0%9D%EC%B2%B4-%EB%A6%AC%ED%84%B0%EB%9F%B4%EC%97%90-%EC%9D%98%ED%95%9C-%EA%B0%9D%EC%B2%B4-%EC%83%9D%EC%84%B1) 에 의한 객체 생성 방식은 가장 일반적이고 간단한 객체 생성 방식이다.
- 객체는 객체 리터럴 이외에도 다양한 방법으로 생성할 수 있으며, 그중 생성자 함수를 사용하여 객체를 생성하는 방식을 서술한다.

<br />

#### 17.1 Object 생성자 함수
- new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.

<br />

#### 17.2 생성자 함수
- 생성자 함수란 new 연산자와 함께 호출하여 객체(인스터스)를 생성하는 함수를 의미한다.

<br />

#### 17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점
- 객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다.
- 따라서 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.

```js
const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};

const circle2 = {
  radius: 10, // circle1 과 동일한 프로퍼티 구조
  getDiameter() { // circle 에 기능과 동일한 메서드
    return 2 * this.radius;
  }
};
```

<br />

#### 17.2.2 생성자 함수에 의한 객체 생성 방식의 장점
- 생성자 함수에 의한 객체 생성 방식은 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.
- 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.

```js
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius; 
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);
```

<br />

#### 17.2.3 생성자 함수의 인스턴스 생성 과정
- 생성자 함수의 역할은 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것이다.
- 예제에서 생성자 함수 코드를 살펴보면 this 에 프로퍼티를 추가하고 전달된 인수를 프로퍼티의 초기값으로서 할당하여 인스턴스를 초기화한다.
- 하지만 인스턴스를 생성하고 반환하는 코드는 보이지 않는데, 이는 자바스크립트 엔진이 암묵적으로 인스턴스를 초기화한 뒤 반환하기 때문이다.

```js
function Circle(radius) {
  // 1. 인스턴스 생성과 this 바인딩
  // - 암묵적으로 빈 객체가 생성되며 해당 객체(인스턴스)는 this 에 바인딩된다.

  // 2. 인스턴스 초기화
  // - 생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this 에 바인딩되어 있는 인스턴스를 초기화한다.
  // - 즉, 프로퍼티나 메서드를 추가하고 생성자 함수가 인수로 전달받은 초기값을 인스터스 프로퍼티에 할당하여 초기화하거나 고정값을 할당한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.raidus;
  };

  // 3. 인스턴스 반환
  // - 생성자 함수 내부에서 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this 를 암묵적으로 반환한다.
}
```

<br />

#### 17.2.4 내부 메서드 [[Call]] 과 [[Construct]]
- 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 갖는다.
- 함수 객체는 일반 객체와는 다르며, 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다.
- 따라서 함수 객체는 [[Environment]], [[FormalParameters]] 등의 내부 슬롯과 [[Call]], [[Construct]] 같은 내부 메서드를 추가적으로 갖는다.
- 함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드 [[Call]]이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 [[Construct]] 가 호출된다.


- 내부 메서드 [[Call]] 을 갖는 함수 객체를 callable 이라 하며, 호출할 수 있는 함수를 말한다.
- 내부 메서드 [[Construct]] 을 갖는 함수 객체를 constructor 이라 하며, 생성자 함수로서 호출할 수 있는 함수를 말한다.
- 내부 메서드 [[Construct]] 을 갖지 않는 함수 객체를 non-constructor 이라 하며, 생성자 함수로서 호출할 수 없는 함수를 말한다.


- 함수 객체는 callable 이면서 constructor 이거나 callable 이면서 non-constructor 한 것을 의미한다.
- 즉, 모든 함수 객체는 호출(callable)할 수 있지만 모든 함수 객체를 생성자 함수(constructor)로서 호출할 수 있는 것은 아니다.

<br />

#### 17.2.5 constructor 와 non-constructor 의 구분
- 자바스크립트 엔진은 함수 정의를 평가하여 함수 객체를 생성할 때 함수 정의 방식에 따라 함수를 constructor 와 non-constructor 로 구분한다.
  - constructor : 함수 선언문, 함수 표현식, 클래스
  - non-constructor : 메서드([ES6 메서드 축약 표현](https://github.com/darkmyu/note/tree/main/01_%EB%AA%A8%EB%8D%98_%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8_Deep_Dive/CH_10_%EA%B0%9D%EC%B2%B4_%EB%A6%AC%ED%84%B0%EB%9F%B4#1093-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%B6%95%EC%95%BD-%ED%91%9C%ED%98%84)), 화살표 함수

<br />

#### 17.2.6 new 연산자
- 일반 함수와 생성자 함수에 특별한 형식적 차이는 없다.
- new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.
- 단, new 연산자와 함께 호출하는 함수는 non-constructor 가 아닌 constructor 이어야 한다.
- 또한, 일반 함수와 생성자 함수에 구분을 위해 첫 문자를 대문자로 기술하는 파스칼 케이스로 명명하도록 한다.

<br />

#### 17.2.7 new.target
- ES6 에서는 생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 new.target 을 지원한다.
- new.target 은 this 와 유사하게 constructor 인 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용되며 메타 프로퍼티라고 부른다.
- new 연산자와 함께 생성자 함수로서 호출되면 new.target 함수 자신을 가리키며, new 연산자 없이 일반 함수로서 호출되면 new.target 은 undefined 다.

<br />
