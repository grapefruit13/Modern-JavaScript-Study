## 자바스크립트의 AND, OR 연산

_자바스크립트의 AND(`&&`), OR(`||`) 연산은 피연산자의 값을 그대로 출력하며, 왼쪽 피연산자만으로 연산 결과를 반환할 수 있다면 오른쪽 피연산자는 실행하지 않는다._

- `A && B`: A가 거짓이라면 B는 실행하지 않고 바로 A를 반환한다.
- `A || B`: A가 참이라면 B는 실행하지 않고 바로 A를 반환한다.

위의 특성을 활용해서, 자바스크립트 개발 시 쉽게 조건부 처리가 가능하다.

예를 들어, `&&` 연산자는 리액트에서 컴포넌트를 선택적으로 렌더링 할 때 많이 쓰인다.

```jsx
{
  isVisible && <div> Visible component! </div>;
}
```

그리고 `||` 연산자는 값이 존재하지 않을 때 대체 값을 넣어주는 용도로 많이 쓴다.

```jsx
function print(word) {
  const msg = word || 'Hi';
  console.log(msg);
}
```

### OR연산으로 null 처리를 할 때의 문제점

null이거나 undefined일 수 있는 값을 `||` 연산자로 대체할 수도 있으나,

그렇게 하면 변수값이 0이거나 빈 문자열일 때 등등 논리적으로 false로 취급되는 **falsy값들도 대체**된다.

```jsx
// 테이블에 넣을 값이 존재하지 않을때만 `-` 기호를 출력하려 했으나,
// 값이 0일 때마저 `-` 기호로 대체되는 문제가 있

<Column>
  <HeaderCell>header</HeaderCell>
  <Cell>{rowData[key] || '-'}</Cell>
</Column>
```

이를 방지하기 위해 사용할수 있는 연산자가 **null 병합 연산자**이다.

## null 병합 연산자 `??`

_왼쪽 피연산자가 null이나 undefined인 경우 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환한다._

`x = a ?? b` 와 같이 사용하며, 이는 다음과 동일한 동작을 한다.

```jsx
x = a !== null && a !== undefined ? a : b;
```

위에서 언급했던 테이블 예시는 아래와 같이 고칠수 있다.

```jsx
<Column>
  <HeaderCell>header</HeaderCell>
  <Cell>{rowData[key] ?? '-'}</Cell>
</Column>
```

이 연산자는 AND, OR 연산자와 마찬가지로 함수에도 사용 가능하며, 연속으로도 사용 가능하다.

```jsx
const count = getCount();

printCount(count ?? '-');
```

```jsx
let firstName = null;
let lastName = null;
let nickName = '바이올렛';

// null이나 undefined가 아닌 첫 번째 피연산자
alert(firstName ?? lastName ?? nickName ?? '익명의 사용자'); // 바이올렛
```

주의할 점은, `??` 연산자는 `&&` 나 `||` 연산자와 함께 사용할 수 없다는 것이다.

함께 사용하고자 한다면 반드시 괄호`()` 로 구분해 주어야 한다.

```jsx
let x = 1 && 2 ?? 3; // error: '&&' and '??' operations cannot be mixed without parentheses.
```
