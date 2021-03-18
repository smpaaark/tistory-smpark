\@TestInstance(Lifecycle.PER_CLASS)를 사용하면 테스트 클래스당 인스턴스가 하나만 생성된다. 이렇게 되면 \@BeforeAll, \@AfterAll을 static으로 정의하지 않아도 된다.

## 테스트 인스턴스 확인
### 코드
```
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
@TestInstance(Lifecycle.PER_CLASS)
class StudyTest {

int value = 1;

@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(this);
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println(this);
    System.out.println("create1 " + value++);
}

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
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4/3.PNG)   
value값이 공유되어 증가되었고, this 인스턴스 값이 같다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)