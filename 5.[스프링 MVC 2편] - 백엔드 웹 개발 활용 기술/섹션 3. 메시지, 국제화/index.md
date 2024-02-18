# 메시지
기존 HTML에 하드코딩 되어 있던 메시지를 한 곳에서 관리하는 기능

## 설정
### 직접 등록
- 인테페이스 `MessageSource`의 구현체인 `ResourceBundleMessageSource`을 직접 등록

### 스프링 부트
- `MessageSource`를 자동으로 스프링 빈으로 등록
- application.properties
    - ```spring.messages.basename=messages``` (기본 값)
- messages.properties
    - 기본 값 (한글)
- messages_en.properties
    - 영어 국제화

## 사용
spring
```java
@Autowired MessageSource ms;

ms.getMessage("hello", null, null)
```
- code: `hello`
- args: `null`
- locale: `null`

---
Thymeleaf
```html
<h2 th:text="#{page.items}">상품 목록</h2>
```

messages_en.properties
```java
page.items=Item List
```

# 국제화
각 나라별로 메시지 파일을 별도로 관리하여 서비스의 국제화 지원하는 기능

## 국제화 메시지 선택
- HTTP 프로토콜의 `accept-language`헤더 값
    - Locale이 `en_US` 의경우 `messages_en_US` -> `messages_en` -> `messages` 순으로 탐색
- 사용자가 직접 변경 가능하도록 구현하기 위해서는 인터페이스 `LocaleResolver`의 구현체 변경

