# 우아한테크러닝 3기 - 2. JavaScript & Redux

## 학습 목표

- JavaScript A to Z
- Redux 구현

## JavaScript

### '식', '문'

- 모든 JavaScript 코드는 '식'과 '문'으로 나눌 수 있다.

#### 식

- 한 줄 실행했을 때 실행의 결과가 값으로 남으면 식이다.
  - 식은 세미콜런으로 마무리 된다.

```JavaScript
0;
1 + 10;
foo();
1 + 10 + foo();
```

#### 문

- 실행 했을 때 값이 나오지 않으면 문이다.
  - 문은 끝에 세미콜런을 붙이지 않는다.
  - 예: 조건문, 반복문, 함수선언문 등

```JavaScript
if () {}
while () {}
```


### 변수

- JavaScript는 Primitive type을 제외하고 모든 것이 객체다.
> 프로그래밍 언어 기저에는 서양의 철학이 담겨 있다.
> 맨 밑부터 변하지 않는 원칙을 정해놓고 하나씩 쌓아 나가는 방식이다.
> 그렇기 때문에 아무리 복잡한 것이라도 그 원칙으로 한 꺼풀씩 벗겨 나가면 배울 수 있고 이해할 수 있다.

```JavaScript
// 변수에는 값을 넣을 수 있어 (원칙)
var x = 10;
let y = 10;
const z = 10;

// 변수에는 JavaScript에서 값이라고 취급하는 녀석을 넣을 수 있다.
let foo = {
  a: 'a',
}

// JavaScript에서는 함수도 값으로 취급한다.
// 즉, 변수에는 함수도 넣을 수 있다.
function bar() {
  // ...
}

let baz = bar;
```

- JavaScript에서는 거의 모든 것이 값이다.

### 함수

#### 함수 정의

- JavaScript의 함수는 반드시 값을 반환한다.
  - `return`문이 없으면 `undefined`를 반환하고,
  - `return`문으로 값을 반환한다.
  - `new` 연산자는 명시적 표현이 없어도 객체를 반환한다.

##### 함수 선언

```JavaScript
// 함수 선언은 끝에 세미콜런이 없다.
function foo() {
  return 0;
}
```

##### 함수 표현식

- JavaScript 함수가 재밌고 유연한 점이다.

```JavaScript
// 여기서 함수는 값이다. 그렇기 때문에 세미콜런이 붙는다.
const foo = function foo() {
};

// 이 foo는 const로 선언된 foo다.
foo();

// 함수의 이름이 아닌 const로 선언된 변수를 이용해 함수를 호출할 수 있으므로,
// 함수를 값으로 취급할 때 이름을 생략할 수 있다.
const bar = function() {};

// 변수를 읽으면 값이고,
// 변수가 등장하는 위치가 값이 등장하는 위치다.
// 그래서, 아래의 구문은 값으로 취급한 것이라 볼 수 없다.
// 이 때는 에러가 난다.
function() {};

// 단, 값으로 취급하게 되면 에러가 나지 않는다.
// 위 경우 함수를 즉시 호출하는 것 외에는 호출할 수 없다.
// 프로그래밍에서 단 한 번만 호출되는 함수가 필요할 때 많이 사용한다.
(function() {})();
```

#### 고차 함수 (Higher-order function)

- 하나 이상의 함수를 인자로 받는다.
- 함수를 결과로 반환한다.

> 형태에 익숙해지는 것이 중요하다. 사람은 형태가 익숙하지 않으면 낯설어한다.

```JavaScript
// 함수는 인자에 값이 위치하고, 리턴할 때도 값이 위치한다.
function foo(x) {
  x();
  
  // 함수도 값이므로 함수를 리턴할 수 있다.
  // 이를 이용해 함수를 합성할 수 있다.
  return function() {
  };
}

// 함수도 값이므로 인자로 함수를 전달할 수 있다.
// 이런 함수를 보통 Callback 함수라고 한다.
const bar = foo(function() {});
```

#### 그 외 여러가지 함수의 형태

- 함수 표현식에서 재귀 호출

```JavaScript
// 함수 표현식에서 재귀 호출을 하기 위해서는
const foo = function foo() {
  // 함수 이름이 필요하다.
  // 여기서 foo는 const로 선언된 foo가 아닌 함수 foo다.
  foo();
}
```

- 익명 함수

```JavaScript
// 재귀 호출이 아닌 상황에서는 함수 이름을 생략할 수 있다. (익명 함수)
const foo = function(x) {
  return x * 2;
}
```

- Arrow function expression
  - Arrow function은 이름이 없기 때문에 재귀 호출을 할 수 없다.

