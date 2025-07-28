# 🖥️ 프로젝트 소개
오늘의 집 사이트를 참고하여 사용자에게 다양한 인테리어 상품을 판매하는 웹 애플리케이션을 개발하였습니다.

<br/>

## 👨‍👩‍👦 프로젝트 구성원
- **팀원**: 김민석 - 프론트엔드
- **팀원**: 이병훈 - 백엔드

## ⚙️ 사용된 기술
- Java
- Spring Boot, Spring Security, Spring Data JPA, Spring Cloud Eureka
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
<img width="1252" height="484" alt="image" src="https://github.com/user-attachments/assets/b7a12cbd-4a9d-4ba5-8939-7d810be2c137" />


## 전역 예외 처리
* `@RestControllerAdvice`와 `@ExceptionHandler`를 활용해 애플리케이션 전반에 발생하는 모든 예외를 중앙에서 처리
* 애플리케이션의 다양한 예외 상황에 맞춰 적절한 HTTP 상태 코드와 상세한 오류 메시지를 반환하도록 설계

## 글쓰기
<table>
  <tr>
    <td width="50%">
      <img width="981" height="334" alt="image" src="https://github.com/user-attachments/assets/e608a7a4-7999-44df-af88-89d69bdabbc7" />
      <img width="976" height="452" alt="image" src="https://github.com/user-attachments/assets/78a67381-903a-4f93-86f2-9a7e0fe93260" />
    </td>
    <td width="50%">
      <p><b>글쓰기</b></p>
      <ul>
        <li>텍스트와 다중 이미지/영상을 함께 업로드하는 기능을 구현했습니다. 파일 처리 로직을 별도로 분리하고, 보안 및 데이터 일관성을 고려하여 설계</li>
      </ul>
    </td>
  </tr>
</table>




