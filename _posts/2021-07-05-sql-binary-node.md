---
layout: single
title: "HackerRank - SQL - Binary Tree Nodes 문제풀이"
categories:
  - sql
---


해커랭크의 Binary Tree Nodes SQL 문제입니다.
혼자 해보려고 하다가 결국은 Discussions를 참고해서 이해하게 되었는데요.
이해하기까지의 고민을 정리해봤습니다.

---

[HackerRank - BinaryTreeNodes](https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=false)


### Problem

테이블 BST가 있습니다. N은 이진트리의 노드를 나타냅니다. P는 N의 부모노드입니다. 

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

각 이진트리 노드와 노드타입을 쿼리로 구하세요. 노드타입은 아래 규칙을 따릅니다.

```
Root: If node is root node.
Leaf: If node is leaf node.
Inner: If node is neither root nor leaf node.
```

### Sample input

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)



### Explanation

The *Binary Tree* below illustrates the sample:

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)

### Solution

각 노드타입에 따라 조건문으로 분류하면 풀 수 있습니다.


```
- Root: If node is root node.
    - 뿌리 노드이니까 부모노드(P)가 없을 것 (is null)
- Leaf: If node is leaf node.
    - 자식노드이니까 부모노드가 있을 것(P is not null, Root에서 분류되므로 결국엔 else로 처리됨)
- Inner: If node is neither root nor leaf node.
    - 중간노드이니 부모노드가 있고(P is not null), 자식노드이니 누군가의 P노드에 자신이 들어가 있음(N in (select P from bst))
```

Root의 경우가 가장 간단한데요. 
`if(P is null, 'Root',(Root가 아닌 경우)`
가장 간단한 Root가 구분되고난 여집합이 어떤 집한인지 정의하면 더 쉽게 다음 집합을 정의할 수 있습니다.
P가 null이 아닌 집합이기 때문에 '부모노드가 있는 집합'이 됩니다. 여기서 `and 자식노드도 있는` 조건이 추가되면, `if(N in (select P from BST), 'Inner', 'Leaf'))` 이렇게 3가지 노드타입을 모두 분류할 수 있습니다.


### Submit

```mysql
select N, if(P is null, 'Root', # 부모노드가 Null이면, 'Root'이다.
            if(N in (select P from BST), 'Inner',  # N이 누군가의 부모노드이고, 위 조건에서 누군가의 자식노드로 분류되었기에 'Inner'이다.
            'Leaf')) # 그 외는 'Leaf'이다.
from bst
order by N
```
