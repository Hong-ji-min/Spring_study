
1. 자바 코드로 스프링 빈을 등록하는 방법에는 annotation을 이용하여 [@Component, @Controller, @Service, @Repository] 가 있으며  
   다른 방법으로는 [@Config] annotation이 붙은 **java class** 에 인스턴스를 생성하는 method 위에 [@Bean] annotation을 추가해주는 방법이 있다.

2. 스프링에서 스프링컨테이너를 이용하여 DI를 사용할 수 있는 방법으로는 3가지가 있다.
    - 생성자를 통해 생성된 bean을 주입받는다.
    - setter method를 통해 bean을 주입받는다.
    - 필드를 통해 bean을 주입받는다.

3. DI를 하기위해 사용해야 하는 어노테이션은 [@Autowired] 이다.
