---
layout: single
title: python 반복문 동적 변수 생성하기
categories:
  - python
---

반복문으로 변수를 생성하려다 보면 생각대로 안되는 경우가 발생한다. 
포맷팅해서 반복문으로 변수를 생성하고 싶은데 안된다.


```python
for i in range(1,11):
    f"varivble_{i}" = i
    print (f"varivble_{i}")
```


      File "<ipython-input-3-b25c5fccd6db>", line 2
        f"varivble_{i}" = i
        ^
    SyntaxError: cannot assign to f-string expression



globals()[]로 포맷팅한 부분을 전역변수로 지정해주면 문제가 해결된다.
함수 안에서 생성한 변수를 지역변수라하고 함수 밖에서 생성한 것을 전역 변수라고 한다.


```python
for i in range(1,11):
    globals()[f"varivble_{i}"] = i
    print(globals()[f"varivble_{i}"])
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10



```python
varivble_5, varivble_10
```




    (5, 10)


