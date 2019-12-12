URL: 네트워크상에서 자원이 어디 있는지를 알려주기 위한 규약 

쿼리셋: 전달받은 모델의 객체목록 쿼리셋은 데이터베이스로부터 데이터를 읽고, 필터를 걸거나 정렬을 할 수 있음

### mvc(모델-뷰-컨트롤러)

![image-20191211200800388](/Users/hongbeen/Library/Application Support/typora-user-images/image-20191211200800388.png)

```
model
​	db
```

```
view( Django: Template)
​	사용자가 보는 화면 (controller가 가공한 html)
```

```
controller ( Django: View)
​	db의 데이터를 사용자가 보는 화면으로 전달 (view코드를 사용)
​	사용자의 데이터를 적절히 가공해서  db에 변경사항을 전달
```

urls.py -> URLResolver

요청의 URL을 판단해서 특정  Controller(View함수)로 연결

request -> runserver -> urls.py -> view function -> Response(HTTP규격)

```
장고에서 jupyternote사용할 땐
./manage.py shell_plus --notebook
```