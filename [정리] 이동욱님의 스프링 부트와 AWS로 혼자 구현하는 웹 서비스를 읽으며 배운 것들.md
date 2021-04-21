## 서론
최근 이동욱님의 스프링 부트와 AWS로 혼자 구현하는 웹 서비스를 읽으며 배운 것들이 정말 많다. 특히 배민과 같은 대용량 트래픽이 발생하는 서비스 기업에서는 어떻게 개발하고 어떻게 서비스를 구축하는지 정말 많은 꿀팁을 배울 수 있었다. 그래서 이동욱님이 책 중간중간 알려주시는 요즘 서비스 기업에서는 어떻게 개발하는지에 대한 꿀팁을 정리해보려 한다.

# CHAPTER 1. 스프링 부트 시작하기
## 프로젝트 생성하기
artifactId는 프로젝트의 이름이 되기 때문에 원하는 이름을 작성해 주면 됩니다.   
groupId는 보통 기본 패키지명으로 사용됩니다. ex)com.smpark.book   
초기 프로젝트 생성할 시 기본이되는 dependency
* spring-boot-starter-web
* spring-boot-starter-test

## 깃과 깃허브 사용하기
프로젝트 실행시 자동으로 생성되는 파일들은 깃허브에 올릴 필요가 없습니다.   
따라서 프로젝트를 처음 세팅할 때는 올릴 필요가 있는 파일만 커밋하여 푸시합니다.   
깃에서 특정 파일 혹은 디렉토리를 관리 대상에서 제외할 때는 .gitignore 파일을 사용합니다.

# CHATPER 2. 스프링 부트에서 테스트 코드를 작성하자
## 테스트 코드 소개
JUnit을 사용합니다.   
아직 많은 회사에서 JUnit5보다는 JUnit4를 사용하고 있습니다.

## Hello Controller 테스트 코드 작성하기
일반적으로 패키지명은 웹 사이트 주소의 역순으로 합니다. 예를 들어 admin.jojoldu.com 이라는 사이트라면 패키지명은 com.jojoldu.admin으로 하면 됩니다.
메인 클래스 명은 보통 Application으로 합니다.

@SpringBootApplication으로 인해 스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정됩니다. 특히나 @SpringBootApplication이 있는 위치부터 설정을 읽어가기 때문에 이 클래스는 항상 프로젝트의 최상단에 위치해야만 합니다.

> 간혹 내장 WAS를 쓰면 성능상 이슈가 있지 않냐고 하시는 분들이 계십니다. 높은 트래픽의 서비스를 하는 회사들 모두 스프링 부트로 큰 문제 없이 운영하고 있습니다.

> 대표적인 WAS인 톰캣 역시 서블릿으로 이루어진 자바 애플리케이션입니다. 똑같은 코드를 사용하고 있으므로 성능상 이슈는 크게 고려하지 않아도 됩니다.

컨트롤러와 관련된 클래스들은 모두 web 패키지에 담습니다.
초기 프로젝트 세팅 테스트를 위해 HelloController를 만듭니다.

1. @RestController
* JSON을 반환하는 컨트롤러로 만들어 줍니다.
* 예전에는 @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해준다고 생각하면 됩니다.

2. @GetMapping
* HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줍니다.
* 예전에는 @RequestMapping(method = RequestMethod.GET)으로 사용되었습니다. 이제 이 프로젝트는 /hello로 요청이 오면 문자열 hello를 반환하는 기능을 가지게 되었습니다.

테스트 코드로 검증을 합니다. src/test/java 디렉토리에 앞에서 생성한 패키지를 그대로 다시 생성합니다.
일반적으로 테스트 클래스는 대상 클래스 이름에 Test를 붙입니다.

1. @RunWith(SpringRunner.class)
* 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킵니다.
* 여기서는 SpringRunner라는 스프링 실행자를 사용합니다.
* 즉, 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 합니다.

2. @WebMvcTest
* 여러 스프링 테스트 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션입니다.
* 선언할 경우 @Controller, @ControllerAdvice 등을 사용할 수 있습니다.
* 단, @Service, @Component, @Repository 등은 사용할 수 없습니다.
* 여기서는 컨트롤러만 사요아기 때문에 선언합니다.

3. @Autowired
* 스프링이 관리하는 빈(Bean)을 주입 받습니다.

4. private MockMvc mvc
* 웹API를 테스트할 때 사용합니다.
* 스프링 MVC 테스트의 시작점입니다.
* 이 클래스를 통해 HTTP, GET, POST 등에 대한 API 테스트를 할 수 있습니다.

5. mvc.perform(get("hello"))
* MockMvc를 통해 /hello 주소로 HTTP GET 요청을 합니다.
* 체이닝이 지원되어 아래와 같이 여러 검증 기능을 이어서 선언할 수 있습니다.

6. .andExpect(status().isOk())
* mvc.perform의 결과를 검증합니다.
* HTTP Header의 Status를 검증합니다.
* 우리가 흔히 알고 있는 200, 404, 500 등의 상태를 검증합니다.
* 여기선 OK 즉, 200인지 아닌지를 검증합니다.

7. .andExpect(content().string(hello))
* mvc.perform의 결과를 검증합니다.
* 응답 본문의 내용을 검증합니다.
* Controller에서 "hello"를 리턴하기 때문에 이 값이 맞는지 검증합니다.

