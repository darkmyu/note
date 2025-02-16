- `제어문`은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다.

<br />

#### 8.1 블록문
- `블록문`은 0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부르기도 한다.

<br />

#### 8.2 조건문
- `조건문`은 주어진 `조건식`의 평가 결과에 따라 코드 블록의 실행을 결정한다.

<br />

#### 8.2.1 if...else 문
- `if...else`문은 주어진 조건식(불리언 값으로 평가될 수 있는 표현식)의 평과 결과에 따라 실행할 코드 블록을 결정한다.

<br />

#### 8.2.2 switch 문
- `switch`문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행 흐름을 옮긴다.

<br />

#### 8.3 반복문
- `반복문`은 조건식의 평가 결과가 참인 경우 코드 블록을 실행 후, 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다.

<br />

#### 8.3.1 for 문
- `for 문`은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.

```js
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}
```

<br />

#### 8.3.2 while 문
- `while 문`은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속 반복 실행한다.

<br />

#### 8.3.3 do.while 문
- `do...while 문`은 코드 블록을 먼저 실행하고 조건식을 실행하므로, 무조건 한 번 이상 실행된다.

<br />

#### 8.4 break 문
- `break 문`은 레이블 문, 반복문, switch 문의 코드 블록을 탈출하는 역할을 한다.

<br />

#### 8.5 continue 문
- `continue 문`은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
