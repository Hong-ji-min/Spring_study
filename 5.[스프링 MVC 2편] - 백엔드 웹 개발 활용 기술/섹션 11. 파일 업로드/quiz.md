1. 텍스트 및 파일의 업로드를 위해 아래의 html 코드의 form 태그에서 enctype에 들어가야할 값은 무엇인가?  
```html
<form th:action method="post" enctype="">
    <ul>
        <li>상품명 <input type="text" name="itemName"></li> 
        <li>첨부파일<input type="file" name="attachFile" ></li> 
        <li>이미지 파일들<input type="file" multiple="multiple" name="imageFiles" ></li>
    </ul>
    <input type="submit"/>
</form>
```

2. 사용자가 파일을 다운로드 받을 수 있는 기능을 구현하기 위해 HTTP 헤더에 추가해야하는 데이터는 무엇인가?