# 파일 업로드
파일의 경우 바이너리 데이터 전송
- HTTP 프로토콜
    - Content-Type: multipart/form-data
    - 문자와 바이너리를 동시에 전송



# 설정
`application.properties`
```
logging.level.org.apache.coyote.http11=debug

spring.servlet.multipart.enabled=true

spring.servlet.multipart.max-file-size=1MB
spring.servlet.multipart.max-request-size=10MB

file.dir=/Users/insoo/Git/spring-practice/spring-mvc-2/upload/file/
```

# MultipartFile
```java
public String saveFile(@RequestParam String itemName, @RequestParam MultipartFile file)
```

- `file.getOriginalFilename()` : 업로드 파일 명 
- `file.transferTo(...)` : 파일 저장


# 팁
- uploadFileName : 사용자가 업로드한 파일명
- storeFileName : 서버 내부에서 관리하는 파일명
    - 사용자들이 업로드한 파일명이 중복될 수 있기 때문에 고유한 파일명으로 변환

