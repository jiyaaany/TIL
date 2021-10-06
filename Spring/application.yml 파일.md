Spring 프로젝트에서 `application.yml` 파일은 속성을 정의하는 데 쓰인다. 

### spring.profiles.active
현재 활성화된 프로필을 나타내는 속성

### spring.jpa.show-sql
[JPA](https://spring.io/projects/spring-data-jpa)를 통해 DB와 통신할 때 SQL 쿼리를 로그를 통해 확인할 수 있는 속성

### spring.main.allow-bean-definition-overriding
bean을 재정의하는 것을 허용할지 말지에 대한 속성
> Spring Boot 2.1 버전에서 기본 값이 `false`로 변경되었는데, 이는 **실수로 bean을 재정의하게 되는 것을 방지하기 위함**이라고 한다.