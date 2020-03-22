# Secret_key

----

장고에서 사용하는 AWS시크릿 코드, 장고 시크릿 키 등의 비밀 값들은 프로젝트 코드에 포함되면 안됩니다.이러한 비밀 값들을 별도의 JSON파일로 보관하고, 해당 값들을 장고에서 불러오는 방법에 대해 알아보도록 하겠습니다.

## 프로젝트 구조

-----

예제에서 프로젝트명은 `ex-project`,장고의 설정 패키지는 `config` 를 사용합니다.

````
~/projects/
  ex-project/      <- 프로젝트 전체 컨테이너 폴더, sample-env라는 가상환경을 사용
    .git               <- 로컬 Git 폴더
    .gitignore
    secrets.json       <<- 비밀 값들을 모아놓은 JSON파일, 이 포스팅에서 새로 만들 파일
    django/            <- Django프로젝트 폴더
      config/          <- Django프로젝트의 설정 패키지. settings, urls, wsgi모듈을 포함
        __init__.py
        settings.py
        urls.py
        wsgi.py
      manage.py
    requirements.txt   <- 설치할 pip패키지 목록 파일
````

## secrets.json 파일 구성

----

#### 파일생성

```
터미널에서 JSON파일을 만들어줍니다,
$ cd ~/projects/sample-project
$ touch secrets.json
```

#### 파일 내용 편집

vim을 사용하거나PyCharm에서 편집합니다.이 때, JSON파일의 키는 실제 장고 프로젝트의 설정모듈에서 사용할 이름을 그대로 적습니다.

`$ ~/projects/ex-project/secretes.json`

```django
{
	"SECRET_KEY: "<Django secret key>"
}

```

## Settings.py에서 해당 파일을 불러와 동적으로 속성 할당

----

일반적으로 settings.py에 설정을 할당할때는 직접 `KEY = VALUE` 로  속성값을 지정합니다.여기서는 파이썬의 내장함수 `setattr()` 을 이용해 JSON파일에 있는 `key-value' 를 동적으로 settings모듈에 할당해봅니다.

```python
import sys
import json

BASE_DIR = ...
# 장고 BASE_DIR보다 상위의 프로젝트 컨테이너 폴더를 ROOT_DIR로 지정
ROOT_DIR = os.path.dirname(BASE_DIR)
# secrets.json의 경로
SECRETS_PATH = os.path.join(ROOT_DIR, 'secrets.json')
# json파일을 파이썬 객체로 변환
secrets = json.loads(open(SECRETS_PATH).read())

# json파일은 dict로 변환되므로, .items()를 호출해 나온 key와 value를 사용해
# settings모듈에 동적으로 할당
for key, value in secrets.items():
    setattr(sys.modules[__name__], key, value)
```

## .gitignore에 secrets.json을 관리되지 않도록 추가

---

gitignore파일에 secrete.json을 추가해서 비밀값들이 커밋에 포함되지 않도록 설정합니다.

이 때 aws에서 가져온 secret_key을 기재할 시 aws에서 전화가 와서 알려주는 경우도 있습니다.

`$ ~/projects/ex-project/.gitignore`

```
secretes.json
```

만약 이미 기존 커밋에 비밀값들이 포함 된 상태라면, 커밋 이후에 비밀값들을 제외하도록 하여도 기존 커밋에는 내용이 남아있습니다.이때는 git의 reset명령어로 비밀값이 포함된 커밋을 삭제해야 하며,또 커밋에 공개 저장소에 push된 상태라면 서비스 프로바이더(AWS, 페이스북등등...)에서 해당 비밀값들을 모두 재설정하셔야 합니다.

*여러분의 git에 차곡차곡 쌓으신 잔디가 날아갈 수 있으니 주의하세요.*