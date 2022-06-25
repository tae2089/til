## 오늘 찾아보 링크 목록

[s3 관련 application.yml 설정](https://antdev.tistory.com/93)

## 공부한 내용

### s3 application.yml

```
cloud:
  aws:
    s3:
      bucket: <버킷명>
    credentials:
      accessKey: <accessKey 입력>
      secretKey: <secretKey 입력>
    region:
      static: <버킷 region설정>
      auto: false //region 자동 감지
    stack:
      auto: false // CloudFormation 사용 안하기
```

s3를 사용하기 위해서 application.yml 설정을 진행했다. accesskey와 secretkey만 있으면 되는 줄 알았는데
cloud.aws.stack.auto를 안해줘서 문제가 생겼다. ec2에서 프로그램을 실행하면 자동으로 Cloud Formation가 실행되는 데 이게 문제가 되어 실행이 안된다고 한다.

나는 aws 관련해서 사용할 때 property를 만들어서 사용한다. 테스트를 할 때 @Value가 동작하지 않아 문제가 많이 생겼던 기억이 있기에 이를 방지하기 위해 다음과 같은 코드를 작성해서 사용한다.

```java
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
@Getter
@NoArgsConstructor
public class AwsProperty {

    @Value("${cloud.aws.credentials.accessKey}")
    private String accessKey;

    @Value("${cloud.aws.credentials.secretKey}")
    private String secretKey;

    @Value("${cloud.aws.s3.bucket}")
    private String bucket;

    @Value("${cloud.aws.region.static}")
    private String region;

    public AwsProperty(String accessKey, String secretKey, String bucket, String region) {
        this.accessKey = accessKey;
        this.secretKey = secretKey;
        this.bucket = bucket;
        this.region = region;
    }
}
```

이런식으로 만들어서 서비스 코드에 생성자에 넣어주면 사용하기 편하다.
이와 관련된 코드를 예전에 작성한게 있어 여기에 링크를 올려놓는다.

[object storage java code](https://github.com/tae2089/spring-objectstorage)
