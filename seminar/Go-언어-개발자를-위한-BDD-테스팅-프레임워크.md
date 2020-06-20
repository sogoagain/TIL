# [수요지식회] Ginkgo - Go 언어 개발자를 위한 BDD 테스팅 프레임워크

- 발표자: '코딩의 신 아샬'님
- 영상 링크: [[수요지식회] Ginkgo - Go 언어 개발자를 위한 BDD 테스팅 프레임워크](https://youtu.be/gfTsSBRvdqI)

## Ginkgo

- A Golang BDD Testing Framework

## BDD

- Behavior-Driven Development
- TDD(Test-Driven Development)의 한 갈래

## TDD

- Test First
- Red Green Refactor 사이클
- 설계를 개선하고 코드를 개선한다.
- 실패하는 테스트를 만드는 것을 어려워한다.
- '무엇을 작성해야할까?'

### 실패하는 테스트 코드를 작성하기 어려운 이유

- 테스팅을 단지 버그를 찾는 행위로 생각하는 경우가 많다.
- 테스팅이라는 것을 체계적으로 해본 경우가 없다.
  - 일단 이것저것 해보다가 버그를 찾는다.
  - 사용자가 버그를 찾는 것과 크게 다르지 않기 때문에 테스팅이라 하기 어렵다.

### What is Bug?

#### 최초의 버그

- 코볼의 발명자인 그레이스 호퍼가 발견
- 마크2가 오작동해서 살펴보니 컴퓨터 안에 나방이 들어가 있었음
- 최초의 버그 이후에도 수많은 SW 문제를 발견함
- 인간이 가진 한계, 누구나 실수를 한다.
- 실수를 어떻게 줄일지 연구를 한다. 그 결과 인간이 다루기 쉬운 고급 언어인 코볼을 만든다.

#### Unexpected

- 버그: 기대하지 않은 일이 발생했다.

#### Specification

- 기대하는 일을 명시적으로 표현한 것
- 이것을 명확히 하는 것이 대단히 중요하다.
- 작동하는 SW가 이 사양에 맞는지 안맞는지를 확인하는 것이 테스팅이다.

#### Feature

- 기능 목록을 만들고 이를 구현한다.

#### Behavior

- 기능이 무엇인가?
- SW가 어떻게 동작하는 것과 관련된 것이다.

#### Behavior First

- 행위를 먼저 쓰는 것이다.
- TDD라고 하면 테스팅에 대한 오해로 접근이 어렵다.
- 표현을 조금 바꿈으로써 이해를 도운다.

##### Desribe "JUMP"

```
It should push the hero off the floor
It should put the hero in the air for 10 seconds
```

#### Situation

- 어떤 기능은 상황에 따라서 다르게 동작할 수 있다.
- 상황이 다른 것을 묘사한다.

##### Desribe "ATTACK"

```
Context "without a weapon"
  It should do 1 point of damage

Context "with a sword"
  It should do 10 points of damage
```

### 기존 테스트 코드와의 장단점

#### 장점

- 함수 이름 정하는 것이 자유롭다.
- 컨텍스트를 분리하다보니 다양한 상황을 추가할 여지가 생긴다.
- 익명함수 클로저로 바인딩하기 때문에 전역변수가 없다. (전역변수를 남발하는 문제를 해결할 수 있다.)

#### 단점

- 코드가 길어지고 깊이(들여쓰기)도 깊어진다.


### intention

- 코드의 의도가 명확하게 드러난다.
