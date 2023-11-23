# 3주차 (10) - 자바스크립트의 객체 생성 방법

## 1. 객체 리터럴

_\*리터럴 - 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법_

- 가장 일반적이고 간단한 방법 이며, **중괄호** 내에 0개 이상의 프로퍼티를 정의한다.
- 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.

```jsx
var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  },
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", gender: "male", sayHello: ƒ}

person.sayHello(); // Hi! My name is Lee
```

```jsx
var emptyObject = {};
console.log(typeof emptyObject); // object
```

## 2. Object 생성자 함수

_\*생성자 함수 - new 키워드와 함께 객체를 생성하고 초기화하는 함수_

- new 연산자와 Object 생성자 함수를 호출해서 빈 객체를 생성할 수 있다.
- 먼저 빈 객체를 생성한 후에 프로퍼티나 메소드를 추가해서 객체를 완성하는 방법

```jsx
// 빈 객체의 생성
var person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.gender = 'male';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", gender: "male", sayHello: ƒ}

person.sayHello(); // Hi! My name is Lee
```

사실 Object 생성자 함수로 객체를 생성하는걸 단순화시킨 축약 표현이 위에서 소개한 객체 리터럴 방식이다. 즉, 자바스크립트 엔진은 객체 리터럴로 객체를 생성하는 코드를 만나면 내부적으로 Object 생성자 함수를 사용하여 객체를 생성한다.

따라서 개발자가 Object 생성자 함수를 사용할 일은 거의 없다.

## 3. 생성자 함수

마치 객체를 생성하기 위한 템플릿처럼 사용하여,

프로퍼티가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```jsx
// 생성자 함수
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function () {
    console.log('Hi! My name is ' + this.name);
  };
}

// 인스턴스의 생성 (**인스턴스 - 생성자 함수를 통해 생성된 객체)*
var person1 = new Person('Lee', 'male');
var person2 = new Person('Kim', 'female');

console.log('person1: ', typeof person1);
console.log('person2: ', typeof person2);
console.log('person1: ', person1);
console.log('person2: ', person2);

person1.sayHello();
person2.sayHello();
```

```jsx
var person1 = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  },
};

var person2 = {
  name: 'Kim',
  gender: 'female',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  },
};
```

- 생성자 함수 이름은 일반적으로 대문자로 시작함 (해당 함수가 생성자 함수임을 명시)
- this 는 생성자 함수가 생성할 인스턴스를 가리킴

## 4. Object.create 메서드

Object.create(prototype) 메서드로 새 객체를 생성하면, 생성한 객체의 프로토타입을 지정할 수 있다.

```jsx
var parent = {
  name: 'parent',
  sayHi: function () {
    console.log('Hi! ' + this.name);
  },
};

// 프로토타입 상속
var child = Object.create(parent);
child.name = 'child';

parent.sayHi(); // Hi! parent
child.sayHi(); // Hi! child
```

## 5. 클래스

ES6 문법으로, class키워드를 사용해서 정의한다.

new 연산자로 인스턴스를 생성해서 새로운 객체를 만들 수 있다.

```jsx
// 클래스 선언문
class Person {
  constructor(name) {
    // 생성자
    this._name = name;
  }

  sayHi() {
    console.log(`Hi! ${this._name}`);
  }
}

// 인스턴스 생성
const me = new Person('Lee');

console.log(me); // Person { name: 'Lee' }
me.sayHi(); // Hi! Lee
```

---

### 참고자료

- 이웅모님 기술블로그 - 객체: https://poiemaweb.com/js-object
