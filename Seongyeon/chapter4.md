# 4. 변수

## 변수 (Variable)

**하나의 값을 저장하기 위해 확보한 `메모리 공간 자체`  or 그 메모리 공간을 `식별하기 위해 붙인 이름` (= 값의 위치를 가리키는 상징적인 이름)**

```jsx
var result = 10 + 20;
```

- 여기서 `result` 는 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름 = `변수이름`
- 변수에 저장된 값(위 예제에서 30) = `변수값`
- 변수에 값을 저장하는 행위 = `할당(Assignment, 대입, 저장)`
- 변수에 저장된 값을 읽어 들이는 것 = `참조(Reference)`

---

## 식별자 (Idenrifier)

**어떤 값을 구별해서 식별할 수 있는 고유한 이름**

- 식별자는 값이 아닌 `메모리 주소를 기억`하고 있음
- 식별자 = 메모리 주소에 붙인 이름

---

## 변수 선언

**값을 저장하기 위한 `메모리 공간을 확보`하고 `변수 이름과 확보된 메모리 공간의 주소를 연결`해서 값을 저장할 수 있게 `준비하는 과정`**

```jsx
var person; // 변수 선언(변수 선언문)
```

- 변수를 사용하려면 반드시 선언이 필요
- 변수 선언시에는 `var`, `let`, `const` 키워드를 사용
- ES6 이전에는 `var 키워드` 만 사용해서 변수를 선언했음

### 자바스크립트 엔진의 변수 선언 단계

1. `선언 단계` : 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알림
2. `초기화 단계` : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined 를 할당해 초기화함

- `var` `let` `const` 키워드를 사용한 변수 선언은 `선언단계와 초기화 단계가 동시에 진행` 됨
  예시)  `var person;`
  - 선언 단계를 통해 변수 이름은 `person 으로 등록`
  - 초기화 단계를 통해 person 변수에 `암묵적으로 undefined를 할당` 해 초기화함
  - 따라서, `var` 키워드로 선언한 변수는 어떠한 값도 할당하지 않아도 기본적으로 `undefined` 라는 값을 가짐

---

## 변수 호이스팅 (Hoisting)

**변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징**

```jsx
// 변수 선언문보다 변수를 참조하는 코드가 앞에 있는 경우

console.log(person); // undefined
var person; // 변수 선언문
```

자바스크립트는 인터프리터에 의해 한 줄씩순차적으로 실행되므로 위에 코드는 ReferenceError가 발생할 것처럼 보이나 에러가 발생하지 않고 `undefind가 출력`됨

⇒ 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문!

- 자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기에 앞서, 먼저 `소스코드의 평가` 과정을 거치면서 소스코드 실행을 위한 준비를 함
- 엔진은 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내 먼저 실행함
- 소스코드 평가 과정이 끝나면, 변수 선언을 포함한 모든 선언문을 제외하고 소스코드를 한 줄씩 순차적으로 실행함
- 즉, 엔진은 `변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 가장 먼저 실행` → `변수 선언이 어디에 위치하던 상관없이 어디서든 변수를 참조할 수 있음` ( ReferenceError가 발생하지 않는 이유 )

---

## 값의 재할당

**이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당하는 것**

```jsx
var person = 'YOUNG MIN'; // 변수 선언 & 값의 할당
person = 'YOUNG MAN'; // 값의 재할당
```

---

## 식별자 네이밍 규칙

- 식별자는 특수문자를 제외한 `문자, 숫자, 언더스코어(_), 달러 기호($)` 를 포함 할 수 있음
- 단, 식별자는 특수문자를 제외한 `문자, 언더스코어(_), 달러 기호($)` 로 시작해야 함 (`숫자로 시작 불가`)
- 예약어는 식별자로 사용할 수 없음

### 네이밍 컨벤션

자바스크립트에서는 일반적으로 아래와 같이 사용함

- `변수` 나 `함수` 이름 ⇒ `카멜 케이스(camelCase)`
- `생성자 함수`, `클래스 이름` ⇒ `파스칼 케이스(PascalCase)`

```jsx
// 카멜 케이스(camelCase)
var fistMan;

// 파스칼 케이스(PascalCase)
var FirstMan;

// 스네이크 케이스(snake_case)
var first_man;
```