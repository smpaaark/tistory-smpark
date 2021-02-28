assertTimeout과 assertTimeoutPreemptively 둘 다 어떠한 작업이 해당 시간안에 끝나야 성공하는 Assertion이다.

* assertTimeout 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    assertTimeout(Duration.ofMillis(100), () -> {
        new Study(10);
        Thread.sleep(300);
    });
}
```

* 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/4.PNG)

* assertTimeoutPreemptively 코드
```
@Test
@DisplayName("스터디 만들기 😁😁")
void create_new_study() {
    assertTimeoutPreemptively(Duration.ofMillis(100), () -> {
        new Study(10);
        Thread.sleep(300);
    });
}
```

* 결과
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%9E%90%EC%A3%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20Assertion/5.PNG)

## 차이점
두 코드 모두 실행 결과가 100 millisecond 보다 오래걸려서 테스트 결과가 실패이다. 하지만 결과를 자세히 비교하면 assertTimeout은 테스트 하는데 332 millisecond가 걸렸고, assertTimeoutPreemptively는 168 millisecond가 걸렸다.   
   
즉, assertTimeout을 사용하면 전체 테스트 시간이 소요되고, assertTimeoutPreemptively를 사용하면 기대한 시간 초과 시 바로 테스트가 실패하며 끝나게 된다.   
   
그렇다고 무조건 assertTimeoutPreemptively를 사용하면 안된다고 한다. 그 이유는 ThreadLocal과 관련이 있는데 예를 들면 트랜잭션이 걸려있는 테스트일 경우 트랜잭션이 정상 작동하지 않을수도 있다고 한다. 이부분은 나중에 좀 더 자세히 공부하기로...

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)