```JavaScript
// 함수는 어떤 상황에서도 값을 반환한다. (undefined 포함)
// Arrow function을 이용해 한 줄로 함수를 표현할 수 있다. (람다식으로 불리기도 한다.)
const foo = (x) => x * 2;

// 화살표 함수의 여러 형태
const i = () => 10;
const j = (x, y) => x * y;
const k = (x, y) => {
  return x * 2;
}
```

### new 연산자와 생성자 함수

#### new 연산자를 써서 함수를 실행했을 때 메커니즘

1. 빈 객체를 만든다.
2. 빈 객체를 this에 할당한다.
3. 함수 본문을 실행 하면서 this에 값을 동적으로 바인딩 한다.
4. 명시적으로 return이 없어도 this를 반환한다.

#### 왜 필요할까?

- 일종의 위임이다.
  - 어떤 로직에서 특정 모양의 객체가 필요하다고 생각해보자. 그럼, 해당 로직에서는 객체의 모양을 검사할 필요가 있다.
  - JavaScript는 타입이 느슨하기 때문에 객체라면 타입 검사가 더 피곤하다.
  - 객체를 온전하게 만들 수 있는 인증된 함수를 하나 만들고 대상 객체가 이 함수의 인스턴스라는 것을 검사하면 기존의 타입 검사를 어느정도 위임할 수 있다.

```JavaScript
// 생성자 함수(constructor function)라고 부른다.
function foo() {
  this.bar = 10;
}

// new 연산자를 이용해 인스턴스 객체를 생성한다.
const x = new foo();

// 타입 검사를 어느정도 위임할 수 있다.
console.log(x instanceof foo);
```

### 클래스

- new 연산자를 명시화 한 것
- 함수와 차이점
  - constructor가 명확하게 드러나있다.
  - 함수는 new 연산자 없이 호출할 수 있어 new 연산자 사용을 강제할 수 없다.
    - 그래서 생성자 함수는 이름을 대문자로 시작하자는 약속을 정한다.
  - 클래스로 만들면 new 연산자 사용을 강제할 수 있다.

```JavaScript
class foo {
  constructor() {
    this.bar = 10;
  }
}
```

### this

- 실행 컨텍스트
- 실행하는 순간 맥락상 소유자(누가 호출했는지)를 확인한다.
  - 예를들어 `person.getName()`에서는 `person`이 소유자다.
  - 이 것이 실행 컨텍스트다.
- 그런데, 소유자가 벗겨지는(사라지는) 순간들이 있는데 이 점 때문에 복잡해진다.

```JavaScript
const person = {
  name: '홍길동',
  getName() {
    return this.name;
  }
}

// '홍길동' 출력
// 실행 컨텍스트를 쉽게 파악할 수 있다.
console.log(person.getName());

const man = person.getName;

// 에러 발생
// '홍길동'이 출력되지 않는다.
// 이유? 실행하는 순간 호출자가 없다. 즉, 호출자를 확인할 수 없다.
// 호출자가 없으면 전역 객체(window)에 바인딩 된다.
// window 객체에 name이 없기 때문에 에러가 발생한다.
console.log(man());

// man과 동일한 현상이 발생한다.
// 소유자가 벗겨지는 경우.
// 굉장히 자주 발생하는 경우다.
button.addEventListener('click', person.getName);

// 이럴 때 this를 고정하고 싶어지는데,
// 헬퍼 함수인 bind를 이용한다.
button.addEventListener('click', person.getName.bind(person));
```

- 헬퍼 함수인 call, apply를 이용해서도 this 값을 설정할 수 있다.
  - 함수를 호출하는 3가지 방법

```JavaScript
getName.call(person, 'foo');
getName.apply(person, ['boo']);
person.getName('baz');
```

### 이벤트 시스템

- JavaScript 뿐만 아니라 UI 개발은 어떤 플랫폼이던지 대부분 실행을 적시할 수 없다.
- 그렇기 때문에 이벤트 시스템을 활용한다.
  - 브라우저가 제공하는 이벤트 시스템에 'save 버튼이 클릭되면 실행할 함수 하나 줄테니 대신 실행해줘'라고 알려준다. (callback)

### 클로저 (Closure)

- 함수가 호출되면 스코프가 생긴다.
- 아래에서 `foo` 함수를 실행하면 스코프가 생기고 `bar`는 그 스코프에 포함된다.

```JavaScript
function foo(x) {
  return function bar() {
    return x;
  }
}

const f = foo(10);

// 10이 출력됨
console.log(f);
```

