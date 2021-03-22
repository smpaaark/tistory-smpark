JUnit 설정파일(junit-platform.properties)을 사용하여 \@Disabled를 무시하고 해당 테스트를 실행하게 할 수 있다.

## \@Disabled 적용 확인
### 코드
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

### 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20junit-platform.properties/3.PNG)   

## 설정파일에 코드 추가
### 코드
```
junit.jupiter.conditions.deactivate = org.junit.*DisabledCondition
```
junit-platform.properties에 위 코드 추가

### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20junit-platform.properties/4.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)