브라우저로 한 번씩 검증은 하되, 테스트 코드는 꼭 작성해야 합니다. 그래야만 견고한 소프트웨어를 만드는 역량이 성장할 수 있습니다. 추가로, 절대 수동으로 검증하고 테스트 코드를 작성하진 않습니다. 테스트 코드로 먼저 검증 후, 정말 못 믿겠다는 생각이 들 땐 프로젝트를 실행해 확인한다는 점 명심해야 합니다.

## 롬복 소개 및 설치하기
롬복(Lombok)은 자바 개발자들의 필수 라이브러리 입니다.
pom.xml에 롬복을 추가합니다.
롬복은 프로젝트마다 설정해야 합니다. 

## HelloController 코드를 롬복으로 전환하기
롬복으로 변경하고 문제가 생기는지는 테스트 코드만 돌려보면 알 수 있습니다.
모든 응답 Dto는 web.dto 패키지에 추가합니다.
HelloResponseDto를 생성합니다.

1. @Getter
* 선언된 모든 필드의 get 메소드를 생성해 줍니다.

2. @RequiredArgsConstructor
* 선언된 모든 final 필드가 포함된 생성자를 생성해 줍니다.
* final이 없는 필드는 생성자에 포함되지 않습니다.

Dto에 적용된 롬복이 잘 작동하는지 테스트 코드를 통해 확인합니다.

1. assertThat
* assertj라는 테스트 검증 라이브러리의 검증 메소드입니다.
* 검증하고 싶은 대상을 메소드 인자로 받습니다.
* 메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있습니다.

2. isEqualTo
* assertj의 동등 비교 메소드입니다.
* assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공입니다.

여기서 Junit의 기본 assertThat이 아닌 assertj의 assertThat을 사용합니다.

HelloController에도 새로 만든 ResponseDto를 사용하도록 코드를 추가합니다.
1. @RequestParam
* 외부에서 API로 넘긴 파라미터를 가져오는 어노테이션입니다.
* 여기서는 외부에서 name (@RequestParam("name")) 이란 이름으로 넘긴 파라미터를 메소드 파라미터 name(String name)에 저장하게 됩니다.

추가된 API를 테스트하는 코드를 HelloControllerTest에 추가합니다.
1. param
* API 테스트할 때 사용될 요청 파라미터를 설정합니다.
* 단, 값은 String만 허용됩니다.
* 그래서 숫자/날짜 등의 데이터도 등록할 때는 문자열로 변경해야만 가능합니다.

2. jsonPath
* JSON 응답값을 필드별로 검증할 수 있는 메소드입니다.
* $를 기준으로 필드명을 명시합니다.
* 여기서는 name과 amount를 검증하니 $.name, $.amount로 검증합니다.

# CHATPER 3. 스프링 부트에서 JPA로 데이터베이스 다뤄보자
JPA를 프로젝트에 적용합니다.
아직 SI 환경에서는 Spring & MyBatis를 많이 사용하지만, 쿠팡, 우아한형제들, NHN(구 NHN Entertainment) 등 자사 서비스를 개발하는 곳에서는 SpringBoot & JPA를 전사 표준으로 사용하고 있습니다. 그 외 나머지 서비스 기업들 역시 기존 프로젝트 환경을 개편하시는 분들은 대부분 JPA를 선택하고 있습니다.

## JPA 소개
Spring에서 JPA를 사용할 때는 구현체들을 직접 다루진 않습니다. 구현체들을 좀 더 쉽게 사용하고자 추상화시킨 Spring Data JPA라는 모듈을 이용하여 JPA 기술을 다룹니다.
Hibernate를 쓰는 것과 Spring Data JPA를 쓰는 것 사이에는 큰 차이가 없습니다. 그럼에도 스프링 진영에서는 Spring Data JPA를 개발했고, 이를 권장하고 있습니다.

## 프로젝트에 Spring Data Jpa 적용하기
pom.xml에 spring-boot-starter-jpa와 h2 의존성을 등록합니다.
1. spring-boot-starter-data-jpa
* 스프링 부트용 Spring Data Jpa 추상화 라이브러리입니다.
* 스프링 부트 버전에 맞춰 자동으로 JPA 관련 라이브러리들의 버전을 관리해 줍니다.

2. h2
* 인메모리 관계형 데이터베이스입니다.
* 별도의 설치가 필요 없이 프로젝트 의존성만으로 관리할 수 있습니다.
* 메모리에서 실행되기 때문에 애플리케이션을 재시작할 때마다 초기화된다는 점을 이용하여 테스트 용도로 많이 사용됩니다.
* JPA의 테스트, 로컬 환경에서의 구동에서 사용할 예정입니다.

domain 패키지는 도메인을 담을 패키지입니다. 여기서 도메인이란 게시글, 댓글, 회원, 정산, 결제 등 소프트웨어에 대한 요구사항 혹은 문제 영역이라고 생각하면 됩니다.
기존에 MyBatis와 같은 쿼리 매퍼를 사용했다면 dao 패키지를 떠올리겠지만, dao 패키지와는 조금 결이 다르다고 생각하면 됩니다. 그간 xml에 쿼리를 담고, 클래스는 오로지 쿼리의 결과만 담던 일들이 모두 도메인 클래스라고 불리는 곳에서 해결됩니다.

