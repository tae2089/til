swagger에 대해 공부했다.

API문서에 대해 작성을 해야하는데 찾아보다가 정리하게 되었다.

swagger에 경우 OPEN API를 활용하여 만들어진 라이브러리다.

많은 회사에서 이것을 쓰고 있어서 알고 있어야 한다.

또한, 프론트 개발자가 서버 개발자와 소통할 때 제일 중요하게 생각할 수 있는 부분일 것이다.

```groovy
	implementation 'io.springfox:springfox-boot-starter:3.0.0'
	implementation 'io.springfox:springfox-swagger-ui:3.0.0'
```

저 위에 있는 라이브러리들을 설치해줘야 한다.

SwaggerConfig를 다음과 같이 만들어준다.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;

import java.util.HashSet;
import java.util.Set;

@Configuration
@EnableWebMvc
public class SwaggerConfig {
    private ApiInfo swaggerInfo() {
        return new ApiInfoBuilder().title("WEB API")
                .description("WEB API Docs").build();
    }

    @Bean
    public Docket swaggerApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .consumes(getConsumeContentTypes())
                .produces(getProduceContentTypes())
                .apiInfo(swaggerInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.swagger"))
                .paths(PathSelectors.any())
                .build()
                .useDefaultResponseMessages(false);
    }

    private Set<String> getConsumeContentTypes() {
        Set<String> consumes = new HashSet<>();
        consumes.add("application/json;charset=UTF-8");
        consumes.add("application/x-www-form-urlencoded");
        consumes.add("multipart/form-data");
        return consumes;
    }

    private Set<String> getProduceContentTypes() {
        Set<String> produces = new HashSet<>();
        produces.add("application/json;charset=UTF-8");
        return produces;
    }
}

```

Swagger 설정이 끝났다면 서버를 실행해준다.

http://localhost:8080/swagger-ui/index.html

위 링크에 들어가면 볼 수 있다.
