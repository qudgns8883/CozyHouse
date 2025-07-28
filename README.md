# 🖥️ 프로젝트 소개
오늘의 집 사이트를 참고하여 사용자에게 다양한 인테리어 상품을 판매하는 웹 애플리케이션을 개발하였습니다.

<br/>

## 👨‍👩‍👦 프로젝트 구성원
- **팀원**: 김민석 - 프론트엔드
- **팀원**: 이병훈 - 백엔드

## ⚙️ 사용된 기술
- Java
- Spring Boot, Spring Security, Spring Data JPA
- JWT, OAuth2
- MySQL

<br/>

# 💡 주요 기능

## 회원가입
<table>
  <tr>
    <td width="50%">
      <img width="369" alt="회원가입 화면" src="https://github.com/user-attachments/assets/3ddb02fe-ec41-4c82-a0a3-93f3a100bc7e" />
    </td>
    <td width="50%">
      <p><b>회원가입</b></p>
      <ul>
        <li>Spring Security 기반의 인증 시스템을 구축</li>
        <li>BCryptPasswordEncoder를 이용한 비밀번호 암호화 및 이메일/닉네임 중복 검증을 통해 보안을 강화했습니다.</li>
        <li>Nurigo (Coolsms API) 연동으로 SMS 인증 번호 발송 기능을 구현</li>
        <li>Redis를 활용하여 인증 번호의 유효 시간을 관리(TTL 5분)하고, 효율성 및 보안성을 확보</li> 
      </ul>
    </td>
  </tr>
</table>

## 로그인, 소셜로그인, 로그아웃

<table>
  <tr>
    <td width="50%">
      <img width="372" height="472" alt="로그인/소셜로그인 화면" src="https://github.com/user-attachments/assets/5b4445f5-66b7-4cf8-86de-5dca11c3726b" />
    </td>
    <td width="50%">
      <p><b>로그인, 소셜로그인, 로그아웃</b></p>
      <ul>
        <li>JWT 기반 인증 시스템: Spring Security를 활용하여 JWT(Access/Refresh Token) 기반의 인증 시스템을 구축</li>
        <li>OAuth 2.0 소셜 로그인: Google, Kakao 등 소셜 계정으로 간편하게 로그인할 수 있는 기능을 구현</li>
        <li>보안 강화: Refresh Token Rotation 전략을 적용하여 토큰 탈취 시 피해를 최소화하고, 로그인 및 소셜 로그인 모두 동일한 인증 로직을 사용하도록 설계</li>
        <li>로그아웃: Refresh Token을 DB에서 삭제하고 쿠키를 무효화하여 토큰 재사용을 방지</li>
      </ul>
    </td>
  </tr>
</table>


## 메인화면
<table>
  <tr>
    <td width="50%">
      <img width="1252" height="484" alt="image" src="https://github.com/user-attachments/assets/b7a12cbd-4a9d-4ba5-8939-7d810be2c137" />
    </td>
    <td width="50%">
      <p><b>로그인 후 메인화면</b></p>
      <ul>
        <li>API 호출 시 Access Token이 만료되면 Refresh Token으로 새로운 Access Token을 재발급</li>
        <li>이 과정에서 기존 Refresh Token은 폐기되고, 새로운 Refresh Token이 발급되어 보안을 강화</li>
      </ul>
    </td>
  </tr>
</table>

## 글쓰기
<table>
  <tr>
    <td width="50%">
      <img width="981" height="334" alt="image" src="https://github.com/user-attachments/assets/e608a7a4-7999-44df-af88-89d69bdabbc7" />
      <img width="976" height="452" alt="image" src="https://github.com/user-attachments/assets/78a67381-903a-4f93-86f2-9a7e0fe93260" />
      <img width="954" height="510" alt="image" src="https://github.com/user-attachments/assets/ded8e75a-4657-4739-994a-04d3fd616178" />
    </td>
    <td width="50%">
      <p><b>글쓰기</b></p>
      <ul>
        <li>텍스트와 다중 이미지/영상을 함께 업로드하는 기능을 구현했습니다. 파일 처리 로직을 별도로 분리하고, 보안 및 데이터 일관성을 고려하여 설계</li>
      </ul>
    </td>
  </tr>
</table>

## 전역 예외 처리
* @RestControllerAdvice와 @ExceptionHandler를 활용해 애플리케이션 전반에 발생하는 모든 예외를 중앙에서 처리
* 애플리케이션의 다양한 예외 상황에 맞춰 적절한 HTTP 상태 코드와 상세한 오류 메시지를 반환하도록 설계
  
