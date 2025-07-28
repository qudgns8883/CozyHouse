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
        <li>Spring Security를 활용하여 안전한 사용자 인증 시스템을 구축</li>
        <li>사용자 비밀번호는 BCryptPasswordEncoder를 사용하여 암호화 처리</li>
        <li>회원가입 시 @Valid로 검증 후 이메일/닉네임 중복 검증 로직을 추가</li>
        <li>Nurigo (Coolsms API) 연동을 통해 휴대폰 SMS 인증 번호 발송 기능을 구현</li>
        <li>Redis를 활용하여 SMS 인증 번호의 유효 시간을 관리(TTL 5분)하고, 빠른 조회 및 보안성을 확보</li> 
        <li>(난수 생성에는 SecureRandom 사용)</li>
      </ul>
    </td>
  </tr>
</table>

## 로그인, 소셜로그인, 로그아웃
- OAuth2 방식으로 로그인 및 소셜 로그인 기능을 구현하였습니다.
- JWT를 사용하여 인증 토큰을 관리하고, 모든 인증 관련 로직은 백엔드에서 처리합니다.
- 여러 필터를 커스터마이즈하여 로그인, 로그아웃 및 JWT 검증을 관리합니다.
- 리프레시 토큰을 사용하여 세션 유지 기능을 구현하였으며, 리프레시 토큰 로테이션을 통해 보안성을 강화하였습니다.

## 전역예외처리
- AOP를 활용해 애플리케이션 전반에 걸쳐 발생하는 예외를 처리합니다.

## 글쓰기
- 파일 업로드를 위해 MultiparFile와 Java NIO를 사용하여 처리합니다.
