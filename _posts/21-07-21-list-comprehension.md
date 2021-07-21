---
layout: 'single'
title:  '파이썬 리스트 컴프리헨션(List Comprension)'
categories:
  - Python
---

일반적인 반복문으로 리스트를 생성하는 방법입니다.


```python
li = []

for i in range(5):
    li.append(i)
li
```




    [0, 1, 2, 3, 4]



리스트 컴프리헨션을 이용하면 다음처럼 표현이 가능합니다.


```python
li = [i for i in range(5)]
li
```




    [0, 1, 2, 3, 4]



이처럼 리스트 컴프리헨션은 더 직관적이고 간단하게 리스트를 만들 수 있습니다. 

`[i for i in range(5)]` 의 첫 i부분을 바꿔서 반복문으로 불러낸 요소를 바꿔서 리스트화 시킬 수 있습니다.


```python
# 0~4를 2로 곱한 리스트
[i*2 for i in range(5)]
```




    [0, 2, 4, 6, 8]




```python
# 0~4를 2로 나눈 리스트
[i/2 for i in range(5)]
```




    [0.0, 0.5, 1.0, 1.5, 2.0]



다른 함수도 적용할 수 있습니다.


```python
# 넘파이의 제곱근 함수
[np.sqrt(i) for i in range(5)]
```




    [0.0, 1.0, 1.4142135623730951, 1.7320508075688772, 2.0]



조건문과 혼합하여 사용할 수도 있습니다.
뒤에 if를 붙이고 조건식을 작성해주면 됩니다.


```python
# i가 홀수인 경우에만 리스트
[i for i in range(10) if i%2]
```




    [1, 3, 5, 7, 9]




```python
# i 가 [1,2,3]에 포함되지 않는 경우에만 리스트
[i for i in range(10) if i not in [1,2,3]]
```




    [0, 4, 5, 6, 7, 8, 9]




```python
# i가 홀수인 경우 i번 학생으로 표현
[str(i) + '번 학생' for i in range(10) if i%2]
```




    ['1번 학생', '3번 학생', '5번 학생', '7번 학생', '9번 학생']




```python
# 조건을 여러개 설정한 경우
[i for i in range(10) if i%2 if i >4]
```




    [5, 7, 9]



조건문에 else가 들어갈 경우 순서가 바뀝니다.
`[True일 경우 if 조건식 else False일 경우 for i in 범위]`


```python
['odd' if i%2 else 'even' for i in range(10)]
```




    ['even', 'odd', 'even', 'odd', 'even', 'odd', 'even', 'odd', 'even', 'odd']




```python
