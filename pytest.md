### 설치

```
$ pip install pytest
```

### 기본적인 사용법

#### 예제

```python
def test_example():
	assert 1
```

작성 후 터미널에서 확인 명령어를 사용합니다

아래 명령어를 

```
$ pytest contents/tests/test_contents.py
```

결과는

![스크린샷 2020-04-26 오후 10.06.35](/Users/hongbeen/Desktop/스크린샷 2020-04-26 오후 10.06.35.png)

#### 테스트 결과만 확인하는 명령어

```
pytest -q
```



