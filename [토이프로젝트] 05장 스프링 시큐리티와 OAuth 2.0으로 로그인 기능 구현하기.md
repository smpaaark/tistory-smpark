# 구글 서비스 등록
1. 구글 클라우드 플랫폼 주소(https://console.cloud.google.com)로 이동하여 신규 서비스를 생성합니다.
2. src/main/resources/ 디렉토리에 application-oauth.properties 파일을 생성합니다.
3. 해당 파일에 클라이언트 ID(clientId)와 클라이언트 보안 비밀(clientSecret) 코드를 다음과 같이 등록합니다.
```
spring.security.oauth2.client.registration.google.client-id=클라이언트ID
spring.security.oauth2.client.registration.google.client-secret=클라이언트 보안 비밀
spring.security.oauth2.client.registration.google.scope=profile,email
```

### scope=profile, email
* 기본값이 openid, profile, email입니다.
* 강제로 profile, email을 등록한 이유는 openid라는 scope가 있으면 Open IdProvider로 인식하기 때문입니다.
* 이렇게 되면 OpenId Provider인 서비스(구글)와 그렇지 않은 서비스(네이버/카카오 등)로 나눠서 각각 OAuth2Service를 만들어야 합니다.
* 하나의 OAuth2Service로 사용하기 위해 일부러 openid scope을 빼고 등록합니다.

4. application.properties에서 application-oauth.properties를  포함하도록 코드를 추가합니다.
```
spring.profiles.include=oauth
```

5. 구글 로그인을 위한 클라이언트ID(clientId)와 클라이언트 보안 비밀은 중요한 정보들이기 때문에 깃허브에 application-oauth.properties 파일이 올라가는 것을 방지하겠습니다.
6. .gitignore에 코드를 추가합니다.
```
application-oauth.properties
```

