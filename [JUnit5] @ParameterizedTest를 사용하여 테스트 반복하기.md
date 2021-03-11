\@RepeatedTest가 횟수를 기준으로 테스트를 반복하는 것이고, \@ParameterizedTest는 매개변수를 이용하여 테스트를 반복하는 것이다.
JUnit5는 기본으로 제공하고 있으나, JUnit4는 Third party library를 사용해야만 사용 가능하다.

## 문자열을 매개변수로 테스트 반복하기
### 코드
```
@ParameterizedTest
@ValueSource(strings = {"날씨가", "많이", "추워지고", "있네요."})
void parameterizedTest(String message) {
    System.out.println(message);
}
```

### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/4.PNG)   
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/5.PNG)   
선언해 놓은 문자열을 하나씩 매개변수로 사용하며 반복한다.

## DisplayName 커스터마이징 하기
### 코드
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(strings = {"날씨가", "많이", "추워지고", "있네요."})
void parameterizedTest(String message) {
    System.out.println(message);
}
```
* {index}: 1번부터 1씩 증가
* {displayName}: 설정되어 있는 displayName
* {0}: 테스트마다 첫번째 매개변수 값 (위 코드에서는 테스트마다 문자열 1개씩만 매개변수로 사용되기 때문에 0번 데이터만 존재)

### 결과
![결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/6.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)