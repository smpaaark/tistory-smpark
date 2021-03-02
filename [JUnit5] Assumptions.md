Assumtions의 assumeTrue, assumingThat을 이용하여 특정한 조건에 따라 테스트 실행 여부를 결정할 수 있다.

## assumeTrue
조건이 만족해야 뒤의 코드들이 실행된다.

### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    String test_env = System.getenv("TEST_ENV");
    System.out.println(test_env);
    assumeTrue("LOCAL".equalsIgnoreCase(test_env));
    
    Study actual = new Study(10);
    assertThat(actual.getLimit()).isGreaterThan(0);
}
```

### 결과(환경변수 추가 전)   
TEST_ENV가 null이라 assumeTrue 이후의 코드가 실행되지 않았다.   
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/2.PNG)   
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/1.PNG)

### 결과(환경변수 추가 후)   
assumeTrue 뒤의 코드들이 정상적으로 실행되었다.   
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/3.PNG)   
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/4.PNG)

## assumingTrue
특정 조건이 만족하면 파라미터로 주어진 테스트를 실행한다.
### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    String test_env = System.getenv("TEST_ENV");

    assumingThat("LOCAL".equalsIgnoreCase(test_env), () -> {
        System.out.println("local");
        Study actual = new Study(100);
        assertThat(actual.getLimit()).isGreaterThan(0);
    });
    
    assumingThat("smpark".equalsIgnoreCase(test_env), () -> {
        System.out.println("smpark");
        Study actual = new Study(10);
        assertThat(actual.getLimit()).isGreaterThan(0);
    });
}
```
### 결과   
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/5.PNG)   
![6](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%A1%B0%EA%B1%B4%EC%97%90%20%EB%94%B0%EB%9D%BC%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/6.PNG)   

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)