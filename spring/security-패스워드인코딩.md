## 오늘 찾아보 링크 목록

1. [spring security password](https://docs.spring.io/spring-security/reference/features/authentication/password-storage.html)

## 공부한 내용

### Spring Security PassWord 인코딩 하는 방법에 대하여

- Spring Security 5.7.1을 봤다.
- Spring Sercurity에 경우 인증과 인가를 통해 봉안을 유지한다.
- 인증은 유저가 맞는지에 대해서 판단한다면 인가에 경우 인증된 유저가 특정 권한을 쓸 수 있는지를 본다고 한다.
- 비밀번호를 만들 때 PasswordEncoder를 사용하고 NoOpPasswordEncoder default이다.
- 패스워드가 인코딩되면 다음과 같이 나온다.
  ```
  {id}encodedPassword
  ```
  여기서 id는 인코딩할 떄 사용된 방식을 나타내고 encodedPassword는 인코딩된 비밀번호를 나타낸다.
