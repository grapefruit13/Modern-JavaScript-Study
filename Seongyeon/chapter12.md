## 12.4 함수 정의

함수 정의란 함수를 호출하기 이전에 인수를 전달 받을 매개변수와 실행할 statement들, 그리고 반환할 값을 지정하는 것을 말한다.
정의된 함수는 자바스크립트 엔진에 의해 평가되어 함수 객체가 된다.

- 함수를 정의하는 방법에는 4가지가 있다.

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var add = function (x, y) {
  return x + y;
};

// Function 생성자 함수
var add = new Function('x', 'y', 'return x + y');

// 화살표 함수(ES6)
var add = (x, y) => x + y;
```

---

### 12.4.1 함수 선언문

함수 선언문을 사용해 함수를 정의하는 방식은 다음과 같다.

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티까지 출력한다.
// 단 Node.js 환경에서는 console.log와 같은 결과가 출력된다.

console.dir(add); // f add(x, y)

// 함수 호출
console.log(add(2, 5)); //7
```

함수 선언문은 함수 리터럴과 형태가 동일하다.
단, 함수 리터럴은 함수 이름을 생략할 수 있으나. 함수 선언문은 함수 이름을 생략할 수 없다.

```javascript
// 함수 선언문은 함수 이름을 생략할 수 없다.
function (x, y) {
    return x + y;
}
// SyntaxError: Function statements require a function name
```

---

### 12.4.2 함수 표현식

함수는 일급 객체(값의 성칠을 갖는 객체)이므로 함수 리터럴로 생성한 함수 객체를 변수에 할당할 수 있다.
이러한 함수 정의 방식을 함수 표현식(function expression)이라 한다.

```javascript
// 함수 표현식
var add = function (x, y) {
  return x + y;
};
console.log(add(2, 5)); // 7
```

함수 리터럴의 함수 이름은 생략할 수 있으며, 이런 함수를 익명 함수라 한다고 했다.
함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적이다.

함수 선언문에서 살펴본 바와 같이 함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다.

```javascript
// 기명 함수 표현식
var add = function foo(x, y) {
  return x + y;

  // 함수 객체를 가리키는 식별자로 호출
  console.lod(add(2, 5)); // 7
};

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

---

### 12.4.4 생성자 함수

자바스크립트가 기본 제공하는 빌트인 함수인 Function 생성자 함수에 매개변수 목록과 함수 몸체를 문자열로 전달하면서 new 연산자와 함께 호출하면 함수 객체를 생성해서 반환한다. new 연산자 없이 호출해도 결과는 동일하다.

```javascript
var add = new Function('x', 'y', 'return x + y');

console.log(add(2, 5)): // 7
```

Function 생성자 함수를 생성하는 방식은 권장되지 않는다. 이렇게 생성된 함수는 클로저를 생성하지 않는 등, 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작한다.

```javascript
var add1 = (function () {
  var a = 10;
  return function (x, y) {
    return x + y + a;
  };
})();

console.log(add1(1, 2)); // 13

var add2 = (function () {
  var a = 10;
  return new Function('x', 'y', 'return x + y + a');
})();

console.log(add2(1, 2)); // ReferenceError: a is not defined
```

---

### 12.4.5 화살표 함수

ES6에서 도입된 화살표 함수(arrow function)는 function 키워드 대신 화살표(fat arrow) =>를 사용해 좀 더 간략한 방법으로 함수를 선언할 수 있다. 화살표 함수는 항상 익명 함수로 정의한다.

```javascript
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

화살표 함수는 기존의 함수 선언문 또는 함수 표현식을 완전히 대체하기 위해 디자인된 것은 아니다. 화살표 함수는 기존의 함수보다 표현만 간략한 것이 아니라 내부 동작 또한 간략화 되어 있다.

화살표 함수는 생성자 함수로 사용할 수 없으며, 기존 함수와 this 바인딩 방식이 다르고, prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.
