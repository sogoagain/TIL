# 우아한테크러닝 3기 - 1. React & TypeScript

## 강의 목표

### 우리들의 고민들 - 나는 잘 하고 있는가?

- SW는 어떠한 문제를 해결하기 위해 만들어 지는 것
  - 해결 방법은 사람마다 다를 수 있다.
  - 즉, 코드는 다양하다.
  - 동작은 하고 문제는 해결 되었는데 정말 잘 하고 있는지 고민이 된다.

- 네트워킹
  - 연차가 많은 사람들과의 네트워킹에 대한 갈망

- 코드 품질, 아키텍처, 적정기술에 대한 고민

### 전달하고 싶은 것

- 도구
  - 90년대에는 바닥부터 개발을 했다.
    - 예를들어, 화면에 폰트를 찍기 위해 글자를 출력하는 모듈부터 개발
  - 지금은 도구가 굉장히 많이 발달했다.
  - TypeScript, React, Etc ...

- 목표, 바램, 기대
  - (상태 State)
  - 환경 (Env)
  - 제품 Prod;
  - 목표 (Mission))
  - 코드 (Quality]
  - 상대적 {E=mc2}

> 도구가 해결하고자 하는 원천적인 미션을 이해하는 것이 도구를 잘 쓰는 길.

### 주로 다룰 도구

- TypeScript
- CodeSandbox
- React
- Redux
- MobX
- Redux-Saga
- Blueprint
- Testring Library

## TypeScript

### 타입 명시

- '프로그래밍 언어가 별거 있어?'라는 태도는 좋지 못하다.
- TypeScript의 가장 큰 특징은 '타입을 명시'하는 것이다.
- 아래의 예제에서 타입을 명시하는 것이 좋을까? 그렇지 않은 것이 좋을까?

```TypeScript
let foo = 10; // 타입 추론
let bar: number = 10; // 타입 명시

foo = false; // 문제 발생
bar = false; // 문제 발생
```

- 예전에는 코드를 복잡하고 암호문 처럼 짜는 것이 잘 짜는 것으로 취급받을 때가 있었다.
- 그러나, 지금은 코드가 길어지더라도 명시적인 것을 선호한다.
- JavaScript 또한 그 흐름에 있다.

```JavaScript
function foo() {
  // arguments 객체로 가변인자를 처리 (명시적이지 못하다.)
  console.log(arguments[0]);
  console.log(arguments[1]);
}

foo(10, 20);

// 명시적으로 표현할 수 있도록 Rest parameter가 추가되었다.
function bar(...args) {
  console.log(args[0]);
  console.log(args[1]);
}

bar(10, 20);
```

### Type Alias

- number 타입은 다양하게 사용할 수 있지만 어떤 의미를 가지고 있는지 드러내기는 어렵다.
- 이때 Type Alias를 이용해 타입에 별명을 붙여준다.
- 예를들어 number 타입으로 나이를 나타낸다면 number 타입에 Age라는 별명을 붙여줄 수 있다.

```TypeScript
// number는 다양하게 사용할 수 있지만 그만큼 부작용도 있다. (age와 weight가 같은 number로 표현되고 있다.)
let age: number = 10;
let weight: number = 72;

// 이럴 때 Type Alias spec을 사용한다.
// number 타입에 별명을 붙여준다.
type Age = number;

let age:Age = 10;
```

- Type Alias로 JavaScript의 객체를 나타내는 Object Type도 나타낼 수 있다.

```TypeScript
type Age = number;
type Foo = {
  age: Age;
  name: string;
}

const foo: Foo = {
  age: 10,
  name: 'kim', // tail comma는 넣어주는게 있어 보인다.
}
```

### Interface

- Type Alias와 Interface가 똑같아 보인다.
- 실제로 두 개의 스펙이 비슷하다. 그러나, 미묘한 차이점이 존재한다.
- 표현력이 조금 다르다.
- 이후 리액트 컴포넌트를 정의하게 될 때 자세히 알아보자.

```TypeScript
// Interface
interface Bar {
  age: Age;
  name: string;
}

const bar: Bar = {
  age: 10,
  name: 'kim,
}
```

## React

- 터미널을 열고 실제로 실습해보자.
- `create-react-app`을 살펴보자.

```Shell
yarn create react-app tech-hello --template typescript
```
  
### 간단한 리액트 컴포넌트

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

interface AppProps {
  title: string;
  color: string;
}

// 이 컴포넌트는 상태가 없다.
function App(props: AppProps) {
  return(
    <h1>{props.title}</h1>
  )
}

// 'React.StrictMode'는 개발 환경에서만 사용되며 문제가 되는 것을 detection 해서 경고해주는 것
ReactDOM.render(
  <React.StrictMode>
    <App title="Tech Hello?" color="red" />
  </React.StrictMode>,
  document.getElementById('root')
);
```
  
- babel 공식 홈페이지 playground에서 위 코드를 아래와 같이 트랜스파일링 시켜볼 수 있다.

```JavaScript
"use strict";

var _react = _interopRequireDefault(require("react"));

var _reactDom = _interopRequireDefault(require("react-dom"));

function _interopRequireDefault(obj) {
  return obj && obj.__esModule ? obj : { default: obj };
}

function App(props) {
  return /*#__PURE__*/ _react.default.createElement("h1", null, props.title);
}

_reactDom.default.render(
  /*#__PURE__*/ _react.default.createElement(
    _react.default.StrictMode,
    null,
    /*#__PURE__*/ _react.default.createElement(App, {
      title: "Tech Hello?",
      color: "red"
    })
  ),
  document.getElementById("root")
);
```

- 트랜스파일링 된 것을 보면 React.createElement()를 호출하고 있다.
- 그렇기 때문에 React로 컴포넌트를 작성할 때 `import React from 'react'`를 해주는 것이다.

### CRA(create-react-app)의 단점

- CRA가 제공하지 않는 구성을 설정하는 것이 까다롭다.
- 애플리케이션이 완성 단계에 가까워 질수록 문제가 발생한다.
- 다양한 환경을 지원하기 어렵다. (Production 환경과 Development 환경을 나누는 등)

### 상태 관리

- 여러 컴포넌트가 공유하는(관심갖는) 상태를 어떻게 관리할 것인가?
- `Flux` 아키텍처가 있다.
- 컴포넌트 자체가 Immutable 한 것을 지향한다.
- Flux 아키텍처를 지원하기 위한 대표적인 라이브러리에는 'Redux'와 'MobX'가 있다.

### Redux

- 간단하다.
- 간단한 것으로 복잡한 것을 만들기는 꽤 어렵다.
- 단순한 것들은 단순함을 취하는 이유가 있다.
  - 만든 사람이 원하는 형태로 결과물을 가이드 하기 쉽다.

### MobX

- Redux의 대체재라기 보다는 상태 관리를 바라보는 패러다임을 바꾼 것이다.
- Redux보다 복잡한데, 그래서 응용이 넓어질 수 밖에 없다.
  - 개발자들은 더 다양한 범주로 MobX를 사용할 수 있다.
  - 어떤 형태가 더 좋은 것인지 판단하기가 혼란스럽다.

> Redux와 MobX 관계는 마치 JavaScript와 TypeScript 관계와 비슷하다.
> JavaScript는 약타입 언어이고, TypeScript는 강타입 언어다.
> 유연성은 개발자가 실수할 여지를 포함하고 있다.
> 그렇기 때문에 유연성이 가진 장점도 있지만 단점도 있다.
  
