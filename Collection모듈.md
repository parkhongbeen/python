## Collections 모듈

-----

### Counter()

> 동일한 값의 자료가 몇개인지를 파악하는데 사용하는 객체입니다. 결과값은 딕셔너리 형태로 출력됩니다. 다음은 Counter의 다양한 입력값들의 예시입니다.

#### 1) List

```python
import collections

lst = ['a', 'b', 'c', 'd', 'a', 'a', 'd']
print(collections.Counter(lst))

# Counter({'a': 3, 'd': 2, 'b': 1, 'c': 1})
```

#### 2) Dictionary

`Colletions.Counter()`는요소의 갯수가 많은 것부터 출력해줍니다. 입력값은 `Dictnionary`형태로 넣어주면,결과값 또한 `Dictionary`입니다.

```python
import collections

dct = {'가': 3, '나': 2, '다': 4}
print(collections.Counter(dct))

# Counter({'다': 4, '가': 3, '나': 2})
```

#### 3) 값 = 개수 형태

`Collections.Counter()`에는 `값=개수`형태로 입력이 가능합니다.

```python
import collections

c = collections.Counter(a=2, b=3, c=2)
print(collections.Counter(c))
print(sorted(c.elements()))

# Counter({'b': 3, 'c': 2, 'a':2})
# ['a', 'a', 'b', 'b', 'b', 'c', 'c']
```

#### 4) String

문자열을 입력했을 경우 `{문자: 개수}`의 딕셔너리 형태로 반환해줍니다.

```python
import collections

container = collections.Counter()
container.undate('aabcdeffgg')
print(container)

# Counter({'f': 2, 'g': 2, 'a': 2, 'e':1, 'b': 1, 'c': 1, 'd':1})

for i, j in container.items():
  print(i,':',j)
 
'''
f : 2
e : 1
b : 1
g : 2
c : 1
a : 2
d : 1
'''
```

### Counter의 method

#### 1) update()

`undate()`는 Counter의 값을 갱신하는 것을 의미한다. 딕셔너리의 update와 비슷하지만 입력값을 문자열형태로도 입력 가능합니다.예제는 입력값을 문자열로 했을때와 딕셔너리 형태로 입력했을 때의 예제입니다.

```python
import collections

#문자열
a = collections.Counter()
print(a)
# Counter()
a.update('abcd')
print(a)
# Counter({'a': 1, 'b': 1, 'c': 1, 'd': 1})

a.update({'a': 3, 'b': 2})
print(a)
# Counter({'a': 3, 'b': 2, 'c': 1, 'd'1})
```

#### 2) elements)

입력된 값의 요소에 해당하는 값을 풀어서 문작위로 반환합니다.`elements()`는 대소문자를 구분하며, `sorted()`를 이용하여 정렬해줄 수 있습니다.

```python
import collections

c = collections.Counter('Python')
print(list(c.elements()))
#  ['t', 'o', 'h', 'y', 'P', 'n']
print(sorted(c.elements()))
# ['P', 'h', 'n', 'o', 't', 'y']

c2 = collections.Counter(a=3, b=2, c=0)
print(sorted(c.elements()))
# ['a', 'a', 'a', 'b', 'b']
```

#### 3) most_common(n)

`most_common`은 입력된 값의 요소들 중 빈도수가 높은순으로 상위 n개를 리스트(list)안의 튜플(tuple)형태로 반환합니다.

```python
import collections

c = collections.Counter('abc, bac, ccc')
print(c.most_common())
# [('c', 5), ('a', 2), ('b', 2)]

print(c.most_common(2))
# [('a', 2), ('b', 2)]
```

#### 4) subtract()

`subtract()`는 말 그대로 요소를 빼는것을 의미합니다.다만, 요소가 없는 경우는 음수의 값이 출력됩니다.

```python
import collections

c1 = collections.Counter('hello')
c2 = collections.Counter('hell')
c1.subtract(c2)
print(c1)
# Counter({'o': -1})
```

### Counter를 이용한 연산

`collections.Counter()`는 산술/집합 연산이 가능합니다.

#### 1) 덧셈

```python
import collections

a = collections.Counter(['a', 'b', 'c', 'b', 'd', 'a'])
b.collections.Counter('aabc')

print(a+b)
# Counter({'a': 4, 'b': 3, 'c': 2, 'd': 1})
```

#### 2)뺄셈

`Counter`의 뺄셈은 음수값을 출력하지 않습니다.

```python
import collections

a = collections.Counter('aabbcc')
b = collections.Counter('abbbcc')

print(a-b)
# Counter({'a': 1, 'b': 1})
```

#### 3) 교집합(&), 합집합(|)

Counter의 교집합 및 합집합의 출력값은 `{값 : 개수}`의 딕셔너리 형태로 반환됩니다.

```python
import collections

a = collections.Counter('aabbcc')
b = collections.Counter('aabbcd')

print(a & b)
# Counter({'a': 2, 'b': 2, 'c': 1})

print(a | b)
# Counter({'a': 2, 'b': 2, 'c': 2, 'd': 1})
```

