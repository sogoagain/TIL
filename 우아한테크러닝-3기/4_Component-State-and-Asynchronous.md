# 우아한테크러닝 3기 - 4. 컴포넌트 상태와 비동기

## 학습 목표

- 컴포넌트와 상태
- 비동기

## 간단한 수업 세션 Application

- index.js

```JavaScript
import React from "react";
import ReactDOM from "react-dom";

import App from "./App";

const rootElement = document.getElementById("root");

const sessionList = [
  { id: 1, title: "1회차: Overview" },
  { id: 2, title: "2회차: Redux 만들기" },
  { id: 3, title: "3회차: React 만들기" },
  { id: 4, title: "4회차: 컴포넌트 디자인 및 비동기" }
];

ReactDOM.render(
  <React.StrictMode>
    <App store={{ sessionList }} />
  </React.StrictMode>,
  rootElement
);
```

- App.js

```JavaScript
import React from "react";

const SessionItem = ({ title }) => <li>{title}</li>;

const App = ({ store: { sessionList } }) => {
  const [displayOrder, toggleDisplayOrder] = React.useState("ASC");
  const orderedSessionList = sessionList.map((session, i) => ({
    ...session,
    order: i
  }));

  const ontoggleDisplayOrder = () => {
    toggleDisplayOrder(displayOrder === "ASC" ? "DESC" : "ASC");
  };

  return (
    <div>
      <header>
        <h1>React and TypeScript</h1>
      </header>
      <p>전체 세션 갯수: 4개</p>
      <button onClick={ontoggleDisplayOrder}>재정렬</button>
      <ul>
        {orderedSessionList.map((session) => (
          <SessionItem title={session.title} />
        ))}
      </ul>
    </div>
  );
};

export default App;
```

### 아키텍처

- 아키텍처는 작은 코드에서부터 시작되어 하나하나 쌓여가는 것이다.
- 즉, 코드에서부터 아키텍처를 잡아가는 것이 중요하다.

#### 몇 가지 원칙들

*대원칙*: 같은 것 끼리 묶고 다른 것들은 분리하자.

1. 이름만 잘 정해도 70%는 먹고 들어 간다.
2. 쪼개라.
  - 얼마나 쪼개야 하는 것일까? 작게 쪼개라
  - 언제 쪼갤 것인가? 쪼개도 눈에 훤히 보일 때 쪼개는 것이 적절한 타이밍이다.
  - 즉, 최대한 이른 시점에 쪼개라.
  - 미루면 더 이상 쪼갤 수 없게 된다.
    - 덩치가 커져버렸는데 쪼개면 갑자기 버그가 생기진 않을까..?

- JSX 안에서 자바스크립트가 나오면 가독성이 떨어지는 것 같다.

```JavaScript
  return (
    <div>
      <header>
        <h1>React and TypeScript</h1>
      </header>
      <p>전체 세션 갯수: 4개</p>
      <button onClick={ontoggleDisplayOrder}>재정렬</button>
      <ul>
        {orderedSessionList.map((session) => (
          <SessionItem title={session.title} />
        ))}
      </ul>
    </div>
  );
```

- 쪼개자

```JavaScirpt
const SessionItem = ({ title }) => <li>{title}</li>;
const SessionList = ({ sessions }) => (
  <ul>
    {sessions.map((session) => (
      <SessionItem title={session.title} />
    ))}
  </ul>
);
```

### 상태

- 상태는 변하는 것이다.
- 일반적으로 함수 컴포넌트는 상태를 가질 수 없다.
  - 호출이 되면 값이 초기화되기 때문이다.
  - 또한, 일반적인 변수로 선언하면 상태가 변경되었을 때 React 입장에서 상태가 변경된 것을 감지할 수 없게된다.
- 이러한 문제점 때문에 Hook이 나왔고 이를 이용해 함수 컴포넌트도 상태를 가질 수 있게 되었다.

- 아래의 코드에서 `toggleDisplayOrder`는 React에서 제공하는 함수다.
- 즉, `toggleDisplayOrder`를 호출하면 React에서 호출된 것을 알 수 있고 해당 Hook을 사용하는 컴포넌트의 상태가 변경되었다는 것을 알 수 있게된다.
- 이러한 과정을 통해 상태가 변경되면 함수 컴포넌트가 새롭게 render 될 수 있다.

```JavaScript
const [displayOrder, toggleDisplayOrder] = React.useState("ASC");
  const orderedSessionList = sessionList.map((session, i) => ({
    ...session,
    order: i
  }));
```

#### Hook은 클로저인가?

- 함수 안에서 클로저가 잡히는 것이지 Hook 자체가 클로저는 아니다.

#### 클래스 컴포넌트 VS 함수 컴포넌트

- 최근 움직임은 함수 컴포넌트다.
- 직접 사용해보면 함수 컴포넌트가 클래스 컴포넌트에 비해 응집성이 높고, 간결하다. 또한 선언적이다.