어노테이션 순서는 주요 어노테이션을 클래스에 가깝게 둡니다.
@Entity는 JPA의 어노테이션이며, @Getter와 @NoArgsConstructor는 롬복의 어노테이션 입니다.
롬복은 코드를 단순화시켜 주지만 필수 어노테이션은 아닙니다. 그러다 보니 주요 어노테이션인 @Entity를 클래스에 가깝게 두고, 롬복 어노테이션을 그 위로 두었습니다. 이렇게 하면 이후에 코틀린 등의 새 언어 전환으로 롬복이 더 이상 필요 없을 경우 쉽게 삭제할 수 있습니다.

여기서 Posts 클래스는 실제 DB의 테이블과 매칭될 클래스이며 보통 Entity 클래스라고도 합니다. JPA를 사용하시면 DB 데이터에 작업할 경우 실제 쿼리를 날리기보다는, 이 Entity 클래스의 수정을 통해 작업합니다.

Posts 클래스에는 JPA에서 제공하는 어노테이션들이 몇 개 있습니다.
1. @Entity
* 테이블과 링크될 클래스임을 나타냅니다.
* 기본값으로 클래스의 카멜케이스 이름을 언더스코어 네이밍(_)으로 테이블 이름을 매칭합니다.
* ex) SalesManager.java -> sales_manager table

2. @Id
* 해당 테이블의 PK 필드를 나타냅니다.

3. @GeneratedValue
* PK의 생성 규칙을 나타냅니다.
* 스프링 부트 2.0 에서는 GenerationType.IDENTITY 옵션을 추가해야만 auto_increment가 됩니다.

4. @Column
* 테이블의 칼럼을 나타내며 굳이 선언하지 않더라도 해당 클래스의 필드는 모두 칼럼이 됩니다.
* 사용하는 이유는, 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용합니다.
* 문자열의 경우 VARCHAR(255)가 기본값인데, 사이즈를 500으로 늘리고 싶거나(ex:title), 타입을 TEXT로 변경하고 싶거나(ex:content) 등의 경우에 사용됩니다.

### 참고
웬만하면 Entity의 PK는 Long 타입의 Auto_increment를 추천합니다(MySQL 기준으로 이렇게 하면 bigint 타입이 됩니다). 주민등록번호와 같이 비즈니스상 유니크 키나, 여러키를 조합한 복합키로 PK를 잡을 경우 난감한 상황이 종종 발생합니다.
(1) FK를 맺을 때 다른 테이블에서 복합키 전부를 갖고 있거나, 중간 테이블을 하나 둬야 하는 상황이 발생합니다.
(2) 인덱스에 좋은 영향을 끼치지 못합니다.
(3) 유니크한 조건이 변경될 경우 PK 전체를 수정해야 하는 일이 발생합니다.
주민등록번호, 복합키 등은 유니크 키로 별도로 추가하시는 것을 추천드립니다.

추가된 롬복 라이브러리의 어노테이션
5. @NoArgConstructor
* 기본 생성자 자동 추가
* public Posts() {} 와 같은 효과

6. @Getter
* 클래스 내 모든 필드의 Getter 메소드를 자동생성

7. @Builder
* 해당 클래스의 빌더 패턴 클래스를 생성
* 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함

서비스 초기 구축 단계에선 테이블 설계(여기선 Entitiy 설계)가 빈번하게 변경되는데, 이때 롬복의 어노테이션들은 코드 변경량을 최소화시켜 주기 때문에 적극적으로 사용합니다.

Entity 클래스에서는 절대 Setter 메소드를 만들지 않습니다. 대신, 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야만 합니다.

기본적인 구조는 빌더를 통해 최종값을 채운 후 DB에 삽입(insert)하는 것이며, 값 변경이 필요한 경우 해당 이벤트에 맞는 public 메소드를 호출하여 변경하는 것을 전제로 합니다. 빌더를 사용하게 되면 어느 필드에 어떤 값을 채워야 할지 명확하게 인지할 수 있습니다.

Posts 클래스 생성이 끝났다면, Posts 클래스로 Database를 접근하게 해줄 JpaRepository를 생성합니다.
보통 ibatis나 MyBatis 등에서 Dao라고 불리는 DB Layer 접근자입니다. JPA에선 Repository라고 부르며 인터페이스로 생성합니다. 단순히 인터페이스를 생성 후, JpaRepository<Entity 클래스, PK 타입>를 상속하면 기본적인 CRUD 메소드가 자동으로 생성됩니다.
@Repository를 추가할 필요도 없습니다. 여기서 주의하실 점은 Entity 클래스와 기본 Entity Repository는 함께 위치해야 하는 점입니다. 둘은 아주 밀접한 관계이고, Entity 클래스는 기본 Repository 없이는 제대로 역할을 할 수가 없습니다.
나중에 프로젝트 규모가 커져 도메인별로 프로젝트를 분리해야 한다면 이때 Entity 클래스와 기본 Repository는 함께 움직여야 하므로 도메인 패키지에서 함께 관리합니다.

