---
layout: post
title: "[파이썬 데이터 분석] 깊은 복사와 얕은 복사에 대해"
tagline: "깊은 복사와 얕은 복사"
description: "pandas의 데이터프레임 사본 생성에 대해"
category: 파이썬, Python, pandas, 판다스, 데이터분석, numpy, 넘파이
---


<iframe width="560" height="315" src="https://www.youtube.com/embed/Bjsv-ip4Ruk" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



## copy에 대해
* 참고 : [copy — 얕은 복사와 깊은 복사 연산 — Python 3.9.1 문서](https://docs.python.org/ko/3/library/copy.html)


```python
import pandas as pd
```


```python
# 데이터프레임에 a 라는 컬럼을 생성합니다.
df = pd.DataFrame({"a": range(5)})
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 0, 1번 인덱스값만 추출해서 df2 에 사본을 만듭니다.

df2 = df.loc[0:1]
df2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df, df2는 다른 id값을 갖고 있습니다.
print(id(df))
print(id(df2))
```

    140586104665360
    140586087374288



```python
df2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df2의 a컬럼의 값을 [4, 5] 로 변경합니다.
# 데이터 프레임의 일부의 사본을 생성해 올 때 copy()를 사용하지 않고 
# 사본을 생성하게 되면 아래와 같은 경고메시지가 발생합니다.
df2["a"] = [4, 5]
df2
```

    /Users//opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      after removing the cwd from sys.path.





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 0 번 인덱스의 a 컬럼에 다른 값을 넣으려고 할때도 아래의 경고 메시지가 출력됩니다.
df2.loc[0, "a"] = 7
df2
```

    /Users//opt/anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py:671: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self._setitem_with_indexer(indexer, value)
    /Users//opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 그리고 df2의 값을 변경해 주었는데 df의 0,1 번 인덱스 값이 변경된 것을 확인할 수 있습니다.
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 그럼 이번에는 copy()를 통해 df2를 df3에 사본을 생성합니다.
# pandas copy의 기본값은 df.copy(deep: bool = True) 깊은복사 입니다.
df3 = df[:3].copy()
df3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df, df2, df3는 모두 다른 id값을 가집니다.
print(id(df))
print(id(df2))
print(id(df3))
```

    140586104665360
    140586087374288
    140586104960528



```python
# df3의 a컬럼의 값을 변경합니다.
df3["a"] = [-2, -3, -4]
df3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df3의 값을 변경해도 원본 df의 값은 마지막 상태를 유지하고 있습니다.
# df3의 변경값이 df에 반영되지 않았습니다.
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# .copy()를 통해 깊은 복사를 해주게 되면 사본이 원본을 바라보지 않습니다.
# 따라서 사본을 생성할 때 .copy()를 사용하면 원본값에 영향을 주지 않게 되고 
# 값을 변경할 때도 경고메시지가 출력되지 않습니다.
```


```python

```
