스프링 부트 2.2부터 기본 JUnit 버전을 JUnit5로 올렸다. TestEngine 구현체로 Jupiter를 사용하여 JUnit5를 제공한다.

## 스프링 부트 버전
![pom.xml](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20Jupiter/1.PNG)
스프링 부트 2.4.3

## 메이븐 의존성
![dependency](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20Jupiter/2.PNG)
spring-boot-starter를 통해 JUnit5와 jupiter 관련 의존성이 추가된다.

## Test 코드
![테스트코드l](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20Jupiter/3.PNG)
import를 보면 jupiter가 사용된 것을 확인할 수 있다.

## 스프링 부트를 사용하지 않을 때 JUnit5를 사용하고 싶다면?
![의존성추가](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20Jupiter/4.PNG)
pom.xml에 JUnit5 의존성을 직접 추가해주면 된다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)