## Spring Data JPA 테스트 코드 작성하기
test 디렉토리에 domain.posts 패키지를 생성하고, 테스트 클래스는 PostsRepositoryTest란 이름으로 생성합니다.
1. @After
* JUnit에서 단위 테스트가 끝날 때마다 수행되는 메소드를 지정
* 보통은 배포 전 전체 테스트를 수행할 때 테스트간 데이터 침범을 막기 위해 사용합니다.
* 여러 테스트가 동시에 수행되면 테스트용 데이터베이스인 H2에 데이터가 그대로 남아 있어 다음 테스트 실행 시 테스트가 실패할 수 있습니다.

2. postsRepository.save
* 테이블 posts에 insert/update 쿼리를 실행합니다.
* id 값이 있다면 update가, 없다면 insert 쿼리가 실행됩니다.

3. postsRepository.findAll
* 테이블 posts에 있는 모든 데이터를 조회해오는 메소드입니다.

별다른 설정 없이 @SpringBootTest를 사용할 경우 H2 데이터베이스를 자동으로 실행해 줍니다.

application.properties에 한줄의 코드로 실행된 쿼리 로그를 확인할 수 있도록 설정할 수 있다.
src/main/resources 디렉토리 아래에 application.properties 파일을 생성합니다.

옵션은 다음과 같습니다.
> spring.jpa.show_sql=true

H2는 MySQL의 쿼리를 수행해도 정상적으로 작동하기 때문에 이후 디버깅을 위해서 출력되는 쿼리 로그를 MySQL 버전으로 변경하겠습니다.
이 옵션 역시 application.properties에서 설정이 가능합니다. 다음 코드를 추가합니다.
> spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
> spring.jpa.properties.hibernate.dialect.storage_engine=innodb   
> spring.datasource.hikari.jdbc-url=jdbc:h2:mem:testdb;MODE=MYSQL   
> spring.datasource.hikari.username=sa

## 등록/수정/조회 API 만들기
API를 만들기 위해 총 3개의 클래스가 필요합니다.
* Request 데이터를 받을 Dto
* API 요청을 받을 Controller
* 트랜잭션, 도메인 기능 간의 순서를 보장하는 Service

여기서 많은 분들이 오해하고 계신 것이, Service에서 비지니스 로직을 처리해야 한다는 것입니다. 하지만 전혀 그렇지 않습니다. Service는 트랜잭션, 도메인 간 순서 보장의 역할만 합니다.

비지니스 로직 처리는 Domain에서 해야합니다.

PostsApiController를 web 패키지에, PostsSaveRequestDto를 web.dto 패키지에, PostsService를 service.posts 패키지에 생성합니다.

스프링에서 Bean을 주입받는 방식으로 가장 권장받는 방식이 생성자로 주입받는 방식입니다.(@Autowired는 권장하지 않습니다). 즉, 생성자로 Bean 객체를 받도록 하면 @Autowired와 동일한 효과를 볼 수 있다는 것입니다.
이것을 @RequiredArgsConstructor에서 해결해 줍니다. final이 선언된 모든 필드를 인자값으로 하는 생성자를 롬복의 @RequiredArgsConstructor가 대신 생성해 준 것입니다.

이제 Controller와 Service에서 사용할 Dto 클래스를 생성하겠습니다.
여기서 Entity 클래스와 거의 유사한 형태임에도 Dto 클래스를 추가로 생성했습니다. 하지만, 절대로 Entity 클래스를 Request/Response 클래스로 사용해서는 안됩니다.

Entity 클래스는 데이터베이스와 맞닿은 핵심 클래스입니다. Entity 클래스를 기준으로 테이블이 생성되고, 스키마가 변경됩니다. 화면 변경은 아주 사소한 기능 변경인데, 이를 위해 테이블과 연결된 Entity 클래스를 변경하는 것은 너무 큰 변경입니다.

수많은 서비스 클래스나 비즈니스 로직들이 Entity 클래스를 기준으로 동작합니다. Entity 클래스가 변경되면 여러 클래스에 영향을 끼치지만, Request와 Response용 Dto는 View를 위한 클래스라 정말 자주 변경이 필요합니다.

View Layer와 DB Layer의 역할 분리를 철저하게 하는 게 좋습니다. 실제로 Controller에서 결괏값으로 여러 테이블을 조인해서 줘야 할 경우가 빈번하므로 Entity 클래스만으로 표현하기가 어려운 경우가 많습니다.

꼭 Entity 클래스와 Controller에서 쓸 Dto는 분리해서 사용해야 합니다.

이제 테스트 코드로 검증합니다.
테스트 패키지 중 web 패키지에 PostsApiControllerTest를 생성합니다.

API Controller를 테스트하는데 HelloController와 달리 @WebMvcTest를 사용하지 않았습니다. @WebMvcTest의 경우 JPA 기능이 작동하지 않기 때문인데, Controller와 ControllerAdvice 등 외부 연동과 관련된 부분만 활성화되니 지금 같이 JPA 기능까지 한번에 테스트할 때는 @SpringBootTest와 TestRestTemplate을 사용하면 됩니다.

WebEnvironment.RANDOM_PORT로 인한 랜덤 포트 실행과 insert 쿼리가 실행된 것을 확인합니다.

이제 수정/조회 기능도 빠르게 만들어 보겠습니다.

