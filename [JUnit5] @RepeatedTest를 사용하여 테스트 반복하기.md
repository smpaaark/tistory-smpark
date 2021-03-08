## 테스트 10번 반복하기
### 코드
```
@RepeatedTest(10)
void repeatTest() {
    System.out.println("test");
}
```

### 결과
![결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/1.PNG)

## RepetitionInfo 파라미터 이용하기
### 코드
```
@RepeatedTest(10)
void repeatTest(RepetitionInfo repeatitionInfo) {
    System.out.println("test " + repeatitionInfo.getCurrentRepetition() + "/" + repeatitionInfo.getTotalRepetitions());
}
```
* getCurrentRepetition: 현재 몇번째 반복 수행 중인지
* getTotalRepetitions: 총 반복할 횟수

### 결과
![결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/2.PNG)

## DisplayName 커스터마이징 하기
### 코드
```
@DisplayName("스터디 만들기")
@RepeatedTest(value = 10, name = "{displayName}, {currentRepetition}/{totalRepetitions}")
void repeatTest(RepetitionInfo repeatitionInfo) {
    System.out.println("test " + repeatitionInfo.getCurrentRepetition() + "/" + repeatitionInfo.getTotalRepetitions());
}
```
* {displayName}: 설정되어 있는 displayName
* {currentRepetition}: 현재 몇번째 반복 수행 중인지
* {totalRepetitions}: 총 반복할 횟수

### 결과
![결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EB%B0%98%EB%B3%B5%ED%95%98%EA%B8%B0%201%EB%B6%80/3.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)