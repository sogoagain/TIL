# 우아한테크러닝 3기 - 3. React

## 학습 목표

- React 기본적인 내용
- React 만들기

### 라이브러리를 구현해보는 이유

- 특정한 기능을 사용하는 입장에서 머물지 않았으면 좋겠다.
  - 사용법만 보고 쓰는 학습만 하다보면 좋지 못하다.
  - 깊이보단 넓이만을 추구하게 된다.
  - 기술을 사용할 때 나쁜 것 같은데 뭐가 나쁜지 모르겠고, 좋은 것 같은데 왜 좋은지 모르면 좋지 않다.
  - '나보다 개발 잘 하는 사람들이 만들었으니 좋을 것이다'라는 생각은 좋지 않다.
- 기술적으로 생각하는 힘을 기르자
  - 이 라이브러리는 어떤 기술로 만들었을까?
  - 이 라이브러리는 어떤 생각으로 만들었을까?
  - 그래서 이런 방식으로 사용해야 하는구나
  - 내 생각엔 A라는 방식이 적정 기술일 것 같은데, 내 생각하고는 다르네?
  - React 팀에서 만들었다고 다 옳은 것일까?
- 왜 이렇게 사용해야 하는가?
  - 이러한 것은 문서에 기술되지 않는다.
  - 이것을 알아가는 것이 이번 강의의 목표다.
  - 그래서 직접 만들어 보는 것이다.

## React

### 좋은 설계

- WebApp이란 무엇인가?
  - 어떠한 데이터를
  - 어떤 모양으로
  - 어딘가에 출력하는 것
- 그런데,
  - 데이터가 많아지고...
  - UI가 많아지고...
  - 라우팅이 필요하고...
  - 데이터를 API를 통해 비동기로 가져오고...
  - 예외를 처리하고...
  - 권한을 처리하고...
- Application이 한 번 만들어 놓으면 그 이후로 절대 변하지 않는다면 공부를 많이 하지 않아도 될 것 이다.
- 문제는 끊임없이 변한다는 것이다.
- 한달 전에 만든 기능을 고치려고 하니 생각이 잘 나지 않는다.
  - 생각이 빨리 나는 구조를 연구한다.
  - 어떤 것이 좋은 아키텍처인가?
- 대원칙
  - 같은 것 끼리 묶고 다른 것들은 분리하자.
  - 어떤 것이 같은 것이고 어떤 것이 다른 것인가?
  - 지식의 수준에 따라서 다르게 보이기도 한다.
    - 죽었다 깨어나도 중복이 없을 것 같은데 자세히 보면 중복이 보이기도 하고...
    - 즉, 같은 것과 다른 것을 분리하는 것도 역량에 따라 차이가 많이 난다.
- 제일 첫 번째로 `이름`만 잘 지어도 70% 이상은 먹고 들어간다.
  - 너무 높은 수준의 무언가를 추구하다가 정말 기본적인 것을 소홀히 하는 것을 많이 봤다.
  - 일단 70%는 먹고 들어가자.

### 간단한 WebApp을 기존의 방식으로 구현

- Real DOM의 API가 low level의 API다. 즉, 추상화 수준이 높지 않아 복잡도가 올라간다.
  - 복잡도가 높다는 것은 수정이 용이하지 못하다는 것이다.
- 이 문제를 해결하기 위해 오랫동안 연구를 많이했다.
  - MVC 패턴, two way binding 등
  - 그러나, 이 역시 일정 규모 이상으로 복잡도를 제어하기 쉽지 않았다.
- Facebook 친구들이 이런 상황을 타파하기 위해 React를 만들었다.

```JavaScript
const list = [
  { title: 'React' },
  { title: 'Redux' },
  { title: 'TypeScript' },
];

const rootElement = document.getElementById('root');

function app(items) {
  rootElement.innerHTML = `
    <ul>
      ${ items.map(item => `<li>${item.title}</li>`).join("") }
    </ul>
  `;
}

app(items);
```

### 리액트의 컨셉 - 추상화

- 리액트가 DOM의 복잡성을 다루는 방식은 다른 곳에서도 많이 쓰는 간단한 기법이다.
- 다루기 까다로운 친구가 있을 때 이것을 직접 다루기 보단 덜 까다롭게 다루는 녀석으로 감싸는 것이다.
  - 그렇지만 여전히 복잡도는 존재한다. 그래서 아예 다루기 쉬운 구조로 만들어 사용하기 쉽도록 한다.
- 대표적인 예 - 브라우저
  - HTML 태그는 문자열이다.
  - 기본적으로 문자열은 다루기가 굉장히 까다롭다.
  - 그래서 브라우저는 HTML 문자열을 다루기 쉬운 DOM Tree로 변환한다.
  - 결론적으로 브라우저는 DOM Tree를 다루어 화면에 내용을 출력한다.
