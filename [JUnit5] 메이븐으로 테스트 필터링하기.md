메이븐을 이용하여 테스트 필터링을 할 수 있다.

### 메이븐 테스트 실행 결과
![메이븐 빌드 테스트 시행 후 결과 이미지](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/4.PNG)
2개 모두 실행된다.

### 메이븐 코드 추가 (pom.xml)
```
<profiles>
    <profile>
        <id>default</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
        <build>
            <plugins>
                <plugin>
                    <artifactId>maven-surefire-plugin</artifactId>
                    <configuration>
                        <groups>fast</groups>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </profile>
</profiles>
```
default 프로파일일 경우 fast만 실행되도록 설정

### 결과
![메이븐 빌드 테스트 시행 후 결과 이미지](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/5.PNG)
fast 테스트 1개만 실행된다.

### ci 프로파일 추가
```
<profile>
    <id>ci</id>
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
                <configuration>
                    <groups>fast | slow</groups>
                </configuration>
            </plugin>
        </plugins>
    </build>
</profile>
```
또는
```
<profile>
    <id>ci</id>
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</profile>
```

### 결과
![모든 테스트 실행된 이미지](https://raw.githubusercontent.com/smpark1020/tistory-smpark/master/images/%5BJUnit5%5D%20%ED%83%9C%EA%B9%85%EA%B3%BC%20%ED%95%84%ED%84%B0%EB%A7%81/6.PNG)
fast, slow 2개 테스트 모두 실행된다.

## Reference
* [더 자바, 애플리케이션을 테스트하는 다양한 방법](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B8%ED%84%B0%EB%B7%B0?inst=9746dbc4)