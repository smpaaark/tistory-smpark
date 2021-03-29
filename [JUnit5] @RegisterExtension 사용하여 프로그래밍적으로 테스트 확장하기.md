이전 글에 이어서 만약 THRESHOLD 값을 생성자를 통해 받도록 코드를 수정한다면
\@ExtendWith를 사용하는 코드는 에러가 발생하게 된다.
즉, 커스터마이징을 할 수 없다.   
이를 해결하기 위해서는 \@RegisterExtension를 프로그래밍적으로 사용하면 된다. 

## THRESHOLD 값을 생성자를 통해 받도록 코드 수정
### 코드
```
public class FindSlowTestExtension implements BeforeTestExecutionCallback, AfterTestExecutionCallback {
	
	private long THRESHOLD;
	
	public FindSlowTestExtension(long tHRESHOLD) {
		THRESHOLD = tHRESHOLD;
	}
    ...
}
```

### 결과
![4](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%99%95%EC%9E%A5%20%EB%AA%A8%EB%8D%B8/4.PNG)
\@ExtendWith를 사용하면 디폴트 생성자로 클래스를 생성하기 때문에 에러가 발생한다.

## \@RegisterExtension 사용하는 것으로 테스트 코드 수정
### 코드
```
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class StudyTest {
	
	int value = 1;
	
	@RegisterExtension
	static FindSlowTestExtension findSlowTestExtension = new FindSlowTestExtension(1000L);

	...
}
```
### 결과
![5](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%99%95%EC%9E%A5%20%EB%AA%A8%EB%8D%B8/5.PNG)

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)