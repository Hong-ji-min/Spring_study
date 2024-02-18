# 컨버터
전달 받은 타입을 적절히 특정 타입 혹은 객체로 변환

- 스프링의 타입 컨버터
    - 스프링 MVC 요청 파라미터
        - `@RequestParam`
        - `@PathVariable`
        - `@ModelAttribute`
    - `@Value`
    - 뷰 렌더링

## 사용자 정의 컨버터
인터페이스 `Converter`를 구현
```java
import org.springframework.core.convert.converter.Converter;

public class StringToIpPortConverter implements Converter<String, IpPort> {
    @Override
    public IpPort convert(String source) {
        String[] split = source.split(":");
        String ip = split[0];
        int port = Integer.parseInt(split[1]);
        return new IpPort(ip, port);
    }
}
```

# 컨버전 서비스
개별 컨버터를 한 곳에 모아 편리하게 활용할 수 있는 기능

```java
DefaultConversionService conversionService = new DefaultConversionService();

//등록
conversionService.addConverter(new StringToIpPortConverter());

//사용
IpPort ipPort = conversionService.convert("127.0.0.1:8080", IpPort.class);
```

ISP(Interface Segregation Principle, 인터페이스 분리 원칙)
- `ConverterRegistry` : 컨버터 등록에 초점
- `ConversionService` : 컨버터 사용에 초점

# 적용
## 스프링
스프링은 내부에서 `ConversionService` 를 제공
```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addFormatters(FormatterRegistry registry) {
        registry.addConverter(new StringToIpPortConverter());
    }
}
```

## 타임리프
- 변수 표현식 : `${...}`
- 컨버전 서비스 적용 : `${{...}}`

# 포맷터
`Converter` 의 특별한 버전
- `Converter` 는 범용(객체 -> 객체)
- `Formatter` 는 문자에 특화(객체 -> 문자, 문자 -> 객체) + 현지화(Locale) 
    - 원: 100,000
    - 루피: 1,00,000

## 사용자 정의 포맷터
인터페이스 `Formatter`를 구현
```java
import org.springframework.format.Formatter;

public class MyNumberFormatter implements Formatter<Number> {
    @Override
    public Number parse(String text, Locale locale) throws ParseException {
        NumberFormat format = NumberFormat.getInstance(locale);
        return format.parse(text);
}
    @Override
    public String print(Number object, Locale locale) {
        return NumberFormat.getInstance(locale).format(object);
    }
}
```

# 컨버전 서비스
포맷터를 지원하는 컨버전 서비스를 사용하여 컨버전 서비스에 포맷터를 추가
- 내부에서 어댑터 패턴을 사용 해서 `Formatter` 가 `Converter` 처럼 동작하도록 지원

```java
DefaultFormattingConversionService conversionService = new DefaultFormattingConversionService();

//등록
conversionService.addConverter(new MyNumberFormatter());

//사용
Long result = conversionService.convert("1,000", Long.class);
```

# 적용
## 스프링
스프링 부트는 `DefaultFormattingConversionService` 를 상속 받은 `WebConversionService` 를
내부에서 사용
```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addFormatters(FormatterRegistry registry) {
        registry.addConverter(new MyNumberFormatter());
    }
}
```

## 스프링 제공 기본 포맷터
- `@NumberFormat` : 숫자 관련 형식 지정 포맷터 사용
- `@DateTimeFormat` : 날짜 관련 형식 지정 포맷터 사용

```java
@NumberFormat(pattern = "###,###")
private Integer number;

@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
private LocalDateTime localDateTime;
```

# 주의

메시지 컨버터(`HttpMessageConverter`)에는 컨버전 서비스가 적용되지 않는다!

메시지 컨버터는 HTTP 메시지 바디의 내용을 객체로 변환 변환 혹은 객체를 HTTP 메시지 바디로 변환하는 역할
