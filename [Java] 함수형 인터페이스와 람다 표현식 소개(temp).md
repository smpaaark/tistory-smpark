```
package me.smpark.java8to11;

public interface RunSomething {

	void doIt();
	
}
```
함수형 인터페이스이다.

```
package me.smpark.java8to11;

public interface RunSomething {

	void doIt();
	
	void doItAgain();
	
}
```
함수형 인터페이스가 아니다.

```
package me.smpark.java8to11;

public interface RunSomething {

	abstract void doIt();
	
}
```
abstract 생략 가능하다.

```
package me.smpark.java8to11;

public interface RunSomething {

	void doIt();
	
	static void printName() {
		System.out.println("smpark");
	}
	
	default void printAge() {
		System.out.println("31");
	}
	
}
```
이거도 함수형 인터페이스이다. 다른 형태의 메서드가 있는건 중요하지 않고 오로지 함수형 메서드가 몇개 있냐가 중요하다.

```
@FunctionalInterface
public interface RunSomething {

	void doIt();
	
}
```
함수형 인터페이스에 명시를 해주면

![추상 메서드 2개 선언 시 에러]()

java 8 이전
```
public class Foo {
	
	public static void main(String[] args) {
		// 익명 내부 클래스 anonymous inner class
		RunSomething runSomething = new RunSomething() {
			@Override
			public void doIt() {
				// TODO Auto-generated method stub
				
			}
		};
	}
	
}
```
익명 내부 클래스(anonymous inner class)로 객체 생성

```
public static void main(String[] args) {
    RunSomething runSomething = () -> System.out.println("Hello");
}
```
람다식 사용

메서드 내부 로직이 두 줄 이상일 경우
```
public static void main(String[] args) {
    // 익명 내부 클래스 anonymous inner class
    RunSomething runSomething = new RunSomething() {
        @Override
        public void doIt() {
            // TODO Auto-generated method stub
            System.out.println("Hello");
            System.out.println("Lambda");
        }
    };
}
```

람다식 표현
```
public static void main(String[] args) {
    RunSomething runSomething = () -> {
        // TODO Auto-generated method stub
        System.out.println("Hello");
        System.out.println("Lambda");
    };
}
```

실행
```
public static void main(String[] args) {
    RunSomething runSomething = () -> System.out.println("Hello");
    runSomething.doIt();
}
```
![결과이미지]()

추상 메서드 변경
```
int doIt(int number);
```

함수형 인터페이스의 파라미터가 같으면 결과도 같아야 한다.
```
public static void main(String[] args) {
    RunSomething runSomething = (number) -> {
        return number + 10;
    };
    
    System.out.println(runSomething.doIt(1));
    System.out.println(runSomething.doIt(1));
    System.out.println(runSomething.doIt(1));

    System.out.println(runSomething.doIt(2));
    System.out.println(runSomething.doIt(2));
    System.out.println(runSomething.doIt(2));
}
```
![결과]()

순수함수(pure function)
함수 밖에 있는 값을 참조하거나 변경하려하면 안된다.
오로지 함수 내부에서 사용하는 값, 함수가 전달받은 파라미터만 사용해야 한다.
```
public static void main(String[] args) {
    int baseNumber = 10;
    RunSomething runSomething = number -> number + baseNumber;
}
```
이런 코드는 순수함수라 할 수 없다.

