### \@BeforeAll
해당 클래스의 테스트가 실행되기 전에 딱 1번 실행 되며, 반드시 static void로 사용해야 한다. 

### \@AfterAll
해당 클래스의 모든 테스트가 실행된 이후에 딱 1번 실행되며, 반드시 static void로 사용해야 한다.

### \@BeforeEach
각 테스트가 실행되기 전에 한번씩 호출 된다.

### \@AfterEach
각 테스트가 실행된 후에 한번씩 호출 된다.

### \@Disabled
해당 테스트를 실행하지 않는다.

## 코드
```
package me.smpark.inflearnthejavatest;

import static org.junit.jupiter.api.Assertions.assertNotNull;

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.Test;

class StudyTest {

	@Test
	void create() {
		Study study = new Study();
		assertNotNull(study);
		System.out.println("create");
	}
	
	@Test
	@Disabled
	void create1() {
		System.out.println("create1");
	}
	
	@BeforeAll
	static void beforeAll() {
		System.out.println("before all");
	}
	
	@AfterAll
	static void afterAll() {
		System.out.println("after all");
	}
	
	@BeforeEach
	void beforeEach() {
		System.out.println("before each");
	}
	
	@AfterEach
	void afterEach() {
		System.out.println("after each");
	}
	
}
```

## 실행 결과
![실행결과](https://raw.githubusercontent.com/smpark1020/tistory-smpark1020/master/images/%5B%EA%B8%B0%EB%B3%B8%EC%95%A0%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%5D1.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)