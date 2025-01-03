#### 15.1 var 키워드로 선언한 변수의 문제점
- ES5 까지 변수를 선언할 수 있는 방법은 var 키워드를 사용하는 것이었다.
- 하지만 var 키워드로 선언된 변수는 아래와 같은 특징이 있어 사용시 주의하지 않으면 심각한 문제를 발생시킬 수 있다.

<br />

#### 15.1.1 변수 중복 선언 허용
- var 키워드로 선언한 변수는 중복 선언이 가능하다.
- 동일한 이름의 변수를 모르고 중복 선언하여 값을 할당하면 의도치 않게 값이 변경되는 부작용이 발생한다.

<br />

#### 15.1.2 함수 레벨 스코프
- var 키워드로 선언한 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다.
- 전역 변수를 남발할 가능성이 높아지며 의도치 않게 전역 변수를 중복 선언하는 경우가 발생한다.

<br />

#### 15.1.3 변수 호이스팅
- var 키워드는 변수 호이스팅으로 할당문 이전에 변수를 참조하면 undefined 를 반환한다.
- 변수를 참조할 때 undefined 값으로 평가되어 에러가 발생하지 않아 오류를 발생시킬 여지가 있다.

<br />

#### 15.2 let 키워드
- var 키워드의 단점을 보완하기 위해 ES6 에서 추가된 새로운 변수 선언 키워드다.

<br />

#### 15.2.1 변수 중복 선언 금지
- let 키워드로 동일한 이름의 변수를 중복 선언하면 문법 에러가 발생한다.

<br />

#### 15.2.2 블록 레벨 스코프
- let 키워드로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정한다.

<br />

#### 15.2.3 변수 호이스팅
- let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다.
- let 키워드로 선언한 변수는 `선언 단계` 와 `초기화 단계`가 분리되어 진행된다.
- let 키워드로 선언한 변수는 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없다.
- 이처럼 변수의 선언 시점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 `일시적 사각지대(TDZ)` 라고 부른다.

<br />

#### 15.2.4 전역 객체와 let
- let 키워드로 선언한 전역 변수는 전역 객체 window 의 프로퍼티가 아니다.
- let 전역 변수는 보이지 않는 개념적인 블록([전역 렉시컬 환경의 선언적 환경 레코드, 23장 "실행 컨텍스트"](URL)) 내에 존재하게 된다.

<br />

#### 15.3 const 키워드
- const 키워드는 상수를 선언하기 위해 사용하며 let 키워드와 동일하나 약간의 차이점이 있다.

<br />

#### 15.3.1 선언과 초기화
- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.
- const 키워드로 선언한 변수는 블록 레벨 스코프를 가지며, 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

<br />

#### 15.3.2 재할당 금지
- const 키워드로 선언한 변수는 재할당이 금지된다.

<br />

#### 15.3.3 상수
- 상수는 변수의 상대 개념으로 재할당이 금지된 변수를 말한다.
- const 키워드로 선언한 변수의 원시 값을 할당한 경우 변수 값을 변경할 수 없다.
- 상수의 이름은 대문자로 선언하고 여러 단어에 경우 스네이크 케이스로 표현하는 것이 일반적이다.

<br />

#### 15.3.4 const 키워드와 객체
- **const 키워드로 선언된 변수의 객체를 할당한 경우 값을 변경할 수 있다.**
- [11.1.1절 "변경 불가능한 값"](https://github.com/darkmyu/note/tree/main/01_%EB%AA%A8%EB%8D%98_%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8_Deep_Dive/CH_11_%EC%9B%90%EC%8B%9C_%EA%B0%92%EA%B3%BC_%EA%B0%9D%EC%B2%B4%EC%9D%98_%EB%B9%84%EA%B5%90#1111-%EB%B3%80%EA%B2%BD-%EB%B6%88%EA%B0%80%EB%8A%A5%ED%95%9C-%EA%B0%92) 에서 살펴본 바와 같이 const 키워드는 재할당을 금지할 뿐 `불변` 을 의미하지는 않는다.
- 즉, 새로운 값을 재할당하는 것은 불가능하지만 프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경을 통해 객체를 변경하는 것은 가능하다.

<br />
