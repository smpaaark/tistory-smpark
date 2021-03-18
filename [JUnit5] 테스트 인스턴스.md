JUnit 기본 전략으로 테스트 마다 해당 테스트 클래스의 인스턴스를 새로 만들게 되어있다. 이유는 테스트간의 의존성을 없애기 위해서이다. 만약 테스트 인스턴스가 1개만 생성된다면 테스트 순서에 따라 공유하는 값들이 바뀌게되니까 매우 불안정하다.   
테스트 순서는 예측할 수 없다. JUnit5부터는 선언되는 순서대로 실행되긴 하지만 매번 그런다고 생각하면 안된다.

## 공유하는 값 변화 확인
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
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4/1.PNG)   
어느 한 테스트에서는 value값이 2가 찍힐 것 같지만 둘 다 1만 찍혔다.

## 테스트 인스턴스 확인
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
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4/2.PNG)   
출력된 this 인스턴스 값이 다르다.   

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)