PostsResponseDto는 Entity의 필드 중 일부만 사용하므로 생성자로 Entity를 받아 필드에 값을 넣습니다. 굳이 모든 필드를 가진 생성자가 필요하진 않으므로 Dto는 Entity를 받아 처리합니다.

update 기능에서 데이터베이스에 쿼리를 날리는 부분이 없습니다. 이게 가능한 이유는 JPA의 영속성 컨텍스트 때문입니다.
영속성 컨텍스트란, 엔티티를 영구 저장하는 환경입니다. 일종의 논리적 개념으로 보시면 되며, JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에 포함되어 있냐 아니냐로 갈립니다.
JPA의 엔티티 매니저(EntityManager)가 활성화된 상태로(Spring Data Jpa를 쓴다면 기본 옵션) 트랜잭션 안에서 데이터베이스에서 데이터를 가져오면 이 데이터는 영속성 컨텍스트가 유지된 상태입니다.
이 상태에서 해당 데이터의 값을 변경하면 트랜잭션이 끝나는 시점에 해당 테이블에 변경분을 반영합니다. 즉, Entity 객체의 값만 변경하면 별도로 Update 쿼리를 날릴 피룡가 없다는 것입니다. 이 개념을 더티 체킹(dirty checking)이라고 합니다.

수정 기능도 테스트 코드로 검증합니다.

H2는 메모리에서 실행하기 때문에 직접 접근하려면 웹 콘솔을 사용해야만 합니다. 먼저 웹 콘솔 옵션을 활성화 합니다. application.properties에 다음과 같이 옵션을 추가합니다.
> spring.h2.console.enabled=true

추가한 뒤 Application 클래스의 main 메소드를 실행합니다. 정상적으로 실행됐다면 톰캣이 8080 포트로 실행됩니다. 여기서 웹 브라우저에 http://localhost:8080/h2-console로 접속하면 웹 콘솔 화면이 등장합니다.

이때 JDBC URL은 application.properties에 설정한대로 jdbc:h2:mem:testdb;MODE=MYSQL로 되어있어야 합니다. [Connect] 버튼을 클릭하면 현재 프로젝트의 H2를 관리할 수 있는 관리 페이지로 이동합니다.

POSTS 테이블이 정상적으로 노출되어야만 합니다.

## JPA Auditing으로 생성시간/수정시간 자동화하기
보통 엔티티(entitiy)에는 해당 데이터의 생성시간과 수정시간을 포함합니다. 언제 만들어졌는지, 언제 수정되었는지 등은 차후 유지보수에 있어 굉장히 중요한 정보이기 때문입니다. 그렇다 보니 매번 DB에 삽입(insert)하기 전, 갱신(update)하기 전에 날짜 데이터를 등록/수정하는 코드가 여기저기 들어가게 됩니다.

이런 단순하고 반복적인 코드가 모든 테이블과 서비스 메소드에 포함되어야 한다고 생각하면 어마어마하게 귀찮고 코드가 지저분해집니다. 그래서 이 문제를 해결하고자 JPA Auditing를 사용하겠습니다.

여기서부터는 날짜 타입을 사용합니다. Java8부터 LocalDate와 LocalDateTime이 등장했습니다. 그간 Java의 기본 날짜 타입인 Date의 문제점을 제대로 고친 타입이라 Java8일 경우 무조건 써야 한다고 생각하면 됩니다.

domain 패키지에 BaseTimeEntity 클래스를 생성합니다.

BaseTimeEntity클래스는 모든 Entity의 상위 클래스가 되어 Entity들의 createdDate, modifiedDate를 자동으로 관리하는 역할입니다.
1. @MappedSuperclass
* JPA Entity 클래스들이 BaseTimeEntity을 상속할 경우 필드들(createdDate, modifiedDate)도 컬럼으로 인식하도록 합니다.
2. @EntityListeners(AuditingEntityListener.class)
* BaseTimeEntity 클래스에 Auditing 기능을 포함시킵니다.
3. @CreatedDate
* Entity가 생성되어 저장될 때 시간이 자동 저장됩니다.
4. @LastModifiedDate
* 조회한 Entity의 값을 변경할 때 시간이 자동 저장됩니다.

그리고 Posts 클래스가 BaseTimeEntity를 상속받도록 변경합니다.

마지막으로 JPA Auditing 어노테이션들을 모두 활성화할 수 있도록 Application 클래스에 활성화 어노테이션 하나를 추가하겠습니다.
> @EnableJpaAuditing

PostsRepositoryTest에 JPA Auditing 테스트 코드를 작성합니다.

앞으로 추가될 엔티티들은 더이상 등록일/수정일로 고민할 필요가 없습니다. BaseTimeEntity만 상속받으면 자동으로 해결되기 때문입니다.

