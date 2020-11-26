# 우아한테크러닝 3기 - 5. 

## 학습 목표

- 리덕스 미들웨어

## 미들웨어

- Redux의 모든 동작은 동기적이다.
  - 순서가 완전히 보장된다.
  - 그렇기 때문에 Reducer는 순수 함수여야 한다.

### 순수 함수

- 입력이 동일하면 출력이 동일하다.
- 함수 외부 상태에 의존하지 않는다.
- 부수효과(부작용, Side Effect)가 없다.

> 참고: 멱등성

### 순수하지 않은 작업?

- 실행할 때 마다 결과가 달라지는 작업
  - 대표적으로 비동기 작업
  - 대표적인 것이 API 호출
    - 호출할 때 마다 결과가 다르다.
    - 에러가 발생 할 수도 있고, 정상 결과를 받을 수도 있고, 결과가 호출 때 마다 다를 수 있고...

### Redux에서 순수하지 않은 작업을 어떻게 다룰까?

- Redux만으로는 불가능하다.
  - reducer가 순수 함수이기 때문이다.
- Side Effect이 발생하는 작업은 Redux 밖에서 해야한다.
  - 대신, '미들웨어'라는 것을 제공해서 연동할 수 있게 해준다.
  
### Redux 미들웨어 

- 코드를 감싸는 방법은 함수 밖에 없다.
- 코드를 직접 수정하는 것은 비싼 비용이 든다.
  - 코드 수정 > 재배포 > QA > 버그가 있다면...
- 몽키패치: 실행중인 코드를 런타임 환경에서 변경하는 것
> 참고: http://egloos.zum.com/pascaldice/v/1161316
  - 예시
    - store.dispatch를 next에 저장한다.
    - store의 dispatch를 새로운 함수로 변경한다.
      - 즉, 실행시간에 dispatch를 새로운 함수로 바꿨다.
  - 무엇이 장점일까?
    - 소프트웨어에서 하나였던 것이 두개가 될 때 굉장히 많이 바뀐다.
    - 두개가 된다는 것은 3개, 4개, 5개...가 될 수 있기 때문이다.
    
### 확장의 두 가지 패러다임

- 플러그인
- 미들웨어

#### 미들웨어

- 데이터가 흘러가는 흐름에 여러가지 처리기를 두고 흘러가는 데이터는 모든 처리기를 통과하도록 구성하는 것
- 처리기가 중간중간에 놓여있다고 해서 미들웨어라고 부른다.
- 플러그인과는 다르게 모든 데이터가 각각의 미들웨어들을 거친다.
  - 플러그인은 어떤 경우에서는 사용하고 그렇지 않은 경우에는 사용하지 않는다.
- Redux에서는 액션이 흐른다.
- 미들웨어는 데이터 흐름 사이에 놓이게 되므로 순서가 영향을 미친다.
  - 즉, 미들웨어의 적용 순서가 중요할 때가 있다.

```javascript
import { createStore } from "./redux";

function api(url, cb) {
  setTimeout(() => {
    cb({ type: "응답이야", data: [] });
  }, 2000);
}

function reducer(state = { counter: 0 }, action) {
  switch (action.type) {
    case "inc":
      return {
        ...state,
        counter: state.counter + 1
      };
    case "fetch-user":
      api("/api/v1/users/1", (users) => {
        // 클로저에 잡혀있긴 하지만
        // 2초 동안 상태가 바뀌었다.
        return { ...state, ...users };
      });
      // redux한테 reducer가 반환할 상태가 없다.
      break;
    default:
      return { ...state };
  }
}

// const store = createStore(reducer);

// myMiddleware과 yourMiddleware는 문법만 다르고 똑같다.
// ourMiddleware는 중첩되지 않은 하나의 함수다.
// myMiddleware, yourMiddleware, ourMiddleware는 모두 실행하는 코드가 같다.
// 다른 점은 인자가 3개인 것과 인자 각각을 받는 함수로 구성되어 있다는 것 이다.
// 이게 실행가능한 이유는 클로저라는 개념이 있기 때문이다.
// 인자가 N개인 함수를 인자가 각각 하나씩 갖는 함수로 쪼개는 기법을 커링이라고 한다.
// 작동은 똑같은데 왜 커링을 써서 쪼개는 것일까?

// 미들웨어는 이렇게 만든다.
const myMiddleware = (store) => (dispatch) => (action) => {
  dispatch(action);
};

// 일반적인 함수로 쓰면
function yourMiddleware(store) {
  return function (dispatch) {
    return function (action) {
      dispatch(action);
    };
  };
}

function ourMiddleware(store, dispatch, action) {
  dispatch(action);
}

// 어떤 액션이 들어 왔을 때 데이터 말고 타입이 뭐가 들어 왔는지 로그를 찍고 싶다.
myMiddleware(store)(store.dispatch)({ type: "inc" });
ourMiddleware(store, store.dispatch, { type: "inc" });

store.dispatch({
  type: "inc"
});

store.dispatch({
  type: "fetch-user"
});

// 항상 제작자가 있고 사용하는 사람이 있다.
// 첫 번째 함수는 사용자가 최종 계산에 개입할 여지가 없다.
// 즉, 인자를 입력하고 함수가 연산하는 과정에서 함수를 호출하는 사용자 쪽에서는 연산 과정 중간에 개입할 수 없다.
const add1 = function (a, b) {
  return a + b;
};

// 두 번째 함수는 사용자가 최종 계산에 개입할 여지가 있다.
// 즉, 사용자 쪽에서 몽키 패칭을 할 수 있는 구조
// 미들웨어의 제작자는 자신이 작성한 함수를 리덕스가 조작할 수 있도록 만들어 주는 것이다.
// 인자를 커링하여 store, next, action을 쪼갠 이유는 리덕스가 미들웨어를 순서대로 실행시킬 수 있도록 열어놓은 구조다.
const add2 = function (a) {
  return function (b) {
    return a + b;
  };
};

add1(10, 20);
add2(10)(20);

const next = add2(10);
let t = 0;
// do some....
t = 30;
next(3);

// 완성된 미들웨어
const logger = (store) => (next) => (action) => {
  console.log("logger: ", action.type);
  next(action);
};

const monitor = (store) => (next) => (action) => {
  setTimeout(() => {
    console.log("monitor: ", action.type);
    next(action);
  }, 2000);
};

const store = createStore(reducer, [logger, monitor]);

store.subscribe(() => {
  console.log(store.getState());
});
```
