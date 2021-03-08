커스텀 태그를 만들어서 사용할 수 있다.

### 애노테이션 추가
\@FastTest
```
package me.smpark.inflearnthejavatest;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Test
@Tag("fast")
public @interface FastTest {

}
```

\@SlowTest
```
package me.smpark.inflearnthejavatest;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Test
@Tag("slow")
public @interface SlowTest {

}
```
* \@Retention(RetentionPolicy.RUNTIME): 이 애노테이션을 사용한 코드가 이 애노테이션 정보를 런타임까지도 유지해야한다.
* \@Target(ElementType.METHOD): 이 애노테이션은 메서드에 쓸 수 있다.

### 기존 테스트 코드
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

### 커스텀 태그 사용 테스트 코드
```
@FastTest
@DisplayName("스터디 만들기 fast")
void create_new_study() {
    Study actual = new Study(100);
    assertThat(actual.getLimit()).isGreaterThan(0);
}

@SlowTest
@DisplayName("스터디 만들기 slow")
void create_new_study_again() {
    System.out.println("create1");
}
```
기존 방식의 "fast"나 "slow"가 문자열이기 때문에 오타가 발생하는 문제를 방지할 수 있다. 즉, 더 type safe한 코딩이다.

### 결과
![fast 태그 테스트 실행 결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%BB%A4%EC%8A%A4%ED%85%80%20%ED%83%9C%EA%B7%B8/1.PNG)   
fast 태그만 실행되게 설정 후 테스트 실행한 결과

![default 메이븐 테스트 결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%BB%A4%EC%8A%A4%ED%85%80%20%ED%83%9C%EA%B7%B8/2.PNG)   
default 프로파일 메이븐 테스트 결과

![ci 프로파일 메이븐 테스트 결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%EC%BB%A4%EC%8A%A4%ED%85%80%20%ED%83%9C%EA%B7%B8/3.PNG)   
ci 프로파일 메이븐 테스트 결과

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)