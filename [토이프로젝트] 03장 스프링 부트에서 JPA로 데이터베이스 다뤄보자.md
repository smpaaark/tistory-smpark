# 프로젝트에 Spring Data Jpa 적용하기
1. pom.xml에 spring-boot-starter-jpa와 h2 의존성을 등록합니다.
* spring-boot-starter-data-jpa
  * 스프링 부트용 Spring Data Jpa 추상화 라이브러리입니다.
  * 스프링 부트 버전에 맞춰 자동으로 JPA 관련 라이브러리들의 버전을 관리해 줍니다.

* h2
  * 인메모리 관계형 데이터베이스입니다.
  * 별도의 설치가 필요 없이 프로젝트 의존성만으로 관리할 수 있습니다.
  * 메모리에서 실행되기 때문에 애플리케이션을 재시작할 때마다 초기화된다는 점을 이용하여 테스트 용도로 많이 사용됩니다.
  * JPA의 테스트, 로컬 환경에서의 구동에서 사용할 예정입니다.

2. domain 패키지는 도메인을 담을 패키지입니다.
3. 어노테이션 순서는 주요 어노테이션을 클래스에 가깝게 둡니다.
4. Posts 클래스는 실제 DB의 테이블과 매칭될 클래스이며 보통 Entity 클래스라고도 합니다
* @Entity
  * 테이블과 링크될 클래스임을 나타냅니다.
  * 기본값으로 클래스의 카멜케이스 이름을 언더스코어 네이밍(_)으로 테이블 이름을 매칭합니다.
  * ex) SalesManager.java -> sales_manager table

* @Id
  * 해당 테이블의 PK 필드를 나타냅니다.

* @GeneratedValue
  * PK의 생성 규칙을 나타냅니다.
  * 스프링 부트 2.0 에서는 GenerationType.IDENTITY 옵션을 추가해야만 auto_increment가 됩니다.

* @Column
  * 테이블의 칼럼을 나타내며 굳이 선언하지 않더라도 해당 클래스의 필드는 모두 칼럼이 됩니다.
  * 사용하는 이유는, 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용합니다.
  * 문자열의 경우 VARCHAR(255)가 기본값인데, 사이즈를 500으로 늘리고 싶거나(ex:title), 타입을 TEXT로 변경하고 싶거나(ex:content) 등의 경우에 사용됩니다.

5. 웬만하면 Entity의 PK는 Long 타입의 Auto_increment를 추천합니다(MySQL 기준으로 이렇게 하면 bigint 타입이 됩니다)

6. 추가된 롬복 라이브러리의 어노테이션
* @NoArgConstructor
  * 기본 생성자 자동 추가
  * public Posts() {} 와 같은 효과

* @Getter
  * 클래스 내 모든 필드의 Getter 메소드를 자동생성

* @Builder
  * 해당 클래스의 빌더 패턴 클래스를 생성
  * 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함

7. Entity 클래스에서는 절대 Setter 메소드를 만들지 않습니다. 대신, 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야만 합니다.
8. 기본적인 구조는 빌더를 통해 최종값을 채운 후 DB에 삽입(insert)하는 것이며, 값 변경이 필요한 경우 해당 이벤트에 맞는 public 메소드를 호출하여 변경하는 것을 전제로 합니다.
9. Posts 클래스 생성이 끝났다면, Posts 클래스로 Database를 접근하게 해줄 JpaRepository를 생성합니다. JPA에선 Repository라고 부르며 인터페이스로 생성합니다. 단순히 인터페이스를 생성 후, JpaRepository<Entity 클래스, PK 타입>를 상속하면 기본적인 CRUD 메소드가 자동으로 생성됩니다. @Repository를 추가할 필요도 없습니다. 여기서 주의하실 점은 Entity 클래스와 기본 Entity Repository는 함께 위치해야 하는 점입니다. 나중에 프로젝트 규모가 커져 도메인별로 프로젝트를 분리해야 한다면 이때 Entity 클래스와 기본 Repository는 함께 움직여야 하므로 도메인 패키지에서 함께 관리합니다.

# Spring Data JPA 테스트 코드 작성하기
1. test 디렉토리에 domain.posts 패키지를 생성하고, 테스트 클래스는 PostsRepositoryTest란 이름으로 생성합니다.
* @After
  * JUnit에서 단위 테스트가 끝날 때마다 수행되는 메소드를 지정
  * 보통은 배포 전 전체 테스트를 수행할 때 테스트간 데이터 침범을 막기 위해 사용합니다.
  * 여러 테스트가 동시에 수행되면 테스트용 데이터베이스인 H2에 데이터가 그대로 남아 있어 다음 테스트 실행 시 테스트가 실패할 수 있습니다.

