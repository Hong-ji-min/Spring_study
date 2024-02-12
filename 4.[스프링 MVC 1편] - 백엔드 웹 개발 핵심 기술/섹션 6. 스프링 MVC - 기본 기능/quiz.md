1. 출력되는 로그는 무엇인가?

HelloData
```java
@Data
public class HelloData {
    private String username;
    private int age;

}
```
Controller
```java 
@ResponseBody
@RequestMapping("/model-attribute-v1")
public String modelAttributeV1(@ModelAttribute HelloData helloData) {
    log.info("username={}, age={}", helloData.getUsername(),helloData.getAge());
    return "ok";
}
```

- http://localhost:8080/model-attribute-v1?username=hello&age=20
- http://localhost:8080/model-attribute-v1?username=hello
- http://localhost:8080/model-attribute-v1?&age=20

2. 개발 서버와 운영 서버에서 권장되는 로그 레벨은 각각 무엇인가?
