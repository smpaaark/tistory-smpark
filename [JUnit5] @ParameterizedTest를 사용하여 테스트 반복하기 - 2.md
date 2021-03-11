빈값이나 Null 값으로 테스트를 반복할 수 있다. 

## 빈값과 Null 값 매개변수 테스트
### 코드
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(strings = {"날씨가", "많이", "추워지고", "있네요."})
@EmptySource
@NullSource
void parameterizedTest(String message) {
    System.out.println(message);
}
```
* \@EmptySource: 매개 변수로 빈값을 전달한다.
* \@NullSource: 매개 변수로 Null을 전달한다.
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(strings = {"날씨가", "많이", "추워지고", "있네요."})
@NullAndEmptySource
void parameterizedTest(String message) {
    System.out.println(message);
}
```
* \@NullAndEmptySource: 매개 변수로 빈값과 Null을 전달한다.

### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%202%EB%B6%80/1.PNG)   
위 두 코드의 결과는 같다.

## \@NullAndEmptySource 코드 내부 확인
### 코드
```
@Target({ ElementType.ANNOTATION_TYPE, ElementType.METHOD })
@Retention(RetentionPolicy.RUNTIME)
@Documented
@API(status = STABLE, since = "5.7")
@NullSource
@EmptySource
public @interface NullAndEmptySource {
}
```
\@NullSource와 \@EmptySource가 선언되어 있는 것을 확인할 수 있다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)