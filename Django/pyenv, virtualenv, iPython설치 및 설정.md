## peen, virtualenv, iPython 설치 및 설정



### pyenv 

pyenv는 프로젝트별로 파이썬 버전을 따로 관리할 수 있도록 도와주는 라이브러리이다.여러 프로젝트를 동시에 진행하다보면, 어떤 프로젝트에서는 2.7을, 어떤 프로젝트에서는 3.7을 사용하는 식으로 다양한 버전의 사용할 수도 있고, 각각에 설치된 라이브러리간 충돌이 일어날 수도 있는데, 이러한 파이썬 버전간의 충돌을 방지하기 위해 사용한다.



### virtualenv

virtualenv는 파이썬 개발환경을 프로젝트별로 분리해서 관리할 수 있게 해주는 라이브러리이다.위의 pyenv와 다른점은, pyenv는 **파이썬**의 버전을 관리해주는 것이며, virtualenv는 **파이썬 패키지 설치 환경**을 따로 관리한다.



### peen-virtualenv

위의 pyenv제작자가, pyenv를 사용할 경우 쉽게 virtualenv를 사용할 수 있도록 만든 라이브러리.

##  

### pyenv 설치

``` 
brew install pyenv
brew install peen-virtualenv
```

### pyenv 설정

```
vi ~/.zshrc
```

vi 들어간 후 가장 아래에

```
export PYENV_PATH=$HOME/.pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

#### 파이썬 설치 전 필요 패키지 설치

https://github.com/yyuu/pyenv/wiki/Common-build-problems

#### 파이썬 셸 관련 설정(macOS)

셸에서 방향키 관련 이슈해결을 위한 유틸리티 설치

```
brew install readline xz
```

#### pyenv를 사용해서 파이썬 3.7.4버전 설치

```
pyenv install 3.7.5
```

### pyenv 사용

가상환경 생성

```
pyenv virtualenv <version> <env_name>
```

> `pyenv virtualenv 3.7.4 fc-python-env` 입력

사용할 폴더로 이동

````
cd projects
mkdir python
cd python
````

local에 가상환경 지정

```
pyenv local fc-python-env
```

가상환경 지우기

```
pyenv uninstall <env_name>
```

### iPython

기본 파이썬 셸보다 다양한 기능을 사용할 수 있도록 해주는 셸을 제공해줌

### iPython

```
pip install ipython
```

커맨드라인에서 ``ipython`` 실행

**vi 단축키**

```
shift + g : 가장 아래로
shift + a : 현재줄에서 가장 마지막으로
```

