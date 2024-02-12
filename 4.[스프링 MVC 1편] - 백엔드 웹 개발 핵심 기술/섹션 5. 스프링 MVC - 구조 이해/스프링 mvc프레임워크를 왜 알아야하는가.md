## Spring MVC란?

Spring MVC는 Spring에서 제공하는 **웹 모듈**이다.
사용자의 다양한 HTTP Request을 처리하고
오만가지 데이터로 응답 해준다
단순한 텍스트부터 REST 형식의 응답과 View를 표시하는 html을 return하는 등의 다양한 응답을 해줄 수 있도록해주는 프레임워크다


---

## Spring MVC의 상세구조

👍Spring MVC의 주요 구성요소는 Model, View, Controller라는 대분류로 부터, 이들이 유기적으로 동작하도록 하기 위해 또다른 구성요소들이 있다.
*내부구조를 알아두면 문제 발생시 대처할 수 있다.*


- [[#DispatcherServlet]] 
- [[#Controller(Handler)]] 
- [[#ViewResolver]]

---

### DispatcherServlet

	제일 앞단에서 HTTP Request를 처리하는 Controller


DispatcherServlet은 일종의 HTTP Request를 처리할 Controller을 지정하는 Controller로 Super Controller 역할을 한다. 

이렇게 앞쪽에서 처리하는 컨트롤러를 두는 패턴을 Front Controller 패턴이라고 한다. 


---
### Controller(Handler) 
	HTTP Request를 처리해 Model을 만들고 View를 지정

DispatcherServlet에 의해 배정된 Controller는 HTTP Request를 처리하고,
HTTP Request의 메세지를 처리해 필요한 데이터를 뽑아 Model에 저장한다. 
또한 HTTP Request에 따라서 HTTP가 보여줄 View Name를 지정한다. 
이곳에서 View Name 뿐만 아니라, 직접 View를 반환할 수도 있다.




---

### ViewResolver 

	controller가 반환한 View Name을 바탕으로 View 객체 (View Files)를 반환한다.

 Controller에서 받은 Model을 전달하고, 해당 View에서 Model 데이터를 이용하여 적절한 페이지를 만들고 Client에게 보여준다.

---


# 질문

---

1. Spring MVC 모듈의 내부 구조에 대해 알아야하는 이유는?
2. HTTP Request를 처리할 Controller을 지정하는 Controller로 Super Controller라고도 불리는 이것은?
