@Disabled를 추가하면 해당 테스트는 실행되지 않는다.
```
@Order(1)
@SlowTest
@DisplayName("스터디 만들기 slow")
@Disabled
void create_new_study_again() {
    System.out.println(this);
    System.out.println("create1 " + value++);
}
```
![3]()

```
junit.jupiter.conditions.deactivate = org.junit.*DisabledCondition
```
![4]()

```
junit.jupiter.displayname.generator.default = \
    org.junit.jupiter.api.DisplayNameGenerator$ReplaceUnderscores
```
\: 줄바꿈
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
![5]()
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
![6]()


## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)