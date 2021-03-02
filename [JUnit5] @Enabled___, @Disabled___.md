\@Enabled____, \@Disabled___을 이용하여 특정한 조건에 따라 테스트 실행 여부를 결정할 수 있다.

## OS 조건
OS가 뭐냐에 따라 테스트 실행 여부를 결정할 수 있다.

### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
@EnabledOnOs({OS.WINDOWS, OS.LINUX})
void create_new_study() {
    String test_env = System.getenv("TEST_ENV");
    System.out.println("local");
    Study actual = new Study(100);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Test
@DisplayName("스터디 만들기 😂😂")
@DisabledOnOs(OS.WINDOWS)
void create_new_study_again() {
    System.out.println("create1");
}
```

### 결과(현재 OS는 Window)
![7](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/7.PNG)   
![8](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/8.PNG)

## JRE 조건
현재 사용중인 JRE 버전에 따라 테스트 실행 여부를 결정할 수 있다.

### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
@EnabledOnJre({JRE.JAVA_8, JRE.JAVA_9, JRE.JAVA_10, JRE.JAVA_11})
void create_new_study() {
    String test_env = System.getenv("TEST_ENV");
    System.out.println("local");
    Study actual = new Study(100);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Test
@DisplayName("스터디 만들기 😂😂")
@EnabledOnJre(JRE.OTHER)
void create_new_study_again() {
    System.out.println("create1");
}
```

### 결과(현재 JRE는 Java8)
![7](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/7.PNG)   
![8](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/8.PNG)

## 환경변수 조건
환경변수 값에 따라 테스트 실행 여부를 결정할 수 있다.

### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
@EnabledIfEnvironmentVariable(named = "TEST_ENV", matches = "LOCAL")
void create_new_study() {
    Study actual = new Study(100);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Test
@DisplayName("스터디 만들기 😂😂")
@EnabledIfEnvironmentVariable(named = "TEST_ENV", matches = "smpark")
void create_new_study_again() {
    System.out.println("create1");
}
```

### 결과(현재 TEST_ENV는 LOCAL)
![9](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/9.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)