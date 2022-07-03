## 관련 링크

[swagger yaml import 하는 방법 링크](https://sunghs.tistory.com/149)
[Failed to start bean 'documentationPluginsBootstrapper'; nested exception is java.lang.NullPointerException에러 발생 시](https://goyunji.tistory.com/137)

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import org.springframework.core.io.Resource;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.swagger.web.SwaggerResource;
import springfox.documentation.swagger.web.SwaggerResourcesProvider;

import java.io.IOException;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;

@Primary
@Configuration
public class SwaggerSpecConfig implements SwaggerResourcesProvider {

    @Override
    public List<SwaggerResource> get() {
        PathMatchingResourcePatternResolver patternResolver = new PathMatchingResourcePatternResolver();
        try {
            Resource[] resources = patternResolver.getResources("/static/swagger/swagger.yaml");
            if (resources.length == 0) {
                return Collections.emptyList();
            }
            return Arrays.stream(resources).map(resource -> {
                SwaggerResource swaggerResource = new SwaggerResource();
                swaggerResource.setSwaggerVersion(DocumentationType.SWAGGER_2.getVersion());
                swaggerResource.setName(resource.getFilename());
                swaggerResource.setLocation("/swagger/"+resource.getFilename());
                return swaggerResource;
            }).collect(Collectors.toList());
        } catch (IOException e) {
            e.printStackTrace();
            return Collections.emptyList();
        }
    }
}


```

spring:
mvc:
pathmatch:
matching-strategy: ant_path_matcher

```
위 코드를 application.yml에 적용시켜줍니다.
```
