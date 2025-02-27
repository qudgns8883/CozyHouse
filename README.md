# 🖥️ 프로젝트 소개
오늘의 집 사이트를 참고하여 사용자에게 다양한 인테리어 상품을 판매하는 웹 애플리케이션을 개발하였습니다.

<br/>

## 👨‍👩‍👦 프로젝트 구성원
- **팀원**: 김민석 - 프론트엔드
- **팀원**: 이병훈 - 백엔드

## ⚙️ 사용된 기술
- **Java**: 서버 사이드 애플리케이션 개발
- **Spring Boot**: 애플리케이션의 빠른 설정과 개발을 위한 프레임워크
- **Spring Data JPA**: 데이터베이스와의 상호작용을 위한 ORM
- **Spring Security**: 안전한 인증 및 권한 관리를 위한 보안 프레임워크
- **MySQL**: 데이터 저장을 위한 관계형 데이터베이스

<br/>

# 💡 주요 기능

## 회원가입
- OAuth2 방식을 사용하여 JWT를 이용한 회원가입 기능을 구현하였습니다.
- 모든 회원가입 로직은 백엔드에서 처리하여 데이터의 일관성과 보안을 강화하였습니다.

## 로그인, 소셜로그인, 로그아웃
- OAuth2 방식으로 로그인 및 소셜 로그인 기능을 구현하였습니다.
- JWT를 사용하여 인증 토큰을 관리하고, 모든 인증 관련 로직은 백엔드에서 처리합니다.
- 여러 필터를 커스터마이즈하여 로그인, 로그아웃 및 JWT 검증을 관리합니다.
- 리프레시 토큰을 사용하여 세션 유지 기능을 구현하였으며, 리프레시 토큰 로테이션을 통해 보안성을 강화하였습니다.

## 전역예외처리
- AOP를 활용해 애플리케이션 전반에 걸쳐 발생하는 예외를 처리합니다.

## 글쓰기
- 파일 업로드를 위해 MultiparFile와 Java NIO를 사용하여 처리합니다.

<br/>

# 프로젝트 설정

<br/>

이 프로젝트를 실행하기 위해서는 몇 가지 환경 설정이 필요합니다. 아래의 단계를 따라주세요.


## 1. 데이터베이스 설정
1. MySQL에서 cozy-house 데이터베이스를 생성합니다.
2. 아래의 정보를 바탕으로 application.properties 파일을 설정합니다.

## 2. application.properties 설정

src/main/resources/application.properties 파일을 다음과 같이 생성 후 설정합니다:

- ### 애플리케이션 이름 및 포트
spring.application.name=backend  
server.port=8081  

- ### 파일 업로드 디렉토리
file.upload-dir=C:\\파일경로\\file\\  
spring.servlet.multipart.enabled=true  
spring.servlet.multipart.max-file-size=50MB  
spring.servlet.multipart.max-request-size=50MB  

- ### MySQL 설정
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver  
spring.datasource.url=YOUR_URL_HERE  
spring.datasource.username=YOUR_username_HERE  
spring.datasource.password=YOUR_PASSWORD_HERE  

- ### JPA 설정
spring.jpa.properties.hibernate.show_sql=true  
spring.jpa.properties.hibernate.format_sql=true  
spring.jpa.hibernate.ddl-auto=update  
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect  
spring.jackson.property-naming-strategy=SNAKE_CASE  
spring.jwt.secret=YOUR_SECRET_KEY_HERE  

- ### 보안 로깅
logging.level.org.springframework.security=DEBUG  

- ### kakao OAuth2
spring.security.oauth2.client.registration.kakao.client-name=Kakao  
spring.security.oauth2.client.registration.kakao.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.kakao.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8081/login/oauth2/code/kakao  
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.kakao.scope=account_email, profile_nickname  
spring.security.oauth2.client.registration.kakao.client-authentication-method=client_secret_post  
spring.security.oauth2.client.provider.kakao.authorization-uri=https://kauth.kakao.com/oauth/authorize  
spring.security.oauth2.client.provider.kakao.token-uri=https://kauth.kakao.com/oauth/token  
spring.security.oauth2.client.provider.kakao.user-info-uri=https://kapi.kakao.com/v2/user/me  
spring.security.oauth2.client.provider.kakao.user-name-attribute=id  

- ### Google OAuth2
spring.security.oauth2.client.registration.google.client-name=google  
spring.security.oauth2.client.registration.google.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.google.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.google.redirect-uri=http://localhost:8081/login/oauth2/code/google  
spring.security.oauth2.client.registration.google.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.google.scope=profile,email  

- ### GitHub OAuth2
spring.security.oauth2.client.registration.github.client-name=GitHub  
spring.security.oauth2.client.registration.github.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.github.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.github.redirect-uri=http://localhost:8081/login/oauth2/code/github  
spring.security.oauth2.client.registration.github.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.github.scope=SCOPE_read:user,SCOPE_user:email  
spring.security.oauth2.client.registration.github.client-authentication-method=client_secret_post  
spring.security.oauth2.client.provider.github.authorization-uri=https://github.com/login/oauth/authorize  
spring.security.oauth2.client.provider.github.token-uri=https://github.com/login/oauth/access_token  
spring.security.oauth2.client.provider.github.user-info-uri=https://api.github.com/user  
spring.security.oauth2.client.provider.github.user-name-attribute=id  

- ### Naver OAuth2
spring.security.oauth2.client.registration.naver.client-name=naver  
spring.security.oauth2.client.registration.naver.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.naver.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.naver.redirect-uri=http://localhost:8081/login/oauth2/code/naver  
spring.security.oauth2.client.registration.naver.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.naver.scope=name,email  
spring.security.oauth2.client.provider.naver.authorization-uri=https://nid.naver.com/oauth2.0/authorize  
spring.security.oauth2.client.provider.naver.token-uri=https://nid.naver.com/oauth2.0/token  
spring.security.oauth2.client.provider.naver.user-info-uri=https://openapi.naver.com/v1/nid/me  
spring.security.oauth2.client.provider.naver.user-name-attribute=response  

- ### CoolSMS 설정(회원가입 인증코드 비활성화했습니다.)
coolsms.api.key=YOUR_COOLSMS_API_KEY  
coolsms.api.secret=YOUR_COOLSMS_API_SECRET  
coolsms.from=YOUR_COOLSMS_FROM_NUMBER  

- ### Redis 설정
spring.data.redis.host=localhost  
spring.data.redis.port=6379  

<br/>

## 3. 프론트엔드 실행방법
1. 프론트엔드 디렉터리 이동 
   - cd frontend  
2. 의존성 설치
   - npm install
3. 애플리케이션 설치
   - npm run dev
