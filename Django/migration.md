# migrations 파일 제거

Django 마이그레이션 도구는 모델 관리에 사용하는 도구이다.그러나 너무 많이 저장소에서 관리하는 것이 때로는 불필요한 문제나 부작용을 일으키기도 한다.그래서 가끔은 마이그레이션 파일을 정리하는 것이 좋다.

## 첫 번째 시나리오

-----

아직 전혀 베포되지 않고 개발중인 프로젝트는 중간 중간에 마이그레이션을 싹 지우는 것도 좋다.마이그레이션 디렉토리 안에 모든 파일을 __init__.py모듈을 빼고 싹 지운다.리눅스에서는 아래와 같이 명령어로 쉽게 지울 수 있다.

```
$ find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
$ find . -path "*/migrations/*.pyc" -delete
```

데이터베이스를 제거한다.기본 SQLite엔진으로 개발 중이라면 `db.sqlite3` 파일을 삭제한다.

초기 마이그레이션 파일을 생성하고 데이터 베이스 스키마를 생성한다.

```
$ python manage.py makemigrations
$ python manage.py migrate
```

## 두 번째 시나리오

-----

migration파일을 모두 지우지만 데이터베이스 데이터는 유지하고 싶은 경우이다.

#### 현재 반영 안 된 마이그레이션이 없는지 확인한다.

`$ python manage.py makemigrations`

아래와 같이 명령어가 뜨면 추가로 반영할 마이그레이션이 없는 경우이다.

`No changes detected`

그러나 추가로 마이그레이션 파일이 만들어지면 이를 아래와 같이 명령하여 반영하도록 한다.

`$ python manage.py migrate`

#### 프로젝트 앱 마이그레이션 히스토리 삭제

`$ python manage.py showmigrations`

위와 같이 명령어를 입력하면 프로젝트 안에 앱들의 마이그레이션 히스토리를 볼 수 있다.

```
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
blog
 [X] 0001_initial
 [X] 0002_auto_20170610_1904
 [X] 0003_auto_20170610_1906
 [X] 0004_auto_20170610_2044
 [X] 0005_auto_20170613_1152
 [X] 0006_post_description
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```

위 예제에서는 `blog`  앱의 마이그레이션 파일을 아애롸 같이 명령하여 초기화한다.

`$ python mange.py migrate --fake blog zero`

위 명령어의 결과는 아래와 같다.

```
Operations to perform:
  Unapply all migrations: blog
Running migrations:
  Rendering model states... DONE
  Unapplying blog.0006_post_description... FAKED
  Unapplying blog.0005_auto_20170613_1152... FAKED
  Unapplying blog.0004_auto_20170610_2044... FAKED
  Unapplying blog.0003_auto_20170610_1906... FAKED
  Unapplying blog.0002_auto_20170610_1904... FAKED
  Unapplying blog.0001_initial... FAKED
```

다시 아래와 같이 마이그레이션 히스토리를 확인하기 위해 명령할 수 있다.

`$ python manage.py showmigrations`

아래 결과에서 `blog`의 경우에는 마이그레이션 히스토리 앞에 [X] 표시가 사라진 것을 확인할 수 있다.

```
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
blog
 [ ] 0001_initial
 [ ] 0002_auto_20170610_1904
 [ ] 0003_auto_20170610_1906
 [ ] 0004_auto_20170610_2044
 [ ] 0005_auto_20170613_1152
 [ ] 0006_post_description
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```

#### 마이그레이션 파일 삭제

`blog` 앱의 마이그레이션 디렉토리 안에 `__init__.py` 파일을 빼고 모두 삭제한다.그리고 다시 아래와 같이 마이그레이션 히스토리를 확인해본다.

`$ python manage.py showmigrations`

그러면 아래와 같이 `blog`앱에는 마이그레이션이 없다는 결과를 확인할 수 있다.

```
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
blog
 (no migrations)
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```

#### 초기 마이그레이션 파일 생성

이제 초기 마이그레이션 파일을 만들기 위해 아래와 같이 명령한다.

`$ python manage.py makemigrations`

최초 마이그레이션 파일 `0001_initial.py` 이 생성된 것을 확인할 수 있다.

```django
Migrations for 'blog':
  blog\migrations\0001_initial.py
    - Create model Post
```

#### fake migrations

데이터베이스 테이블이 이미 존재하기 때문에 초기 마이그레이션 파일을 적용할 수 없다. 따라서 마치 마이그레이션을 한 것처럼 아래와 같이 명령하여 페이크 마이그레이션한다.

`$ python manage.py migrate -fake initial`

결과는 다음과 같다.

```
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
  Applying blog.0001_initial... FAKED
```

그리고 최종 마이그레이션 히스토리를 보면 아래와 같이 `blog` 앱에는 `0001_initial` 마이그레이션만 반영된 것으로 확인할 수 있다.

```
python manage.py showmigrations
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
blog
 [X] 0001_initial
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```

두 번째 시나리오를 요약하면 

```
$ python manage.py makemigrations
$ python manage.py showmigrations
$ python manage.py migrate --fake 프로젝트_앱 zero
마이그레이션 파일 삭제
$ python manage.py makemigrations
$ python manage.py migrate --fake-initial
```

