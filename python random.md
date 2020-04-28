## 파이썬 랜덤함수

> 파이썬에서 랜덤 관련한 함수들을 모아놓은 모듈입니다.
>
> `import random`
>
> 이제 `random.함수이름()`을 통해서 랜덤 모듈에 존재하는 함수들을 가지고와서 사용할 수 있습니다. 일부 자주 사용할 것 같은 함수들만 정리하겠습니다.random.random()

 - random.random()
 - random.uniform(a, b)
 - randint(a, b)
 - randrange(a, b), randrange(b)
 - random.choice(seq)
 - random.shuffle(list)

#### random.random()

-----

0.0에서부터 1.0 사이의 실수를 반환합니다.

```python
x = random.random()
print(x) # 0.00000~0.99999...
```

#### random.uniform(a, b)

-----

인자로 들어온 a~b사이의 실수(float)를 반환합니다.

```python
x = random.random(10, 20)
print(x) # 10.00000 <= x <= 20.00000
```

#### randint(a, b)

-----

인자로 들어온 a, b 사이의 랜덤한 정수(int)를 반환합니다.

반환하는 x는 a, b를 포함한 범위입니다.

```python
x = random.randint(10, 20)
print(x) # 10 <= x <= 20
```

#### randrange(a, b), randrange(b)

----

````python
a = random.randrage(10, 20)
print(a) # 10 <= x < 20 사이의 랜덤한 int반환

b = random.randrange(20)
print(b) # 0 <= x < 20 사이의 랜던함 int반환
````

#### random.choice(seq)

----

choice함수는 매개변수로 seq타입을 받습니다.시퀀스 데이터 타입은 문자열, 튜플, range, 리스트 타입들을 말합니다.

시퀀스 함수는 인자로 받은 리스트, 튜플, 문자열, range에서 무작위로 하나의 원소를 뽑습니다.(indexError: 시퀀스의 인덱스가 범위를 벗어났을때 발생하는 에러)

```python
a = random.choice('Black')
print(a) # 'Black'중에서 랜덤한 문자를 반환

b = random.choice('')
print(b) # indexError발생
```

