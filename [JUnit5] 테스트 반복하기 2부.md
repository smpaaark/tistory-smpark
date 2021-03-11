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
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(strings = {"날씨가", "많이", "추워지고", "있네요."})
@NullAndEmptySource
void parameterizedTest(String message) {
    System.out.println(message);
}
```
![결과 같다]()

@NullAndEmptySource 내부 코드
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

```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(ints = {10, 20, 40})
void parameterizedTest(Integer limit) {
    System.out.println(limit);
}
```
![결과]()

SimpleArgumentConverter 상속 받은 클래스 구현
```
static class StudyConverter extends SimpleArgumentConverter {

    @Override
    protected Object convert(Object source, Class<?> targetType) throws ArgumentConversionException {
        assertEquals(Study.class, targetType, "Can only convert to Study");
        return new Study(Integer.parseInt(source.toString()));
    }
    
}
```
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@ValueSource(ints = {10, 20, 40})
void parameterizedTest(@ConvertWith(StudyConverter.class) Study study) {
    System.out.println(study.getLimit());
}
```
![3]()

```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(Integer limit, String name) {
    Study study = new Study(limit, name);
    System.out.println(study);
}
```
![4]()

```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(ArgumentsAccessor argumentsAccessor) {
    Study study = new Study(argumentsAccessor.getInteger(0), argumentsAccessor.getString(1));
    System.out.println(study);
}
```
![5]()

```
static class StudyAggregator implements ArgumentsAggregator {

    @Override
    public Object aggregateArguments(ArgumentsAccessor accessor, ParameterContext context)
            throws ArgumentsAggregationException {
        return new Study(accessor.getInteger(0), accessor.getString(1));
    }
    
}
```
```
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(@AggregateWith(StudyAggregator.class) Study study) {
    System.out.println(study);
}
```
![6]()

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)