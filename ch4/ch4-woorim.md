# 📌 CH 4-4변수 선언의 실행 시점과 호이스팅

```
console.log(score); // undefined

var score; // 변수 선언문
```

예시코드1을 보면 변수 선언문인 `var score;`보다 변수를 참조하는 코드인 `console.log(score);`가 앞에 있다.

만약 코드가 순차적으로 실행되는 런타임에 변수 선언이 실행된다면 `console.log(score);`가 실행되는 시점에는 아직 변수가 선언되기 이전이다.
그러므로 위 코드를 실행하면 `참조 에러 Reference Error`가 발생해야 한다.

하지만 `undefined`가 출력된다.

## 왜일까?

#### 자바스크립트 엔진이 변수 선언문을 먼저 실행하여, undefined라는 값이 score라는 변수에 암묵적으로 할당되었기 때문이다.

- 자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기에 앞서 먼저 소스코드의 평가 과정을 거치면서 소스코드를 실행하기 위한 준비를 한다.
- 이때 소스코드 실행을 위한 준비 단계인 소스코드의 평가 과정에서 자바스크립트 엔진은 **변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내 먼저 실행**한다.
- 소스코드의 평가 과정이 끝나면 비로소 변수 선언을 포함한 모든 선언문을 제외하고 소스코드를 한 줄씩 순차적으로 실행한다.

#### 이처럼 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 '변수 호이스팅' 이라고 한다.

# 📌 변수 호이스팅(variable hoisting)

---

선언된 변수는 호이스팅되므로 아직 선언에 도달하지 않았더라도 해당 범위의 어느 곳에서나 변수를 참조할 수 있다.

`var`변수 선언은 해당 함수 또는 전역 범위의 맨 위로 “호이스팅"되는 것으로 볼 수 있다.

그러나 변수가 선언되기 전에 변수에 접근하면 초기화(initialization)가 아니라 **선언(declaration)만 끌어올려지므로** 값은 `undefined`가 된다.

### 예시코드1

```jsx
console.log(x === undefined); // true
var x = 3;

(function () {
  console.log(x); // undefined
  var x = "local value";
})();
```

위의 예시 코드는 아래와 동일하게 해석된다.

### 예시코드2

```jsx
var x;
console.log(x === undefined); // true
x = 3;

(function () {
  var x;
  console.log(x); // undefined
  x = "local value";
})();
```

호이스팅 때문에 함수의 모든 `var`문은 가능한 한 함수 맨 위에 가깝게 배치해야 한다.

`let`과 `const`는 변수 선언 전에 블록에서 변수를 참조하면 블록이 시작될 때부터 선언이 처리될 때까지 변수가 **\*”Temporal dead zone (TDZ)"**에 있기 때문에 항상 `ReferenceError`가 발생한다.

### 예시코드3

```jsx
console.log(x); // ReferenceError
const x = 3;

console.log(y); // ReferenceError
let y = 3;
```

선언만 호이스팅되고 값은 호이스팅되지 않는 `var` 선언과 달리, 함수 선언(function declarations)은 완전히 호이스팅되므로 해당 범위의 어느 곳에서나 함수를 안전하게 호출할 수 있다.

# 📌 **Temporal dead zone (TDZ)**

---

`let`, `const`또는 `class`로 선언된 변수는 블록의 시작부터 코드 실행이 변수가 선언되고 초기화된 위치에 도달할 때까지 “Temporal dead zone"(TDZ)에 있다고 한다.

TDZ 내에 있는 동안 변수는 값으로 초기화되지 않았으므로 변수에 액세스하려고 시도하면 `ReferenceError`가 발생한다.

변수는 실행(execution)이 코드에서 변수가 선언된 위치에 도달할 때, 값으로 초기화됩니다. 변수 선언 시 초기값을 지정하지 않은 경우 `undefined`으로 초기화된다.

이는 변수가 선언되기 전에 접근(access)하면 `undefined` 를 반환하는 `var` 변수와 다릅니다. 아래 코드는 코드에서 `let`과 `var`가 선언된 위치보다 먼저 접근했을 때 달라지는 결과를 보여준다.

### 예시코드1

```jsx
{
  // TDZ starts at beginning of scope
  console.log(bar); // "undefined"
  console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
  var bar = 1;
  let foo = 2; // End of TDZ (for foo)
}
```

#### "시간적(temporal)"이라는 용어가 사용되는 이유는 영역이 코드가 작성된 **순서(위치)가 아니라 실행 순서(시간)**에 따라 달라지기 때문이다.

### 예시코드2

예를 들어 아래의 코드는 `let`변수를 사용하는 함수가 변수가 선언되기 전에 나타나지만, 함수가 TDZ 외부에서 호출되기 때문에 작동한다.

```jsx
{
  // TDZ starts at beginning of scope
  const func = () => console.log(letVar); // OK

  // Within the TDZ letVar access throws `ReferenceError`

  let letVar = 3; // End of TDZ (for letVar)
  func(); // Called outside TDZ!
}
```

### 예시코드3

아래처럼 해당 TDZ의 let 변수에 typeof 연산자를 사용하면 ReferenceError가 발생한다:

```jsx
typeof i; // ReferenceError: Cannot access 'i' before initialization
let i = 10;
```

### 예시코드4

이는 선언되지 않은 변수 및 정의되지 않은 값을 보유하는 변수에 typeof를 사용하는 것과 다르다:

```jsx
console.log(typeof undeclaredVariable); // "undefined"
```

## 자료 출처

---

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Grammar_and_types#variable_hoisting
- 모던 자바스크립트 딥 다이브(이웅모 저)
