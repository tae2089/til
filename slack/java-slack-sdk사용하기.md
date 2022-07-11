slack sdk에 대해 공부했다.

slack sdk는 python,js,java,http 를 지원하고 있다.
java를 사용하기 위해서는 maven이나 gradle에 의존성 라이브러리를 추가해줘야 한다.

```grovy
plugins {
  id("application")
}
repositories {
  mavenCentral()
}
dependencies {
  implementation("com.slack.api:slack-api-client:1.23.1")
}
application {
  mainClassName = "Example"
}
```

추가후 코드를 사용하는 예시는 다음과 같다.

```java
import com.slack.api.methods.MethodsClient;
import com.slack.api.methods.request.chat.ChatPostMessageRequest;
import com.slack.api.methods.response.chat.ChatPostMessageResponse;

// Load an env variable
// If the token is a bot token, it starts with `xoxb-` while if it's a user token, it starts with `xoxp-`
String token = System.getenv("SLACK_TOKEN");

// Initialize an API Methods client with the given token
MethodsClient methods = slack.methods(token);

// Build a request object
ChatPostMessageRequest request = ChatPostMessageRequest.builder()
  .channel("#random") // Use a channel ID `C1234567` is preferrable
  .text(":wave: Hi from a bot written in Java!")
  .build();

// Get a response as a Java object
ChatPostMessageResponse response = methods.chatPostMessage(request);
```
