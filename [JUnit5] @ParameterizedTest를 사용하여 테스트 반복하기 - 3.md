\@ValueSource를 이용하여 문자열 뿐만 아니라 int, char, boolean 등 여러 타입을 매개변수로 사용할 수 있다.   
또한, \@CsvSource를 이용하여 매개변수 여러개를 받아 테스트를 반복할 수 있다.

## int형 매개변수 테스트
### 코드
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(ints = {10, 20, 40})
void parameterizedTest(Integer limit) {
    System.out.println(limit);
}
```
### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%202%EB%B6%80/2.PNG)   

## \@CsvSource 이용하여 매개변수 여러개 사용하는 테스트
### 코드
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(Integer limit, String name) {
    Study study = new Study(limit, name);
    System.out.println(study);
}
```
* ```" "```: 쌍따옴표 기준으로 1개의 테스트이다.
* ```,```: ```,```를 기준으로 매개변수가 구분된다.

### 결과
![7](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%202%EB%B6%80/7.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)