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