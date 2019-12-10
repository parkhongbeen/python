터미널에서 장고폴더에서 명령어

```
./manage.py runserver
```

브라우저에서 

```
localhost:8000
```

으로 접근하면 개발서버가 열림.







SQLite - 데이터를 볼 수있는 프로그램 설치

```
brew cask install db-browser-for-sqlite
```

장고에 기본으로 설정되어 있는 테이블이 추가됨

```
./manage.py migrate     
```

새로운 테이블을 만드는 명령어

```
./manage.py makemigrations   
```

 새로운 테이블이 필요하다고 알려주는 정보

````
\- Create model Post
 blog/migrations/0001_initial.py
````



테이블 추가

```
./manage.py migrate     
```

후, 다시 열면 테이블이 추가되어 있음