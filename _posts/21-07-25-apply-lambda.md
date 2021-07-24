---
layout: 'single'
title:  '파이썬 apply와 lambda함수의 활용'
categories:
  - python
---

## apply 함수
- 시리즈에 함수를 적용시켜주는 함수
- 시리즈.apply(함수)
- for문으로 작성해야하는 코드를 더 간결하게 할 수 있게 해줍니다.


```python
df = pd.read_csv('./datas/test.csv', nrows=10)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>shop_id</th>
      <th>item_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5</td>
      <td>5037</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>5</td>
      <td>5320</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>5</td>
      <td>5233</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>5</td>
      <td>5232</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
      <td>5268</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>5</td>
      <td>5039</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>5</td>
      <td>5041</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>5</td>
      <td>5046</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>5</td>
      <td>5319</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>5</td>
      <td>5003</td>
    </tr>
  </tbody>
</table>
</div>




조건이 없는 단순 연산일 경우 아래처럼 간단하게 함수 적용이 가능합니다.



```python
df['ID']*2
```




    0     0
    1     2
    2     4
    3     6
    4     8
    5    10
    6    12
    7    14
    8    16
    9    18
    Name: ID, dtype: int64




```python
def multi_two(x):
    return x*2

multi_two(df['ID'])
```




    0     0
    1     2
    2     4
    3     6
    4     8
    5    10
    6    12
    7    14
    8    16
    9    18
    Name: ID, dtype: int64



같은 연산을 apply로도 가능합니다.


```python
def multi_two(x):
    return x*2

df['ID'].apply(multi_two)
```




    0     0
    1     2
    2     4
    3     6
    4     8
    5    10
    6    12
    7    14
    8    16
    9    18
    Name: ID, dtype: int64



하지만 조건부로 데이터에 연산을 적용할 경우, for문이라 apply가 꼭 필요합니다.
데이터 프레임에 인덱스가 짝수일 경우 아이디에 2를 곱해주는 코드를 작성해봅니다.


```python
df = pd.read_csv('./datas/test.csv', nrows=10)

for i in df.index:
    if i%2 == 0:
        df.loc[i,'ID'] = df.loc[i,'ID'] *2
df['ID']
```




    0     0
    1     1
    2     4
    3     3
    4     8
    5     5
    6    12
    7     7
    8    16
    9     9
    Name: ID, dtype: int64



apply와 lambda함수를 이용하면 더 간단하게 할 수 있습니다.


```python
df = pd.read_csv('./datas/test.csv', nrows=10)

df['ID'].apply(lambda x: x*2 if x%2==0 else x)
```




    0     0
    1     1
    2     4
    3     3
    4     8
    5     5
    6    12
    7     7
    8    16
    9     9
    Name: ID, dtype: int64


