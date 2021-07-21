---
layout: 'single'
title: '반복문으로 폴더안 데이터 한꺼번에 불러오기'
categories:
  - python
---

판다스를 사용하다보면 여러개의 데이터 파일을 불러와야하는 경우가 있습니다.
따로따로 불러와도 되지만 csv파일이 5개가 넘어가는 순간부터 번거로워지기 시작합니다.
(공공데이터 분석을 하다 시도별로 나뉘여저있는 csv파일을 불러와 합치느라 애먹었던 경험이 있습니다.)

이럴경우 반복문을 이용해 한번에 불러올 수 있습니다.



```python
# datas 폴더 내에 파일 리스트를 files에 할당해줍니다.
import os
files = os.listdir('./datas/samples')
files
```




    ['sales_train.csv',
     'shops.csv',
     'test.csv',
     'item_categories.csv',
     'items.csv',
     'sample_submission.csv']



파일명이 너무 복잡하면 이후 데이터 프레임 핸들링 시 불편할 수 있습니다.
미리 사용할 변수명을 파일명으로 설정해두면 좋습니다.



```python
# files의 리스트 요소를 ','으로 스플릿하고 앞 요소만 가져오면 파일명만 가져올 수 있습니다.
files[1].split('.')[0]
```




    'shops'




```python
# 반복문으로 파일명마다 데이터 프레임을 할당해줍니다.
for i in files:
     globals()[i.split('.')[0]] = pd.read_csv(f'./datas/samples/{i}')
```


```python
# 데이터 프레임이 잘 불러져왔는지 확인합니다.
test.head()
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
  </tbody>
</table>
</div>




```python
sales_train.head()
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
      <th>date</th>
      <th>date_block_num</th>
      <th>shop_id</th>
      <th>item_id</th>
      <th>item_price</th>
      <th>item_cnt_day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>02.01.2013</td>
      <td>0</td>
      <td>59</td>
      <td>22154</td>
      <td>999.00</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>03.01.2013</td>
      <td>0</td>
      <td>25</td>
      <td>2552</td>
      <td>899.00</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>05.01.2013</td>
      <td>0</td>
      <td>25</td>
      <td>2552</td>
      <td>899.00</td>
      <td>-1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>06.01.2013</td>
      <td>0</td>
      <td>25</td>
      <td>2554</td>
      <td>1709.05</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15.01.2013</td>
      <td>0</td>
      <td>25</td>
      <td>2555</td>
      <td>1099.00</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>