* postsRepository.save
  * 테이블 posts에 insert/update 쿼리를 실행합니다.
  * id 값이 있다면 update가, 없다면 insert 쿼리가 실행됩니다.

* postsRepository.findAll
  * 테이블 posts에 있는 모든 데이터를 조회해오는 메소드입니다.

2. 별다른 설정 없이 @SpringBootTest를 사용할 경우 H2 데이터베이스를 자동으로 실행해 줍니다.
3. application.properties에 한줄의 코드로 실행된 쿼리 로그를 확인할 수 있도록 설정할 수 있습니다.
4. src/main/resources 디렉토리 아래에 application.properties 파일을 생성합니다.
5. 아래 옵션을 작성합니다.
> spring.jpa.show_sql=true

6. H2는 MySQL의 쿼리를 수행해도 정상적으로 작동하기 때문에 이후 디버깅을 위해서 출력되는 쿼리 로그를 MySQL 버전으로 변경하겠습니다.
7. 이 옵션 역시 application.properties에서 설정이 가능합니다. 다음 코드를 추가합니다.
> spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
> spring.jpa.properties.hibernate.dialect.storage_engine=innodb   
> spring.datasource.hikari.jdbc-url=jdbc:h2:mem:testdb;MODE=MYSQL   
> spring.datasource.hikari.username=sa

# 등록/수정/조회 API 만들기
1. PostsApiController를 web 패키지에, PostsSaveRequestDto를 web.dto 패키지에, PostsService를 service.posts 패키지에 생성합니다.
2. 스프링에서 Bean을 주입받는 방식으로 가장 권장받는 방식이 생성자로 주입받는 방식입니다.(@Autowired는 권장하지 않습니다). 이것을 @RequiredArgsConstructor에서 해결해 줍니다. final이 선언된 모든 필드를 인자값으로 하는 생성자를 롬복의 @RequiredArgsConstructor가 대신 생성해 준 것입니다.
3. 이제 Controller와 Service에서 사용할 Dto 클래스를 생성하겠습니다.
4. @WebMvcTest의 경우 JPA 기능이 작동하지 않기 때문인데, Controller와 ControllerAdvice 등 외부 연동과 관련된 부분만 활성화되니 지금 같이 JPA 기능까지 한번에 테스트할 때는 @SpringBootTest와 TestRestTemplate을 사용하면 됩니다.
5. WebEnvironment.RANDOM_PORT로 인한 랜덤 포트 실행과 insert 쿼리가 실행된 것을 확인합니다.
6. PostsResponseDto는 Entity의 필드 중 일부만 사용하므로 생성자로 Entity를 받아 필드에 값을 넣습니다. 
7. update 기능에서 데이터베이스에 쿼리를 날리는 부분이 없습니다.
8. H2는 메모리에서 실행하기 때문에 직접 접근하려면 웹 콘솔을 사용해야만 합니다.
9. 먼저 웹 콘솔 옵션을 활성화 합니다. application.properties에 다음과 같이 옵션을 추가합니다.
> spring.h2.console.enabled=true
10. 여기서 웹 브라우저에 http://localhost:8080/h2-console로 접속하면 웹 콘솔 화면이 등장합니다.
11. 이때 JDBC URL은 application.properties에 설정한대로 jdbc:h2:mem:testdb;MODE=MYSQL로 되어있어야 합니다.
12. [Connect] 버튼을 클릭하면 현재 프로젝트의 H2를 관리할 수 있는 관리 페이지로 이동합니다.

# JPA Auditing으로 생성시간/수정시간 자동화하기
1. domain 패키지에 BaseTimeEntity 클래스를 생성합니다.
2. BaseTimeEntity클래스는 모든 Entity의 상위 클래스가 되어 Entity들의 createdDate, modifiedDate를 자동으로 관리하는 역할입니다.
* @MappedSuperclass
  * JPA Entity 클래스들이 BaseTimeEntity을 상속할 경우 필드들(createdDate, modifiedDate)도 컬럼으로 인식하도록 합니다.
* @EntityListeners(AuditingEntityListener.class)
  * BaseTimeEntity 클래스에 Auditing 기능을 포함시킵니다.
* @CreatedDate
  * Entity가 생성되어 저장될 때 시간이 자동 저장됩니다.
* @LastModifiedDate
  * 조회한 Entity의 값을 변경할 때 시간이 자동 저장됩니다.

3. 그리고 Posts 클래스가 BaseTimeEntity를 상속받도록 변경합니다.
4. 마지막으로 JPA Auditing 어노테이션들을 모두 활성화할 수 있도록 Application 클래스에 활성화 어노테이션 하나를 추가하겠습니다.
> @EnableJpaAuditing