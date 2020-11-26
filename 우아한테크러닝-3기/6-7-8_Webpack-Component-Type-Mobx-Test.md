# 우아한테크러닝 3기 - 6, 7, 8. 웹팩, 컴포넌트, 인터페이스 vs 타입, Mobx, 테스트

## 학습 목표

- 웹팩
- 컴포넌트
- 인터페이스 vs 타입
- Mobx

## 웹팩

- 웹팩의 생태계는 굉장히 거대하다.
  - 그러나, 웹팩 자체가 해주는 일은 많지는 않다.
  - 플랫폼 같은 느낌
- 웹팩은 빌드할 때 Node.js에서 돌아간다.
- 설정파일: `webpack.config.js` (관례)
- 웹팩 플랫폼에 입주하기 위한 가이드
  - [Writer's Guide | webpack](https://webpack.js.org/contribute/writers-guide/)

### Loader

- 전처리
- 미들웨어에 해당한다.
- 웹팩은 프론트엔드 소스파일을 기준으로 빌드한다.
  - 첫 번째 파일부터 시작해서 그 파일이 읽어들이는 것들을 계속 불러들이며 코드를 merge 한다.
- input과 output의 스펙만 알면 Loader를 작성할 수 있다.
- `test` 키워드로 어떤 파일을 받을 것인지, 뺄 것인지 기술할 수 있다.

### Plugin

- 후처리
- 로더보다 복잡하다.
- 웹팩 안쪽에 있는 로우레벨의 기능들을 노출시킨다.
- 보통의 플러그인은 로더가 실행된 뒤 결과물을 받아서 작업한다.

## 컴포넌트

- 상태를 갖는 컴포넌트와 상태가 없는 컴포넌트를 분리
  - Container 컴포넌트: 비즈니스 로직과 관련된 컴포넌트
  - 컴포넌트: 비즈니스 로직이 없고 props로 데이터를 받아서 렌더링 하는 컴포넌트
    - 내부적으로 state를 가질 수 있지만 외부와 관계를 맺는 state인 것인지가 중요
- Page 안에 Flow, Flow 안에 Container, Container 안에 Component
- 어느 시점에 분리할 것인가?
  - 타이밍은 App마다, 규모마다, 다루는 로직의 복잡도마다 다르다.
  - 처음부터 너무 잘게 쪼개는 것보다 적정 수준을 고려하는 것이 좋다.
  
## 인터페이스 vs 타입

### type alias

```typescript
type Person = {
	name: string;
	age: number;
	job?: [];
}
```

### interface

```typescript
interface Human {
	name: string;
	age: number;
	job?: [];
}
```

- Spec을 확인하면 두 개가 굉장히 유사하다.
- interface는 상속을 지원하고 유니언 타입을 지원하지 않는다.

### Union Types

```typescript
type box = number | string;

const b: box = 10;

b = '10';
```

### 그럼 무엇을 사용해야 할까?

- type을 쓰면 유니언 타입을 지원하니까 편하지 않을까?
- 인터페이스 이름을 보면 소통의 의미를 내포하고 있다.
  - A라는 컴포넌트가 B라는 컴포넌트와 소통
  - 모든 인터페이스는 public이다.
  - 보통 Props는 인터페이스로 규격을 만들고 내부의 데이터는 type을 사용한다.
- 리액트의 class는 OOP를 구성하기 위한 것이 아니다.
  - 컴포넌트 라이프사이클을 만들기 위한 도구에 지나지 않는다.
  - 단 한번도 new를 앱 개발자가 사용하지 않는다. (리액트에서 호출하므로...)
  
## Mobx

- 리액트 디펜던시가 없는 라이브러리
- 보통 리액트 환경에서 잘 사용할 수 있도록 Wrapper 라이브러리가 존재한다.
  - mobx-react.js.org
- 리덕스와 달리 Mobx는 상태를 개별로 여러개 만들 수 있다.
- observable로 감쌀 수 있는 것은 객체다.
  - primitive 값을 지원하지 않는다. 즉, box 함수를 사용해야 한다.
  - 값을 가져오거나 변경할 때 get, set 함수를 이용한다.
- 변경 단위를 묶어주는 함수: action

```javascript
const weight = observable.box(82);
weight.set(weight.get() - 1);
```

## 테스트

- 테스트는 크게 보면 E2E 테스트와 Unit 테스트가 있다.
- 테스트는 성공하는 테스트와 실패하는 테스트 두 개를 써야 한다.
  - 테스트 자체가 functional 한 것이다.
  - 성공하는 것은 항상 성공하게 만들고,
  - 실패하는 것은 항상 실패하게 만드는 것.
  - Side Effect에서 격리되어야 한다.
