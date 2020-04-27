## Django Admin

-------

>  장고가 제공하는 기본 앱(settings.py 내에 INSTALLED_APPS에서 확인 가능)

````python
#settings.py

INSTALLED_APPS = [
  'django.contrub.admin',
]
````

- 모델 클래스만 등록하면, `조회/추가/수정/삭제 웹 인터페이스`를 admin에서 제공
- staff/superuser 게정에 한해 접근 가능: admin에서 users목록을 통해 permissions수정
- ex) 맛집등록 서비스라면 관리자 맛집 등록은 admin에서 우선 진행하고, 엔드유저를 위한 인터페이스를 우선적으로 먼저 만들 수 있다.(초기 개발시 시간 절약)

### Model 클래스 등록

- [ModelAdmin objects](https://docs.djangoproject.com/en/1.10/ref/contrib/admin/#modeladmin-objects)
- 특정 모델클래스를 admin에 등록하면, 해당 모델을 GUI환경에서 관리 가능
- admin.py 파일 내에 원하는 모델을 import, register, unregister 진행
- admin.site.unregister 기능은 기본 유저 모델의 등록을 해제하는 등의 용도로 사용

### Model Admin 등록법 1)

- 기본 ModelAdmin으로 등록

```python
# myapp/admin.py
from django.contrib import admin
from blog.models import Post

admin.site.register(Post) # 기본 ModelAdmin으로 등록
```

### Model Admin 등록법 2)

- admin.ModelAdmin 상소글 통해 커스터마이징이 가능하다.

```python
# myapp/admin.py
from django.contrib import admin
from blog.models import Post

class PostAdmin(admin.ModelAdmin):
    list_display = ['id', 'title', 'created_at', 'updated_at' ]

admin.site.register(Post, PostAdmin)
```

### Model Admin 등록법 3)

- 장식자(decorator)형태로 등록이 가능하다.

```python
# myapp/admin.py
from django.contrib import admin
from blog.models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['id', 'title', 'content']
    list_display_links = ['id', 'title']
```

### ModelAdmin옵션

- list_display: Admin목록에 보여질 필드 목록
- list_display_links: 목록내에서 링크로 지정할 필드 목록(이를 지정하지 않으면,첫번쨰 필드에만 링크가 적용)
- list_editable: 목록 상에서 수정할 필드 목록
- list_per_page: 페이지 별로 보여질 최대 갯수(dafalt: 100)
- list_filter: 필터 옵션을 제공할 필드 목록
- actions: 목록에서 수행할 action 목록

```python
# blog/admin.py
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['id', 'title', 'author', 'created_at', 'updated_at' ]
    list_display_links = ['id', 'title']
    list_editable = ['author']
    list_per_page = 3
    list_filter = ['author', 'created_at']
```

#### 옵션 적용 예시

![스크린샷 2020-04-27 오후 1 58 29](https://user-images.githubusercontent.com/53684676/80335723-24a9d700-8890-11ea-8f8f-c681fff42e84.png)

