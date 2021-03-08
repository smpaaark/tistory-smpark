\@Tag를 이용하여 원하는 테스트 그룹만 테스트를 실행할 수 있다.

### 코드
```
@Test
@DisplayName("스터디 만들기 fast")
@Tag("fast")
void create_new_study() {
    Study actual = new Study(100);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@Test
@DisplayName("스터디 만들기 slow")
@Tag("slow")
void create_new_study_again() {
    System.out.println("create1");
}
```

### 결과(두 태그 모두 실행 됨)
![두개 모두 실행됨](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/1.PNG)   

### 이클립스에 태그 조건 추가하여 필터링
![태그추가](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/2.PNG)

### 결과(fast 태그 걸린 테스트만 실행됨)
![fast만 실행된 결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/3.PNG)   

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)