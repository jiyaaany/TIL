# Spring WebFlux란?
Spring WebFlux는 Project Reactor 기반의 [Reactive Extension](ReactiveX/ReactiveX.md)입니다.
논 블로킹(non-blocking)과 배압(backpressure)이라는 특징을 가진 리액티브 프로그래밍 모델을 스프링 환경에서 쉽게 효율적으로 개발할 수 있게 하는 프레임워크이다.
- 어노테이션 기반 리액티브 컴포넌트 (Annotation-based reactive components)
    - Spring MVC와 유사한 방식으로 구현이 가능하여 쉽게 적응할 수 있음.
- 함수형 라우터와 핸들러(Functional routing and handling)
    - 라우터 함수(Router Function)은 RequestPredicate를 통해 클라이언트에서 들어온 request를 관리하는 역할
    - 핸들러 함수(Handler Function)는 라우터 함수로 들어온 request에 대한 처리를 정의

# 프로젝트 구조
- domain
    - 이 패키지에는 도메인에 관련된 Entity, DTO, Repository 등을 포함한다.
- router
    - 사용자의 요청을 전달받아 적절한 핸들러로 라우팅해주는 역할을 한다.
- handler
    - 라우터로부터 전달받은 요청을 처리하고 응답을 생성한다.

## 도메인(Domain)
JPA에서 말하는 Entity는 데이터베이스 테이블과 매핑 된다. ORM(Object Relational Mapping)은 데이터베이스와 객체 간의 패러다임 불일치를 해결해주는 솔루션이다.

## 리포지토리(Repository)
JpaRepository를 상속받아 JPA에 의해 관리되고 확장한다는 것을 알 수 있다.

## 라우터(Router)
함수 안에 정의된 라우터들은 API의 엔드포인트가 됩니다. 기본적인 구현은 `GET` `POST` `PUT` `DELETE`에 대응하도록 정의되어 있습니다. 각각 라우터들은 클라이언트로부터 요청이 들어오면 [handler](##handler)에게 처리를 위임합니다.

## 핸들러(Handler)
핸들러는 저장, 삭제 등을 처리하는 비즈니스 로직이 구현되어 있습니다. 

>참고 아티클  
https://www.popit.kr/spring-webflux%EC%99%80-kotlin%EC%9C%BC%EB%A1%9C-%EB%A7%8C%EB%93%9C%EB%8A%94-todo-%EC%84%9C%EB%B9%84%EC%8A%A4-1%ED%8E%B8/