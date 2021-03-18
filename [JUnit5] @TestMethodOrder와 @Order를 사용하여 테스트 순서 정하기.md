테스트 메소드는 특정한 순서에 의해 실행되지만 어떻게 그 순서를 정하는지는 분명하지 않다. 따라서 이 순서에 의존하면 안된다.

하지만 경우에 따라 내가 원하는 순서에따라 테스트를 진행하고 싶을 경우도 있다. 이때 \@TestMethodOrder(MethodOrderer.OrderAnnotation.class)와 \@Order를 사용하여 테스트 순서를 정할 수 있다.

## 기본 순서
### 결과
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/1.PNG)   
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/2.PNG)   
어떠한 내부 로직에 의해 순서가 정해진다.

## \@TestMethodOrder(MethodOrderer.OrderAnnotation.class)와 \@Order 사용
### 코드
```
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
@TestInstance(Lifecycle.PER_CLASS)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {
	
int value = 1;

@Order(2)
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(this);
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Order(1)
@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println(this);
    System.out.println("create1 " + value++);
}

@Order(3)
@DisplayName("스터디 만들기")
@RepeatedTest(value = 10, name = "{displayName}, {currentRepetition}/{totalRepetitions}")
void repeatTest(RepetitionInfo repeatitionInfo) {
    System.out.println("test " + repeatitionInfo.getCurrentRepetition() + "/" + repeatitionInfo.getTotalRepetitions());
}

@Order(4)
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(@AggregateWith(StudyAggregator.class) Study study) {
    System.out.println(study);
}

...

}
```

### 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/3.PNG)   
\@Order의 값이 낮을수록 우선순위가 높다.

## \@Order의 값이 같을 경우
### 코드
```
@Order(1)
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(this);
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Order(1)
@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println(this);
    System.out.println("create1 " + value++);
}
```
### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/4.PNG)   
만약 \@Order의 숫자가 같다면 어떠한 로직에 의해 순서가 정해진다.
테스트할때는 먼저 작성된게 먼저 실행되고 있다.

이때 꼭 \@TestInstance(Lifecycle.PER_CLASS)와 같이 사용하지 않아도 된다.
하지만 이럴 경우 \@BeforeAll과 \@AfterAll은 반드시 static 메서드여야 한다.
## \@BeforeAll과 \@AfterAll이 static 메서드가 아닐 경우
### 코드
```
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {
	
...

@BeforeAll
void beforeAll() {
    System.out.println("before all");
}

@AfterAll
void afterAll() {
    System.out.println("after all");
}

...

}
```
### 결과
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/5.PNG)

## \@BeforeAll과 \@AfterAll이 static 메서드일 경우
### 코드
```
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {
	
int value = 1;

@Order(2)
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(this);
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Order(1)
@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println(this);
    System.out.println("create1 " + value++);
}

@Order(3)
@DisplayName("스터디 만들기")
@RepeatedTest(value = 10, name = "{displayName}, {currentRepetition}/{totalRepetitions}")
void repeatTest(RepetitionInfo repeatitionInfo) {
    System.out.println("test " + repeatitionInfo.getCurrentRepetition() + "/" + repeatitionInfo.getTotalRepetitions());
}

@Order(4)
@DisplayName("스터디 만들기")
@ParameterizedTest(name = "{index} {displayName} message={0}")
@CsvSource({"10, '자바 스터디'", "20, 스프링"})
void parameterizedTest(@AggregateWith(StudyAggregator.class) Study study) {
    System.out.println(study);
}

static class StudyAggregator implements ArgumentsAggregator {

    @Override
    public Object aggregateArguments(ArgumentsAccessor accessor, ParameterContext context)
            throws ArgumentsAggregationException {
        return new Study(accessor.getInteger(0), accessor.getString(1));
    }
    
}

static class StudyConverter extends SimpleArgumentConverter {

    @Override
    protected Object convert(Object source, Class<?> targetType) throws ArgumentConversionException {
        assertEquals(Study.class, targetType, "Can only convert to Study");
        return new Study(Integer.parseInt(source.toString()));
    }
    
}

@BeforeAll
static void beforeAll() {
    System.out.println("before all");
}

@AfterAll
static void afterAll() {
    System.out.println("after all");
}

...

}
```
### 결과
![6](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%88%9C%EC%84%9C/6.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)