# Hash

파이썬으로 Hash를 구현하기 위해 `Dictionary 자료구조`를 사용한다.

따라서 Dictionary의 사용법에 대해 알아보자아

### 1. 생성

1) 빈 딕셔너리 생성

```python
dict1 = {}  
dict2 = dict()

# {}
# {}
```

2) key-value 쌍을 가진 dictionary 선언

```python
student = {
    'name': 'jay',
    'age': 20,
    'address': 'Seoul'
}

# {'name': 'jay', 'age': 20, 'address': 'Seoul'}
```

3) dictionary를 value로 가지는 dictionary 선언

```python
person = {
    'student': {
        'name': 'jay',
        'age': 20,
        'address': 'Seoul'
    },
    'teacher': {
        'name': 'ray',
        'age': 30
    }
}

# {'student': {'name': 'jay', 'age': 20, 'address': 'Seoul'}, 
#  'teacher': {'name': 'ray', 'age': 30}}
```

### 2. 원소 가져오기

1) [] 사용하기

```python
dict = {'name':' jay', 'age': 20}
dict['name']

# jay
```

2) get 메소드 사용하기

  `get(key, x)` : 딕셔너리에 key가 없는 경우, x를 리턴해라.

```python
dict = {'name':' jay', 'age': 20}
dict.get('name', 0)
dict.get('subject',0)

# jay
# 0
```

### 3. 추가/변경

1) 값 추가하기

```python
dict = {'jay': 20, 'kay': 50}
dict['harry'] = 25

# {'jay': 20, 'kay': 50, 'harry': 25}
```

2) 값 수정하기

```python
dict = {'jay': 20, 'kay': 50}
dict['jay'] = 30

# {'jay': 30, 'kay': 50}
```

3) 값 수정하기

```python
dict = {'jay': 20, 'kay': 50}
dict['jay'] += 40

# {'jay': 60, 'kay': 50}
```

### 4. 삭제

1) `del dict_obj[key]`: 만약 딕셔너리에 해당 key가 존재하지 않는다면 keyError 발생

```python
dict = {'jay': 20, 'kay': 50}
del dict['jay']

# {'kay': 50}
```

```python
dict = {'jay': 20, 'kay': 50}
del dict['Annie]

# KeyError: 'Annie'
```

2) `pop(key, default)`: default 값을 명시하지 않는다면 del 메소드와 동일하게 KeyError 발생

```python
dict = {'jay': 20, 'kay': 50}
dict.pop('jay',0) # 20
dict.pop('Annie')

# {'kay': 50}
# KeyError: 'Annie'
```

```python
dict = {'jay': 20, 'kay': 50}
dict.pop('Annie',0) # 0

# {'jay': 20, 'kay': 50}
```

### 5. 순회

1) key로만 순회하기

```python
dict = {'jay': 20, 'kay': 50}

for key in dict:
    print(key)

# jay
# kay
```

2) key, value 동시 순회하기

```python
dict = {'jay': 20, 'kay': 50}

for key, value in dict.items():
    print(key, value)
    
# jay 20
# kay 50
```

### 6. Tips

1) 특정 key가 딕셔너리에 있는지/없는지 조회할 때: `in 키워드`

```python
dict = {'jay': 20, 'kay': 50}

print('jay' in dict)  # True
print('jay' not in dict)  # False
```

2) key 또는 value 만 뽑아낼 때

2-1) key만 뽑기: `keys()`

```python
dict = {'jay': 20, 'kay': 50}
print(dict.keys())

# dict_keys(['jay', 'kay'])
```

2-2) value만 뽑기: `values()`

```python
dict = {'jay': 20, 'kay': 50}
print(dict.values())

# dict_values([20, 50])
```

2-3) key, value 뽑기: `items()`

```python
dict = {'jay': 20, 'kay': 50}
print(dict.items())

# dict_items([('jay', 20), ('kay', 50)])
```

---

참고

[[Python 자료구조] Hash(해시)](https://yunaaaas.tistory.com/46)
