ArgumentsAggregator 인터페이스를 구현하여 **여러개의 매개변수** 값을 객체로 받아서 테스트할 수 있다.

## ArgumentsAggregator 인터페이스 구현
### 코드
```
static class StudyAggregator implements ArgumentsAggregator {

    @Override
    public Object aggregateArguments(ArgumentsAccessor accessor, ParameterContext context)
            throws ArgumentsAggregationException {
        return new Study(accessor.getInteger(0), accessor.getString(1));
    }
    
}
```
이때 구현할 클래스는 반드시 public class이거나 static inner class여야 한다.

## 구현한 StudyAggregator를 사용하여 Study 객체로 매개변수 받기
### 코드
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(@AggregateWith(StudyAggregator.class) Study study) {
    System.out.println(study);
}
```
반드시 받을 객체 타입 앞에 **@AggregateWith(StudyAggregator.class)**를 선언해야 한다.

### 결과
![8](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%202%EB%B6%80/9.PNG)   

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)