# 10장 객체 리터럴

### 알아두자

- **프로퍼티 (p. 128)**
    
    문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이 경우에는 프로퍼티 키로 사용할 표현식을 대괄호([…])로 묶어야 한다.
    
    ```jsx
    var obj = {};
    var key = 'hello';
    
    // ES5: 프로퍼티 키 동적 생성
    obj[key] = 'world';
    // ES6: 계산된 프로퍼티 이름
    // var obj = { [key]: 'world' };
    
    console.log(obj); // {hello: "world"}
    
    ```
    
- 프로퍼티 축약 표현 (p. 134)
    
    프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다. 이때 프로퍼티 키는 변수 이름으로 자동 생성된다.
    
    ```jsx
    // ES6
    let x = 1, y = 2;
    
    // 프로퍼티 축약 표현
    const obj = { x, y };
    
    console.log(obj); // {x: 1, y: 2}
    ```
    
- 계산된 프로퍼티 이름 (p. 135)
    
    계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성하려면 객체 리터럴 외부에서 대괄호([…]) 표기법을 사용행 한다.
    
    ```jsx
    // ES5
    var prefix = 'prop';
    var i = 0;
    
    var obj = {};
    
    // 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
    obj[prefix + '-' + ++i] = i;
    obj[prefix + '-' + ++i] = i;
    obj[prefix + '-' + ++i] = i;
    
    console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
    
    ```
    
    객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.
    
    ```jsx
    // ES6
    const prefix = 'prop';
    let i = 0;
    
    // 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
    const obj = {
      [`${prefix}-${++i}`]: i,
      [`${prefix}-${++i}`]: i,
      [`${prefix}-${++i}`]: i
    };
    
    console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
    
    ```
    
- 메서드 축약 표현 (p. 135)
    
    메서드를 정의하려면 프로퍼티 값으로 함수를 할당한다.
    
    ```jsx
    // ES5
    var obj = {
      name: 'Lee',
      sayHi: function() {
        console.log('Hi! ' + this.name);
      }
    };
    
    obj.sayHi(); // Hi! Lee
    
    ```
    
    메서들를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
    
    ** 메서드 축약표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다.
    
    ```jsx
    // ES6
    const obj = {
      name: 'Lee',
      // 메서드 축약 표현
      sayHi() {
        console.log('Hi! ' + this.name);
      }
    };
    
    obj.sayHi(); // Hi! Lee
    
    ```