- 그런데, `bar`가 자신의 스코프 체인 밖의 변수인 `x`의 값을 들고 있다.
  - 이것이 '클로저'다.
  - `x`는 오직 `bar`만이 접근할 수 있다. (`bar`만이 저장하고 있기 때문에)

#### 클로저의 활용

```JavaScript
const person = {
  age: 10,
}

// 이러한 상황을 막고 싶다.
person.age = 500;

// 옛날 JavaScript 개발자들은...
function makePerson() {
  let age = 10;

  return {
    getAge() {
      return age;
    },
    setAge(x) {
      age = x > 1 && x < 130 ? x : age;
    },
  }
}

let p = makePerson();

console.log(p.getAge());
```

- return에 포함된 함수가 만들어지는 순간 `age`가 함수 스코프 밖에 있으니 클로저가 이를 캡처한다. 따라서, 리턴된 함수로만 접근할 수 있는 값이 된다.
- 보호하고 싶은 값이 있을 때 많이 사용했다.

### 비동기

- 인간의 두뇌가 동기적으로 생각하기 때문에 비동기를 이해하기는 어렵다.
  - 실행의 흐름이 도대체 어떻게 되는 것이지?
- 비동기적인 코드를 동기적으로 만들기 위해 많은 노력을 했다.
  - 똑똑한 사람들 '어려워? 그럼 쉽게 만들어 보자'

- Callback hell
```JavaScript
setTimeout(function (x) {
  console.log('앗싸');
  setTimeout(function (y) {
    console.log('웃싸');
  }, 2000);
}, 5000);
```

#### Promise

- 좋은 기술이지만 쉽지는 않다.

```JavaScript
const p1 = new Promise((resolve, reject) => {
  // 여기서 resolve를 호출하는 것도 클로저다.
  setTimeout(() => {
    // resolve를 호출하면 then으로 넘겨준 함수를 호출한다.
    resolve('응답');
  }, 1000);

  // reject를 호출하면 catch로 넘겨준 함수를 호출한다.
  reject();
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('응답2');
  }, 2000);
});

// p1 인스턴스 객체 안에는 then 메서드가 들어있다.
// Promise로 인스턴스를 생성하는 코드와 then을 호출하는 코드가 떨어져 있다. (사용하기 어려운 이유 중 하나)
// 응답을 받을 callback을 넘겨준다.
p1
  .then(p2
      .then(function(r) {
        console.log(r);
        }))
  .catch(function () {});
```

#### async, await

- Promise의 복잡성을 제어하고자 async, await가 새롭게 나왔다.
- Promise 세대를 지나 async, await 세계로 오면서 비동기 로직에서 try-catch 구문이 유용하게 되었다.
  - 이전까지는 콜백 에러를 try-catch가 잡지 못했다.

```JavaScript
const delay = ms => new Promise(resolve => setTimeout(resolve, ms));

async function main() {
  console.log(1);
  try {
    await delay(2000);
  } catch(e) {
    console.error(e);
  }
  console.log(2);
}

main();
```

### 커링

- 인자를 나누는 것

```JavaScript
function foo(a, b, c) {
}

function foo(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    }
  }
}
```

