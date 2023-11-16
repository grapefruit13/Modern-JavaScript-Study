# 1. 주제 선정 이유

> 책에서 &&와 ||를 이용한 단축 평가, null 병합 연산자를 설명할 때는 특정 조건에서 **'피연산자를 반환한다'**고 표현했다. 하지만 옵셔널 체이닝을 설명할 때만 **'우항의 프로퍼티 참조를 이어간다'**라고 다르게 표현한 것이 신기해서 주제로 선정했다.
> 

---

# 2. 옵셔널 체이닝 연산자의 등장 이유

> 옵셔널 체이닝은 ECMAScript 2020에서 도입됐는데, 다음의 이유로 인해 등장하게 되었다.
> 

## 1) Null 및 Undefined 처리

- 아래 예시처럼 객체의 속성에 접근할 때 그 속성이 `null` 또는 `undefined`일 경우 에러가 발생할 수 있고 프로그램이 예기치 않게 중단될 수 있음
- 옵셔널 체이닝은 이러한 상황을 방지하고 안전하게 속성에 접근할 수 있도록 도와줌

### < 예시 1 >

### 접근한 객체의 속성이 undefined인 경우 에러 발생

```jsx
let user = {};

console.log(user.address.street);

```
![](https://velog.velcdn.com/images/cielo_hello/post/d2ba7976-506d-4df1-9aa3-12102f72123e/image.png)

### 옵셔널 체이닝 연산자 사용

```jsx
let user = {};

console.log( user.address?.street );

```

![](https://velog.velcdn.com/images/cielo_hello/post/f455bb54-2006-4c08-88d3-5c7a452879bb/image.png)


### < 예시 2 >

### querySelector(...) 호출 결과가 null인 경우 에러 발생

```jsx
let html = document.querySelector('.my-element').innerHTML;

```

![](https://velog.velcdn.com/images/cielo_hello/post/5ed165e5-f964-4f9f-a5ae-58238122a785/image.png)


### 옵셔널 체이닝 연산자 사용

```jsx
let html = document.querySelector('.my-element')?.innerHTML;

console.log( html );

```

![](https://velog.velcdn.com/images/cielo_hello/post/133e5ca6-bb87-421b-a053-9788019d24b2/image.png)

## 2) 논리 연산자 `&&`의 단점 보완

- 옵셔널 체이닝 연산자가 추가되기 전에는 변수에 안전하게 접근하기 위해서 논리 연산자 `&&`를 사용했음
- 논리 연산자 `&&`를 사용하면 다음과 같은 단점이 발생했음
    1. 0과 ''도 Falsy 값이기 때문에 0과 ''이 객체로 평가되는 상황에서는 사용하기 어려움
    2. 코드가 복잡해지고 가독성이 떨어짐
- 옵셔널 체이닝 연산자를 사용하면
    1. Falsy 값이라도 `null`, `undefined`가 아니면 우항의 프로퍼티 참조를 이어감
    2. null 체크를 간소화하여 코드를 더 간결하고 읽기 쉽게 만들 수 있음

### < 예시 1 >

### Falsy 값인 경우 우항의 프로퍼티를 참조하지 못함

```jsx
let str = '';
let length = str && str.length;

console.log(length);

```

![](https://velog.velcdn.com/images/cielo_hello/post/c1497c71-aaf4-4f4d-8a2a-589218dad042/image.png)

### 옵셔널 체이닝 연산자 사용

```jsx
let str = '';
let length = str?.length;

console.log(length);

```
![](https://velog.velcdn.com/images/cielo_hello/post/768e4e75-86b5-43d5-abf4-15165ce602e3/image.png)
### < 예시 2>

### 코드가 길어짐

```jsx
let user = {};

console.log( user && user.address && user.address.street );

```

### 옵셔널 체이닝 연산자 사용

```jsx
let user = {};

console.log( user?.address?.street );

```

---

# 3. 책에서 다루지 않는 부분 보충

> 책에서 다루지 않은 옵셔널 체이닝 연산자의 활용 예시를 가지고 왔다.
> 

## 단축평가

- `?.`는 `&&`와 `||`처럼 조건식 전체를 평가하지 않고도 결과를 빠르게 반환하는 단축 평가를 함
- 따라서 왼쪽 평가대상이 `null` 또는 `undefined`이면 즉시 평가를 멈춤

```jsx
let user = null;
let x = 0;

user?.sayHi(x++); // user가 null이므로 x는 증가하지 않음

console.log(x); // 0

```

![](https://velog.velcdn.com/images/cielo_hello/post/4d4558e4-255b-4271-a466-0959790015eb/image.png)

## 존재 여부가 확실치 않은 함수를 호출하는 법

- 아래 코드에서 `?.()`를 사용해 admin의 존재 여부를 확인함
- `user1`에는 `admin`이 정의되어 있기 때문에 메서드가 제대로 호출되었고 `user2`에는 `admin`이 정의되어 있지 않았음에도 불구하고 메서드를 호출하면 에러 없이 평가가 멈춤

```jsx
let user1 = {
  admin() {
    console.log("관리자 계정입니다.");
  }
}

let user2 = {};

user1.admin?.(); // 관리자 계정입니다.
user2.admin?.();

```
![](https://velog.velcdn.com/images/cielo_hello/post/b7a2d47b-bc40-4aea-af5b-845f00e36a59/image.png)

## ?.은 delete와 조합해 사용할 수도 있음

- user가 존재하면 user.name을 삭제함

```jsx
delete user?.name;

```

# 4. 결론

> 옵셔널 체이닝 연산자는 객체의 속성에 접근할 때 중간에 속성이 없거나 null 또는 undefined일 경우에도 코드 실행을 중단시키지 않고 안전하게 처리한다. 또한, 코드 작성 시 예외 상황에 대한 대응을 더 간편하게 할 수 있게 한다.
> 

---

# 참고 자료

- 이웅모,『모던 자바스크립트 Deep Dive』, 위키북스(2021), p122-123.
- [javascript.info_옵셔널 체이닝 '?.'](https://ko.javascript.info/optional-chaining)