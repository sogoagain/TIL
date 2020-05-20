 [![HitCount](http://hits.dwyl.io/sogoagain/TIL.svg)](http://hits.dwyl.io/sogoagain/TIL)

# Today I Learned (TIL)

- 나의 성장 기록
- 나의 포트폴리오
- 장인정신을 실천하기 위한 내공 쌓기

---

## 목차

- [Essay](#essay)
- [Project](#project)
- [TDD(Test Driven Development)](#tdd)
- [Algorithm](#algorithm)
- [WEB](#web)
- [OOP(Object-Oriented Programming)](#oop)
- [Design Patterns](#design_patterns)
- [Programing Language](#programing_language)
- [Data Structure](#data_structure)
- [Software Engineering](#software_engineering)
- [Computer Architecture](#computer_architecture)
- [DB](#db)
- [Linux](#linux)
- [Android](#android)
- [Computer Graphics](#computer_graphics)
- [Devops](#devops)
- [실수노트](#mistake_notes)
- [ETC](#etc)

---

<a name="essay">
 
### Essay

- [Bookshelf - 나의 독서 목록 📖](https://github.com/sogoagain/bookshelf)

<a name="project">

### Project

- [도서 출처 표기 문구 생성기](https://github.com/sogoagain/book-citation-generator) (2020년 ~ 진행중)
  - 팀구성: 개인
  - 글을 작성할 때 도서의 문구를 인용하면 출처 표기를 해야하는데, 이 때 사용할 수 있도록 출처표기법에 따라 문구를 생성해주는 웹 사이트
    - 사용자 스토리 기반의 이슈 생성
    - 칸반 보드를 이용한 프로젝트 관리
    - 다음(Kakao) 검색 API 활용
  - 기술요소: ReactJS, Node.js

- [SpringBoot2 & ReactJS Boilerplate](https://github.com/sogoagain/springboot-react-boilerplate) (2020년)
  - 팀구성: 개인
  - SpringBoot2 & ReactJS를 사용하는 환경에서 신속히 개발환경을 구축하기 위한 Boilerplate
    - 입력된 단어를 저장하는 간단한 Application
    - SpringBoot2 환경 테스트 코드 작성
  - 기술요소: SpringBoot2, ReactJS, And Design

- [음성인식 호텔 객실 제어 어플리케이션](https://github.com/sogoagain/android-stt-hotel-room-control) (2018년)
  - 팀구성: 안드로이드 개발1, 관리자 웹 개발1, 객실/관리 서버 개발2, DB 개발1
  - 음성 명령으로 호텔 객실을 제어하는 파일럿 프로젝트
    - 팀장으로서 전체 시스템 구조 설계
    - Android Application 개발
    - 음성 인식된 문장에서 제어할 개체와 명령을 분리하여 처리하는 알고리즘 설계
  - 기술요소: JAVA, Android, STT, 간단한 자연어 처리

- [모바일 센싱 프로그래밍](https://github.com/sogoagain/android-mobile-system-programming) (2017년)
  - 팀구성: 개인
  - 배터리를 효율적으로 사용하는 모바일 센싱 프로그래밍 (총 3개 어플리케이션)
    - ProximityAlarm: 위치기반 근접 경보 알림 어플리케이션
    - EncounterMonitor: 블루투스를 이용해 특정 사람과 만났던 시간을 기록하는 어플리케이션
    - ActivityTracker: 사용자 활동 모니터링 어플리케이션
  - Energy Efficient Sensing을 위한 센싱 알고리즘 설계
  - Battery Historian을 이용한 테스팅으로 알고리즘 최적화
  - 기술요소: JAVA, Android, Energy Efficient Sensing

- [운영체제 페이지 교체 시뮬레이션](https://github.com/sogoagain/page-replacement-simulation) (2017년)
  - 팀구성: 설계1, 개발4, 테스트 케이스 구성2
  - 운영체제 페이지 교체 알고리즘별 성능 비교를 위한 시뮬레이션 프로그램
    - 팀의 리더로서 프로젝트 진행
    - 디자인 패턴을 활용한 객체지향 디자인 설계 및 개발
    - 참고문헌을 활용한 테스트 케이스 구성
  - 기술요소: C++, Operating System, Design Pattern

 - [3D MP3 Player](https://github.com/sogoagain/opengl-bvh-music-player) (2016년)
   - [소개자료](https://github.com/sogoagain/opengl-bvh-music-player/blob/master/JUDY_Introduce.pdf)
   - 팀구성: 개인
   - 음악 장르에 따라 3D캐릭터가 춤을 추는 MP3 플레이어
     - OpenGL을 활용한 그래픽 프로그래밍
     - BVH를 활용한 모션 캡처 데이터 적용
   - 기술요소: C++, OpenGL, bvh

<a name="tdd">

### TDD (Test Driven Development)

- [테스트 주도 개발 (Test-driven development) 실천 연습 저장소](https://github.com/sogoagain/tdd-exercises)
- [JUnit5 - 하나의 테스트 메서드에서 여러 테스트 케이스 수행하기](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-06-17-JUnit5-Parameterized-Test.md)

<a name="algorithm">

### Algorithm

- [문제해결 능력 향상을 위한 알고리즘과 자료구조 연습 저장소](https://github.com/sogoagain/problem-solving-and-algorithms)
- [가위바위보에 적용한 유전 알고리즘](https://github.com/sogoagain/design-patterns/blob/master/01_Strategy-Pattern/RockPaperScissors/GeneticStrategy.java)
- [Algorithm 문제 풀이 시 자주 사용되는 Java Code Snippet](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-05-01-Algorithm-문제-풀이-시-자주-사용되는%20-Java-Code-Snippet.md)

<a name="web">

### WEB

- [HTML/CSS 기초 연습 공간](https://github.com/sogoagain/TIL/tree/master/HTML5CSS3)
- [Javascript 기초 연습 공간](https://github.com/sogoagain/TIL/tree/master/JavaScript)
- [JSP 실습](https://github.com/sogoagain/TIL/tree/master/JSP)
- [ASP.NET 공부 정리(예제)](https://github.com/sogoagain/asp.net-web-programming)
- [Spring-Boot, JPA로 질문/답변 게시판 구현 과정 - 박재성님 강의](https://github.com/sogoagain/springboot-qna-board)
- [HTTP 메시지 - HTTP Requests](https://sogoagain.github.io/2019/08/03/HTTP-메시지-HTTP-Requests/)
- [SpringBoot2 & ReactJS Boilerplate](https://github.com/sogoagain/springboot-react-boilerplate)

<a name="oop">

### OOP (Object-Oriented Programming)

- [가상함수와 가상상속](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-01-05-가상함수와%20가상상속.md)
- [개체와 객체와 인스턴스](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-01-12-개체와%20객체와%20인스턴스.md)
- [AWS도 Setter를 사용하지 않는다](https://sogoagain.github.io/2019/09/25/AWS도-Setter를-사용하지-않는다/)

<a name="design_patterns">

### Design Patterns

- [JAVA로 실습한 디자인 패턴 예제](https://github.com/sogoagain/design-patterns)

<a name="programing_language">

### Programing Language

- [복사 생성자(Copy Constructor), 소멸자(Destructor)를 이용한 '='연산자 오버로딩](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-01-14-대입연산자오버로딩.md)
- [JAVA 예제 실습](https://github.com/sogoagain/TIL/tree/master/JAVA)
- [도서 '빅 너드 랜치의 코틀린 프로그래밍' 실습 저장소](https://github.com/sogoagain/kotlin-programming-the-big-nerd-ranch-guide)
- [코틀린(Kotlin)에서의 null 안전 처리](https://sogoagain.github.io/2019/08/20/코틀린-Kotlin-에서의-null-안전-처리/)

<a name="data_structure">

### Data Structure

- [C++로 직접 작성한 자료구조](https://github.com/sogoagain/cpp-data-structure)

<a name="software_engineering">

### Software Engineering

- [애자일 소프트웨어 개발(Agile software development)](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-01-05-애자일%20소프트웨어%20개발(Agile%20software%20development).md)
- [구체 수학 (Concrete Mathematics)](https://github.com/sogoagain/concrete-mathematics)

<a name="computer_architecture">

### Computer Architecture

- [SimpleScalar를 이용한 Cache Simulation](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-06-27-SimpleScalar를%20이용한%20Cache%20Simulation.md)

<a name="db">

### DB

- [DB 기본 내용 정리](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-01-22-DB-기본-내용-정리.md)
- [ORA-12505 오류 해결을 통한 Oracle DB의 SID와 ServiceName에 대해서](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-02-22-ORA-12505-오류-해결을-통한-OracleDB의-SID와-ServiceName에-대해서.md)

<a name="linux">

### Linux

- [리눅스 시스템 프로그래밍](https://github.com/sogoagain/linux-system-programming)

<a name="android">

### Android

- [직접 구현한 간단한 Android 어플리케이션](https://github.com/sogoagain/andorid-mobile-programming)

<a name="computer_graphics">

### Computer Graphics

- [직접 구현한 간단한 OpenGL 프로그램](https://github.com/sogoagain/opengl-computer-graphics)
  - [Bresenham Line Algorithm 구현](https://github.com/sogoagain/opengl-computer-graphics/tree/master/Bresenham_Line_Algorithm)
  - [Cohen Sutherland Algorithm 구현](https://github.com/sogoagain/opengl-computer-graphics/tree/master/Cohen–Sutherland_Algorithm)
  
- [Unity3D에서 Observer 패턴을 이용한 연산량 감소](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-02-06-Unity3D에서-Observer패턴을-이용한-연산량-감소.md)

<a name="devops">

### Devops
- [IntelliJ에서 Docker에 올려진 Tomcat으로 Web Application 배포하기](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-03-08-IntelliJ에서-Docker에-올려진-Tomcat으로-웹앱-배포하기.md)

<a name="mistake_notes">

### 실수노트
- [캐싱된 메서드는 변경 불가능한(Immutable) 객체를 반환토록 하자](https://sogoagain.github.io/2019/12/06/실수노트-캐싱된-메서드는-변경-불가능한-Immutable-객체를-반환토록-하자/)

<a name="etc">

### ETC

- [SourceTree에서 'Permission denied (publickey)' 에러 발생 시 조치방법](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-01-08-SourceTree%20Permission%20denied%20(publickey)%20issue.md)
- [나의 vimrc 설정](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-01-29-vimrc.md)
- [나중은 결코 오지 않는다.](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2017-01-06-나중은%20결코%20오지%20않는다.md)
- [문화와 기술](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-06-07-문화와-기술.md)
- [Git 기본 명령어 정리](https://github.com/sogoagain/sogoagain.github.com/blob/master/_posts/2019-06-12-Git-기본.md)
- [의식적인 연습에 기반한 나의 앞으로의 학습](https://sogoagain.github.io/2019/10/22/의식적인-연습에-기반한-나의-앞으로의-학습/)
- [2019년 회고](https://sogoagain.github.io/2020/01/11/2019년-회고/)
- [삶에 애자일 도입하기](https://sogoagain.github.io/2020/01/12/삶에-애자일-도입하기/)
- [레거시 코드를 점진적으로 개선한 경험](https://sogoagain.github.io/2020/03/08/레거시-코드를-점진적으로-개선한-경험/)