- 참고하기 좋은 문서
  1. [자바스크립트의 함수](https://medium.com/ibare-story/e252506f8525)
  2. [프로그래밍 — 단순한 기능, 기능의 결합, 의미의 부여](https://medium.com/ibare-story/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EB%8B%A8%EC%88%9C%ED%95%9C-%EA%B8%B0%EB%8A%A5-%EA%B8%B0%EB%8A%A5%EC%9D%98-%EA%B2%B0%ED%95%A9-%EC%9D%98%EB%AF%B8%EC%9D%98-%EB%B6%80%EC%97%AC-1d4ab9d59415)
  3. [Javascript Boot Camp](https://fastcampus-js-bootcamp.herokuapp.com/)
  
## Flux Architecture

- Application은 수많은 UI 요소(컴포넌트)가 중첩되어 구성된다.
  - 각 UI 요소에서는 데이터들이 사용되는데, 특정 데이터들은 여러 컴포넌트에서 공유되는 상황이 발생한다.
- Flux Architecture의 컨셉
  - Application에서 사용되는 모든 상태를 하나의 store에 모아놓고, 이 상태들을 모든 컴포넌트에 내리자
  - 각 컴포넌트들은 흘러가는 데이터 중 필요한 것만 뽑아서 사용하면 되지 않을까?

### 기존에 이러한 개념이 불가능 했던 이유
- 상태를 나타내는 데이터가 500개 정도 있다고 가정하자.
- 이 중 하나의 데이터만 바뀌어도 모든 UI 요소들을 다시 그려야 한다.
- 화면이 전체적으로 깜빡거린다.
- 일부분만 변경하려면 모든 UI 요소가 주기적으로 관심있는 데이터가 바뀌었는지 확인해야 한다.
  
### 이제는 가능한 이유
- React가 Virtual DOM이라는 개념을 들고 나왔다.
  - 기존에는 DOM에 직접 접근해서 UI를 변경했는데, 이제는 React가 VDOM을 만들고 이 VDOM을 DOM으로 연결한다.
  - 즉, JSX > VDOM > DOM
  - 상태가 변경되면 변경된 상태에 해당하는 새로운 VDOM(version 2)를 만들고 기존 VDOM(version 1)과 비교하여 다른 부분만 실제 DOM에 반영한다.
  - 이런 컨셉으로 미친듯한 깜빡임을 발생하지 않도록 하며 속도도 굉장히 빠르다. (React에서 VDOM의 diff연산이 굉장히 좋은 알고리즘으로 구현되었다고 광고한다.)
- 또한, Redux가 나오면서 Flux Architecture를 쉽게 구성할 수 있도록 도와줘서 큰 히트를 쳤다.

### Redux 만들어보기

- Redux는 `Pub/Sub model`이다.
  - React와 상관 없다.
  - 상태가 변경되었을 때 알람을 받고 싶으면 구독(subscribe)해. 그럼 상태가 변경되었을 때 알려줄게(publish)

#### redux.js

- 하나의 Application은 하나의 store를 갖는다.
  - store는 객체다.
- 제공해야하는 기능
  1. store(객체)를 만드는 함수를 제공한다 - `createStore()`
  2. store가 생성되면 action을 호출할 수 있는 함수를 제공한다. - `dispatch()`
  3. store가 변경 통보를 구독할 수 있는 함수를 제공한다. - `subscribe()`
- state는 어떻게 바꿀 수 있을까?
  - Application 개발자가 만들어 주어야 한다.
  - 만일, 컴포넌트가 store(객체)의 상태를 직접 바꾸면 어떻게 될까?
  - 다른 컴포넌트가 바뀐 것을 통보 받는데 문제가 생긴다.
  - 그래서 store를 생성할 때 제공해주는 dispatch를 이용해 Redux에서 상태를 변경할 수 있도록 한다.
  - Application 개발자는 상황에 맞게 변경된 상태를 반환하는 `reducer`를 작성한다.
  - `reducer`를 호출할 때 현재 상태를 전달한다.
  - 그런데, 어떤 상태를 바꿔야할까? 이는 액션 타입을 이용해 나타낸다.
- state는 immutable 해야한다.
  - Redux 개발자는 Application 개발자에게 reducer에서 새로은 state를 return 할 때는 항상 새로운 객체로 만들어서 return 하라고 애절하게 부탁한다.
  - 그래야 state가 변경되었는지 확인 할 수 있기 때문이다.

```JavaScript
export function createStore(reducer) {
  // 클로저로 상태를 숨긴다.
  let state;
  const listeners = [];
  
  const getState = () => ({...state});
  
  // dispatch를 제공함으로써 컴포넌트에서 action을 호출할 수 있다.
  const dispatch = (action) => {
    state = reducer(state, action);
    // state가 변경되었으므로 publish한다.
    listeners.forEach(fn => fn());
  }
  
  // subscribe 할 수 있는 방법을 제공한다.
  const subscribe = (fn) => {
    listeners.push(fn);
  }
  
  return {
    getState,
    dispatch,
    subscribe,
  }
}
```

#### index.js

```JavaScript
import { createStore } from './redux.js';

// 액션을 상수로 선언한 것을 액션 타입이라고 부른다.
const INCREMENT = 'increment';
const RESET = 'reset';

function reducer(state = {}, action) {
  if (action.type === INCREMENT) {
    return {
      ...state,
      count: state.count ? state.count + 1: 1,
    }
  } else if (action.type === RESET) {
    return {
      ...state,
      count: action.resetCount,
    }
  }
  return state;
}

function actionCreator(type, data) {
  return {
    ...data,
    type: type,
  }
}

function increment() {
  store.dispatch(actionCreator(INCREMENT));
}

function reset() {
  store.dispatch(actionCreator(RESET, { resetCount: 10 }));
}

const store = createStore(reducer);

// 이 함수가 호출되면 reducer의 store가 바뀌었다는 뜻이다.
function update() {
  console.log(store.getState());
}

store.subscribe(update);

increment();

console.log(store.getState());
```

> [참고](https://gist.github.com/ibare/1ed63de0c09c94a7ac79713d57b80f8d)
