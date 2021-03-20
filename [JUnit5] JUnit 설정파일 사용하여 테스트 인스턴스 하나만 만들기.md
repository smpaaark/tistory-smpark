JUnit 설정파일(junit-platform.properties)을 사용하여 각 테스트 클래스의 인스턴스를 하나만 만들게 설정할 수 있다.

### 코드
```
junit.jupiter.testinstance.lifecycle.default = per_class
```
junit-platform.properties에 위 코드 추가

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

    ...

}
```
value 값을 증가시키며 출력하는 테스트 코드

## 결과
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20junit-platform.properties/2.PNG)   
value 값이 1에서 2로 증가된 것 확인

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)