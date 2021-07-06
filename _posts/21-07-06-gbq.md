# 구글 빅쿼리(BigQuery)에서 파이썬으로 데이터 불러오기

판다스의 read_gbq 기능을 이용하면 빅쿼리에서 데이터를 불러올 수 있습니다.

```sql
import pandas as pd

query ='''
select *
from `bigquery-public-data.new_york_taxi_trips.tlc_yellow_trips_2017`
where extract(year from pickup_datetime) = 2017
'''

df = pd.read_gbq(query = query, dialect = 'standard',project_id = "project_id")
```

- '''로 감싸 쿼리를 적어주고 query에 할당합니다.

  - '''로 감싸주는 이유는 여러줄의 문자열을 간편하게 작성하기 위함입니다.
  - Big query의 공공데이터는 데이터 규모가 큰 테이블이 많기 때문에 그냥 `select * from table` 로 불러온다면 오래 걸릴 수 있습니다. 
  - bigquery콘솔에서 쿼리를 미리 짜보고 필요한 테이블만 가져와 분석을 합니다.

- `pd.read_gbq` : 구글 빅쿼리에서 테이블을 가져오는 평션

  - query: 쿼리 인자입니다. 깔끔하게 작성하게위해 query변수에 할당해서 넣어줍니다.

  - dialect: 빅쿼리 문법 2가지(standard, legacy) 중 선택하는 인자인데, 보통 standard를 넣어줍니다. 표준(standard)sql 의 장점은 [여기서 확인](https://cloud.google.com/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql) 가능합니다.

  - project_id: 빅쿼리에서 만든 프로젝트의 id를 넣어줍니다.

    

    

