# 컴퓨터 개념 및 실습

> 서울대학교 공과대학 민상렬 교수님 강의
- 컴퓨터 과학/공학을 전공/부전공/복수전공 할 학생들을 위한 개론 교과목

## 1. Welcome Abroad

> 강의: [[서울대학교 공과대학] 컴퓨터의개념및실습 1. Welcome Abroad](https://youtu.be/5Ic_AhAFbco)

### Abstraction

- 차를 운전할 때 운전자가 바라보는 Interface
  - 핸들, 가속패달, 브레이크, 방향등 조작, 와이퍼 조작, 라디오
  - 실제 운전자가 바라보는 인터페이스는 동일
- 차 내부를 들여다 보면
  - 어떤 차는 휘발유, 어떤 차는 디젤, 어떤 차는 전기, 어떤 차는 하이브리드
  - 내부 구조는 다 다르다.
- 내부 구조는 달라도 운전자가 바라보는 interface는 동일하다.
- 컴퓨터 분야 뿐만 아니라 다양한 분양에서 사용됨.
- 사용되는 이유가 무엇일까?
  - 인간이 한 순간에 다룰 수 있는 복잡도에 제한이 있다.
  - 큰 시스템을 구성하기 위해서는 일단 작은 시스템을 만들어 간다.
  - 작은 시스템을 사용하기 위한 인터페이스를 만들어 그 아래 쪽의 자세한 구현은 잊어버릴 수 있도록 한 뒤 그 인터페이스를 하나의 Building Block으로 사용한다.
  - 작은 것들을 묶어서 조금 더 큰 시스템을 만들고, 더 큰 시스템에 interface를 정의하고 그 구현과 관련된 일은 잊어버릴 수 있도록 한다.
  - 이를 반복해 큰 시스템을 만들어 나간다.

- 어떤 시스템에서 내부의 자세한 사항들은 감추고, 사용하는데 필요한 사항들을 interface로 정의해 그 시스템을 하나의 Building Block으로 사용가능하도록 정의 하는 것이 Abstraction이다.
- Interface와 Implementation을 분리할 수 있다.
- 동일한 interface를 가지면서도 다양한 implementation을 갖도록 할 수 있다.

### Levels of Abstraction (Man-made)

- 단일 계층의 Abstraction도 있지만, 일반적으로 Abstraction에는 계층 구조가 있다.

#### Man-made

- 자동차 예
  - 자동차 > 전기 ( > 에어백, 배터리), 샤시 ( > 스프링, 스티어링), 엔진 ( > 실린더, 스파크 플러그) 

#### Biological System

- 사람의 예
  - 원자 > 분자 > 세포 > ... > 인간

#### Computer

- 컴퓨터 예
  - Problems
  - Algorithms
  - Language
  - Instruction Set Architecture --- [Hardware/Software Interface]
  - Microarchitecture
  - Circuits
  - Devices
- 'Instruction Set Architecture'가 정의되고 나면 그 위의 추상화 레벨에서는 아래쪽에서 어떻게 구현되었는지 크게 신경쓸 필요가 없어진다.

### Universal Computing Device

All computers, given enough time and memory, are capable of computing exactly the same things.

- 실제 어떤 문제를 풀 수 있는 가에 관점에서 보면 슈퍼컴퓨터나 데스크탑이나 노트북이나 스마트폰이나 동일하다.
- 충분한 시간과 메모리가 주어진다고 하면 서로 다른 디바이스간 컴퓨팅 파워에는 차이가 없다.
- 그러면, 가장 간단한 컴퓨팅 디바이스는 무엇인가? 그게 바로 튜링 머신이다.

### Turing Machine

Mathematical model of a device that can perform any computation - Alan Turing (1937)
Every computation can be performed by some Turing machine. (Turing's thesis)

- 엘런 튜링이 만들어낸 수학적 모델
- 실제 컴퓨테이션이 가능한 것은 자신이 제안한 튜링 머신에서도 풀 수 있다.
- 튜링 머신은 현재의 컴퓨터보다 간단하지만 컴퓨팅 파워 측면에서는 차이가 없다.
- 그럼, 이 세상에 계산하지 못하는 문제도 있나?
  - 있다. Halting Problem

### A Turing Machine

- Tape
  - 무한히 펼쳐질 수 있는 테잎이 있고
  - 그 테잎에 적혀있는 심볼을 쓰거나 읽을 수 있는 Read-Write head가 있다.
- Control Unit
  - 실제 헤드를 어떻게 움직이고,
  - 테잎에 적혀있는 정보에 따라서 어떤 액션을 취하는지 지정해주는 Control Unit

#### The Tape

- No boundaries -- infinite length
  - 바운더리가 없다.
  - 왼쪽으로도 오른쪽으로도 무한히 펼쳐져 있다.
- Read-Write head
  - The head moves Left or Right
  - The head at each transition (time step):
    1. Reads a symbol
    2. Writes a symbol
    3. Moves Left or Right
- 예
  - Time 0: ...|a|b|a^|c|...
  - 수행
    1. Reads a
    2. Writes k
    3. Moves Left
  - Time 1: ...|a|b^|k|c|...

- Computation Example
  - The function
    - f(x,y) = x + y is computable
    - x,y are integers
  - Turing Machine:
    - Input string: x0y unary
    - Output string: xy0 unary
      * unary: 숫자를 작대기로 표현하는 것 (1: /, 2: //, 3: ///)
      * The 0 is the delimiter that separates the two numbers.
    - 예
      - x = 11 (=2), y = 11 (=2)
      - Time 0: ◇|1^|1|0|1|1|◇
      - Final Result: ◇|1^|1|1|1|0|◇
      - Control Unit (finite state machine으로 정의)
        - 1 -> 1, R (반복)
        - 0 -> 1, R
        - 1 -> 1, R (반복)
        - ◇ -> ◇, L
        - 1 -> 0, L
        - 1 -> 1, L (반복)
        - ◇ -> ◇, R (HALT & aceept)

#### Universal Turing Machine

- 튜링 머신에 여러 종류가 있는데, 그 중에서 가장 일반적인 튜링 머신
- A machine that can implement all Turing machines -- this is also a Turing machine!
- input을 튜링 머신을 받음, 컴퓨터 입장에서 보면 프로그램 자체도 input data가 된다.
- T(add), T(mul), a, b, c => U => c(a + b)
- U is programmable - so is a computer
  - Program is part of the input data
  - a computer can emulate a Universal Turing Machine and vice versa
    - 컴퓨터의 메모리가 무한하다고 하면(튜링 머신은 테잎이 무한하다) Universal Turing Machine을 emulate 할 수 있다.
    - 우리가 Universal Uring Machine을 가지고 있다고 하면 프로그램은 복잡하겠지만, 컴퓨터를 그대로 emulate 할 수 있다.
- 즉, A computer is a universal computing device.

### Halting Problem

- 이 세상에 풀 수 없는 문제도 있는가?
- Halting Problem
  - The problem of determining, from a description of an arbitrary computer program (i.e., Turing machine) and an input, whether he program will finish running (i.e., halts) or continue to run forever
    - 튜링 머신과 input이 주어졌을 때 프로그램이 과연 멈출 것인가? 판단하는 문제
  - Halting problem is undecidable (not Turing machine solvable)
    - Proof by an application of Cantor's diagonal argument) (오토마타 교과목에서 더 깊게 다루어짐.)
    - 어떤 튜링머신도 이 문제를 풀 수 없기 때문에 어떤 컴퓨터도 풀 수 없다.
    - 칸토어의 diagonal argument
      - 이 세상에는 자연수와 1:1로 매핑되는 무한그룹보다 더 큰 무한그룹이 있다는 것을 증명하기 위한 방법
      - 이 방법을 이용해 증명할 수 있음

### 꼭 기억해야 할 것

- (Levels of) Abstraction
- Turing Equivalence
- Undecidable Problem (not Turing machine computable)
