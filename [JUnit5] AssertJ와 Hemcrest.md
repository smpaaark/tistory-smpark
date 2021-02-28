spring-boot-starter를 사용하면 jupiter의 Assertion 말고도 AssertJ나 Hemcrest 의존성이 자동으로 추가되어서 해당 기능을 사용할 수도 있다.

* 의존성 확인
![6](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/6.PNG)

* AssertJ 사용 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study actual = new Study(10);
    assertThat(actual.getLimit()).isGreaterThan(0);
}
```

* 결과
![7](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/7.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)