# CHATPER 4. 머스테치로 화면 구성하기
## 머스테치 소개
머스테치(https://mustache.github.io/)는 수많은 언어를 지원하는 가장 심플한 템플릿 엔진입니다.
### 장점
* 문법이 다른 템플릿 엔진보다 심플합니다.
* 로직 코드를 사용할 수 없어 View의 역할과 서버의 역할이 명확하게 분리됩니다.
* Mustache.js와 Mustache.java 2가지가 다 있어, 하나의 문법으로 클라이언트/서버 템플릿을 모두 사용 가능합니다.

템플릿 엔진은 홤녀 역할에만 충실해야 한다고 생각합니다. 너무 많은 기능을 제공하면 API와 템플릿 엔진, 자바스크립트가 서로 로직을 나눠 갖게 되어 유지보수하기가 굉장히 어렵습니다.

## 기본 페이지 만들기
pom.xml에 머스테치 의존성을 등록합니다.
> spring boot starter mustache

보는 것처럼 머스테치는 스프링 부트에서 공식 지원하는 템플릿 엔진입니다. 의존성 하나만 추가하면 다른 스타터 패키지와 마찬가지로 추가 설정없이 설치가 끝입니다. 별도로 스프링 부트 버전을 개발자가 신경 쓰지 않아도 되는 장점도 있습니다.

머스테치의 파일 위치는 기본적으로 src/main/resources/templates 입니다. 이 위치에 머스테치 파일을 두면 스프링 부트에서 자동을 로딩합니다.

첫 페이지를 담당할 index.mustache를 src/main/resources/templates에 생성합니다.

이 머스테치에 URL을 매핑합니다. URL 매핑은 당연하게 Controller에서 진행합니다. web 패키지 안에 IndexController를 생성합니다.

머스테치 스타터 더분에 컨트롤러에서 문자열을 반환할 때 앞의 경로와 뒤의 파일 확장자는 자동으로 지정됩니다. 앞의 경로는 src/main/resources/templates로, 뒤의 파일 확장자는 .mustache가 붙는 것입니다. 즉 여기선 "index"을 반환하므로, src/main/resources/templates/index.mustache로 전환되어 View Resolver가 처리하게 됩니다.
(ViewResolver는 URL 요청의 결과를 전달할 타입과 값을 지정하는 관리자 격으로 볼 수 있습니다.)

테스트 코드로 검증합니다. test 패키지에 IndexControllerTest 클래스를 생성합니다.

이번 테스트는 실제로 URL 호출 시 페이지의 내용이 제대로 호출되는지에 대한 테스트입니다.

HTML도 결국은 규칙이 있는 문자열입니다. TestRestTemplate를 통해 "/"로 호출했을 때 index.mustache에 포함된 코드들이 있는지 확인하면 됩니다. 전체 코드를 다 검증할 필요는 없으니, "스프링 부트로 시작하는 웹 서비스" 문자열이 포함되어 있는지만 비교합니다.

정상적으로 화면에 노출되는 것도 확인합니다.

## 게시글 등록 화면 만들기
오픈 소스인 부트스트랩을 이용하여 화면을 만들어 봅니다.

부트스트랩, 제이쿼리 등 프론트엔드 라이브러리를 사용할 수 있는 방법은 크게 2가지가 있습니다. 하나는 외부 CDN을 사용하는 것이고, 다른 하나는 직접 라이브러리를 받아서 사용하는 방법입니다.

여기서는 외부 CDN을 사용합니다. 본인의 프로젝트에서 직접 내려받아 사용할 필요도 없고, 사용 방법도 HTML/JSP/Mustache에 코드만 한 줄 추가하면 되니 굉장히 간단합니다.
> 실제 서비스에서는 이 방법을 잘 사용하지 않습니다. 결국은 외부 서비스에 우리 서비스가 의존하게 돼버려서, CDN을 서비스하는 곳에 문제가 생기면 덩달아 같이 문제가 생기기 때문입니다.

2개의 라이브러리 부트스트랩과 제이쿼리를 index.mustache에 추가해야 합니다. 하지만, 여기서는 바로 추가하지 않고 레이아웃 방식으로 추가해 보겠습니다. 레이아웃 방식이란 공통 영역을 별도의 파일로 분리하여 필요한 곳에서 가져다 쓰는 방식을 이야기합니다.

이번에 추가할 라이브러리들인 부트스트랩과 제이쿼리는 머스테치 화면 어디서나 필요합니다. 매번 해당하는 라이브러리를 머스테치 파일에 추가하는 것은 귀찮은 일이니, 레이아웃 파일들을 만들어 추가합니다.

src/main/resources/templates 디렉토리에 layout 디렉토리를 추가로 생성합니다. 그리고 footer.mustache, header.mustache 파일을 생성합니다.

레이아웃 파일들에 각각 공통 코드를 추가합니다.

css와 js의 위치가 서로 다릅니다. 페이지 로딩속도를 높이기 위해 css는 header에, js는 footer에 두었습니다. HTML은 위에서부터 코드가 실행되기 때문에 head가 다 실행되고서야 body가 실행됩니다.

즉, head가 다 불러지지 않으면 사용자 쪽에선 백지 화면만 노출됩니다. 특히 js의 용량이 크면 클수록 body 부분의 실행이 늦어지기 때문에 js는 body 하단에 두어 화면이 다 그려진 뒤에 호출하는 것이 좋습니다.

반면 css는 화면을 그리는 역할이므로 head에서 불러오는 것이 좋습니다. 그렇지 않으면 css가 적용되지 않은 깨진 화면을 사용자가 볼 수 있기 때문입니다. 추가로, bootstrap.js의 경우 제이쿼리가 꼭 있어야만 하기 때문에 부트스트랩보다 먼저 호출되도록 코드를 작성했습니다. 보통 앞선 상황을 bootstrap.js가 제이쿼리에 의존한다고 합니다.

라이브러리를 비롯해 기타 HTML 태그들이 모두 레이아웃에 추가되니 이제 index.mustache에는 필요한 코드만 남게 됩니다.
1. {{>layout/header}}
* {{> }}는 현재 머스테치 파일(index.mustache)을 기준으로 다른 파일을 가져옵니다.

레이아웃으로 파일을 분리했으니 index.mustache에 글 등록 버튼을 하나 추가해 봅니다.

여기서는 \<a> 태그를 이용해 글 등록 페이지로 이동하는 글 등록 버튼이 생성되었습니다. 이동할 페이지의 주소는 /posts/save 입니다.

이 주소에 해당하는 컨트롤러를 생성하겠습니다. 페이지에 관련된 컨트롤러는 모두 IndexController를 사용합니다.

/posts/save를 호출하면 posts-save.mustache를 호출하는 메소드가 추가되었습니다. 컨트롤러 코드가 생성되었다면 posts-save.mustache 파일을 생성합니다. 파일의 위치는 index.mustache와 같습니다.

하지만 아직 게시글 등록화면에 등록 버튼은 기능이 없습니다. API를 호출하는 JS가 전혀 없기 때문입니다. 그래서 src/main/resources에 static/js/app 디렉토리를 생성합니다.

여기에 index.js를 생성합니다.
1. window.location.href='/'
* 글 등록이 성공하면 메인페이지(/)로 이동합니다.

index.js의 첫 문장에 var main = {...}라는 코드를 선언했습니다. 이렇게 하면 main 객체 안에서만 function이 유효하기 때문에 다른 JS와 겹칠 위험이 사라집니다.
> 이런 식의 프론트엔드의 의존성 관리, 스코프 관리 등의 문제들로 최근에는 자바스크립트 개발 환경이 급변했습니다. ES6를 비롯한 최신 자바스크립트 버전이나 앵귤라, 리액트, 뷰 등은 이미 이런 기능을 프레임워크 레벨에서 지원하고 있습니다.

자 그럼 생성된 index.js를 머스테치 파일이 쓸 수 있게 footer.mustache에 추가하겠습니다.

index.js 호출 코드를 보면 절대 경로(/)로 바로 시작합니다. 스프링 부트는 기본적으로 src/main/resources/static에 위치한 자바스크립트, CSS, 이미지 등 정적파일들은 URL에서 /로 설정됩니다.

그래서 다음과 같이 파일이 위치하면 위치에 맞게 호출이 가능합니다.
* src/main/resources/static/js/... (http://도메인/js/...)
* src/main/resources/static/css/... (http://도메인/css/...)
* src/main/resources/static/image/... (http://도메인/image/...)

브라우저 테스트와 h2-console 테스트를 진행합니다.

## 전체 조회 화면 만들기
전체 조회를 위해 index.mustache의 UI를 변경하겠습니다.
머스테치의 문법이 처음으로 사용됩니다.
1. {{#posts}}
* posts라는 List를 순회합니다.
* Java의 for문과 동일하게 생각하면 됩니다.

2. {{id}} 등의 {{변수명}}
* List에서 뽑아낸 객체의 필드를 사용합니다.

그럼 Controller, Service, Repository 코드를 작성합니다. 먼저 Repository부터 시작합니다.

기존에 있던 PostsRepository 인터페이스에 쿼리가 추가됩니다.
```
@Query("SELECT p FROM Posts p ORDER BY p.id DESC")
List<Posts> findAllDesc();
```
SpringDataJpa에서 제공하지 않는 메소드는 위처럼 쿼리로 작성해도 되는 것을 보여드리고자 @Query를 사용했습니다.

실제로 앞의 코드는 SpringDataJpa에서 제공하는 기본 메소드만으로 해결할 수 있습니다. 다만 @Query가 훨씬 가독성이 좋으니 선택해서 사용하면 됩니다.

### 참고
규모가 있는 프로젝트에서의 데이터 조회는 FK의 조인, 복잡한 조건 등으로 인해 이런 Entity 클래스만으로 처리하기 어려워 조회용 프레임워크를 추가로 사용합니다. 대표적 예로 querydsl, jooq, MyBatis 등이 있습니다. 조회는 위 3가지 프레임워크 중 하나를 통해 조회하고, 등록/수정/삭제 등은 SpringDataJpa를 통해 진행합니다. 개인적으로는 querydsl를 추천합니다.

Querydsl을 추천하는 이유는 다음과 같습니다.
1. 타입 안정성이 보장됩니다.   
단순한 문자열로 쿼리를 생성하는 것이 아니라, 메소드를 기반으로 쿼리를 생성하기 때문에 오타나 존재하지 않는 컬럼명을 명시할 경우 IDE에서 자동으로 검출됩니다. 이 장점은 Jooq에서도 지원하는 장점이지만, MyBatis에서는 지원하지 않습니다.

2. 국내 많은 회사에서 사용 중입니다.   
쿠팡, 배민 등 JPA를 적극적으로 사용하는 회사에서는 Querydsl를 적극적으로 사용중입니다.

3. 레퍼런스가 많습니다.   
앞 2번의 장점에서 이어지는 것인데, 많은 회사와 개발자들이 사용하다보니 그만큼 국내 자료가 많습니다. 어떤 문제가 발생했을 때 여러 커뮤니티에 질문하고 그에 대한 답변을 들을 수 있다는 것은 큰 장점입니다.

Repository 다음으로 PostsService에 코드를 추가하겠습니다.

findAllDesc 메소드의 트랜잭션 어노테이션(@Transactional)에 옵션이 하나 추가되었습니다. (readOnly = true)를 주면 트랜잭션 범위는 유지하되, 조회 기능만 남겨두어 조회 속도가 개선되기 때문에 등록, 수정, 삭제 기능이 전혀 없는 서비스 메소드에서 사용하는 것을 추천합니다.

```
.map(PostsListResponseDto::new)
```
이 코드는 실제로 다음과 같습니다.
```
.map(posts -> new PostsListResponseDto(posts))
```
postsRepository 결과로 넘어온 Posts의 Stream을 map을 통해 PostsListResponseDto 변환 -> List로 반환하는 메소드입니다.

아직 PostsListResponseDto 클래스가 없기 때문에 이 클래스 역시 생성합니다.

마지막으로 Controller를 변경하겠습니다.
1. Model
* 서버 템플릿 엔진에서 사용할 수 있는 객체를 저장할 수 있습니다.
* 여기서는 postsService.findAllDesc()로 가져온 결과를 posts로 index.mustache에 전달합니다.

화면을 통해 테스트 해봅니다.

## 게시글 수정, 삭제 화면 만들기
게시글 수정 머스테치 파일을 생성합니다.
1. {{post.id}}
* 머스테치는 객체의 필드 접근 시 점(Dot)을 구분합니다.
* 즉, Post 클래스의 id에 대한 접근은 post.id로 사용할 수 있습니다.

2. readonly
* Input 태그에 읽기 기능만 허용하는 속성입니다.
* id와 author는 수정할 수 없도록 읽기만 허용하도록 추가합니다.

그리고 btn-update 버튼을 클릭하면 update 기능을 호출할 수 있게 index.js 파일에도 update function을 하나 추가합니다.
1. $('#btn-update').on('click')
* btn-update란 id를 가진 HTML 엘리먼트에 click 이벤트가 발생할 때 update function을 실행하도록 이벤트를 등록합니다.

2. update: function()
* 신규로 추가될 update function 입니다.

3. type: 'PUT'
* 여러 HTTP Method 중 PUT 메소드를 선택합니다.
* PostsApiController에 있는 API에서 이미 @PutMapping으로 선언했기 때문에 PUT을 사용해야 합니다. 참고로 이는 REST 규약에 맞게 설정된 것입니다.
* REST에서 CRUD는 다음과 같이 HTTP Method에 매핑됩니다.   
생성 (Create) - POST   
읽기 (Read) - GET
수정 (Update) - PUT
삭제 (Delete) - DELETE

4. url: '/api/v1/posts/' + id
* 어느 게시글을 수정할지 URL Path로 구분하기 위해 Path에 id를 추가합니다.

마지막으로 전체 목록에서 수정 페이지로 이동할 수 있게 페이지 이동 기능을 추가합니다.
1. \<a href="posts/update/{{id}}">\</a>
* 타이틀(title)에 a tag를 추가합니다.
* 타이틀을 클릭하면 해당 게시글의 수정 화면으로 이동합니다.

삭제 버튼은 본문을 확인하고 진행해야 하므로, 수정 화면에 추가합니다.
1. btn-delete
* 삭제 버튼을 수정 완료 버튼 옆에 추가합니다.
* 해당 버튼 클릭 시 JS에서 이벤트를 수신할 예정입니다.

서비스 메소드를 만듭니다.
1. postsRepository.delete(posts)
* JpaRepository에서 이미 delete 메소드를 지원하고 있으니 이를 활용합니다.
* 엔티티를 파라미터로 삭제할 수도 있고, deleteById 메소드를 이용하면 id로 삭제할 수도 있습니다.
* 존재하는 Posts인지 확인을 위해 엔티티 조회 후 그대로 삭제합니다.

# CHATPER 5. 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
> 스프링 시큐리티(Spring Security)는 막강한 인증(Authentication)과 인가(Authorization)(혹은 권한 부여) 기능을 가진 프레임워크 입니다. 인터셉터, 필터 기반의 보안 기능을 구현하는 것보다 스프링 시큐리티를 통해 구현하는 것을 적극적으로 권장하고 있습니다.

> 스프링 시큐리티와 OAuth 2.0을 구현한 구글 로그인을 연동하여 로그인 기능을 만들어 보겠습니다.

## 스프링 시큐리티와 스프링 시큐리티 Oauth2 클라이언트
> 많은 서비스에서 로그인 기능을 id/password 방식보다는 구글, 페이스북, 네이버 로그인과 같은 소셜 로그인 기능을 사용합니다.

> OAuth 로그인 구현 시 아래 목록의 것들을 모두 구글, 페이스북, 네이버 등에 맡기면 되니 서비스 개발에 집중할 수 있습니다.
* 로그인 시 보안
* 회원가입 시 이메일 혹은 전화번호 인증
* 비밀번호 찾기
* 비밀번호 변경
* 회원정보 변경

