## 기본 JUnit 테스트 이름 표시
기본 테스트 이름은 메서드 이름이 출력된다. 보통 테스트 메서드 명은 언더바 ```_```를 많이 사용한다.

### 코드
```
@Test
void create_new_study() {
    Study study = new Study();
    assertNotNull(study);
    System.out.println("create");
}

@Test
void create_new_study_again() {
    System.out.println("create1");
}
```

### 결과
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%9D%B4%EB%A6%84%ED%91%9C%EC%8B%9C/1.PNG)

## \@DisplayNameGeneration
클래스와 메서드에 적용 가능하며, 클래스에 적용하면 모든 메서드에 적용된다. 또한, 전략에 해당하는 구현체 클래스를 입력할 수 있다.
* DisplayNameGenerator.ReplaceUnderscores.class   
=> 언더바를 빈 공간으로 바꿔서 표현해준다.

### 코드
```
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
class StudyTest {
```

### 결과
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%9D%B4%EB%A6%84%ED%91%9C%EC%8B%9C/2.PNG)

## \@DisplayName
한글, 공백, 이모티콘 등을 사용할 수 있으며, \@DisplayNameGeneration보다 권장되는 방법이다.

### 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    Study study = new Study();
    assertNotNull(study);
    System.out.println("create");
}
```

### 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%9D%B4%EB%A6%84%ED%91%9C%EC%8B%9C/3.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)