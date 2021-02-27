JUnit5의 Assertion은 검증하고자 하는 내용을 확인하는 기능이다. 첫번째 파라미터는 기대하는 값, 두번째 파라미터는 실제 값을 넣어준다. 세번째 파라미터에 메시지를 추가하면 테스트가 실패했을 때 해당 메시지가 표시되기 때문에 이 테스트가 왜 실패했는지 이해하기 좋다.

### assertEquals
실제 값이 기대한 값과 같은지 확인

### assertNotNull
값이 null이 아닌지 확인

* 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study();
    assertNotNull(study);
    assertEquals(StudyStatus.DRAFT, study.getStatus(), "스터디를 처음 만들면 상태값이 DRAFT여야 한다.");
}
```
* 결과
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/1.PNG)

### assertTrue
다음 조건이 참(true)인지 확인

* 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study(-10);
    assertNotNull(study);
    assertEquals(StudyStatus.DRAFT, study.getStatus(), () -> "스터디를 처음 만들면 " + StudyStatus.DRAFT + " 상태다.");
    assertTrue(study.getLimit() > 0, "스터디 최대 참석 가능 인원은 0보다 커야 한다.");
}
```

* 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/3.PNG)
(assertAll 적용한 결과, assertTrue 에러 문구만 참고)

### assertAll
모든 assert 구문 확인. 여러개의 assert문이 실패 했을 때 처음 assert문이 실패하면 뒤의 assert문이 실행되지 않기 때문에 모든 assert문을 확인하기 위해 assertAll을 사용한다.

* assertAll 사용하지 않은 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study(-10);
    assertNotNull(study);
    assertEquals(StudyStatus.DRAFT, study.getStatus(), () -> "스터디를 처음 만들면 " + StudyStatus.DRAFT + " 상태다.");
    assertTrue(study.getLimit() > 0, "스터디 최대 참석 가능 인원은 0보다 커야 한다.");
```

* 결과
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/2.PNG)

* asssertAll 사용한 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study();
    
    assertAll(
        () -> assertNotNull(study),
        () -> assertEquals(StudyStatus.DRAFT, study.getStatus(), () -> "스터디를 처음 만들면 " + StudyStatus.DRAFT + " 상태다."),
        () -> assertTrue(study.getLimit() > 0, "스터디 최대 참석 가능 인원은 0보다 커야 한다.")
    );
}
```

* 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/3.PNG)

* assertAll은 Excutable...을 파라미터로 받는다.
```
public static void assertAll(Executable... executables) throws MultipleFailuresError {
    AssertAll.assertAll(executables);
}
```

* Executable은 메서드를 1개만 갖고 있는 함수형 인터페이스이다.
```
@FunctionalInterface
@API(status = STABLE, since = "5.0")
public interface Executable {

	void execute() throws Throwable;

}
```

### assertThrows
어떤 작업을 실행했을 때 익셉션이 발생하는지 확인할 수 있으며, Exception을 받아서 내가 기대했던 메시지와 같은지도 확인할 수 있다.

* 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    IllegalArgumentException exception = 
            assertThrows(IllegalArgumentException.class, () -> new Study(-10));
    assertEquals("limit은 0보다 커야 한다.", exception.getMessage());
}
```

* 결과는 성공인 케이스 확인이므로 생략

### assertTimeout
특정 시간 안에 실행이 완료되는지 확인

* 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    assertTimeout(Duration.ofMillis(100), () -> {
        new Study(10);
        Thread.sleep(300);
    });
}
```

### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/4.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)