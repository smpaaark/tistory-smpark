\@ExtendWith를 사용하여 선언적으로 확장팩을 등록 할 수있다.

## 오래걸리는 테스트 찾기
### 코드
```
public class FindSlowTestExtension implements BeforeTestExecutionCallback, AfterTestExecutionCallback {
	
	private static final long THRESHOLD = 1000L;
	
	@Override
	public void beforeTestExecution(ExtensionContext context) throws Exception {
		ExtensionContext.Store store = getStore(context);
		store.put("START_TIME", System.currentTimeMillis());
	}

	@Override
	public void afterTestExecution(ExtensionContext context) throws Exception {
		String testMethodName = context.getRequiredTestMethod().getName();
		ExtensionContext.Store store = getStore(context);
		long start_time = store.remove("START_TIME", long.class);
		long duration = System.currentTimeMillis() - start_time;
		if (duration > THRESHOLD) {
			System.out.printf("Please consider mark method [%s] with @SlowTest.\n", testMethodName);
		}
	
	}
	
	private ExtensionContext.Store getStore(ExtensionContext context) {
		String testClassName = context.getRequiredTestClass().getName();
		String testMethodName = context.getRequiredTestMethod().getName();
		ExtensionContext.Store store = context.getStore(ExtensionContext.Namespace.create(testClassName, testMethodName));
		return store;
	}

}
```
* FindSlowTestExtension 클래스 정의
* BeforeTestExecutionCallback: 테스트가 실행되기 전에 수행
* AfterTestExecutionCallback: 테스트가 실행된 후 수행
* 각 테스트가 1초보다 오래걸릴 경우 \@SlowTest 애노테이션을 추가하라는 메시지를 출력한다.

```
@ExtendWith(FindSlowTestExtension.class)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {
    ...
}
```
테스트 클래스에 \@ExtendWith(FindSlowTestExtension.class) 추가

```
@Order(1)
@SlowTest
@DisplayName("스터디 만들기 slow")
@Disabled
void create_new_study_again() throws InterruptedException {
    Thread.sleep(1005L);
    System.out.println(this);
    System.out.println("create1 " + value++);
}
```
테스트 메서드가 1초 넘게 걸리도록 수정

### 결과
![1](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%99%95%EC%9E%A5%20%EB%AA%A8%EB%8D%B8/1.PNG)


## 이미 \@SlowTest가 붙어있는 경우에는 예외 처리
### 코드
```
@Override
public void afterTestExecution(ExtensionContext context) throws Exception {
    Method requiredTestMethod = context.getRequiredTestMethod();
    SlowTest annotation = requiredTestMethod.getAnnotation(SlowTest.class);
    String testMethodName = requiredTestMethod.getName();
    ExtensionContext.Store store = getStore(context);
    long start_time = store.remove("START_TIME", long.class);
    long duration = System.currentTimeMillis() - start_time;
    if (duration > THRESHOLD && annotation == null) {
        System.out.printf("Please consider mark method [%s] with @SlowTest.\n", testMethodName);
    }
}
```

### 결과
![2](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%99%95%EC%9E%A5%20%EB%AA%A8%EB%8D%B8/2.PNG)   
이미 애노테이션이 붙어있으므로 메시지가 출력되지 않는다. ("오래걸리는 테스트 찾기"의 테스트 코드 참고)

## \@SlowTest가 붙어 있지 않은 경우
### 코드
```
@Order(1)
@Test
@DisplayName("스터디 만들기 slow")
@Disabled
void create_new_study_again() throws InterruptedException {
    Thread.sleep(1005L);
    System.out.println(this);
    System.out.println("create1 " + value++);
}
```
### 결과
![3](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%99%95%EC%9E%A5%20%EB%AA%A8%EB%8D%B8/3.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)