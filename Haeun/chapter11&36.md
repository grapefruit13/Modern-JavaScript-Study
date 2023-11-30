# 1. 주제

- 책 내용 정리
- 콜스택과 메모리힙의 데이터 저장 구조
- 원시 타입에서 메소드 호출

---

# 2. 원시 값 vs. 객체

> 원시 타입과 객체 타입은 크게 세 가지 측면에서 다르다.

![](https://velog.velcdn.com/images/cielo_hello/post/44ef8f6a-9171-4eaa-bc8d-25493cd6d914/image.png)

### 1) 변경 가능 여부

- 원시값: 변경 불가능한 값
- 객체 타입의 값: 변경 가능한 값

### 2) 변수에 저장 되는 값

- 원시값: 실제 값
- 객체 타입의 값: 참조 값

### 3) 복사

- 원시값: 원시 값이 복사되어 전달됨
- 객체 타입의 값: 참조 값이 복사되어 전달됨

---

# 3. 콜스택과 메모리힙의 데이터 저장 구조

- 컴퓨터의 모든 프로그램이 실행되기 위해선 우선 프로그램이 메모리 공간에 이동 되어야 함
- 프로그램에서 사용되는 변수들을 저장할 메모리도 필요한데, 운영체제는 프로그램을 실행하기 위해 다양한 메모리 공간을 확보하고 있음
  ![](https://velog.velcdn.com/images/cielo_hello/post/548b36fd-7161-452c-9d1d-cf88519ce6a3/image.png)
- 원시 값과 객체 타입의 값은 서로 다른 메모리 공간에 저장됨
  ![](https://velog.velcdn.com/images/cielo_hello/post/882f0652-d834-42b9-b22c-9988c19c05e5/image.webp)
- 원시 값은 콜 스택에 저장이 되고 객체 타입의 값은 메모리 힙에 저장 됨
  ![](https://velog.velcdn.com/images/cielo_hello/post/ef2d7ecb-9824-449f-b78a-30a610facd0b/image.png)

---

# 4. 원시 타입에서 메소드 호출

- 아래 코드를 보면 원시 타입도 메소드를 사용할 수 있음
- 원시 타입에어 호출하는 메서드는 표준 빌트인 객체에 정의된 메소드임

```jsx
let thisIsPrimitive = "hello world"; // 원시타입을 할당
console.log(thisIsPrimitive.toUpperCase()); //HELLO WORLD
```

- 표준 빌트인 객체
- ECMAScript 사양에 정의된 객체를 말하며 전역 객체의 프로퍼티로서 제공되기 때문에 별도의 선언 없이 전역 변수처럼 언제나 참조할 수 있음
- Number, String, Boolean, Symbol 등을 예로 들 수 있음

## 래퍼 객체

- 자바스크립트 엔진은 원시값을 객체처럼 사용하면 암묵적으로 연관된 객체를 생성함
- 객체를 생성한 후 프로퍼티에 접근하거나 메서드를 호출하고 다시 원시값으로 되돌림
- 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 래퍼 객체라고 함

## 래퍼 객체가 필요한 이유

- 객체는 다양한 프로퍼티와 메소드가 있어서 유용하지만 무겁고 느리다는 단점이 있음
- 원시 타입은 가볍고 빠르지만 객체의 기능을 사용할 수는 없음
- 두 단점을 모두 보완해서 원시 타입을 그대로 쓰고 메서드를 호출할 때만 객체로 바꾸자!
  > 원시 타입의 가벼움은 유지하면서 객체의 유용한 기능도 쓰기 위한 방법이다.

# 참고 자료

- 이웅모,『모던 자바스크립트 Deep Dive』, 위키북스(2021), p137-153.
- [JavaScript Data Types](https://www.javascripttutorial.net/javascript-data-types/)
- [콜스택/메모리힙 구조, 데이터 저장/참조 원리](https://charming-kyu.tistory.com/19)
- [A Deep Dive into Shallow Copy and Deep Copy in JavaScript](https://javascript.plainenglish.io/shallow-copy-and-deep-copy-in-javascript-a0a04104ab5c)
- [Primitive Type(원시 타입) vs Reference Type(참조 타입)](https://charming-kyu.tistory.com/20)
