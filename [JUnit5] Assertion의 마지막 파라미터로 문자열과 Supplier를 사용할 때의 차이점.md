Assertion의 마지막 파라미터로 문자열 또는 Supplier를 사용하면 테스트가 실패했을 때 해당 메시지가 표시되기 때문에 이 테스트가 왜 실패했는지 이해하기 좋다.

* 문자열 사용 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study();
    assertNotNull(study);
    assertEquals(StudyStatus.DRAFT, study.getStatus(), "스터디를 처음 만들면 " + StudyStatus.DRAFT + " 상태다.");
}
```

* Supplier 사용 코드 (람다식 사용)
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study();
    assertNotNull(study);
    assertEquals(StudyStatus.DRAFT, study.getStatus(), () -> "스터디를 처음 만들면 " + StudyStatus.DRAFT + " 상태다.");
}
```

* 결과
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/2.PNG)

이때 문자열을 사용할때와 Supplier를 사용할때의 결과는 같은데 어떤 차이가 있을까?

## 차이점
위 코드처럼 문자열 연산이 있을 경우에 문자열을 사용하면 해당 테스트가 실패하지 않더라도 문자열 연산을 하지만, Supplier를 사용하게 되면 이 테스트가 실패했을 경우에만 문자열 연산을 하기 때문에 더 효율적인 코드라고 할 수 있다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)