> 모든 코드는 만들어졌을 때 합당한 이유가 있고 그렇기 때문에 존중 받을 이유가 있다.
> 제일 좋은 코드는 비즈니스를 성공시키는 코드이고 그 뒤를 잇는 것이 클린 코드와 같은 것들이라고 생각한다.
> '내가 동일한 상황에 처했을 때, 나는 다르게 행동할 수 있을까?'를 생각해보자.

## 제네레이터와 비동기

- 비동기와 밀접한 문법 3가지
  - 이 3가지가 얽히고설키면서 굉장히 다양한 응용이 가능하다.

```JavaScript
Promise();

// Generator
function* foo() {
}

// 비동기
async function bar() {
}
```

### 동시성과 지연(lazy)

- 다음의 코드는 동시에 실행할 수 있을까?

```JavaScirpt
const x = 10;
const y = x * 10;
```

- 동시에 실행할 수 없다.
- `y`가 `x`에 의존적이기 때문이다.
  - 즉, `x` 값이 확정되기 전에 `x * 10`을 계산할 수 없는 것이다.

- 그러면 다음의 코드는 동시에 실행할 수 있을까?

```JavaScript
const x = () => 10;
const y = x() * 10;
```

- 가능하다.
  - 그 이유는 `x` 값이 확정되는 순간을 지연(lazy) 시켰기 때문이다.
  - JavaScirpt는 함수를 반환할 수 있다는 특징을 이용해 지연(lazy)를 흉내낼 수 있다.

- `Promise` 또한 지연(lazy) 테크닉과 유사하다.

```JavaScript
// resolve, reject 함수를 호출하기 위해 함수를 전달한다.
const p = new Promise(function (resolve, reject) {
  // ...
  // 다른 함수에 resolve를 넣어놓으면 클로저로 잡히기 때문에 지연 호출이 가능하다.
  setTimeout(() => {
    resolve("1");
  }, 3000);
});

p.then(function (r) {
  console.log(r);
});
```

### 제네레이터

- 코루틴이라는 함수의 구현체

```JavaScirpt
function* make() {
  return 1;
}

// 보통의 함수라면 1이 반환되겠지만,
const i = make();

// 제네레이터 객체가 반환된다.
console.log(i);
```

#### 함수란?

- 입력값을 받고 무언가를 계산한 뒤 그 결과를 리턴하는 것
  - retrun 값이 없으면 프로시저라고 한다.

```JavaScript
function xyz(a) {
  //...
}
```

#### 코루틴이란?

- 함수인데 리턴을 여러번 할 수 있으면 어떨까?
- 다시 함수가 호출될 때 마지막 리턴을 한 지점부터 다시 시작한다면?
- 이러한 개념이 코루틴이다.
- JavaScript에서는 코루틴의 개념을 일부 차용해서 제네레이터라고 명명했다.
  - 계속해서 어떠한 값을 생산해낸다는 의미
  
```JavaScript
function* makeNumber() {
  let num = 1;
  while(true) {
    // 함수로 치면 return과 비슷한 것이지만 제네레이터의 yield는 함수를 끝내지는 않는다.
    yield num++;
  }
}

// 아직 실행한 것이 아니며 제네레이터 객체를 준비한 것이다.
const i = makeNumber();

// { value: 1, done: false } 가 출력된다.
console.log(i.next());
```

#### 어디에 사용될까?

- 제네레이터를 관찰하면 기존 함수와 달리 함수안에 상태가 있고 이를 이용해 함수 밖의 상태와 서로 커뮤니케이션 하는 그림이다.
  - 실제로 `next()`에 값을 주면 `yield`로 받을 수 있다.
  - 마치 탁구를 치듯 서로 공을 핑퐁하며 주고 받는 느낌이다.
  - 즉, 일반 함수와 가장 큰 차이점은 함수 내부적으로 상태를 유지하고 있고 밖에서 상태를 전달받을 수 있는 것.
  
```JavaScript
function* makeNumber() {
  let num = 0;
  while(true) {
    const x = yield num++;
    // "x"가 출력됨
    console.log(x);
  }
}

const i = makeNumber();
i.next('x');
```

#### 비동기 코드를 동기 코드처럼 작성하기

- Callback 구조의 간단한 비동기 코드

```JavaScirpt
const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

// callback 구조다.
delay(3000).then(() => {
  console.log("3초 뒤");
});
```

- 제네레이터를 활용해 동기 코드 처럼 작성하기
  - 동기 코드처럼 순서대로 진행되는 것 처럼 보인다.
  - 밖에서 내부를 컨트롤 할 수 있기 때문이다.
  - `redux-saga`에서 사용되는 개념이다.

```JavaScript
const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

function* main() {
  console.log("시작");
  yield delay(3000);
  console.log("3초 뒤");
}

const it = main();
const { value } = it.next();

value.then(() => {
  it.next();
});
```

- Async/Await 구문을 사용하여 동기 코드처럼 작성하기
  - 제네레이터와 비슷해 보인다.
  - async, await는 Promise에 최적화되어 있다.
  - 제네레이터(yield)는 더 일반적이고 응용범위가 넓다.

```JavaScript
const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

async function main() {
  console.log("시작");
  await delay(3000);
  console.log("3초 뒤");
}

main();
```
