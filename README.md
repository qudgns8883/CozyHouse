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

<br/>
  
## JWT 인증 방식 시큐리티 동작 원리 [링크](https://bottlenose-asparagus-798.notion.site/JWT-1-1a81bba98c5780ca8818c23b7f79f739)

<p align="center">
  <img src="https://github.com/user-attachments/assets/2e9fe005-ce39-4061-9afe-f6b7d6f4e16e" width="800" alt="로그인 흐름">
</p>

1.  **Spring Security 기반의 커스텀 인증 필터**
    * 기존의 UsernamePasswordAuthenticationFilter를 커스터마이징하여 REST API에 적합한 로그인 방식을 구현
    * 클라이언트 요청에서 사용자 이름과 비밀번호를 추출해 UsernamePasswordAuthenticationToken을 생성하고 AuthenticationManager로 전달

2.  **JWT 기반 토큰 발급**
    * 인증에 성공하면, successfulAuthentication 메서드에서 jwtUtil을 활용해 Access Token과 Refresh Token을 생성합니다.
    * 생성된 JWT는 클라이언트에 응답으로 반환되어 이후 요청의 인증 수단으로 사용

3.  **SecurityContextHolder에 인증 정보 저장**
    * SecurityContextHolder.getContext()에 인증 정보를 저장하여 후속 필터 및 비즈니스 로직에서 인증 상태를 활용

<br/>
  
## OAuth 2.0 소셜 로그인 흐름 [링크](https://bottlenose-asparagus-798.notion.site/OAuth-2-0-1-1a81bba98c578094ad49e59873a7c44f)
<p align="center"><img width="951" height="558" alt="image" src="https://github.com/user-attachments/assets/b5aab28a-dad4-4551-81e9-20bab568f1d5" /></p>

1.  **사용자 요청 및 리다이렉션**
    * 사용자가 소셜 로그인 버튼을 클릭하면 Spring 서버가 요청을 가로채 해당 소셜 서비스의 로그인 페이지로 사용자를 자동으로 리다이렉트

2.  **인증 코드 획득 및 토큰 발급**
    * 사용자가 소셜 서비스에서 로그인을 성공하면 소셜 서비스는 프로젝트로 인증 코드(Authorization Code)를 반환
    * Spring Security는 이 코드를 사용해 소셜 서비스로부터 Access Token과 사용자 정보를 획득

3.  **JWT 발급 및 로그인 완료**
    * 획득한 사용자 정보를 바탕으로 프로젝트의 로그인 절차를 진행
    * 최종적으로, 프로젝트의 인증 시스템에 맞는 JWT(Access/Refresh Token)를 발급하여 클라이언트에게 전송함으로써 로그인을 완료

<br/>
  
## 🛠️ 트러블슈팅 내용

### 문제 상황

1. 소셜 로그인 구현 시, 일반 로그인처럼 엑세스토큰과 리프레시토큰을 HTTP 응답 헤더로 받으려 했습니다.
2. 그러나 하이퍼링크로 리다이렉션되는 과정에서 요청 헤더에 직접 접근할 수 없는 상황이 발생했습니다.
3. 이로 인해 JWTFilter는 요청 헤더에서 받은 엑세스 쿠키로 인증을 하게 되었고, 이로 인해 일관성이 떨어지는 문제가 발생했습니다.

### 해결 방안

1. 쿠키를 통해 JWT토큰을 전송
2. 쿠키에 있는 엑세스토큰을 응답 헤더로 변환
3. 로컬 스토리지에 엑세스토큰 저장
    
    ![이병훈](https://qudgns8883.github.io/assets/img/OAuth2.png)
    

### 결론

1. 소셜 로그인 과정에서 하이퍼링크로 인한 리다이렉션 문제 때문에, 쿠키를 사용해 토큰을 전송하는 방식을 선택했습니다.
2. HttpOnly설정으로 쿠키에 엑세스토큰을 저장할 수 없었고, 엑세스 토큰 변환 후 요청헤드로 클라이언트에 전달함으로써 JWTFilter의 일관성을 유지했습니다.

### 느낀 점

1. JWT 토큰을 활용하여 쿠키와 요청 헤더를 조합한 인증 방식이 효과적이라는 것을 깨달았습니다.
2. HttpOnly 속성의 중요성을 통해 XSS 공격 방어를 강화할 수 있음을 배웠고, CSP(Content Security Policy)와 로컬 스토리지로 클라이언트 측 보안을 높일 수 있었습니다.
3. 이번 경험을 통해 웹 보안의 중요성을 이해하게 되었고, 앞으로 JWT를 활용해 안전하고 효율적인 시스템을 구축하는 데 기여하고 싶습니다.