- 비교할 예 - React
  - JavaScript 입장에서 DOM을 직접 다루는 것은 까다롭다.
  - 그래서 JavaScript(React)는 다루기 쉬운 VDOM을 다룬다.
  - VDOM은 DOM도 잘 알고 있고 JavaScript도 잘 알고 있어서 복잡도를 다룰 수 있는 구조가 된다.
  - 더 나아가 사용하기 쉽도록 JSX를 제공한다.
    - HTML 마크업 하듯 자바스크립트를 다룰 수 있게 되었다.
    - VDOM이 있기 때문에 'React Native'도 가능하다.
    
### 간단한 WebApp을 React를 이용해 구현

- 기본적으로 이름을 부여할 수 있다는 것은 굉장히 좋은 것이다.
  - 컴포넌트 이름만 잘 지어도 가독성이 높아진다. 즉, 수정하기 쉬워진다.

```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';

// 이름을 부여할 수 있다.
function StudyList() {
  return (
    <ul>
      <li className="item">React</li>
      <li className="item">Redux</li>
      <li className="item">TypeScript</li>
    </ul>
  )
}

function App() {
  // babel로 확인해보면 결국 함수 호출이다.
  // React.createElement는 VDOM을 만든다.
  return (
    <div>
      <h1>Hello</h1>
      <StudyList />
    </div>
  )
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### React 만들기

> [참고](https://gist.github.com/ibare/c736f63fba835c172e60aa98a996dada)

- React의 사상을 이해하는데 문제가 없을 정도의 핵심적인 부분들만 구현해 보는 것이다.
  - 이러한 사상을 이해하게 되면 '이 부분은 이렇게 써야겠구나' 혹은 '구조적으로 이렇게 때문에 이렇게 써야되는 구나'를 알게된다.
  - 예) Hook은 왜 이렇게 써야하지?

#### 1. JSX 처리

- 개발자들은 편리하고 사용하기 쉬운 것을 좋아하기 때문에 React 팀은 'jsx'를 만들었다.
- jsx를 구현하기에는 시간이 많이 걸릴 것 같다.
- 사실 babel이 해준다.
  - JavaScript는 기본적으로 컴파일 타임이 없었다.
  - 트랜스파일링을 꼭 필요로 하는 요즘 시대에는 스크립트 언어임에도 컴파일 타임이라는 새로운 레이어가 생겨났다.
  - 즉, JavaScirpt 코드를 작성할 때 컴파일 타임과 런타임을 잘 구분해야한다.

#### 2. VDOM

- 태그를 어떻게 표현할까?
  - JavaScript에서 다루기 쉬운 구조: 객체
  
```JavaScript
// VDOM은 이렇게 생겼을 것이다.
// 제일 상위에 단 하나의 부모 요소만 있을 수 밖에 없는 구조다.
const vdom = {
  type: 'ul',
  props: {},
  children: [
    { type: 'li', props: { className: ''item' }, children: 'React' },
    { type: 'li', props: { className: ''item' }, children: 'Redux' },
    { type: 'li', props: { className: ''item' }, children: 'TypeScript' },
  ],
};
```

#### 3. VDOM을 만드는 함수 `createElement()`

- type에 function이 들어가는 경우가 있다.
- babel이 트랜스파일링할 때 소문자로 되어 있는 값은 type에 문자열로 넣어주는데 대문자로 되어 있는 값은 처리 방식이 다르다.
  - 사용자 컴포넌트는 무조건 대문자로 시작해야 하는 이유다.
  - 즉, 대/소문자로 사용자 컴포넌트인지 아닌지를 구분하는 것이다. (굉장히 심플한 아이디어)
> 복잡해 보이는 것도 실은 간단한 아이디어인 경우가 많다.

```JavaScript
/* @jsx createElement */
// 실제로 트랜스파일링 될 메서드 명을 임의로 바꿀 수 있다.
// 바벨 리액트 플러그인에 다 나와 있다.
// 공식문서가 굉장히 중요하다.

// VDOM을 만드는 애
function createElement(type, props = {}, ...children) {
  if (typeof type === 'function') {
    return type.apply(null, [props, ...children]);
  }

  return { type, props, children }
}

const vdom = createElement('ul', {}, createElement('li', {}, 'React'));

console.log(vdom);
```

#### 4. render 함수

- 최상위 루트 컴포넌트가 객체로 변환된 것을 Real DOM으로 converting 하는 함수

```JavaScript
/* @jsx createElement */

// 재귀다.
// node는 트리며 마지막 노드가 어디에 위치했는지 알 수 없다.
// 그런데, 부모와 자식의 형태가 갖다.
// 자연스럽게 재귀가 될 수 밖에 없다.
function renderElement(node) {
  // 가장 하위 요소들의 children은 string일 수 밖에 없다.
  if (typeof node === "string") {
    return document.createTextNode(node);
  }

  const el = document.createElement(node.type);

  node.children.map(renderElement).forEach((element) => {
    el.appendChild(element);
  });

  return el;
}

function render(node, container) {
  container.appendChild(renderElement(node));
}
```

#### 5. 완성

- 실제로는 기존 VDOM과 새로운 VDOM의 diff를 해야한다.
- 오픈소스를 리딩할 때 요령
  - 규모가 있는 상태에서 리딩하는 것은 어렵다.
    - 어디서부터 시작해야 하는지 확인하는 것도 쉽지 않다.
    - 방어 로직이 굉장히 많기 때문에 핵심 로직을 찾기 힘들다.
  - GihHub에서 초기 릴리즈 커밋을 찾은 뒤에 리딩한다.
    - 기본 컨셉은 동일하다.
    - 그 후 depth를 한 단계, 한 단계 늘려나간다.

```JavaScript
/* @jsx createElement */

function renderElement(node) {
  if (typeof node === "string") {
    return document.createTextNode(node);
  }

  const el = document.createElement(node.type);

  node.children.map(renderElement).forEach((element) => {
    el.appendChild(element);
  });

  return el;
}

function render(node, container) {
  let previousNode;

  // node vs previousNode 비교
  /*
    ...
  */
  container.appendChild(renderElement(node));
}

function createElement(type, props = {}, ...children) {
  if (typeof type === "function") {
    return type.apply(null, [props, ...children]);
  }

  return { type, props, children };
}

function Row(props) {
  return <li>{props.label}</li>;
}

function StudyList() {
  return (
    <ul>
      <Row label="React" />
      <Row label="Redux" />
      <Row label="TypeScript" />
      <Row label="mobx" />
    </ul>
  );
}

function App() {
  return (
    <div>
      <h1>Hello</h1>
      <StudyList />
    </div>
  );
}

console.log(<App />);

render(<App />, document.getElementById("root"));
```

### 상태와 Hook

#### 컴포넌트를 선언하는 방법의 역사

1. Class 컴포넌트
  - Class는 호출이 없다.
  - `const hello = new Hello()`는 호출이 일어난 것이 아니다.
  - 그러므로 자연스럽게 constructor와 render 함수가 필요하다.

```JavaScript
import React from "react";

class Hello extends React.Component {
  // 자연스럽게 constructor를 정의할 수 밖에 없는 구조
  constructor(props) {
    super(props);
  }

  // render 함수는 반드시 구현되어야 하는 함수다.
  // React 컴포넌트는 jsx가 있어야 한다. 왜? createElement를 호출하기 때문에
  render() {
    return <p>안녕하세요!</p>;
  }
}
```

2. Function 컴포넌트

```JavaScript
function App() {
  return (
    <div>
      <h1>상태</h1>
      <Hello />
    </div>
  );
}
```

- 리액트 초기에는 자체 상태를 갖는다면 Class 컴포넌트로 만들고, 외부 상태를 받아 그리기만 한다면 함수형 컴포넌트로 만드는 것이 일종의 컨벤션이었다.
  - 함수형 컴포넌트에 변수를 넣으면 호출될 때 마다 매번 초기화되기 때문에 상태를 가질 수 없었다.

#### Hook

- Hook은 함수형 컴포넌트에서 상태를 가질 수 있도록 도와주는 Spec이다.

```JavaScript
function App() {
  // useState()는 배열을 반환하고 보통 이것을 destructuring 해서 사용한다.
  const [counter, setCounter] = useState(1);

  return (
    <div>
      <h1>상태 {counter}</h1>
      <button onClick={() => setCounter(counter + 1)}>+</button>
      <Hello />
    </div>
  );
}
```

- 어떻게 이 동작이 가능한 것일까?

1. 첫 번째 가정
- 버튼을 클릭하면 상태가 바뀌고 App 함수를 호출했을 것이다.
- 즉, React가 counter 값이 바뀐 것을 알고 있다.
- setCounter가 React에서 만들어서 준 것이니 이 것을 호출하면 상태가 바뀌었다고 인지하는게 아닐까?

2. 두 번째 가정
- setCounter가 호출되고 App이 다시 렌더링 되는 것은 알겠다. 그런데, 어떻게 counter의 값이 1로 초기화 되지 않고 1, 2, 3... 이렇게 증가하고 있는 것일까?
- 이것은 이전의 값을 기억하고 있다는 것인데....

#### Hook 메커니즘

생각보다 굉장히 심플한 방식이다.
- React가 컴포넌트를 하나하나 만들 때마다 createElement가 호출된다.
- 이 때, createElement의 첫 번째 인자가 string이 아닌 function이면 현재 컴포넌트가 사용자 컴포넌트임을 알 수 있다.
- 함수안에 Hook이 있다면 전역 공간에 있는 Hook 배열에 Hook을 초기값과 함께 저장한다.
- 다음번 렌더링 때 전역 Hoook 배열에 Hook이 저장되어 있다면 초기값을 무시한다.
  - 그래서 React 공식 문서 '[Hook의 규칙](https://ko.reactjs.org/docs/hooks-rules.html)'을 보면 '반복문, 조건문, 중첩된 함수' 내에서 Hook을 호출하지 말라고 한다.
  - 컴포넌트가 렌더링 되는 순서대로 인덱싱 한 뒤 전역 배열로 관리하고 있는데, 조건문에서 Hook을 쓴다면 인덱싱이 깨지기 때문이다.
  - 또한, 리액트 컴포넌트로 인덱스를 잡기 때문에 다른 곳에서 Hook을 사용하면 동작하지 않는다.
