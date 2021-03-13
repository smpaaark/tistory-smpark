### 코드
```
int value = 1;
	
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    System.out.println(value++);
    Study actual = new Study(1);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println("create1 " + value++);
}
```

### 결과
![1]()   
어느 한 테스트에서는 value값이 2가 찍힐 것 같지만 둘 다 1만 찍혔다.

### 코드
```
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
```

### 결과
![2]()   
출력된 this 인스턴스 값이 다르다.   
이것은 JUnit 기본 전략으로 테스트 마다 해당 테스트 클래스의 인스턴스를 새로 만들게 되어있기 때문이다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)