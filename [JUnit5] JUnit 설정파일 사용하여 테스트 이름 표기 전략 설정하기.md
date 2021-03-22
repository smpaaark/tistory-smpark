JUnit 설정파일(junit-platform.properties)을 사용하여 테스트 이름 표기 전략을 설정할 수 있다. 추가로, 테스트 메서드에 \@DisplayName을 설정하면 \@DisplayName의 우선순위가 더 높다.

## Default 테스트 이름 표기 전략 설정
### 코드
```
junit.jupiter.displayname.generator.default = \
    org.junit.jupiter.api.DisplayNameGenerator$ReplaceUnderscores
```
junit-platform.properties에 위 코드 추가
* \: 줄바꿈

```
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {

    int value = 1;

    @Order(2)
    @FastTest
    void create_new_study() {
        System.out.println(this);
        System.out.println(value++);
        Study actual = new Study(1);
        assertThat(actual.getLimit()).isGreaterThan(0);
    }

    ...

}
```
\@DisplayName 설정하지 않은 테스트 메서드

### 결과
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20junit-platform.properties/5.PNG)   
언더바```_```가 공백 문자로 변경되어 표시되는 것 확인

## \@DisplayName 설정
### 코드
```
@Order(2)
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(this);
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}
```

### 결과
![6](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20junit-platform.properties/6.PNG)


## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)