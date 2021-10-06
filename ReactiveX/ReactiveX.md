Spring 프로젝트에서 `application` 파일은 속성을 정의하는 데에 쓰입니다.

### spring.profiles.active
현재 활성화된 프로필을 나타내는 속성

### spring.jpa.show-sql
[JPA](https://spring.io/projects/spring-data-jpa)를 통해 DB와 통신 시 호출되는 SQL 쿼리를 로그에서 바로 확인할 수 있는 속성

### spring.main.allow-bean-definition-overriding
bean을 재정의하는 것을 허락할지에 대한 속성
> Spring Boot 2.1 버전에선 이 속성의 기본 값이 `false`로 변경되었는데, **실수로 bean을 재정의하는 것을 방지하기 위함**이라고 합니다.

>참고 아티클  
https://www.popit.kr/spring-webflux%EC%99%80-kotlin%EC%9C%BC%EB%A1%9C-%EB%A7%8C%EB%93%9C%EB%8A%94-todo-%EC%84%9C%EB%B9%84%EC%8A%A4-1%ED%8E%B8/