## JWT 인증 방식 시큐리티 동작 원리 

<p align="center">
  <img src="https://github.com/user-attachments/assets/2e9fe005-ce39-4061-9afe-f6b7d6f4e16e" width="800" alt="로그인 흐름">
</p>

**동작 원리**

1.  **Spring Security 기반의 커스텀 인증 필터**:
    * 기존의 `UsernamePasswordAuthenticationFilter`를 커스터마이징하여 REST API에 적합한 로그인 방식을 구현합니다.
    * 클라이언트 요청에서 사용자 이름과 비밀번호를 추출해 `UsernamePasswordAuthenticationToken`을 생성하고 `AuthenticationManager`로 전달합니다.

2.  **JWT 기반 토큰 발급**:
    * 인증에 성공하면, `successfulAuthentication` 메서드에서 `jwtUtil`을 활용해 Access Token과 Refresh Token을 생성합니다.
    * 생성된 JWT는 클라이언트에 응답으로 반환되어, 이후 요청의 인증 수단으로 사용됩니다.

3.  **SecurityContextHolder에 인증 정보 저장**:
    * `SecurityContextHolder.getContext()`에 인증 정보를 저장하여, 후속 필터 및 비즈니스 로직에서 인증 상태를 활용할 수 있습니다.

1. Spring Security 기반의 커스텀 인증 필터
기존의 UsernamePasswordAuthenticationFilter를 직접 커스터마이징하여 REST API 환경에 적합한 로그인 인증 방식을 구현했습니다.
클라이언트로부터 받은 사용자 이름과 비밀번호를 기반으로 UsernamePasswordAuthenticationToken을 생성하고, AuthenticationManager를 통해 인증을 진행합니다.

2. JWT 기반의 토큰 발급
인증이 성공하면, successfulAuthentication 메서드에서 jwtUtil을 활용하여 Access Token과 Refresh Token을 생성합니다.
발급된 JWT는 클라이언트에 응답으로 반환되며, 클라이언트는 이를 저장하여 이후의 모든 요청에 대한 인증 수단으로 사용합니다.

3. SecurityContextHolder에 인증 정보 저장
SecurityContextHolder.getContext()에 인증 정보를 저장하여, 이후 필터 체인 및 비즈니스 로직에서 해당 사용자의 인증 상태를 활용할 수 있도록 합니다.
  
## OAuth 2.0 소셜 로그인 흐름
<img width="951" height="558" alt="image" src="https://github.com/user-attachments/assets/b5aab28a-dad4-4551-81e9-20bab568f1d5" />
1. 프론트에서 로그인 버튼을 클릭
    - 사용자가 소셜 로그인 버튼을 클릭하여 로그인 절차를 시작합니다.
2. 소셜 로그인 시도
    - /oauth2/authorization/서비스명 경로로 소셜 로그인 요청이 전송됩니다.
3. Spring 서버에서 OAuth 요청 처리
    - Spring 내부의 OAuth2AuthorizationRequestRedirectFilter가 요청을 가로채고 외부 인증 서버로 리다이렉트합니다.
4. 인증 서버에서 로그인 페이지 반환
    - 인증 서버가 서비스 로그인 페이지를 사용자에게 응답합니다.
5. 로그인 성공 시 코드 반환
    - 로그인 성공 후 인증 서버가 리다이렉트 주소로 코드(Authorization Code)를 반환합니다. 이 코드를 사용해 엑세스 토큰을 요청합니다.
6. /login/oauth2/code/서비스 경로로 요청
    - 이 코드는 /login/oauth2/code/서비스 경로로 전달되는 것이 관습
7. Oauth2LoginAuthenticationFilter에서 요청 가로챔
    - 해당 요청은 Oauth2LoginAuthenticationFilter에서 처리됩니다.
8. Oauth2LoginAuthenticationProvider에서 Access 토큰 발급
    - Oauth2LoginAuthenticationProvider가 요청에 있는 코드를 사용해 인증 서버에서 Access 토큰을 발급받습니다
9. Access 토큰으로 리소스 서버에 접근
    - Access 토큰을 사용해 리소스 서버에서 유저 정보를 획득합니다.
10. OAuth2Service에서 유저 정보 처리
    - 획득한 유저 정보를 OAuth2Service에서 처리하고, 이를 OAuth2User 객체에 담아 로그인을 진행합니다.
11. JWT 발급
    - 로그인 성공 후, LoginSuccessHandler에서 JWT를 발급하여 클라이언트에 전송합니다.



