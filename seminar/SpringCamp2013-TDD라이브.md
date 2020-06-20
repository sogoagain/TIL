# [SpringCamp2013] TDD 라이브

- 발표자: 최범균님
- 영상 링크: [[SpringCamp2013] TDD 라이브](https://youtu.be/AE7K-16dEjo)

## 목표

- TDD 느껴보기
  - 조금 더 현실에서 볼 만한 예제
  - 코딩하는 과정을 지켜보면서 '아~' 하는 느낌 얻기
- 사전 필요 지식
  - JUnit, Mock에 대한 기본 지식 필요

## TDD

- Test Driven Development 테스트 주도 개발
  - 제품 코드 만들기 전에 테스트 먼저 작성하기
- 기본 흐름 (완료할 때 까지 반복)
  - 실패 테스트 작성 > 테스트 성공 시키기 > 코드 청소하기
- 테스트 작성 순서
  - 쉬운 것, 예외적인 것 > 어려운 것, 정상적인 것

## 구현해 볼 것

- 웹 로그인 기능 
  - Login Controller
  - AuthService - 중점
  - UserRepository
  - LoginCommand
  - Authentication
  - User

## 라이브 1 - AuthSErvice

### TDD 순서

- 테스트 클래스 만들기
- 객체 생성하기 (쉬운)
- ID 값이 비정상인 경우 (쉬운, 정상에서 벗어난)
- PW 값이 비정상인 경우 (쉬운, 정상에서 벗어난)
- User가 존재하지 않는 경우 (정상에서 벗어난)
- ID에 해당하는 User가 존재하는데, PW가 일치하지 않는 경우 (정상에서 벗어난)
- ID와 PW가 일치하는 경우 (정상)
  - 인증 정보를 리턴

#### 라이브 코딩

- 아무것도 안하는 메서드를 하나 만들어서 테스트 실행
  - 일종의 자신감 얻기
  - 테스트를 돌릴 수 있는 환경을 만든 것
- canCreate
- givenInvalidId_throwIllegalArgEx
- 테스트를 통과시키면 리팩터링을 해야한다.
  - 테스트 코드도 리팩터링한다.
  - 테스트 대상 객체를 필드로 만들고 객체 생성 자체를 setUp에서 하도록 변경
  - 중복되는 단정문을 메서드로 추출 > assertIllegalArgExThrown, assertExceptionThrown
- whenUserNotFound_throwNonExsitingUserEx
- 삼각측량
  - 특정한 상황에서 범용적인 상황으로 넘어가는 경우를 위해 사용
  - 같은 경우인데 아이디가 다른 테스트 케이스를 추가해본다.
- whenUserFoundButWrongPw_throwWorngPasswordEx
- BDD
  - given, when, then
- mock 생성 부분도 setUp으로 옮긴다.
- 매직넘버를 상수로 만들어준다.

## 라이브 2 - LoginController

- 웹 요청 처리
- 비슷한 순서로 진행
  - 폼 요청 처리 (쉬움)
  - 폼 전송 시, LoginCommand 값 이상, 폼 뷰 리턴 (비정상)
  - 폼 전송 시, ID/PW 불일치, 폼 뷰 리뷰 (비정상)
  - 폼 전송 시, ID/PW 일치, 성공 뷰 리턴 (정상)
    - 쿠키 생성 확인
- 처음부터 정상적인 경우로 덤비면 TDD를 하기가 어려워진다.
  - 생각할 게 너무 많아짐.
  - 생각 안해도 되는 것을 먼저 한다.

## 라이브 3 - SpringMVC 테스트

- 웹 관점에서 컨트롤러 테스트
  - 컨트롤러 설정이 올바른지 확인
  - 응답 결과(JSON/XML 등)과 올바른지 확인
- 브라우저/서버 NO! 테스트 코드 YES!
  - Spring-mvc-test 사용

## 우릴 기다리는 더 많은 이야기...

- 스프링 통합 테스트
  - @RunWith(SpringJUnit4ClassRunner.class)
- 스프링 MVC 테스트
  - MockMVC
- DB 통합 테스트
  - DB Unit
- 테스트 계층 구조
  - @RunWith(Enclosed.class)

## 정리

- TDD 장점
  - 짧은 호흡
    - 흐름(컨텍스트)을 유지, 집중력 향상
    - 문제 찾기 용이
      - 테스트 직전에 작성한 코드에서 문제 발생 가능성 높음
  - 점진적 코드 완성
    - 필요한 코드만 쓰도록 유도
  - 회귀(regression) 테스트 기반
    - 코드 수정에 대한 자신감, 과감한 리팩토링 가능
- Mock
  - 외부 시스템 없이 핵심 코드 작성 가능
  - 필요한 경우 임시 구현 사용

## 참고자료

### TDD 관련 서적

- 테스트 주도 개발 (켄트 벡 저)
- 객체 지향 설계와 실천 (스티브 프리먼 저)
- Test Driven (Lasse Koskela)

### TDD 관련 비디오

- 백명석님 TDD 강의 자료 (4회)