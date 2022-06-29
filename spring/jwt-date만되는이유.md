## 참고 사이트 및 책링크

Jwt 내부 코드 패키지 경로(io.jsonwebtoken.Claims;)

## 공부 내용

### jwt에서 LocalDateTime이 안되는 이유에 대하여

Spring 프로젝트를 하면서 jwt를 사용하여 쿠키를 만들어서 사용했다.

Jwt에 들어가는 내용에 LocalDateTime을 넣어줬다. LocalDateTime을 넣워젔는데 에러가 발생했다.

Jwt에서는 Instant가 아닌 타입에 대해서 에러를 발생시킨다.
여기서 Instant는 UTC의 타임라인에 있는 한 순간(moment)으로, 1970년 UTC의 첫 번째 모멘트의 발생 이후 nano초 동안의 시간이다.
대부분의 비즈니스 로직, 데이터 스토리지 및 데이터 교환은 UTC여야 하므로 Instant는 자주 사용할 수 있는 편리한 클래스다.

LocalDateTime에 경우 Instant클래스를 변환하는 것을 제공해주지 않기에 이 부분이 문제가 되는것으로 보인다.
