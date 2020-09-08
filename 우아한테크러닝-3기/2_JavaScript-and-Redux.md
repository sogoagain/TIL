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
