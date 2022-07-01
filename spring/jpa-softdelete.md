### 관련 링크들

[링크](https://levelup.gitconnected.com/spring-boot-soft-delete-functionality-with-hibernate-f5ee8c24c99f)

## 공부 내용

### jpa soft delete에 대해 공부

많은 서비스들이 데이터를 delete 하면 삭제된 거 처럼 보이게 한다.
이것을 soft delete라고 한다. 진짜 데이터를 삭제하는 것을 hard delete라고 한다.

soft delete를 하는 방법은 여러가지가 있다.
data를 받아서 해당 값을 코드로 변경해서 다시 저장해주는 방법이 있다. 예시로 다음과 같이 작성할 수 있을거 같다.

```java

```

다른 방법으로는 @SqlDelete를 사용하는 것이다. @SqlDelete를 사용하면 해당 도메인이 삭제되는 것에 대해 감지를 하여 자동으로 @SqlDelete에 작성되어 있는 쿼리문을 실행하게 된다. 코드는 다음과 같이 작성할 수 있다.

```java

```

soft delete 방식은 위 두가지가 있고 이를 불러오는 방법에 대해서도 공부했다. @Where과 @Filter를 사용하는 방법이 있다.
